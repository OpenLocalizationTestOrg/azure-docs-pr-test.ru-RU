---
title: "с помощью API REST служб мультимедиа политики доставки активов aaaConfiguring | Документы Microsoft"
description: "В этом разделе показано, как политики доставки активов tooconfigure, с помощью API REST служб мультимедиа."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5cb9d32a-e68b-4585-aa82-58dded0691d0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 8203230d570935e17382c598820dbfe42f83f8d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-asset-delivery-policies"></a>Настройка политик доставки ресурсов-контейнеров
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

Если планируется toodeliver динамически зашифрованные активы, один из hello шагов в hello Media Services содержимого, что рабочий процесс доставки является настройка политики доставки активов. политики доставки активов Hello сообщает служб мультимедиа, порядок отображения для вашего toobe активов доставить: в какой протокол потоковой передачи следует актива динамического упаковать (для примера, MPEG DASH, HLS, Smooth Streaming или все), ли требуется toodynamically шифрование актива и способ (конверта или общее шифрование).

В этом разделе обсуждаются почему и как toocreate и настроить политики доставки активов.

>[!NOTE]
>При создании учетной записи AMS **по умолчанию** конечной точки потоковой передачи в hello добавлена учетная запись tooyour **остановлена** состояния. Потоковая передача вашего содержимого и примите преимуществами динамической упаковки и динамического шифрования toostart hello конечной точки потоковой передачи, из которого нужно имеет содержимое toostream toobe в hello **под управлением** состояния. 
>
>Кроме того, toobe может toouse динамической упаковки и динамического шифрования ваш ресурс должен содержать набор MP4 с адаптивным битрейтом или файлов Smooth Streaming с адаптивной скоростью.

Можно применить различные политики toohello одного средства. Например, можно применить PlayReady шифрования tooSmooth потоковой передачи и AES Envelope шифрования tooMPEG DASH и HLS. Все протоколы, которые не определены в политике доставки (например, добавить отдельную политику, которая указывает в качестве протокола hello только HLS) будут заблокированы для потоковой передачи. Hello toothis исключение — когда нет определенных политик доставки активов. Затем все протоколы будут разрешены в hello снимите флажок.

Если вы хотите toodeliver зашифрованного актива хранилища, необходимо настроить политику доставки актива hello. Перед потоковой актива hello, потоковая передача контента с помощью hello шифрование хранилища сервера удаляет hello и потоки указан политики доставки. Например, toodeliver актива зашифрован ключ шифрования конвертов Advanced Encryption Standard (AES), установите тип политики hello слишком**DynamicEnvelopeEncryption**. шифрование хранилища tooremove и средства hello потока в hello очевидна, установите тип политики hello слишком**NoDynamicEncryption**. Примеры, которые показывают, как tooconfigure этими типами политики выполните.

В зависимости от способа настройки политики доставки активов hello вы бы быть пакета может toodynamically, динамически зашифровать и поток hello следующие протоколы потоковых: Smooth Streaming, HLS, потоки MPEG DASH.

Следующий список показывает hello Hello форматирует используется toostream Smooth, HLS, ТИРЕ.

Smooth Streaming:

{имя конечной точки потоковой передачи - имя учетной записи служб мультимедиа}.streaming.mediaservices.windows.net/{идентификатор указателя}/{имя файла}.ism/Manifest

HLS:

{имя конечной точки потоковой передачи - имя учетной записи служб мультимедиа}.streaming.mediaservices.windows.net/{идентификатор указателя}/{имя файла}.ism/Manifest(format=m3u8-aapl)

MPEG DASH

{имя конечной точки потоковой передачи - имя учетной записи служб мультимедиа}.streaming.mediaservices.windows.net/{идентификатор указателя}/{имя файла}.ism/Manifest(format=mpd-time-csf)


Инструкции по статье toopublish актива и построения URL-АДРЕСЕ потоковой передачи, [построения URL-адрес потоковой передачи](media-services-deliver-streaming-content.md).

