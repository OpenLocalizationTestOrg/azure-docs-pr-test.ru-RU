---
title: "aaaConnecting tooMedia учетной записи службы, с помощью API-интерфейса REST | Документы Microsoft"
description: "В этом разделе показано, как в подписку служб tooMedia tooconnect REST API."
services: media-services
documentationcenter: 
author: Juliako
manager: erikre
editor: 
ms.assetid: 79dc64f1-15d8-4a81-b9d9-3d3c44d2e1e8
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: 1d5064a3612dc96f5c5ad910d183d84fb70a3b6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-toomedia-services-account-using-media-services-rest-api"></a>Подключение tooMedia учетной записи службы, с помощью API REST служб мультимедиа
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-connect-programmatically.md)
> * [REST](media-services-rest-connect-programmatically.md)
> 
> 

В этом разделе описывается, как tooobtain tooMicrosoft программное подключение при программировании с использованием служб мультимедиа Azure hello API REST служб мультимедиа.

При доступе к Microsoft Azure Media Services требуются две вещи: маркер доступа, предоставляемые службы управления доступом Azure (ACS) и hello URI служб Media Services сам. Можно использовать любые средства, необходимые при создании этих запросов, так как указать hello правильные значения заголовка и передайте в маркере доступа hello правильно при вызове в службы мультимедиа.

следующие шаги Hello описания наиболее распространенных hello рабочего процесса, при tooMedia tooconnect hello API REST служб мультимедиа с помощью служб:

1. Получение маркера доступа 
2. Подключение toohello URI служб Media Services 
   
   > [!NOTE]
   > После успешного подключения toohttps://media.windows.net, будет получено перенаправление 301 указывающее другой URI служб Media Services. Необходимо внести toohello последующих вызовов новый URI.
   > Может также появиться HTTP/1.1 200 ответ, содержащий описание метаданных ODATA API hello.
   > 
   > 
