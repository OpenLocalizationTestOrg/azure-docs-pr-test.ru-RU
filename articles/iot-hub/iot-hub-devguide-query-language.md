---
title: "Общие сведения о языке запросов Центра Интернета вещей Azure | Документация Майкрософт"
description: "Руководство разработчика. Описание похожего на SQL языка запросов Центра Интернета вещей, используемого для получения сведений о двойниках устройств и заданиях из Центра Интернета вещей."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 851a9ed3-b69e-422e-8a5d-1d79f91ddf15
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/17
ms.author: elioda
ms.openlocfilehash: a7650104eda58923558892f6f0f6666d16dbce28
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="reference---iot-hub-query-language-for-device-twins-jobs-and-message-routing"></a><span data-ttu-id="cdbad-103">Справочник — язык запросов Центра Интернета вещей для двойников устройств, заданий и маршрутизации сообщений</span><span class="sxs-lookup"><span data-stu-id="cdbad-103">Reference - IoT Hub query language for device twins, jobs, and message routing</span></span>

<span data-ttu-id="cdbad-104">Центр Интернета вещей предоставляет эффективный язык запросов, похожий на SQL, для получения сведений о [двойниках устройств][lnk-twins], [заданиях][lnk-jobs] и [маршрутизации сообщений][lnk-devguide-messaging-routes].</span><span class="sxs-lookup"><span data-stu-id="cdbad-104">IoT Hub provides a powerful SQL-like language to retrieve information regarding [device twins][lnk-twins] and [jobs][lnk-jobs], and [message routing][lnk-devguide-messaging-routes].</span></span> <span data-ttu-id="cdbad-105">В этой статье представлены:</span><span class="sxs-lookup"><span data-stu-id="cdbad-105">This article presents:</span></span>

* <span data-ttu-id="cdbad-106">общие сведения об основных возможностях языка запросов Центра Интернета вещей;</span><span class="sxs-lookup"><span data-stu-id="cdbad-106">An introduction to the major features of the IoT Hub query language, and</span></span>
* <span data-ttu-id="cdbad-107">подробное описание языка.</span><span class="sxs-lookup"><span data-stu-id="cdbad-107">The detailed description of the language.</span></span>

## <a name="get-started-with-device-twin-queries"></a><span data-ttu-id="cdbad-108">Начало работы с запросами двойника устройства</span><span class="sxs-lookup"><span data-stu-id="cdbad-108">Get started with device twin queries</span></span>
<span data-ttu-id="cdbad-109">[Двойники устройств][lnk-twins] могут содержать произвольные объекты JSON в качестве тегов и свойств.</span><span class="sxs-lookup"><span data-stu-id="cdbad-109">[Device twins][lnk-twins] can contain arbitrary JSON objects as both tags and properties.</span></span> <span data-ttu-id="cdbad-110">Центр Интернета вещей позволяет выполнять запросы к двойникам устройств как к одному документу JSON, содержащему все сведения о двойниках устройств.</span><span class="sxs-lookup"><span data-stu-id="cdbad-110">IoT Hub enables you to query device twins as a single JSON document containing all device twin information.</span></span>
<span data-ttu-id="cdbad-111">Например, предположим, что двойники устройств Центра Интернета вещей имеют следующую структуру:</span><span class="sxs-lookup"><span data-stu-id="cdbad-111">Assume, for instance, that your IoT hub device twins have the following structure:</span></span>

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        "location": {
            "region": "US",
            "plant": "Redmond43"
        }
    },
    "properties": {
        "desired": {
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300
            },
            "$metadata": {
            ...
            },
            "$version": 4
        },
        "reported": {
            "connectivity": {
                "type": "cellular"
            },
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300,
                "status": "Success"
            },
            "$metadata": {
            ...
            },
            "$version": 7
        }
    }
}
```

<span data-ttu-id="cdbad-112">Центр Интернета вещей предоставляет двойники устройства как коллекцию документов с именем **devices**.</span><span class="sxs-lookup"><span data-stu-id="cdbad-112">IoT Hub exposes the device twins as a document collection called **devices**.</span></span>
<span data-ttu-id="cdbad-113">Следующий запрос получает весь набор двойников устройства:</span><span class="sxs-lookup"><span data-stu-id="cdbad-113">So the following query retrieves the whole set of device twins:</span></span>

```sql
SELECT * FROM devices
```

> [!NOTE]
> <span data-ttu-id="cdbad-114">[Пакеты SDK для Azure IoT][lnk-hub-sdks] поддерживают разбивку на страницы объемных результатов.</span><span class="sxs-lookup"><span data-stu-id="cdbad-114">[Azure IoT SDKs][lnk-hub-sdks] support paging of large results.</span></span>

<span data-ttu-id="cdbad-115">Центр Интернета вещей позволяет получить двойники устройств, отфильтрованные по произвольным условиям.</span><span class="sxs-lookup"><span data-stu-id="cdbad-115">IoT Hub allows you to retrieve device twins filtering with arbitrary conditions.</span></span> <span data-ttu-id="cdbad-116">Например,</span><span class="sxs-lookup"><span data-stu-id="cdbad-116">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
```

<span data-ttu-id="cdbad-117">извлекает двойники устройств, для тега **location.region** которых задано значение **US**.</span><span class="sxs-lookup"><span data-stu-id="cdbad-117">retrieves the device twins with the **location.region** tag set to **US**.</span></span>
<span data-ttu-id="cdbad-118">Кроме того, поддерживаются логические операторы и арифметические сравнения. Например,</span><span class="sxs-lookup"><span data-stu-id="cdbad-118">Boolean operators and arithmetic comparisons are supported as well, for example</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
    AND properties.reported.telemetryConfig.sendFrequencyInSecs >= 60
```

<span data-ttu-id="cdbad-119">извлекает все двойники устройств, расположенные в США, для которых настроена отправка телеметрии реже, чем раз в минуту.</span><span class="sxs-lookup"><span data-stu-id="cdbad-119">retrieves all device twins located in the US configured to send telemetry less often than every minute.</span></span> <span data-ttu-id="cdbad-120">Для удобства можно также использовать константы массива с операторами **IN** ("входит") и **NIN** ("не входит").</span><span class="sxs-lookup"><span data-stu-id="cdbad-120">As a convenience, it is also possible to use array constants with the **IN** and **NIN** (not in) operators.</span></span> <span data-ttu-id="cdbad-121">Например,</span><span class="sxs-lookup"><span data-stu-id="cdbad-121">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE properties.reported.connectivity IN ['wired', 'wifi']
```

<span data-ttu-id="cdbad-122">извлекает все двойники устройств, сообщившие о подключении по Wi-Fi или проводной сети.</span><span class="sxs-lookup"><span data-stu-id="cdbad-122">retrieves all device twins that reported WiFi or wired connectivity.</span></span> <span data-ttu-id="cdbad-123">Часто требуется определить все двойники устройств, содержащие определенное свойство.</span><span class="sxs-lookup"><span data-stu-id="cdbad-123">It is often necessary to identify all device twins that contain a specific property.</span></span> <span data-ttu-id="cdbad-124">Для этой цели Центр Интернета вещей поддерживает функцию `is_defined()`.</span><span class="sxs-lookup"><span data-stu-id="cdbad-124">IoT Hub supports the function `is_defined()` for this purpose.</span></span> <span data-ttu-id="cdbad-125">Например,</span><span class="sxs-lookup"><span data-stu-id="cdbad-125">For instance,</span></span>

```SQL
SELECT * FROM devices
WHERE is_defined(properties.reported.connectivity)
```

