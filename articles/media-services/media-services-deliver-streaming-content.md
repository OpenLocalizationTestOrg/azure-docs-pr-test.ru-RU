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
# <a name="publish-azure-media-services-content-using-net"></a>Публикация содержимого служб мультимедиа Azure с помощью .NET
> [!div class="op_single_selector"]
> * [REST](media-services-rest-deliver-streaming-content.md)
> * [.NET](media-services-deliver-streaming-content.md)
> * [Портал](media-services-portal-publish.md)
> 
> 

## <a name="overview"></a>Обзор
Вы можете осуществлять потоковую передачу набора MP4-файлов с адаптивной скоростью, создавая указатель потоковой передачи OnDemand и формируя URL-адрес потоковой передачи. Hello [кодирование актива](media-services-encode-asset.md) разделе показано, как задать tooencode в MP4 с адаптивной скоростью. 

> [!NOTE]
> Если содержимое шифруется, то перед созданием указателя настройте политику доставки ресурсов-контейнеров (как описано в [этой](media-services-dotnet-configure-asset-delivery-policy.md) статье). 
> 
> 

Также можно использовать OnDemand streaming URL toobuild этой точки tooMP4 файлы, которые могут быть загружены постепенно.  

В этом разделе показано, как toocreate OnDemand потоковой передачи toopublish локатора актива и построения Smooth, MPEG DASH и HLS URL-адреса потоковой передачи. Он также показывает горячей toobuild URL-адресов прогрессивной загрузки. 

## <a name="create-an-ondemand-streaming-locator"></a>Создание указателя потоковой передачи OnDemand
toocreate hello указатель потоковой передачи по запросу и получить URL-адреса, вы должны hello toodo следующие действия:

1. При шифровании содержимого hello определите политику доступа.
2. создать указатель потоковой передачи OnDemand.
3. Если планируется toostream получите hello потоковой передачи файла манифеста (.ism) в ресурсе hello. 
   
   Если планируется tooprogressively загрузки, получите имена hello MP4-файлов в ресурсе hello.  
4. Создавать файл манифеста toohello URL-адреса или MP4-файлов. 


>[!NOTE]
>Действует ограничение в 1 000 000 записей для разных политик AMS (например, для политики Locator или ContentKeyAuthorizationPolicy). Используйте hello же идентификатор политики, если вы используете всегда hello же дней или разрешения на доступ. Например политики для указателей, которые являются предназначен tooremain на месте в течение длительного времени (без передачи политики). Чтобы узнать больше, ознакомьтесь с [этим](media-services-dotnet-manage-entities.md#limit-access-policies) разделом.

### <a name="use-media-services-net-sdk"></a>Использование пакета SDK служб мультимедиа для .NET
Создание URL-адресов потоковой передачи 

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

Hello выходные данные:

    URL toomanifest for client streaming using Smooth Streaming protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest
    URL toomanifest for client streaming using HLS protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=m3u8-aapl)
    URL toomanifest for client streaming using MPEG DASH protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=mpd-time-csf)


> [!NOTE]
> Также по SSL-подключению можно выполнять потоковую передачу содержимого. toodo это подход, убедитесь, что потоковой передачи запуска URL-адреса с помощью протокола HTTPS. Сейчас AMS не поддерживает SSL для личных доменов.
> 
> 

Создание URL-адресов последовательного скачивания 

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

Hello выходные данные:

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4

    . . . 

### <a name="use-media-services-net-sdk-extensions"></a>Использование расширения пакета SDK служб мультимедиа для .NET
Hello следующий код вызывает методы расширения пакета SDK для .NET, создать указатель, а также создавать hello Smooth Streaming, HLS и MPEG-DASH URL-адреса для адаптивной потоковой передачи.

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


## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Дальнейшие действия
* [Скачивание файлов](media-services-deliver-asset-download.md)
* [Настройка политики доставки для ресурса-контейнера](media-services-dotnet-configure-asset-delivery-policy.md)