3. Учет последующие вызовы API toohello новый URL-адрес. 
   
    Например если после попытки tooconnect, полученный hello следующее:
   
        HTTP/1.1 301 Moved Permanently
        Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
   
    Вам следует опубликовать в последующих toohttps://wamsbayclus001rest-hs.cloudapp.net/api/ вызовы API.

    >[!NOTE]
    >Действует ограничение в 1 000 000 записей для разных политик AMS (например, для политики Locator или ContentKeyAuthorizationPolicy). Следует использовать hello же идентификатор политики, если вы используете всегда hello же дни / доступа разрешения, например, политики для указатели, которые являются предполагаемого tooremain на месте в течение длительного времени (без передачи политики). Чтобы узнать больше, ознакомьтесь с [этим](media-services-dotnet-manage-entities.md#limit-access-policies) разделом.

## <a name="access-control-address"></a>Адрес контроля доступа
Адрес для контроля доступа к службам мультимедиа: https://wamsprodglobal001acs.accesscontrol.windows.net. Для северного Китая используется другой адрес: https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn.

## <a name="getting-an-access-token"></a>Получение маркера доступа
tooaccess Media Services непосредственно через hello REST API, извлечения токена доступа из службы ACS и используйте его при каждом HTTP-запросе, внесенные в службу hello. Этот маркер является аналогичные tooother токенам, выдаваемым ACS на основе утверждений в заголовке HTTP-запроса и с использованием протокола OAuth v2 hello hello. Другие необходимые компоненты для прямого подключения служб tooMedia необязательно.

Hello пример hello заголовка HTTP-запроса и tooretrieve используется текст токена.

**Заголовок**:

    POST https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13 HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Host: wamsprodglobal001acs.accesscontrol.windows.net
    Content-Length: 120
    Expect: 100-continue
    Connection: Keep-Alive
    Accept: application/json


**Текст**:

Требуются tooprove hello client_id и client_secret значения в тексте hello этого запроса; client_id и client_secret соответствуют toohello AccountName и AccountKey значения, соответственно. Эти значения предоставляются tooyou службами мультимедиа при настройке учетной записи. 

Обратите внимание, hello AccountKey для учетной записи службы мультимедиа должно быть URL-адреса (в разделе [процентное кодирование](http://tools.ietf.org/html/rfc3986#section-2.1) при его использовании в качестве client_secret hello в запросе токена доступа.

    grant_type=client_credentials&client_id=ams_account_name&client_secret=URL_encoded_ams_account_key&scope=urn%3aWindowsAzureMediaServices


Например: 

    grant_type=client_credentials&client_id=amstestaccount001&client_secret=wUNbKhNj07oqjqU3Ah9R9f4kqTJ9avPpfe6Pk3YZ7ng%3d&scope=urn%3aWindowsAzureMediaServices


Hello пример hello HTTP-ответ, содержащий доступа hello маркеров в тексте hello.

    HTTP/1.1 200 OK
    Cache-Control: no-cache, no-store
    Pragma: no-cache
    Content-Type: application/json; charset=utf-8
    Expires: -1
    request-id: a65150f5-2784-4a01-a4b7-33456187ad83
    X-Content-Type-Options: nosniff
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Thu, 15 Jan 2015 08:07:20 GMT
    Content-Length: 670

    {  
       "token_type":"http://schemas.xmlsoap.org/ws/2009/11/swt-token-profile-1.0",
       "access_token":"http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421330840&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=uf69n82KlqZmkJDNxhJkOxpyIpA2HDyeGUTtSnq1vlE%3d",
       "expires_in":"21600",
       "scope":"urn:WindowsAzureMediaServices"
    }


> [!NOTE]
> Рекомендуется toocache hello «access_token» и «expires_in» значения tooan внешнего хранилища. данные токена Hello позже может получить из хранилища hello и повторно использовать в вызовах API REST служб мультимедиа. Это особенно полезно для сценариев, где маркер hello, могут безопасно использоваться нескольких процессах или компьютеров.
> 
> 

Убедитесь, что toomonitor hello «expires_in» значение hello доступа маркера и при необходимости обновите вызовы REST API новые токены.

### <a name="connecting-toohello-media-services-uri"></a>Подключение toohello URI служб Media Services
Hello корневой URI служб мультимедиа — https://media.windows.net/. Изначально необходимо подключиться toothis URI и при появлении перенаправление 301 обратно в ответе, следует делать toohello последующих вызовов новый URI. Кроме того, не используйте в запросах логику автоматического перенаправления или следования. Глаголы HTTP и текст запросов не будут перенаправляться toohello новый универсальный код Ресурса.

Обратите внимание, что hello корневой URI для отправки и загрузки файлов активов находится https://yourstorageaccount.blob.core.windows.net/ имя учетной записи хранения hello hello же тот, который был использован во время настройки учетной записи служб мультимедиа.

Привет, следующий пример демонстрирует HTTP запроса toohello Media Services корневой URI (https://media.windows.net/). Hello запроса получает перенаправление 301 обратно в ответе. Hello последующий запрос использует hello новый универсальный код Ресурса (https://wamsbayclus001rest-hs.cloudapp.net/api/).     

**HTTP-запрос**:

    GET https://media.windows.net/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: media.windows.net


**HTTP-ответ**:

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
    Server: Microsoft-IIS/8.5
    request-id: 987d7652-497a-44e5-b815-f492e02aef97
    x-ms-request-id: 987d7652-497a-44e5-b815-f492e02aef97
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sat, 17 Jan 2015 07:44:53 GMT
    Content-Length: 164

    <html><head><title>Object moved</title></head><body>
    <h2>Object moved too<a href="https://wamsbayclus001rest-hs.cloudapp.net/api/">here</a>.</h2>
    </body></html>


**HTTP-запроса** (с помощью hello новый универсальный код Ресурса):

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: wamsbayclus001rest-hs.cloudapp.net


**HTTP-ответ**:

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 1250
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 5f52ea9d-177e-48fe-9709-24953d19f84a
    x-ms-request-id: 5f52ea9d-177e-48fe-9709-24953d19f84a
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sat, 17 Jan 2015 07:44:52 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata","value":[{"name":"AccessPolicies","url":"AccessPolicies"},{"name":"Locators","url":"Locators"},{"name":"ContentKeys","url":"ContentKeys"},{"name":"ContentKeyAuthorizationPolicyOptions","url":"ContentKeyAuthorizationPolicyOptions"},{"name":"ContentKeyAuthorizationPolicies","url":"ContentKeyAuthorizationPolicies"},{"name":"Files","url":"Files"},{"name":"Assets","url":"Assets"},{"name":"AssetDeliveryPolicies","url":"AssetDeliveryPolicies"},{"name":"IngestManifestFiles","url":"IngestManifestFiles"},{"name":"IngestManifestAssets","url":"IngestManifestAssets"},{"name":"IngestManifests","url":"IngestManifests"},{"name":"StorageAccounts","url":"StorageAccounts"},{"name":"Tasks","url":"Tasks"},{"name":"NotificationEndPoints","url":"NotificationEndPoints"},{"name":"Jobs","url":"Jobs"},{"name":"TaskTemplates","url":"TaskTemplates"},{"name":"JobTemplates","url":"JobTemplates"},{"name":"MediaProcessors","url":"MediaProcessors"},{"name":"EncodingReservedUnitTypes","url":"EncodingReservedUnitTypes"},{"name":"Operations","url":"Operations"},{"name":"StreamingEndpoints","url":"StreamingEndpoints"},{"name":"Channels","url":"Channels"},{"name":"Programs","url":"Programs"}]}



> [!NOTE]
> После передачи hello новый URI, который является hello URI, который должен быть toocommunicate используется со службами мультимедиа. 
> 
> 

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

