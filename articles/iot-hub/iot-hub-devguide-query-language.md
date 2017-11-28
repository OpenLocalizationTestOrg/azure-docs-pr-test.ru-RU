---
title: "hello aaaUnderstand язык запросов центр IoT Azure | Документы Microsoft"
description: "Руководство разработчика по - описание языка запросов SQL-подобного центра IoT hello используется tooretrieve сведения об устройстве близнецы и заданиях из вашего центра IoT."
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
ms.openlocfilehash: 01a7c8ffdf44c6c27b834739d02c8fef1dd3d3fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-query-language-for-device-twins-jobs-and-message-routing"></a><span data-ttu-id="12aba-103">Справочник — язык запросов Центра Интернета вещей для двойников устройств, заданий и маршрутизации сообщений</span><span class="sxs-lookup"><span data-stu-id="12aba-103">Reference - IoT Hub query language for device twins, jobs, and message routing</span></span>

<span data-ttu-id="12aba-104">Центр IoT сведения tooretrieve мощный язык SQL-подобного в отношении [близнецы устройства] [ lnk-twins] и [заданий][lnk-jobs]и [Маршрутизация сообщений][lnk-devguide-messaging-routes].</span><span class="sxs-lookup"><span data-stu-id="12aba-104">IoT Hub provides a powerful SQL-like language tooretrieve information regarding [device twins][lnk-twins] and [jobs][lnk-jobs], and [message routing][lnk-devguide-messaging-routes].</span></span> <span data-ttu-id="12aba-105">В этой статье представлены:</span><span class="sxs-lookup"><span data-stu-id="12aba-105">This article presents:</span></span>

* <span data-ttu-id="12aba-106">Введение toohello основные функции hello центра IoT язык запросов, и</span><span class="sxs-lookup"><span data-stu-id="12aba-106">An introduction toohello major features of hello IoT Hub query language, and</span></span>
* <span data-ttu-id="12aba-107">Hello подробное описание языка hello.</span><span class="sxs-lookup"><span data-stu-id="12aba-107">hello detailed description of hello language.</span></span>

## <a name="get-started-with-device-twin-queries"></a><span data-ttu-id="12aba-108">Начало работы с запросами двойника устройства</span><span class="sxs-lookup"><span data-stu-id="12aba-108">Get started with device twin queries</span></span>
<span data-ttu-id="12aba-109">[Двойники устройств][lnk-twins] могут содержать произвольные объекты JSON в качестве тегов и свойств.</span><span class="sxs-lookup"><span data-stu-id="12aba-109">[Device twins][lnk-twins] can contain arbitrary JSON objects as both tags and properties.</span></span> <span data-ttu-id="12aba-110">Центр IoT позволяет близнецы tooquery устройства как единый документ JSON, содержащий все сведения об устройстве двойных.</span><span class="sxs-lookup"><span data-stu-id="12aba-110">IoT Hub enables you tooquery device twins as a single JSON document containing all device twin information.</span></span>
<span data-ttu-id="12aba-111">Предполагается, для экземпляра, что ваш близнецы устройство концентратора IoT hello следующие структуры:</span><span class="sxs-lookup"><span data-stu-id="12aba-111">Assume, for instance, that your IoT hub device twins have hello following structure:</span></span>

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

<span data-ttu-id="12aba-112">Центр IoT предоставляет близнецы устройства hello в виде документа коллекцию с именем **устройств**.</span><span class="sxs-lookup"><span data-stu-id="12aba-112">IoT Hub exposes hello device twins as a document collection called **devices**.</span></span>
<span data-ttu-id="12aba-113">Поэтому приветствия при следующем запросе извлекает hello весь набор близнецы устройства:</span><span class="sxs-lookup"><span data-stu-id="12aba-113">So hello following query retrieves hello whole set of device twins:</span></span>

```sql
SELECT * FROM devices
```

> [!NOTE]
> <span data-ttu-id="12aba-114">[Пакеты SDK для Azure IoT][lnk-hub-sdks] поддерживают разбивку на страницы объемных результатов.</span><span class="sxs-lookup"><span data-stu-id="12aba-114">[Azure IoT SDKs][lnk-hub-sdks] support paging of large results.</span></span>

<span data-ttu-id="12aba-115">Центр IoT позволяет близнецы устройства tooretrieve произвольный условиям фильтрации.</span><span class="sxs-lookup"><span data-stu-id="12aba-115">IoT Hub allows you tooretrieve device twins filtering with arbitrary conditions.</span></span> <span data-ttu-id="12aba-116">Например,</span><span class="sxs-lookup"><span data-stu-id="12aba-116">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
```

<span data-ttu-id="12aba-117">Извлекает hello близнецы устройства с hello **location.region** пара тегов слишком**США**.</span><span class="sxs-lookup"><span data-stu-id="12aba-117">retrieves hello device twins with hello **location.region** tag set too**US**.</span></span>
<span data-ttu-id="12aba-118">Кроме того, поддерживаются логические операторы и арифметические сравнения. Например,</span><span class="sxs-lookup"><span data-stu-id="12aba-118">Boolean operators and arithmetic comparisons are supported as well, for example</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
    AND properties.reported.telemetryConfig.sendFrequencyInSecs >= 60
```