<span data-ttu-id="cdbad-126">извлекает все двойники устройств, которые определяют сообщаемое свойство `connectivity`.</span><span class="sxs-lookup"><span data-stu-id="cdbad-126">retrieved all device twins that define the `connectivity` reported property.</span></span> <span data-ttu-id="cdbad-127">Полное описание возможностей фильтрации см. в разделе [Предложение WHERE][lnk-query-where].</span><span class="sxs-lookup"><span data-stu-id="cdbad-127">Refer to the [WHERE clause][lnk-query-where] section for the full reference of the filtering capabilities.</span></span>

<span data-ttu-id="cdbad-128">Кроме того, поддерживаются группирование и агрегаты.</span><span class="sxs-lookup"><span data-stu-id="cdbad-128">Grouping and aggregations are also supported.</span></span> <span data-ttu-id="cdbad-129">Например,</span><span class="sxs-lookup"><span data-stu-id="cdbad-129">For instance,</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="cdbad-130">возвращает количество устройств в каждом состоянии конфигурации телеметрии.</span><span class="sxs-lookup"><span data-stu-id="cdbad-130">returns the count of the devices in each telemetry configuration status.</span></span>

```json
[
    {
        "numberOfDevices": 3,
        "status": "Success"
    },
    {
        "numberOfDevices": 2,
        "status": "Pending"
    },
    {
        "numberOfDevices": 1,
        "status": "Error"
    }
]
```

<span data-ttu-id="cdbad-131">В предыдущем примере показана ситуация, когда три устройства сообщили об успешной конфигурации, два все еще применяют конфигурацию, а одно сообщило об ошибке.</span><span class="sxs-lookup"><span data-stu-id="cdbad-131">The preceding example illustrates a situation where three devices reported successful configuration, two are still applying the configuration, and one reported an error.</span></span>

### <a name="c-example"></a><span data-ttu-id="cdbad-132">Пример C#</span><span class="sxs-lookup"><span data-stu-id="cdbad-132">C# example</span></span>
<span data-ttu-id="cdbad-133">Функция обработки запросов предоставляется в [пакете SDK для служб C#][lnk-hub-sdks] в классе **RegistryManager**.</span><span class="sxs-lookup"><span data-stu-id="cdbad-133">The query functionality is exposed by the [C# service SDK][lnk-hub-sdks] in the **RegistryManager** class.</span></span>
<span data-ttu-id="cdbad-134">Ниже приведен пример простого запроса:</span><span class="sxs-lookup"><span data-stu-id="cdbad-134">Here is an example of a simple query:</span></span>

```csharp
var query = registryManager.CreateQuery("SELECT * FROM devices", 100);
while (query.HasMoreResults)
{
    var page = await query.GetNextAsTwinAsync();
    foreach (var twin in page)
    {
        // do work on twin object
    }
}
```

<span data-ttu-id="cdbad-135">Обратите внимание, как создается экземпляр объекта **query** с размером страницы (до 1000), а затем можно получить несколько страниц, вызвав метод **GetNextAsTwinAsync** несколько раз.</span><span class="sxs-lookup"><span data-stu-id="cdbad-135">Note how the **query** object is instantiated with a page size (up to 1000), and then multiple pages can be retrieved by calling the **GetNextAsTwinAsync** methods multiple times.</span></span>
<span data-ttu-id="cdbad-136">Обратите внимание, что объект query предоставляет несколько вариантов **next\*** в зависимости от параметра десериализации, требуемого для запроса. Это могут быть объекты двойников устройств, объекты заданий или простой JSON, который применяется при использовании проекций.</span><span class="sxs-lookup"><span data-stu-id="cdbad-136">Note that the query object exposes multiple **Next\***, depending on the deserialization option required by the query, such as device twin or job objects, or plain JSON to be used when using projections.</span></span>

### <a name="nodejs-example"></a><span data-ttu-id="cdbad-137">Пример для Node.js</span><span class="sxs-lookup"><span data-stu-id="cdbad-137">Node.js example</span></span>
<span data-ttu-id="cdbad-138">Функция обработки запросов предоставляется в [пакете SDK службы Azure IoT для Node.js][lnk-hub-sdks] в объекте **Registry**.</span><span class="sxs-lookup"><span data-stu-id="cdbad-138">The query functionality is exposed by the [Azure IoT service SDK for Node.js][lnk-hub-sdks] in the **Registry** object.</span></span>
<span data-ttu-id="cdbad-139">Ниже приведен пример простого запроса:</span><span class="sxs-lookup"><span data-stu-id="cdbad-139">Here is an example of a simple query:</span></span>

```nodejs
var query = registry.createQuery('SELECT * FROM devices', 100);
var onResults = function(err, results) {
    if (err) {
        console.error('Failed to fetch the results: ' + err.message);
    } else {
        // Do something with the results
        results.forEach(function(twin) {
            console.log(twin.deviceId);
        });

        if (query.hasMoreResults) {
            query.nextAsTwin(onResults);
        }
    }
};
query.nextAsTwin(onResults);
```

<span data-ttu-id="cdbad-140">Обратите внимание, как создается экземпляр объекта **query** с размером страницы (до 1000), а затем можно получить несколько страниц, вызвав метод **nextAsTwin** несколько раз.</span><span class="sxs-lookup"><span data-stu-id="cdbad-140">Note how the **query** object is instantiated with a page size (up to 1000), and then multiple pages can be retrieved by calling the **nextAsTwin** methods multiple times.</span></span>
<span data-ttu-id="cdbad-141">Обратите внимание, что объект query предоставляет несколько вариантов **next\*** в зависимости от параметра десериализации, требуемого для запроса. Это могут быть объекты двойников устройств, объекты заданий или простой JSON, который применяется при использовании проекций.</span><span class="sxs-lookup"><span data-stu-id="cdbad-141">Note that the query object exposes multiple **next\***, depending on the deserialization option required by the query, such as device twin or job objects, or plain JSON to be used when using projections.</span></span>

### <a name="limitations"></a><span data-ttu-id="cdbad-142">Ограничения</span><span class="sxs-lookup"><span data-stu-id="cdbad-142">Limitations</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cdbad-143">Результаты запросов могут поступать с задержкой в несколько минут и не учитывать последние значения в двойниках устройств.</span><span class="sxs-lookup"><span data-stu-id="cdbad-143">Query results can have a few minutes of delay with respect to the latest values in device twins.</span></span> <span data-ttu-id="cdbad-144">При запросе данных отдельных двойников устройств по идентификатору всегда предпочтительнее использовать интерфейс API, который применяется для извлечения таких двойников. Он всегда содержит последние значения и обладает более высокими пределами регулирования.</span><span class="sxs-lookup"><span data-stu-id="cdbad-144">If querying individual device twins by id, it is always preferable to use the retrieve device twin API, which always contains the latest values and has higher throttling limits.</span></span>

<span data-ttu-id="cdbad-145">В настоящее время сравнения поддерживаются только между типами-примитивами (не объектами), например, `... WHERE properties.desired.config = properties.reported.config` поддерживается только в том случае, если эти свойства имеют примитивные значения.</span><span class="sxs-lookup"><span data-stu-id="cdbad-145">Currently, comparisons are supported only between primitive types (no objects), for instance `... WHERE properties.desired.config = properties.reported.config` is supported only if those properties have primitive values.</span></span>

## <a name="get-started-with-jobs-queries"></a><span data-ttu-id="cdbad-146">Начало работы с запросами заданий</span><span class="sxs-lookup"><span data-stu-id="cdbad-146">Get started with jobs queries</span></span>
<span data-ttu-id="cdbad-147">[Задания][lnk-jobs] позволяют выполнять операции с наборами устройств.</span><span class="sxs-lookup"><span data-stu-id="cdbad-147">[Jobs][lnk-jobs] provide a way to execute operations on sets of devices.</span></span> <span data-ttu-id="cdbad-148">Каждый двойник устройства содержит сведения о заданиях, в которых он участвует, в коллекции с именем **jobs**.</span><span class="sxs-lookup"><span data-stu-id="cdbad-148">Each device twin contains the information of the jobs of which it is part in a collection called **jobs**.</span></span>
<span data-ttu-id="cdbad-149">Логически получается следующее:</span><span class="sxs-lookup"><span data-stu-id="cdbad-149">Logically,</span></span>

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        ...
    },
    "properties": {
        ...
    },
    "jobs": [
        {
            "deviceId": "myDeviceId",
            "jobId": "myJobId",
            "jobType": "scheduleTwinUpdate",
            "status": "completed",
            "startTimeUtc": "2016-09-29T18:18:52.7418462",
            "endTimeUtc": "2016-09-29T18:20:52.7418462",
            "createdDateTimeUtc": "2016-09-29T18:18:56.7787107Z",
            "lastUpdatedDateTimeUtc": "2016-09-29T18:18:56.8894408Z",
            "outcome": {
                "deviceMethodResponse": null
            }
        },
        ...
    ]
}
```

<span data-ttu-id="cdbad-150">В настоящее время к этой коллекции можно выполнить запрос как к **devices.jobs** на языке запросов Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="cdbad-150">Currently, this collection is queryable as **devices.jobs** in the IoT Hub query language.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cdbad-151">Сейчас свойство jobs никогда не возвращается при запросах двойников устройств (т. е. при запросах, содержащих текст FROM devices).</span><span class="sxs-lookup"><span data-stu-id="cdbad-151">Currently, the jobs property is never returned when querying device twins (that is, queries that contains 'FROM devices').</span></span> <span data-ttu-id="cdbad-152">Доступ к нему можно получить только непосредственно с помощью запросов, использующих `FROM devices.jobs`.</span><span class="sxs-lookup"><span data-stu-id="cdbad-152">It can only be accessed directly with queries using `FROM devices.jobs`.</span></span>
>
>

<span data-ttu-id="cdbad-153">Например, чтобы получить все задания (выполненные и запланированные), влияющие на одно устройство, можно использовать следующий запрос:</span><span class="sxs-lookup"><span data-stu-id="cdbad-153">For instance, to get all jobs (past and scheduled) that affect a single device, you can use the following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
```

