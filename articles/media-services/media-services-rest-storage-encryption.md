---
title: "aaaEncrypting содержимого с помощью шифрования хранилища с помощью API-интерфейса REST AMS"
description: "Узнайте, как tooencrypt содержимого с помощью шифрования хранилища с помощью API REST AMS."
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
ms.openlocfilehash: d5f8cb8dd1dcded76c9fededccc772d8102ccbad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="encrypting-your-content-with-storage-encryption"></a>Шифрование содержимого с помощью шифрования хранилища

Настоятельно рекомендуется tooencrypt-битное шифрование содержимого локально с помощью AES-256, а затем передать его tooAzure хранилища, где он будет храниться в зашифрованном виде.

В этой статье приводится обзор AMS шифрование хранилища и показано, как хранилище hello tooupload зашифрованного содержимого:

* Создайте ключ содержимого.
* Создайте ресурс. Установка hello AssetCreationOption tooStorageEncryption при создании hello активов.
  
     Зашифрованные активы имеют toobe, связанные с ключами содержимого.
* Ссылка hello содержимого ключа toohello активов.  
* Задайте параметры для сущностей AssetFile hello, связанные с шифрованием hello.

## <a name="considerations"></a>Рекомендации 

Если вы хотите toodeliver зашифрованного актива хранилища, необходимо настроить политику доставки актива hello. Перед потоковой актива hello, потоковая передача контента с помощью hello шифрование хранилища сервера удаляет hello и потоки указан политики доставки. Дополнительные сведения см. в статье [Настройка политик доставки ресурсов](media-services-rest-configure-asset-delivery-policy.md).

При доступе к сущностям в службах мультимедиа необходимо задать определенные поля и значения заголовков в HTTP-запросах. Дополнительную информацию см. в статье [Обзор интерфейса REST API служб мультимедиа](media-services-rest-how-to-use.md). 

## <a name="connect-toomedia-services"></a>Подключение служб tooMedia

