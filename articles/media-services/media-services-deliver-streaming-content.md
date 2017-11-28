---
title: "aaaPublish содержимого служб мультимедиа Azure, с помощью .NET | Документы Microsoft"
description: "Узнайте, как toocreate в указатель, который будет использоваться toobuild URL-адрес потоковой передачи. Примеры кода на языке C# и используйте hello пакета SDK служб мультимедиа для .NET."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: c53b1f83-4cb1-4b09-840f-9c145b7d6f8d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: c941cd93c252a96e66546cce2793bb426afac059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="publish-azure-media-services-content-using-net"></a><span data-ttu-id="5c969-104">Публикация содержимого служб мультимедиа Azure с помощью .NET</span><span class="sxs-lookup"><span data-stu-id="5c969-104">Publish Azure Media Services content using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5c969-105">REST</span><span class="sxs-lookup"><span data-stu-id="5c969-105">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> * [<span data-ttu-id="5c969-106">.NET</span><span class="sxs-lookup"><span data-stu-id="5c969-106">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="5c969-107">Портал</span><span class="sxs-lookup"><span data-stu-id="5c969-107">Portal</span></span>](media-services-portal-publish.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="5c969-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="5c969-108">Overview</span></span>
<span data-ttu-id="5c969-109">Вы можете осуществлять потоковую передачу набора MP4-файлов с адаптивной скоростью, создавая указатель потоковой передачи OnDemand и формируя URL-адрес потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="5c969-109">You can stream an adaptive bitrate MP4 set by creating an OnDemand streaming locator and building a streaming URL.</span></span> <span data-ttu-id="5c969-110">Hello [кодирование актива](media-services-encode-asset.md) разделе показано, как задать tooencode в MP4 с адаптивной скоростью.</span><span class="sxs-lookup"><span data-stu-id="5c969-110">hello [encoding an asset](media-services-encode-asset.md) topic shows how tooencode into an adaptive bitrate MP4 set.</span></span> 

> [!NOTE]
> <span data-ttu-id="5c969-111">Если содержимое шифруется, то перед созданием указателя настройте политику доставки ресурсов-контейнеров (как описано в [этой](media-services-dotnet-configure-asset-delivery-policy.md) статье).</span><span class="sxs-lookup"><span data-stu-id="5c969-111">If your content is encrypted, configure asset delivery policy (as described in [this](media-services-dotnet-configure-asset-delivery-policy.md) topic) before creating a locator.</span></span> 
> 
> 

<span data-ttu-id="5c969-112">Также можно использовать OnDemand streaming URL toobuild этой точки tooMP4 файлы, которые могут быть загружены постепенно.</span><span class="sxs-lookup"><span data-stu-id="5c969-112">You can also use an OnDemand streaming locator toobuild URLs that point tooMP4 files that can be progressively downloaded.</span></span>  

<span data-ttu-id="5c969-113">В этом разделе показано, как toocreate OnDemand потоковой передачи toopublish локатора актива и построения Smooth, MPEG DASH и HLS URL-адреса потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="5c969-113">This topic shows how toocreate an OnDemand streaming locator toopublish your asset and build a Smooth, MPEG DASH, and HLS streaming URLs.</span></span> <span data-ttu-id="5c969-114">Он также показывает горячей toobuild URL-адресов прогрессивной загрузки.</span><span class="sxs-lookup"><span data-stu-id="5c969-114">It also shows hot toobuild progressive download URLs.</span></span> 

## <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="5c969-115">Создание указателя потоковой передачи OnDemand</span><span class="sxs-lookup"><span data-stu-id="5c969-115">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="5c969-116">toocreate hello указатель потоковой передачи по запросу и получить URL-адреса, вы должны hello toodo следующие действия:</span><span class="sxs-lookup"><span data-stu-id="5c969-116">toocreate hello OnDemand streaming locator and get URLs, you need toodo hello following things:</span></span>

