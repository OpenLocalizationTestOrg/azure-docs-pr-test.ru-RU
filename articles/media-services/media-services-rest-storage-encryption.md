---
title: "Шифрование содержимого с помощью шифрования хранилища посредством REST API AMS"
description: "Узнайте, как шифровать содержимое с шифрованием хранилища, используя API REST AMS."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a0a79f3d-76a1-4994-9202-59b91a2230e0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 1979f5bf5e8cab88dab5fba49018afacf24504b3
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="encrypting-your-content-with-storage-encryption"></a>Шифрование содержимого с помощью шифрования хранилища

Настоятельно рекомендуется шифровать содержимое локально, используя 256-битное шифрование AES, а затем передавать его в хранилище Azure, где оно будет храниться в зашифрованном виде.

В этой статье приводятся общие сведения о шифровании хранилища AMS и показывается, как передавать зашифрованное содержимое хранилища.

* Создайте ключ содержимого.
* Создайте ресурс. При создании ресурса задайте для параметра AssetCreationOption значение StorageEncryption.
  
     Зашифрованные ресурсы-контейнеры должны быть связаны с типами содержимого.
* Привяжите ключ содержимого к ресурсу.  
* Настройте связанные с шифрованием параметры в сущностях AssetFile.

## <a name="considerations"></a>Рекомендации 

Если необходимо доставить зашифрованный в хранилище ресурс-контейнер, необходимо настроить его политику доставки. Перед выполнением потоковой передачи ресурса сервер потоковой передачи удаляет шифрование хранилища и осуществляет потоковую передачу содержимого с помощью указанной политики доставки. Дополнительные сведения см. в статье [Настройка политик доставки ресурсов](media-services-rest-configure-asset-delivery-policy.md).

При доступе к сущностям в службах мультимедиа необходимо задать определенные поля и значения заголовков в HTTP-запросах. Дополнительную информацию см. в статье [Обзор интерфейса REST API служб мультимедиа](media-services-rest-how-to-use.md). 

## <a name="connect-to-media-services"></a>Подключение к службам мультимедиа

