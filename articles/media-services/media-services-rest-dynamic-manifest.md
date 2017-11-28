---
title: "Фильтры aaaCreating с API REST служб мультимедиа Azure | Документы Microsoft"
description: "Описывается, как фильтры toocreate, поэтому клиент может их использовать toostream определенных разделов потока. Службы мультимедиа создает динамические манифесты tooachieve Выборочный streaming."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: f7d23daf-7cd2-49c7-a195-ab902912ab3c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako;cenkdin
ms.openlocfilehash: d0b5af3b193b35f22ac70887963c2f0a06b60bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="creating-filters-with-azure-media-services-rest-api"></a><span data-ttu-id="02a8c-104">Создание фильтров с помощью с помощью API REST служб мультимедиа</span><span class="sxs-lookup"><span data-stu-id="02a8c-104">Creating Filters with Azure Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="02a8c-105">.NET</span><span class="sxs-lookup"><span data-stu-id="02a8c-105">.NET</span></span>](media-services-dotnet-dynamic-manifest.md)
> * [<span data-ttu-id="02a8c-106">REST</span><span class="sxs-lookup"><span data-stu-id="02a8c-106">REST</span></span>](media-services-rest-dynamic-manifest.md)
> 
> 

<span data-ttu-id="02a8c-107">Начиная с выпуска 2.11, службы мультимедиа позволяют фильтры toodefine средств.</span><span class="sxs-lookup"><span data-stu-id="02a8c-107">Starting with 2.11 release, Media Services enables you toodefine filters for your assets.</span></span> <span data-ttu-id="02a8c-108">Эти фильтры являются правила стороне сервера, позволяющие клиентам toochoose toodo таких вещей, как: воспроизведения только части видео (вместо воспроизведение hello всего видео), или укажите только набор представлений аудио и видео обработки (устройства клиента вместо всех hello представлений, которые связаны с активом hello).</span><span class="sxs-lookup"><span data-stu-id="02a8c-108">These filters are server side rules that will allow your customers toochoose toodo things like: playback only a section of a video (instead of playing hello whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all hello renditions that are associated with hello asset).</span></span> <span data-ttu-id="02a8c-109">Такая фильтрация средств архивируется через **динамического манифеста**, созданных после toostream запрос клиента видео на основе указанного фильтров.</span><span class="sxs-lookup"><span data-stu-id="02a8c-109">This filtering of your assets is archived through **Dynamic Manifest**s that are created upon your customer's request toostream a video based on specified filter(s).</span></span>

<span data-ttu-id="02a8c-110">Для получения дополнительных сведений см связанные toofilters и динамические манифеста [динамической манифесты Обзор](media-services-dynamic-manifest-overview.md).</span><span class="sxs-lookup"><span data-stu-id="02a8c-110">For more detailed information related toofilters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span></span>

<span data-ttu-id="02a8c-111">В этом разделе показано, как toocreate toouse API-интерфейс REST, обновления и удаления фильтров.</span><span class="sxs-lookup"><span data-stu-id="02a8c-111">This topic shows how toouse REST APIs toocreate, update, and delete filters.</span></span> 

## <a name="types-used-toocreate-filters"></a><span data-ttu-id="02a8c-112">Использовать фильтры toocreate типы</span><span class="sxs-lookup"><span data-stu-id="02a8c-112">Types used toocreate filters</span></span>
<span data-ttu-id="02a8c-113">Hello используются следующие типы при создании фильтров:</span><span class="sxs-lookup"><span data-stu-id="02a8c-113">hello following types are used when creating filters:</span></span>  

