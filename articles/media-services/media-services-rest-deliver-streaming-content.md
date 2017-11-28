---
title: "Публикация содержимого служб мультимедиа Azure с помощью REST"
description: "Узнайте, как создать указатель для создания URL-адреса потоковой передачи. Код использует REST API."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: ff332c30-30c6-4ed1-99d0-5fffd25d4f23
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: d1e0a112040f6aa4cfa9e8c323507b1c0a223f3e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="publish-azure-media-services-content-using-rest"></a><span data-ttu-id="a9bf7-104">Публикация содержимого служб мультимедиа Azure с помощью REST</span><span class="sxs-lookup"><span data-stu-id="a9bf7-104">Publish Azure Media Services content using REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a9bf7-105">.NET</span><span class="sxs-lookup"><span data-stu-id="a9bf7-105">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="a9bf7-106">REST</span><span class="sxs-lookup"><span data-stu-id="a9bf7-106">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> * [<span data-ttu-id="a9bf7-107">Портал</span><span class="sxs-lookup"><span data-stu-id="a9bf7-107">Portal</span></span>](media-services-portal-publish.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="a9bf7-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="a9bf7-108">Overview</span></span>
<span data-ttu-id="a9bf7-109">Вы можете осуществлять потоковую передачу набора MP4-файлов с адаптивной скоростью, создавая указатель потоковой передачи OnDemand и формируя URL-адрес потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="a9bf7-109">You can stream an adaptive bitrate MP4 set by creating an OnDemand streaming locator and building a streaming URL.</span></span> <span data-ttu-id="a9bf7-110">В разделе, посвященном [кодированию ресурса](media-services-rest-encode-asset.md) , описано кодирование данных в набор MP4-файлов с переменной скоростью.</span><span class="sxs-lookup"><span data-stu-id="a9bf7-110">The [encoding an asset](media-services-rest-encode-asset.md) topic shows how to encode into an adaptive bitrate MP4 set.</span></span> <span data-ttu-id="a9bf7-111">Если содержимое шифруется, то перед созданием указателя настройте политику доставки ресурсов-контейнеров (как описано в [этой](media-services-rest-configure-asset-delivery-policy.md) статье).</span><span class="sxs-lookup"><span data-stu-id="a9bf7-111">If your content is encrypted, configure asset delivery policy (as described in [this](media-services-rest-configure-asset-delivery-policy.md) topic) before creating a locator.</span></span> 

<span data-ttu-id="a9bf7-112">Можно также использовать указатель потоковой передачи OnDemand, чтобы формировать URL-адреса, указывающие на MP4-файлы для последовательного скачивания.</span><span class="sxs-lookup"><span data-stu-id="a9bf7-112">You can also use an OnDemand streaming locator to build URLs that point to MP4 files that can be progressively downloaded.</span></span>  

<span data-ttu-id="a9bf7-113">В этом разделе показано, как создать указатель потоковой передачи OnDemand, чтобы опубликовать ресурс-контейнер и сформировать URL-адреса потоковой передачи Smooth, MPEG DASH и HLS.</span><span class="sxs-lookup"><span data-stu-id="a9bf7-113">This topic shows how to create an OnDemand streaming locator in order to publish your asset and build a Smooth, MPEG DASH, and HLS streaming URLs.</span></span> <span data-ttu-id="a9bf7-114">В нем также показывается, как создать URL-адреса последовательного скачивания.</span><span class="sxs-lookup"><span data-stu-id="a9bf7-114">It also shows hot to build progressive download URLs.</span></span>