Сведения о подключении к API AMS см. в разделе [Доступ к API служб мультимедиа Azure с помощью аутентификации Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>После успешного подключения к https://media.windows.net вы получите ошибку 301 (перенаправление), в которой будет указан другой URI служб мультимедиа. Используйте для последующих вызовов новый URI.

## <a name="storage-encryption-overview"></a>Общие сведения о шифровании хранилища
Шифрование хранилища AMS применяет режим шифрования **AES-CTR** ко всему файлу.  AES-CTR — это блочный шифр, который может шифровать данные произвольной длины и не требует заполнения. Он шифрует блок счетчика, используя алгоритм AES, а затем применяет XOR к выходным данным AES, содержащим данные для шифрования или расшифровки.  Используемый блок счетчика формируется путем копирования значения InitializationVector в байты 0–7 значения счетчика и присвоения байтам 8–15 нулевого значения. Байты 8–15 в 16-байтовом блоке счетчика (т. е. наименее значимые) используются как простое 64-разрядное целое число без знака, увеличивающееся на единицу с каждым последующим блоком данных, которые обрабатываются и хранятся в соответствии с порядком байтов в сети. Если это число достигает максимального значения (0xFFFFFFFFFFFFFFFF), при следующем приращении счетчик блока сбрасывается до нуля (байты 8–15) и не влияет на другие 64 разряда в счетчика (байты 0–7).   Для обеспечения безопасности шифрования в режиме AES-CTR значение InitializationVector для соответствующего идентификатора ключа должно быть уникальным для каждого файла содержимого, а длина файлов должна быть меньше 2^64 блоков.  Это гарантирует, что значение счетчика не будет использоваться с данным ключом повторно. Дополнительные сведения о режиме CTR см. на [этой вики-странице](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (в вики-статье вместо InitializationVector используется термин Nonce).

Параметр **Storage Encryption** используется для локального удаления незашифрованного содержимого с помощью AES 256 и его добавления в хранилище Azure, где оно хранится в зашифрованном виде. Ресурсы, защищенные с помощью шифрования хранилища, автоматически расшифровываются и помещаются в зашифрованную файловую систему до кодирования, а затем при необходимости повторно кодируются перед добавлением в виде нового выходного актива. Основная причина использования шифрования хранилища — для защиты входных файлов мультимедиа высокого качества с помощью стойкого шифрования при хранении на диске.

Для доставки ресурса из зашифрованного хранилища необходимо настроить политику доставки ресурсов, чтобы службы мультимедиа могли определить, как вы хотите доставлять содержимое. Перед выполнением потоковой передачи ресурса-контейнера сервер потоковой передачи удаляет шифрование хранилища и осуществляет потоковую передачу содержимого с помощью указанной политики доставки (например, AES, общее шифрование или без шифрования).

## <a name="create-contentkeys-used-for-encryption"></a>Создание сущности ContentKeys, используемой для шифрования
Зашифрованные ресурсы должны быть связаны с ключом шифрования хранилища. Прежде чем создавать файлы ресурсов, необходимо создать ключ содержимого, который будет использоваться для шифрования. В этой статье описывается, как создать ключ содержимого.

Ниже приведены общие шаги создания ключей содержимого, которые нужно связать с ресурсами, подлежащими шифрованию. 

1. Для шифрования хранилища случайным образом формируется 32-разрядный ключ AES. 
   
    Это будет ключ содержимого для ресурса, то есть для всех файлов, связанных с этим ресурсом, при расшифровке будет использоваться один и тот же ключ содержимого. 
2. Вызовите методы [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) и [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey), чтобы получить правильный сертификат X.509, который должен использоваться для шифрования ключа содержимого.
3. Зашифруйте ключ содержимого с помощью открытого ключа сертификата X.509. 
   
   Пакет SDK служб мультимедиа для .NET использует при выполнении шифрования RSA с OAEP.  Примером .NETможет служить [функция EncryptSymmetricKeyData](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).
4. Создайте значение контрольной суммы, вычисленное с помощью идентификатора ключа и ключа содержимого. В следующем примере .NET контрольная сумма вычисляется с помощью части "GUID" идентификатора ключа и незащищенного ключа содержимого.

        public static string CalculateChecksum(byte[] contentKey, Guid keyId)
        {
            const int ChecksumLength = 8;
            const int KeyIdLength = 16;

            byte[] encryptedKeyId = null;

            // Checksum is computed by AES-ECB encrypting the KID
            // with the content key.
            using (AesCryptoServiceProvider rijndael = new AesCryptoServiceProvider())
            {
                rijndael.Mode = CipherMode.ECB;
                rijndael.Key = contentKey;
                rijndael.Padding = PaddingMode.None;

                ICryptoTransform encryptor = rijndael.CreateEncryptor();
                encryptedKeyId = new byte[KeyIdLength];
                encryptor.TransformBlock(keyId.ToByteArray(), 0, KeyIdLength, encryptedKeyId, 0);
            }

            byte[] retVal = new byte[ChecksumLength];
            Array.Copy(encryptedKeyId, retVal, ChecksumLength);

            return Convert.ToBase64String(retVal);
        }

1. Создайте ключ содержимого, используя значения **EncryptedContentKey** (преобразуется в строку с кодировкой base64), **ProtectionKeyId**, **ProtectionKeyType**, **ContentKeyType** и **Checksum**, полученные на предыдущих шагах.

    Для шифрования хранилища в текст запроса необходимо включить указанные ниже свойства.

    Свойство текста запроса    | Описание
    ---|---
    Идентификатор | Идентификатор ContentKey, созданный нами в следующем формате "nb:kid:UUID:<NEW GUID>".
    ContentKeyType | Тип ключа содержимого, который в данном случае выражается целым числом. Для шифрования хранилища передается значение 1.
    EncryptedContentKey | Мы создаем новое значение ключа содержимого, которое представляет собой 256-битное (32-байтное) значение. Ключ шифруется с помощью сертификата шифрования хранилища X.509, полученного из служб мультимедиа Microsoft Azure с помощью HTTP- запроса GET для методов GetProtectionKeyId и GetProtectionKey. Например, см. следующий код .NET: метод **EncryptSymmetricKeyData**, определенный [здесь](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).
    ProtectionKeyId | Идентификатор ключа защиты для сертификата шифрования хранилища X.509, который использовался для шифрования ключа содержимого.
    ProtectionKeyType | Тип шифрования для защиты ключа, который использовался для шифрования ключа содержимого. В нашем примере этим значением является StorageEncryption(1).
    Checksum |Контрольная сумма, рассчитанная для ключа содержимого с помощью MD5. Она вычисляется путем шифрования идентификатора содержимого с использованием ключа содержимого. В примере кода показано, как вычислить контрольную сумму.


### <a name="retrieve-the-protectionkeyid"></a>Получение ProtectionKeyId
В следующем примере показано, как получить ProtectionKeyId (отпечаток сертификата) для сертификата, который необходимо использовать при шифровании ключа содержимого. Выполните этот шаг, чтобы проверить наличие соответствующего сертификата на компьютере.

Запрос:

    GET https://media.windows.net/api/GetProtectionKeyId?contentKeyType=0 HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net

Ответ:

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 139
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 2b6aa7a4-3a09-4b08-b581-26b55667f817
    x-ms-request-id: 2b6aa7a4-3a09-4b08-b581-26b55667f817
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 04 Feb 2015 02:42:52 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Edm.String","value":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C"}

### <a name="retrieve-the-protectionkey-for-the-protectionkeyid"></a>Получение ProtectionKey для ProtectionKeyId
В следующем примере показано, как получить сертификат X.509, используя значение ProtectionKeyId, полученное на предыдущем шаге.

Запрос:

    GET https://media.windows.net/api/GetProtectionKey?ProtectionKeyId='7D9BB04D9D0A4A24800CADBFEF232689E048F69C' HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    Host: media.windows.net

Ответ:

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 1227
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    request-id: 1523e8f3-8ed2-40fe-8a9a-5d81eb572cc8
    x-ms-request-id: 1523e8f3-8ed2-40fe-8a9a-5d81eb572cc8
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Thu, 05 Feb 2015 07:52:30 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Edm.String",
    "value":"MIIDSTCCAjGgAwIBAgIQqf92wku/HLJGCbMAU8GEnDANBgkqhkiG9w0BAQQFADAuMSwwKgYDVQQDEyN3YW1zYmx1cmVnMDAxZW5jcnlwdGFsbHNlY3JldHMtY2VydDAeFw0xMjA1MjkwNzAwMDBaFw0zMjA1MjkwNzAwMDBaMC4xLDAqBgNVBAMTI3dhbXNibHVyZWcwMDFlbmNyeXB0YWxsc2VjcmV0cy1jZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAzR0SEbXefvUjb9wCUfkEiKtGQ5Gc328qFPrhMjSo+YHe0AVviZ9YaxPPb0m1AaaRV4dqWpST2+JtDhLOmGpWmmA60tbATJDdmRzKi2eYAyhhE76MgJgL3myCQLP42jDusWXWSMabui3/tMDQs+zfi1sJ4Ch/lm5EvksYsu6o8sCv29VRwxfDLJPBy2NlbV4GbWz5Qxp2tAmHoROnfaRhwp6WIbquk69tEtu2U50CpPN2goLAqx2PpXAqA+prxCZYGTHqfmFJEKtZHhizVBTFPGS3ncfnQC9QIEwFbPw6E5PO5yNaB68radWsp5uvDg33G1i8IT39GstMW6zaaG7cNQIDAQABo2MwYTBfBgNVHQEEWDBWgBCOGT2hPhsvQioZimw8M+jOoTAwLjEsMCoGA1UEAxMjd2Ftc2JsdXJlZzAwMWVuY3J5cHRhbGxzZWNyZXRzLWNlcnSCEKn/dsJLvxyyRgmzAFPBhJwwDQYJKoZIhvcNAQEEBQADggEBABcrQPma2ekNS3Wc5wGXL/aHyQaQRwFGymnUJ+VR8jVUZaC/U/f6lR98eTlwycjVwRL7D15BfClGEHw66QdHejaViJCjbEIJJ3p2c9fzBKhjLhzB3VVNiLIaH6RSI1bMPd2eddSCqhDIn3VBN605GcYXMzhYp+YA6g9+YMNeS1b+LxX3fqixMQIxSHOLFZ1G/H2xfNawv0VikH3djNui3EKT1w/8aRkUv/AAV0b3rYkP/jA1I0CPn0XFk7STYoiJ3gJoKq9EMXhit+Iwfz0sMkfhWG12/XO+TAWqsK1ZxEjuC9OzrY7pFnNxs4Mu4S8iinehduSpY+9mDd3dHynNwT4="}

