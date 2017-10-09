---
title: "aaaAzure модели данных аналитики приложений | Документы Microsoft"
description: "Описание свойств, экспортируемых с помощью непрерывного экспорта в формате JSON и используемых в качестве фильтров."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: cabad41c-0518-4669-887f-3087aef865ea
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/21/2016
ms.author: bwren
ms.openlocfilehash: 5ff3ce7953b91cc69b5d96c0ea9b6d58a6016e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-export-data-model"></a><span data-ttu-id="0b49f-103">Экспорт модели данных Application Insights</span><span class="sxs-lookup"><span data-stu-id="0b49f-103">Application Insights Export Data Model</span></span>
<span data-ttu-id="0b49f-104">В этой таблице перечислены свойства hello телеметрии, отправленные hello [Application Insights](app-insights-overview.md) портала toohello пакеты SDK.</span><span class="sxs-lookup"><span data-stu-id="0b49f-104">This table lists hello properties of telemetry sent from hello [Application Insights](app-insights-overview.md) SDKs toohello portal.</span></span>
<span data-ttu-id="0b49f-105">Вы увидите эти свойства в выходных данных [непрерывного экспорта](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="0b49f-105">You'll see these properties in data output from [Continuous Export](app-insights-export-telemetry.md).</span></span>
<span data-ttu-id="0b49f-106">Они также отображаются в фильтрах свойств в [обозревателе метрик](app-insights-metrics-explorer.md) и при [диагностическом поиске](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="0b49f-106">They also appear in property filters in [Metric Explorer](app-insights-metrics-explorer.md) and [Diagnostic Search](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="0b49f-107">Toonote точек:</span><span class="sxs-lookup"><span data-stu-id="0b49f-107">Points toonote:</span></span>

* <span data-ttu-id="0b49f-108">`[0]`в этих таблицах обозначает точку пути hello, когда имеется tooinsert индекса; но не всегда 0.</span><span class="sxs-lookup"><span data-stu-id="0b49f-108">`[0]` in these tables denotes a point in hello path where you have tooinsert an index; but it isn't always 0.</span></span>
* <span data-ttu-id="0b49f-109">Продолжительность времени указана в десятых долях микросекунды, поэтому 10 000 000 = 1 с.</span><span class="sxs-lookup"><span data-stu-id="0b49f-109">Time durations are in tenths of a microsecond, so 10000000 == 1 second.</span></span>
* <span data-ttu-id="0b49f-110">Значения даты и времени UTC и указываются в формате ISO hello`yyyy-MM-DDThh:mm:ss.sssZ`</span><span class="sxs-lookup"><span data-stu-id="0b49f-110">Dates and times are UTC, and are given in hello ISO format `yyyy-MM-DDThh:mm:ss.sssZ`</span></span>


## <a name="example"></a><span data-ttu-id="0b49f-111">Пример</span><span class="sxs-lookup"><span data-stu-id="0b49f-111">Example</span></span>
    // A server report about an HTTP request
    {
    "request": [
      {
        "urlData": { // derived from 'url'
          "host": "contoso.org",
          "base": "/",
          "hashTag": ""
        },
        "responseCode": 200, // Sent tooclient
        "success": true, // Default == responseCode<400
        // Request id becomes hello operation id of child events
        "id": "fCOhCdCnZ9I=",  
        "name": "GET Home/Index",
        "count": 1, // 100% / sampling rate
        "durationMetric": {
          "value": 1046804.0, // 10000000 == 1 second
          // Currently hello following fields are redundant:
          "count": 1.0,
          "min": 1046804.0,
          "max": 1046804.0,
          "stdDev": 0.0,
          "sampledValue": 1046804.0
        },
        "url": "/"
      }
    ],
    "internal": {
      "data": {
        "id": "7f156650-ef4c-11e5-8453-3f984b167d05",
        "documentVersion": "1.61"
      }
    },
    "context": {
      "device": { // client browser
        "type": "PC",
        "screenResolution": { },
        "roleInstance": "WFWEB14B.fabrikam.net"
      },
      "application": { },
      "location": { // derived from client ip
        "continent": "North America",
        "country": "United States",
        // last octagon is anonymized too0 at portal:
        "clientip": "168.62.177.0",
        "province": "",
        "city": ""
      },
      "data": {
        "isSynthetic": true, // we identified source as a bot
        // percentage of generated data sent tooportal:
        "samplingRate": 100.0,
        "eventTime": "2016-03-21T10:05:45.7334717Z" // UTC
      },
      "user": {
        "isAuthenticated": false,
        "anonId": "us-tx-sn1-azr", // bot agent id
        "anonAcquisitionDate": "0001-01-01T00:00:00Z",
        "authAcquisitionDate": "0001-01-01T00:00:00Z",
        "accountAcquisitionDate": "0001-01-01T00:00:00Z"
      },
      "operation": {
        "id": "fCOhCdCnZ9I=",
        "parentId": "fCOhCdCnZ9I=",
        "name": "GET Home/Index"
      },
      "cloud": { },
      "serverDevice": { },
      "custom": { // set by custom fields of track calls
        "dimensions": [ ],
        "metrics": [ ]
      },
      "session": {
        "id": "65504c10-44a6-489e-b9dc-94184eb00d86",
        "isFirst": true
      }
    }
  <span data-ttu-id="0b49f-112">}</span><span class="sxs-lookup"><span data-stu-id="0b49f-112">}</span></span>

## <a name="context"></a><span data-ttu-id="0b49f-113">Context</span><span class="sxs-lookup"><span data-stu-id="0b49f-113">Context</span></span>
<span data-ttu-id="0b49f-114">Для каждого типа данных телеметрии приведен пример с разделом контекста.</span><span class="sxs-lookup"><span data-stu-id="0b49f-114">All types of telemetry are accompanied by a context section.</span></span> <span data-ttu-id="0b49f-115">Не все эти поля передаются со всеми точками данных.</span><span class="sxs-lookup"><span data-stu-id="0b49f-115">Not all of these fields are transmitted with every data point.</span></span>

| <span data-ttu-id="0b49f-116">Путь</span><span class="sxs-lookup"><span data-stu-id="0b49f-116">Path</span></span> | <span data-ttu-id="0b49f-117">Тип</span><span class="sxs-lookup"><span data-stu-id="0b49f-117">Type</span></span> | <span data-ttu-id="0b49f-118">Примечания</span><span class="sxs-lookup"><span data-stu-id="0b49f-118">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0b49f-119">context.custom.dimensions [0]</span><span class="sxs-lookup"><span data-stu-id="0b49f-119">context.custom.dimensions [0]</span></span> |<span data-ttu-id="0b49f-120">объект [ ]</span><span class="sxs-lookup"><span data-stu-id="0b49f-120">object [ ]</span></span> |<span data-ttu-id="0b49f-121">Набор пар "ключ — значение", заданный параметром пользовательских свойств.</span><span class="sxs-lookup"><span data-stu-id="0b49f-121">Key-value string pairs set by custom properties parameter.</span></span> <span data-ttu-id="0b49f-122">Максимальная длина ключа — 100, максимальная длина значения —1024.</span><span class="sxs-lookup"><span data-stu-id="0b49f-122">Key max length 100, values max length 1024.</span></span> <span data-ttu-id="0b49f-123">Более 100 уникальные значения, свойство hello может выполняться поиск, но не может использоваться для сегментации.</span><span class="sxs-lookup"><span data-stu-id="0b49f-123">More than 100 unique values, hello property can be searched but cannot be used for segmentation.</span></span> <span data-ttu-id="0b49f-124">Максимальное количество — 200 ключей на ключ ikey.</span><span class="sxs-lookup"><span data-stu-id="0b49f-124">Max 200 keys per ikey.</span></span> |
| <span data-ttu-id="0b49f-125">context.custom.metrics [0]</span><span class="sxs-lookup"><span data-stu-id="0b49f-125">context.custom.metrics [0]</span></span> |<span data-ttu-id="0b49f-126">объект [ ]</span><span class="sxs-lookup"><span data-stu-id="0b49f-126">object [ ]</span></span> |<span data-ttu-id="0b49f-127">Набор пар "ключ — значение", заданный параметром пользовательских измерений и метриками TrackMetric.</span><span class="sxs-lookup"><span data-stu-id="0b49f-127">Key-value pairs set by custom measurements parameter and by TrackMetrics.</span></span> <span data-ttu-id="0b49f-128">Максимальная длина ключа — 100. Значения могут быть числовыми.</span><span class="sxs-lookup"><span data-stu-id="0b49f-128">Key max length 100, values may be numeric.</span></span> |
| <span data-ttu-id="0b49f-129">context.data.eventTime</span><span class="sxs-lookup"><span data-stu-id="0b49f-129">context.data.eventTime</span></span> |<span data-ttu-id="0b49f-130">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-130">string</span></span> |<span data-ttu-id="0b49f-131">Формат UTC.</span><span class="sxs-lookup"><span data-stu-id="0b49f-131">UTC</span></span> |
| <span data-ttu-id="0b49f-132">context.data.isSynthetic</span><span class="sxs-lookup"><span data-stu-id="0b49f-132">context.data.isSynthetic</span></span> |<span data-ttu-id="0b49f-133">Логическое</span><span class="sxs-lookup"><span data-stu-id="0b49f-133">boolean</span></span> |<span data-ttu-id="0b49f-134">Запрос отображается toocome нижняя или веб-теста.</span><span class="sxs-lookup"><span data-stu-id="0b49f-134">Request appears toocome from a bot or web test.</span></span> |
| <span data-ttu-id="0b49f-135">context.data.samplingRate</span><span class="sxs-lookup"><span data-stu-id="0b49f-135">context.data.samplingRate</span></span> |<span data-ttu-id="0b49f-136">number</span><span class="sxs-lookup"><span data-stu-id="0b49f-136">number</span></span> |<span data-ttu-id="0b49f-137">Процент создаваемых hello SDK, который отправляется tooportal телеметрии.</span><span class="sxs-lookup"><span data-stu-id="0b49f-137">Percentage of telemetry generated by hello SDK that is sent tooportal.</span></span> <span data-ttu-id="0b49f-138">Диапазон 0,0–100,0.</span><span class="sxs-lookup"><span data-stu-id="0b49f-138">Range 0.0-100.0.</span></span> |
| <span data-ttu-id="0b49f-139">context.device</span><span class="sxs-lookup"><span data-stu-id="0b49f-139">context.device</span></span> |<span data-ttu-id="0b49f-140">object</span><span class="sxs-lookup"><span data-stu-id="0b49f-140">object</span></span> |<span data-ttu-id="0b49f-141">Устройство клиента</span><span class="sxs-lookup"><span data-stu-id="0b49f-141">Client device</span></span> |
| <span data-ttu-id="0b49f-142">context.device.browser</span><span class="sxs-lookup"><span data-stu-id="0b49f-142">context.device.browser</span></span> |<span data-ttu-id="0b49f-143">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-143">string</span></span> |<span data-ttu-id="0b49f-144">IE, Chrome…</span><span class="sxs-lookup"><span data-stu-id="0b49f-144">IE, Chrome, ...</span></span> |
| <span data-ttu-id="0b49f-145">context.device.browserVersion</span><span class="sxs-lookup"><span data-stu-id="0b49f-145">context.device.browserVersion</span></span> |<span data-ttu-id="0b49f-146">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-146">string</span></span> |<span data-ttu-id="0b49f-147">Chrome 48.0…</span><span class="sxs-lookup"><span data-stu-id="0b49f-147">Chrome 48.0, ...</span></span> |
| <span data-ttu-id="0b49f-148">context.device.deviceModel</span><span class="sxs-lookup"><span data-stu-id="0b49f-148">context.device.deviceModel</span></span> |<span data-ttu-id="0b49f-149">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-149">string</span></span> | |
| <span data-ttu-id="0b49f-150">context.device.deviceName</span><span class="sxs-lookup"><span data-stu-id="0b49f-150">context.device.deviceName</span></span> |<span data-ttu-id="0b49f-151">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-151">string</span></span> | |
| <span data-ttu-id="0b49f-152">context.device.id</span><span class="sxs-lookup"><span data-stu-id="0b49f-152">context.device.id</span></span> |<span data-ttu-id="0b49f-153">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-153">string</span></span> | |
| <span data-ttu-id="0b49f-154">context.device.locale</span><span class="sxs-lookup"><span data-stu-id="0b49f-154">context.device.locale</span></span> |<span data-ttu-id="0b49f-155">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-155">string</span></span> |<span data-ttu-id="0b49f-156">en-GB, de-DE…</span><span class="sxs-lookup"><span data-stu-id="0b49f-156">en-GB, de-DE, ...</span></span> |
| <span data-ttu-id="0b49f-157">context.device.network</span><span class="sxs-lookup"><span data-stu-id="0b49f-157">context.device.network</span></span> |<span data-ttu-id="0b49f-158">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-158">string</span></span> | |
| <span data-ttu-id="0b49f-159">context.device.oemName</span><span class="sxs-lookup"><span data-stu-id="0b49f-159">context.device.oemName</span></span> |<span data-ttu-id="0b49f-160">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-160">string</span></span> | |
| <span data-ttu-id="0b49f-161">context.device.osVersion</span><span class="sxs-lookup"><span data-stu-id="0b49f-161">context.device.osVersion</span></span> |<span data-ttu-id="0b49f-162">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-162">string</span></span> |<span data-ttu-id="0b49f-163">ОС узла</span><span class="sxs-lookup"><span data-stu-id="0b49f-163">Host OS</span></span> |
| <span data-ttu-id="0b49f-164">context.device.roleInstance</span><span class="sxs-lookup"><span data-stu-id="0b49f-164">context.device.roleInstance</span></span> |<span data-ttu-id="0b49f-165">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-165">string</span></span> |<span data-ttu-id="0b49f-166">Идентификатор узла сервера</span><span class="sxs-lookup"><span data-stu-id="0b49f-166">ID of server host</span></span> |
| <span data-ttu-id="0b49f-167">context.device.roleName</span><span class="sxs-lookup"><span data-stu-id="0b49f-167">context.device.roleName</span></span> |<span data-ttu-id="0b49f-168">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-168">string</span></span> | |
| <span data-ttu-id="0b49f-169">context.device.type</span><span class="sxs-lookup"><span data-stu-id="0b49f-169">context.device.type</span></span> |<span data-ttu-id="0b49f-170">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-170">string</span></span> |<span data-ttu-id="0b49f-171">ПК, браузер…</span><span class="sxs-lookup"><span data-stu-id="0b49f-171">PC, Browser, ...</span></span> |
| <span data-ttu-id="0b49f-172">context.location</span><span class="sxs-lookup"><span data-stu-id="0b49f-172">context.location</span></span> |<span data-ttu-id="0b49f-173">object</span><span class="sxs-lookup"><span data-stu-id="0b49f-173">object</span></span> |<span data-ttu-id="0b49f-174">На основе значения clientip.</span><span class="sxs-lookup"><span data-stu-id="0b49f-174">Derived from clientip.</span></span> |
| <span data-ttu-id="0b49f-175">context.location.city</span><span class="sxs-lookup"><span data-stu-id="0b49f-175">context.location.city</span></span> |<span data-ttu-id="0b49f-176">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-176">string</span></span> |<span data-ttu-id="0b49f-177">На основе значения clientip (если известно)</span><span class="sxs-lookup"><span data-stu-id="0b49f-177">Derived from clientip, if known</span></span> |
| <span data-ttu-id="0b49f-178">context.location.clientip</span><span class="sxs-lookup"><span data-stu-id="0b49f-178">context.location.clientip</span></span> |<span data-ttu-id="0b49f-179">string</span><span class="sxs-lookup"><span data-stu-id="0b49f-179">string</span></span> |<span data-ttu-id="0b49f-180">Последний восьмиугольник — анонимные too0.</span><span class="sxs-lookup"><span data-stu-id="0b49f-180">Last octagon is anonymized too0.</span></span> |
| <span data-ttu-id="0b49f-181">context.location.continent</span><span class="sxs-lookup"><span data-stu-id="0b49f-181">context.location.continent</span></span> |<span data-ttu-id="0b49f-182">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-182">string</span></span> | |
| <span data-ttu-id="0b49f-183">context.location.country</span><span class="sxs-lookup"><span data-stu-id="0b49f-183">context.location.country</span></span> |<span data-ttu-id="0b49f-184">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-184">string</span></span> | |
| <span data-ttu-id="0b49f-185">context.location.province</span><span class="sxs-lookup"><span data-stu-id="0b49f-185">context.location.province</span></span> |<span data-ttu-id="0b49f-186">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-186">string</span></span> |<span data-ttu-id="0b49f-187">Страна или область</span><span class="sxs-lookup"><span data-stu-id="0b49f-187">State or province</span></span> |
| <span data-ttu-id="0b49f-188">context.operation.id</span><span class="sxs-lookup"><span data-stu-id="0b49f-188">context.operation.id</span></span> |<span data-ttu-id="0b49f-189">string</span><span class="sxs-lookup"><span data-stu-id="0b49f-189">string</span></span> |<span data-ttu-id="0b49f-190">Элементы, имеющие hello таким же идентификатором операции отображаются в виде связанных элементов портала hello.</span><span class="sxs-lookup"><span data-stu-id="0b49f-190">Items that have hello same operation id are shown as Related Items in hello portal.</span></span> <span data-ttu-id="0b49f-191">Обычно идентификатор запроса hello.</span><span class="sxs-lookup"><span data-stu-id="0b49f-191">Usually hello request id.</span></span> |
| <span data-ttu-id="0b49f-192">context.operation.name</span><span class="sxs-lookup"><span data-stu-id="0b49f-192">context.operation.name</span></span> |<span data-ttu-id="0b49f-193">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-193">string</span></span> |<span data-ttu-id="0b49f-194">URL-адрес или имя запроса</span><span class="sxs-lookup"><span data-stu-id="0b49f-194">url or request name</span></span> |
| <span data-ttu-id="0b49f-195">context.operation.parentId</span><span class="sxs-lookup"><span data-stu-id="0b49f-195">context.operation.parentId</span></span> |<span data-ttu-id="0b49f-196">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-196">string</span></span> |<span data-ttu-id="0b49f-197">Разрешает использование вложенных связанных элементов.</span><span class="sxs-lookup"><span data-stu-id="0b49f-197">Allows nested related items.</span></span> |
| <span data-ttu-id="0b49f-198">context.session.id</span><span class="sxs-lookup"><span data-stu-id="0b49f-198">context.session.id</span></span> |<span data-ttu-id="0b49f-199">string</span><span class="sxs-lookup"><span data-stu-id="0b49f-199">string</span></span> |<span data-ttu-id="0b49f-200">Идентификатор группы операций из hello одного источника.</span><span class="sxs-lookup"><span data-stu-id="0b49f-200">Id of a group of operations from hello same source.</span></span> <span data-ttu-id="0b49f-201">Период, в течение 30 минут без операции сигналы hello завершение сеанса.</span><span class="sxs-lookup"><span data-stu-id="0b49f-201">A period of 30 minutes without an operation signals hello end of a session.</span></span> |
| <span data-ttu-id="0b49f-202">context.session.isFirst</span><span class="sxs-lookup"><span data-stu-id="0b49f-202">context.session.isFirst</span></span> |<span data-ttu-id="0b49f-203">Логическое</span><span class="sxs-lookup"><span data-stu-id="0b49f-203">boolean</span></span> | |
| <span data-ttu-id="0b49f-204">context.user.accountAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="0b49f-204">context.user.accountAcquisitionDate</span></span> |<span data-ttu-id="0b49f-205">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-205">string</span></span> | |
| <span data-ttu-id="0b49f-206">context.user.anonAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="0b49f-206">context.user.anonAcquisitionDate</span></span> |<span data-ttu-id="0b49f-207">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-207">string</span></span> | |
| <span data-ttu-id="0b49f-208">context.user.anonId</span><span class="sxs-lookup"><span data-stu-id="0b49f-208">context.user.anonId</span></span> |<span data-ttu-id="0b49f-209">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-209">string</span></span> | |
| <span data-ttu-id="0b49f-210">context.user.authAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="0b49f-210">context.user.authAcquisitionDate</span></span> |<span data-ttu-id="0b49f-211">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-211">string</span></span> |[<span data-ttu-id="0b49f-212">Прошедший проверку пользователь.</span><span class="sxs-lookup"><span data-stu-id="0b49f-212">Authenticated User</span></span>](app-insights-api-custom-events-metrics.md#authenticated-users) |
| <span data-ttu-id="0b49f-213">context.user.isAuthenticated</span><span class="sxs-lookup"><span data-stu-id="0b49f-213">context.user.isAuthenticated</span></span> |<span data-ttu-id="0b49f-214">Логическое</span><span class="sxs-lookup"><span data-stu-id="0b49f-214">boolean</span></span> | |
| <span data-ttu-id="0b49f-215">internal.data.documentVersion</span><span class="sxs-lookup"><span data-stu-id="0b49f-215">internal.data.documentVersion</span></span> |<span data-ttu-id="0b49f-216">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-216">string</span></span> | |
| <span data-ttu-id="0b49f-217">internal.data.id</span><span class="sxs-lookup"><span data-stu-id="0b49f-217">internal.data.id</span></span> |<span data-ttu-id="0b49f-218">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-218">string</span></span> | |

## <a name="events"></a><span data-ttu-id="0b49f-219">События</span><span class="sxs-lookup"><span data-stu-id="0b49f-219">Events</span></span>
<span data-ttu-id="0b49f-220">Пользовательские события, создаваемые элементом [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="0b49f-220">Custom events generated by [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent).</span></span>

| <span data-ttu-id="0b49f-221">Путь</span><span class="sxs-lookup"><span data-stu-id="0b49f-221">Path</span></span> | <span data-ttu-id="0b49f-222">Тип</span><span class="sxs-lookup"><span data-stu-id="0b49f-222">Type</span></span> | <span data-ttu-id="0b49f-223">Примечания</span><span class="sxs-lookup"><span data-stu-id="0b49f-223">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0b49f-224">event [0] count</span><span class="sxs-lookup"><span data-stu-id="0b49f-224">event [0] count</span></span> |<span data-ttu-id="0b49f-225">целое число</span><span class="sxs-lookup"><span data-stu-id="0b49f-225">integer</span></span> |<span data-ttu-id="0b49f-226">100/(частота[выборки](app-insights-sampling.md) ).</span><span class="sxs-lookup"><span data-stu-id="0b49f-226">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="0b49f-227">Например, 4 = &gt; 25 %.</span><span class="sxs-lookup"><span data-stu-id="0b49f-227">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="0b49f-228">event [0] name</span><span class="sxs-lookup"><span data-stu-id="0b49f-228">event [0] name</span></span> |<span data-ttu-id="0b49f-229">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-229">string</span></span> |<span data-ttu-id="0b49f-230">Имя события.</span><span class="sxs-lookup"><span data-stu-id="0b49f-230">Event name.</span></span>  <span data-ttu-id="0b49f-231">Максимальная длина: 250</span><span class="sxs-lookup"><span data-stu-id="0b49f-231">Max length 250.</span></span> |
| <span data-ttu-id="0b49f-232">event [0] url</span><span class="sxs-lookup"><span data-stu-id="0b49f-232">event [0] url</span></span> |<span data-ttu-id="0b49f-233">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-233">string</span></span> | |
| <span data-ttu-id="0b49f-234">event [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="0b49f-234">event [0] urlData.base</span></span> |<span data-ttu-id="0b49f-235">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-235">string</span></span> | |
| <span data-ttu-id="0b49f-236">event [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="0b49f-236">event [0] urlData.host</span></span> |<span data-ttu-id="0b49f-237">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-237">string</span></span> | |

## <a name="exceptions"></a><span data-ttu-id="0b49f-238">Исключения</span><span class="sxs-lookup"><span data-stu-id="0b49f-238">Exceptions</span></span>
<span data-ttu-id="0b49f-239">Отчеты [исключения](app-insights-asp-net-exceptions.md) в hello server и hello браузера.</span><span class="sxs-lookup"><span data-stu-id="0b49f-239">Reports [exceptions](app-insights-asp-net-exceptions.md) in hello server and in hello browser.</span></span>

| <span data-ttu-id="0b49f-240">Путь</span><span class="sxs-lookup"><span data-stu-id="0b49f-240">Path</span></span> | <span data-ttu-id="0b49f-241">Тип</span><span class="sxs-lookup"><span data-stu-id="0b49f-241">Type</span></span> | <span data-ttu-id="0b49f-242">Примечания</span><span class="sxs-lookup"><span data-stu-id="0b49f-242">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0b49f-243">basicException [0] assembly</span><span class="sxs-lookup"><span data-stu-id="0b49f-243">basicException [0] assembly</span></span> |<span data-ttu-id="0b49f-244">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-244">string</span></span> | |
| <span data-ttu-id="0b49f-245">basicException [0] count</span><span class="sxs-lookup"><span data-stu-id="0b49f-245">basicException [0] count</span></span> |<span data-ttu-id="0b49f-246">целое число</span><span class="sxs-lookup"><span data-stu-id="0b49f-246">integer</span></span> |<span data-ttu-id="0b49f-247">100/(частота[выборки](app-insights-sampling.md) ).</span><span class="sxs-lookup"><span data-stu-id="0b49f-247">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="0b49f-248">Например, 4 = &gt; 25 %.</span><span class="sxs-lookup"><span data-stu-id="0b49f-248">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="0b49f-249">basicException [0] exceptionGroup</span><span class="sxs-lookup"><span data-stu-id="0b49f-249">basicException [0] exceptionGroup</span></span> |<span data-ttu-id="0b49f-250">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-250">string</span></span> | |
| <span data-ttu-id="0b49f-251">basicException [0] exceptionType</span><span class="sxs-lookup"><span data-stu-id="0b49f-251">basicException [0] exceptionType</span></span> |<span data-ttu-id="0b49f-252">string</span><span class="sxs-lookup"><span data-stu-id="0b49f-252">string</span></span> | |
| <span data-ttu-id="0b49f-253">basicException [0] failedUserCodeMethod</span><span class="sxs-lookup"><span data-stu-id="0b49f-253">basicException [0] failedUserCodeMethod</span></span> |<span data-ttu-id="0b49f-254">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-254">string</span></span> | |
| <span data-ttu-id="0b49f-255">basicException [0] failedUserCodeAssembly</span><span class="sxs-lookup"><span data-stu-id="0b49f-255">basicException [0] failedUserCodeAssembly</span></span> |<span data-ttu-id="0b49f-256">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-256">string</span></span> | |
| <span data-ttu-id="0b49f-257">basicException [0] handledAt</span><span class="sxs-lookup"><span data-stu-id="0b49f-257">basicException [0] handledAt</span></span> |<span data-ttu-id="0b49f-258">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-258">string</span></span> | |
| <span data-ttu-id="0b49f-259">basicException [0] hasFullStack</span><span class="sxs-lookup"><span data-stu-id="0b49f-259">basicException [0] hasFullStack</span></span> |<span data-ttu-id="0b49f-260">Логическое</span><span class="sxs-lookup"><span data-stu-id="0b49f-260">boolean</span></span> | |
| <span data-ttu-id="0b49f-261">basicException [0] id</span><span class="sxs-lookup"><span data-stu-id="0b49f-261">basicException [0] id</span></span> |<span data-ttu-id="0b49f-262">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-262">string</span></span> | |
| <span data-ttu-id="0b49f-263">basicException [0] method</span><span class="sxs-lookup"><span data-stu-id="0b49f-263">basicException [0] method</span></span> |<span data-ttu-id="0b49f-264">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-264">string</span></span> | |
| <span data-ttu-id="0b49f-265">basicException [0] message</span><span class="sxs-lookup"><span data-stu-id="0b49f-265">basicException [0] message</span></span> |<span data-ttu-id="0b49f-266">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-266">string</span></span> |<span data-ttu-id="0b49f-267">Сообщение об исключении.</span><span class="sxs-lookup"><span data-stu-id="0b49f-267">Exception message.</span></span> <span data-ttu-id="0b49f-268">Максимальная длина: 10 000</span><span class="sxs-lookup"><span data-stu-id="0b49f-268">Max length 10k.</span></span> |
| <span data-ttu-id="0b49f-269">basicException [0] outerExceptionMessage</span><span class="sxs-lookup"><span data-stu-id="0b49f-269">basicException [0] outerExceptionMessage</span></span> |<span data-ttu-id="0b49f-270">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-270">string</span></span> | |
| <span data-ttu-id="0b49f-271">basicException [0] outerExceptionThrownAtAssembly</span><span class="sxs-lookup"><span data-stu-id="0b49f-271">basicException [0] outerExceptionThrownAtAssembly</span></span> |<span data-ttu-id="0b49f-272">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-272">string</span></span> | |
| <span data-ttu-id="0b49f-273">basicException [0] outerExceptionThrownAtMethod</span><span class="sxs-lookup"><span data-stu-id="0b49f-273">basicException [0] outerExceptionThrownAtMethod</span></span> |<span data-ttu-id="0b49f-274">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-274">string</span></span> | |
| <span data-ttu-id="0b49f-275">basicException [0] outerExceptionType</span><span class="sxs-lookup"><span data-stu-id="0b49f-275">basicException [0] outerExceptionType</span></span> |<span data-ttu-id="0b49f-276">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-276">string</span></span> | |
| <span data-ttu-id="0b49f-277">basicException [0] outerId</span><span class="sxs-lookup"><span data-stu-id="0b49f-277">basicException [0] outerId</span></span> |<span data-ttu-id="0b49f-278">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-278">string</span></span> | |
| <span data-ttu-id="0b49f-279">basicException [0] parsedStack [0] assembly</span><span class="sxs-lookup"><span data-stu-id="0b49f-279">basicException [0] parsedStack [0] assembly</span></span> |<span data-ttu-id="0b49f-280">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-280">string</span></span> | |
| <span data-ttu-id="0b49f-281">basicException [0] parsedStack [0] fileName</span><span class="sxs-lookup"><span data-stu-id="0b49f-281">basicException [0] parsedStack [0] fileName</span></span> |<span data-ttu-id="0b49f-282">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-282">string</span></span> | |
| <span data-ttu-id="0b49f-283">basicException [0] parsedStack [0] level</span><span class="sxs-lookup"><span data-stu-id="0b49f-283">basicException [0] parsedStack [0] level</span></span> |<span data-ttu-id="0b49f-284">целое число</span><span class="sxs-lookup"><span data-stu-id="0b49f-284">integer</span></span> | |
| <span data-ttu-id="0b49f-285">basicException [0] parsedStack [0] line</span><span class="sxs-lookup"><span data-stu-id="0b49f-285">basicException [0] parsedStack [0] line</span></span> |<span data-ttu-id="0b49f-286">целое число</span><span class="sxs-lookup"><span data-stu-id="0b49f-286">integer</span></span> | |
| <span data-ttu-id="0b49f-287">basicException [0] parsedStack [0] method</span><span class="sxs-lookup"><span data-stu-id="0b49f-287">basicException [0] parsedStack [0] method</span></span> |<span data-ttu-id="0b49f-288">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-288">string</span></span> | |
| <span data-ttu-id="0b49f-289">basicException [0] stack</span><span class="sxs-lookup"><span data-stu-id="0b49f-289">basicException [0] stack</span></span> |<span data-ttu-id="0b49f-290">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-290">string</span></span> |<span data-ttu-id="0b49f-291">Максимальная длина: 10 000</span><span class="sxs-lookup"><span data-stu-id="0b49f-291">Max length 10k</span></span> |
| <span data-ttu-id="0b49f-292">basicException [0] typeName</span><span class="sxs-lookup"><span data-stu-id="0b49f-292">basicException [0] typeName</span></span> |<span data-ttu-id="0b49f-293">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-293">string</span></span> | |

## <a name="trace-messages"></a><span data-ttu-id="0b49f-294">Сообщения трассировки</span><span class="sxs-lookup"><span data-stu-id="0b49f-294">Trace Messages</span></span>
<span data-ttu-id="0b49f-295">Отправленные [TrackTrace](app-insights-api-custom-events-metrics.md#tracktrace), а по hello [адаптеры ведения журналов](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="0b49f-295">Sent by [TrackTrace](app-insights-api-custom-events-metrics.md#tracktrace), and by hello [logging adapters](app-insights-asp-net-trace-logs.md).</span></span>

| <span data-ttu-id="0b49f-296">Путь</span><span class="sxs-lookup"><span data-stu-id="0b49f-296">Path</span></span> | <span data-ttu-id="0b49f-297">Тип</span><span class="sxs-lookup"><span data-stu-id="0b49f-297">Type</span></span> | <span data-ttu-id="0b49f-298">Примечания</span><span class="sxs-lookup"><span data-stu-id="0b49f-298">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0b49f-299">message [0] loggerName</span><span class="sxs-lookup"><span data-stu-id="0b49f-299">message [0] loggerName</span></span> |<span data-ttu-id="0b49f-300">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-300">string</span></span> | |
| <span data-ttu-id="0b49f-301">message [0] parameters</span><span class="sxs-lookup"><span data-stu-id="0b49f-301">message [0] parameters</span></span> |<span data-ttu-id="0b49f-302">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-302">string</span></span> | |
| <span data-ttu-id="0b49f-303">message [0] raw</span><span class="sxs-lookup"><span data-stu-id="0b49f-303">message [0] raw</span></span> |<span data-ttu-id="0b49f-304">string</span><span class="sxs-lookup"><span data-stu-id="0b49f-304">string</span></span> |<span data-ttu-id="0b49f-305">сообщение журнала Hello, максимальной длиной 10 КБ.</span><span class="sxs-lookup"><span data-stu-id="0b49f-305">hello log message, max length 10k.</span></span> |
| <span data-ttu-id="0b49f-306">message [0] severityLevel</span><span class="sxs-lookup"><span data-stu-id="0b49f-306">message [0] severityLevel</span></span> |<span data-ttu-id="0b49f-307">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-307">string</span></span> | |

## <a name="remote-dependency"></a><span data-ttu-id="0b49f-308">Удаленная зависимость</span><span class="sxs-lookup"><span data-stu-id="0b49f-308">Remote dependency</span></span>
<span data-ttu-id="0b49f-309">Отправитель: TrackDependency.</span><span class="sxs-lookup"><span data-stu-id="0b49f-309">Sent by TrackDependency.</span></span> <span data-ttu-id="0b49f-310">Использовать tooreport производительности и использовании [вызывает toodependencies](app-insights-asp-net-dependencies.md) сервера hello и вызовы AJAX в браузере hello.</span><span class="sxs-lookup"><span data-stu-id="0b49f-310">Used tooreport performance and usage of [calls toodependencies](app-insights-asp-net-dependencies.md) in hello server, and AJAX calls in hello browser.</span></span>

| <span data-ttu-id="0b49f-311">Путь</span><span class="sxs-lookup"><span data-stu-id="0b49f-311">Path</span></span> | <span data-ttu-id="0b49f-312">Тип</span><span class="sxs-lookup"><span data-stu-id="0b49f-312">Type</span></span> | <span data-ttu-id="0b49f-313">Примечания</span><span class="sxs-lookup"><span data-stu-id="0b49f-313">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0b49f-314">remoteDependency [0] async</span><span class="sxs-lookup"><span data-stu-id="0b49f-314">remoteDependency [0] async</span></span> |<span data-ttu-id="0b49f-315">Логическое</span><span class="sxs-lookup"><span data-stu-id="0b49f-315">boolean</span></span> | |
| <span data-ttu-id="0b49f-316">remoteDependency [0] baseName</span><span class="sxs-lookup"><span data-stu-id="0b49f-316">remoteDependency [0] baseName</span></span> |<span data-ttu-id="0b49f-317">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-317">string</span></span> | |
| <span data-ttu-id="0b49f-318">remoteDependency [0] commandName</span><span class="sxs-lookup"><span data-stu-id="0b49f-318">remoteDependency [0] commandName</span></span> |<span data-ttu-id="0b49f-319">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-319">string</span></span> |<span data-ttu-id="0b49f-320">Например, home/index</span><span class="sxs-lookup"><span data-stu-id="0b49f-320">For example "home/index"</span></span> |
| <span data-ttu-id="0b49f-321">remoteDependency [0] count</span><span class="sxs-lookup"><span data-stu-id="0b49f-321">remoteDependency [0] count</span></span> |<span data-ttu-id="0b49f-322">целое число</span><span class="sxs-lookup"><span data-stu-id="0b49f-322">integer</span></span> |<span data-ttu-id="0b49f-323">100/(частота[выборки](app-insights-sampling.md) ).</span><span class="sxs-lookup"><span data-stu-id="0b49f-323">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="0b49f-324">Например, 4 = &gt; 25 %.</span><span class="sxs-lookup"><span data-stu-id="0b49f-324">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="0b49f-325">remoteDependency [0] dependencyTypeName</span><span class="sxs-lookup"><span data-stu-id="0b49f-325">remoteDependency [0] dependencyTypeName</span></span> |<span data-ttu-id="0b49f-326">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-326">string</span></span> |<span data-ttu-id="0b49f-327">HTTP, SQL, …</span><span class="sxs-lookup"><span data-stu-id="0b49f-327">HTTP, SQL, ...</span></span> |
| <span data-ttu-id="0b49f-328">remoteDependency [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="0b49f-328">remoteDependency [0] durationMetric.value</span></span> |<span data-ttu-id="0b49f-329">number</span><span class="sxs-lookup"><span data-stu-id="0b49f-329">number</span></span> |<span data-ttu-id="0b49f-330">Время от вызова toocompletion ответа зависимостей</span><span class="sxs-lookup"><span data-stu-id="0b49f-330">Time from call toocompletion of response by dependency</span></span> |
| <span data-ttu-id="0b49f-331">remoteDependency [0] id</span><span class="sxs-lookup"><span data-stu-id="0b49f-331">remoteDependency [0] id</span></span> |<span data-ttu-id="0b49f-332">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-332">string</span></span> | |
| <span data-ttu-id="0b49f-333">remoteDependency [0] name</span><span class="sxs-lookup"><span data-stu-id="0b49f-333">remoteDependency [0] name</span></span> |<span data-ttu-id="0b49f-334">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-334">string</span></span> |<span data-ttu-id="0b49f-335">URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="0b49f-335">Url.</span></span> <span data-ttu-id="0b49f-336">Максимальная длина: 250</span><span class="sxs-lookup"><span data-stu-id="0b49f-336">Max length 250.</span></span> |
| <span data-ttu-id="0b49f-337">remoteDependency [0] resultCode</span><span class="sxs-lookup"><span data-stu-id="0b49f-337">remoteDependency [0] resultCode</span></span> |<span data-ttu-id="0b49f-338">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-338">string</span></span> |<span data-ttu-id="0b49f-339">Из зависимости HTTP.</span><span class="sxs-lookup"><span data-stu-id="0b49f-339">from HTTP dependency</span></span> |
| <span data-ttu-id="0b49f-340">remoteDependency [0] success</span><span class="sxs-lookup"><span data-stu-id="0b49f-340">remoteDependency [0] success</span></span> |<span data-ttu-id="0b49f-341">Логическое</span><span class="sxs-lookup"><span data-stu-id="0b49f-341">boolean</span></span> | |
| <span data-ttu-id="0b49f-342">remoteDependency [0] type</span><span class="sxs-lookup"><span data-stu-id="0b49f-342">remoteDependency [0] type</span></span> |<span data-ttu-id="0b49f-343">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-343">string</span></span> |<span data-ttu-id="0b49f-344">HTTP, SQL, …</span><span class="sxs-lookup"><span data-stu-id="0b49f-344">Http, Sql,...</span></span> |
| <span data-ttu-id="0b49f-345">remoteDependency [0] url</span><span class="sxs-lookup"><span data-stu-id="0b49f-345">remoteDependency [0] url</span></span> |<span data-ttu-id="0b49f-346">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-346">string</span></span> |<span data-ttu-id="0b49f-347">Максимальная длина: 2000</span><span class="sxs-lookup"><span data-stu-id="0b49f-347">Max length 2000</span></span> |
| <span data-ttu-id="0b49f-348">remoteDependency [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="0b49f-348">remoteDependency [0] urlData.base</span></span> |<span data-ttu-id="0b49f-349">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-349">string</span></span> |<span data-ttu-id="0b49f-350">Максимальная длина: 2000</span><span class="sxs-lookup"><span data-stu-id="0b49f-350">Max length 2000</span></span> |
| <span data-ttu-id="0b49f-351">remoteDependency [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="0b49f-351">remoteDependency [0] urlData.hashTag</span></span> |<span data-ttu-id="0b49f-352">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-352">string</span></span> | |
| <span data-ttu-id="0b49f-353">remoteDependency [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="0b49f-353">remoteDependency [0] urlData.host</span></span> |<span data-ttu-id="0b49f-354">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-354">string</span></span> |<span data-ttu-id="0b49f-355">Максимальная длина: 200</span><span class="sxs-lookup"><span data-stu-id="0b49f-355">Max length 200</span></span> |

## <a name="requests"></a><span data-ttu-id="0b49f-356">Requests (Запросы)</span><span class="sxs-lookup"><span data-stu-id="0b49f-356">Requests</span></span>
<span data-ttu-id="0b49f-357">Отправитель: [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest).</span><span class="sxs-lookup"><span data-stu-id="0b49f-357">Sent by [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest).</span></span> <span data-ttu-id="0b49f-358">Стандартные модули Hello использовать этот tooreports время ответа сервера, на сервере hello.</span><span class="sxs-lookup"><span data-stu-id="0b49f-358">hello standard modules use this tooreports server response time, measured at hello server.</span></span>

| <span data-ttu-id="0b49f-359">Путь</span><span class="sxs-lookup"><span data-stu-id="0b49f-359">Path</span></span> | <span data-ttu-id="0b49f-360">Тип</span><span class="sxs-lookup"><span data-stu-id="0b49f-360">Type</span></span> | <span data-ttu-id="0b49f-361">Примечания</span><span class="sxs-lookup"><span data-stu-id="0b49f-361">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0b49f-362">request [0] count</span><span class="sxs-lookup"><span data-stu-id="0b49f-362">request [0] count</span></span> |<span data-ttu-id="0b49f-363">целое число</span><span class="sxs-lookup"><span data-stu-id="0b49f-363">integer</span></span> |<span data-ttu-id="0b49f-364">100/(частота[выборки](app-insights-sampling.md) ).</span><span class="sxs-lookup"><span data-stu-id="0b49f-364">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="0b49f-365">Например: 4 =&gt; 25 %.</span><span class="sxs-lookup"><span data-stu-id="0b49f-365">For example: 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="0b49f-366">request [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="0b49f-366">request [0] durationMetric.value</span></span> |<span data-ttu-id="0b49f-367">number</span><span class="sxs-lookup"><span data-stu-id="0b49f-367">number</span></span> |<span data-ttu-id="0b49f-368">Время от tooresponse поступающих запросов.</span><span class="sxs-lookup"><span data-stu-id="0b49f-368">Time from request arriving tooresponse.</span></span> <span data-ttu-id="0b49f-369">1e7 = 1 с.</span><span class="sxs-lookup"><span data-stu-id="0b49f-369">1e7 == 1s</span></span> |
| <span data-ttu-id="0b49f-370">request [0] id</span><span class="sxs-lookup"><span data-stu-id="0b49f-370">request [0] id</span></span> |<span data-ttu-id="0b49f-371">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-371">string</span></span> |<span data-ttu-id="0b49f-372">Идентификатор операции</span><span class="sxs-lookup"><span data-stu-id="0b49f-372">Operation id</span></span> |
| <span data-ttu-id="0b49f-373">request [0] name</span><span class="sxs-lookup"><span data-stu-id="0b49f-373">request [0] name</span></span> |<span data-ttu-id="0b49f-374">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-374">string</span></span> |<span data-ttu-id="0b49f-375">GET или POST + базовый URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="0b49f-375">GET/POST + url base.</span></span>  <span data-ttu-id="0b49f-376">Максимальная длина: 250</span><span class="sxs-lookup"><span data-stu-id="0b49f-376">Max length 250</span></span> |
| <span data-ttu-id="0b49f-377">request [0] responseCode</span><span class="sxs-lookup"><span data-stu-id="0b49f-377">request [0] responseCode</span></span> |<span data-ttu-id="0b49f-378">целое число</span><span class="sxs-lookup"><span data-stu-id="0b49f-378">integer</span></span> |<span data-ttu-id="0b49f-379">Отправлено ответов tooclient HTTP</span><span class="sxs-lookup"><span data-stu-id="0b49f-379">HTTP response sent tooclient</span></span> |
| <span data-ttu-id="0b49f-380">request [0] success</span><span class="sxs-lookup"><span data-stu-id="0b49f-380">request [0] success</span></span> |<span data-ttu-id="0b49f-381">Логическое</span><span class="sxs-lookup"><span data-stu-id="0b49f-381">boolean</span></span> |<span data-ttu-id="0b49f-382">Значение по умолчанию == (responseCode &lt; 400)</span><span class="sxs-lookup"><span data-stu-id="0b49f-382">Default == (responseCode &lt; 400)</span></span> |
| <span data-ttu-id="0b49f-383">request [0] url</span><span class="sxs-lookup"><span data-stu-id="0b49f-383">request [0] url</span></span> |<span data-ttu-id="0b49f-384">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-384">string</span></span> |<span data-ttu-id="0b49f-385">Не включая узел.</span><span class="sxs-lookup"><span data-stu-id="0b49f-385">Not including host</span></span> |
| <span data-ttu-id="0b49f-386">request [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="0b49f-386">request [0] urlData.base</span></span> |<span data-ttu-id="0b49f-387">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-387">string</span></span> | |
| <span data-ttu-id="0b49f-388">request [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="0b49f-388">request [0] urlData.hashTag</span></span> |<span data-ttu-id="0b49f-389">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-389">string</span></span> | |
| <span data-ttu-id="0b49f-390">request [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="0b49f-390">request [0] urlData.host</span></span> |<span data-ttu-id="0b49f-391">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-391">string</span></span> | |

## <a name="page-view-performance"></a><span data-ttu-id="0b49f-392">Производительность просмотра страницы</span><span class="sxs-lookup"><span data-stu-id="0b49f-392">Page View Performance</span></span>
<span data-ttu-id="0b49f-393">Отправленные hello браузера.</span><span class="sxs-lookup"><span data-stu-id="0b49f-393">Sent by hello browser.</span></span> <span data-ttu-id="0b49f-394">Меры hello tooprocess время страницы, от пользователя вызывающей стороны hello запроса toodisplay завершения (за исключением асинхронные вызовы AJAX).</span><span class="sxs-lookup"><span data-stu-id="0b49f-394">Measures hello time tooprocess a page, from user initiating hello request toodisplay complete (excluding async AJAX calls).</span></span>

<span data-ttu-id="0b49f-395">Контекстные значения показывают версию клиентской ОС и версию браузера.</span><span class="sxs-lookup"><span data-stu-id="0b49f-395">Context values show client OS and browser version.</span></span>

| <span data-ttu-id="0b49f-396">Путь</span><span class="sxs-lookup"><span data-stu-id="0b49f-396">Path</span></span> | <span data-ttu-id="0b49f-397">Тип</span><span class="sxs-lookup"><span data-stu-id="0b49f-397">Type</span></span> | <span data-ttu-id="0b49f-398">Примечания</span><span class="sxs-lookup"><span data-stu-id="0b49f-398">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0b49f-399">clientPerformance [0] clientProcess.value</span><span class="sxs-lookup"><span data-stu-id="0b49f-399">clientPerformance [0] clientProcess.value</span></span> |<span data-ttu-id="0b49f-400">целое число</span><span class="sxs-lookup"><span data-stu-id="0b49f-400">integer</span></span> |<span data-ttu-id="0b49f-401">Время в конце получение toodisplaying hello hello HTML-страницы.</span><span class="sxs-lookup"><span data-stu-id="0b49f-401">Time from end of receiving hello HTML toodisplaying hello page.</span></span> |
| <span data-ttu-id="0b49f-402">clientPerformance [0] name</span><span class="sxs-lookup"><span data-stu-id="0b49f-402">clientPerformance [0] name</span></span> |<span data-ttu-id="0b49f-403">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-403">string</span></span> | |
| <span data-ttu-id="0b49f-404">clientPerformance [0] networkConnection.value</span><span class="sxs-lookup"><span data-stu-id="0b49f-404">clientPerformance [0] networkConnection.value</span></span> |<span data-ttu-id="0b49f-405">целое число</span><span class="sxs-lookup"><span data-stu-id="0b49f-405">integer</span></span> |<span data-ttu-id="0b49f-406">Время, затраченное tooestablish сетевое подключение.</span><span class="sxs-lookup"><span data-stu-id="0b49f-406">Time taken tooestablish a network connection.</span></span> |
| <span data-ttu-id="0b49f-407">clientPerformance [0] receiveRequest.value</span><span class="sxs-lookup"><span data-stu-id="0b49f-407">clientPerformance [0] receiveRequest.value</span></span> |<span data-ttu-id="0b49f-408">целое число</span><span class="sxs-lookup"><span data-stu-id="0b49f-408">integer</span></span> |<span data-ttu-id="0b49f-409">Время в конце отправки hello запроса tooreceiving hello HTML в ответе.</span><span class="sxs-lookup"><span data-stu-id="0b49f-409">Time from end of sending hello request tooreceiving hello HTML in reply.</span></span> |
| <span data-ttu-id="0b49f-410">clientPerformance [0] sendRequest.value</span><span class="sxs-lookup"><span data-stu-id="0b49f-410">clientPerformance [0] sendRequest.value</span></span> |<span data-ttu-id="0b49f-411">целое число</span><span class="sxs-lookup"><span data-stu-id="0b49f-411">integer</span></span> |<span data-ttu-id="0b49f-412">Время от запроса сделанной toosend hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="0b49f-412">Time from taken toosend hello HTTP request.</span></span> |
| <span data-ttu-id="0b49f-413">clientPerformance [0] total.value</span><span class="sxs-lookup"><span data-stu-id="0b49f-413">clientPerformance [0] total.value</span></span> |<span data-ttu-id="0b49f-414">целое число</span><span class="sxs-lookup"><span data-stu-id="0b49f-414">integer</span></span> |<span data-ttu-id="0b49f-415">Время от начала страницы toosend hello запроса toodisplaying hello.</span><span class="sxs-lookup"><span data-stu-id="0b49f-415">Time from starting toosend hello request toodisplaying hello page.</span></span> |
| <span data-ttu-id="0b49f-416">clientPerformance [0] url</span><span class="sxs-lookup"><span data-stu-id="0b49f-416">clientPerformance [0] url</span></span> |<span data-ttu-id="0b49f-417">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-417">string</span></span> |<span data-ttu-id="0b49f-418">URL-адрес запроса.</span><span class="sxs-lookup"><span data-stu-id="0b49f-418">URL of this request</span></span> |
| <span data-ttu-id="0b49f-419">clientPerformance [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="0b49f-419">clientPerformance [0] urlData.base</span></span> |<span data-ttu-id="0b49f-420">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-420">string</span></span> | |
| <span data-ttu-id="0b49f-421">clientPerformance [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="0b49f-421">clientPerformance [0] urlData.hashTag</span></span> |<span data-ttu-id="0b49f-422">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-422">string</span></span> | |
| <span data-ttu-id="0b49f-423">clientPerformance [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="0b49f-423">clientPerformance [0] urlData.host</span></span> |<span data-ttu-id="0b49f-424">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-424">string</span></span> | |
| <span data-ttu-id="0b49f-425">clientPerformance [0] urlData.protocol</span><span class="sxs-lookup"><span data-stu-id="0b49f-425">clientPerformance [0] urlData.protocol</span></span> |<span data-ttu-id="0b49f-426">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-426">string</span></span> | |

## <a name="page-views"></a><span data-ttu-id="0b49f-427">Просмотры страницы</span><span class="sxs-lookup"><span data-stu-id="0b49f-427">Page Views</span></span>
<span data-ttu-id="0b49f-428">Отправитель: trackPageView() или [stopTrackPage](app-insights-api-custom-events-metrics.md#page-views)</span><span class="sxs-lookup"><span data-stu-id="0b49f-428">Sent by trackPageView() or [stopTrackPage](app-insights-api-custom-events-metrics.md#page-views)</span></span>

| <span data-ttu-id="0b49f-429">Путь</span><span class="sxs-lookup"><span data-stu-id="0b49f-429">Path</span></span> | <span data-ttu-id="0b49f-430">Тип</span><span class="sxs-lookup"><span data-stu-id="0b49f-430">Type</span></span> | <span data-ttu-id="0b49f-431">Примечания</span><span class="sxs-lookup"><span data-stu-id="0b49f-431">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0b49f-432">view [0] count</span><span class="sxs-lookup"><span data-stu-id="0b49f-432">view [0] count</span></span> |<span data-ttu-id="0b49f-433">целое число</span><span class="sxs-lookup"><span data-stu-id="0b49f-433">integer</span></span> |<span data-ttu-id="0b49f-434">100/(частота[выборки](app-insights-sampling.md) ).</span><span class="sxs-lookup"><span data-stu-id="0b49f-434">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="0b49f-435">Например, 4 = &gt; 25 %.</span><span class="sxs-lookup"><span data-stu-id="0b49f-435">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="0b49f-436">view [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="0b49f-436">view [0] durationMetric.value</span></span> |<span data-ttu-id="0b49f-437">целое число</span><span class="sxs-lookup"><span data-stu-id="0b49f-437">integer</span></span> |<span data-ttu-id="0b49f-438">При необходимости значение можно указать в методе trackPageView() или с помощью метода start/stopTrackPage().</span><span class="sxs-lookup"><span data-stu-id="0b49f-438">Value optionally set in trackPageView() or by startTrackPage() - stopTrackPage().</span></span> <span data-ttu-id="0b49f-439">Не Здравствуйте таким же, как clientPerformance значения.</span><span class="sxs-lookup"><span data-stu-id="0b49f-439">Not hello same as clientPerformance values.</span></span> |
| <span data-ttu-id="0b49f-440">view [0] name</span><span class="sxs-lookup"><span data-stu-id="0b49f-440">view [0] name</span></span> |<span data-ttu-id="0b49f-441">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-441">string</span></span> |<span data-ttu-id="0b49f-442">Заголовок страницы.</span><span class="sxs-lookup"><span data-stu-id="0b49f-442">Page title.</span></span>  <span data-ttu-id="0b49f-443">Максимальная длина: 250</span><span class="sxs-lookup"><span data-stu-id="0b49f-443">Max length 250</span></span> |
| <span data-ttu-id="0b49f-444">view [0] url</span><span class="sxs-lookup"><span data-stu-id="0b49f-444">view [0] url</span></span> |<span data-ttu-id="0b49f-445">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-445">string</span></span> | |
| <span data-ttu-id="0b49f-446">view [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="0b49f-446">view [0] urlData.base</span></span> |<span data-ttu-id="0b49f-447">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-447">string</span></span> | |
| <span data-ttu-id="0b49f-448">view [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="0b49f-448">view [0] urlData.hashTag</span></span> |<span data-ttu-id="0b49f-449">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-449">string</span></span> | |
| <span data-ttu-id="0b49f-450">view [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="0b49f-450">view [0] urlData.host</span></span> |<span data-ttu-id="0b49f-451">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-451">string</span></span> | |

## <a name="availability"></a><span data-ttu-id="0b49f-452">Доступность</span><span class="sxs-lookup"><span data-stu-id="0b49f-452">Availability</span></span>
<span data-ttu-id="0b49f-453">Это свойство создает отчеты о [веб-тестах на доступность](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="0b49f-453">Reports [availability web tests](app-insights-monitor-web-app-availability.md).</span></span>

| <span data-ttu-id="0b49f-454">Путь</span><span class="sxs-lookup"><span data-stu-id="0b49f-454">Path</span></span> | <span data-ttu-id="0b49f-455">Тип</span><span class="sxs-lookup"><span data-stu-id="0b49f-455">Type</span></span> | <span data-ttu-id="0b49f-456">Примечания</span><span class="sxs-lookup"><span data-stu-id="0b49f-456">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0b49f-457">availability [0] availabilityMetric.name</span><span class="sxs-lookup"><span data-stu-id="0b49f-457">availability [0] availabilityMetric.name</span></span> |<span data-ttu-id="0b49f-458">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-458">string</span></span> |<span data-ttu-id="0b49f-459">Доступность</span><span class="sxs-lookup"><span data-stu-id="0b49f-459">availability</span></span> |
| <span data-ttu-id="0b49f-460">availability [0] availabilityMetric.value</span><span class="sxs-lookup"><span data-stu-id="0b49f-460">availability [0] availabilityMetric.value</span></span> |<span data-ttu-id="0b49f-461">number</span><span class="sxs-lookup"><span data-stu-id="0b49f-461">number</span></span> |<span data-ttu-id="0b49f-462">1,0 или 0,0.</span><span class="sxs-lookup"><span data-stu-id="0b49f-462">1.0 or 0.0</span></span> |
| <span data-ttu-id="0b49f-463">availability [0] count</span><span class="sxs-lookup"><span data-stu-id="0b49f-463">availability [0] count</span></span> |<span data-ttu-id="0b49f-464">целое число</span><span class="sxs-lookup"><span data-stu-id="0b49f-464">integer</span></span> |<span data-ttu-id="0b49f-465">100/(частота[выборки](app-insights-sampling.md) ).</span><span class="sxs-lookup"><span data-stu-id="0b49f-465">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="0b49f-466">Например, 4 = &gt; 25 %.</span><span class="sxs-lookup"><span data-stu-id="0b49f-466">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="0b49f-467">availability [0] dataSizeMetric.name</span><span class="sxs-lookup"><span data-stu-id="0b49f-467">availability [0] dataSizeMetric.name</span></span> |<span data-ttu-id="0b49f-468">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-468">string</span></span> | |
| <span data-ttu-id="0b49f-469">availability [0] dataSizeMetric.value</span><span class="sxs-lookup"><span data-stu-id="0b49f-469">availability [0] dataSizeMetric.value</span></span> |<span data-ttu-id="0b49f-470">целое число</span><span class="sxs-lookup"><span data-stu-id="0b49f-470">integer</span></span> | |
| <span data-ttu-id="0b49f-471">availability [0] durationMetric.name</span><span class="sxs-lookup"><span data-stu-id="0b49f-471">availability [0] durationMetric.name</span></span> |<span data-ttu-id="0b49f-472">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-472">string</span></span> | |
| <span data-ttu-id="0b49f-473">availability [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="0b49f-473">availability [0] durationMetric.value</span></span> |<span data-ttu-id="0b49f-474">number</span><span class="sxs-lookup"><span data-stu-id="0b49f-474">number</span></span> |<span data-ttu-id="0b49f-475">Продолжительность теста.</span><span class="sxs-lookup"><span data-stu-id="0b49f-475">Duration of test.</span></span> <span data-ttu-id="0b49f-476">1e7 = 1 с.</span><span class="sxs-lookup"><span data-stu-id="0b49f-476">1e7==1s</span></span> |
| <span data-ttu-id="0b49f-477">availability [0] message</span><span class="sxs-lookup"><span data-stu-id="0b49f-477">availability [0] message</span></span> |<span data-ttu-id="0b49f-478">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-478">string</span></span> |<span data-ttu-id="0b49f-479">Диагностика сбоя.</span><span class="sxs-lookup"><span data-stu-id="0b49f-479">Failure diagnostic</span></span> |
| <span data-ttu-id="0b49f-480">availability [0] result</span><span class="sxs-lookup"><span data-stu-id="0b49f-480">availability [0] result</span></span> |<span data-ttu-id="0b49f-481">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-481">string</span></span> |<span data-ttu-id="0b49f-482">Успех или сбой.</span><span class="sxs-lookup"><span data-stu-id="0b49f-482">Pass/Fail</span></span> |
| <span data-ttu-id="0b49f-483">availability [0] runLocation</span><span class="sxs-lookup"><span data-stu-id="0b49f-483">availability [0] runLocation</span></span> |<span data-ttu-id="0b49f-484">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-484">string</span></span> |<span data-ttu-id="0b49f-485">Географический объект-источник HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="0b49f-485">Geo source of http req</span></span> |
| <span data-ttu-id="0b49f-486">availability [0] testName</span><span class="sxs-lookup"><span data-stu-id="0b49f-486">availability [0] testName</span></span> |<span data-ttu-id="0b49f-487">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-487">string</span></span> | |
| <span data-ttu-id="0b49f-488">availability [0] testRunId</span><span class="sxs-lookup"><span data-stu-id="0b49f-488">availability [0] testRunId</span></span> |<span data-ttu-id="0b49f-489">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-489">string</span></span> | |
| <span data-ttu-id="0b49f-490">availability [0] testTimestamp</span><span class="sxs-lookup"><span data-stu-id="0b49f-490">availability [0] testTimestamp</span></span> |<span data-ttu-id="0b49f-491">строка</span><span class="sxs-lookup"><span data-stu-id="0b49f-491">string</span></span> | |

## <a name="metrics"></a><span data-ttu-id="0b49f-492">Метрики</span><span class="sxs-lookup"><span data-stu-id="0b49f-492">Metrics</span></span>
<span data-ttu-id="0b49f-493">Создатель: TrackMetric().</span><span class="sxs-lookup"><span data-stu-id="0b49f-493">Generated by TrackMetric().</span></span>

<span data-ttu-id="0b49f-494">найдено значение метрики Hello в context.custom.metrics[0]</span><span class="sxs-lookup"><span data-stu-id="0b49f-494">hello metric value is found in context.custom.metrics[0]</span></span>

<span data-ttu-id="0b49f-495">Например:</span><span class="sxs-lookup"><span data-stu-id="0b49f-495">For example:</span></span>

    {
     "metric": [ ],
     "context": {
     ...
     "custom": {
        "dimensions": [
          { "ProcessId": "4068" }
        ],
        "metrics": [
          {
            "dispatchRate": {
              "value": 0.001295,
              "count": 1.0,
              "min": 0.001295,
              "max": 0.001295,
              "stdDev": 0.0,
              "sampledValue": 0.001295,
              "sum": 0.001295
            }
          }
         } ] }
    }

## <a name="about-metric-values"></a><span data-ttu-id="0b49f-496">О значениях метрик</span><span class="sxs-lookup"><span data-stu-id="0b49f-496">About metric values</span></span>
<span data-ttu-id="0b49f-497">Значения метрик (как в отчетах, так и в других элементах) сообщаются в рамках стандартной структуры объекта.</span><span class="sxs-lookup"><span data-stu-id="0b49f-497">Metric values, both in metric reports and elsewhere, are reported with a standard object structure.</span></span> <span data-ttu-id="0b49f-498">Например:</span><span class="sxs-lookup"><span data-stu-id="0b49f-498">For example:</span></span>

      "durationMetric": {
        "name": "contoso.org",
        "type": "Aggregation",
        "value": 468.71603053650279,
        "count": 1.0,
        "min": 468.71603053650279,
        "max": 468.71603053650279,
        "stdDev": 0.0,
        "sampledValue": 468.71603053650279
      }

<span data-ttu-id="0b49f-499">В настоящее время - то, что это может изменить в будущих - сообщили hello стандартные модули SDK, все значения hello `count==1` и только hello `name` и `value` поля могут быть полезны.</span><span class="sxs-lookup"><span data-stu-id="0b49f-499">Currently - though this might change in hello future - in all values reported from hello standard SDK modules, `count==1` and only hello `name` and `value` fields are useful.</span></span> <span data-ttu-id="0b49f-500">Hello единственный случай, где они будут отличаться бы при написании TrackMetric вызовы в которых hello другие параметры.</span><span class="sxs-lookup"><span data-stu-id="0b49f-500">hello only case where they would be different would be if you write your own TrackMetric calls in which you set hello other parameters.</span></span>

<span data-ttu-id="0b49f-501">Здравствуйте, назначение hello остальные поля — toobe tooallow метрики, статистически hello SDK tooreduce трафика toohello портала.</span><span class="sxs-lookup"><span data-stu-id="0b49f-501">hello purpose of hello other fields is tooallow metrics toobe aggregated in hello SDK, tooreduce traffic toohello portal.</span></span> <span data-ttu-id="0b49f-502">Например, перед отправкой каждого отчета с метриками вы можете получить среднее значение для нескольких последовательных показаний.</span><span class="sxs-lookup"><span data-stu-id="0b49f-502">For example, you could average several successive readings before sending each metric report.</span></span> <span data-ttu-id="0b49f-503">Затем будет расчета hello min, max, стандартное отклонение и статистическое значение (сумма или среднее) и задайте заданное число toohello показания, представленный hello отчета.</span><span class="sxs-lookup"><span data-stu-id="0b49f-503">Then you would calculate hello min, max, standard deviation and aggregate value (sum or average) and set count toohello number of readings represented by hello report.</span></span>

<span data-ttu-id="0b49f-504">В таблицах hello выше мы опущен hello редко используемые поля count, min, max, stdDev и sampledValue.</span><span class="sxs-lookup"><span data-stu-id="0b49f-504">In hello tables above, we have omitted hello rarely-used fields count, min, max, stdDev and sampledValue.</span></span>

<span data-ttu-id="0b49f-505">Вместо предварительной статистической обработке метрик, можно использовать [выборки](app-insights-sampling.md) при необходимости tooreduce hello объем телеметрии.</span><span class="sxs-lookup"><span data-stu-id="0b49f-505">Instead of pre-aggregating metrics, you can use [sampling](app-insights-sampling.md) if you need tooreduce hello volume of telemetry.</span></span>

### <a name="durations"></a><span data-ttu-id="0b49f-506">Длительность</span><span class="sxs-lookup"><span data-stu-id="0b49f-506">Durations</span></span>
<span data-ttu-id="0b49f-507">За исключением оговоренных случаев, показатели длительности представлены в десятых долях микросекунды, то есть 10 000 000,0 — это 1 с.</span><span class="sxs-lookup"><span data-stu-id="0b49f-507">Except where otherwise noted, durations are represented in tenths of a microsecond, so that 10000000.0 means 1 second.</span></span>

## <a name="see-also"></a><span data-ttu-id="0b49f-508">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="0b49f-508">See also</span></span>
* [<span data-ttu-id="0b49f-509">Application Insights</span><span class="sxs-lookup"><span data-stu-id="0b49f-509">Application Insights</span></span>](app-insights-overview.md)
* [<span data-ttu-id="0b49f-510">Непрерывный экспорт</span><span class="sxs-lookup"><span data-stu-id="0b49f-510">Continuous Export</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="0b49f-511">Примеры кода</span><span class="sxs-lookup"><span data-stu-id="0b49f-511">Code samples</span></span>](app-insights-export-telemetry.md#code-samples)
