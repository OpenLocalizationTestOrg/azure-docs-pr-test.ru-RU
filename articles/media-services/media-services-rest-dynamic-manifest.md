---
title: "Создание фильтров с помощью REST API служб мультимедиа | Документация Майкрософт"
description: "В этом разделе описывается создание фильтров, с помощью которых клиент может передавать определенные секции потока. Для достижения такой выборочной потоковой передачи службы мультимедиа создают динамические манифесты."
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
ms.openlocfilehash: 76d2721138668d9f0a908af3fa42840309b068ef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="creating-filters-with-azure-media-services-rest-api"></a><span data-ttu-id="9b253-104">Создание фильтров с помощью с помощью API REST служб мультимедиа</span><span class="sxs-lookup"><span data-stu-id="9b253-104">Creating Filters with Azure Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9b253-105">.NET</span><span class="sxs-lookup"><span data-stu-id="9b253-105">.NET</span></span>](media-services-dotnet-dynamic-manifest.md)
> * [<span data-ttu-id="9b253-106">REST</span><span class="sxs-lookup"><span data-stu-id="9b253-106">REST</span></span>](media-services-rest-dynamic-manifest.md)
> 
> 

<span data-ttu-id="9b253-107">Начиная с версии 2.11, службы мультимедиа позволяют определять фильтры для активов.</span><span class="sxs-lookup"><span data-stu-id="9b253-107">Starting with 2.11 release, Media Services enables you to define filters for your assets.</span></span> <span data-ttu-id="9b253-108">Эти фильтры представляют собой правила на стороне сервера, позволяющие пользователям выполнять следующие действия: воспроизведение только части видео (вместо целого) или указание подмножества представлений аудио и видео, которые может обрабатывать устройство клиента (вместо всех представлений, связанных с активом).</span><span class="sxs-lookup"><span data-stu-id="9b253-108">These filters are server side rules that will allow your customers to choose to do things like: playback only a section of a video (instead of playing the whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all the renditions that are associated with the asset).</span></span> <span data-ttu-id="9b253-109">Такая фильтрация активов достигается с помощью **динамических манифестов**, которые создаются по запросу клиента для потоковой передачи видео на основе указанных фильтров.</span><span class="sxs-lookup"><span data-stu-id="9b253-109">This filtering of your assets is archived through **Dynamic Manifest**s that are created upon your customer's request to stream a video based on specified filter(s).</span></span>

