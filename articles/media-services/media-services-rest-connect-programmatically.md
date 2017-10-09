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
# <a name="connecting-toomedia-services-account-using-media-services-rest-api"></a><span data-ttu-id="e98b0-103">Подключение tooMedia учетной записи службы, с помощью API REST служб мультимедиа</span><span class="sxs-lookup"><span data-stu-id="e98b0-103">Connecting tooMedia Services Account using Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e98b0-104">.NET</span><span class="sxs-lookup"><span data-stu-id="e98b0-104">.NET</span></span>](media-services-dotnet-connect-programmatically.md)
> * [<span data-ttu-id="e98b0-105">REST</span><span class="sxs-lookup"><span data-stu-id="e98b0-105">REST</span></span>](media-services-rest-connect-programmatically.md)
> 
> 

<span data-ttu-id="e98b0-106">В этом разделе описывается, как tooobtain tooMicrosoft программное подключение при программировании с использованием служб мультимедиа Azure hello API REST служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="e98b0-106">This topic describes how tooobtain a programmatic connection tooMicrosoft Azure Media Services when you are programming with hello Media Services REST API.</span></span>

<span data-ttu-id="e98b0-107">При доступе к Microsoft Azure Media Services требуются две вещи: маркер доступа, предоставляемые службы управления доступом Azure (ACS) и hello URI служб Media Services сам.</span><span class="sxs-lookup"><span data-stu-id="e98b0-107">Two things are required when accessing Microsoft Azure Media Services: An access token provided by Azure Access Control Services (ACS), and hello URI of Media Services itself.</span></span> <span data-ttu-id="e98b0-108">Можно использовать любые средства, необходимые при создании этих запросов, так как указать hello правильные значения заголовка и передайте в маркере доступа hello правильно при вызове в службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="e98b0-108">You can use any means you want when creating these requests as long as you specify hello correct header values and pass in hello access token correctly when calling into Media Services.</span></span>

<span data-ttu-id="e98b0-109">следующие шаги Hello описания наиболее распространенных hello рабочего процесса, при tooMedia tooconnect hello API REST служб мультимедиа с помощью служб:</span><span class="sxs-lookup"><span data-stu-id="e98b0-109">hello following steps describe hello most common workflow when using hello Media Services REST API tooconnect tooMedia Services:</span></span>

1. <span data-ttu-id="e98b0-110">Получение маркера доступа</span><span class="sxs-lookup"><span data-stu-id="e98b0-110">Getting an access token</span></span> 
2. <span data-ttu-id="e98b0-111">Подключение toohello URI служб Media Services</span><span class="sxs-lookup"><span data-stu-id="e98b0-111">Connecting toohello Media Services URI</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="e98b0-112">После успешного подключения toohttps://media.windows.net, будет получено перенаправление 301 указывающее другой URI служб Media Services.</span><span class="sxs-lookup"><span data-stu-id="e98b0-112">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="e98b0-113">Необходимо внести toohello последующих вызовов новый URI.</span><span class="sxs-lookup"><span data-stu-id="e98b0-113">You must make subsequent calls toohello new URI.</span></span>
   > <span data-ttu-id="e98b0-114">Может также появиться HTTP/1.1 200 ответ, содержащий описание метаданных ODATA API hello.</span><span class="sxs-lookup"><span data-stu-id="e98b0-114">You may also receive a HTTP/1.1 200 response that contains hello ODATA API metadata description.</span></span>
   > 
   > 