<span data-ttu-id="cdbad-154">Обратите внимание, как этот запрос предоставляет сведения о состоянии конкретного устройства (и, возможно, ответ на прямой метод) в каждом возвращенном задании.</span><span class="sxs-lookup"><span data-stu-id="cdbad-154">Note how this query provides the device-specific status (and possibly the direct method response) of each job returned.</span></span>
<span data-ttu-id="cdbad-155">Все свойства объектов в коллекции **devices.jobs** можно также отфильтровать с помощью произвольных логических условий.</span><span class="sxs-lookup"><span data-stu-id="cdbad-155">It is also possible to filter with arbitrary Boolean conditions on all object properties in the **devices.jobs** collection.</span></span>
<span data-ttu-id="cdbad-156">Например, следующий запрос:</span><span class="sxs-lookup"><span data-stu-id="cdbad-156">For instance, the following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
    AND devices.jobs.jobType = 'scheduleTwinUpdate'
    AND devices.jobs.status = 'completed'
    AND devices.jobs.createdTimeUtc > '2016-09-01'
```

<span data-ttu-id="cdbad-157">получает список всех завершенных заданий обновления двойников устройств для устройства **myDeviceId**, созданных после сентября 2016 года.</span><span class="sxs-lookup"><span data-stu-id="cdbad-157">retrieves all completed device twin update jobs for device **myDeviceId** that were created after September 2016.</span></span>

<span data-ttu-id="cdbad-158">Кроме того, можно получить результаты выполнения одного задания для каждого устройства.</span><span class="sxs-lookup"><span data-stu-id="cdbad-158">It is also possible to retrieve the per-device outcomes of a single job.</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.jobId = 'myJobId'
```

### <a name="limitations"></a><span data-ttu-id="cdbad-159">Ограничения</span><span class="sxs-lookup"><span data-stu-id="cdbad-159">Limitations</span></span>
<span data-ttu-id="cdbad-160">В настоящее время запросы к **devices.jobs** не поддерживают следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="cdbad-160">Currently, queries on **devices.jobs** do not support:</span></span>

* <span data-ttu-id="cdbad-161">проекции, поэтому можно использовать только `SELECT *`;</span><span class="sxs-lookup"><span data-stu-id="cdbad-161">Projections, therefore only `SELECT *` is possible.</span></span>
* <span data-ttu-id="cdbad-162">условия, касающиеся двойника устройства, и свойства задания (см. предыдущий раздел);</span><span class="sxs-lookup"><span data-stu-id="cdbad-162">Conditions that refer to the device twin in addition to job properties (see the preceding section).</span></span>
* <span data-ttu-id="cdbad-163">выполняемые агрегаты, например count, avg, group by.</span><span class="sxs-lookup"><span data-stu-id="cdbad-163">Performing aggregations, such as count, avg, group by.</span></span>

## <a name="get-started-with-device-to-cloud-message-routes-query-expressions"></a><span data-ttu-id="cdbad-164">Начало работы с выражениями запросов по маршрутам сообщений, отправляемых с устройства в облако</span><span class="sxs-lookup"><span data-stu-id="cdbad-164">Get started with device-to-cloud message routes query expressions</span></span>

<span data-ttu-id="cdbad-165">С помощью [маршрутов от устройства в облако][lnk-devguide-messaging-routes] можно сделать так, чтобы Центр Интернета вещей передавал сообщения, отправляемые с устройства в облако, в разные конечные точки на основе условий, вычисляемых для отдельных сообщений.</span><span class="sxs-lookup"><span data-stu-id="cdbad-165">Using [device-to-cloud routes][lnk-devguide-messaging-routes], you can configure IoT Hub to dispatch device-to-cloud messages to different endpoints based on expressions evaluated against individual messages.</span></span>

<span data-ttu-id="cdbad-166">Используемое в маршруте [условие][lnk-query-expressions] создается на том же языка запросов Центра Интернета вещей, что и условия в запросах двойников и заданий.</span><span class="sxs-lookup"><span data-stu-id="cdbad-166">The route [condition][lnk-query-expressions] uses the same IoT Hub query language as conditions in twin and job queries.</span></span> <span data-ttu-id="cdbad-167">Условия маршрута вычисляются по заголовкам и тексту сообщения.</span><span class="sxs-lookup"><span data-stu-id="cdbad-167">Route conditions are evaluated on the message headers and body.</span></span> <span data-ttu-id="cdbad-168">Выражение запроса маршрутизации может включать только заголовки сообщений, только текст сообщения или заголовки и текст сообщения.</span><span class="sxs-lookup"><span data-stu-id="cdbad-168">Your routing query expression may involve only message headers, only the message body, or both message headers and message body.</span></span> <span data-ttu-id="cdbad-169">Центр Интернета вещей предполагает наличие определенной схемы для заголовков и текста сообщения для маршрутизации сообщений. В следующих разделах описываются необходимые условия правильной маршрутизации Центра Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="cdbad-169">IoT Hub assumes a specific schema for the headers and message body in order to route messages, and the following sections describe what is required for IoT Hub to properly route:</span></span>

### <a name="routing-on-message-headers"></a><span data-ttu-id="cdbad-170">Маршрутизация по заголовкам сообщений</span><span class="sxs-lookup"><span data-stu-id="cdbad-170">Routing on message headers</span></span>

<span data-ttu-id="cdbad-171">Центр Интернета вещей предполагает следующее представление JSON заголовков сообщений для маршрутизации:</span><span class="sxs-lookup"><span data-stu-id="cdbad-171">IoT Hub assumes the following JSON representation of message headers for message routing:</span></span>