### <a name="create-the-content-key"></a>Создание ключа содержимого
После получения сертификата X.509 и использования его открытого ключа для шифрования ключа содержимого создайте сущность **ContentKey** и задайте для нее соответствующие свойства.

Одно из значений, которые необходимо задать при создания ключа содержимого — это тип. Для шифрования хранилища используется значение "1". 

В следующем примере показано, как создать **ContentKey**, когда для параметра **ContentKeyType** задано шифрование в хранилище (значение 1), а для параметра **ProtectionKeyType** — значение 0, указывающее на то, что идентификатор ключа защиты является отпечатком сертификата X.509.  

Запрос

    POST https://media.windows.net/api/ContentKeys HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net
    {
    "Name":"ContentKey",
    "ProtectionKeyId":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C", 
    "ContentKeyType":"1", 
    "ProtectionKeyType":"0",
    "EncryptedContentKey":"your encrypted content key",
    "Checksum":"calculated checksum"
    }

Ответ:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 777
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/ContentKeys('nb%3Akid%3AUUID%3A9c8ea9c6-52bd-4232-8a43-8e43d8564a99')
    Server: Microsoft-IIS/8.5
    request-id: 76e85e0f-5cf1-44cb-b689-b3455888682c
    x-ms-request-id: 76e85e0f-5cf1-44cb-b689-b3455888682c
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 04 Feb 2015 02:37:46 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeys/@Element",
    "Id":"nb:kid:UUID:9c8ea9c6-52bd-4232-8a43-8e43d8564a99","Created":"2015-02-04T02:37:46.9684379Z",
    "LastModified":"2015-02-04T02:37:46.9684379Z",
    "ContentKeyType":1,
    "EncryptedContentKey":"your encrypted content key",
    "Name":"ContentKey",
    "ProtectionKeyId":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C",
    "ProtectionKeyType":0,
    "Checksum":"calculated checksum"}