* [<span data-ttu-id="02a8c-114">Filter</span><span class="sxs-lookup"><span data-stu-id="02a8c-114">Filter</span></span>](https://docs.microsoft.com/rest/api/media/operations/filter)
* [<span data-ttu-id="02a8c-115">AssetFilter</span><span class="sxs-lookup"><span data-stu-id="02a8c-115">AssetFilter</span></span>](https://docs.microsoft.com/rest/api/media/operations/assetfilter)
* [<span data-ttu-id="02a8c-116">PresentationTimeRange</span><span class="sxs-lookup"><span data-stu-id="02a8c-116">PresentationTimeRange</span></span>](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)
* [<span data-ttu-id="02a8c-117">FilterTrackSelect и FilterTrackPropertyCondition</span><span class="sxs-lookup"><span data-stu-id="02a8c-117">FilterTrackSelect and FilterTrackPropertyCondition</span></span>](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)

>[!NOTE]

><span data-ttu-id="02a8c-118">При доступе к сущностям в службах мультимедиа необходимо задать определенные поля и значения заголовков в HTTP-запросах.</span><span class="sxs-lookup"><span data-stu-id="02a8c-118">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="02a8c-119">Дополнительную информацию см. в статье [Обзор интерфейса REST API служб мультимедиа](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="02a8c-119">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="02a8c-120">Подключение служб tooMedia</span><span class="sxs-lookup"><span data-stu-id="02a8c-120">Connect tooMedia Services</span></span>

<span data-ttu-id="02a8c-121">Сведения о tooconnect toohello AMS API, в статье [hello доступа к API служб мультимедиа Azure с проверкой подлинности Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="02a8c-121">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="02a8c-122">После успешного подключения toohttps://media.windows.net, будет получено перенаправление 301 указывающее другой URI служб Media Services.</span><span class="sxs-lookup"><span data-stu-id="02a8c-122">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="02a8c-123">Необходимо внести toohello последующих вызовов новый URI.</span><span class="sxs-lookup"><span data-stu-id="02a8c-123">You must make subsequent calls toohello new URI.</span></span>

## <a name="create-filters"></a><span data-ttu-id="02a8c-124">Создание фильтров</span><span class="sxs-lookup"><span data-stu-id="02a8c-124">Create filters</span></span>
### <a name="create-global-filters"></a><span data-ttu-id="02a8c-125">Создание глобальных фильтров</span><span class="sxs-lookup"><span data-stu-id="02a8c-125">Create global Filters</span></span>
<span data-ttu-id="02a8c-126">toocreate глобального фильтра, используйте hello, выполнив HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="02a8c-126">toocreate a global Filter, use hello following HTTP requests:</span></span>  

#### <a name="http-request"></a><span data-ttu-id="02a8c-127">HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="02a8c-127">HTTP Request</span></span>
<span data-ttu-id="02a8c-128">Заголовки запроса</span><span class="sxs-lookup"><span data-stu-id="02a8c-128">Request Headers</span></span>

    POST https://media.windows.net/API/Filters HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host:media.windows.net 

<span data-ttu-id="02a8c-129">Тело запроса</span><span class="sxs-lookup"><span data-stu-id="02a8c-129">Request body</span></span> 

    {  
       "Name":"GlobalFilter",
       "PresentationTimeRange":{  
          "StartTimestamp":"0",
          "EndTimestamp":"9223372036854775807",
          "PresentationWindowDuration":"12000000000",
          "LiveBackoffDuration":"0",
          "Timescale":"10000000"
       },
       "Tracks":[  
          {  
             "PropertyConditions":
                  [  
                {  
                   "Property":"Type",
                   "Value":"audio",
                   "Operator":"Equal"
                },
                {  
                   "Property":"Bitrate",
                   "Value":"0-2147483647",
                   "Operator":"Equal"
                }
             ]
          }
       ]
    }




#### <a name="http-response"></a><span data-ttu-id="02a8c-130">HTTP-ответ</span><span class="sxs-lookup"><span data-stu-id="02a8c-130">HTTP Response</span></span>
    HTTP/1.1 201 Created 

### <a name="create-local-assetfilters"></a><span data-ttu-id="02a8c-131">Создание локальных фильтров активов</span><span class="sxs-lookup"><span data-stu-id="02a8c-131">Create local AssetFilters</span></span>
<span data-ttu-id="02a8c-132">toocreate локального AssetFilter, используйте hello, выполнив HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="02a8c-132">toocreate a local AssetFilter, use hello following HTTP requests:</span></span>  

#### <a name="http-request"></a><span data-ttu-id="02a8c-133">HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="02a8c-133">HTTP Request</span></span>
<span data-ttu-id="02a8c-134">Заголовки запроса</span><span class="sxs-lookup"><span data-stu-id="02a8c-134">Request Headers</span></span>

    POST https://media.windows.net/API/AssetFilters HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net  

<span data-ttu-id="02a8c-135">Тело запроса</span><span class="sxs-lookup"><span data-stu-id="02a8c-135">Request body</span></span> 

    {   
       "Name":"AssetFilter", 
       "ParentAssetId":"nb:cid:UUID:536e555d-1500-80c3-92dc-f1e4fdc6c592", 
       "PresentationTimeRange":{   
          "StartTimestamp":"0", 
          "EndTimestamp":"9223372036854775807", 
          "PresentationWindowDuration":"12000000000", 
          "LiveBackoffDuration":"0", 
          "Timescale":"10000000" 
       }, 
       "Tracks":[   
          {   
             "PropertyConditions": 
                  [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 

#### <a name="http-response"></a><span data-ttu-id="02a8c-136">HTTP-ответ</span><span class="sxs-lookup"><span data-stu-id="02a8c-136">HTTP Response</span></span>
    HTTP/1.1 201 Created 
    . . . 

## <a name="list-filters"></a><span data-ttu-id="02a8c-137">Вывод списка фильтров</span><span class="sxs-lookup"><span data-stu-id="02a8c-137">List filters</span></span>
### <a name="get-all-global-filters-in-hello-ams-account"></a><span data-ttu-id="02a8c-138">Получить все глобальные **фильтра**s в hello AMS учетной записи</span><span class="sxs-lookup"><span data-stu-id="02a8c-138">Get all global **Filter**s in hello AMS account</span></span>
<span data-ttu-id="02a8c-139">фильтры toolist используйте hello, выполнив HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="02a8c-139">toolist filters, use hello following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="02a8c-140">HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="02a8c-140">HTTP Request</span></span>
    GET https://media.windows.net/API/Filters HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

### <a name="get-assetfilters-associated-with-an-asset"></a><span data-ttu-id="02a8c-141">Получение фильтров активов ( **AssetFilter**), связанных с тем или иным активом</span><span class="sxs-lookup"><span data-stu-id="02a8c-141">Get **AssetFilter**s associated with an asset</span></span>
#### <a name="http-request"></a><span data-ttu-id="02a8c-142">HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="02a8c-142">HTTP Request</span></span>
    GET https://media.windows.net/API/Assets('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592')/AssetFilters HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 

### <a name="get-an-assetfilter-based-on-its-id"></a><span data-ttu-id="02a8c-143">Получение фильтра активов ( **AssetFilter** ) по его идентификатору</span><span class="sxs-lookup"><span data-stu-id="02a8c-143">Get an **AssetFilter** based on its Id</span></span>
#### <a name="http-request"></a><span data-ttu-id="02a8c-144">HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="02a8c-144">HTTP Request</span></span>
    GET https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000


## <a name="update-filters"></a><span data-ttu-id="02a8c-145">Обновление фильтров</span><span class="sxs-lookup"><span data-stu-id="02a8c-145">Update filters</span></span>
<span data-ttu-id="02a8c-146">Используйте PATCH, PUT или СЛИЯНИЯ tooupdate фильтр с новыми значениями свойства.</span><span class="sxs-lookup"><span data-stu-id="02a8c-146">Use PATCH, PUT or MERGE tooupdate a filter with new property values.</span></span>  <span data-ttu-id="02a8c-147">Дополнительные сведения об этих операциях см. [здесь](http://msdn.microsoft.com/library/dd541276.aspx).</span><span class="sxs-lookup"><span data-stu-id="02a8c-147">For more information about these operations, see [PATCH, PUT, MERGE](http://msdn.microsoft.com/library/dd541276.aspx).</span></span>

<span data-ttu-id="02a8c-148">При обновлении фильтра может занять too2 минут для потоковой передачи конечной точки toorefresh hello правила.</span><span class="sxs-lookup"><span data-stu-id="02a8c-148">If you update a filter, it can take up too2 minutes for streaming endpoint toorefresh hello rules.</span></span> <span data-ttu-id="02a8c-149">Если содержимое hello был обработан с помощью этого фильтра (и кэширования в прокси-серверы и CDN кэши), обновление этого фильтра может привести к проигрывателя сбоев.</span><span class="sxs-lookup"><span data-stu-id="02a8c-149">If hello content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span></span> <span data-ttu-id="02a8c-150">Рекомендуется tooclear hello кэша после обновления hello фильтра.</span><span class="sxs-lookup"><span data-stu-id="02a8c-150">It is recommend tooclear hello cache after updating hello filter.</span></span> <span data-ttu-id="02a8c-151">Если такой вариант невозможен, рассмотрите возможность использования другого фильтра.</span><span class="sxs-lookup"><span data-stu-id="02a8c-151">If this option is not possible, consider using a different filter.</span></span>  

### <a name="update-global-filters"></a><span data-ttu-id="02a8c-152">Обновление глобальных фильтров</span><span class="sxs-lookup"><span data-stu-id="02a8c-152">Update global Filters</span></span>
<span data-ttu-id="02a8c-153">tooupdate глобального фильтра, используйте hello, выполнив HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="02a8c-153">tooupdate a global filter, use hello following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="02a8c-154">HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="02a8c-154">HTTP Request</span></span>
<span data-ttu-id="02a8c-155">Заголовки запроса:</span><span class="sxs-lookup"><span data-stu-id="02a8c-155">Request headers:</span></span> 

    MERGE https://media.windows.net/API/Filters('filterName') HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 
    Content-Length: 384

<span data-ttu-id="02a8c-156">Тело запроса:</span><span class="sxs-lookup"><span data-stu-id="02a8c-156">Request body:</span></span> 

    { 
       "Tracks":[   
          {   
             "PropertyConditions": 
             [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 

### <a name="update-local-assetfilters"></a><span data-ttu-id="02a8c-157">Обновление локальных фильтров ресурсов-контейнеров</span><span class="sxs-lookup"><span data-stu-id="02a8c-157">Update local AssetFilters</span></span>
<span data-ttu-id="02a8c-158">tooupdate локальный фильтр, используйте hello, выполнив HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="02a8c-158">tooupdate a local filter, use hello following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="02a8c-159">HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="02a8c-159">HTTP Request</span></span>
<span data-ttu-id="02a8c-160">Заголовки запроса:</span><span class="sxs-lookup"><span data-stu-id="02a8c-160">Request headers:</span></span> 

    MERGE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter')  HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 

<span data-ttu-id="02a8c-161">Тело запроса:</span><span class="sxs-lookup"><span data-stu-id="02a8c-161">Request body:</span></span> 

    { 
       "Tracks":[   
          {   
             "PropertyConditions": 
             [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 


## <a name="delete-filters"></a><span data-ttu-id="02a8c-162">Удаление фильтров</span><span class="sxs-lookup"><span data-stu-id="02a8c-162">Delete filters</span></span>
### <a name="delete-global-filters"></a><span data-ttu-id="02a8c-163">Удаление глобальных фильтров</span><span class="sxs-lookup"><span data-stu-id="02a8c-163">Delete global Filters</span></span>
<span data-ttu-id="02a8c-164">toodelete глобального фильтра, используйте hello, выполнив HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="02a8c-164">toodelete a global Filter, use hello following HTTP requests:</span></span>

#### <a name="http-request"></a><span data-ttu-id="02a8c-165">HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="02a8c-165">HTTP Request</span></span>
    DELETE https://media.windows.net/api/Filters('GlobalFilter') HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 


### <a name="delete-local-assetfilters"></a><span data-ttu-id="02a8c-166">Удаление локальных фильтров активов</span><span class="sxs-lookup"><span data-stu-id="02a8c-166">Delete local AssetFilters</span></span>
<span data-ttu-id="02a8c-167">toodelete локального AssetFilter, используйте hello, выполнив HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="02a8c-167">toodelete a local AssetFilter, use hello following HTTP requests:</span></span>

#### <a name="http-request"></a><span data-ttu-id="02a8c-168">HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="02a8c-168">HTTP Request</span></span>
    DELETE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__LocalFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

## <a name="build-streaming-urls-that-use-filters"></a><span data-ttu-id="02a8c-169">Построение URL-адресов потоковой передачи с использованием фильтров</span><span class="sxs-lookup"><span data-stu-id="02a8c-169">Build streaming URLs that use filters</span></span>
<span data-ttu-id="02a8c-170">Сведения о toopublish и предоставления имеющихся ресурсов. в статье [доставки содержимого tooCustomers Обзор](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="02a8c-170">For information on how toopublish and deliver your assets, see [Delivering Content tooCustomers Overview](media-services-deliver-content-overview.md).</span></span>

<span data-ttu-id="02a8c-171">Hello следующих примерах показано, как tooadd фильтрует tooyour URL-адреса потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="02a8c-171">hello following examples show how tooadd filters tooyour streaming URLs.</span></span>

<span data-ttu-id="02a8c-172">**MPEG DASH**</span><span class="sxs-lookup"><span data-stu-id="02a8c-172">**MPEG DASH**</span></span> 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

<span data-ttu-id="02a8c-173">**Apple HTTP Live Streaming (HLS) V4**</span><span class="sxs-lookup"><span data-stu-id="02a8c-173">**Apple HTTP Live Streaming (HLS) V4**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

<span data-ttu-id="02a8c-174">**Apple HTTP Live Streaming (HLS) V3**</span><span class="sxs-lookup"><span data-stu-id="02a8c-174">**Apple HTTP Live Streaming (HLS) V3**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

<span data-ttu-id="02a8c-175">**Smooth Streaming**</span><span class="sxs-lookup"><span data-stu-id="02a8c-175">**Smooth Streaming**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)

    
## <a name="media-services-learning-paths"></a><span data-ttu-id="02a8c-176">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="02a8c-176">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="02a8c-177">Отзывы</span><span class="sxs-lookup"><span data-stu-id="02a8c-177">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="02a8c-178">См. также</span><span class="sxs-lookup"><span data-stu-id="02a8c-178">See Also</span></span>
[<span data-ttu-id="02a8c-179">Обзор динамических манифестов</span><span class="sxs-lookup"><span data-stu-id="02a8c-179">Dynamic manifests overview</span></span>](media-services-dynamic-manifest-overview.md)