<span data-ttu-id="9b253-110">Подробные сведения о фильтрах и динамическом манифесте см. в статье [Фильтры и динамические манифесты](media-services-dynamic-manifest-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9b253-110">For more detailed information related to filters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span></span>

<span data-ttu-id="9b253-111">В этом разделе показано, как использовать интерфейсы REST API для создания, обновления и удаления фильтров.</span><span class="sxs-lookup"><span data-stu-id="9b253-111">This topic shows how to use REST APIs to create, update, and delete filters.</span></span> 

## <a name="types-used-to-create-filters"></a><span data-ttu-id="9b253-112">Типы, используемые для создания фильтров</span><span class="sxs-lookup"><span data-stu-id="9b253-112">Types used to create filters</span></span>
<span data-ttu-id="9b253-113">При создании фильтров используются следующие типы:</span><span class="sxs-lookup"><span data-stu-id="9b253-113">The following types are used when creating filters:</span></span>  

* [<span data-ttu-id="9b253-114">Filter</span><span class="sxs-lookup"><span data-stu-id="9b253-114">Filter</span></span>](https://docs.microsoft.com/rest/api/media/operations/filter)
* [<span data-ttu-id="9b253-115">AssetFilter</span><span class="sxs-lookup"><span data-stu-id="9b253-115">AssetFilter</span></span>](https://docs.microsoft.com/rest/api/media/operations/assetfilter)
* [<span data-ttu-id="9b253-116">PresentationTimeRange</span><span class="sxs-lookup"><span data-stu-id="9b253-116">PresentationTimeRange</span></span>](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)
* [<span data-ttu-id="9b253-117">FilterTrackSelect и FilterTrackPropertyCondition</span><span class="sxs-lookup"><span data-stu-id="9b253-117">FilterTrackSelect and FilterTrackPropertyCondition</span></span>](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)

>[!NOTE]

><span data-ttu-id="9b253-118">При доступе к сущностям в службах мультимедиа необходимо задать определенные поля и значения заголовков в HTTP-запросах.</span><span class="sxs-lookup"><span data-stu-id="9b253-118">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="9b253-119">Дополнительную информацию см. в статье [Обзор интерфейса REST API служб мультимедиа](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="9b253-119">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="9b253-120">Подключение к службам мультимедиа</span><span class="sxs-lookup"><span data-stu-id="9b253-120">Connect to Media Services</span></span>

<span data-ttu-id="9b253-121">Сведения о подключении к API AMS см. в разделе [Доступ к API служб мультимедиа Azure с помощью аутентификации Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="9b253-121">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="9b253-122">После успешного подключения к https://media.windows.net вы получите ошибку 301 (перенаправление), в которой будет указан другой URI служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="9b253-122">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="9b253-123">Используйте для последующих вызовов новый URI.</span><span class="sxs-lookup"><span data-stu-id="9b253-123">You must make subsequent calls to the new URI.</span></span>

## <a name="create-filters"></a><span data-ttu-id="9b253-124">Создание фильтров</span><span class="sxs-lookup"><span data-stu-id="9b253-124">Create filters</span></span>
### <a name="create-global-filters"></a><span data-ttu-id="9b253-125">Создание глобальных фильтров</span><span class="sxs-lookup"><span data-stu-id="9b253-125">Create global Filters</span></span>
<span data-ttu-id="9b253-126">Чтобы создать глобальный фильтр, используйте следующие запросы HTTP:</span><span class="sxs-lookup"><span data-stu-id="9b253-126">To create a global Filter, use the following HTTP requests:</span></span>  

#### <a name="http-request"></a><span data-ttu-id="9b253-127">HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="9b253-127">HTTP Request</span></span>
<span data-ttu-id="9b253-128">Заголовки запроса</span><span class="sxs-lookup"><span data-stu-id="9b253-128">Request Headers</span></span>

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

<span data-ttu-id="9b253-129">Тело запроса</span><span class="sxs-lookup"><span data-stu-id="9b253-129">Request body</span></span> 

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




#### <a name="http-response"></a><span data-ttu-id="9b253-130">HTTP-ответ</span><span class="sxs-lookup"><span data-stu-id="9b253-130">HTTP Response</span></span>
    HTTP/1.1 201 Created 

### <a name="create-local-assetfilters"></a><span data-ttu-id="9b253-131">Создание локальных фильтров активов</span><span class="sxs-lookup"><span data-stu-id="9b253-131">Create local AssetFilters</span></span>
<span data-ttu-id="9b253-132">Чтобы создать локальный фильтр активов (AssetFilter), используйте следующие запросы HTTP:</span><span class="sxs-lookup"><span data-stu-id="9b253-132">To create a local AssetFilter, use the following HTTP requests:</span></span>  

#### <a name="http-request"></a><span data-ttu-id="9b253-133">HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="9b253-133">HTTP Request</span></span>
<span data-ttu-id="9b253-134">Заголовки запроса</span><span class="sxs-lookup"><span data-stu-id="9b253-134">Request Headers</span></span>

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

<span data-ttu-id="9b253-135">Тело запроса</span><span class="sxs-lookup"><span data-stu-id="9b253-135">Request body</span></span> 

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

#### <a name="http-response"></a><span data-ttu-id="9b253-136">HTTP-ответ</span><span class="sxs-lookup"><span data-stu-id="9b253-136">HTTP Response</span></span>
    HTTP/1.1 201 Created 
    . . . 

## <a name="list-filters"></a><span data-ttu-id="9b253-137">Вывод списка фильтров</span><span class="sxs-lookup"><span data-stu-id="9b253-137">List filters</span></span>
### <a name="get-all-global-filters-in-the-ams-account"></a><span data-ttu-id="9b253-138">Получение всех глобальных фильтров ( **Filter**) в учетной записи AMS</span><span class="sxs-lookup"><span data-stu-id="9b253-138">Get all global **Filter**s in the AMS account</span></span>
<span data-ttu-id="9b253-139">Для вывода списка фильтров используйте следующие запросы HTTP:</span><span class="sxs-lookup"><span data-stu-id="9b253-139">To list filters, use the following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="9b253-140">HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="9b253-140">HTTP Request</span></span>
    GET https://media.windows.net/API/Filters HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

### <a name="get-assetfilters-associated-with-an-asset"></a><span data-ttu-id="9b253-141">Получение фильтров активов ( **AssetFilter**), связанных с тем или иным активом</span><span class="sxs-lookup"><span data-stu-id="9b253-141">Get **AssetFilter**s associated with an asset</span></span>
#### <a name="http-request"></a><span data-ttu-id="9b253-142">HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="9b253-142">HTTP Request</span></span>
    GET https://media.windows.net/API/Assets('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592')/AssetFilters HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 

### <a name="get-an-assetfilter-based-on-its-id"></a><span data-ttu-id="9b253-143">Получение фильтра активов ( **AssetFilter** ) по его идентификатору</span><span class="sxs-lookup"><span data-stu-id="9b253-143">Get an **AssetFilter** based on its Id</span></span>
#### <a name="http-request"></a><span data-ttu-id="9b253-144">HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="9b253-144">HTTP Request</span></span>
    GET https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000


## <a name="update-filters"></a><span data-ttu-id="9b253-145">Обновление фильтров</span><span class="sxs-lookup"><span data-stu-id="9b253-145">Update filters</span></span>
<span data-ttu-id="9b253-146">Для обновления фильтра новыми значениями свойства используйте операции PATCH, PUT или MERGE.</span><span class="sxs-lookup"><span data-stu-id="9b253-146">Use PATCH, PUT or MERGE to update a filter with new property values.</span></span>  <span data-ttu-id="9b253-147">Дополнительные сведения об этих операциях см. [здесь](http://msdn.microsoft.com/library/dd541276.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b253-147">For more information about these operations, see [PATCH, PUT, MERGE](http://msdn.microsoft.com/library/dd541276.aspx).</span></span>

<span data-ttu-id="9b253-148">При обновлении фильтра может понадобиться до 2 минут на обновление правил конечной точкой потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="9b253-148">If you update a filter, it can take up to 2 minutes for streaming endpoint to refresh the rules.</span></span> <span data-ttu-id="9b253-149">Если содержимое было обработано с помощью данного фильтра (и кэшировано на прокси-серверах и в кэшах CDN), обновление этого фильтра может привести к сбоям проигрывателя.</span><span class="sxs-lookup"><span data-stu-id="9b253-149">If the content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span></span> <span data-ttu-id="9b253-150">Рекомендуется очистить кэш после обновления фильтра.</span><span class="sxs-lookup"><span data-stu-id="9b253-150">It is recommend to clear the cache after updating the filter.</span></span> <span data-ttu-id="9b253-151">Если такой вариант невозможен, рассмотрите возможность использования другого фильтра.</span><span class="sxs-lookup"><span data-stu-id="9b253-151">If this option is not possible, consider using a different filter.</span></span>  

### <a name="update-global-filters"></a><span data-ttu-id="9b253-152">Обновление глобальных фильтров</span><span class="sxs-lookup"><span data-stu-id="9b253-152">Update global Filters</span></span>
<span data-ttu-id="9b253-153">Чтобы обновить глобальный фильтр, используйте следующие запросы HTTP:</span><span class="sxs-lookup"><span data-stu-id="9b253-153">To update a global filter, use the following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="9b253-154">HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="9b253-154">HTTP Request</span></span>
<span data-ttu-id="9b253-155">Заголовки запроса:</span><span class="sxs-lookup"><span data-stu-id="9b253-155">Request headers:</span></span> 

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

<span data-ttu-id="9b253-156">Тело запроса:</span><span class="sxs-lookup"><span data-stu-id="9b253-156">Request body:</span></span> 

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

### <a name="update-local-assetfilters"></a><span data-ttu-id="9b253-157">Обновление локальных фильтров ресурсов-контейнеров</span><span class="sxs-lookup"><span data-stu-id="9b253-157">Update local AssetFilters</span></span>
<span data-ttu-id="9b253-158">Чтобы обновить локальный фильтр, используйте следующие запросы HTTP:</span><span class="sxs-lookup"><span data-stu-id="9b253-158">To update a local filter, use the following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="9b253-159">HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="9b253-159">HTTP Request</span></span>
<span data-ttu-id="9b253-160">Заголовки запроса:</span><span class="sxs-lookup"><span data-stu-id="9b253-160">Request headers:</span></span> 

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

<span data-ttu-id="9b253-161">Тело запроса:</span><span class="sxs-lookup"><span data-stu-id="9b253-161">Request body:</span></span> 

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


## <a name="delete-filters"></a><span data-ttu-id="9b253-162">Удаление фильтров</span><span class="sxs-lookup"><span data-stu-id="9b253-162">Delete filters</span></span>
### <a name="delete-global-filters"></a><span data-ttu-id="9b253-163">Удаление глобальных фильтров</span><span class="sxs-lookup"><span data-stu-id="9b253-163">Delete global Filters</span></span>
<span data-ttu-id="9b253-164">Чтобы удалить глобальный фильтр, используйте следующие запросы HTTP:</span><span class="sxs-lookup"><span data-stu-id="9b253-164">To delete a global Filter, use the following HTTP requests:</span></span>

#### <a name="http-request"></a><span data-ttu-id="9b253-165">HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="9b253-165">HTTP Request</span></span>
    DELETE https://media.windows.net/api/Filters('GlobalFilter') HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 


### <a name="delete-local-assetfilters"></a><span data-ttu-id="9b253-166">Удаление локальных фильтров активов</span><span class="sxs-lookup"><span data-stu-id="9b253-166">Delete local AssetFilters</span></span>
<span data-ttu-id="9b253-167">Чтобы удалить локальный фильтр активов, используйте следующие запросы HTTP:</span><span class="sxs-lookup"><span data-stu-id="9b253-167">To delete a local AssetFilter, use the following HTTP requests:</span></span>

#### <a name="http-request"></a><span data-ttu-id="9b253-168">HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="9b253-168">HTTP Request</span></span>
    DELETE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__LocalFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

## <a name="build-streaming-urls-that-use-filters"></a><span data-ttu-id="9b253-169">Построение URL-адресов потоковой передачи с использованием фильтров</span><span class="sxs-lookup"><span data-stu-id="9b253-169">Build streaming URLs that use filters</span></span>
<span data-ttu-id="9b253-170">Сведения о публикации и доставке ресурсов см. в статье [Доставка содержимого клиентам](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9b253-170">For information on how to publish and deliver your assets, see [Delivering Content to Customers Overview](media-services-deliver-content-overview.md).</span></span>

<span data-ttu-id="9b253-171">Следующие примеры показывают, как добавлять фильтры к URL-адресам потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="9b253-171">The following examples show how to add filters to your streaming URLs.</span></span>

<span data-ttu-id="9b253-172">**MPEG DASH**</span><span class="sxs-lookup"><span data-stu-id="9b253-172">**MPEG DASH**</span></span> 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

<span data-ttu-id="9b253-173">**Apple HTTP Live Streaming (HLS) V4**</span><span class="sxs-lookup"><span data-stu-id="9b253-173">**Apple HTTP Live Streaming (HLS) V4**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

<span data-ttu-id="9b253-174">**Apple HTTP Live Streaming (HLS) V3**</span><span class="sxs-lookup"><span data-stu-id="9b253-174">**Apple HTTP Live Streaming (HLS) V3**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

<span data-ttu-id="9b253-175">**Smooth Streaming**</span><span class="sxs-lookup"><span data-stu-id="9b253-175">**Smooth Streaming**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)

    
## <a name="media-services-learning-paths"></a><span data-ttu-id="9b253-176">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="9b253-176">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9b253-177">Отзывы</span><span class="sxs-lookup"><span data-stu-id="9b253-177">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="9b253-178">См. также</span><span class="sxs-lookup"><span data-stu-id="9b253-178">See Also</span></span>
[<span data-ttu-id="9b253-179">Обзор динамических манифестов</span><span class="sxs-lookup"><span data-stu-id="9b253-179">Dynamic manifests overview</span></span>](media-services-dynamic-manifest-overview.md)