1. <span data-ttu-id="5c969-117">При шифровании содержимого hello определите политику доступа.</span><span class="sxs-lookup"><span data-stu-id="5c969-117">If hello content is encrypted, define an access policy.</span></span>
2. <span data-ttu-id="5c969-118">создать указатель потоковой передачи OnDemand.</span><span class="sxs-lookup"><span data-stu-id="5c969-118">Create an OnDemand streaming locator.</span></span>
3. <span data-ttu-id="5c969-119">Если планируется toostream получите hello потоковой передачи файла манифеста (.ism) в ресурсе hello.</span><span class="sxs-lookup"><span data-stu-id="5c969-119">If you plan toostream, get hello streaming manifest file (.ism) in hello asset.</span></span> 
   
   <span data-ttu-id="5c969-120">Если планируется tooprogressively загрузки, получите имена hello MP4-файлов в ресурсе hello.</span><span class="sxs-lookup"><span data-stu-id="5c969-120">If you plan tooprogressively download, get hello names of MP4 files in hello asset.</span></span>  
4. <span data-ttu-id="5c969-121">Создавать файл манифеста toohello URL-адреса или MP4-файлов.</span><span class="sxs-lookup"><span data-stu-id="5c969-121">Build URLs toohello manifest file or MP4 files.</span></span> 


>[!NOTE]
><span data-ttu-id="5c969-122">Действует ограничение в 1 000 000 записей для разных политик AMS (например, для политики Locator или ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="5c969-122">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="5c969-123">Используйте hello же идентификатор политики, если вы используете всегда hello же дней или разрешения на доступ.</span><span class="sxs-lookup"><span data-stu-id="5c969-123">Use hello same policy ID if you are always using hello same days / access permissions.</span></span> <span data-ttu-id="5c969-124">Например политики для указателей, которые являются предназначен tooremain на месте в течение длительного времени (без передачи политики).</span><span class="sxs-lookup"><span data-stu-id="5c969-124">For example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="5c969-125">Чтобы узнать больше, ознакомьтесь с [этим](media-services-dotnet-manage-entities.md#limit-access-policies) разделом.</span><span class="sxs-lookup"><span data-stu-id="5c969-125">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

### <a name="use-media-services-net-sdk"></a><span data-ttu-id="5c969-126">Использование пакета SDK служб мультимедиа для .NET</span><span class="sxs-lookup"><span data-stu-id="5c969-126">Use Media Services .NET SDK</span></span>
<span data-ttu-id="5c969-127">Создание URL-адресов потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="5c969-127">Build Streaming URLs</span></span> 

    private static void BuildStreamingURLs(IAsset asset)
    {

        // Create a 30-day readonly access policy. 
          // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.
        IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

        // Create a locator toohello streaming content on an origin. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

        // Display some useful values based on hello locator.
        Console.WriteLine("Streaming asset base path on origin: ");
        Console.WriteLine(originLocator.Path);
        Console.WriteLine();

        // Get a reference toohello streaming manifest file from hello  
        // collection of files in hello asset. 
        var manifestFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                                    EndsWith(".ism")).
                                    FirstOrDefault();

        // Create a full URL toohello manifest file. Use this for playback
        // in streaming media clients. 
        string urlForClientStreaming = originLocator.Path + manifestFile.Name + "/manifest";
        Console.WriteLine("URL toomanifest for client streaming using Smooth Streaming protocol: ");
        Console.WriteLine(urlForClientStreaming);
        Console.WriteLine("URL toomanifest for client streaming using HLS protocol: ");
        Console.WriteLine(urlForClientStreaming + "(format=m3u8-aapl)");
        Console.WriteLine("URL toomanifest for client streaming using MPEG DASH protocol: ");
        Console.WriteLine(urlForClientStreaming + "(format=mpd-time-csf)"); 
        Console.WriteLine();
    }

<span data-ttu-id="5c969-128">Hello выходные данные:</span><span class="sxs-lookup"><span data-stu-id="5c969-128">hello outputs:</span></span>

    URL toomanifest for client streaming using Smooth Streaming protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest
    URL toomanifest for client streaming using HLS protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=m3u8-aapl)
    URL toomanifest for client streaming using MPEG DASH protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=mpd-time-csf)


