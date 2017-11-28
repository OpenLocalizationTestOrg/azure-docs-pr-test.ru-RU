---
title: "Фильтры aaaCreating с Azure Media Services .NET SDK"
description: "Описывается, как фильтры toocreate, поэтому клиент может их использовать toostream определенных разделов потока. Службы мультимедиа создает динамические манифесты tooachieve Выборочный streaming."
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
ms.openlocfilehash: 16d9497d48ab1d3f841dd97efb0f66016a2435c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="creating-filters-with-azure-media-services-net-sdk"></a><span data-ttu-id="84642-104">Создание фильтров с помощью пакета SDK для .NET служб мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="84642-104">Creating Filters with Azure Media Services .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="84642-105">.NET</span><span class="sxs-lookup"><span data-stu-id="84642-105">.NET</span></span>](media-services-dotnet-dynamic-manifest.md)
> * [<span data-ttu-id="84642-106">REST</span><span class="sxs-lookup"><span data-stu-id="84642-106">REST</span></span>](media-services-rest-dynamic-manifest.md)
> 
> 

<span data-ttu-id="84642-107">Начиная с выпуска 2.11, службы мультимедиа позволяют фильтры toodefine средств.</span><span class="sxs-lookup"><span data-stu-id="84642-107">Starting with 2.11 release, Media Services enables you toodefine filters for your assets.</span></span> <span data-ttu-id="84642-108">Эти фильтры являются правила стороне сервера, позволяющие клиентам toochoose toodo таких вещей, как: воспроизведения только части видео (вместо воспроизведение hello всего видео), или укажите только набор представлений аудио и видео обработки (устройства клиента вместо всех hello представлений, которые связаны с активом hello).</span><span class="sxs-lookup"><span data-stu-id="84642-108">These filters are server side rules that will allow your customers toochoose toodo things like: playback only a section of a video (instead of playing hello whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all hello renditions that are associated with hello asset).</span></span> <span data-ttu-id="84642-109">Такая фильтрация ресурсов достигается за счет **динамического манифеста**, созданных после toostream запрос клиента видео на основе указанного фильтров.</span><span class="sxs-lookup"><span data-stu-id="84642-109">This filtering of your assets is achieved through **Dynamic Manifest**s that are created upon your customer's request toostream a video based on specified filter(s).</span></span>

<span data-ttu-id="84642-110">Для получения дополнительных сведений см связанные toofilters и динамические манифеста [динамической манифесты Обзор](media-services-dynamic-manifest-overview.md).</span><span class="sxs-lookup"><span data-stu-id="84642-110">For more detailed information related toofilters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span></span>

<span data-ttu-id="84642-111">В этом разделе показано, как toocreate toouse Media Services .NET SDK, обновления и удаления фильтров.</span><span class="sxs-lookup"><span data-stu-id="84642-111">This topic shows how toouse Media Services .NET SDK toocreate, update, and delete filters.</span></span> 

<span data-ttu-id="84642-112">Обратите внимание, если обновить фильтр может занять too2 минут для потоковой передачи конечной точки toorefresh hello правила.</span><span class="sxs-lookup"><span data-stu-id="84642-112">Note if you update a filter, it can take up too2 minutes for streaming endpoint toorefresh hello rules.</span></span> <span data-ttu-id="84642-113">Если содержимое hello был обработан с помощью этого фильтра (и кэширования в прокси-серверы и CDN кэши), обновление этого фильтра может привести к проигрывателя сбоев.</span><span class="sxs-lookup"><span data-stu-id="84642-113">If hello content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span></span> <span data-ttu-id="84642-114">Рекомендуется tooclear hello кэша после обновления hello фильтра.</span><span class="sxs-lookup"><span data-stu-id="84642-114">It is recommend tooclear hello cache after updating hello filter.</span></span> <span data-ttu-id="84642-115">Если такой вариант невозможен, рассмотрите возможность использования другого фильтра.</span><span class="sxs-lookup"><span data-stu-id="84642-115">If this option is not possible, consider using a different filter.</span></span> 

## <a name="types-used-toocreate-filters"></a><span data-ttu-id="84642-116">Использовать фильтры toocreate типы</span><span class="sxs-lookup"><span data-stu-id="84642-116">Types used toocreate filters</span></span>
<span data-ttu-id="84642-117">Hello используются следующие типы при создании фильтров:</span><span class="sxs-lookup"><span data-stu-id="84642-117">hello following types are used when creating filters:</span></span> 