```json
{
    "$messageId": "",
    "$enqueuedTime": "",
    "$to": "",
    "$expiryTimeUtc": "",
    "$correlationId": "",
    "$userId": "",
    "$ack": "",
    "$connectionDeviceId": "",
    "$connectionDeviceGenerationId": "",
    "$connectionAuthMethod": "",
    "$content-type": "",
    "$content-encoding": "",

    "userProperty1": "",
    "userProperty2": ""
}
```

<span data-ttu-id="cdbad-172">Системные свойства сообщений начинаются с символов `'$'`.</span><span class="sxs-lookup"><span data-stu-id="cdbad-172">Message system properties are prefixed with the `'$'` symbol.</span></span>
<span data-ttu-id="cdbad-173">Доступ к пользовательским свойствам всегда осуществляется с использованием их имен.</span><span class="sxs-lookup"><span data-stu-id="cdbad-173">User properties are always accessed with their name.</span></span> <span data-ttu-id="cdbad-174">Если имя пользовательского свойства совпадает с системным свойством (например, `$to`), такое пользовательское свойство будут извлечено с помощью выражения `$to`.</span><span class="sxs-lookup"><span data-stu-id="cdbad-174">If a user property name happens to coincide with a system property (such as `$to`), the user property will be retrieved with the `$to` expression.</span></span>
<span data-ttu-id="cdbad-175">Вы всегда можете получить доступ к системному свойству с помощью квадратных скобок `{}`: например, можно использовать выражение `{$to}` для доступа к системному свойству `to`.</span><span class="sxs-lookup"><span data-stu-id="cdbad-175">You can always access the system property using brackets `{}`: for instance, you can use the expression `{$to}` to access the system property `to`.</span></span> <span data-ttu-id="cdbad-176">Имена свойств в квадратных скобках всегда позволяют получить соответствующее системное свойство.</span><span class="sxs-lookup"><span data-stu-id="cdbad-176">Bracketed property names always retrieve the corresponding system property.</span></span>

<span data-ttu-id="cdbad-177">Не забывайте, что в именах свойств не учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="cdbad-177">Remember that property names are case insensitive.</span></span>

> [!NOTE]
> <span data-ttu-id="cdbad-178">Все свойства сообщения являются строками.</span><span class="sxs-lookup"><span data-stu-id="cdbad-178">All message properties are strings.</span></span> <span data-ttu-id="cdbad-179">Системные свойства сейчас нельзя использовать в запросах (см. [руководство разработчика][lnk-devguide-messaging-format]).</span><span class="sxs-lookup"><span data-stu-id="cdbad-179">System properties, as described in the [developer guide][lnk-devguide-messaging-format], are currently not available to use in queries.</span></span>
>

<span data-ttu-id="cdbad-180">Например, если вы используете свойство `messageType`, вы можете направлять все данные телеметрии в одну конечную точку, а все оповещения — в другую.</span><span class="sxs-lookup"><span data-stu-id="cdbad-180">For example, if you use a `messageType` property, you might want to route all telemetry to one endpoint, and all alerts to another endpoint.</span></span> <span data-ttu-id="cdbad-181">Следующее выражение позволяет перенаправить данные телеметрии:</span><span class="sxs-lookup"><span data-stu-id="cdbad-181">You can write the following expression to route the telemetry:</span></span>

```sql
messageType = 'telemetry'
```

<span data-ttu-id="cdbad-182">А это выражение будет перенаправлять текст оповещения:</span><span class="sxs-lookup"><span data-stu-id="cdbad-182">And the following expression to route the alert messages:</span></span>

```sql
messageType = 'alert'
```

<span data-ttu-id="cdbad-183">Также поддерживаются логические выражения и функции.</span><span class="sxs-lookup"><span data-stu-id="cdbad-183">Boolean expressions and functions are also supported.</span></span> <span data-ttu-id="cdbad-184">Например, это позволяет различать сообщения по уровню серьезности:</span><span class="sxs-lookup"><span data-stu-id="cdbad-184">This feature enables you to distinguish between severity level, for example:</span></span>

```sql
messageType = 'alerts' AND as_number(severity) <= 2
```

<span data-ttu-id="cdbad-185">Полный список поддерживаемых операторов и функций вы найдете в разделе [Выражения и условия][lnk-query-expressions].</span><span class="sxs-lookup"><span data-stu-id="cdbad-185">Refer to the [Expression and conditions][lnk-query-expressions] section for the full list of supported operators and functions.</span></span>

### <a name="routing-on-message-bodies"></a><span data-ttu-id="cdbad-186">Маршрутизация по тексту сообщений</span><span class="sxs-lookup"><span data-stu-id="cdbad-186">Routing on message bodies</span></span>

<span data-ttu-id="cdbad-187">Центр Интернета вещей поддерживает маршрутизацию на основе содержимого текста сообщения, только если текст сообщения соответствует формату JSON в кодировке UTF-8, UTF-16 или UTF-32.</span><span class="sxs-lookup"><span data-stu-id="cdbad-187">IoT Hub can only route based on message body contents if the message body is properly formed JSON encoded in either UTF-8, UTF-16, or UTF-32.</span></span> <span data-ttu-id="cdbad-188">В качестве типа содержимого сообщения необходимо задать `application/json`, а в качестве кодировки содержимого — одну из поддерживаемых кодировок UTF в заголовках сообщения, чтобы Центр Интернета вещей мог осуществлять маршрутизацию сообщений на основе содержимого текста.</span><span class="sxs-lookup"><span data-stu-id="cdbad-188">You must set the content type of the message to `application/json` and the content encoding to one of the supported UTF encodings in the message headers to allow IoT Hub to route the message based on the body contents.</span></span> <span data-ttu-id="cdbad-189">Если один из заголовков не указан, Центр Интернета вещей не будет пытаться вычислить любое выражение запроса, включающее текст, по сообщению.</span><span class="sxs-lookup"><span data-stu-id="cdbad-189">If either of the headers is not specified, IoT Hub will not attempt to evaluate any query expression involving the body against the message.</span></span> <span data-ttu-id="cdbad-190">Если формат сообщения отличается от JSON или сообщение не указывает тип и кодировку содержимого, маршрутизацию сообщений, тем не менее, можно выполнить на основе заголовков сообщения.</span><span class="sxs-lookup"><span data-stu-id="cdbad-190">If your message is not a JSON message, or if the message does not specify the content type and content encoding, you may still use message routing to route the message based on the message headers.</span></span>

<span data-ttu-id="cdbad-191">Для маршрутизации сообщения можно использовать `$body` в выражении запроса.</span><span class="sxs-lookup"><span data-stu-id="cdbad-191">You can use `$body` in the query expression to route the message.</span></span> <span data-ttu-id="cdbad-192">В выражении запроса можно использовать простую ссылку на текст, ссылку на массив текста или несколько ссылок на текст.</span><span class="sxs-lookup"><span data-stu-id="cdbad-192">You can use a simple body reference, body array reference, or multiple body references in the query expression.</span></span> <span data-ttu-id="cdbad-193">В выражении запроса можно также указывать сочетание ссылки на текст со ссылкой на заголовок сообщения.</span><span class="sxs-lookup"><span data-stu-id="cdbad-193">Your query expression can also combine a body reference with a message header reference.</span></span> <span data-ttu-id="cdbad-194">Например, все выражения, приведенные ниже, допустимы:</span><span class="sxs-lookup"><span data-stu-id="cdbad-194">For example, the following are all valid query expressions:</span></span>

```sql
$body.message.Weather.Location.State = 'WA'
$body.Weather.HistoricalData[0].Month = 'Feb'
$body.Weather.Temperature = 50 AND $body.message.Weather.IsEnabled
length($body.Weather.Location.State) = 2
$body.Weather.Temperature = 50 AND Status = 'Active'
```