## <a name="considerations"></a>Рекомендации
* Невозможно удалить политику доставки ресурсов-контейнеров (AssetDeliveryPolicy), связанную с ресурсом-контейнером, пока существует указатель OnDemand (потоковой передачи) для этого ресурса-контейнера. Hello рекомендуется tooremove hello политику из ресурса hello перед удалением политики hello.
* Если политика доставки ресурсов-контейнеров не задана, создать указатель потоковой передачи в зашифрованном ресурсе-контейнере хранилища.  При hello активов не зашифрованного в хранилище, система hello позволит создать hello средства обнаружения и потоком в hello снимите без политики доставки активов.
* Может существовать несколько политик доставки активов, связанные с одного актива, но можно указать только один из способов toohandle данного AssetDeliveryProtocol.  То есть при попытке toolink две доставки политики, которые необходимо указать протокол AssetDeliveryProtocol.SmoothStreaming hello, вызовет ошибку поскольку hello системы неизвестно, какой из них необходимо tooapply когда клиент делает запрос Smooth Streaming.
* При наличии актива с существующий указатель потоковой передачи нельзя связать новый актив toohello политики, отменить привязку существующую политику из ресурса hello или обновлении политики доставки, связанный с активом hello.  Сначала имеют указатель потоковой передачи tooremove hello, настройте политики hello и повторного создания hello потоковой передачи указателя.  Можно использовать приветствия же locatorId при повторном создании hello потоковой передачи указателя, но следует убедиться, не будут вызывать проблемы для клиентов, так как содержимое, кэшируемых средой hello происхождения или подчиненным CDN.

>[!NOTE]

>При доступе к сущностям в службах мультимедиа необходимо задать определенные поля и значения заголовков в HTTP-запросах. Дополнительную информацию см. в статье [Обзор интерфейса REST API служб мультимедиа](media-services-rest-how-to-use.md).

## <a name="connect-toomedia-services"></a>Подключение служб tooMedia