> [!NOTE]
> <span data-ttu-id="5c969-129">Также по SSL-подключению можно выполнять потоковую передачу содержимого.</span><span class="sxs-lookup"><span data-stu-id="5c969-129">You can also stream your content over an SSL connection.</span></span> <span data-ttu-id="5c969-130">toodo это подход, убедитесь, что потоковой передачи запуска URL-адреса с помощью протокола HTTPS.</span><span class="sxs-lookup"><span data-stu-id="5c969-130">toodo this approach, make sure your streaming URLs start with HTTPS.</span></span> <span data-ttu-id="5c969-131">Сейчас AMS не поддерживает SSL для личных доменов.</span><span class="sxs-lookup"><span data-stu-id="5c969-131">Currently, AMS doesn’t support SSL with custom domains.</span></span>
> 
> 

<span data-ttu-id="5c969-132">Создание URL-адресов последовательного скачивания</span><span class="sxs-lookup"><span data-stu-id="5c969-132">Build progressive download URLs</span></span> 

    private static void BuildProgressiveDownloadURLs(IAsset asset)
    {
        // Create a 30-day readonly access policy. 
        IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

        // Create an OnDemandOrigin locator toohello asset. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

        // Display some useful values based on hello locator.
        Console.WriteLine("Streaming asset base path on origin: ");
        Console.WriteLine(originLocator.Path);
        Console.WriteLine();

        // Get MP4 files.
        IEnumerable<IAssetFile> mp4AssetFiles = asset
            .AssetFiles
            .ToList()
            .Where(af => af.Name.EndsWith(".mp4", StringComparison.OrdinalIgnoreCase));

        // Create a full URL toohello MP4 files. Use this tooprogressively download files.
        foreach (var pd in mp4AssetFiles)
            Console.WriteLine(originLocator.Path + pd.Name);
    }

<span data-ttu-id="5c969-133">Hello выходные данные:</span><span class="sxs-lookup"><span data-stu-id="5c969-133">hello outputs:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4

    . . . 

### <a name="use-media-services-net-sdk-extensions"></a><span data-ttu-id="5c969-134">Использование расширения пакета SDK служб мультимедиа для .NET</span><span class="sxs-lookup"><span data-stu-id="5c969-134">Use Media Services .NET SDK Extensions</span></span>
<span data-ttu-id="5c969-135">Hello следующий код вызывает методы расширения пакета SDK для .NET, создать указатель, а также создавать hello Smooth Streaming, HLS и MPEG-DASH URL-адреса для адаптивной потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="5c969-135">hello following code calls .NET SDK extensions methods that create a locator and generate hello Smooth Streaming, HLS, and MPEG-DASH URLs for adaptive streaming.</span></span>

    // Create a loctor.
    _context.Locators.Create(
        LocatorType.OnDemandOrigin,
        inputAsset,
        AccessPermissions.Read,
        TimeSpan.FromDays(30));

    // Get hello streaming URLs.
    Uri smoothStreamingUri = inputAsset.GetSmoothStreamingUri();
    Uri hlsUri = inputAsset.GetHlsUri();
    Uri mpegDashUri = inputAsset.GetMpegDashUri();

    Console.WriteLine(smoothStreamingUri);
    Console.WriteLine(hlsUri);
    Console.WriteLine(mpegDashUri);


## <a name="media-services-learning-paths"></a><span data-ttu-id="5c969-136">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="5c969-136">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5c969-137">Отзывы</span><span class="sxs-lookup"><span data-stu-id="5c969-137">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="5c969-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5c969-138">Next steps</span></span>
* [<span data-ttu-id="5c969-139">Скачивание файлов</span><span class="sxs-lookup"><span data-stu-id="5c969-139">Download assets</span></span>](media-services-deliver-asset-download.md)
* [<span data-ttu-id="5c969-140">Настройка политики доставки для ресурса-контейнера</span><span class="sxs-lookup"><span data-stu-id="5c969-140">Configure asset delivery policy</span></span>](media-services-dotnet-configure-asset-delivery-policy.md)