## <a name="basics-of-an-iot-hub-query"></a><span data-ttu-id="cdbad-195">Основные сведения о запросе Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="cdbad-195">Basics of an IoT Hub query</span></span>
<span data-ttu-id="cdbad-196">Каждый запрос Центра Интернета вещей состоит из предложений SELECT и FROM, а также необязательных предложений WHERE и GROUP BY.</span><span class="sxs-lookup"><span data-stu-id="cdbad-196">Every IoT Hub query consists of a SELECT and FROM clauses and by optional WHERE and GROUP BY clauses.</span></span> <span data-ttu-id="cdbad-197">Каждый запрос выполняется для коллекции документов JSON, например двойников устройств.</span><span class="sxs-lookup"><span data-stu-id="cdbad-197">Every query is run on a collection of JSON documents, for example device twins.</span></span> <span data-ttu-id="cdbad-198">Предложение FROM указывает коллекцию документов, по которой будет выполняться итерация (**devices** или **devices.jobs**).</span><span class="sxs-lookup"><span data-stu-id="cdbad-198">The FROM clause indicates the document collection to be iterated on (**devices** or **devices.jobs**).</span></span> <span data-ttu-id="cdbad-199">Затем применяется фильтр в предложении WHERE.</span><span class="sxs-lookup"><span data-stu-id="cdbad-199">Then, the filter in the WHERE clause is applied.</span></span> <span data-ttu-id="cdbad-200">При использовании агрегатов результаты этого шага группируются, как указано в предложении GROUP BY. Для каждой группы создается строка, как указано в предложении SELECT.</span><span class="sxs-lookup"><span data-stu-id="cdbad-200">With aggregations, the results of this step are grouped as specified in the GROUP BY clause and, for each group, a row is generated as specified in the SELECT clause.</span></span>

```sql
SELECT <select_list>
FROM <from_specification>
[WHERE <filter_condition>]
[GROUP BY <group_specification>]
```

## <a name="from-clause"></a><span data-ttu-id="cdbad-201">Предложение FROM</span><span class="sxs-lookup"><span data-stu-id="cdbad-201">FROM clause</span></span>
<span data-ttu-id="cdbad-202">Предложение **FROM <из_спецификации>** может предоставить только два значения: **FROM devices** для запроса двойников устройства или **FROM devices.jobs** для запроса сведений о задании для каждого устройства.</span><span class="sxs-lookup"><span data-stu-id="cdbad-202">The **FROM <from_specification>** clause can assume only two values: **FROM devices**, to query device twins, or **FROM devices.jobs**, to query job per-device details.</span></span>

## <a name="where-clause"></a><span data-ttu-id="cdbad-203">Предложение WHERE</span><span class="sxs-lookup"><span data-stu-id="cdbad-203">WHERE clause</span></span>
<span data-ttu-id="cdbad-204">Предложение **WHERE <условие_фильтрации>** является необязательным.</span><span class="sxs-lookup"><span data-stu-id="cdbad-204">The **WHERE <filter_condition>** clause is optional.</span></span> <span data-ttu-id="cdbad-205">Оно определяет одно или несколько условий, которым должны соответствовать документы JSON в коллекции FROM, чтобы быть включенными в результат.</span><span class="sxs-lookup"><span data-stu-id="cdbad-205">It specifies one or more conditions that the JSON documents in the FROM collection must satisfy to be included as part of the result.</span></span> <span data-ttu-id="cdbad-206">Любой документ JSON должен при вычислении указанных условий возвращать значение true, чтобы быть включенным в результат.</span><span class="sxs-lookup"><span data-stu-id="cdbad-206">Any JSON document must evaluate the specified conditions to "true" to be included in the result.</span></span>

<span data-ttu-id="cdbad-207">Допустимые условия описаны в разделе [Выражения и условия][lnk-query-expressions].</span><span class="sxs-lookup"><span data-stu-id="cdbad-207">The allowed conditions are described in section [Expressions and conditions][lnk-query-expressions].</span></span>

## <a name="select-clause"></a><span data-ttu-id="cdbad-208">Предложение SELECT</span><span class="sxs-lookup"><span data-stu-id="cdbad-208">SELECT clause</span></span>
<span data-ttu-id="cdbad-209">Предложение SELECT (**SELECT <список_для_выбора>**) является обязательным. Оно указывает значения, которые будут получены из запроса.</span><span class="sxs-lookup"><span data-stu-id="cdbad-209">The SELECT clause (**SELECT <select_list>**) is mandatory and specifies what values are retrieved from the query.</span></span> <span data-ttu-id="cdbad-210">Здесь задаются значения JSON, которые используются для создания новых объектов JSON.</span><span class="sxs-lookup"><span data-stu-id="cdbad-210">It specifies the JSON values to be used to generate new JSON objects.</span></span>
<span data-ttu-id="cdbad-211">На этапе проекции для каждого элемента, отфильтрованного (и при необходимости сгруппированного) подмножества коллекции FROM создается объект JSON, собранный из значений, которые указаны в предложении SELECT.</span><span class="sxs-lookup"><span data-stu-id="cdbad-211">For each element of the filtered (and optionally grouped) subset of the FROM collection, the projection phase generates a new JSON object, constructed with the values specified in the SELECT clause.</span></span>

<span data-ttu-id="cdbad-212">Далее приводится грамматика предложения SELECT:</span><span class="sxs-lookup"><span data-stu-id="cdbad-212">Following is the grammar of the SELECT clause:</span></span>

```
SELECT [TOP <max number>] <projection list>

<projection_list> ::=
    '*'
    | <projection_element> AS alias [, <projection_element> AS alias]+

<projection_element> :==
    attribute_name
    | <projection_element> '.' attribute_name
    | <aggregate>

<aggregate> :==
    count()
    | avg(<projection_element>)
    | sum(<projection_element>)
    | min(<projection_element>)
    | max(<projection_element>)
```

<span data-ttu-id="cdbad-213">где **attribute_name** относится к любому свойству документа JSON в коллекции FROM.</span><span class="sxs-lookup"><span data-stu-id="cdbad-213">where **attribute_name** refers to any property of the JSON document in the FROM collection.</span></span> <span data-ttu-id="cdbad-214">Некоторые примеры предложений SELECT можно найти в разделе [Начало работы с запросами двойника устройства][lnk-query-getstarted].</span><span class="sxs-lookup"><span data-stu-id="cdbad-214">Some examples of SELECT clauses can be found in the [Getting started with device twin queries][lnk-query-getstarted] section.</span></span>

<span data-ttu-id="cdbad-215">В настоящее время предложения для осуществления выбора, отличные от **SELECT \***, поддерживаются только в статистических запросах к двойникам устройств.</span><span class="sxs-lookup"><span data-stu-id="cdbad-215">Currently, selection clauses different than **SELECT \*** are only supported in aggregate queries on device twins.</span></span>

## <a name="group-by-clause"></a><span data-ttu-id="cdbad-216">Предложение GROUP BY</span><span class="sxs-lookup"><span data-stu-id="cdbad-216">GROUP BY clause</span></span>
<span data-ttu-id="cdbad-217">Предложение **GROUP BY <спецификация_группирования>** является необязательным. Оно выполняется после фильтра, указанного в предложении WHERE, и перед проекцией, указанной в предложении SELECT.</span><span class="sxs-lookup"><span data-stu-id="cdbad-217">The **GROUP BY <group_specification>** clause is an optional step that can be executed after the filter specified in the WHERE clause, and before the projection specified in the SELECT.</span></span> <span data-ttu-id="cdbad-218">Оно группирует документы на основе значения атрибута.</span><span class="sxs-lookup"><span data-stu-id="cdbad-218">It groups documents based on the value of an attribute.</span></span> <span data-ttu-id="cdbad-219">Эти группы используются для создания статистических значений, как указано в предложении SELECT.</span><span class="sxs-lookup"><span data-stu-id="cdbad-219">These groups are used to generate aggregated values as specified in the SELECT clause.</span></span>