Сведения о tooconnect toohello AMS API, в статье [hello доступа к API служб мультимедиа Azure с проверкой подлинности Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>После успешного подключения toohttps://media.windows.net, будет получено перенаправление 301 указывающее другой URI служб Media Services. Необходимо внести toohello последующих вызовов новый URI.

## <a name="clear-asset-delivery-policy"></a>Политики доставки незашифрованных ресурсов
### <a id="create_asset_delivery_policy"></a>Создание политики доставки активов
Hello следующий запрос HTTP создает политики доставки активов, указывающее toonot применения динамического шифрования и протоколов toodeliver поток hello в любом из следующих hello: протоколы MPEG DASH, HLS и Smooth Streaming. 

Сведения по вы значений можно указать при создании AssetDeliveryPolicy, см. в разделе hello [типы, используемые при определении AssetDeliveryPolicy](#types) раздела.   

Запрос:

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423397827&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Szo6lbJAvL3dyecAeVmyAnzv3mGzfUNClR5shk9Ivbk%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 4651882c-d7ad-4d5e-86ab-f07f47dcb41e
    Host: media.windows.net

    {"Name":"Clear Policy",
    "AssetDeliveryProtocol":7,
    "AssetDeliveryPolicyType":2,
    "AssetDeliveryConfiguration":null}

Ответ:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 363
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3A92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 4651882c-d7ad-4d5e-86ab-f07f47dcb41e
    request-id: 6aedbf93-4bc2-4586-8845-fd45590136af
    x-ms-request-id: 6aedbf93-4bc2-4586-8845-fd45590136af
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 08 Feb 2015 06:21:27 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#AssetDeliveryPolicies/@Element",
    "Id":"nb:adpid:UUID:92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd",
    "Name":"Clear Policy",
    "AssetDeliveryProtocol":7,
    "AssetDeliveryPolicyType":2,
    "AssetDeliveryConfiguration":null,
    "Created":"2015-02-08T06:21:27.6908329Z",
    "LastModified":"2015-02-08T06:21:27.6908329Z"}

### <a id="link_asset_with_asset_delivery_policy"></a>Привязка ресурса к политике доставки ресурсов
Привет, следуя hello ссылки запроса HTTP указан политики доставки активов toohello активов для.

Запрос:

    POST https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A86933344-9539-4d0c-be7d-f842458693e0')/$links/DeliveryPolicies HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-e769-3344-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423397827&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Szo6lbJAvL3dyecAeVmyAnzv3mGzfUNClR5shk9Ivbk%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 56d2763f-6e72-419d-ba3c-685f6db97e81
    Host: media.windows.net

    {"uri":"https://media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3A92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd')"}

Ответ:

    HTTP/1.1 204 No Content


## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a>Политика доставки ресурсов DynamicEnvelopeEncryption
### <a name="create-content-key-of-hello-envelopeencryption-type-and-link-it-toohello-asset"></a>Создать ключ контента для типа EnvelopeEncryption hello и связать его toohello активов
При определении политики доставки DynamicEnvelopeEncryption, что toolink toomake необходимо активов tooa ключа содержимого из hello EnvelopeEncryption типа. Дополнительные сведения см. в статье, посвященной [созданию ключей содержимого](media-services-rest-create-contentkey.md).

### <a id="get_delivery_url"></a>Получение URL-адреса доставки
URL-адрес доставки hello Get для hello указанного метода доставки ключа контента hello на предыдущем шаге hello. Клиент использует hello, возвращаемый URL-адрес toorequest ключ AES или лицензию PlayReady в порядке tooplayback hello защищенного содержимого.

Укажите тип hello hello tooget URL-адрес в тексте hello hello HTTP-запроса. Если необходимо обеспечить защиту содержимого с помощью PlayReady, запрошенный URL приобретения лицензий PlayReady служб мультимедиа, используя 1 для hello keyDeliveryType: {«keyDeliveryType»: 1}. При защите контента с шифрование конвертов hello запроса URL-адрес получения ключа путем указания 2 для keyDeliveryType: {«keyDeliveryType»: 2}.

Запрос:

    POST https://media.windows.net/api/ContentKeys('nb:kid:UUID:dc88f996-2859-4cf7-a279-c52a9d6b2f04')/GetKeyDeliveryUrl HTTP/1.1
    Content-Type: application/json
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423452029&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=IEXV06e3drSIN5naFRBdhJZCbfEqQbFZsGSIGmawhEo%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 569d4b7c-a446-4edc-b77c-9fb686083dd8
    Host: media.windows.net
    Content-Length: 21

    {"keyDeliveryType":2}

Ответ:

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 198
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 569d4b7c-a446-4edc-b77c-9fb686083dd8
    request-id: d26f65d2-fe65-4136-8fcf-31545be68377
    x-ms-request-id: d26f65d2-fe65-4136-8fcf-31545be68377
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 08 Feb 2015 21:42:30 GMT

    {"odata.metadata":"media.windows.net/api/$metadata#Edm.String","value":"https://amsaccount1.keydelivery.mediaservices.windows.net/?KID=dc88f996-2859-4cf7-a279-c52a9d6b2f04"}


### <a name="create-asset-delivery-policy"></a>Создание политики доставки активов
Hello следующий запрос HTTP создает hello **AssetDeliveryPolicy** , настроенных tooapply динамического конверта шифрования (**DynamicEnvelopeEncryption**) toohello **HLS**протокола (в этом примере другие протоколы, будет заблокирован потоковой передачи). 

Сведения по вы значений можно указать при создании AssetDeliveryPolicy, см. в разделе hello [типы, используемые при определении AssetDeliveryPolicy](#types) раздела.   

Запрос:

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423480651&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=T2FG3tIV0e2ETzxQ6RDWxWAsAzuy3ez2ruXPhrBe62Y%3d
    x-ms-version: 2.11
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    Host: media.windows.net

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":4,"AssetDeliveryPolicyType":3,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\\/\"}]"}


Ответ:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 460
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3Aec9b994e-672c-4a5b-8490-a464eeb7964b')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    request-id: c2a1ac0e-9644-474f-b38f-b9541c3a7c5f
    x-ms-request-id: c2a1ac0e-9644-474f-b38f-b9541c3a7c5f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 09 Feb 2015 05:24:38 GMT

    {"odata.metadata":"media.windows.net/api/$metadata#AssetDeliveryPolicies/@Element","Id":"nb:adpid:UUID:ec9b994e-672c-4a5b-8490-a464eeb7964b","Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":4,"AssetDeliveryPolicyType":3,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\\/\"}]","Created":"2015-02-09T05:24:38.9167436Z","LastModified":"2015-02-09T05:24:38.9167436Z"}


### <a name="link-asset-with-asset-delivery-policy"></a>Привязка ресурса к политике доставки ресурсов
См. раздел [Привязка ресурса к политике доставки ресурсов](#link_asset_with_asset_delivery_policy).

## <a name="dynamiccommonencryption-asset-delivery-policy"></a>Политика доставки ресурсов DynamicCommonEncryption
### <a name="create-content-key-of-hello-commonencryption-type-and-link-it-toohello-asset"></a>Создать ключ контента для типа CommonEncryption hello и связать его toohello активов
При определении политики доставки DynamicCommonEncryption, что toolink toomake необходимо активов tooa ключа содержимого из hello CommonEncryption типа. Дополнительные сведения см. в статье, посвященной [созданию ключей содержимого](media-services-rest-create-contentkey.md).

### <a name="get-delivery-url"></a>Получение URL-адреса доставки
Получите URL-адрес доставки hello для метода доставки PlayReady hello hello ключа контента на предыдущем шаге hello. Клиент использует hello вернул toorequest URL-адрес лицензии PlayReady в порядке tooplayback hello защищенного содержимого. Дополнительные сведения см. в разделе [Получение URL-адреса доставки](#get_delivery_url).

### <a name="create-asset-delivery-policy"></a>Создание политики доставки активов
Hello следующий запрос HTTP создает hello **AssetDeliveryPolicy** , настроенных tooapply динамического общее шифрование (**DynamicCommonEncryption**) toohello **Smooth Streaming**  протокола (в этом примере другие протоколы, будет заблокирован потоковой передачи). 

Сведения по вы значений можно указать при создании AssetDeliveryPolicy, см. в разделе hello [типы, используемые при определении AssetDeliveryPolicy](#types) раздела.   

Запрос:

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423480651&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=T2FG3tIV0e2ETzxQ6RDWxWAsAzuy3ez2ruXPhrBe62Y%3d
    x-ms-version: 2.11
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    Host: media.windows.net

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":1,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\/PlayReady\/"}]"}


Если требуется tooprotect контент с помощью Widevine DRM обновления hello AssetDeliveryConfiguration значения toouse WidevineLicenseAcquisitionUrl (которая имеет значение hello 7) и укажите hello URL-адрес службы доставки лицензий. Можно использовать следующие toohelp партнеров AMS доставки лицензии Widevine hello: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).

Например: 

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":2,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":7,\"Value\":\"https:\\/\\/example.net\/WidevineLicenseAcquisition\/"}]"}

