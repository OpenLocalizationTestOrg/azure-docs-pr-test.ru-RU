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
# <a name="creating-filters-with-azure-media-services-net-sdk"></a>Создание фильтров с помощью пакета SDK для .NET служб мультимедиа Azure
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-dynamic-manifest.md)
> * [REST](media-services-rest-dynamic-manifest.md)
> 
> 

Начиная с выпуска 2.11, службы мультимедиа позволяют фильтры toodefine средств. Эти фильтры являются правила стороне сервера, позволяющие клиентам toochoose toodo таких вещей, как: воспроизведения только части видео (вместо воспроизведение hello всего видео), или укажите только набор представлений аудио и видео обработки (устройства клиента вместо всех hello представлений, которые связаны с активом hello). Такая фильтрация ресурсов достигается за счет **динамического манифеста**, созданных после toostream запрос клиента видео на основе указанного фильтров.

Для получения дополнительных сведений см связанные toofilters и динамические манифеста [динамической манифесты Обзор](media-services-dynamic-manifest-overview.md).

В этом разделе показано, как toocreate toouse Media Services .NET SDK, обновления и удаления фильтров. 

Обратите внимание, если обновить фильтр может занять too2 минут для потоковой передачи конечной точки toorefresh hello правила. Если содержимое hello был обработан с помощью этого фильтра (и кэширования в прокси-серверы и CDN кэши), обновление этого фильтра может привести к проигрывателя сбоев. Рекомендуется tooclear hello кэша после обновления hello фильтра. Если такой вариант невозможен, рассмотрите возможность использования другого фильтра. 

## <a name="types-used-toocreate-filters"></a>Использовать фильтры toocreate типы
Hello используются следующие типы при создании фильтров: 

* **IStreamingFilter**.  Этот тип основан на следующих API-интерфейса REST hello [фильтра](https://docs.microsoft.com/rest/api/media/operations/filter)
* **IStreamingAssetFilter**. Этот тип основан на следующих API-интерфейса REST hello [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)
* **PresentationTimeRange**. Этот тип основан на следующих API-интерфейса REST hello [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)
* **FilterTrackSelectStatement** и **IFilterTrackPropertyCondition**. Эти типы основаны на следующих API-интерфейсов REST hello [FilterTrackSelect и FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)

## <a name="createupdatereaddelete-global-filters"></a>Создание, обновление, чтение и удаление глобальных фильтров
Hello следующий код показывает, как toouse .NET toocreate, обновления, чтения и удаления фильтров активов.

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


## <a name="createupdatereaddelete-asset-filters"></a>Создание, обновление, чтение и удаление фильтров ресурсов-контейнеров
Hello следующий код показывает, как toouse .NET toocreate, обновления, чтения и удаления фильтров активов.

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




## <a name="build-streaming-urls-that-use-filters"></a>Построение URL-адресов потоковой передачи с использованием фильтров
Сведения о toopublish и предоставления имеющихся ресурсов. в статье [доставки содержимого tooCustomers Обзор](media-services-deliver-content-overview.md).

Hello следующих примерах показано, как tooadd фильтрует tooyour URL-адреса потоковой передачи.

**MPEG DASH** 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

**Apple HTTP Live Streaming (HLS) V4**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

**Apple HTTP Live Streaming (HLS) V3**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

**Smooth Streaming**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)


## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>См. также
[Обзор динамических манифестов](media-services-dynamic-manifest-overview.md)