<span data-ttu-id="cdbad-220">Ниже представлен пример запроса с использованием предложения GROUP BY:</span><span class="sxs-lookup"><span data-stu-id="cdbad-220">An example of a query using GROUP BY is:</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="cdbad-221">Далее указан формальный синтаксис предложения GROUP BY:</span><span class="sxs-lookup"><span data-stu-id="cdbad-221">The formal syntax for GROUP BY is:</span></span>

```
GROUP BY <group_by_element>
<group_by_element> :==
    attribute_name
    | < group_by_element > '.' attribute_name
```

<span data-ttu-id="cdbad-222">где **attribute_name** относится к любому свойству документа JSON в коллекции FROM.</span><span class="sxs-lookup"><span data-stu-id="cdbad-222">where **attribute_name** refers to any property of the JSON document in the FROM collection.</span></span>

<span data-ttu-id="cdbad-223">В настоящее время предложение GROUP BY поддерживается только при запросе к двойникам устройств.</span><span class="sxs-lookup"><span data-stu-id="cdbad-223">Currently, the GROUP BY clause is only supported when querying device twins.</span></span>

## <a name="expressions-and-conditions"></a><span data-ttu-id="cdbad-224">Выражения и условия</span><span class="sxs-lookup"><span data-stu-id="cdbad-224">Expressions and conditions</span></span>
<span data-ttu-id="cdbad-225">В общем *выражение*:</span><span class="sxs-lookup"><span data-stu-id="cdbad-225">At a high level, an *expression*:</span></span>

* <span data-ttu-id="cdbad-226">возвращает экземпляр типа JSON (например логическое значение, число, строка, массив или объект);</span><span class="sxs-lookup"><span data-stu-id="cdbad-226">Evaluates to an instance of a JSON type (such as Boolean, number, string, array, or object), and</span></span>
* <span data-ttu-id="cdbad-227">определяется обработкой данных, поступающих из документа JSON устройства, и констант с помощью встроенных операторов и функций.</span><span class="sxs-lookup"><span data-stu-id="cdbad-227">Is defined by manipulating data coming from the device JSON document and constants using built-in operators and functions.</span></span>

<span data-ttu-id="cdbad-228">*Условия* — это выражения, результатом вычисления которых является логическое значение.</span><span class="sxs-lookup"><span data-stu-id="cdbad-228">*Conditions* are expressions that evaluate to a Boolean.</span></span> <span data-ttu-id="cdbad-229">Все константы, значения которых отличаются от логического значения **true**, трактуются как значение **false** (в том числе значения **null**, **undefined**, любые экземпляры объектов или массивов, любые строки и, разумеется, само логическое значение **false**).</span><span class="sxs-lookup"><span data-stu-id="cdbad-229">Any constant different than Boolean **true** is considered as **false** (including **null**, **undefined**, any object or array instance, any string, and clearly the Boolean **false**).</span></span>

<span data-ttu-id="cdbad-230">Выражения имеют следующий синтаксис:</span><span class="sxs-lookup"><span data-stu-id="cdbad-230">The syntax for expressions is:</span></span>

```
<expression> ::=
    <constant> |
    attribute_name |
    <function_call> |
    <expression> binary_operator <expression> |
    <create_array_expression> |
    '(' <expression> ')'

<function_call> ::=
    <function_name> '(' expression ')'

<constant> ::=
    <undefined_constant>
    | <null_constant>
    | <number_constant>
    | <string_constant>
    | <array_constant>

<undefined_constant> ::= undefined
<null_constant> ::= null
<number_constant> ::= decimal_literal | hexadecimal_literal
<string_constant> ::= string_literal
<array_constant> ::= '[' <constant> [, <constant>]+ ']'
```

<span data-ttu-id="cdbad-231">Описание:</span><span class="sxs-lookup"><span data-stu-id="cdbad-231">where:</span></span>

