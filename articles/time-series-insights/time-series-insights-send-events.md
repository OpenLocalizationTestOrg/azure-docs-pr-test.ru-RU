---
title: "Отправка событий в среду Azure Time Series Insights | Документация Майкрософт"
description: "Это руководство содержит сведения об отправке событий в среду Time Series Insights."
keywords: 
services: tsi
documentationcenter: 
author: venkatgct
manager: jhubbard
editor: 
ms.assetid: 
ms.service: tsi
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/21/2017
ms.author: venkatja
ms.openlocfilehash: b4ef96a045393f28b3cd750068fe82a5a8411afa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="send-events-to-a-time-series-insights-environment-using-event-hub"></a><span data-ttu-id="5f7b2-103">Отправка событий в среду Time Series Insights через концентратор событий</span><span class="sxs-lookup"><span data-stu-id="5f7b2-103">Send events to a Time Series Insights environment using event hub</span></span>

<span data-ttu-id="5f7b2-104">Это руководство содержит сведения о том, как создать и настроить концентратор событий и запустить пример приложения для передачи событий.</span><span class="sxs-lookup"><span data-stu-id="5f7b2-104">This tutorial explains how to create and configure event hub and run a sample application to push events.</span></span> <span data-ttu-id="5f7b2-105">Если у вас уже есть концентратор событий, содержащий события в формате JSON, пропустите это руководство и просмотрите свою среду в [Time Series Insights](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5f7b2-105">If you have an existing event hub with events in JSON format, skip this tutorial and view your environment in [time series insights](https://insights.timeseries.azure.com).</span></span>

## <a name="configure-an-event-hub"></a><span data-ttu-id="5f7b2-106">Настройка концентратора событий</span><span class="sxs-lookup"><span data-stu-id="5f7b2-106">Configure an event hub</span></span>
1. <span data-ttu-id="5f7b2-107">Чтобы создать концентратор событий, следуйте инструкциям из [документации](https://docs.microsoft.com/azure/event-hubs/event-hubs-create) по концентратору событий.</span><span class="sxs-lookup"><span data-stu-id="5f7b2-107">To create an event hub, follow instructions from the Event Hub [documentation](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).</span></span>

2. <span data-ttu-id="5f7b2-108">Создайте группу потребителей, которая используется исключительно источником событий Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="5f7b2-108">Make sure you create a consumer group that is used exclusively by your Time Series Insights event source.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="5f7b2-109">Убедитесь, что эта группа потребителей не используется другой службой (например, заданием Stream Analytics или другой средой Time Series Insights).</span><span class="sxs-lookup"><span data-stu-id="5f7b2-109">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment).</span></span> <span data-ttu-id="5f7b2-110">Если группа потребителей используется другими службами, это негативно скажется на операции чтения в этой среде и в других службах.</span><span class="sxs-lookup"><span data-stu-id="5f7b2-110">If consumer group is used by other services, read operation is negatively affected for this environment and the other services.</span></span> <span data-ttu-id="5f7b2-111">Использование $Default в качестве группы потребителей может потенциально привести к ее повторному использованию другими читателями.</span><span class="sxs-lookup"><span data-stu-id="5f7b2-111">If you are using “$Default” as the consumer group, it could lead to potential reuse by other readers.</span></span>

  ![Выбор группы потребителей концентратора событий](media/send-events/consumer-group.png)

3. <span data-ttu-id="5f7b2-113">В концентраторе событий создайте политику MySendPolicy, используемую для отправки событий в примере C#.</span><span class="sxs-lookup"><span data-stu-id="5f7b2-113">On the event hub, create “MySendPolicy” that is used to send events in the csharp sample.</span></span>

  ![Выбор "Политики общего доступа" и кнопка "Добавить"](media/send-events/shared-access-policy.png)  

  ![Добавление новой политики общего доступа](media/send-events/shared-access-policy-2.png)  

## <a name="create-time-series-insights-event-source"></a><span data-ttu-id="5f7b2-116">Создание источника событий Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="5f7b2-116">Create Time Series Insights event source</span></span>
1. <span data-ttu-id="5f7b2-117">Если вы еще не создали источник событий, создайте его, [следуя инструкциям](time-series-insights-add-event-source.md).</span><span class="sxs-lookup"><span data-stu-id="5f7b2-117">If you haven't created an event source, follow [these instructions](time-series-insights-add-event-source.md) to create an event source.</span></span>

2. <span data-ttu-id="5f7b2-118">В качестве имени свойства метки времени укажите deviceTimestamp. Это свойство будет использоваться в качестве фактической метки времени в примере C#.</span><span class="sxs-lookup"><span data-stu-id="5f7b2-118">Specify “deviceTimestamp” as the timestamp property name – this property is used as the actual timestamp in the csharp sample.</span></span> <span data-ttu-id="5f7b2-119">Имя свойства метки времени чувствительно к регистру, поэтому при отправке в концентратор событий в формате JSON значения должны иметь формат __yyyy-MM-ddTHH:mm:ss.FFFFFFFK__.</span><span class="sxs-lookup"><span data-stu-id="5f7b2-119">The timestamp property name is case-sensitive and values must follow the format __yyyy-MM-ddTHH:mm:ss.FFFFFFFK__ when sent as JSON to event hub.</span></span> <span data-ttu-id="5f7b2-120">Если свойство не существует в событии, используется время размещения в очереди для концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="5f7b2-120">If the property does not exist in the event, then the event hub enqueued time is used.</span></span>

  ![Создание источника событий](media/send-events/event-source-1.png)

## <a name="sample-code-to-push-events"></a><span data-ttu-id="5f7b2-122">Пример кода для принудительной отправки событий</span><span class="sxs-lookup"><span data-stu-id="5f7b2-122">Sample code to push events</span></span>
1. <span data-ttu-id="5f7b2-123">Перейдите к политике концентратора событий MySendPolicy и скопируйте строку подключения с ключом политики.</span><span class="sxs-lookup"><span data-stu-id="5f7b2-123">Go to the event hub policy “MySendPolicy” and copy the connection string with the policy key.</span></span>

  ![Копирование строки подключения MySendPolicy](media/send-events/sample-code-connection-string.png)

2. <span data-ttu-id="5f7b2-125">Выполните следующий код, который будет отправлять 600 событий для каждого из трех устройств.</span><span class="sxs-lookup"><span data-stu-id="5f7b2-125">Run the following code that to send 600 events per each of the three devices.</span></span> <span data-ttu-id="5f7b2-126">Обновите `eventHubConnectionString` с помощью строки подключений.</span><span class="sxs-lookup"><span data-stu-id="5f7b2-126">Update `eventHubConnectionString` with your connection string.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Globalization;
using System.IO;
using Microsoft.ServiceBus.Messaging;

namespace Microsoft.Rdx.DataGenerator
{
    internal class Program
    {
        private static void Main(string[] args)
        {
            var from = new DateTime(2017, 4, 20, 15, 0, 0, DateTimeKind.Utc);
            Random r = new Random();
            const int numberOfEvents = 600;

            var deviceIds = new[] { "device1", "device2", "device3" };

            var events = new List<string>();
            for (int i = 0; i < numberOfEvents; ++i)
            {
                for (int device = 0; device < deviceIds.Length; ++device)
                {
                    // Generate event and serialize as JSON object:
                    // { "deviceTimestamp": "utc timestamp", "deviceId": "guid", "value": 123.456 }
                    events.Add(
                        String.Format(
                            CultureInfo.InvariantCulture,
                            @"{{ ""deviceTimestamp"": ""{0}"", ""deviceId"": ""{1}"", ""value"": {2} }}",
                            (from + TimeSpan.FromSeconds(i * 30)).ToString("o"),
                            deviceIds[device],
                            r.NextDouble()));
                }
            }

            // Create event hub connection.
            var eventHubConnectionString = @"Endpoint=sb://...";
            var eventHubClient = EventHubClient.CreateFromConnectionString(eventHubConnectionString);

            using (var ms = new MemoryStream())
            using (var sw = new StreamWriter(ms))
            {
                // Wrap events into JSON array:
                sw.Write("[");
                for (int i = 0; i < events.Count; ++i)
                {
                    if (i > 0)
                    {
                        sw.Write(',');
                    }
                    sw.Write(events[i]);
                }
                sw.Write("]");

                sw.Flush();
                ms.Position = 0;

                // Send JSON to event hub.
                EventData eventData = new EventData(ms);
                eventHubClient.Send(eventData);
            }
        }
    }
}

```
## <a name="supported-json-shapes"></a><span data-ttu-id="5f7b2-127">Поддерживаемые формы JSON</span><span class="sxs-lookup"><span data-stu-id="5f7b2-127">Supported JSON shapes</span></span>
### <a name="sample-1"></a><span data-ttu-id="5f7b2-128">Пример 1</span><span class="sxs-lookup"><span data-stu-id="5f7b2-128">Sample 1</span></span>

#### <a name="input"></a><span data-ttu-id="5f7b2-129">Входные данные</span><span class="sxs-lookup"><span data-stu-id="5f7b2-129">Input</span></span>

<span data-ttu-id="5f7b2-130">Простой объект JSON.</span><span class="sxs-lookup"><span data-stu-id="5f7b2-130">A simple JSON object.</span></span>

```json
{
    "id":"device1",
    "timestamp":"2016-01-08T01:08:00Z"
}
```
#### <a name="output---1-event"></a><span data-ttu-id="5f7b2-131">Выходные данные, одно событие</span><span class="sxs-lookup"><span data-stu-id="5f7b2-131">Output - 1 event</span></span>

|<span data-ttu-id="5f7b2-132">id</span><span class="sxs-lookup"><span data-stu-id="5f7b2-132">id</span></span>|<span data-ttu-id="5f7b2-133">Timestamp</span><span class="sxs-lookup"><span data-stu-id="5f7b2-133">timestamp</span></span>|
|--------|---------------|
|<span data-ttu-id="5f7b2-134">device1</span><span class="sxs-lookup"><span data-stu-id="5f7b2-134">device1</span></span>|<span data-ttu-id="5f7b2-135">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="5f7b2-135">2016-01-08T01:08:00Z</span></span>|

### <a name="sample-2"></a><span data-ttu-id="5f7b2-136">Пример 2</span><span class="sxs-lookup"><span data-stu-id="5f7b2-136">Sample 2</span></span>

#### <a name="input"></a><span data-ttu-id="5f7b2-137">Входные данные</span><span class="sxs-lookup"><span data-stu-id="5f7b2-137">Input</span></span>
<span data-ttu-id="5f7b2-138">Массив JSON с двумя объектами JSON.</span><span class="sxs-lookup"><span data-stu-id="5f7b2-138">A JSON array with two JSON objects.</span></span> <span data-ttu-id="5f7b2-139">Каждый объект JSON будет преобразован в событие.</span><span class="sxs-lookup"><span data-stu-id="5f7b2-139">Each JSON object will be converted to an event.</span></span>
```json
[
    {
        "id":"device1",
        "timestamp":"2016-01-08T01:08:00Z"
    },
    {
        "id":"device2",
        "timestamp":"2016-01-17T01:17:00Z"
    }
]
```
#### <a name="output---2-events"></a><span data-ttu-id="5f7b2-140">Выходные данные, два события</span><span class="sxs-lookup"><span data-stu-id="5f7b2-140">Output - 2 Events</span></span>

|<span data-ttu-id="5f7b2-141">id</span><span class="sxs-lookup"><span data-stu-id="5f7b2-141">id</span></span>|<span data-ttu-id="5f7b2-142">Timestamp</span><span class="sxs-lookup"><span data-stu-id="5f7b2-142">timestamp</span></span>|
|--------|---------------|
|<span data-ttu-id="5f7b2-143">device1</span><span class="sxs-lookup"><span data-stu-id="5f7b2-143">device1</span></span>|<span data-ttu-id="5f7b2-144">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="5f7b2-144">2016-01-08T01:08:00Z</span></span>|
|<span data-ttu-id="5f7b2-145">device2</span><span class="sxs-lookup"><span data-stu-id="5f7b2-145">device2</span></span>|<span data-ttu-id="5f7b2-146">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="5f7b2-146">2016-01-08T01:17:00Z</span></span>|
### <a name="sample-3"></a><span data-ttu-id="5f7b2-147">Пример 3</span><span class="sxs-lookup"><span data-stu-id="5f7b2-147">Sample 3</span></span>

#### <a name="input"></a><span data-ttu-id="5f7b2-148">Входные данные</span><span class="sxs-lookup"><span data-stu-id="5f7b2-148">Input</span></span>

<span data-ttu-id="5f7b2-149">Объект JSON с вложенным массивом JSON, содержащий два объекта JSON.</span><span class="sxs-lookup"><span data-stu-id="5f7b2-149">A JSON object with a nested JSON array containing two JSON objects.</span></span>
```json
{
    "location":"WestUs",
    "events":[
        {
            "id":"device1",
            "timestamp":"2016-01-08T01:08:00Z"
        },
        {
            "id":"device2",
            "timestamp":"2016-01-17T01:17:00Z"
        }
    ]
}

```
#### <a name="output---2-events"></a><span data-ttu-id="5f7b2-150">Выходные данные, два события</span><span class="sxs-lookup"><span data-stu-id="5f7b2-150">Output - 2 Events</span></span>
<span data-ttu-id="5f7b2-151">Обратите внимание, что свойство location копируется для каждого события.</span><span class="sxs-lookup"><span data-stu-id="5f7b2-151">Note that the property "location" is copied over to each of the event.</span></span>

|<span data-ttu-id="5f7b2-152">location</span><span class="sxs-lookup"><span data-stu-id="5f7b2-152">location</span></span>|<span data-ttu-id="5f7b2-153">events.id</span><span class="sxs-lookup"><span data-stu-id="5f7b2-153">events.id</span></span>|<span data-ttu-id="5f7b2-154">events.timestamp</span><span class="sxs-lookup"><span data-stu-id="5f7b2-154">events.timestamp</span></span>|
|--------|---------------|----------------------|
|<span data-ttu-id="5f7b2-155">WestUs</span><span class="sxs-lookup"><span data-stu-id="5f7b2-155">WestUs</span></span>|<span data-ttu-id="5f7b2-156">device1</span><span class="sxs-lookup"><span data-stu-id="5f7b2-156">device1</span></span>|<span data-ttu-id="5f7b2-157">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="5f7b2-157">2016-01-08T01:08:00Z</span></span>|
|<span data-ttu-id="5f7b2-158">WestUs</span><span class="sxs-lookup"><span data-stu-id="5f7b2-158">WestUs</span></span>|<span data-ttu-id="5f7b2-159">device2</span><span class="sxs-lookup"><span data-stu-id="5f7b2-159">device2</span></span>|<span data-ttu-id="5f7b2-160">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="5f7b2-160">2016-01-08T01:17:00Z</span></span>|

### <a name="sample-4"></a><span data-ttu-id="5f7b2-161">Пример 4</span><span class="sxs-lookup"><span data-stu-id="5f7b2-161">Sample 4</span></span>

#### <a name="input"></a><span data-ttu-id="5f7b2-162">Входные данные</span><span class="sxs-lookup"><span data-stu-id="5f7b2-162">Input</span></span>

<span data-ttu-id="5f7b2-163">Объект JSON с вложенным массивом JSON, содержащий два объекта JSON.</span><span class="sxs-lookup"><span data-stu-id="5f7b2-163">A JSON object with a nested JSON array containing two JSON objects.</span></span> <span data-ttu-id="5f7b2-164">Эти входные данные указывают на то, что глобальные свойства могут быть представлены сложным объектом JSON.</span><span class="sxs-lookup"><span data-stu-id="5f7b2-164">This input demonstrates that the global properties may be represented by the complex JSON object.</span></span>

```json
{
    "location":"WestUs",
    "manufacturer":{
        "name":"manufacturer1",
        "location":"EastUs"
    },
    "events":[
        {
            "id":"device1",
            "timestamp":"2016-01-08T01:08:00Z",
            "data":{
                "type":"pressure",
                "units":"psi",
                "value":108.09
            }
        },
        {
            "id":"device2",
            "timestamp":"2016-01-17T01:17:00Z",
            "data":{
                "type":"vibration",
                "units":"abs G",
                "value":217.09
            }
        }
    ]
}
```
#### <a name="output---2-events"></a><span data-ttu-id="5f7b2-165">Выходные данные, два события</span><span class="sxs-lookup"><span data-stu-id="5f7b2-165">Output - 2 Events</span></span>

|<span data-ttu-id="5f7b2-166">location</span><span class="sxs-lookup"><span data-stu-id="5f7b2-166">location</span></span>|<span data-ttu-id="5f7b2-167">manufacturer.name</span><span class="sxs-lookup"><span data-stu-id="5f7b2-167">manufacturer.name</span></span>|<span data-ttu-id="5f7b2-168">manufacturer.location</span><span class="sxs-lookup"><span data-stu-id="5f7b2-168">manufacturer.location</span></span>|<span data-ttu-id="5f7b2-169">events.id</span><span class="sxs-lookup"><span data-stu-id="5f7b2-169">events.id</span></span>|<span data-ttu-id="5f7b2-170">events.timestamp</span><span class="sxs-lookup"><span data-stu-id="5f7b2-170">events.timestamp</span></span>|<span data-ttu-id="5f7b2-171">events.data.type</span><span class="sxs-lookup"><span data-stu-id="5f7b2-171">events.data.type</span></span>|<span data-ttu-id="5f7b2-172">events.data.units</span><span class="sxs-lookup"><span data-stu-id="5f7b2-172">events.data.units</span></span>|<span data-ttu-id="5f7b2-173">events.data.value</span><span class="sxs-lookup"><span data-stu-id="5f7b2-173">events.data.value</span></span>|
|---|---|---|---|---|---|---|---|
|<span data-ttu-id="5f7b2-174">WestUs</span><span class="sxs-lookup"><span data-stu-id="5f7b2-174">WestUs</span></span>|<span data-ttu-id="5f7b2-175">manufacturer1</span><span class="sxs-lookup"><span data-stu-id="5f7b2-175">manufacturer1</span></span>|<span data-ttu-id="5f7b2-176">EastUs</span><span class="sxs-lookup"><span data-stu-id="5f7b2-176">EastUs</span></span>|<span data-ttu-id="5f7b2-177">device1</span><span class="sxs-lookup"><span data-stu-id="5f7b2-177">device1</span></span>|<span data-ttu-id="5f7b2-178">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="5f7b2-178">2016-01-08T01:08:00Z</span></span>|<span data-ttu-id="5f7b2-179">pressure</span><span class="sxs-lookup"><span data-stu-id="5f7b2-179">pressure</span></span>|<span data-ttu-id="5f7b2-180">psi</span><span class="sxs-lookup"><span data-stu-id="5f7b2-180">psi</span></span>|<span data-ttu-id="5f7b2-181">108.09</span><span class="sxs-lookup"><span data-stu-id="5f7b2-181">108.09</span></span>|
|<span data-ttu-id="5f7b2-182">WestUs</span><span class="sxs-lookup"><span data-stu-id="5f7b2-182">WestUs</span></span>|<span data-ttu-id="5f7b2-183">manufacturer1</span><span class="sxs-lookup"><span data-stu-id="5f7b2-183">manufacturer1</span></span>|<span data-ttu-id="5f7b2-184">EastUs</span><span class="sxs-lookup"><span data-stu-id="5f7b2-184">EastUs</span></span>|<span data-ttu-id="5f7b2-185">device2</span><span class="sxs-lookup"><span data-stu-id="5f7b2-185">device2</span></span>|<span data-ttu-id="5f7b2-186">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="5f7b2-186">2016-01-08T01:17:00Z</span></span>|<span data-ttu-id="5f7b2-187">vibration</span><span class="sxs-lookup"><span data-stu-id="5f7b2-187">vibration</span></span>|<span data-ttu-id="5f7b2-188">abs G</span><span class="sxs-lookup"><span data-stu-id="5f7b2-188">abs G</span></span>|<span data-ttu-id="5f7b2-189">217.09</span><span class="sxs-lookup"><span data-stu-id="5f7b2-189">217.09</span></span>|

## <a name="next-steps"></a><span data-ttu-id="5f7b2-190">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5f7b2-190">Next steps</span></span>

* <span data-ttu-id="5f7b2-191">Просмотрите свою среду на [портале Time Series Insights](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5f7b2-191">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