3. <span data-ttu-id="e98b0-115">Учет последующие вызовы API toohello новый URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="e98b0-115">Post your subsequent API calls toohello new URL.</span></span> 
   
    <span data-ttu-id="e98b0-116">Например если после попытки tooconnect, полученный hello следующее:</span><span class="sxs-lookup"><span data-stu-id="e98b0-116">For example, if after trying tooconnect, you got hello following:</span></span>
   
        HTTP/1.1 301 Moved Permanently
        Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
   
    <span data-ttu-id="e98b0-117">Вам следует опубликовать в последующих toohttps://wamsbayclus001rest-hs.cloudapp.net/api/ вызовы API.</span><span class="sxs-lookup"><span data-stu-id="e98b0-117">You should post your subsequent API calls toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

    >[!NOTE]
    ><span data-ttu-id="e98b0-118">Действует ограничение в 1 000 000 записей для разных политик AMS (например, для политики Locator или ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="e98b0-118">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="e98b0-119">Следует использовать hello же идентификатор политики, если вы используете всегда hello же дни / доступа разрешения, например, политики для указатели, которые являются предполагаемого tooremain на месте в течение длительного времени (без передачи политики).</span><span class="sxs-lookup"><span data-stu-id="e98b0-119">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="e98b0-120">Чтобы узнать больше, ознакомьтесь с [этим](media-services-dotnet-manage-entities.md#limit-access-policies) разделом.</span><span class="sxs-lookup"><span data-stu-id="e98b0-120">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

## <a name="access-control-address"></a><span data-ttu-id="e98b0-121">Адрес контроля доступа</span><span class="sxs-lookup"><span data-stu-id="e98b0-121">Access control address</span></span>
<span data-ttu-id="e98b0-122">Адрес для контроля доступа к службам мультимедиа: https://wamsprodglobal001acs.accesscontrol.windows.net. Для северного Китая используется другой адрес: https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn.</span><span class="sxs-lookup"><span data-stu-id="e98b0-122">Media Services access control address is https://wamsprodglobal001acs.accesscontrol.windows.net, except for North China region, where it is https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn.</span></span>

## <a name="getting-an-access-token"></a><span data-ttu-id="e98b0-123">Получение маркера доступа</span><span class="sxs-lookup"><span data-stu-id="e98b0-123">Getting an access token</span></span>
<span data-ttu-id="e98b0-124">tooaccess Media Services непосредственно через hello REST API, извлечения токена доступа из службы ACS и используйте его при каждом HTTP-запросе, внесенные в службу hello.</span><span class="sxs-lookup"><span data-stu-id="e98b0-124">tooaccess Media Services directly through hello REST API, retrieve an access token from ACS and use it during every HTTP request you make into hello service.</span></span> <span data-ttu-id="e98b0-125">Этот маркер является аналогичные tooother токенам, выдаваемым ACS на основе утверждений в заголовке HTTP-запроса и с использованием протокола OAuth v2 hello hello.</span><span class="sxs-lookup"><span data-stu-id="e98b0-125">This token is similar tooother tokens provided by ACS based on access claims provided in hello header of an HTTP request and using hello OAuth v2 protocol.</span></span> <span data-ttu-id="e98b0-126">Другие необходимые компоненты для прямого подключения служб tooMedia необязательно.</span><span class="sxs-lookup"><span data-stu-id="e98b0-126">You do not need any other prerequisites before directly connecting tooMedia Services.</span></span>

<span data-ttu-id="e98b0-127">Hello пример hello заголовка HTTP-запроса и tooretrieve используется текст токена.</span><span class="sxs-lookup"><span data-stu-id="e98b0-127">hello following example shows hello HTTP request header and body used tooretrieve a token.</span></span>

<span data-ttu-id="e98b0-128">**Заголовок**:</span><span class="sxs-lookup"><span data-stu-id="e98b0-128">**Header**:</span></span>

    POST https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13 HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Host: wamsprodglobal001acs.accesscontrol.windows.net
    Content-Length: 120
    Expect: 100-continue
    Connection: Keep-Alive
    Accept: application/json


<span data-ttu-id="e98b0-129">**Текст**:</span><span class="sxs-lookup"><span data-stu-id="e98b0-129">**Body**:</span></span>

<span data-ttu-id="e98b0-130">Требуются tooprove hello client_id и client_secret значения в тексте hello этого запроса; client_id и client_secret соответствуют toohello AccountName и AccountKey значения, соответственно.</span><span class="sxs-lookup"><span data-stu-id="e98b0-130">You need tooprove hello client_id and client_secret values in hello body of this request; client_id and client_secret correspond toohello AccountName and AccountKey values, respectively.</span></span> <span data-ttu-id="e98b0-131">Эти значения предоставляются tooyou службами мультимедиа при настройке учетной записи.</span><span class="sxs-lookup"><span data-stu-id="e98b0-131">These values are provided tooyou by Media Services when you set up your account.</span></span> 

<span data-ttu-id="e98b0-132">Обратите внимание, hello AccountKey для учетной записи службы мультимедиа должно быть URL-адреса (в разделе [процентное кодирование](http://tools.ietf.org/html/rfc3986#section-2.1) при его использовании в качестве client_secret hello в запросе токена доступа.</span><span class="sxs-lookup"><span data-stu-id="e98b0-132">Note that hello AccountKey for your Media Services account must be URL-encoded (see [Percent-Encoding](http://tools.ietf.org/html/rfc3986#section-2.1) when using it as hello client_secret value in your access token request.</span></span>

    grant_type=client_credentials&client_id=ams_account_name&client_secret=URL_encoded_ams_account_key&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="e98b0-133">Например:</span><span class="sxs-lookup"><span data-stu-id="e98b0-133">For example:</span></span> 

    grant_type=client_credentials&client_id=amstestaccount001&client_secret=wUNbKhNj07oqjqU3Ah9R9f4kqTJ9avPpfe6Pk3YZ7ng%3d&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="e98b0-134">Hello пример hello HTTP-ответ, содержащий доступа hello маркеров в тексте hello.</span><span class="sxs-lookup"><span data-stu-id="e98b0-134">hello following example shows hello HTTP response that contains hello access token in hello response body.</span></span>

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
> <span data-ttu-id="e98b0-135">Рекомендуется toocache hello «access_token» и «expires_in» значения tooan внешнего хранилища.</span><span class="sxs-lookup"><span data-stu-id="e98b0-135">It is recommended toocache hello "access_token " and "expires_in " values tooan external storage.</span></span> <span data-ttu-id="e98b0-136">данные токена Hello позже может получить из хранилища hello и повторно использовать в вызовах API REST служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="e98b0-136">hello token data could later be retrieved from hello storage and re-used in your Media Services REST API calls.</span></span> <span data-ttu-id="e98b0-137">Это особенно полезно для сценариев, где маркер hello, могут безопасно использоваться нескольких процессах или компьютеров.</span><span class="sxs-lookup"><span data-stu-id="e98b0-137">This is especially useful for scenarios where hello token can be securely shared among multiple processes or computers.</span></span>
> 
> 

<span data-ttu-id="e98b0-138">Убедитесь, что toomonitor hello «expires_in» значение hello доступа маркера и при необходимости обновите вызовы REST API новые токены.</span><span class="sxs-lookup"><span data-stu-id="e98b0-138">Make sure toomonitor hello "expires_in" value of hello access token and update your REST API calls with new tokens as needed.</span></span>

### <a name="connecting-toohello-media-services-uri"></a><span data-ttu-id="e98b0-139">Подключение toohello URI служб Media Services</span><span class="sxs-lookup"><span data-stu-id="e98b0-139">Connecting toohello Media Services URI</span></span>
<span data-ttu-id="e98b0-140">Hello корневой URI служб мультимедиа — https://media.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="e98b0-140">hello root URI for Media Services is https://media.windows.net/.</span></span> <span data-ttu-id="e98b0-141">Изначально необходимо подключиться toothis URI и при появлении перенаправление 301 обратно в ответе, следует делать toohello последующих вызовов новый URI.</span><span class="sxs-lookup"><span data-stu-id="e98b0-141">You should initially connect toothis URI, and if you get a 301 redirect back in response, you should make subsequent calls toohello new URI.</span></span> <span data-ttu-id="e98b0-142">Кроме того, не используйте в запросах логику автоматического перенаправления или следования.</span><span class="sxs-lookup"><span data-stu-id="e98b0-142">In addition, do not use any auto-redirect/follow logic in your requests.</span></span> <span data-ttu-id="e98b0-143">Глаголы HTTP и текст запросов не будут перенаправляться toohello новый универсальный код Ресурса.</span><span class="sxs-lookup"><span data-stu-id="e98b0-143">HTTP verbs and request bodies will not be forwarded toohello new URI.</span></span>

<span data-ttu-id="e98b0-144">Обратите внимание, что hello корневой URI для отправки и загрузки файлов активов находится https://yourstorageaccount.blob.core.windows.net/ имя учетной записи хранения hello hello же тот, который был использован во время настройки учетной записи служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="e98b0-144">Note that hello root URI for uploading and downloading Asset files is https://yourstorageaccount.blob.core.windows.net/ where hello storage account name is hello same one you used during your Media Services account setup.</span></span>

<span data-ttu-id="e98b0-145">Привет, следующий пример демонстрирует HTTP запроса toohello Media Services корневой URI (https://media.windows.net/).</span><span class="sxs-lookup"><span data-stu-id="e98b0-145">hello following example demonstrates HTTP request toohello Media Services root URI (https://media.windows.net/).</span></span> <span data-ttu-id="e98b0-146">Hello запроса получает перенаправление 301 обратно в ответе.</span><span class="sxs-lookup"><span data-stu-id="e98b0-146">hello request gets a 301 redirect back in response.</span></span> <span data-ttu-id="e98b0-147">Hello последующий запрос использует hello новый универсальный код Ресурса (https://wamsbayclus001rest-hs.cloudapp.net/api/).</span><span class="sxs-lookup"><span data-stu-id="e98b0-147">hello subsequent request is using hello new URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).</span></span>     

<span data-ttu-id="e98b0-148">**HTTP-запрос**:</span><span class="sxs-lookup"><span data-stu-id="e98b0-148">**HTTP Request**:</span></span>

    GET https://media.windows.net/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: media.windows.net


<span data-ttu-id="e98b0-149">**HTTP-ответ**:</span><span class="sxs-lookup"><span data-stu-id="e98b0-149">**HTTP Response**:</span></span>

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


<span data-ttu-id="e98b0-150">**HTTP-запроса** (с помощью hello новый универсальный код Ресурса):</span><span class="sxs-lookup"><span data-stu-id="e98b0-150">**HTTP Request** (using hello new URI):</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="e98b0-151">**HTTP-ответ**:</span><span class="sxs-lookup"><span data-stu-id="e98b0-151">**HTTP Response**:</span></span>

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
> <span data-ttu-id="e98b0-152">После передачи hello новый URI, который является hello URI, который должен быть toocommunicate используется со службами мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="e98b0-152">Once you get hello new URI, that is hello URI that should be used toocommunicate with Media Services.</span></span> 
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="e98b0-153">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="e98b0-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e98b0-154">Отзывы</span><span class="sxs-lookup"><span data-stu-id="e98b0-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