| <span data-ttu-id="cdbad-232">Знак</span><span class="sxs-lookup"><span data-stu-id="cdbad-232">Symbol</span></span> | <span data-ttu-id="cdbad-233">Определение</span><span class="sxs-lookup"><span data-stu-id="cdbad-233">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="cdbad-234">attribute_name</span><span class="sxs-lookup"><span data-stu-id="cdbad-234">attribute_name</span></span> | <span data-ttu-id="cdbad-235">Любое свойство документа JSON в коллекции **FROM**.</span><span class="sxs-lookup"><span data-stu-id="cdbad-235">Any property of the JSON document in the **FROM** collection.</span></span> |
| <span data-ttu-id="cdbad-236">binary_operator</span><span class="sxs-lookup"><span data-stu-id="cdbad-236">binary_operator</span></span> | <span data-ttu-id="cdbad-237">Любой бинарный оператор, перечисленный в разделе [Операторы](#operators).</span><span class="sxs-lookup"><span data-stu-id="cdbad-237">Any binary operator listed in the [Operators](#operators) section.</span></span> |
| <span data-ttu-id="cdbad-238">function_name</span><span class="sxs-lookup"><span data-stu-id="cdbad-238">function_name</span></span>| <span data-ttu-id="cdbad-239">Любая функция, перечисленная в разделе [Функции](#functions).</span><span class="sxs-lookup"><span data-stu-id="cdbad-239">Any function listed in the [Functions](#functions) section.</span></span> |
| <span data-ttu-id="cdbad-240">decimal_literal</span><span class="sxs-lookup"><span data-stu-id="cdbad-240">decimal_literal</span></span> |<span data-ttu-id="cdbad-241">Число с плавающей запятой в десятичном представлении.</span><span class="sxs-lookup"><span data-stu-id="cdbad-241">A float expressed in decimal notation.</span></span> |
| <span data-ttu-id="cdbad-242">hexadecimal_literal</span><span class="sxs-lookup"><span data-stu-id="cdbad-242">hexadecimal_literal</span></span> |<span data-ttu-id="cdbad-243">Число, представленное строкой 0x, за которой следует строка с шестнадцатеричными цифрами.</span><span class="sxs-lookup"><span data-stu-id="cdbad-243">A number expressed by the string ‘0x’ followed by a string of hexadecimal digits.</span></span> |
| <span data-ttu-id="cdbad-244">string_literal</span><span class="sxs-lookup"><span data-stu-id="cdbad-244">string_literal</span></span> |<span data-ttu-id="cdbad-245">Строковые литералы — это строки Юникода, представленные в виде последовательности из нуля или более знаков Юникода или escape-последовательностей.</span><span class="sxs-lookup"><span data-stu-id="cdbad-245">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="cdbad-246">Строковые литералы заключаются в одинарные кавычки (апостроф — ') или двойные кавычки (кавычки — ").</span><span class="sxs-lookup"><span data-stu-id="cdbad-246">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span> <span data-ttu-id="cdbad-247">В знаках Юникода, определяемых 4 шестнадцатеричными цифрами, разрешено использовать escape-символы `\'`, `\"`, `\\` и `\uXXXX`.</span><span class="sxs-lookup"><span data-stu-id="cdbad-247">Allowed escapes: `\'`, `\"`, `\\`, `\uXXXX` for Unicode characters defined by 4 hexadecimal digits.</span></span> |

### <a name="operators"></a><span data-ttu-id="cdbad-248">Операторы</span><span class="sxs-lookup"><span data-stu-id="cdbad-248">Operators</span></span>
<span data-ttu-id="cdbad-249">Поддерживаются следующие операторы:</span><span class="sxs-lookup"><span data-stu-id="cdbad-249">The following operators are supported:</span></span>

| <span data-ttu-id="cdbad-250">Семейство</span><span class="sxs-lookup"><span data-stu-id="cdbad-250">Family</span></span> | <span data-ttu-id="cdbad-251">Операторы</span><span class="sxs-lookup"><span data-stu-id="cdbad-251">Operators</span></span> |
| --- | --- |
| <span data-ttu-id="cdbad-252">Арифметические</span><span class="sxs-lookup"><span data-stu-id="cdbad-252">Arithmetic</span></span> |<span data-ttu-id="cdbad-253">+,-,*,/,%</span><span class="sxs-lookup"><span data-stu-id="cdbad-253">+,-,*,/,%</span></span> |
| <span data-ttu-id="cdbad-254">Логические</span><span class="sxs-lookup"><span data-stu-id="cdbad-254">Logical</span></span> |<span data-ttu-id="cdbad-255">AND, OR, NOT</span><span class="sxs-lookup"><span data-stu-id="cdbad-255">AND, OR, NOT</span></span> |
| <span data-ttu-id="cdbad-256">Сравнение</span><span class="sxs-lookup"><span data-stu-id="cdbad-256">Comparison</span></span> |<span data-ttu-id="cdbad-257">=, !=, <, >, <=, >=, <></span><span class="sxs-lookup"><span data-stu-id="cdbad-257">=, !=, <, >, <=, >=, <></span></span> |

### <a name="functions"></a><span data-ttu-id="cdbad-258">Функции</span><span class="sxs-lookup"><span data-stu-id="cdbad-258">Functions</span></span>
<span data-ttu-id="cdbad-259">В запросах двойников и заданий поддерживается только одна функция.</span><span class="sxs-lookup"><span data-stu-id="cdbad-259">When querying twins and jobs the only supported function is:</span></span>

| <span data-ttu-id="cdbad-260">Функция</span><span class="sxs-lookup"><span data-stu-id="cdbad-260">Function</span></span> | <span data-ttu-id="cdbad-261">Описание</span><span class="sxs-lookup"><span data-stu-id="cdbad-261">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="cdbad-262">IS_DEFINED(Свойство)</span><span class="sxs-lookup"><span data-stu-id="cdbad-262">IS_DEFINED(property)</span></span> | <span data-ttu-id="cdbad-263">Возвращает логическое значение, указывающее, назначено ли свойству значение (в том числе значение `null`).</span><span class="sxs-lookup"><span data-stu-id="cdbad-263">Returns a Boolean indicating if the property has been assigned a value (including `null`).</span></span> |

<span data-ttu-id="cdbad-264">В условиях маршрута поддерживаются следующие математические функции.</span><span class="sxs-lookup"><span data-stu-id="cdbad-264">In routes conditions, the following math functions are supported:</span></span>

| <span data-ttu-id="cdbad-265">Функция</span><span class="sxs-lookup"><span data-stu-id="cdbad-265">Function</span></span> | <span data-ttu-id="cdbad-266">Описание</span><span class="sxs-lookup"><span data-stu-id="cdbad-266">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="cdbad-267">ABS(x)</span><span class="sxs-lookup"><span data-stu-id="cdbad-267">ABS(x)</span></span> | <span data-ttu-id="cdbad-268">Возвращает модуль (положительное значение) указанного числового выражения.</span><span class="sxs-lookup"><span data-stu-id="cdbad-268">Returns the absolute (positive) value of the specified numeric expression.</span></span> |
| <span data-ttu-id="cdbad-269">EXP(x)</span><span class="sxs-lookup"><span data-stu-id="cdbad-269">EXP(x)</span></span> | <span data-ttu-id="cdbad-270">Возвращает значение экспоненты для указанного числового выражения (e^x).</span><span class="sxs-lookup"><span data-stu-id="cdbad-270">Returns the exponential value of the specified numeric expression (e^x).</span></span> |
| <span data-ttu-id="cdbad-271">POWER(x,y)</span><span class="sxs-lookup"><span data-stu-id="cdbad-271">POWER(x,y)</span></span> | <span data-ttu-id="cdbad-272">Возвращает результат возведения указанного числового выражения в заданную степень (x^y).</span><span class="sxs-lookup"><span data-stu-id="cdbad-272">Returns the value of the specified expression to the specified power (x^y).</span></span>|
| <span data-ttu-id="cdbad-273">SQUARE(x)</span><span class="sxs-lookup"><span data-stu-id="cdbad-273">SQUARE(x)</span></span> | <span data-ttu-id="cdbad-274">Возвращает квадратный корень из указанного числового значения.</span><span class="sxs-lookup"><span data-stu-id="cdbad-274">Returns the square of the specified numeric value.</span></span> |
| <span data-ttu-id="cdbad-275">CEILING(x)</span><span class="sxs-lookup"><span data-stu-id="cdbad-275">CEILING(x)</span></span> | <span data-ttu-id="cdbad-276">Возвращает наименьшее целочисленное значение, которое больше или равно указанному числовому выражению.</span><span class="sxs-lookup"><span data-stu-id="cdbad-276">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span></span> |
| <span data-ttu-id="cdbad-277">FLOOR(x)</span><span class="sxs-lookup"><span data-stu-id="cdbad-277">FLOOR(x)</span></span> | <span data-ttu-id="cdbad-278">Возвращает наибольшее целочисленное значение, которое меньше или равно указанному числовому выражению.</span><span class="sxs-lookup"><span data-stu-id="cdbad-278">Returns the largest integer less than or equal to the specified numeric expression.</span></span> |
| <span data-ttu-id="cdbad-279">SIGN(x)</span><span class="sxs-lookup"><span data-stu-id="cdbad-279">SIGN(x)</span></span> | <span data-ttu-id="cdbad-280">Возвращает знак указанного числового выражения (+1 для положительных чисел, 0 для нуля или -1 для отрицательных).</span><span class="sxs-lookup"><span data-stu-id="cdbad-280">Returns the positive (+1), zero (0), or negative (-1) sign of the specified numeric expression.</span></span>|
| <span data-ttu-id="cdbad-281">SQRT(x)</span><span class="sxs-lookup"><span data-stu-id="cdbad-281">SQRT(x)</span></span> | <span data-ttu-id="cdbad-282">Возвращает квадратный корень из указанного числового значения.</span><span class="sxs-lookup"><span data-stu-id="cdbad-282">Returns the square of the specified numeric value.</span></span> |

<span data-ttu-id="cdbad-283">В условиях маршрута поддерживаются следующие функции проверки и приведения типов.</span><span class="sxs-lookup"><span data-stu-id="cdbad-283">In routes conditions, the following type checking and casting functions are supported:</span></span>

| <span data-ttu-id="cdbad-284">Функция</span><span class="sxs-lookup"><span data-stu-id="cdbad-284">Function</span></span> | <span data-ttu-id="cdbad-285">Описание</span><span class="sxs-lookup"><span data-stu-id="cdbad-285">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="cdbad-286">AS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="cdbad-286">AS_NUMBER</span></span> | <span data-ttu-id="cdbad-287">Преобразует входную строку в число.</span><span class="sxs-lookup"><span data-stu-id="cdbad-287">Converts the input string to a number.</span></span> <span data-ttu-id="cdbad-288">Возвращает `noop`, если аргумент является числом, или `Undefined`, если строка не представляет число.</span><span class="sxs-lookup"><span data-stu-id="cdbad-288">`noop` if input is a number; `Undefined` if string does not represent a number.</span></span>|
| <span data-ttu-id="cdbad-289">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="cdbad-289">IS_ARRAY</span></span> | <span data-ttu-id="cdbad-290">Возвращает логическое значение, указывающее, является ли указанное выражение массивом.</span><span class="sxs-lookup"><span data-stu-id="cdbad-290">Returns a Boolean value indicating if the type of the specified expression is an array.</span></span> |
| <span data-ttu-id="cdbad-291">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="cdbad-291">IS_BOOL</span></span> | <span data-ttu-id="cdbad-292">Возвращает логическое значение, указывающее, является ли указанное выражение логическим значением.</span><span class="sxs-lookup"><span data-stu-id="cdbad-292">Returns a Boolean value indicating if the type of the specified expression is a Boolean.</span></span> |
| <span data-ttu-id="cdbad-293">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="cdbad-293">IS_DEFINED</span></span> | <span data-ttu-id="cdbad-294">Возвращает логическое значение, указывающее, назначено ли свойству значение.</span><span class="sxs-lookup"><span data-stu-id="cdbad-294">Returns a Boolean indicating if the property has been assigned a value.</span></span> |
| <span data-ttu-id="cdbad-295">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="cdbad-295">IS_NULL</span></span> | <span data-ttu-id="cdbad-296">Возвращает логическое значение, указывающее, является ли указанное выражение значением Null.</span><span class="sxs-lookup"><span data-stu-id="cdbad-296">Returns a Boolean value indicating if the type of the specified expression is null.</span></span> |
| <span data-ttu-id="cdbad-297">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="cdbad-297">IS_NUMBER</span></span> | <span data-ttu-id="cdbad-298">Возвращает логическое значение, указывающее, является ли указанное выражение числовым значением.</span><span class="sxs-lookup"><span data-stu-id="cdbad-298">Returns a Boolean value indicating if the type of the specified expression is a number.</span></span> |
| <span data-ttu-id="cdbad-299">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="cdbad-299">IS_OBJECT</span></span> | <span data-ttu-id="cdbad-300">Возвращает логическое значение, указывающее, является ли указанное выражение объектом JSON.</span><span class="sxs-lookup"><span data-stu-id="cdbad-300">Returns a Boolean value indicating if the type of the specified expression is a JSON object.</span></span> |
| <span data-ttu-id="cdbad-301">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="cdbad-301">IS_PRIMITIVE</span></span> | <span data-ttu-id="cdbad-302">Возвращает логическое значение, указывающее, является ли указанное выражение примитивом (строкой, логическим значением, числовым значением или `null`).</span><span class="sxs-lookup"><span data-stu-id="cdbad-302">Returns a Boolean value indicating if the type of the specified expression is a primitive (string, Boolean, numeric or `null`).</span></span> |
| <span data-ttu-id="cdbad-303">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="cdbad-303">IS_STRING</span></span> | <span data-ttu-id="cdbad-304">Возвращает логическое значение, указывающее, является ли указанное выражение строковым значением.</span><span class="sxs-lookup"><span data-stu-id="cdbad-304">Returns a Boolean value indicating if the type of the specified expression is a string.</span></span> |

<span data-ttu-id="cdbad-305">В условиях маршрутов поддерживаются следующие строковые функции.</span><span class="sxs-lookup"><span data-stu-id="cdbad-305">In routes conditions, the following string functions are supported:</span></span>

| <span data-ttu-id="cdbad-306">Функция</span><span class="sxs-lookup"><span data-stu-id="cdbad-306">Function</span></span> | <span data-ttu-id="cdbad-307">Описание</span><span class="sxs-lookup"><span data-stu-id="cdbad-307">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="cdbad-308">CONCAT(x, …)</span><span class="sxs-lookup"><span data-stu-id="cdbad-308">CONCAT(x, …)</span></span> | <span data-ttu-id="cdbad-309">Возвращает строку, являющуюся результатом объединения двух или более строковых значений.</span><span class="sxs-lookup"><span data-stu-id="cdbad-309">Returns a string that is the result of concatenating two or more string values.</span></span> |
| <span data-ttu-id="cdbad-310">LENGTH(x)</span><span class="sxs-lookup"><span data-stu-id="cdbad-310">LENGTH(x)</span></span> | <span data-ttu-id="cdbad-311">Возвращает число символов указанного строкового выражения.</span><span class="sxs-lookup"><span data-stu-id="cdbad-311">Returns the number of characters of the specified string expression.</span></span>|
| <span data-ttu-id="cdbad-312">LOWER(x)</span><span class="sxs-lookup"><span data-stu-id="cdbad-312">LOWER(x)</span></span> | <span data-ttu-id="cdbad-313">Возвращает строковое выражение после преобразования символов верхнего регистра в нижний.</span><span class="sxs-lookup"><span data-stu-id="cdbad-313">Returns a string expression after converting uppercase character data to lowercase.</span></span> |
| <span data-ttu-id="cdbad-314">UPPER(x)</span><span class="sxs-lookup"><span data-stu-id="cdbad-314">UPPER(x)</span></span> | <span data-ttu-id="cdbad-315">Возвращает строковое выражение после преобразования символов нижнего регистра в верхний.</span><span class="sxs-lookup"><span data-stu-id="cdbad-315">Returns a string expression after converting lowercase character data to uppercase.</span></span> |
| <span data-ttu-id="cdbad-316">SUBSTRING(строка, начало[, длина])</span><span class="sxs-lookup"><span data-stu-id="cdbad-316">SUBSTRING(string, start [, length])</span></span> | <span data-ttu-id="cdbad-317">Возвращает часть строкового выражения, начиная с указанной позиции (отсчет начинается с нуля) и до достижения указанной длины (или до конца строки).</span><span class="sxs-lookup"><span data-stu-id="cdbad-317">Returns part of a string expression starting at the specified character zero-based position and continues to the specified length, or to the end of the string.</span></span> |
| <span data-ttu-id="cdbad-318">INDEX_OF(строка, фрагмент)</span><span class="sxs-lookup"><span data-stu-id="cdbad-318">INDEX_OF(string, fragment)</span></span> | <span data-ttu-id="cdbad-319">Возвращает начальную позицию первого вхождения второго строкового выражения в первое указанное строковое выражение или –1, если строка не найдена.</span><span class="sxs-lookup"><span data-stu-id="cdbad-319">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span></span>|
| <span data-ttu-id="cdbad-320">STARTS_WITH(x, y)</span><span class="sxs-lookup"><span data-stu-id="cdbad-320">STARTS_WITH(x, y)</span></span> | <span data-ttu-id="cdbad-321">Возвращает значение логического типа, указывающее, начинается ли первое строковое выражение вторым.</span><span class="sxs-lookup"><span data-stu-id="cdbad-321">Returns a Boolean indicating whether the first string expression starts with the second.</span></span> |
| <span data-ttu-id="cdbad-322">ENDS_WITH(x, y)</span><span class="sxs-lookup"><span data-stu-id="cdbad-322">ENDS_WITH(x, y)</span></span> | <span data-ttu-id="cdbad-323">Возвращает значение логического типа, указывающее, заканчивается ли первое строковое выражение вторым.</span><span class="sxs-lookup"><span data-stu-id="cdbad-323">Returns a Boolean indicating whether the first string expression ends with the second.</span></span> |
| <span data-ttu-id="cdbad-324">CONTAINS(x,y)</span><span class="sxs-lookup"><span data-stu-id="cdbad-324">CONTAINS(x,y)</span></span> | <span data-ttu-id="cdbad-325">Возвращает значение логического типа, указывающее, содержит ли первое строковое выражение второе.</span><span class="sxs-lookup"><span data-stu-id="cdbad-325">Returns a Boolean indicating whether the first string expression contains the second.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="cdbad-326">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cdbad-326">Next steps</span></span>
<span data-ttu-id="cdbad-327">Узнайте, как выполнять запросы в своих приложениях с помощью [пакетов SDK для Azure IoT][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="cdbad-327">Learn how to execute queries in your apps using [Azure IoT SDKs][lnk-hub-sdks].</span></span>

[lnk-query-where]: iot-hub-devguide-query-language.md#where-clause
[lnk-query-expressions]: iot-hub-devguide-query-language.md#expressions-and-conditions
[lnk-query-getstarted]: iot-hub-devguide-query-language.md#get-started-with-device-twin-queries

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-devguide-messaging-routes]: iot-hub-devguide-messages-read-custom.md
[lnk-devguide-messaging-format]: iot-hub-devguide-messages-construct.md
[lnk-devguide-messaging-routes]: ./iot-hub-devguide-messages-read-custom.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