Сведения о tooconnect toohello AMS API, в статье [hello доступа к API служб мультимедиа Azure с проверкой подлинности Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>После успешного подключения toohttps://media.windows.net, будет получено перенаправление 301 указывающее другой URI служб Media Services. Необходимо внести toohello последующих вызовов новый URI.

## <a name="storage-encryption-overview"></a>Общие сведения о шифровании хранилища
применяет шифрование хранилища Hello AMS **AES CTR** режим шифрования toohello весь файл.  AES-CTR — это блочный шифр, который может шифровать данные произвольной длины и не требует заполнения. Он работает путем шифрования блок счетчика с hello алгоритм AES, а затем оператор XOR hello выходные данные AES с tooencrypt данных hello или расшифровать.  Счетчик блока Hello, используемой создается путем копирования hello значение hello InitializationVector toobytes 0 too7 значения счетчика hello и too15 8 байтов значения счетчика hello установлены toozero. 16-разрядный счетчик hello блока, too15 8 байт (т. е. наименее значащие байты hello) используются как простой 64-разрядное целое число без знака, увеличивается на единицу для каждого блока данных, обрабатываемая и хранится в сетевой порядок байтов. Обратите внимание, что если это целое число достигает hello максимальное значение (0xFFFFFFFFFFFFFFFF) его увеличением сбрасывает hello блок счетчика toozero (8 байт too15) без влияния на другие hello 64 бита hello счетчика (т. е. too7 0 байт).   В порядке toomaintain hello безопасность режим шифрования AES CTR hello hello InitializationVector значение для данного идентификатора ключа для каждого ключа контента должен быть уникальным для каждого файла и файлы должны быть меньше 2 ^ 64 блоков в длину.  Это tooensure, значение счетчика не может повторно использовать с данным ключом. Дополнительные сведения о режиме CTR hello см. в разделе [этой странице вики-сайте](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (статья wiki hello использует hello термин «Nonce» вместо «InitializationVector»).

Используйте **шифрование хранилища** tooencrypt-битное шифрование незащищенного содержимого локально с помощью AES-256, а затем передать его tooAzure хранилища, где она хранится в зашифрованном виде. Активы, защищенные с помощью шифрования хранилища, автоматически дешифруются и помещаются в предыдущих tooencoding зашифрованный файл системы и при необходимости повторно зашифрован предыдущих toouploading возвращены в виде нового выходного актива. Hello основным случаем использования шифрования хранилища удобно, если нужно toosecure rest вашей высококачественных входных файлов мультимедиа с помощью строгого шифрования на диске.

В порядке toodeliver зашифрованного актива хранилища необходимо настроить политику доставки актива hello, службы мультимедиа получили информацию о способе toodeliver контента. Перед потоковой актива hello, потоковая передача контента с помощью hello шифрование хранилища сервера удаляет hello и потоки указан политики доставки (например, AES, общее шифрование или шифрование).

## <a name="create-contentkeys-used-for-encryption"></a>Создание сущности ContentKeys, используемой для шифрования
Зашифрованные активы имеют toobe, связанное с ключом шифрования хранилища. Необходимо создать ключа toobe с содержимым hello используется для шифрования перед созданием hello файлов активов. В этом разделе описываются как toocreate ключа содержимого.

Hello ниже приведены общие шаги для создания ключей контента будет связана с основные средства toobe зашифрованы. 

1. Для шифрования хранилища случайным образом формируется 32-разрядный ключ AES. 
   
    Это будет hello ключ содержимого для ресурса, что означает все файлы, связанные с этим ресурсом будет необходимо toouse hello один ключ содержимого во время расшифровки. 
2. Вызовите hello [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) и [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) tooget методы hello правильный сертификат X.509, который должен быть используется tooencrypt ключа содержимого.
3. Шифрование ключа содержимого с помощью открытого ключа сертификата X.509 hello hello. 
   
   Пакет SDK .NET служб мультимедиа использует алгоритм RSA с OAEP при выполнении шифрования hello.  Вы увидите пример .NET в hello [EncryptSymmetricKeyData функция](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).
4. Создайте значение контрольной суммы, вычисленных с помощью идентификатора ключа hello и ключа содержимого. Следующий пример .NET Hello вычисляет контрольную hello, с помощью hello GUID части идентификатора ключа hello и hello снимите ключа содержимого.

        public static string CalculateChecksum(byte[] contentKey, Guid keyId)
        {
            const int ChecksumLength = 8;
            const int KeyIdLength = 16;

            byte[] encryptedKeyId = null;

            // Checksum is computed by AES-ECB encrypting hello KID
            // with hello content key.
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

1. Создание ключа контента hello с hello **EncryptedContentKey** (преобразовать строку в кодировке toobase64), **ProtectionKeyId**, **ProtectionKeyType**,  **ContentKeyType**, и **контрольной суммы** значений, получаемых в предыдущих шагах.

    Для шифрования хранилища hello следующие свойства должны быть включены в текст запроса hello.

    Свойство текста запроса    | Описание
    ---|---
    Идентификатор | Hello код ContentKey, который мы создаем сами с помощью следующих hello отформатировать, «nb:kid:UUID:<NEW GUID>».
    ContentKeyType | Это тип ключа контента hello как целое число для этого ключа контента. Мы передаем hello значение 1 для шифрования хранилища.
    EncryptedContentKey | Мы создаем новое значение ключа содержимого, которое представляет собой 256-битное (32-байтное) значение. Hello ключ шифруется с помощью hello сертификата хранилища шифрования X.509 который получен из службы мультимедиа Microsoft Azure, выполнив запрос HTTP GET для hello GetProtectionKeyId и GetProtectionKey методов. Например, в разделе hello после кода .NET: hello **EncryptSymmetricKeyData** определенный метод [здесь](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).
    ProtectionKeyId | Это является hello код ключа защиты для hello сертификата хранилища шифрования X.509, используемый tooencrypt ключа контента.
    ProtectionKeyType | Это тип шифрования hello для hello защиты ключа, который был ключ содержимого используется tooencrypt hello. В нашем примере этим значением является StorageEncryption(1).
    Checksum |Hello MD5 вычисленная контрольная сумма для ключа контента hello. Она рассчитывается при шифровании кода hello контента с помощью ключа содержимого hello. Hello примере кода показано, как toocalculate hello контрольной суммы.


### <a name="retrieve-hello-protectionkeyid"></a>Получить hello ProtectionKeyId
Hello в следующем примере показано, как tooretrieve hello ProtectionKeyId, отпечаток сертификата, для hello сертификат, который необходимо использовать при шифровании ключа содержимого. Выполните этот шаг toomake, что уже имеется hello соответствующий сертификат на компьютере.

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

### <a name="retrieve-hello-protectionkey-for-hello-protectionkeyid"></a>Получить hello ProtectionKey для hello ProtectionKeyId
Hello следующем примере показано, как сертификат X.509 hello tooretrieve, с помощью значения ProtectionKeyId hello полученный в предыдущем шаге hello.

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

### <a name="create-hello-content-key"></a>Создание ключа контента hello
После получения сертификата X.509 hello и использовать его открытого ключа tooencrypt ключа содержимого создайте **ContentKey** сущности и установите его свойство значений соответствующим образом.

Одно из значений hello, необходимо задать при создания содержимого, что ключ имеет тип hello hello. В случае шифрования хранилища hello hello равно "1". 

Следующий пример показывает как Hello toocreate **ContentKey** с **ContentKeyType** для шифрования хранилища («1») и hello **ProtectionKeyType** значение слишком «0» tooindicate, hello идентификатор ключа защиты является отпечатком сертификата X.509 hello.  

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
Следующий пример показывает как Hello toocreate актива.

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

В случае успешного выполнения возвращается hello следующее:

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

## <a name="associate-hello-contentkey-with-an-asset"></a>Связать с активом hello ContentKey
После создания hello ContentKey, свяжите его с ресурсом, используя операцию hello $links, как показано в следующий пример hello:

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
Hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) сущности представляет видео- или файл, хранящийся в контейнере больших двоичных объектов. Файл ресурса всегда связан с ресурсом, который, в свою очередь, может содержать один или несколько файлов ресурса. задачу Hello Media Services Encoder завершается ошибкой, если объект файла ресурса не связан с цифровым файлом в контейнере больших двоичных объектов.

Обратите внимание, что hello **AssetFile** экземпляра и hello фактический файл мультимедиа являются двумя отдельными объектами. экземпляр AssetFile Hello содержит метаданные о файле мультимедиа hello, а файл мультимедиа hello hello фактический контент мультимедиа.

После отправки файла мультимедиа в контейнер больших двоичных объектов, используется hello **СЛИЯНИЯ** hello tooupdate HTTP-запроса AssetFile со сведениями о файл (не показано в этом разделе). 

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
