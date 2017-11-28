---
title: "Модель данных Azure Application Insights | Документация Майкрософт"
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
ms.openlocfilehash: a485ddd555f65473d81896effc4a3562bda71410
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-export-data-model"></a><span data-ttu-id="e8ac9-103">Экспорт модели данных Application Insights</span><span class="sxs-lookup"><span data-stu-id="e8ac9-103">Application Insights Export Data Model</span></span>
<span data-ttu-id="e8ac9-104">В этой таблице перечислены свойства телеметрии, отправляемой из различных пакетов SDK для [Application Insights](app-insights-overview.md) на портал.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-104">This table lists the properties of telemetry sent from the [Application Insights](app-insights-overview.md) SDKs to the portal.</span></span>
<span data-ttu-id="e8ac9-105">Вы увидите эти свойства в выходных данных [непрерывного экспорта](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="e8ac9-105">You'll see these properties in data output from [Continuous Export](app-insights-export-telemetry.md).</span></span>
<span data-ttu-id="e8ac9-106">Они также отображаются в фильтрах свойств в [обозревателе метрик](app-insights-metrics-explorer.md) и при [диагностическом поиске](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="e8ac9-106">They also appear in property filters in [Metric Explorer](app-insights-metrics-explorer.md) and [Diagnostic Search](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="e8ac9-107">Примечания:</span><span class="sxs-lookup"><span data-stu-id="e8ac9-107">Points to note:</span></span>

* <span data-ttu-id="e8ac9-108">`[0]` в этих таблицах обозначает точку в пути, куда необходимо вставить индекс. При этом значение не всегда равно 0.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-108">`[0]` in these tables denotes a point in the path where you have to insert an index; but it isn't always 0.</span></span>
* <span data-ttu-id="e8ac9-109">Продолжительность времени указана в десятых долях микросекунды, поэтому 10 000 000 = 1 с.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-109">Time durations are in tenths of a microsecond, so 10000000 == 1 second.</span></span>
* <span data-ttu-id="e8ac9-110">Значения даты и времени в формате UTC указаны в формате ISO `yyyy-MM-DDThh:mm:ss.sssZ`</span><span class="sxs-lookup"><span data-stu-id="e8ac9-110">Dates and times are UTC, and are given in the ISO format `yyyy-MM-DDThh:mm:ss.sssZ`</span></span>


## <a name="example"></a><span data-ttu-id="e8ac9-111">Пример</span><span class="sxs-lookup"><span data-stu-id="e8ac9-111">Example</span></span>
    // A server report about an HTTP request
    {
    "request": [
      {
        "urlData": { // derived from 'url'
          "host": "contoso.org",
          "base": "/",
          "hashTag": ""
        },
        "responseCode": 200, // Sent to client
        "success": true, // Default == responseCode<400
        // Request id becomes the operation id of child events
        "id": "fCOhCdCnZ9I=",  
        "name": "GET Home/Index",
        "count": 1, // 100% / sampling rate
        "durationMetric": {
          "value": 1046804.0, // 10000000 == 1 second
          // Currently the following fields are redundant:
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
        // last octagon is anonymized to 0 at portal:
        "clientip": "168.62.177.0",
        "province": "",
        "city": ""
      },
      "data": {
        "isSynthetic": true, // we identified source as a bot
        // percentage of generated data sent to portal:
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
  <span data-ttu-id="e8ac9-112">}</span><span class="sxs-lookup"><span data-stu-id="e8ac9-112">}</span></span>

## <a name="context"></a><span data-ttu-id="e8ac9-113">Context</span><span class="sxs-lookup"><span data-stu-id="e8ac9-113">Context</span></span>
<span data-ttu-id="e8ac9-114">Для каждого типа данных телеметрии приведен пример с разделом контекста.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-114">All types of telemetry are accompanied by a context section.</span></span> <span data-ttu-id="e8ac9-115">Не все эти поля передаются со всеми точками данных.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-115">Not all of these fields are transmitted with every data point.</span></span>

| <span data-ttu-id="e8ac9-116">Путь</span><span class="sxs-lookup"><span data-stu-id="e8ac9-116">Path</span></span> | <span data-ttu-id="e8ac9-117">Тип</span><span class="sxs-lookup"><span data-stu-id="e8ac9-117">Type</span></span> | <span data-ttu-id="e8ac9-118">Примечания</span><span class="sxs-lookup"><span data-stu-id="e8ac9-118">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e8ac9-119">context.custom.dimensions [0]</span><span class="sxs-lookup"><span data-stu-id="e8ac9-119">context.custom.dimensions [0]</span></span> |<span data-ttu-id="e8ac9-120">объект [ ]</span><span class="sxs-lookup"><span data-stu-id="e8ac9-120">object [ ]</span></span> |<span data-ttu-id="e8ac9-121">Набор пар "ключ — значение", заданный параметром пользовательских свойств.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-121">Key-value string pairs set by custom properties parameter.</span></span> <span data-ttu-id="e8ac9-122">Максимальная длина ключа — 100, максимальная длина значения —1024.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-122">Key max length 100, values max length 1024.</span></span> <span data-ttu-id="e8ac9-123">Более 100 уникальных значений. Свойства можно использовать для поиска, но не для сегментации.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-123">More than 100 unique values, the property can be searched but cannot be used for segmentation.</span></span> <span data-ttu-id="e8ac9-124">Максимальное количество — 200 ключей на ключ ikey.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-124">Max 200 keys per ikey.</span></span> |
| <span data-ttu-id="e8ac9-125">context.custom.metrics [0]</span><span class="sxs-lookup"><span data-stu-id="e8ac9-125">context.custom.metrics [0]</span></span> |<span data-ttu-id="e8ac9-126">объект [ ]</span><span class="sxs-lookup"><span data-stu-id="e8ac9-126">object [ ]</span></span> |<span data-ttu-id="e8ac9-127">Набор пар "ключ — значение", заданный параметром пользовательских измерений и метриками TrackMetric.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-127">Key-value pairs set by custom measurements parameter and by TrackMetrics.</span></span> <span data-ttu-id="e8ac9-128">Максимальная длина ключа — 100. Значения могут быть числовыми.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-128">Key max length 100, values may be numeric.</span></span> |
| <span data-ttu-id="e8ac9-129">context.data.eventTime</span><span class="sxs-lookup"><span data-stu-id="e8ac9-129">context.data.eventTime</span></span> |<span data-ttu-id="e8ac9-130">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-130">string</span></span> |<span data-ttu-id="e8ac9-131">Формат UTC.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-131">UTC</span></span> |
| <span data-ttu-id="e8ac9-132">context.data.isSynthetic</span><span class="sxs-lookup"><span data-stu-id="e8ac9-132">context.data.isSynthetic</span></span> |<span data-ttu-id="e8ac9-133">Логическое</span><span class="sxs-lookup"><span data-stu-id="e8ac9-133">boolean</span></span> |<span data-ttu-id="e8ac9-134">Запрос поступает от программы-робота или веб-теста.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-134">Request appears to come from a bot or web test.</span></span> |
| <span data-ttu-id="e8ac9-135">context.data.samplingRate</span><span class="sxs-lookup"><span data-stu-id="e8ac9-135">context.data.samplingRate</span></span> |<span data-ttu-id="e8ac9-136">number</span><span class="sxs-lookup"><span data-stu-id="e8ac9-136">number</span></span> |<span data-ttu-id="e8ac9-137">Процентная доля данных телеметрии, созданных с помощью пакета SDK, отправленного на портал.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-137">Percentage of telemetry generated by the SDK that is sent to portal.</span></span> <span data-ttu-id="e8ac9-138">Диапазон 0,0–100,0.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-138">Range 0.0-100.0.</span></span> |
| <span data-ttu-id="e8ac9-139">context.device</span><span class="sxs-lookup"><span data-stu-id="e8ac9-139">context.device</span></span> |<span data-ttu-id="e8ac9-140">object</span><span class="sxs-lookup"><span data-stu-id="e8ac9-140">object</span></span> |<span data-ttu-id="e8ac9-141">Устройство клиента</span><span class="sxs-lookup"><span data-stu-id="e8ac9-141">Client device</span></span> |
| <span data-ttu-id="e8ac9-142">context.device.browser</span><span class="sxs-lookup"><span data-stu-id="e8ac9-142">context.device.browser</span></span> |<span data-ttu-id="e8ac9-143">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-143">string</span></span> |<span data-ttu-id="e8ac9-144">IE, Chrome…</span><span class="sxs-lookup"><span data-stu-id="e8ac9-144">IE, Chrome, ...</span></span> |
| <span data-ttu-id="e8ac9-145">context.device.browserVersion</span><span class="sxs-lookup"><span data-stu-id="e8ac9-145">context.device.browserVersion</span></span> |<span data-ttu-id="e8ac9-146">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-146">string</span></span> |<span data-ttu-id="e8ac9-147">Chrome 48.0…</span><span class="sxs-lookup"><span data-stu-id="e8ac9-147">Chrome 48.0, ...</span></span> |
| <span data-ttu-id="e8ac9-148">context.device.deviceModel</span><span class="sxs-lookup"><span data-stu-id="e8ac9-148">context.device.deviceModel</span></span> |<span data-ttu-id="e8ac9-149">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-149">string</span></span> | |
| <span data-ttu-id="e8ac9-150">context.device.deviceName</span><span class="sxs-lookup"><span data-stu-id="e8ac9-150">context.device.deviceName</span></span> |<span data-ttu-id="e8ac9-151">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-151">string</span></span> | |
| <span data-ttu-id="e8ac9-152">context.device.id</span><span class="sxs-lookup"><span data-stu-id="e8ac9-152">context.device.id</span></span> |<span data-ttu-id="e8ac9-153">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-153">string</span></span> | |
| <span data-ttu-id="e8ac9-154">context.device.locale</span><span class="sxs-lookup"><span data-stu-id="e8ac9-154">context.device.locale</span></span> |<span data-ttu-id="e8ac9-155">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-155">string</span></span> |<span data-ttu-id="e8ac9-156">en-GB, de-DE…</span><span class="sxs-lookup"><span data-stu-id="e8ac9-156">en-GB, de-DE, ...</span></span> |
| <span data-ttu-id="e8ac9-157">context.device.network</span><span class="sxs-lookup"><span data-stu-id="e8ac9-157">context.device.network</span></span> |<span data-ttu-id="e8ac9-158">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-158">string</span></span> | |
| <span data-ttu-id="e8ac9-159">context.device.oemName</span><span class="sxs-lookup"><span data-stu-id="e8ac9-159">context.device.oemName</span></span> |<span data-ttu-id="e8ac9-160">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-160">string</span></span> | |
| <span data-ttu-id="e8ac9-161">context.device.osVersion</span><span class="sxs-lookup"><span data-stu-id="e8ac9-161">context.device.osVersion</span></span> |<span data-ttu-id="e8ac9-162">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-162">string</span></span> |<span data-ttu-id="e8ac9-163">ОС узла</span><span class="sxs-lookup"><span data-stu-id="e8ac9-163">Host OS</span></span> |
| <span data-ttu-id="e8ac9-164">context.device.roleInstance</span><span class="sxs-lookup"><span data-stu-id="e8ac9-164">context.device.roleInstance</span></span> |<span data-ttu-id="e8ac9-165">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-165">string</span></span> |<span data-ttu-id="e8ac9-166">Идентификатор узла сервера</span><span class="sxs-lookup"><span data-stu-id="e8ac9-166">ID of server host</span></span> |
| <span data-ttu-id="e8ac9-167">context.device.roleName</span><span class="sxs-lookup"><span data-stu-id="e8ac9-167">context.device.roleName</span></span> |<span data-ttu-id="e8ac9-168">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-168">string</span></span> | |
| <span data-ttu-id="e8ac9-169">context.device.type</span><span class="sxs-lookup"><span data-stu-id="e8ac9-169">context.device.type</span></span> |<span data-ttu-id="e8ac9-170">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-170">string</span></span> |<span data-ttu-id="e8ac9-171">ПК, браузер…</span><span class="sxs-lookup"><span data-stu-id="e8ac9-171">PC, Browser, ...</span></span> |
| <span data-ttu-id="e8ac9-172">context.location</span><span class="sxs-lookup"><span data-stu-id="e8ac9-172">context.location</span></span> |<span data-ttu-id="e8ac9-173">object</span><span class="sxs-lookup"><span data-stu-id="e8ac9-173">object</span></span> |<span data-ttu-id="e8ac9-174">На основе значения clientip.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-174">Derived from clientip.</span></span> |
| <span data-ttu-id="e8ac9-175">context.location.city</span><span class="sxs-lookup"><span data-stu-id="e8ac9-175">context.location.city</span></span> |<span data-ttu-id="e8ac9-176">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-176">string</span></span> |<span data-ttu-id="e8ac9-177">На основе значения clientip (если известно)</span><span class="sxs-lookup"><span data-stu-id="e8ac9-177">Derived from clientip, if known</span></span> |
| <span data-ttu-id="e8ac9-178">context.location.clientip</span><span class="sxs-lookup"><span data-stu-id="e8ac9-178">context.location.clientip</span></span> |<span data-ttu-id="e8ac9-179">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-179">string</span></span> |<span data-ttu-id="e8ac9-180">Последний восьмиугольник анонимизирован и имеет значение 0.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-180">Last octagon is anonymized to 0.</span></span> |
| <span data-ttu-id="e8ac9-181">context.location.continent</span><span class="sxs-lookup"><span data-stu-id="e8ac9-181">context.location.continent</span></span> |<span data-ttu-id="e8ac9-182">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-182">string</span></span> | |
| <span data-ttu-id="e8ac9-183">context.location.country</span><span class="sxs-lookup"><span data-stu-id="e8ac9-183">context.location.country</span></span> |<span data-ttu-id="e8ac9-184">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-184">string</span></span> | |
| <span data-ttu-id="e8ac9-185">context.location.province</span><span class="sxs-lookup"><span data-stu-id="e8ac9-185">context.location.province</span></span> |<span data-ttu-id="e8ac9-186">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-186">string</span></span> |<span data-ttu-id="e8ac9-187">Страна или область</span><span class="sxs-lookup"><span data-stu-id="e8ac9-187">State or province</span></span> |
| <span data-ttu-id="e8ac9-188">context.operation.id</span><span class="sxs-lookup"><span data-stu-id="e8ac9-188">context.operation.id</span></span> |<span data-ttu-id="e8ac9-189">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-189">string</span></span> |<span data-ttu-id="e8ac9-190">Элементы с одинаковым идентификатором операций отображаются на портале как связанные элементы.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-190">Items that have the same operation id are shown as Related Items in the portal.</span></span> <span data-ttu-id="e8ac9-191">Как правило, это идентификатор запроса.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-191">Usually the request id.</span></span> |
| <span data-ttu-id="e8ac9-192">context.operation.name</span><span class="sxs-lookup"><span data-stu-id="e8ac9-192">context.operation.name</span></span> |<span data-ttu-id="e8ac9-193">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-193">string</span></span> |<span data-ttu-id="e8ac9-194">URL-адрес или имя запроса</span><span class="sxs-lookup"><span data-stu-id="e8ac9-194">url or request name</span></span> |
| <span data-ttu-id="e8ac9-195">context.operation.parentId</span><span class="sxs-lookup"><span data-stu-id="e8ac9-195">context.operation.parentId</span></span> |<span data-ttu-id="e8ac9-196">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-196">string</span></span> |<span data-ttu-id="e8ac9-197">Разрешает использование вложенных связанных элементов.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-197">Allows nested related items.</span></span> |
| <span data-ttu-id="e8ac9-198">context.session.id</span><span class="sxs-lookup"><span data-stu-id="e8ac9-198">context.session.id</span></span> |<span data-ttu-id="e8ac9-199">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-199">string</span></span> |<span data-ttu-id="e8ac9-200">Идентификатор группы операций из одного источника.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-200">Id of a group of operations from the same source.</span></span> <span data-ttu-id="e8ac9-201">30-минутный период без операций указывает на завершение сеанса.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-201">A period of 30 minutes without an operation signals the end of a session.</span></span> |
| <span data-ttu-id="e8ac9-202">context.session.isFirst</span><span class="sxs-lookup"><span data-stu-id="e8ac9-202">context.session.isFirst</span></span> |<span data-ttu-id="e8ac9-203">Логическое</span><span class="sxs-lookup"><span data-stu-id="e8ac9-203">boolean</span></span> | |
| <span data-ttu-id="e8ac9-204">context.user.accountAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="e8ac9-204">context.user.accountAcquisitionDate</span></span> |<span data-ttu-id="e8ac9-205">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-205">string</span></span> | |
| <span data-ttu-id="e8ac9-206">context.user.anonAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="e8ac9-206">context.user.anonAcquisitionDate</span></span> |<span data-ttu-id="e8ac9-207">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-207">string</span></span> | |
| <span data-ttu-id="e8ac9-208">context.user.anonId</span><span class="sxs-lookup"><span data-stu-id="e8ac9-208">context.user.anonId</span></span> |<span data-ttu-id="e8ac9-209">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-209">string</span></span> | |
| <span data-ttu-id="e8ac9-210">context.user.authAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="e8ac9-210">context.user.authAcquisitionDate</span></span> |<span data-ttu-id="e8ac9-211">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-211">string</span></span> |[<span data-ttu-id="e8ac9-212">Прошедший проверку пользователь.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-212">Authenticated User</span></span>](app-insights-api-custom-events-metrics.md#authenticated-users) |
| <span data-ttu-id="e8ac9-213">context.user.isAuthenticated</span><span class="sxs-lookup"><span data-stu-id="e8ac9-213">context.user.isAuthenticated</span></span> |<span data-ttu-id="e8ac9-214">Логическое</span><span class="sxs-lookup"><span data-stu-id="e8ac9-214">boolean</span></span> | |
| <span data-ttu-id="e8ac9-215">internal.data.documentVersion</span><span class="sxs-lookup"><span data-stu-id="e8ac9-215">internal.data.documentVersion</span></span> |<span data-ttu-id="e8ac9-216">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-216">string</span></span> | |
| <span data-ttu-id="e8ac9-217">internal.data.id</span><span class="sxs-lookup"><span data-stu-id="e8ac9-217">internal.data.id</span></span> |<span data-ttu-id="e8ac9-218">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-218">string</span></span> | |

## <a name="events"></a><span data-ttu-id="e8ac9-219">События</span><span class="sxs-lookup"><span data-stu-id="e8ac9-219">Events</span></span>
<span data-ttu-id="e8ac9-220">Пользовательские события, создаваемые элементом [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="e8ac9-220">Custom events generated by [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent).</span></span>

| <span data-ttu-id="e8ac9-221">Путь</span><span class="sxs-lookup"><span data-stu-id="e8ac9-221">Path</span></span> | <span data-ttu-id="e8ac9-222">Тип</span><span class="sxs-lookup"><span data-stu-id="e8ac9-222">Type</span></span> | <span data-ttu-id="e8ac9-223">Примечания</span><span class="sxs-lookup"><span data-stu-id="e8ac9-223">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e8ac9-224">event [0] count</span><span class="sxs-lookup"><span data-stu-id="e8ac9-224">event [0] count</span></span> |<span data-ttu-id="e8ac9-225">целое число</span><span class="sxs-lookup"><span data-stu-id="e8ac9-225">integer</span></span> |<span data-ttu-id="e8ac9-226">100/(частота[выборки](app-insights-sampling.md) ).</span><span class="sxs-lookup"><span data-stu-id="e8ac9-226">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="e8ac9-227">Например, 4 = &gt; 25 %.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-227">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="e8ac9-228">event [0] name</span><span class="sxs-lookup"><span data-stu-id="e8ac9-228">event [0] name</span></span> |<span data-ttu-id="e8ac9-229">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-229">string</span></span> |<span data-ttu-id="e8ac9-230">Имя события.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-230">Event name.</span></span>  <span data-ttu-id="e8ac9-231">Максимальная длина: 250</span><span class="sxs-lookup"><span data-stu-id="e8ac9-231">Max length 250.</span></span> |
| <span data-ttu-id="e8ac9-232">event [0] url</span><span class="sxs-lookup"><span data-stu-id="e8ac9-232">event [0] url</span></span> |<span data-ttu-id="e8ac9-233">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-233">string</span></span> | |
| <span data-ttu-id="e8ac9-234">event [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="e8ac9-234">event [0] urlData.base</span></span> |<span data-ttu-id="e8ac9-235">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-235">string</span></span> | |
| <span data-ttu-id="e8ac9-236">event [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="e8ac9-236">event [0] urlData.host</span></span> |<span data-ttu-id="e8ac9-237">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-237">string</span></span> | |

## <a name="exceptions"></a><span data-ttu-id="e8ac9-238">Исключения</span><span class="sxs-lookup"><span data-stu-id="e8ac9-238">Exceptions</span></span>
<span data-ttu-id="e8ac9-239">Отправляются сведения об [исключениях](app-insights-asp-net-exceptions.md) на сервере и в браузере.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-239">Reports [exceptions](app-insights-asp-net-exceptions.md) in the server and in the browser.</span></span>

| <span data-ttu-id="e8ac9-240">Путь</span><span class="sxs-lookup"><span data-stu-id="e8ac9-240">Path</span></span> | <span data-ttu-id="e8ac9-241">Тип</span><span class="sxs-lookup"><span data-stu-id="e8ac9-241">Type</span></span> | <span data-ttu-id="e8ac9-242">Примечания</span><span class="sxs-lookup"><span data-stu-id="e8ac9-242">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e8ac9-243">basicException [0] assembly</span><span class="sxs-lookup"><span data-stu-id="e8ac9-243">basicException [0] assembly</span></span> |<span data-ttu-id="e8ac9-244">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-244">string</span></span> | |
| <span data-ttu-id="e8ac9-245">basicException [0] count</span><span class="sxs-lookup"><span data-stu-id="e8ac9-245">basicException [0] count</span></span> |<span data-ttu-id="e8ac9-246">целое число</span><span class="sxs-lookup"><span data-stu-id="e8ac9-246">integer</span></span> |<span data-ttu-id="e8ac9-247">100/(частота[выборки](app-insights-sampling.md) ).</span><span class="sxs-lookup"><span data-stu-id="e8ac9-247">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="e8ac9-248">Например, 4 = &gt; 25 %.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-248">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="e8ac9-249">basicException [0] exceptionGroup</span><span class="sxs-lookup"><span data-stu-id="e8ac9-249">basicException [0] exceptionGroup</span></span> |<span data-ttu-id="e8ac9-250">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-250">string</span></span> | |
| <span data-ttu-id="e8ac9-251">basicException [0] exceptionType</span><span class="sxs-lookup"><span data-stu-id="e8ac9-251">basicException [0] exceptionType</span></span> |<span data-ttu-id="e8ac9-252">string</span><span class="sxs-lookup"><span data-stu-id="e8ac9-252">string</span></span> | |
| <span data-ttu-id="e8ac9-253">basicException [0] failedUserCodeMethod</span><span class="sxs-lookup"><span data-stu-id="e8ac9-253">basicException [0] failedUserCodeMethod</span></span> |<span data-ttu-id="e8ac9-254">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-254">string</span></span> | |
| <span data-ttu-id="e8ac9-255">basicException [0] failedUserCodeAssembly</span><span class="sxs-lookup"><span data-stu-id="e8ac9-255">basicException [0] failedUserCodeAssembly</span></span> |<span data-ttu-id="e8ac9-256">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-256">string</span></span> | |
| <span data-ttu-id="e8ac9-257">basicException [0] handledAt</span><span class="sxs-lookup"><span data-stu-id="e8ac9-257">basicException [0] handledAt</span></span> |<span data-ttu-id="e8ac9-258">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-258">string</span></span> | |
| <span data-ttu-id="e8ac9-259">basicException [0] hasFullStack</span><span class="sxs-lookup"><span data-stu-id="e8ac9-259">basicException [0] hasFullStack</span></span> |<span data-ttu-id="e8ac9-260">Логическое</span><span class="sxs-lookup"><span data-stu-id="e8ac9-260">boolean</span></span> | |
| <span data-ttu-id="e8ac9-261">basicException [0] id</span><span class="sxs-lookup"><span data-stu-id="e8ac9-261">basicException [0] id</span></span> |<span data-ttu-id="e8ac9-262">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-262">string</span></span> | |
| <span data-ttu-id="e8ac9-263">basicException [0] method</span><span class="sxs-lookup"><span data-stu-id="e8ac9-263">basicException [0] method</span></span> |<span data-ttu-id="e8ac9-264">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-264">string</span></span> | |
| <span data-ttu-id="e8ac9-265">basicException [0] message</span><span class="sxs-lookup"><span data-stu-id="e8ac9-265">basicException [0] message</span></span> |<span data-ttu-id="e8ac9-266">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-266">string</span></span> |<span data-ttu-id="e8ac9-267">Сообщение об исключении.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-267">Exception message.</span></span> <span data-ttu-id="e8ac9-268">Максимальная длина: 10 000</span><span class="sxs-lookup"><span data-stu-id="e8ac9-268">Max length 10k.</span></span> |
| <span data-ttu-id="e8ac9-269">basicException [0] outerExceptionMessage</span><span class="sxs-lookup"><span data-stu-id="e8ac9-269">basicException [0] outerExceptionMessage</span></span> |<span data-ttu-id="e8ac9-270">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-270">string</span></span> | |
| <span data-ttu-id="e8ac9-271">basicException [0] outerExceptionThrownAtAssembly</span><span class="sxs-lookup"><span data-stu-id="e8ac9-271">basicException [0] outerExceptionThrownAtAssembly</span></span> |<span data-ttu-id="e8ac9-272">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-272">string</span></span> | |
| <span data-ttu-id="e8ac9-273">basicException [0] outerExceptionThrownAtMethod</span><span class="sxs-lookup"><span data-stu-id="e8ac9-273">basicException [0] outerExceptionThrownAtMethod</span></span> |<span data-ttu-id="e8ac9-274">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-274">string</span></span> | |
| <span data-ttu-id="e8ac9-275">basicException [0] outerExceptionType</span><span class="sxs-lookup"><span data-stu-id="e8ac9-275">basicException [0] outerExceptionType</span></span> |<span data-ttu-id="e8ac9-276">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-276">string</span></span> | |
| <span data-ttu-id="e8ac9-277">basicException [0] outerId</span><span class="sxs-lookup"><span data-stu-id="e8ac9-277">basicException [0] outerId</span></span> |<span data-ttu-id="e8ac9-278">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-278">string</span></span> | |
| <span data-ttu-id="e8ac9-279">basicException [0] parsedStack [0] assembly</span><span class="sxs-lookup"><span data-stu-id="e8ac9-279">basicException [0] parsedStack [0] assembly</span></span> |<span data-ttu-id="e8ac9-280">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-280">string</span></span> | |
| <span data-ttu-id="e8ac9-281">basicException [0] parsedStack [0] fileName</span><span class="sxs-lookup"><span data-stu-id="e8ac9-281">basicException [0] parsedStack [0] fileName</span></span> |<span data-ttu-id="e8ac9-282">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-282">string</span></span> | |
| <span data-ttu-id="e8ac9-283">basicException [0] parsedStack [0] level</span><span class="sxs-lookup"><span data-stu-id="e8ac9-283">basicException [0] parsedStack [0] level</span></span> |<span data-ttu-id="e8ac9-284">целое число</span><span class="sxs-lookup"><span data-stu-id="e8ac9-284">integer</span></span> | |
| <span data-ttu-id="e8ac9-285">basicException [0] parsedStack [0] line</span><span class="sxs-lookup"><span data-stu-id="e8ac9-285">basicException [0] parsedStack [0] line</span></span> |<span data-ttu-id="e8ac9-286">целое число</span><span class="sxs-lookup"><span data-stu-id="e8ac9-286">integer</span></span> | |
| <span data-ttu-id="e8ac9-287">basicException [0] parsedStack [0] method</span><span class="sxs-lookup"><span data-stu-id="e8ac9-287">basicException [0] parsedStack [0] method</span></span> |<span data-ttu-id="e8ac9-288">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-288">string</span></span> | |
| <span data-ttu-id="e8ac9-289">basicException [0] stack</span><span class="sxs-lookup"><span data-stu-id="e8ac9-289">basicException [0] stack</span></span> |<span data-ttu-id="e8ac9-290">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-290">string</span></span> |<span data-ttu-id="e8ac9-291">Максимальная длина: 10 000</span><span class="sxs-lookup"><span data-stu-id="e8ac9-291">Max length 10k</span></span> |
| <span data-ttu-id="e8ac9-292">basicException [0] typeName</span><span class="sxs-lookup"><span data-stu-id="e8ac9-292">basicException [0] typeName</span></span> |<span data-ttu-id="e8ac9-293">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-293">string</span></span> | |

## <a name="trace-messages"></a><span data-ttu-id="e8ac9-294">Сообщения трассировки</span><span class="sxs-lookup"><span data-stu-id="e8ac9-294">Trace Messages</span></span>
<span data-ttu-id="e8ac9-295">Отправитель: [TrackTrace](app-insights-api-custom-events-metrics.md#tracktrace) и [адаптеры ведения журналов](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="e8ac9-295">Sent by [TrackTrace](app-insights-api-custom-events-metrics.md#tracktrace), and by the [logging adapters](app-insights-asp-net-trace-logs.md).</span></span>

| <span data-ttu-id="e8ac9-296">Путь</span><span class="sxs-lookup"><span data-stu-id="e8ac9-296">Path</span></span> | <span data-ttu-id="e8ac9-297">Тип</span><span class="sxs-lookup"><span data-stu-id="e8ac9-297">Type</span></span> | <span data-ttu-id="e8ac9-298">Примечания</span><span class="sxs-lookup"><span data-stu-id="e8ac9-298">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e8ac9-299">message [0] loggerName</span><span class="sxs-lookup"><span data-stu-id="e8ac9-299">message [0] loggerName</span></span> |<span data-ttu-id="e8ac9-300">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-300">string</span></span> | |
| <span data-ttu-id="e8ac9-301">message [0] parameters</span><span class="sxs-lookup"><span data-stu-id="e8ac9-301">message [0] parameters</span></span> |<span data-ttu-id="e8ac9-302">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-302">string</span></span> | |
| <span data-ttu-id="e8ac9-303">message [0] raw</span><span class="sxs-lookup"><span data-stu-id="e8ac9-303">message [0] raw</span></span> |<span data-ttu-id="e8ac9-304">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-304">string</span></span> |<span data-ttu-id="e8ac9-305">Сообщение журнала, максимальная длина — 10 тысяч символов.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-305">The log message, max length 10k.</span></span> |
| <span data-ttu-id="e8ac9-306">message [0] severityLevel</span><span class="sxs-lookup"><span data-stu-id="e8ac9-306">message [0] severityLevel</span></span> |<span data-ttu-id="e8ac9-307">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-307">string</span></span> | |

## <a name="remote-dependency"></a><span data-ttu-id="e8ac9-308">Удаленная зависимость</span><span class="sxs-lookup"><span data-stu-id="e8ac9-308">Remote dependency</span></span>
<span data-ttu-id="e8ac9-309">Отправитель: TrackDependency.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-309">Sent by TrackDependency.</span></span> <span data-ttu-id="e8ac9-310">Используется для создания отчетов о производительности и использовании [вызовов к зависимостям](app-insights-asp-net-dependencies.md) на сервере, а также вызовов AJAX в браузере.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-310">Used to report performance and usage of [calls to dependencies](app-insights-asp-net-dependencies.md) in the server, and AJAX calls in the browser.</span></span>

| <span data-ttu-id="e8ac9-311">Путь</span><span class="sxs-lookup"><span data-stu-id="e8ac9-311">Path</span></span> | <span data-ttu-id="e8ac9-312">Тип</span><span class="sxs-lookup"><span data-stu-id="e8ac9-312">Type</span></span> | <span data-ttu-id="e8ac9-313">Примечания</span><span class="sxs-lookup"><span data-stu-id="e8ac9-313">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e8ac9-314">remoteDependency [0] async</span><span class="sxs-lookup"><span data-stu-id="e8ac9-314">remoteDependency [0] async</span></span> |<span data-ttu-id="e8ac9-315">Логическое</span><span class="sxs-lookup"><span data-stu-id="e8ac9-315">boolean</span></span> | |
| <span data-ttu-id="e8ac9-316">remoteDependency [0] baseName</span><span class="sxs-lookup"><span data-stu-id="e8ac9-316">remoteDependency [0] baseName</span></span> |<span data-ttu-id="e8ac9-317">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-317">string</span></span> | |
| <span data-ttu-id="e8ac9-318">remoteDependency [0] commandName</span><span class="sxs-lookup"><span data-stu-id="e8ac9-318">remoteDependency [0] commandName</span></span> |<span data-ttu-id="e8ac9-319">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-319">string</span></span> |<span data-ttu-id="e8ac9-320">Например, home/index</span><span class="sxs-lookup"><span data-stu-id="e8ac9-320">For example "home/index"</span></span> |
| <span data-ttu-id="e8ac9-321">remoteDependency [0] count</span><span class="sxs-lookup"><span data-stu-id="e8ac9-321">remoteDependency [0] count</span></span> |<span data-ttu-id="e8ac9-322">целое число</span><span class="sxs-lookup"><span data-stu-id="e8ac9-322">integer</span></span> |<span data-ttu-id="e8ac9-323">100/(частота[выборки](app-insights-sampling.md) ).</span><span class="sxs-lookup"><span data-stu-id="e8ac9-323">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="e8ac9-324">Например, 4 = &gt; 25 %.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-324">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="e8ac9-325">remoteDependency [0] dependencyTypeName</span><span class="sxs-lookup"><span data-stu-id="e8ac9-325">remoteDependency [0] dependencyTypeName</span></span> |<span data-ttu-id="e8ac9-326">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-326">string</span></span> |<span data-ttu-id="e8ac9-327">HTTP, SQL, …</span><span class="sxs-lookup"><span data-stu-id="e8ac9-327">HTTP, SQL, ...</span></span> |
| <span data-ttu-id="e8ac9-328">remoteDependency [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="e8ac9-328">remoteDependency [0] durationMetric.value</span></span> |<span data-ttu-id="e8ac9-329">number</span><span class="sxs-lookup"><span data-stu-id="e8ac9-329">number</span></span> |<span data-ttu-id="e8ac9-330">Время от вызова до завершения отклика зависимостью.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-330">Time from call to completion of response by dependency</span></span> |
| <span data-ttu-id="e8ac9-331">remoteDependency [0] id</span><span class="sxs-lookup"><span data-stu-id="e8ac9-331">remoteDependency [0] id</span></span> |<span data-ttu-id="e8ac9-332">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-332">string</span></span> | |
| <span data-ttu-id="e8ac9-333">remoteDependency [0] name</span><span class="sxs-lookup"><span data-stu-id="e8ac9-333">remoteDependency [0] name</span></span> |<span data-ttu-id="e8ac9-334">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-334">string</span></span> |<span data-ttu-id="e8ac9-335">URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-335">Url.</span></span> <span data-ttu-id="e8ac9-336">Максимальная длина: 250</span><span class="sxs-lookup"><span data-stu-id="e8ac9-336">Max length 250.</span></span> |
| <span data-ttu-id="e8ac9-337">remoteDependency [0] resultCode</span><span class="sxs-lookup"><span data-stu-id="e8ac9-337">remoteDependency [0] resultCode</span></span> |<span data-ttu-id="e8ac9-338">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-338">string</span></span> |<span data-ttu-id="e8ac9-339">Из зависимости HTTP.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-339">from HTTP dependency</span></span> |
| <span data-ttu-id="e8ac9-340">remoteDependency [0] success</span><span class="sxs-lookup"><span data-stu-id="e8ac9-340">remoteDependency [0] success</span></span> |<span data-ttu-id="e8ac9-341">Логическое</span><span class="sxs-lookup"><span data-stu-id="e8ac9-341">boolean</span></span> | |
| <span data-ttu-id="e8ac9-342">remoteDependency [0] type</span><span class="sxs-lookup"><span data-stu-id="e8ac9-342">remoteDependency [0] type</span></span> |<span data-ttu-id="e8ac9-343">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-343">string</span></span> |<span data-ttu-id="e8ac9-344">HTTP, SQL, …</span><span class="sxs-lookup"><span data-stu-id="e8ac9-344">Http, Sql,...</span></span> |
| <span data-ttu-id="e8ac9-345">remoteDependency [0] url</span><span class="sxs-lookup"><span data-stu-id="e8ac9-345">remoteDependency [0] url</span></span> |<span data-ttu-id="e8ac9-346">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-346">string</span></span> |<span data-ttu-id="e8ac9-347">Максимальная длина: 2000</span><span class="sxs-lookup"><span data-stu-id="e8ac9-347">Max length 2000</span></span> |
| <span data-ttu-id="e8ac9-348">remoteDependency [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="e8ac9-348">remoteDependency [0] urlData.base</span></span> |<span data-ttu-id="e8ac9-349">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-349">string</span></span> |<span data-ttu-id="e8ac9-350">Максимальная длина: 2000</span><span class="sxs-lookup"><span data-stu-id="e8ac9-350">Max length 2000</span></span> |
| <span data-ttu-id="e8ac9-351">remoteDependency [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="e8ac9-351">remoteDependency [0] urlData.hashTag</span></span> |<span data-ttu-id="e8ac9-352">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-352">string</span></span> | |
| <span data-ttu-id="e8ac9-353">remoteDependency [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="e8ac9-353">remoteDependency [0] urlData.host</span></span> |<span data-ttu-id="e8ac9-354">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-354">string</span></span> |<span data-ttu-id="e8ac9-355">Максимальная длина: 200</span><span class="sxs-lookup"><span data-stu-id="e8ac9-355">Max length 200</span></span> |

## <a name="requests"></a><span data-ttu-id="e8ac9-356">Requests (Запросы)</span><span class="sxs-lookup"><span data-stu-id="e8ac9-356">Requests</span></span>
<span data-ttu-id="e8ac9-357">Отправитель: [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest).</span><span class="sxs-lookup"><span data-stu-id="e8ac9-357">Sent by [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest).</span></span> <span data-ttu-id="e8ac9-358">Используется стандартными модулями для создания отчетов о времени отклика сервера (измеряется на сервере).</span><span class="sxs-lookup"><span data-stu-id="e8ac9-358">The standard modules use this to reports server response time, measured at the server.</span></span>

| <span data-ttu-id="e8ac9-359">Путь</span><span class="sxs-lookup"><span data-stu-id="e8ac9-359">Path</span></span> | <span data-ttu-id="e8ac9-360">Тип</span><span class="sxs-lookup"><span data-stu-id="e8ac9-360">Type</span></span> | <span data-ttu-id="e8ac9-361">Примечания</span><span class="sxs-lookup"><span data-stu-id="e8ac9-361">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e8ac9-362">request [0] count</span><span class="sxs-lookup"><span data-stu-id="e8ac9-362">request [0] count</span></span> |<span data-ttu-id="e8ac9-363">целое число</span><span class="sxs-lookup"><span data-stu-id="e8ac9-363">integer</span></span> |<span data-ttu-id="e8ac9-364">100/(частота[выборки](app-insights-sampling.md) ).</span><span class="sxs-lookup"><span data-stu-id="e8ac9-364">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="e8ac9-365">Например: 4 =&gt; 25 %.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-365">For example: 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="e8ac9-366">request [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="e8ac9-366">request [0] durationMetric.value</span></span> |<span data-ttu-id="e8ac9-367">number</span><span class="sxs-lookup"><span data-stu-id="e8ac9-367">number</span></span> |<span data-ttu-id="e8ac9-368">Время от поступления запроса до отклика.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-368">Time from request arriving to response.</span></span> <span data-ttu-id="e8ac9-369">1e7 = 1 с.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-369">1e7 == 1s</span></span> |
| <span data-ttu-id="e8ac9-370">request [0] id</span><span class="sxs-lookup"><span data-stu-id="e8ac9-370">request [0] id</span></span> |<span data-ttu-id="e8ac9-371">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-371">string</span></span> |<span data-ttu-id="e8ac9-372">Идентификатор операции</span><span class="sxs-lookup"><span data-stu-id="e8ac9-372">Operation id</span></span> |
| <span data-ttu-id="e8ac9-373">request [0] name</span><span class="sxs-lookup"><span data-stu-id="e8ac9-373">request [0] name</span></span> |<span data-ttu-id="e8ac9-374">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-374">string</span></span> |<span data-ttu-id="e8ac9-375">GET или POST + базовый URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-375">GET/POST + url base.</span></span>  <span data-ttu-id="e8ac9-376">Максимальная длина: 250</span><span class="sxs-lookup"><span data-stu-id="e8ac9-376">Max length 250</span></span> |
| <span data-ttu-id="e8ac9-377">request [0] responseCode</span><span class="sxs-lookup"><span data-stu-id="e8ac9-377">request [0] responseCode</span></span> |<span data-ttu-id="e8ac9-378">целое число</span><span class="sxs-lookup"><span data-stu-id="e8ac9-378">integer</span></span> |<span data-ttu-id="e8ac9-379">HTTP-отклик, отправленный клиенту.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-379">HTTP response sent to client</span></span> |
| <span data-ttu-id="e8ac9-380">request [0] success</span><span class="sxs-lookup"><span data-stu-id="e8ac9-380">request [0] success</span></span> |<span data-ttu-id="e8ac9-381">Логическое</span><span class="sxs-lookup"><span data-stu-id="e8ac9-381">boolean</span></span> |<span data-ttu-id="e8ac9-382">Значение по умолчанию == (responseCode &lt; 400)</span><span class="sxs-lookup"><span data-stu-id="e8ac9-382">Default == (responseCode &lt; 400)</span></span> |
| <span data-ttu-id="e8ac9-383">request [0] url</span><span class="sxs-lookup"><span data-stu-id="e8ac9-383">request [0] url</span></span> |<span data-ttu-id="e8ac9-384">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-384">string</span></span> |<span data-ttu-id="e8ac9-385">Не включая узел.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-385">Not including host</span></span> |
| <span data-ttu-id="e8ac9-386">request [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="e8ac9-386">request [0] urlData.base</span></span> |<span data-ttu-id="e8ac9-387">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-387">string</span></span> | |
| <span data-ttu-id="e8ac9-388">request [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="e8ac9-388">request [0] urlData.hashTag</span></span> |<span data-ttu-id="e8ac9-389">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-389">string</span></span> | |
| <span data-ttu-id="e8ac9-390">request [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="e8ac9-390">request [0] urlData.host</span></span> |<span data-ttu-id="e8ac9-391">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-391">string</span></span> | |

## <a name="page-view-performance"></a><span data-ttu-id="e8ac9-392">Производительность просмотра страницы</span><span class="sxs-lookup"><span data-stu-id="e8ac9-392">Page View Performance</span></span>
<span data-ttu-id="e8ac9-393">Отправитель: браузер.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-393">Sent by the browser.</span></span> <span data-ttu-id="e8ac9-394">Измеряет время обработки страницы — с момента инициации пользователем запроса до полного отображения страницы (за исключением асинхронных вызовов AJAX).</span><span class="sxs-lookup"><span data-stu-id="e8ac9-394">Measures the time to process a page, from user initiating the request to display complete (excluding async AJAX calls).</span></span>

<span data-ttu-id="e8ac9-395">Контекстные значения показывают версию клиентской ОС и версию браузера.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-395">Context values show client OS and browser version.</span></span>

| <span data-ttu-id="e8ac9-396">Путь</span><span class="sxs-lookup"><span data-stu-id="e8ac9-396">Path</span></span> | <span data-ttu-id="e8ac9-397">Тип</span><span class="sxs-lookup"><span data-stu-id="e8ac9-397">Type</span></span> | <span data-ttu-id="e8ac9-398">Примечания</span><span class="sxs-lookup"><span data-stu-id="e8ac9-398">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e8ac9-399">clientPerformance [0] clientProcess.value</span><span class="sxs-lookup"><span data-stu-id="e8ac9-399">clientPerformance [0] clientProcess.value</span></span> |<span data-ttu-id="e8ac9-400">целое число</span><span class="sxs-lookup"><span data-stu-id="e8ac9-400">integer</span></span> |<span data-ttu-id="e8ac9-401">Время от завершения получения HTML до отображения страницы.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-401">Time from end of receiving the HTML to displaying the page.</span></span> |
| <span data-ttu-id="e8ac9-402">clientPerformance [0] name</span><span class="sxs-lookup"><span data-stu-id="e8ac9-402">clientPerformance [0] name</span></span> |<span data-ttu-id="e8ac9-403">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-403">string</span></span> | |
| <span data-ttu-id="e8ac9-404">clientPerformance [0] networkConnection.value</span><span class="sxs-lookup"><span data-stu-id="e8ac9-404">clientPerformance [0] networkConnection.value</span></span> |<span data-ttu-id="e8ac9-405">целое число</span><span class="sxs-lookup"><span data-stu-id="e8ac9-405">integer</span></span> |<span data-ttu-id="e8ac9-406">Время, необходимое для установки подключения к сети.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-406">Time taken to establish a network connection.</span></span> |
| <span data-ttu-id="e8ac9-407">clientPerformance [0] receiveRequest.value</span><span class="sxs-lookup"><span data-stu-id="e8ac9-407">clientPerformance [0] receiveRequest.value</span></span> |<span data-ttu-id="e8ac9-408">целое число</span><span class="sxs-lookup"><span data-stu-id="e8ac9-408">integer</span></span> |<span data-ttu-id="e8ac9-409">Время от завершения отправки запроса до получения HTML в отклике.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-409">Time from end of sending the request to receiving the HTML in reply.</span></span> |
| <span data-ttu-id="e8ac9-410">clientPerformance [0] sendRequest.value</span><span class="sxs-lookup"><span data-stu-id="e8ac9-410">clientPerformance [0] sendRequest.value</span></span> |<span data-ttu-id="e8ac9-411">целое число</span><span class="sxs-lookup"><span data-stu-id="e8ac9-411">integer</span></span> |<span data-ttu-id="e8ac9-412">Время на отправку HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-412">Time from taken to send the HTTP request.</span></span> |
| <span data-ttu-id="e8ac9-413">clientPerformance [0] total.value</span><span class="sxs-lookup"><span data-stu-id="e8ac9-413">clientPerformance [0] total.value</span></span> |<span data-ttu-id="e8ac9-414">целое число</span><span class="sxs-lookup"><span data-stu-id="e8ac9-414">integer</span></span> |<span data-ttu-id="e8ac9-415">Время от запуска отправки запроса до отображения страницы.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-415">Time from starting to send the request to displaying the page.</span></span> |
| <span data-ttu-id="e8ac9-416">clientPerformance [0] url</span><span class="sxs-lookup"><span data-stu-id="e8ac9-416">clientPerformance [0] url</span></span> |<span data-ttu-id="e8ac9-417">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-417">string</span></span> |<span data-ttu-id="e8ac9-418">URL-адрес запроса.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-418">URL of this request</span></span> |
| <span data-ttu-id="e8ac9-419">clientPerformance [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="e8ac9-419">clientPerformance [0] urlData.base</span></span> |<span data-ttu-id="e8ac9-420">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-420">string</span></span> | |
| <span data-ttu-id="e8ac9-421">clientPerformance [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="e8ac9-421">clientPerformance [0] urlData.hashTag</span></span> |<span data-ttu-id="e8ac9-422">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-422">string</span></span> | |
| <span data-ttu-id="e8ac9-423">clientPerformance [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="e8ac9-423">clientPerformance [0] urlData.host</span></span> |<span data-ttu-id="e8ac9-424">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-424">string</span></span> | |
| <span data-ttu-id="e8ac9-425">clientPerformance [0] urlData.protocol</span><span class="sxs-lookup"><span data-stu-id="e8ac9-425">clientPerformance [0] urlData.protocol</span></span> |<span data-ttu-id="e8ac9-426">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-426">string</span></span> | |

## <a name="page-views"></a><span data-ttu-id="e8ac9-427">Просмотры страницы</span><span class="sxs-lookup"><span data-stu-id="e8ac9-427">Page Views</span></span>
<span data-ttu-id="e8ac9-428">Отправитель: trackPageView() или [stopTrackPage](app-insights-api-custom-events-metrics.md#page-views)</span><span class="sxs-lookup"><span data-stu-id="e8ac9-428">Sent by trackPageView() or [stopTrackPage](app-insights-api-custom-events-metrics.md#page-views)</span></span>

| <span data-ttu-id="e8ac9-429">Путь</span><span class="sxs-lookup"><span data-stu-id="e8ac9-429">Path</span></span> | <span data-ttu-id="e8ac9-430">Тип</span><span class="sxs-lookup"><span data-stu-id="e8ac9-430">Type</span></span> | <span data-ttu-id="e8ac9-431">Примечания</span><span class="sxs-lookup"><span data-stu-id="e8ac9-431">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e8ac9-432">view [0] count</span><span class="sxs-lookup"><span data-stu-id="e8ac9-432">view [0] count</span></span> |<span data-ttu-id="e8ac9-433">целое число</span><span class="sxs-lookup"><span data-stu-id="e8ac9-433">integer</span></span> |<span data-ttu-id="e8ac9-434">100/(частота[выборки](app-insights-sampling.md) ).</span><span class="sxs-lookup"><span data-stu-id="e8ac9-434">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="e8ac9-435">Например, 4 = &gt; 25 %.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-435">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="e8ac9-436">view [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="e8ac9-436">view [0] durationMetric.value</span></span> |<span data-ttu-id="e8ac9-437">целое число</span><span class="sxs-lookup"><span data-stu-id="e8ac9-437">integer</span></span> |<span data-ttu-id="e8ac9-438">При необходимости значение можно указать в методе trackPageView() или с помощью метода start/stopTrackPage().</span><span class="sxs-lookup"><span data-stu-id="e8ac9-438">Value optionally set in trackPageView() or by startTrackPage() - stopTrackPage().</span></span> <span data-ttu-id="e8ac9-439">Не совпадает со значениями clientPerformance.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-439">Not the same as clientPerformance values.</span></span> |
| <span data-ttu-id="e8ac9-440">view [0] name</span><span class="sxs-lookup"><span data-stu-id="e8ac9-440">view [0] name</span></span> |<span data-ttu-id="e8ac9-441">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-441">string</span></span> |<span data-ttu-id="e8ac9-442">Заголовок страницы.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-442">Page title.</span></span>  <span data-ttu-id="e8ac9-443">Максимальная длина: 250</span><span class="sxs-lookup"><span data-stu-id="e8ac9-443">Max length 250</span></span> |
| <span data-ttu-id="e8ac9-444">view [0] url</span><span class="sxs-lookup"><span data-stu-id="e8ac9-444">view [0] url</span></span> |<span data-ttu-id="e8ac9-445">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-445">string</span></span> | |
| <span data-ttu-id="e8ac9-446">view [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="e8ac9-446">view [0] urlData.base</span></span> |<span data-ttu-id="e8ac9-447">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-447">string</span></span> | |
| <span data-ttu-id="e8ac9-448">view [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="e8ac9-448">view [0] urlData.hashTag</span></span> |<span data-ttu-id="e8ac9-449">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-449">string</span></span> | |
| <span data-ttu-id="e8ac9-450">view [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="e8ac9-450">view [0] urlData.host</span></span> |<span data-ttu-id="e8ac9-451">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-451">string</span></span> | |

## <a name="availability"></a><span data-ttu-id="e8ac9-452">Доступность</span><span class="sxs-lookup"><span data-stu-id="e8ac9-452">Availability</span></span>
<span data-ttu-id="e8ac9-453">Это свойство создает отчеты о [веб-тестах на доступность](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="e8ac9-453">Reports [availability web tests](app-insights-monitor-web-app-availability.md).</span></span>

| <span data-ttu-id="e8ac9-454">Путь</span><span class="sxs-lookup"><span data-stu-id="e8ac9-454">Path</span></span> | <span data-ttu-id="e8ac9-455">Тип</span><span class="sxs-lookup"><span data-stu-id="e8ac9-455">Type</span></span> | <span data-ttu-id="e8ac9-456">Примечания</span><span class="sxs-lookup"><span data-stu-id="e8ac9-456">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e8ac9-457">availability [0] availabilityMetric.name</span><span class="sxs-lookup"><span data-stu-id="e8ac9-457">availability [0] availabilityMetric.name</span></span> |<span data-ttu-id="e8ac9-458">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-458">string</span></span> |<span data-ttu-id="e8ac9-459">Доступность</span><span class="sxs-lookup"><span data-stu-id="e8ac9-459">availability</span></span> |
| <span data-ttu-id="e8ac9-460">availability [0] availabilityMetric.value</span><span class="sxs-lookup"><span data-stu-id="e8ac9-460">availability [0] availabilityMetric.value</span></span> |<span data-ttu-id="e8ac9-461">number</span><span class="sxs-lookup"><span data-stu-id="e8ac9-461">number</span></span> |<span data-ttu-id="e8ac9-462">1,0 или 0,0.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-462">1.0 or 0.0</span></span> |
| <span data-ttu-id="e8ac9-463">availability [0] count</span><span class="sxs-lookup"><span data-stu-id="e8ac9-463">availability [0] count</span></span> |<span data-ttu-id="e8ac9-464">целое число</span><span class="sxs-lookup"><span data-stu-id="e8ac9-464">integer</span></span> |<span data-ttu-id="e8ac9-465">100/(частота[выборки](app-insights-sampling.md) ).</span><span class="sxs-lookup"><span data-stu-id="e8ac9-465">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="e8ac9-466">Например, 4 = &gt; 25 %.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-466">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="e8ac9-467">availability [0] dataSizeMetric.name</span><span class="sxs-lookup"><span data-stu-id="e8ac9-467">availability [0] dataSizeMetric.name</span></span> |<span data-ttu-id="e8ac9-468">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-468">string</span></span> | |
| <span data-ttu-id="e8ac9-469">availability [0] dataSizeMetric.value</span><span class="sxs-lookup"><span data-stu-id="e8ac9-469">availability [0] dataSizeMetric.value</span></span> |<span data-ttu-id="e8ac9-470">целое число</span><span class="sxs-lookup"><span data-stu-id="e8ac9-470">integer</span></span> | |
| <span data-ttu-id="e8ac9-471">availability [0] durationMetric.name</span><span class="sxs-lookup"><span data-stu-id="e8ac9-471">availability [0] durationMetric.name</span></span> |<span data-ttu-id="e8ac9-472">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-472">string</span></span> | |
| <span data-ttu-id="e8ac9-473">availability [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="e8ac9-473">availability [0] durationMetric.value</span></span> |<span data-ttu-id="e8ac9-474">number</span><span class="sxs-lookup"><span data-stu-id="e8ac9-474">number</span></span> |<span data-ttu-id="e8ac9-475">Продолжительность теста.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-475">Duration of test.</span></span> <span data-ttu-id="e8ac9-476">1e7 = 1 с.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-476">1e7==1s</span></span> |
| <span data-ttu-id="e8ac9-477">availability [0] message</span><span class="sxs-lookup"><span data-stu-id="e8ac9-477">availability [0] message</span></span> |<span data-ttu-id="e8ac9-478">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-478">string</span></span> |<span data-ttu-id="e8ac9-479">Диагностика сбоя.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-479">Failure diagnostic</span></span> |
| <span data-ttu-id="e8ac9-480">availability [0] result</span><span class="sxs-lookup"><span data-stu-id="e8ac9-480">availability [0] result</span></span> |<span data-ttu-id="e8ac9-481">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-481">string</span></span> |<span data-ttu-id="e8ac9-482">Успех или сбой.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-482">Pass/Fail</span></span> |
| <span data-ttu-id="e8ac9-483">availability [0] runLocation</span><span class="sxs-lookup"><span data-stu-id="e8ac9-483">availability [0] runLocation</span></span> |<span data-ttu-id="e8ac9-484">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-484">string</span></span> |<span data-ttu-id="e8ac9-485">Географический объект-источник HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-485">Geo source of http req</span></span> |
| <span data-ttu-id="e8ac9-486">availability [0] testName</span><span class="sxs-lookup"><span data-stu-id="e8ac9-486">availability [0] testName</span></span> |<span data-ttu-id="e8ac9-487">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-487">string</span></span> | |
| <span data-ttu-id="e8ac9-488">availability [0] testRunId</span><span class="sxs-lookup"><span data-stu-id="e8ac9-488">availability [0] testRunId</span></span> |<span data-ttu-id="e8ac9-489">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-489">string</span></span> | |
| <span data-ttu-id="e8ac9-490">availability [0] testTimestamp</span><span class="sxs-lookup"><span data-stu-id="e8ac9-490">availability [0] testTimestamp</span></span> |<span data-ttu-id="e8ac9-491">строка</span><span class="sxs-lookup"><span data-stu-id="e8ac9-491">string</span></span> | |

## <a name="metrics"></a><span data-ttu-id="e8ac9-492">Метрики</span><span class="sxs-lookup"><span data-stu-id="e8ac9-492">Metrics</span></span>
<span data-ttu-id="e8ac9-493">Создатель: TrackMetric().</span><span class="sxs-lookup"><span data-stu-id="e8ac9-493">Generated by TrackMetric().</span></span>

<span data-ttu-id="e8ac9-494">Значение метрики можно найти в context.custom.metrics[0].</span><span class="sxs-lookup"><span data-stu-id="e8ac9-494">The metric value is found in context.custom.metrics[0]</span></span>

<span data-ttu-id="e8ac9-495">Например:</span><span class="sxs-lookup"><span data-stu-id="e8ac9-495">For example:</span></span>

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

## <a name="about-metric-values"></a><span data-ttu-id="e8ac9-496">О значениях метрик</span><span class="sxs-lookup"><span data-stu-id="e8ac9-496">About metric values</span></span>
<span data-ttu-id="e8ac9-497">Значения метрик (как в отчетах, так и в других элементах) сообщаются в рамках стандартной структуры объекта.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-497">Metric values, both in metric reports and elsewhere, are reported with a standard object structure.</span></span> <span data-ttu-id="e8ac9-498">Например:</span><span class="sxs-lookup"><span data-stu-id="e8ac9-498">For example:</span></span>

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

<span data-ttu-id="e8ac9-499">Сейчас (хотя это может измениться в будущем) во всех значениях, включенных в отчеты стандартных модулей SDK, полезными являются только поля `name` и `value`, а также `count==1`.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-499">Currently - though this might change in the future - in all values reported from the standard SDK modules, `count==1` and only the `name` and `value` fields are useful.</span></span> <span data-ttu-id="e8ac9-500">Они будут отличаться, только если вы напишете собственный вызов TrackMetric, указав другие параметры.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-500">The only case where they would be different would be if you write your own TrackMetric calls in which you set the other parameters.</span></span>

<span data-ttu-id="e8ac9-501">Другие поля нужны для того, чтобы разрешить статистическое вычисление метрик в пакете SDK, тем самым снизив нагрузку (в виде трафика) на портал.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-501">The purpose of the other fields is to allow metrics to be aggregated in the SDK, to reduce traffic to the portal.</span></span> <span data-ttu-id="e8ac9-502">Например, перед отправкой каждого отчета с метриками вы можете получить среднее значение для нескольких последовательных показаний.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-502">For example, you could average several successive readings before sending each metric report.</span></span> <span data-ttu-id="e8ac9-503">Затем вы можете рассчитать минимальное и максимальное значение, а также стандартное отклонение и агрегированное значение (сумму или среднее), а затем указать в счетчике количество показаний, представленных в отчете.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-503">Then you would calculate the min, max, standard deviation and aggregate value (sum or average) and set count to the number of readings represented by the report.</span></span>

<span data-ttu-id="e8ac9-504">В таблицах выше мы опустили редко используемые поля count, min, max, stdDev и sampledValue.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-504">In the tables above, we have omitted the rarely-used fields count, min, max, stdDev and sampledValue.</span></span>

<span data-ttu-id="e8ac9-505">Вместо предварительного статистического вычисления метрик вы можете использовать [выборки](app-insights-sampling.md) , чтобы сократить объем данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-505">Instead of pre-aggregating metrics, you can use [sampling](app-insights-sampling.md) if you need to reduce the volume of telemetry.</span></span>

### <a name="durations"></a><span data-ttu-id="e8ac9-506">Длительность</span><span class="sxs-lookup"><span data-stu-id="e8ac9-506">Durations</span></span>
<span data-ttu-id="e8ac9-507">За исключением оговоренных случаев, показатели длительности представлены в десятых долях микросекунды, то есть 10 000 000,0 — это 1 с.</span><span class="sxs-lookup"><span data-stu-id="e8ac9-507">Except where otherwise noted, durations are represented in tenths of a microsecond, so that 10000000.0 means 1 second.</span></span>

## <a name="see-also"></a><span data-ttu-id="e8ac9-508">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="e8ac9-508">See also</span></span>
* [<span data-ttu-id="e8ac9-509">Application Insights</span><span class="sxs-lookup"><span data-stu-id="e8ac9-509">Application Insights</span></span>](app-insights-overview.md)
* [<span data-ttu-id="e8ac9-510">Непрерывный экспорт</span><span class="sxs-lookup"><span data-stu-id="e8ac9-510">Continuous Export</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="e8ac9-511">Примеры кода</span><span class="sxs-lookup"><span data-stu-id="e8ac9-511">Code samples</span></span>](app-insights-export-telemetry.md#code-samples)
