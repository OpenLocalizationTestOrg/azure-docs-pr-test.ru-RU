---
title: "Создание фильтров с помощью пакета SDK для .NET служб мультимедиа Azure"
description: "В этом разделе описывается создание фильтров, с помощью которых клиент может передавать определенные секции потока. Для достижения такой выборочной потоковой передачи службы мультимедиа создают динамические манифесты."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 2f6894ca-fb43-43c0-9151-ddbb2833cafd
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 07/21/2017
ms.author: juliako;cenkdin
ms.openlocfilehash: 6c43473b86c14679ace558de478bd95f41d476da
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="creating-filters-with-azure-media-services-net-sdk"></a><span data-ttu-id="4647c-104">Создание фильтров с помощью пакета SDK для .NET служб мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="4647c-104">Creating Filters with Azure Media Services .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4647c-105">.NET</span><span class="sxs-lookup"><span data-stu-id="4647c-105">.NET</span></span>](media-services-dotnet-dynamic-manifest.md)
> * [<span data-ttu-id="4647c-106">REST</span><span class="sxs-lookup"><span data-stu-id="4647c-106">REST</span></span>](media-services-rest-dynamic-manifest.md)
> 
> 

<span data-ttu-id="4647c-107">Начиная с версии 2.11, службы мультимедиа позволяют определять фильтры для активов.</span><span class="sxs-lookup"><span data-stu-id="4647c-107">Starting with 2.11 release, Media Services enables you to define filters for your assets.</span></span> <span data-ttu-id="4647c-108">Эти фильтры представляют собой правила на стороне сервера, позволяющие пользователям выполнять следующие действия: воспроизведение только части видео (вместо целого) или указание подмножества представлений аудио и видео, которые может обрабатывать устройство клиента (вместо всех представлений, связанных с активом).</span><span class="sxs-lookup"><span data-stu-id="4647c-108">These filters are server side rules that will allow your customers to choose to do things like: playback only a section of a video (instead of playing the whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all the renditions that are associated with the asset).</span></span> <span data-ttu-id="4647c-109">Такая фильтрация активов достигается с помощью **динамических манифестов**, которые создаются по запросу клиента для потоковой передачи видео на основе указанных фильтров.</span><span class="sxs-lookup"><span data-stu-id="4647c-109">This filtering of your assets is achieved through **Dynamic Manifest**s that are created upon your customer's request to stream a video based on specified filter(s).</span></span>