> [!NOTE]
> При шифровании с Widevine будет только может toodeliver, с помощью ТИРЕ. Убедитесь, что toospecify протокол доставки актива ТИРЕ (2) в hello.
> 
> 

### <a name="link-asset-with-asset-delivery-policy"></a>Привязка ресурса к политике доставки ресурсов
См. раздел [Привязка ресурса к политике доставки ресурсов](#link_asset_with_asset_delivery_policy).

## <a id="types"></a>Типы, используемые при определении AssetDeliveryPolicy

### <a name="assetdeliveryprotocol"></a>AssetDeliveryProtocol

Hello следующие перечисления описаны значения, которые можно задать для hello протокол доставки актива.

    [Flags]
    public enum AssetDeliveryProtocol
    {
        /// <summary>
        /// No protocols.
        /// </summary>
        None = 0x0,

        /// <summary>
        /// Smooth streaming protocol.
        /// </summary>
        SmoothStreaming = 0x1,

        /// <summary>
        /// MPEG Dynamic Adaptive Streaming over HTTP (DASH)
        /// </summary>
        Dash = 0x2,

        /// <summary>
        /// Apple HTTP Live Streaming protocol.
        /// </summary>
        HLS = 0x4,

        ProgressiveDownload = 0x10, 
 
        /// <summary>
        /// Include all protocols.
        /// </summary>
        All = 0xFFFF
    }

### <a name="assetdeliverypolicytype"></a>AssetDeliveryPolicyType

Hello следующие перечисления описаны значения, которые можно задать для типа политики доставки активов hello.  

    public enum AssetDeliveryPolicyType
    {
        /// <summary>
        /// Delivery Policy Type not set.  An invalid value.
        /// </summary>
        None,

        /// <summary>
        /// hello Asset should not be delivered via this AssetDeliveryProtocol. 
        /// </summary>
        Blocked, 

        /// <summary>
        /// Do not apply dynamic encryption toohello asset.
        /// </summary>
        /// 
        NoDynamicEncryption,  

        /// <summary>
        /// Apply Dynamic Envelope encryption.
        /// </summary>
        DynamicEnvelopeEncryption,

        /// <summary>
        /// Apply Dynamic Common encryption.
        /// </summary>
        DynamicCommonEncryption
        }

### <a name="contentkeydeliverytype"></a>ContentKeyDeliveryType

Hello следующие перечисления описаны значения, можно использовать метод доставки hello tooconfigure hello содержимого toohello ключа клиента.
    
    public enum ContentKeyDeliveryType
    {
        /// <summary>
        /// None.
        ///
        </summary>
        None = 0,

        /// <summary>
        /// Use PlayReady License acquistion protocol
        ///
        </summary>
        PlayReadyLicense = 1,

        /// <summary>
        /// Use MPEG Baseline HTTP key protocol.
        ///
        </summary>
        BaselineHttp = 2,

        /// <summary>
        /// Use Widevine License acquistion protocol
        ///
        </summary>
        Widevine = 3

    }


### <a name="assetdeliverypolicyconfigurationkey"></a>AssetDeliveryPolicyConfigurationKey

следующие перечисления Hello описаны значения, можно задать tooconfigure ключи, используемые tooget конфигурация политики доставки активов.

    public enum AssetDeliveryPolicyConfigurationKey
    {
        /// <summary>
        /// No policies.
        /// </summary>
        None,

        /// <summary>
        /// Exact Envelope key URL.
        /// </summary>
        EnvelopeKeyAcquisitionUrl,

        /// <summary>
        /// Base key url that will have KID=<Guid> appended for Envelope.
        /// </summary>
        EnvelopeBaseKeyAcquisitionUrl,

        /// <summary>
        /// hello initialization vector toouse for envelope encryption in Base64 format.
        /// </summary>
        EnvelopeEncryptionIVAsBase64,

        /// <summary>
        /// hello PlayReady License Acquisition Url toouse for common encryption.
        /// </summary>
        PlayReadyLicenseAcquisitionUrl,

        /// <summary>
        /// hello PlayReady Custom Attributes tooadd toohello PlayReady Content Header
        /// </summary>
        PlayReadyCustomAttributes,

        /// <summary>
        /// hello initialization vector toouse for envelope encryption.
        /// </summary>
        EnvelopeEncryptionIV,

        /// <summary>
        /// Widevine DRM acquisition url
        /// </summary>
        WidevineLicenseAcquisitionUrl
    }

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