<span data-ttu-id="a9bf7-115">В [этих](#types) разделах показаны типы перечисления, значения которых используются в вызовах REST.</span><span class="sxs-lookup"><span data-stu-id="a9bf7-115">The [following](#types) section shows the enum types whose values are used in the REST calls.</span></span>   

> [!NOTE]
> <span data-ttu-id="a9bf7-116">При доступе к сущностям в службах мультимедиа необходимо задать определенные поля и значения заголовков в HTTP-запросах.</span><span class="sxs-lookup"><span data-stu-id="a9bf7-116">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="a9bf7-117">Дополнительную информацию см. в статье [Обзор интерфейса REST API служб мультимедиа](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="a9bf7-117">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 

## <a name="connect-to-media-services"></a><span data-ttu-id="a9bf7-118">Подключение к службам мультимедиа</span><span class="sxs-lookup"><span data-stu-id="a9bf7-118">Connect to Media Services</span></span>

<span data-ttu-id="a9bf7-119">Сведения о подключении к API AMS см. в разделе [Доступ к API служб мультимедиа Azure с помощью аутентификации Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="a9bf7-119">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="a9bf7-120">После успешного подключения к https://media.windows.net вы получите ошибку 301 (перенаправление), в которой будет указан другой URI служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="a9bf7-120">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="a9bf7-121">Используйте для последующих вызовов новый URI.</span><span class="sxs-lookup"><span data-stu-id="a9bf7-121">You must make subsequent calls to the new URI.</span></span>

## <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="a9bf7-122">Создание указателя потоковой передачи OnDemand</span><span class="sxs-lookup"><span data-stu-id="a9bf7-122">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="a9bf7-123">Чтобы создать указатель потоковой передачи OnDemand и получить URL-адреса, вам нужно выполнить следующее:</span><span class="sxs-lookup"><span data-stu-id="a9bf7-123">To create the OnDemand streaming locator and get URLs you need to do the following:</span></span>

1. <span data-ttu-id="a9bf7-124">Если содержимое шифруется, установите политику доступа.</span><span class="sxs-lookup"><span data-stu-id="a9bf7-124">If the content is encrypted, define an access policy.</span></span>
2. <span data-ttu-id="a9bf7-125">создать указатель потоковой передачи OnDemand.</span><span class="sxs-lookup"><span data-stu-id="a9bf7-125">Create an OnDemand streaming locator.</span></span>
3. <span data-ttu-id="a9bf7-126">Если планируется потоковая передача, получите файл манифеста потоковой передачи (ISM-файл) в ресурсе.</span><span class="sxs-lookup"><span data-stu-id="a9bf7-126">If you plan to stream, get the streaming manifest file (.ism) in the asset.</span></span> 
   
   <span data-ttu-id="a9bf7-127">Если вы планируете последовательное скачивание, получите имена MP4-файлов в ресурсе.</span><span class="sxs-lookup"><span data-stu-id="a9bf7-127">If you plan to progressively download, get the names of MP4 files in the asset.</span></span> 
4. <span data-ttu-id="a9bf7-128">Создайте URL-адрес файла манифеста или URL-адреса MP4-файлов.</span><span class="sxs-lookup"><span data-stu-id="a9bf7-128">Build URLs to the manifest file or MP4 files.</span></span> 
5. <span data-ttu-id="a9bf7-129">Обратите внимание на то, что указатель потоковой передачи невозможно создать с использованием политики доступа, включающей разрешения на запись или удаление.</span><span class="sxs-lookup"><span data-stu-id="a9bf7-129">Note that you cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.</span></span>

### <a name="create-an-access-policy"></a><span data-ttu-id="a9bf7-130">Создание политики доступа</span><span class="sxs-lookup"><span data-stu-id="a9bf7-130">Create an access policy</span></span>

>[!NOTE]
><span data-ttu-id="a9bf7-131">Действует ограничение в 1 000 000 записей для разных политик AMS (например, для политики Locator или ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="a9bf7-131">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="a9bf7-132">Следует указывать один и тот же идентификатор политики, если вы используете те же дни, разрешения доступа и т. д. Например, политики для указателей, которые должны оставаться на месте в течение длительного времени (не политики передачи).</span><span class="sxs-lookup"><span data-stu-id="a9bf7-132">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="a9bf7-133">Чтобы узнать больше, ознакомьтесь с [этим](media-services-dotnet-manage-entities.md#limit-access-policies) разделом.</span><span class="sxs-lookup"><span data-stu-id="a9bf7-133">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="a9bf7-134">Запрос:</span><span class="sxs-lookup"><span data-stu-id="a9bf7-134">Request:</span></span>

    POST https://media.windows.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstest1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1424263184&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=NWE%2f986Hr5lZTzVGKtC%2ftzHm9n6U%2fxpTFULItxKUGC4%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 6bcfd511-a561-448d-a022-a319a89ecffa
    Host: media.windows.net
    Content-Length: 68

    {"Name":"access policy","DurationInMinutes":43200.0,"Permissions":1}

<span data-ttu-id="a9bf7-135">Ответ:</span><span class="sxs-lookup"><span data-stu-id="a9bf7-135">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 311
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https:/media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3A69c80d98-7830-407f-a9af-e25f4b0d3e5f')
    Server: Microsoft-IIS/8.5
    request-id: a877528a-bdb4-4414-9862-273f8e64f882
    x-ms-request-id: a877528a-bdb4-4414-9862-273f8e64f882
    x-ms-client-request-id: 6bcfd511-a561-448d-a022-a319a89ecffa
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 18 Feb 2015 06:52:09 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#AccessPolicies/@Element","Id":"nb:pid:UUID:69c80d98-7830-407f-a9af-e25f4b0d3e5f","Created":"2015-02-18T06:52:09.8862191Z","LastModified":"2015-02-18T06:52:09.8862191Z","Name":"access policy","DurationInMinutes":43200.0,"Permissions":1}

### <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="a9bf7-136">Создание указателя потоковой передачи OnDemand</span><span class="sxs-lookup"><span data-stu-id="a9bf7-136">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="a9bf7-137">Создание указателя для указанного ресурса и политики активов.</span><span class="sxs-lookup"><span data-stu-id="a9bf7-137">Create the locator for the specified asset and asset policy.</span></span>

<span data-ttu-id="a9bf7-138">Запрос:</span><span class="sxs-lookup"><span data-stu-id="a9bf7-138">Request:</span></span>

    POST https://media.windows.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstest1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1424263184&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=NWE%2f986Hr5lZTzVGKtC%2ftzHm9n6U%2fxpTFULItxKUGC4%3d
    x-ms-version: 2.11
    x-ms-client-request-id: ac159492-9a0c-40c3-aacc-551b1b4c5f62
    Host: media.windows.net
    Content-Length: 181

    {"AccessPolicyId":"nb:pid:UUID:1480030d-c481-430a-9687-535c6a5cb272","AssetId":"nb:cid:UUID:cc1e445d-1500-80bd-538e-f1e4b71b465e","StartTime":"2015-02-18T06:34:47.267872Z","Type":2}

<span data-ttu-id="a9bf7-139">Ответ:</span><span class="sxs-lookup"><span data-stu-id="a9bf7-139">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 637
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Abe245661-2bbd-4fc6-b14f-9cf9a1492e5e')
    Server: Microsoft-IIS/8.5
    request-id: 5bd5864a-0afd-44c0-a67a-4044a2c9043b
    x-ms-request-id: 5bd5864a-0afd-44c0-a67a-4044a2c9043b
    x-ms-client-request-id: ac159492-9a0c-40c3-aacc-551b1b4c5f62
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 18 Feb 2015 06:58:37 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#Locators/@Element","Id":"nb:lid:UUID:be245661-2bbd-4fc6-b14f-9cf9a1492e5e","ExpirationDateTime":"2015-03-20T06:34:47.267872+00:00","Type":2,"Path":"http://amstest1.streaming.mediaservices.windows.net/be245661-2bbd-4fc6-b14f-9cf9a1492e5e/","BaseUri":"http://amstest1.streaming.mediaservices.windows.net","ContentAccessComponent":"be245661-2bbd-4fc6-b14f-9cf9a1492e5e","AccessPolicyId":"nb:pid:UUID:1480030d-c481-430a-9687-535c6a5cb272","AssetId":"nb:cid:UUID:cc1e445d-1500-80bd-538e-f1e4b71b465e","StartTime":"2015-02-18T06:34:47.267872+00:00","Name":null}

### <a name="build-streaming-urls"></a><span data-ttu-id="a9bf7-140">Создание URL-адресов потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="a9bf7-140">Build streaming URLs</span></span>
<span data-ttu-id="a9bf7-141">Для построения URL-адресов Smooth, HLS и MPEG DASH используется значение **Путь** , возвращаемое после создания указателя.</span><span class="sxs-lookup"><span data-stu-id="a9bf7-141">Use the **Path** value returned after the creation of the locator to build the Smooth, HLS, and MPEG DASH URLs.</span></span> 

<span data-ttu-id="a9bf7-142">Smooth Streaming: **Путь** + имя файла манифеста + "/manifest"</span><span class="sxs-lookup"><span data-stu-id="a9bf7-142">Smooth Streaming: **Path** + manifest file name + "/manifest"</span></span>

<span data-ttu-id="a9bf7-143">Пример:</span><span class="sxs-lookup"><span data-stu-id="a9bf7-143">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest

<span data-ttu-id="a9bf7-144">HLS: **Путь** + имя файла манифеста + "/manifest(format=m3u8-aapl)"</span><span class="sxs-lookup"><span data-stu-id="a9bf7-144">HLS: **Path** + manifest file name + "/manifest(format=m3u8-aapl)"</span></span>

<span data-ttu-id="a9bf7-145">Пример:</span><span class="sxs-lookup"><span data-stu-id="a9bf7-145">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=m3u8-aapl)


<span data-ttu-id="a9bf7-146">DASH: **Путь** + имя файла манифеста + "/manifest(format=mpd-time-csf)"</span><span class="sxs-lookup"><span data-stu-id="a9bf7-146">DASH: **Path** + manifest file name + "/manifest(format=mpd-time-csf)"</span></span>

<span data-ttu-id="a9bf7-147">Пример:</span><span class="sxs-lookup"><span data-stu-id="a9bf7-147">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=mpd-time-csf)


### <a name="build-progressive-download-urls"></a><span data-ttu-id="a9bf7-148">Создание URL-адресов последовательного скачивания</span><span class="sxs-lookup"><span data-stu-id="a9bf7-148">Build progressive download URLs</span></span>
<span data-ttu-id="a9bf7-149">Для построения URL-адреса поэтапного скачивания используется значение **Путь** , возвращаемое после создания указателя.</span><span class="sxs-lookup"><span data-stu-id="a9bf7-149">Use the **Path** value returned after the creation of the locator to build the progressive download URL.</span></span>   

<span data-ttu-id="a9bf7-150">URL: **Путь** + имя MP4-файла ресурса</span><span class="sxs-lookup"><span data-stu-id="a9bf7-150">URL: **Path** + asset file mp4 name</span></span>

<span data-ttu-id="a9bf7-151">Пример:</span><span class="sxs-lookup"><span data-stu-id="a9bf7-151">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

## <span data-ttu-id="a9bf7-152"><a id="types"></a>Типы перечислений</span><span class="sxs-lookup"><span data-stu-id="a9bf7-152"><a id="types"></a>Enum types</span></span>
    [Flags]
    public enum AccessPermissions
    {
        None = 0,
        Read = 1,
        Write = 2,
        Delete = 4,
        List = 8,
    }

    public enum LocatorType
    {
        None = 0,
        Sas = 1,
        OnDemandOrigin = 2,
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="a9bf7-153">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="a9bf7-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a9bf7-154">Отзывы</span><span class="sxs-lookup"><span data-stu-id="a9bf7-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="a9bf7-155">См. также</span><span class="sxs-lookup"><span data-stu-id="a9bf7-155">See also</span></span>
[<span data-ttu-id="a9bf7-156">Обзор REST API операций служб мультимедиа</span><span class="sxs-lookup"><span data-stu-id="a9bf7-156">Media Services operations REST API overview</span></span>](media-services-rest-how-to-use.md)

[<span data-ttu-id="a9bf7-157">Настройка политики доставки для ресурса-контейнера</span><span class="sxs-lookup"><span data-stu-id="a9bf7-157">Configure asset delivery policy</span></span>](media-services-rest-configure-asset-delivery-policy.md)