<span data-ttu-id="4647c-110">Подробные сведения о фильтрах и динамическом манифесте см. в статье [Фильтры и динамические манифесты](media-services-dynamic-manifest-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4647c-110">For more detailed information related to filters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span></span>

<span data-ttu-id="4647c-111">В этом разделе показано, как использовать пакет SDK .NET служб мультимедиа для создания, обновления и удаления фильтров.</span><span class="sxs-lookup"><span data-stu-id="4647c-111">This topic shows how to use Media Services .NET SDK to create, update, and delete filters.</span></span> 

<span data-ttu-id="4647c-112">Обратите внимание, что при обновлении фильтра может понадобиться до 2 минут на обновление правил конечной точкой потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="4647c-112">Note if you update a filter, it can take up to 2 minutes for streaming endpoint to refresh the rules.</span></span> <span data-ttu-id="4647c-113">Если содержимое было обработано с помощью данного фильтра (и кэшировано на прокси-серверах и в кэшах CDN), обновление этого фильтра может привести к сбоям проигрывателя.</span><span class="sxs-lookup"><span data-stu-id="4647c-113">If the content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span></span> <span data-ttu-id="4647c-114">Рекомендуется очистить кэш после обновления фильтра.</span><span class="sxs-lookup"><span data-stu-id="4647c-114">It is recommend to clear the cache after updating the filter.</span></span> <span data-ttu-id="4647c-115">Если такой вариант невозможен, рассмотрите возможность использования другого фильтра.</span><span class="sxs-lookup"><span data-stu-id="4647c-115">If this option is not possible, consider using a different filter.</span></span> 

## <a name="types-used-to-create-filters"></a><span data-ttu-id="4647c-116">Типы, используемые для создания фильтров</span><span class="sxs-lookup"><span data-stu-id="4647c-116">Types used to create filters</span></span>
<span data-ttu-id="4647c-117">При создании фильтров используются следующие типы:</span><span class="sxs-lookup"><span data-stu-id="4647c-117">The following types are used when creating filters:</span></span> 

* <span data-ttu-id="4647c-118">**IStreamingFilter**.</span><span class="sxs-lookup"><span data-stu-id="4647c-118">**IStreamingFilter**.</span></span>  <span data-ttu-id="4647c-119">В основе этого типа лежит следующий интерфейс API REST: [Filter](https://docs.microsoft.com/rest/api/media/operations/filter)</span><span class="sxs-lookup"><span data-stu-id="4647c-119">This type is based on the following REST API [Filter](https://docs.microsoft.com/rest/api/media/operations/filter)</span></span>
* <span data-ttu-id="4647c-120">**IStreamingAssetFilter**.</span><span class="sxs-lookup"><span data-stu-id="4647c-120">**IStreamingAssetFilter**.</span></span> <span data-ttu-id="4647c-121">В основе этого типа лежит следующий интерфейс API REST: [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)</span><span class="sxs-lookup"><span data-stu-id="4647c-121">This type is based on the following REST API [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)</span></span>
* <span data-ttu-id="4647c-122">**PresentationTimeRange**.</span><span class="sxs-lookup"><span data-stu-id="4647c-122">**PresentationTimeRange**.</span></span> <span data-ttu-id="4647c-123">В основе этого типа лежит следующий интерфейс API REST: [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)</span><span class="sxs-lookup"><span data-stu-id="4647c-123">This type is based on the following REST API [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)</span></span>
* <span data-ttu-id="4647c-124">**FilterTrackSelectStatement** и **IFilterTrackPropertyCondition**.</span><span class="sxs-lookup"><span data-stu-id="4647c-124">**FilterTrackSelectStatement** and **IFilterTrackPropertyCondition**.</span></span> <span data-ttu-id="4647c-125">В основе этих типов лежат следующие интерфейсы API REST: [FilterTrackSelect и FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)</span><span class="sxs-lookup"><span data-stu-id="4647c-125">These types are based on the following REST APIs [FilterTrackSelect and FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)</span></span>

## <a name="createupdatereaddelete-global-filters"></a><span data-ttu-id="4647c-126">Создание, обновление, чтение и удаление глобальных фильтров</span><span class="sxs-lookup"><span data-stu-id="4647c-126">Create/Update/Read/Delete global filters</span></span>
<span data-ttu-id="4647c-127">Следующий код демонстрирует, как использовать .NET для создания, обновления, чтения и удаления фильтров ресурсов-контейнеров.</span><span class="sxs-lookup"><span data-stu-id="4647c-127">The following code shows how to use .NET to create, update,read, and delete asset filters.</span></span>

    string filterName = "GlobalFilter_" + Guid.NewGuid().ToString();

    List<FilterTrackSelectStatement> filterTrackSelectStatements = new List<FilterTrackSelectStatement>();

    FilterTrackSelectStatement filterTrackSelectStatement = new FilterTrackSelectStatement();
    filterTrackSelectStatement.PropertyConditions = new List<IFilterTrackPropertyCondition>();
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackNameCondition("Track Name", FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackBitrateRangeCondition(new FilterTrackBitrateRange(0, 1), FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackTypeCondition(FilterTrackType.Audio, FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatements.Add(filterTrackSelectStatement);

    // Create
    IStreamingFilter filter = _context.Filters.Create(filterName, new PresentationTimeRange(), filterTrackSelectStatements);

    // Update
    filter.PresentationTimeRange = new PresentationTimeRange(timescale: 500);
    filter.Update();

    // Read
    var filterUpdated = _context.Filters.FirstOrDefault();
    Console.WriteLine(filterUpdated.Name);

    // Delete
    filter.Delete();


## <a name="createupdatereaddelete-asset-filters"></a><span data-ttu-id="4647c-128">Создание, обновление, чтение и удаление фильтров ресурсов-контейнеров</span><span class="sxs-lookup"><span data-stu-id="4647c-128">Create/Update/Read/Delete asset filters</span></span>
<span data-ttu-id="4647c-129">Следующий код демонстрирует, как использовать .NET для создания, обновления, чтения и удаления фильтров ресурсов-контейнеров.</span><span class="sxs-lookup"><span data-stu-id="4647c-129">The following code shows how to use .NET to create, update,read, and delete asset filters.</span></span>

    string assetName = "AssetFilter_" + Guid.NewGuid().ToString();
    var asset = _context.Assets.Create(assetName, AssetCreationOptions.None);

    string filterName = "AssetFilter_" + Guid.NewGuid().ToString();


    // Create
    IStreamingAssetFilter filter = asset.AssetFilters.Create(filterName,
                                        new PresentationTimeRange(), 
                                        new List<FilterTrackSelectStatement>());

    // Update
    filter.PresentationTimeRange = 
            new PresentationTimeRange(start: 6000000000, end: 72000000000);

    filter.Update();

    // Read
    asset = _context.Assets.Where(c => c.Id == asset.Id).FirstOrDefault();
    var filterUpdated = asset.AssetFilters.FirstOrDefault();
    Console.WriteLine(filterUpdated.Name);

    // Delete
    filterUpdated.Delete();




## <a name="build-streaming-urls-that-use-filters"></a><span data-ttu-id="4647c-130">Построение URL-адресов потоковой передачи с использованием фильтров</span><span class="sxs-lookup"><span data-stu-id="4647c-130">Build streaming URLs that use filters</span></span>
<span data-ttu-id="4647c-131">Сведения о публикации и доставке ресурсов см. в статье [Доставка содержимого клиентам](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4647c-131">For information on how to publish and deliver your assets, see [Delivering Content to Customers Overview](media-services-deliver-content-overview.md).</span></span>

<span data-ttu-id="4647c-132">Следующие примеры показывают, как добавлять фильтры к URL-адресам потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="4647c-132">The following examples show how to add filters to your streaming URLs.</span></span>

<span data-ttu-id="4647c-133">**MPEG DASH**</span><span class="sxs-lookup"><span data-stu-id="4647c-133">**MPEG DASH**</span></span> 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

<span data-ttu-id="4647c-134">**Apple HTTP Live Streaming (HLS) V4**</span><span class="sxs-lookup"><span data-stu-id="4647c-134">**Apple HTTP Live Streaming (HLS) V4**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

<span data-ttu-id="4647c-135">**Apple HTTP Live Streaming (HLS) V3**</span><span class="sxs-lookup"><span data-stu-id="4647c-135">**Apple HTTP Live Streaming (HLS) V3**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

<span data-ttu-id="4647c-136">**Smooth Streaming**</span><span class="sxs-lookup"><span data-stu-id="4647c-136">**Smooth Streaming**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)


## <a name="media-services-learning-paths"></a><span data-ttu-id="4647c-137">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="4647c-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4647c-138">Отзывы</span><span class="sxs-lookup"><span data-stu-id="4647c-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="4647c-139">См. также</span><span class="sxs-lookup"><span data-stu-id="4647c-139">See Also</span></span>
[<span data-ttu-id="4647c-140">Обзор динамических манифестов</span><span class="sxs-lookup"><span data-stu-id="4647c-140">Dynamic manifests overview</span></span>](media-services-dynamic-manifest-overview.md)