* <span data-ttu-id="84642-118">**IStreamingFilter**.</span><span class="sxs-lookup"><span data-stu-id="84642-118">**IStreamingFilter**.</span></span>  <span data-ttu-id="84642-119">Этот тип основан на следующих API-интерфейса REST hello [фильтра](https://docs.microsoft.com/rest/api/media/operations/filter)</span><span class="sxs-lookup"><span data-stu-id="84642-119">This type is based on hello following REST API [Filter](https://docs.microsoft.com/rest/api/media/operations/filter)</span></span>
* <span data-ttu-id="84642-120">**IStreamingAssetFilter**.</span><span class="sxs-lookup"><span data-stu-id="84642-120">**IStreamingAssetFilter**.</span></span> <span data-ttu-id="84642-121">Этот тип основан на следующих API-интерфейса REST hello [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)</span><span class="sxs-lookup"><span data-stu-id="84642-121">This type is based on hello following REST API [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)</span></span>
* <span data-ttu-id="84642-122">**PresentationTimeRange**.</span><span class="sxs-lookup"><span data-stu-id="84642-122">**PresentationTimeRange**.</span></span> <span data-ttu-id="84642-123">Этот тип основан на следующих API-интерфейса REST hello [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)</span><span class="sxs-lookup"><span data-stu-id="84642-123">This type is based on hello following REST API [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)</span></span>
* <span data-ttu-id="84642-124">**FilterTrackSelectStatement** и **IFilterTrackPropertyCondition**.</span><span class="sxs-lookup"><span data-stu-id="84642-124">**FilterTrackSelectStatement** and **IFilterTrackPropertyCondition**.</span></span> <span data-ttu-id="84642-125">Эти типы основаны на следующих API-интерфейсов REST hello [FilterTrackSelect и FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)</span><span class="sxs-lookup"><span data-stu-id="84642-125">These types are based on hello following REST APIs [FilterTrackSelect and FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)</span></span>

## <a name="createupdatereaddelete-global-filters"></a><span data-ttu-id="84642-126">Создание, обновление, чтение и удаление глобальных фильтров</span><span class="sxs-lookup"><span data-stu-id="84642-126">Create/Update/Read/Delete global filters</span></span>
<span data-ttu-id="84642-127">Hello следующий код показывает, как toouse .NET toocreate, обновления, чтения и удаления фильтров активов.</span><span class="sxs-lookup"><span data-stu-id="84642-127">hello following code shows how toouse .NET toocreate, update,read, and delete asset filters.</span></span>

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


## <a name="createupdatereaddelete-asset-filters"></a><span data-ttu-id="84642-128">Создание, обновление, чтение и удаление фильтров ресурсов-контейнеров</span><span class="sxs-lookup"><span data-stu-id="84642-128">Create/Update/Read/Delete asset filters</span></span>
<span data-ttu-id="84642-129">Hello следующий код показывает, как toouse .NET toocreate, обновления, чтения и удаления фильтров активов.</span><span class="sxs-lookup"><span data-stu-id="84642-129">hello following code shows how toouse .NET toocreate, update,read, and delete asset filters.</span></span>

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




## <a name="build-streaming-urls-that-use-filters"></a><span data-ttu-id="84642-130">Построение URL-адресов потоковой передачи с использованием фильтров</span><span class="sxs-lookup"><span data-stu-id="84642-130">Build streaming URLs that use filters</span></span>
<span data-ttu-id="84642-131">Сведения о toopublish и предоставления имеющихся ресурсов. в статье [доставки содержимого tooCustomers Обзор](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="84642-131">For information on how toopublish and deliver your assets, see [Delivering Content tooCustomers Overview](media-services-deliver-content-overview.md).</span></span>

<span data-ttu-id="84642-132">Hello следующих примерах показано, как tooadd фильтрует tooyour URL-адреса потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="84642-132">hello following examples show how tooadd filters tooyour streaming URLs.</span></span>

<span data-ttu-id="84642-133">**MPEG DASH**</span><span class="sxs-lookup"><span data-stu-id="84642-133">**MPEG DASH**</span></span> 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

<span data-ttu-id="84642-134">**Apple HTTP Live Streaming (HLS) V4**</span><span class="sxs-lookup"><span data-stu-id="84642-134">**Apple HTTP Live Streaming (HLS) V4**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

<span data-ttu-id="84642-135">**Apple HTTP Live Streaming (HLS) V3**</span><span class="sxs-lookup"><span data-stu-id="84642-135">**Apple HTTP Live Streaming (HLS) V3**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

<span data-ttu-id="84642-136">**Smooth Streaming**</span><span class="sxs-lookup"><span data-stu-id="84642-136">**Smooth Streaming**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)


## <a name="media-services-learning-paths"></a><span data-ttu-id="84642-137">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="84642-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="84642-138">Отзывы</span><span class="sxs-lookup"><span data-stu-id="84642-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="84642-139">См. также</span><span class="sxs-lookup"><span data-stu-id="84642-139">See Also</span></span>
[<span data-ttu-id="84642-140">Обзор динамических манифестов</span><span class="sxs-lookup"><span data-stu-id="84642-140">Dynamic manifests overview</span></span>](media-services-dynamic-manifest-overview.md)