<span data-ttu-id="12aba-119">Извлекает все устройства близнецы, расположенный в hello нам настроен toosend телеметрии меньше часто каждую минуту.</span><span class="sxs-lookup"><span data-stu-id="12aba-119">retrieves all device twins located in hello US configured toosend telemetry less often than every minute.</span></span> <span data-ttu-id="12aba-120">Для удобства можно также константы массива возможных toouse с hello **в** и **NIN** операторы (не в).</span><span class="sxs-lookup"><span data-stu-id="12aba-120">As a convenience, it is also possible toouse array constants with hello **IN** and **NIN** (not in) operators.</span></span> <span data-ttu-id="12aba-121">Например,</span><span class="sxs-lookup"><span data-stu-id="12aba-121">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE properties.reported.connectivity IN ['wired', 'wifi']
```

<span data-ttu-id="12aba-122">извлекает все двойники устройств, сообщившие о подключении по Wi-Fi или проводной сети.</span><span class="sxs-lookup"><span data-stu-id="12aba-122">retrieves all device twins that reported WiFi or wired connectivity.</span></span> <span data-ttu-id="12aba-123">Он является зачастую необходимо tooidentify все близнецы устройств, содержащих определенное свойство.</span><span class="sxs-lookup"><span data-stu-id="12aba-123">It is often necessary tooidentify all device twins that contain a specific property.</span></span> <span data-ttu-id="12aba-124">Центр IoT поддерживает функции hello `is_defined()` для этой цели.</span><span class="sxs-lookup"><span data-stu-id="12aba-124">IoT Hub supports hello function `is_defined()` for this purpose.</span></span> <span data-ttu-id="12aba-125">Например,</span><span class="sxs-lookup"><span data-stu-id="12aba-125">For instance,</span></span>

```SQL
SELECT * FROM devices
WHERE is_defined(properties.reported.connectivity)
```

<span data-ttu-id="12aba-126">получить все близнецы устройств, определяющие hello `connectivity` сообщил свойство.</span><span class="sxs-lookup"><span data-stu-id="12aba-126">retrieved all device twins that define hello `connectivity` reported property.</span></span> <span data-ttu-id="12aba-127">См. toohello [предложение WHERE] [ lnk-query-where] раздел для полной ссылки hello hello возможности фильтрации.</span><span class="sxs-lookup"><span data-stu-id="12aba-127">Refer toohello [WHERE clause][lnk-query-where] section for hello full reference of hello filtering capabilities.</span></span>

<span data-ttu-id="12aba-128">Кроме того, поддерживаются группирование и агрегаты.</span><span class="sxs-lookup"><span data-stu-id="12aba-128">Grouping and aggregations are also supported.</span></span> <span data-ttu-id="12aba-129">Например,</span><span class="sxs-lookup"><span data-stu-id="12aba-129">For instance,</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="12aba-130">Возвращает состояние конфигурации каждого телеметрии hello число устройств hello.</span><span class="sxs-lookup"><span data-stu-id="12aba-130">returns hello count of hello devices in each telemetry configuration status.</span></span>

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

<span data-ttu-id="12aba-131">Hello предыдущий пример иллюстрирует ситуацию, где три устройства подтверждать успешной настройки двух применение конфигурации hello и один сообщил об ошибке.</span><span class="sxs-lookup"><span data-stu-id="12aba-131">hello preceding example illustrates a situation where three devices reported successful configuration, two are still applying hello configuration, and one reported an error.</span></span>

### <a name="c-example"></a><span data-ttu-id="12aba-132">Пример C#</span><span class="sxs-lookup"><span data-stu-id="12aba-132">C# example</span></span>
<span data-ttu-id="12aba-133">функции запросов Hello предоставляется hello [службу C# SDK] [ lnk-hub-sdks] в hello **RegistryManager** класса.</span><span class="sxs-lookup"><span data-stu-id="12aba-133">hello query functionality is exposed by hello [C# service SDK][lnk-hub-sdks] in hello **RegistryManager** class.</span></span>
<span data-ttu-id="12aba-134">Ниже приведен пример простого запроса:</span><span class="sxs-lookup"><span data-stu-id="12aba-134">Here is an example of a simple query:</span></span>

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

<span data-ttu-id="12aba-135">Обратите внимание, каким образом hello **запроса** создается с размер страницы (вверх too1000) и затем можно получить несколько страниц с вызывающему Привет **GetNextAsTwinAsync** методы несколько раз.</span><span class="sxs-lookup"><span data-stu-id="12aba-135">Note how hello **query** object is instantiated with a page size (up too1000), and then multiple pages can be retrieved by calling hello **GetNextAsTwinAsync** methods multiple times.</span></span>
<span data-ttu-id="12aba-136">Примечание hello объекта запроса предоставляет доступ к нескольким **Далее\***, в зависимости от предусмотренного hello запроса, таких как объекты устройств двойных или задания параметр десериализации hello или обычный toobe JSON при использовании проекций.</span><span class="sxs-lookup"><span data-stu-id="12aba-136">Note that hello query object exposes multiple **Next\***, depending on hello deserialization option required by hello query, such as device twin or job objects, or plain JSON toobe used when using projections.</span></span>

### <a name="nodejs-example"></a><span data-ttu-id="12aba-137">Пример для Node.js</span><span class="sxs-lookup"><span data-stu-id="12aba-137">Node.js example</span></span>
<span data-ttu-id="12aba-138">функции запросов Hello предоставляется hello [службы Azure IoT SDK для Node.js] [ lnk-hub-sdks] в hello **реестра** объекта.</span><span class="sxs-lookup"><span data-stu-id="12aba-138">hello query functionality is exposed by hello [Azure IoT service SDK for Node.js][lnk-hub-sdks] in hello **Registry** object.</span></span>
<span data-ttu-id="12aba-139">Ниже приведен пример простого запроса:</span><span class="sxs-lookup"><span data-stu-id="12aba-139">Here is an example of a simple query:</span></span>

```nodejs
var query = registry.createQuery('SELECT * FROM devices', 100);
var onResults = function(err, results) {
    if (err) {
        console.error('Failed toofetch hello results: ' + err.message);
    } else {
        // Do something with hello results
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

<span data-ttu-id="12aba-140">Обратите внимание, каким образом hello **запроса** создается с размер страницы (вверх too1000) и затем можно получить несколько страниц с вызывающему Привет **nextAsTwin** методы несколько раз.</span><span class="sxs-lookup"><span data-stu-id="12aba-140">Note how hello **query** object is instantiated with a page size (up too1000), and then multiple pages can be retrieved by calling hello **nextAsTwin** methods multiple times.</span></span>
<span data-ttu-id="12aba-141">Примечание hello объекта запроса предоставляет доступ к нескольким **Далее\***, в зависимости от предусмотренного hello запроса, таких как объекты устройств двойных или задания параметр десериализации hello или обычный toobe JSON при использовании проекций.</span><span class="sxs-lookup"><span data-stu-id="12aba-141">Note that hello query object exposes multiple **next\***, depending on hello deserialization option required by hello query, such as device twin or job objects, or plain JSON toobe used when using projections.</span></span>

### <a name="limitations"></a><span data-ttu-id="12aba-142">Ограничения</span><span class="sxs-lookup"><span data-stu-id="12aba-142">Limitations</span></span>
> [!IMPORTANT]
> <span data-ttu-id="12aba-143">Результаты запроса могут иметь несколько минут задержки с учетом toohello последние значения в близнецы устройства.</span><span class="sxs-lookup"><span data-stu-id="12aba-143">Query results can have a few minutes of delay with respect toohello latest values in device twins.</span></span> <span data-ttu-id="12aba-144">Если запросы к близнецы отдельное устройство по идентификатору, его всегда является предпочтительным toouse hello извлечения устройства двойных API, который всегда содержит последние значения hello и имеет выше регулирование пределы.</span><span class="sxs-lookup"><span data-stu-id="12aba-144">If querying individual device twins by id, it is always preferable toouse hello retrieve device twin API, which always contains hello latest values and has higher throttling limits.</span></span>

<span data-ttu-id="12aba-145">В настоящее время сравнения поддерживаются только между типами-примитивами (не объектами), например, `... WHERE properties.desired.config = properties.reported.config` поддерживается только в том случае, если эти свойства имеют примитивные значения.</span><span class="sxs-lookup"><span data-stu-id="12aba-145">Currently, comparisons are supported only between primitive types (no objects), for instance `... WHERE properties.desired.config = properties.reported.config` is supported only if those properties have primitive values.</span></span>

## <a name="get-started-with-jobs-queries"></a><span data-ttu-id="12aba-146">Начало работы с запросами заданий</span><span class="sxs-lookup"><span data-stu-id="12aba-146">Get started with jobs queries</span></span>
<span data-ttu-id="12aba-147">[Задания] [ lnk-jobs] предоставляют tooexecute способом операции на наборы устройств.</span><span class="sxs-lookup"><span data-stu-id="12aba-147">[Jobs][lnk-jobs] provide a way tooexecute operations on sets of devices.</span></span> <span data-ttu-id="12aba-148">Каждый двойных устройства сведениями hello hello заданий, из которых он входит в коллекцию с именем **задания**.</span><span class="sxs-lookup"><span data-stu-id="12aba-148">Each device twin contains hello information of hello jobs of which it is part in a collection called **jobs**.</span></span>
<span data-ttu-id="12aba-149">Логически получается следующее:</span><span class="sxs-lookup"><span data-stu-id="12aba-149">Logically,</span></span>

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

<span data-ttu-id="12aba-150">В настоящее время эта коллекция поддерживает запросы как **devices.jobs** в hello центра IoT язык запросов.</span><span class="sxs-lookup"><span data-stu-id="12aba-150">Currently, this collection is queryable as **devices.jobs** in hello IoT Hub query language.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="12aba-151">В настоящее время hello свойства задания никогда не возвращается при запросе близнецы устройства (запросы, содержащих «с устройств»).</span><span class="sxs-lookup"><span data-stu-id="12aba-151">Currently, hello jobs property is never returned when querying device twins (that is, queries that contains 'FROM devices').</span></span> <span data-ttu-id="12aba-152">Доступ к нему можно получить только непосредственно с помощью запросов, использующих `FROM devices.jobs`.</span><span class="sxs-lookup"><span data-stu-id="12aba-152">It can only be accessed directly with queries using `FROM devices.jobs`.</span></span>
>
>

<span data-ttu-id="12aba-153">Например, tooget все задания (последние и запланированные), влияющих на отдельном устройстве, можно использовать приветствия при следующем запросе:</span><span class="sxs-lookup"><span data-stu-id="12aba-153">For instance, tooget all jobs (past and scheduled) that affect a single device, you can use hello following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
```

<span data-ttu-id="12aba-154">Обратите внимание на то, как этот запрос предоставляет hello конкретного устройства состояние каждого задания возвращается (и, возможно hello прямой метод ответа).</span><span class="sxs-lookup"><span data-stu-id="12aba-154">Note how this query provides hello device-specific status (and possibly hello direct method response) of each job returned.</span></span>
<span data-ttu-id="12aba-155">Это также возможно toofilter с произвольной логических условий для всех свойств объекта в hello **devices.jobs** коллекции.</span><span class="sxs-lookup"><span data-stu-id="12aba-155">It is also possible toofilter with arbitrary Boolean conditions on all object properties in hello **devices.jobs** collection.</span></span>
<span data-ttu-id="12aba-156">Например hello следующий запрос:</span><span class="sxs-lookup"><span data-stu-id="12aba-156">For instance, hello following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
    AND devices.jobs.jobType = 'scheduleTwinUpdate'
    AND devices.jobs.status = 'completed'
    AND devices.jobs.createdTimeUtc > '2016-09-01'
```

<span data-ttu-id="12aba-157">получает список всех завершенных заданий обновления двойников устройств для устройства **myDeviceId**, созданных после сентября 2016 года.</span><span class="sxs-lookup"><span data-stu-id="12aba-157">retrieves all completed device twin update jobs for device **myDeviceId** that were created after September 2016.</span></span>

<span data-ttu-id="12aba-158">Это также tooretrieve возможные результаты на устройство hello одним заданием.</span><span class="sxs-lookup"><span data-stu-id="12aba-158">It is also possible tooretrieve hello per-device outcomes of a single job.</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.jobId = 'myJobId'
```

### <a name="limitations"></a><span data-ttu-id="12aba-159">Ограничения</span><span class="sxs-lookup"><span data-stu-id="12aba-159">Limitations</span></span>
<span data-ttu-id="12aba-160">В настоящее время запросы к **devices.jobs** не поддерживают следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="12aba-160">Currently, queries on **devices.jobs** do not support:</span></span>

* <span data-ttu-id="12aba-161">проекции, поэтому можно использовать только `SELECT *`;</span><span class="sxs-lookup"><span data-stu-id="12aba-161">Projections, therefore only `SELECT *` is possible.</span></span>
* <span data-ttu-id="12aba-162">Условия, которые ссылаются двойных toohello устройства в свойствах toojob сложения (см. раздел hello предшествующий раздела).</span><span class="sxs-lookup"><span data-stu-id="12aba-162">Conditions that refer toohello device twin in addition toojob properties (see hello preceding section).</span></span>
* <span data-ttu-id="12aba-163">выполняемые агрегаты, например count, avg, group by.</span><span class="sxs-lookup"><span data-stu-id="12aba-163">Performing aggregations, such as count, avg, group by.</span></span>

## <a name="get-started-with-device-to-cloud-message-routes-query-expressions"></a><span data-ttu-id="12aba-164">Начало работы с выражениями запросов по маршрутам сообщений, отправляемых с устройства в облако</span><span class="sxs-lookup"><span data-stu-id="12aba-164">Get started with device-to-cloud message routes query expressions</span></span>

<span data-ttu-id="12aba-165">С помощью [маршруты устройства в облако][lnk-devguide-messaging-routes], можно настроить центр IoT toodispatch устройства в облако сообщений toodifferent конечные точки на основе выражений, оцениваются на отдельных сообщений.</span><span class="sxs-lookup"><span data-stu-id="12aba-165">Using [device-to-cloud routes][lnk-devguide-messaging-routes], you can configure IoT Hub toodispatch device-to-cloud messages toodifferent endpoints based on expressions evaluated against individual messages.</span></span>

<span data-ttu-id="12aba-166">маршрут Hello [условие] [ lnk-query-expressions] использует hello же язык запросов центр IoT в качестве условий в запросах двойных и задания.</span><span class="sxs-lookup"><span data-stu-id="12aba-166">hello route [condition][lnk-query-expressions] uses hello same IoT Hub query language as conditions in twin and job queries.</span></span> <span data-ttu-id="12aba-167">Маршрут условий в заголовки сообщений hello и текст.</span><span class="sxs-lookup"><span data-stu-id="12aba-167">Route conditions are evaluated on hello message headers and body.</span></span> <span data-ttu-id="12aba-168">Маршрутизации запроса выражение может включать только заголовки сообщений, но только тела сообщения hello, или заголовки сообщения и тело сообщения.</span><span class="sxs-lookup"><span data-stu-id="12aba-168">Your routing query expression may involve only message headers, only hello message body, or both message headers and message body.</span></span> <span data-ttu-id="12aba-169">Центр IoT предполагается определенной схеме hello заголовки и текст сообщения в порядке tooroute сообщений и hello в следующих разделах описываются требования для центра IoT tooproperly маршрута:</span><span class="sxs-lookup"><span data-stu-id="12aba-169">IoT Hub assumes a specific schema for hello headers and message body in order tooroute messages, and hello following sections describe what is required for IoT Hub tooproperly route:</span></span>

### <a name="routing-on-message-headers"></a><span data-ttu-id="12aba-170">Маршрутизация по заголовкам сообщений</span><span class="sxs-lookup"><span data-stu-id="12aba-170">Routing on message headers</span></span>

<span data-ttu-id="12aba-171">Центр IoT предполагается следующий JSON-представление заголовков сообщений для маршрутизации сообщений hello.</span><span class="sxs-lookup"><span data-stu-id="12aba-171">IoT Hub assumes hello following JSON representation of message headers for message routing:</span></span>

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

<span data-ttu-id="12aba-172">Системные свойства сообщения имеют префикс hello `'$'` символов.</span><span class="sxs-lookup"><span data-stu-id="12aba-172">Message system properties are prefixed with hello `'$'` symbol.</span></span>
<span data-ttu-id="12aba-173">Доступ к пользовательским свойствам всегда осуществляется с использованием их имен.</span><span class="sxs-lookup"><span data-stu-id="12aba-173">User properties are always accessed with their name.</span></span> <span data-ttu-id="12aba-174">Если имя свойства пользователя происходит toocoincide с системного свойства (такие как `$to`), свойство hello пользователя будут извлечены с hello `$to` выражение.</span><span class="sxs-lookup"><span data-stu-id="12aba-174">If a user property name happens toocoincide with a system property (such as `$to`), hello user property will be retrieved with hello `$to` expression.</span></span>
<span data-ttu-id="12aba-175">Вы всегда можете открыть Свойства системы hello квадратными скобками `{}`: например, можно использовать выражение hello `{$to}` tooaccess hello системное свойство `to`.</span><span class="sxs-lookup"><span data-stu-id="12aba-175">You can always access hello system property using brackets `{}`: for instance, you can use hello expression `{$to}` tooaccess hello system property `to`.</span></span> <span data-ttu-id="12aba-176">Имена свойств в квадратных скобках всегда получают hello соответствующего свойства системы.</span><span class="sxs-lookup"><span data-stu-id="12aba-176">Bracketed property names always retrieve hello corresponding system property.</span></span>

<span data-ttu-id="12aba-177">Не забывайте, что в именах свойств не учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="12aba-177">Remember that property names are case insensitive.</span></span>

> [!NOTE]
> <span data-ttu-id="12aba-178">Все свойства сообщения являются строками.</span><span class="sxs-lookup"><span data-stu-id="12aba-178">All message properties are strings.</span></span> <span data-ttu-id="12aba-179">Системные свойства, как описано в hello [руководстве разработчика][lnk-devguide-messaging-format], в настоящий момент не доступны toouse в запросах.</span><span class="sxs-lookup"><span data-stu-id="12aba-179">System properties, as described in hello [developer guide][lnk-devguide-messaging-format], are currently not available toouse in queries.</span></span>
>

<span data-ttu-id="12aba-180">Например, если вы используете `messageType` свойства, может потребоваться tooroute все данные телеметрии tooone и все оповещения tooanother конечная.</span><span class="sxs-lookup"><span data-stu-id="12aba-180">For example, if you use a `messageType` property, you might want tooroute all telemetry tooone endpoint, and all alerts tooanother endpoint.</span></span> <span data-ttu-id="12aba-181">Можно написать следующие выражения tooroute hello телеметрии hello:</span><span class="sxs-lookup"><span data-stu-id="12aba-181">You can write hello following expression tooroute hello telemetry:</span></span>

```sql
messageType = 'telemetry'
```

<span data-ttu-id="12aba-182">И hello следующие выражения tooroute hello предупреждающих сообщений.</span><span class="sxs-lookup"><span data-stu-id="12aba-182">And hello following expression tooroute hello alert messages:</span></span>

```sql
messageType = 'alert'
```

<span data-ttu-id="12aba-183">Также поддерживаются логические выражения и функции.</span><span class="sxs-lookup"><span data-stu-id="12aba-183">Boolean expressions and functions are also supported.</span></span> <span data-ttu-id="12aba-184">Эта функция позволяет toodistinguish между уровень серьезности, например:</span><span class="sxs-lookup"><span data-stu-id="12aba-184">This feature enables you toodistinguish between severity level, for example:</span></span>

```sql
messageType = 'alerts' AND as_number(severity) <= 2
```

<span data-ttu-id="12aba-185">См. toohello [выражений и условий] [ lnk-query-expressions] раздел hello полный список поддерживаемых операторов и функций.</span><span class="sxs-lookup"><span data-stu-id="12aba-185">Refer toohello [Expression and conditions][lnk-query-expressions] section for hello full list of supported operators and functions.</span></span>

### <a name="routing-on-message-bodies"></a><span data-ttu-id="12aba-186">Маршрутизация по тексту сообщений</span><span class="sxs-lookup"><span data-stu-id="12aba-186">Routing on message bodies</span></span>

<span data-ttu-id="12aba-187">Центр IoT только маршрутизацию на основе тела сообщения содержимое, если текст сообщения hello правильно сформированный JSON в кодировке UTF-8, UTF-16 или UTF-32.</span><span class="sxs-lookup"><span data-stu-id="12aba-187">IoT Hub can only route based on message body contents if hello message body is properly formed JSON encoded in either UTF-8, UTF-16, or UTF-32.</span></span> <span data-ttu-id="12aba-188">Необходимо задать тип содержимого hello приветственное сообщение слишком`application/json` и hello содержимого кодировки tooone hello поддерживается кодировки UTF в tooallow заголовки сообщений hello, центр IoT tooroute приветственное сообщение в зависимости от содержимого текста hello.</span><span class="sxs-lookup"><span data-stu-id="12aba-188">You must set hello content type of hello message too`application/json` and hello content encoding tooone of hello supported UTF encodings in hello message headers tooallow IoT Hub tooroute hello message based on hello body contents.</span></span> <span data-ttu-id="12aba-189">Если один из заголовков hello не указан, центр IoT не будет tooevaluate любое выражение запроса, включающие текст hello от приветственное сообщение.</span><span class="sxs-lookup"><span data-stu-id="12aba-189">If either of hello headers is not specified, IoT Hub will not attempt tooevaluate any query expression involving hello body against hello message.</span></span> <span data-ttu-id="12aba-190">Если сообщение не является сообщением JSON или приветственное сообщение не указывает тип содержимого hello и кодировку содержимого, по-прежнему может использовать сообщение hello tooroute на основании заголовков сообщений hello Маршрутизация сообщений.</span><span class="sxs-lookup"><span data-stu-id="12aba-190">If your message is not a JSON message, or if hello message does not specify hello content type and content encoding, you may still use message routing tooroute hello message based on hello message headers.</span></span>

<span data-ttu-id="12aba-191">Можно использовать `$body` в сообщение hello tooroute выражение запроса hello.</span><span class="sxs-lookup"><span data-stu-id="12aba-191">You can use `$body` in hello query expression tooroute hello message.</span></span> <span data-ttu-id="12aba-192">Простой текст ссылки, ссылка на массив текст или несколько ссылок на текст можно использовать в выражении запроса hello.</span><span class="sxs-lookup"><span data-stu-id="12aba-192">You can use a simple body reference, body array reference, or multiple body references in hello query expression.</span></span> <span data-ttu-id="12aba-193">В выражении запроса можно также указывать сочетание ссылки на текст со ссылкой на заголовок сообщения.</span><span class="sxs-lookup"><span data-stu-id="12aba-193">Your query expression can also combine a body reference with a message header reference.</span></span> <span data-ttu-id="12aba-194">Например hello ниже приведены допустимые выражения.</span><span class="sxs-lookup"><span data-stu-id="12aba-194">For example, hello following are all valid query expressions:</span></span>

```sql
$body.message.Weather.Location.State = 'WA'
$body.Weather.HistoricalData[0].Month = 'Feb'
$body.Weather.Temperature = 50 AND $body.message.Weather.IsEnabled
length($body.Weather.Location.State) = 2
$body.Weather.Temperature = 50 AND Status = 'Active'
```

## <a name="basics-of-an-iot-hub-query"></a><span data-ttu-id="12aba-195">Основные сведения о запросе Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="12aba-195">Basics of an IoT Hub query</span></span>
<span data-ttu-id="12aba-196">Каждый запрос Центра Интернета вещей состоит из предложений SELECT и FROM, а также необязательных предложений WHERE и GROUP BY.</span><span class="sxs-lookup"><span data-stu-id="12aba-196">Every IoT Hub query consists of a SELECT and FROM clauses and by optional WHERE and GROUP BY clauses.</span></span> <span data-ttu-id="12aba-197">Каждый запрос выполняется для коллекции документов JSON, например двойников устройств.</span><span class="sxs-lookup"><span data-stu-id="12aba-197">Every query is run on a collection of JSON documents, for example device twins.</span></span> <span data-ttu-id="12aba-198">Hello предложение FROM указывает hello документа коллекции toobe итерация на (**устройств** или **devices.jobs**).</span><span class="sxs-lookup"><span data-stu-id="12aba-198">hello FROM clause indicates hello document collection toobe iterated on (**devices** or **devices.jobs**).</span></span> <span data-ttu-id="12aba-199">Затем hello hello, ГДЕ применяется предложение фильтра.</span><span class="sxs-lookup"><span data-stu-id="12aba-199">Then, hello filter in hello WHERE clause is applied.</span></span> <span data-ttu-id="12aba-200">С агрегаты, а результаты этого шага hello группируются как hello указано в предложении GROUP BY, и для каждой группы формируется строку как указано в предложении SELECT hello.</span><span class="sxs-lookup"><span data-stu-id="12aba-200">With aggregations, hello results of this step are grouped as specified in hello GROUP BY clause and, for each group, a row is generated as specified in hello SELECT clause.</span></span>

```sql
SELECT <select_list>
FROM <from_specification>
[WHERE <filter_condition>]
[GROUP BY <group_specification>]
```

## <a name="from-clause"></a><span data-ttu-id="12aba-201">Предложение FROM</span><span class="sxs-lookup"><span data-stu-id="12aba-201">FROM clause</span></span>
<span data-ttu-id="12aba-202">Hello **из < from_specification >** предложение можно предположить только два значения: **с устройств**, близнецы tooquery устройство, или **из devices.jobs**, tooquery задания на устройство Подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="12aba-202">hello **FROM <from_specification>** clause can assume only two values: **FROM devices**, tooquery device twins, or **FROM devices.jobs**, tooquery job per-device details.</span></span>

## <a name="where-clause"></a><span data-ttu-id="12aba-203">Предложение WHERE</span><span class="sxs-lookup"><span data-stu-id="12aba-203">WHERE clause</span></span>
<span data-ttu-id="12aba-204">Hello **ГДЕ < filter_condition >** предложение является необязательным.</span><span class="sxs-lookup"><span data-stu-id="12aba-204">hello **WHERE <filter_condition>** clause is optional.</span></span> <span data-ttu-id="12aba-205">Указывает одно или несколько условий, которым hello документов JSON в коллекции hello FROM должны удовлетворять toobe включается как часть результата hello.</span><span class="sxs-lookup"><span data-stu-id="12aba-205">It specifies one or more conditions that hello JSON documents in hello FROM collection must satisfy toobe included as part of hello result.</span></span> <span data-ttu-id="12aba-206">Любой документ JSON должно быть указано hello условия слишком «true» toobe включается в результат hello.</span><span class="sxs-lookup"><span data-stu-id="12aba-206">Any JSON document must evaluate hello specified conditions too"true" toobe included in hello result.</span></span>

<span data-ttu-id="12aba-207">Допускается Hello условия, описанные в разделе [выражений и условий][lnk-query-expressions].</span><span class="sxs-lookup"><span data-stu-id="12aba-207">hello allowed conditions are described in section [Expressions and conditions][lnk-query-expressions].</span></span>

## <a name="select-clause"></a><span data-ttu-id="12aba-208">Предложение SELECT</span><span class="sxs-lookup"><span data-stu-id="12aba-208">SELECT clause</span></span>
<span data-ttu-id="12aba-209">предложение SELECT Hello (**ВЫБЕРИТЕ < select_list >**) является обязательным и указывает, какие значения извлекаются из запроса hello.</span><span class="sxs-lookup"><span data-stu-id="12aba-209">hello SELECT clause (**SELECT <select_list>**) is mandatory and specifies what values are retrieved from hello query.</span></span> <span data-ttu-id="12aba-210">Он указывает toobe значения JSON hello toogenerate новых объектов JSON.</span><span class="sxs-lookup"><span data-stu-id="12aba-210">It specifies hello JSON values toobe used toogenerate new JSON objects.</span></span>
<span data-ttu-id="12aba-211">Для каждого элемента Здравствуйте отфильтрованные (и при необходимости сгруппированные) подмножеством hello FROM коллекции, этап отображения hello создает новый объект JSON, созданные с помощью hello значения, указанные в предложении SELECT hello.</span><span class="sxs-lookup"><span data-stu-id="12aba-211">For each element of hello filtered (and optionally grouped) subset of hello FROM collection, hello projection phase generates a new JSON object, constructed with hello values specified in hello SELECT clause.</span></span>

<span data-ttu-id="12aba-212">Ниже приведен hello грамматики hello предложения SELECT.</span><span class="sxs-lookup"><span data-stu-id="12aba-212">Following is hello grammar of hello SELECT clause:</span></span>

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

<span data-ttu-id="12aba-213">где **attribute_name** ссылается свойство tooany документа JSON hello в коллекции hello FROM.</span><span class="sxs-lookup"><span data-stu-id="12aba-213">where **attribute_name** refers tooany property of hello JSON document in hello FROM collection.</span></span> <span data-ttu-id="12aba-214">Некоторые примеры предложения SELECT можно найти в hello [Приступая к работе с запросами двойных устройства] [ lnk-query-getstarted] раздела.</span><span class="sxs-lookup"><span data-stu-id="12aba-214">Some examples of SELECT clauses can be found in hello [Getting started with device twin queries][lnk-query-getstarted] section.</span></span>

<span data-ttu-id="12aba-215">В настоящее время предложения для осуществления выбора, отличные от **SELECT \***, поддерживаются только в статистических запросах к двойникам устройств.</span><span class="sxs-lookup"><span data-stu-id="12aba-215">Currently, selection clauses different than **SELECT \*** are only supported in aggregate queries on device twins.</span></span>

## <a name="group-by-clause"></a><span data-ttu-id="12aba-216">Предложение GROUP BY</span><span class="sxs-lookup"><span data-stu-id="12aba-216">GROUP BY clause</span></span>
<span data-ttu-id="12aba-217">Hello **GROUP BY < group_specification >** предложение является необязательным элементом, могут быть выполнены после фильтр hello, указан в hello предложение WHERE и перед hello проекции, указанной в hello выбрать.</span><span class="sxs-lookup"><span data-stu-id="12aba-217">hello **GROUP BY <group_specification>** clause is an optional step that can be executed after hello filter specified in hello WHERE clause, and before hello projection specified in hello SELECT.</span></span> <span data-ttu-id="12aba-218">Он группирует документов на основании hello значение атрибута.</span><span class="sxs-lookup"><span data-stu-id="12aba-218">It groups documents based on hello value of an attribute.</span></span> <span data-ttu-id="12aba-219">Эти группы представлены используемые toogenerate суммарный значения, указанные в предложении SELECT hello.</span><span class="sxs-lookup"><span data-stu-id="12aba-219">These groups are used toogenerate aggregated values as specified in hello SELECT clause.</span></span>

<span data-ttu-id="12aba-220">Ниже представлен пример запроса с использованием предложения GROUP BY:</span><span class="sxs-lookup"><span data-stu-id="12aba-220">An example of a query using GROUP BY is:</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="12aba-221">Hello формальных для GROUP BY используется синтаксис:</span><span class="sxs-lookup"><span data-stu-id="12aba-221">hello formal syntax for GROUP BY is:</span></span>

```
GROUP BY <group_by_element>
<group_by_element> :==
    attribute_name
    | < group_by_element > '.' attribute_name
```

<span data-ttu-id="12aba-222">где **attribute_name** ссылается свойство tooany документа JSON hello в коллекции hello FROM.</span><span class="sxs-lookup"><span data-stu-id="12aba-222">where **attribute_name** refers tooany property of hello JSON document in hello FROM collection.</span></span>

<span data-ttu-id="12aba-223">В настоящее время hello предложения GROUP BY поддерживается только при запросе близнецы устройства.</span><span class="sxs-lookup"><span data-stu-id="12aba-223">Currently, hello GROUP BY clause is only supported when querying device twins.</span></span>

## <a name="expressions-and-conditions"></a><span data-ttu-id="12aba-224">Выражения и условия</span><span class="sxs-lookup"><span data-stu-id="12aba-224">Expressions and conditions</span></span>
<span data-ttu-id="12aba-225">В общем *выражение*:</span><span class="sxs-lookup"><span data-stu-id="12aba-225">At a high level, an *expression*:</span></span>

* <span data-ttu-id="12aba-226">Результатом является tooan экземпляр типа JSON (например, логическое значение, число, строка, массив или объект.), и</span><span class="sxs-lookup"><span data-stu-id="12aba-226">Evaluates tooan instance of a JSON type (such as Boolean, number, string, array, or object), and</span></span>
* <span data-ttu-id="12aba-227">Определяется путем обработки данных, поступающих из документа JSON устройства hello и константы, с помощью встроенных операторов и функций.</span><span class="sxs-lookup"><span data-stu-id="12aba-227">Is defined by manipulating data coming from hello device JSON document and constants using built-in operators and functions.</span></span>

<span data-ttu-id="12aba-228">*Условия* , выражений, которые оценивают tooa логическое значение.</span><span class="sxs-lookup"><span data-stu-id="12aba-228">*Conditions* are expressions that evaluate tooa Boolean.</span></span> <span data-ttu-id="12aba-229">Любой другой константой, отличный от Boolean **true** считается **false** (включая **null**, **не определено**, любой экземпляр объекта или массива все строки и четко hello логическое значение **false**).</span><span class="sxs-lookup"><span data-stu-id="12aba-229">Any constant different than Boolean **true** is considered as **false** (including **null**, **undefined**, any object or array instance, any string, and clearly hello Boolean **false**).</span></span>

<span data-ttu-id="12aba-230">Hello для выражения используется синтаксис:</span><span class="sxs-lookup"><span data-stu-id="12aba-230">hello syntax for expressions is:</span></span>

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

<span data-ttu-id="12aba-231">Описание:</span><span class="sxs-lookup"><span data-stu-id="12aba-231">where:</span></span>

| <span data-ttu-id="12aba-232">Знак</span><span class="sxs-lookup"><span data-stu-id="12aba-232">Symbol</span></span> | <span data-ttu-id="12aba-233">Определение</span><span class="sxs-lookup"><span data-stu-id="12aba-233">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="12aba-234">attribute_name</span><span class="sxs-lookup"><span data-stu-id="12aba-234">attribute_name</span></span> | <span data-ttu-id="12aba-235">Любое свойство документа JSON hello в hello **FROM** коллекции.</span><span class="sxs-lookup"><span data-stu-id="12aba-235">Any property of hello JSON document in hello **FROM** collection.</span></span> |
| <span data-ttu-id="12aba-236">binary_operator</span><span class="sxs-lookup"><span data-stu-id="12aba-236">binary_operator</span></span> | <span data-ttu-id="12aba-237">Любого бинарного оператора, перечисленные в hello [операторы](#operators) раздела.</span><span class="sxs-lookup"><span data-stu-id="12aba-237">Any binary operator listed in hello [Operators](#operators) section.</span></span> |
| <span data-ttu-id="12aba-238">function_name</span><span class="sxs-lookup"><span data-stu-id="12aba-238">function_name</span></span>| <span data-ttu-id="12aba-239">Любая функция, перечисленные в hello [функции](#functions) раздела.</span><span class="sxs-lookup"><span data-stu-id="12aba-239">Any function listed in hello [Functions](#functions) section.</span></span> |
| <span data-ttu-id="12aba-240">decimal_literal</span><span class="sxs-lookup"><span data-stu-id="12aba-240">decimal_literal</span></span> |<span data-ttu-id="12aba-241">Число с плавающей запятой в десятичном представлении.</span><span class="sxs-lookup"><span data-stu-id="12aba-241">A float expressed in decimal notation.</span></span> |
| <span data-ttu-id="12aba-242">hexadecimal_literal</span><span class="sxs-lookup"><span data-stu-id="12aba-242">hexadecimal_literal</span></span> |<span data-ttu-id="12aba-243">Число выражен строкой hello, "0 x», за которым следует строка шестнадцатеричных цифр.</span><span class="sxs-lookup"><span data-stu-id="12aba-243">A number expressed by hello string ‘0x’ followed by a string of hexadecimal digits.</span></span> |
| <span data-ttu-id="12aba-244">string_literal</span><span class="sxs-lookup"><span data-stu-id="12aba-244">string_literal</span></span> |<span data-ttu-id="12aba-245">Строковые литералы — это строки Юникода, представленные в виде последовательности из нуля или более знаков Юникода или escape-последовательностей.</span><span class="sxs-lookup"><span data-stu-id="12aba-245">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="12aba-246">Строковые литералы заключаются в одинарные кавычки (апостроф — ') или двойные кавычки (кавычки — ").</span><span class="sxs-lookup"><span data-stu-id="12aba-246">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span> <span data-ttu-id="12aba-247">В знаках Юникода, определяемых 4 шестнадцатеричными цифрами, разрешено использовать escape-символы `\'`, `\"`, `\\` и `\uXXXX`.</span><span class="sxs-lookup"><span data-stu-id="12aba-247">Allowed escapes: `\'`, `\"`, `\\`, `\uXXXX` for Unicode characters defined by 4 hexadecimal digits.</span></span> |

### <a name="operators"></a><span data-ttu-id="12aba-248">Операторы</span><span class="sxs-lookup"><span data-stu-id="12aba-248">Operators</span></span>
<span data-ttu-id="12aba-249">поддерживаются следующие операторы Hello:</span><span class="sxs-lookup"><span data-stu-id="12aba-249">hello following operators are supported:</span></span>

| <span data-ttu-id="12aba-250">Семейство</span><span class="sxs-lookup"><span data-stu-id="12aba-250">Family</span></span> | <span data-ttu-id="12aba-251">Операторы</span><span class="sxs-lookup"><span data-stu-id="12aba-251">Operators</span></span> |
| --- | --- |
| <span data-ttu-id="12aba-252">Арифметические</span><span class="sxs-lookup"><span data-stu-id="12aba-252">Arithmetic</span></span> |<span data-ttu-id="12aba-253">+,-,*,/,%</span><span class="sxs-lookup"><span data-stu-id="12aba-253">+,-,*,/,%</span></span> |
| <span data-ttu-id="12aba-254">Логические</span><span class="sxs-lookup"><span data-stu-id="12aba-254">Logical</span></span> |<span data-ttu-id="12aba-255">AND, OR, NOT</span><span class="sxs-lookup"><span data-stu-id="12aba-255">AND, OR, NOT</span></span> |
| <span data-ttu-id="12aba-256">Сравнение</span><span class="sxs-lookup"><span data-stu-id="12aba-256">Comparison</span></span> |<span data-ttu-id="12aba-257">=, !=, <, >, <=, >=, <></span><span class="sxs-lookup"><span data-stu-id="12aba-257">=, !=, <, >, <=, >=, <></span></span> |

### <a name="functions"></a><span data-ttu-id="12aba-258">Функции</span><span class="sxs-lookup"><span data-stu-id="12aba-258">Functions</span></span>
<span data-ttu-id="12aba-259">При выполнении запроса задания и близнецы hello поддерживается только функция является:</span><span class="sxs-lookup"><span data-stu-id="12aba-259">When querying twins and jobs hello only supported function is:</span></span>

| <span data-ttu-id="12aba-260">Функция</span><span class="sxs-lookup"><span data-stu-id="12aba-260">Function</span></span> | <span data-ttu-id="12aba-261">Описание</span><span class="sxs-lookup"><span data-stu-id="12aba-261">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="12aba-262">IS_DEFINED(Свойство)</span><span class="sxs-lookup"><span data-stu-id="12aba-262">IS_DEFINED(property)</span></span> | <span data-ttu-id="12aba-263">Возвращает логическое значение, указывающее, если свойство hello назначено значение (включая `null`).</span><span class="sxs-lookup"><span data-stu-id="12aba-263">Returns a Boolean indicating if hello property has been assigned a value (including `null`).</span></span> |

<span data-ttu-id="12aba-264">В условиях маршруты поддерживаются следующие математические функции hello.</span><span class="sxs-lookup"><span data-stu-id="12aba-264">In routes conditions, hello following math functions are supported:</span></span>

| <span data-ttu-id="12aba-265">Функция</span><span class="sxs-lookup"><span data-stu-id="12aba-265">Function</span></span> | <span data-ttu-id="12aba-266">Описание</span><span class="sxs-lookup"><span data-stu-id="12aba-266">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="12aba-267">ABS(x)</span><span class="sxs-lookup"><span data-stu-id="12aba-267">ABS(x)</span></span> | <span data-ttu-id="12aba-268">Возвращает hello абсолютное (положительное) значение hello указанного числового выражения.</span><span class="sxs-lookup"><span data-stu-id="12aba-268">Returns hello absolute (positive) value of hello specified numeric expression.</span></span> |
| <span data-ttu-id="12aba-269">EXP(x)</span><span class="sxs-lookup"><span data-stu-id="12aba-269">EXP(x)</span></span> | <span data-ttu-id="12aba-270">Возвращает значение экспоненты hello объекта hello указанного числового выражения (e ^ x).</span><span class="sxs-lookup"><span data-stu-id="12aba-270">Returns hello exponential value of hello specified numeric expression (e^x).</span></span> |
| <span data-ttu-id="12aba-271">POWER(x,y)</span><span class="sxs-lookup"><span data-stu-id="12aba-271">POWER(x,y)</span></span> | <span data-ttu-id="12aba-272">Здравствуйте, возвращает значение указанного hello toohello выражения указанная степень (x ^ y).</span><span class="sxs-lookup"><span data-stu-id="12aba-272">Returns hello value of hello specified expression toohello specified power (x^y).</span></span>|
| <span data-ttu-id="12aba-273">SQUARE(x)</span><span class="sxs-lookup"><span data-stu-id="12aba-273">SQUARE(x)</span></span> | <span data-ttu-id="12aba-274">Квадратный из hello hello возвращает указанное числовое значение.</span><span class="sxs-lookup"><span data-stu-id="12aba-274">Returns hello square of hello specified numeric value.</span></span> |
| <span data-ttu-id="12aba-275">CEILING(x)</span><span class="sxs-lookup"><span data-stu-id="12aba-275">CEILING(x)</span></span> | <span data-ttu-id="12aba-276">Возвращает hello наименьшее целочисленное значение больше или равно, hello указанного числового выражения.</span><span class="sxs-lookup"><span data-stu-id="12aba-276">Returns hello smallest integer value greater than, or equal to, hello specified numeric expression.</span></span> |
| <span data-ttu-id="12aba-277">FLOOR(x)</span><span class="sxs-lookup"><span data-stu-id="12aba-277">FLOOR(x)</span></span> | <span data-ttu-id="12aba-278">Возвращает наибольшее целое число hello меньше или равно toohello указанного числового выражения.</span><span class="sxs-lookup"><span data-stu-id="12aba-278">Returns hello largest integer less than or equal toohello specified numeric expression.</span></span> |
| <span data-ttu-id="12aba-279">SIGN(x)</span><span class="sxs-lookup"><span data-stu-id="12aba-279">SIGN(x)</span></span> | <span data-ttu-id="12aba-280">Здравствуйте, возвращает положительное (+ 1), ноль (0) или отрицательный знак (-1) hello указанного числового выражения.</span><span class="sxs-lookup"><span data-stu-id="12aba-280">Returns hello positive (+1), zero (0), or negative (-1) sign of hello specified numeric expression.</span></span>|
| <span data-ttu-id="12aba-281">SQRT(x)</span><span class="sxs-lookup"><span data-stu-id="12aba-281">SQRT(x)</span></span> | <span data-ttu-id="12aba-282">Квадратный из hello hello возвращает указанное числовое значение.</span><span class="sxs-lookup"><span data-stu-id="12aba-282">Returns hello square of hello specified numeric value.</span></span> |

<span data-ttu-id="12aba-283">В условиях маршруты hello после типа, проверка и приведение функции поддерживаются:</span><span class="sxs-lookup"><span data-stu-id="12aba-283">In routes conditions, hello following type checking and casting functions are supported:</span></span>

| <span data-ttu-id="12aba-284">Функция</span><span class="sxs-lookup"><span data-stu-id="12aba-284">Function</span></span> | <span data-ttu-id="12aba-285">Описание</span><span class="sxs-lookup"><span data-stu-id="12aba-285">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="12aba-286">AS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="12aba-286">AS_NUMBER</span></span> | <span data-ttu-id="12aba-287">Преобразует число tooa hello входной строки.</span><span class="sxs-lookup"><span data-stu-id="12aba-287">Converts hello input string tooa number.</span></span> <span data-ttu-id="12aba-288">Возвращает `noop`, если аргумент является числом, или `Undefined`, если строка не представляет число.</span><span class="sxs-lookup"><span data-stu-id="12aba-288">`noop` if input is a number; `Undefined` if string does not represent a number.</span></span>|
| <span data-ttu-id="12aba-289">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="12aba-289">IS_ARRAY</span></span> | <span data-ttu-id="12aba-290">Возвращает логическое значение, указывающее, если тип hello hello задать выражение является массивом.</span><span class="sxs-lookup"><span data-stu-id="12aba-290">Returns a Boolean value indicating if hello type of hello specified expression is an array.</span></span> |
| <span data-ttu-id="12aba-291">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="12aba-291">IS_BOOL</span></span> | <span data-ttu-id="12aba-292">Возвращает логическое значение, указывающее, если тип hello hello задать выражение является логическим.</span><span class="sxs-lookup"><span data-stu-id="12aba-292">Returns a Boolean value indicating if hello type of hello specified expression is a Boolean.</span></span> |
| <span data-ttu-id="12aba-293">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="12aba-293">IS_DEFINED</span></span> | <span data-ttu-id="12aba-294">Возвращает логическое значение, указывающее, если свойство hello назначено значение.</span><span class="sxs-lookup"><span data-stu-id="12aba-294">Returns a Boolean indicating if hello property has been assigned a value.</span></span> |
| <span data-ttu-id="12aba-295">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="12aba-295">IS_NULL</span></span> | <span data-ttu-id="12aba-296">Возвращает логическое значение, указывающее, если тип hello hello задать выражение имеет значение null.</span><span class="sxs-lookup"><span data-stu-id="12aba-296">Returns a Boolean value indicating if hello type of hello specified expression is null.</span></span> |
| <span data-ttu-id="12aba-297">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="12aba-297">IS_NUMBER</span></span> | <span data-ttu-id="12aba-298">Возвращает логическое значение, указывающее, если тип hello hello задать выражение является числом.</span><span class="sxs-lookup"><span data-stu-id="12aba-298">Returns a Boolean value indicating if hello type of hello specified expression is a number.</span></span> |
| <span data-ttu-id="12aba-299">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="12aba-299">IS_OBJECT</span></span> | <span data-ttu-id="12aba-300">Возвращает логическое значение, указывающее, если тип hello hello задать выражение, объект JSON.</span><span class="sxs-lookup"><span data-stu-id="12aba-300">Returns a Boolean value indicating if hello type of hello specified expression is a JSON object.</span></span> |
| <span data-ttu-id="12aba-301">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="12aba-301">IS_PRIMITIVE</span></span> | <span data-ttu-id="12aba-302">Возвращает логическое значение, указывающее, если тип hello hello задать выражение является примитивом (строка, логическое значение, числовое или `null`).</span><span class="sxs-lookup"><span data-stu-id="12aba-302">Returns a Boolean value indicating if hello type of hello specified expression is a primitive (string, Boolean, numeric or `null`).</span></span> |
| <span data-ttu-id="12aba-303">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="12aba-303">IS_STRING</span></span> | <span data-ttu-id="12aba-304">Возвращает логическое значение, указывающее, если тип hello hello выражения является строка.</span><span class="sxs-lookup"><span data-stu-id="12aba-304">Returns a Boolean value indicating if hello type of hello specified expression is a string.</span></span> |

<span data-ttu-id="12aba-305">В условиях маршруты поддерживаются следующие строковые функции hello.</span><span class="sxs-lookup"><span data-stu-id="12aba-305">In routes conditions, hello following string functions are supported:</span></span>

| <span data-ttu-id="12aba-306">Функция</span><span class="sxs-lookup"><span data-stu-id="12aba-306">Function</span></span> | <span data-ttu-id="12aba-307">Описание</span><span class="sxs-lookup"><span data-stu-id="12aba-307">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="12aba-308">CONCAT(x, …)</span><span class="sxs-lookup"><span data-stu-id="12aba-308">CONCAT(x, …)</span></span> | <span data-ttu-id="12aba-309">Возвращает строку, являющуюся результатом объединения двух или более строковых значений hello.</span><span class="sxs-lookup"><span data-stu-id="12aba-309">Returns a string that is hello result of concatenating two or more string values.</span></span> |
| <span data-ttu-id="12aba-310">LENGTH(x)</span><span class="sxs-lookup"><span data-stu-id="12aba-310">LENGTH(x)</span></span> | <span data-ttu-id="12aba-311">Количество символов для hello hello возвращает указанного строкового выражения.</span><span class="sxs-lookup"><span data-stu-id="12aba-311">Returns hello number of characters of hello specified string expression.</span></span>|
| <span data-ttu-id="12aba-312">LOWER(x)</span><span class="sxs-lookup"><span data-stu-id="12aba-312">LOWER(x)</span></span> | <span data-ttu-id="12aba-313">Возвращает строковое выражение после преобразования данных toolowercase символ верхнего регистра.</span><span class="sxs-lookup"><span data-stu-id="12aba-313">Returns a string expression after converting uppercase character data toolowercase.</span></span> |
| <span data-ttu-id="12aba-314">UPPER(x)</span><span class="sxs-lookup"><span data-stu-id="12aba-314">UPPER(x)</span></span> | <span data-ttu-id="12aba-315">Возвращает строковое выражение после преобразования данных toouppercase строчные буквы.</span><span class="sxs-lookup"><span data-stu-id="12aba-315">Returns a string expression after converting lowercase character data toouppercase.</span></span> |
| <span data-ttu-id="12aba-316">SUBSTRING(строка, начало[, длина])</span><span class="sxs-lookup"><span data-stu-id="12aba-316">SUBSTRING(string, start [, length])</span></span> | <span data-ttu-id="12aba-317">Возвращает часть строкового выражения, начиная с hello указан символ Отсчитываемая от нуля позиция и продолжает toohello указывается длина или toohello конца строки hello.</span><span class="sxs-lookup"><span data-stu-id="12aba-317">Returns part of a string expression starting at hello specified character zero-based position and continues toohello specified length, or toohello end of hello string.</span></span> |
| <span data-ttu-id="12aba-318">INDEX_OF(строка, фрагмент)</span><span class="sxs-lookup"><span data-stu-id="12aba-318">INDEX_OF(string, fragment)</span></span> | <span data-ttu-id="12aba-319">Возвращает hello, начальная позиция первого вхождения hello hello второго строкового выражения внутри первого указанного строкового выражения hello, или значение -1, если строка hello не найдена.</span><span class="sxs-lookup"><span data-stu-id="12aba-319">Returns hello starting position of hello first occurrence of hello second string expression within hello first specified string expression, or -1 if hello string is not found.</span></span>|
| <span data-ttu-id="12aba-320">STARTS_WITH(x, y)</span><span class="sxs-lookup"><span data-stu-id="12aba-320">STARTS_WITH(x, y)</span></span> | <span data-ttu-id="12aba-321">Возвращает логическое значение, указывающее, является ли первое строковое выражение hello начинается с hello во-вторых.</span><span class="sxs-lookup"><span data-stu-id="12aba-321">Returns a Boolean indicating whether hello first string expression starts with hello second.</span></span> |
| <span data-ttu-id="12aba-322">ENDS_WITH(x, y)</span><span class="sxs-lookup"><span data-stu-id="12aba-322">ENDS_WITH(x, y)</span></span> | <span data-ttu-id="12aba-323">Возвращает логическое значение, указывающее, было ли первое строковое выражение hello заканчивается hello второй.</span><span class="sxs-lookup"><span data-stu-id="12aba-323">Returns a Boolean indicating whether hello first string expression ends with hello second.</span></span> |
| <span data-ttu-id="12aba-324">CONTAINS(x,y)</span><span class="sxs-lookup"><span data-stu-id="12aba-324">CONTAINS(x,y)</span></span> | <span data-ttu-id="12aba-325">Возвращает логическое значение, указывающее, является ли hello первое строковое выражение содержит hello второй.</span><span class="sxs-lookup"><span data-stu-id="12aba-325">Returns a Boolean indicating whether hello first string expression contains hello second.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="12aba-326">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="12aba-326">Next steps</span></span>
<span data-ttu-id="12aba-327">Узнайте, как tooexecute запросы в приложения с помощью [пакеты SDK Azure IoT][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="12aba-327">Learn how tooexecute queries in your apps using [Azure IoT SDKs][lnk-hub-sdks].</span></span>

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