## <a name="create-an-asset"></a>Создание ресурса
В следующем примере показано, как создать ресурс.

**HTTP-запрос**

    POST https://media.windows.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"BigBuckBunny" "Options":1}

**HTTP-ответ**

При успешном выполнении возвращается следующий результат:

    HTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 452
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    request-id: e98be122-ae09-473a-8072-0ccd234a0657
    x-ms-request-id: e98be122-ae09-473a-8072-0ccd234a0657
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT
    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny.mp4",
       "Options":1,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

## <a name="associate-the-contentkey-with-an-asset"></a>Связывание сущности ContentKey с сущностью Asset
После создания сущности ContentKey свяжите ее с сущностью Asset, используя операцию $links, как показано в следующем примере:

Запрос:

    POST https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Afbd7ce05-1087-401b-aaae-29f16383c801')/$links/ContentKeys HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeys('nb%3Akid%3AUUID%3A01e6ea36-2285-4562-91f1-82c45736047c')"}

Ответ:

    HTTP/1.1 204 No Content 

## <a name="create-an-assetfile"></a>Создание сущности AssetFile
Сущность [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) представляет собой аудио- или видеофайл, который хранится в контейнере больших двоичных объектов. Файл ресурса всегда связан с ресурсом, который, в свою очередь, может содержать один или несколько файлов ресурса. Задача кодировщика служб мультимедиа завершится с ошибкой, если объект файла ресурса не связан с цифровым файлом в контейнере больших двоичных объектов.

Обратите внимание, что экземпляр **AssetFile** и фактический файл мультимедиа – это два разных объекта. Экземпляр AssetFile содержит метаданные о файле мультимедиа, а сам файл мультимедиа — фактическое мультимедийное содержимое.

После отправки цифрового файла мультимедиа в контейнер больших двоичных объектов будет использоваться HTTP-запрос **MERGE** , чтобы обновить сущность AssetFile информацией о файле мультимедиа (не показано в этом разделе). 

**HTTP-запрос**

    POST https://media.windows.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
    Content-Length: 164

    {  
       "IsEncrypted":"true",
       "EncryptionScheme" : "StorageEncryption", 
       "EncryptionVersion" : "1.0",       
       "EncryptionKeyId" : "nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510",
       "InitializationVector" : "397304628502661816</d:InitializationVector",
       "Options":0,
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }

**HTTP-ответ**

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 535
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5')
    Server: Microsoft-IIS/8.5
    request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    x-ms-request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 00:34:07 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Files/@Element",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "Name":"BigBuckBunny.mp4",
       "ContentFileSize":"0",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "EncryptionVersion": "1.0",
       "EncryptionScheme": "StorageEncryption",
       "IsEncrypted":true,
       "EncryptionKeyId":"nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510",
       "InitializationVector":"397304628502661816</d:InitializationVector",
       "IsPrimary":false,
       "LastModified":"2015-01-19T00:34:08.1934137Z",
       "Created":"2015-01-19T00:34:08.1934137Z",
       "MimeType":"video/mp4",
       "ContentChecksum":null
    }
