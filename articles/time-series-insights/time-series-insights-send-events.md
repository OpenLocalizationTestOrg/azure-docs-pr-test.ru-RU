---
title: "aaaSend события tooAzure аналитики ряда времени среда | Документы Microsoft"
description: "В этом учебнике hello действия toopush события tooyour аналитики ряда времени среды"
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
ms.openlocfilehash: dbccc23f61351a0033cd48c1a02fb3841b45d560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooa-time-series-insights-environment-using-event-hub"></a><span data-ttu-id="6694a-103">Отправка событий tooa аналитики ряда времени среды с помощью концентратора событий</span><span class="sxs-lookup"><span data-stu-id="6694a-103">Send events tooa Time Series Insights environment using event hub</span></span>

<span data-ttu-id="6694a-104">В этом учебнике описано как toocreate и настройка концентратора событий и запустить образец приложения toopush событий.</span><span class="sxs-lookup"><span data-stu-id="6694a-104">This tutorial explains how toocreate and configure event hub and run a sample application toopush events.</span></span> <span data-ttu-id="6694a-105">Если у вас уже есть концентратор событий, содержащий события в формате JSON, пропустите это руководство и просмотрите свою среду в [Time Series Insights](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6694a-105">If you have an existing event hub with events in JSON format, skip this tutorial and view your environment in [time series insights](https://insights.timeseries.azure.com).</span></span>

## <a name="configure-an-event-hub"></a><span data-ttu-id="6694a-106">Настройка концентратора событий</span><span class="sxs-lookup"><span data-stu-id="6694a-106">Configure an event hub</span></span>
1. <span data-ttu-id="6694a-107">toocreate концентратора событий, следуйте инструкциям из концентратора событий hello [документации](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).</span><span class="sxs-lookup"><span data-stu-id="6694a-107">toocreate an event hub, follow instructions from hello Event Hub [documentation](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).</span></span>

2. <span data-ttu-id="6694a-108">Создайте группу потребителей, которая используется исключительно источником событий Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="6694a-108">Make sure you create a consumer group that is used exclusively by your Time Series Insights event source.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="6694a-109">Убедитесь, что эта группа потребителей не используется другой службой (например, заданием Stream Analytics или другой средой Time Series Insights).</span><span class="sxs-lookup"><span data-stu-id="6694a-109">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment).</span></span> <span data-ttu-id="6694a-110">Если группа потребителей используется другими службами, считать операции отрицательно влияет для этой среды и hello других служб.</span><span class="sxs-lookup"><span data-stu-id="6694a-110">If consumer group is used by other services, read operation is negatively affected for this environment and hello other services.</span></span> <span data-ttu-id="6694a-111">При использовании как hello группа потребителей «$Default» может привести toopotential повторного использования другими пользователями.</span><span class="sxs-lookup"><span data-stu-id="6694a-111">If you are using “$Default” as hello consumer group, it could lead toopotential reuse by other readers.</span></span>

  ![Выбор группы потребителей концентратора событий](media/send-events/consumer-group.png)

3. <span data-ttu-id="6694a-113">На концентратор событий hello, создайте «MySendPolicy», используется toosend событий в c# образца hello.</span><span class="sxs-lookup"><span data-stu-id="6694a-113">On hello event hub, create “MySendPolicy” that is used toosend events in hello csharp sample.</span></span>

  ![Выбор "Политики общего доступа" и кнопка "Добавить"](media/send-events/shared-access-policy.png)  

  ![Добавление новой политики общего доступа](media/send-events/shared-access-policy-2.png)  

## <a name="create-time-series-insights-event-source"></a><span data-ttu-id="6694a-116">Создание источника событий Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="6694a-116">Create Time Series Insights event source</span></span>
1. <span data-ttu-id="6694a-117">Если вы еще не создали источник событий, выполните [эти инструкции](time-series-insights-add-event-source.md) toocreate источника события.</span><span class="sxs-lookup"><span data-stu-id="6694a-117">If you haven't created an event source, follow [these instructions](time-series-insights-add-event-source.md) toocreate an event source.</span></span>

2. <span data-ttu-id="6694a-118">Укажите «deviceTimestamp» в качестве имени свойства hello отметка времени — это свойство используется как hello фактическое timestamp в образце hello csharp.</span><span class="sxs-lookup"><span data-stu-id="6694a-118">Specify “deviceTimestamp” as hello timestamp property name – this property is used as hello actual timestamp in hello csharp sample.</span></span> <span data-ttu-id="6694a-119">Имя свойства timestamp Hello учитывается регистр, и значения должны иметь формат hello __гггг-мм-ДДТЧЧ. FFFFFFFK__ при отправке в качестве концентратора tooevent JSON.</span><span class="sxs-lookup"><span data-stu-id="6694a-119">hello timestamp property name is case-sensitive and values must follow hello format __yyyy-MM-ddTHH:mm:ss.FFFFFFFK__ when sent as JSON tooevent hub.</span></span> <span data-ttu-id="6694a-120">Если свойство hello не существует в событии hello, то hello время нахождения концентратора событий будет использоваться.</span><span class="sxs-lookup"><span data-stu-id="6694a-120">If hello property does not exist in hello event, then hello event hub enqueued time is used.</span></span>

  ![Создание источника событий](media/send-events/event-source-1.png)

## <a name="sample-code-toopush-events"></a><span data-ttu-id="6694a-122">Примеры кода toopush событий</span><span class="sxs-lookup"><span data-stu-id="6694a-122">Sample code toopush events</span></span>
1. <span data-ttu-id="6694a-123">Вернитесь к политики концентратора событий toohello «MySendPolicy» и скопируйте строку подключения hello с ключом политики hello.</span><span class="sxs-lookup"><span data-stu-id="6694a-123">Go toohello event hub policy “MySendPolicy” and copy hello connection string with hello policy key.</span></span>

  ![Копирование строки подключения MySendPolicy](media/send-events/sample-code-connection-string.png)

2. <span data-ttu-id="6694a-125">Запустите после кода hello toosend 600 событий для каждого из трех hello устройств.</span><span class="sxs-lookup"><span data-stu-id="6694a-125">Run hello following code that toosend 600 events per each of hello three devices.</span></span> <span data-ttu-id="6694a-126">Обновите `eventHubConnectionString` с помощью строки подключений.</span><span class="sxs-lookup"><span data-stu-id="6694a-126">Update `eventHubConnectionString` with your connection string.</span></span>

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

                // Send JSON tooevent hub.
                EventData eventData = new EventData(ms);
                eventHubClient.Send(eventData);
            }
        }
    }
}

```
## <a name="supported-json-shapes"></a><span data-ttu-id="6694a-127">Поддерживаемые формы JSON</span><span class="sxs-lookup"><span data-stu-id="6694a-127">Supported JSON shapes</span></span>
### <a name="sample-1"></a><span data-ttu-id="6694a-128">Пример 1</span><span class="sxs-lookup"><span data-stu-id="6694a-128">Sample 1</span></span>

#### <a name="input"></a><span data-ttu-id="6694a-129">Входные данные</span><span class="sxs-lookup"><span data-stu-id="6694a-129">Input</span></span>

<span data-ttu-id="6694a-130">Простой объект JSON.</span><span class="sxs-lookup"><span data-stu-id="6694a-130">A simple JSON object.</span></span>

```json
{
    "id":"device1",
    "timestamp":"2016-01-08T01:08:00Z"
}
```
#### <a name="output---1-event"></a><span data-ttu-id="6694a-131">Выходные данные, одно событие</span><span class="sxs-lookup"><span data-stu-id="6694a-131">Output - 1 event</span></span>

|<span data-ttu-id="6694a-132">id</span><span class="sxs-lookup"><span data-stu-id="6694a-132">id</span></span>|<span data-ttu-id="6694a-133">Timestamp</span><span class="sxs-lookup"><span data-stu-id="6694a-133">timestamp</span></span>|
|--------|---------------|
|<span data-ttu-id="6694a-134">device1</span><span class="sxs-lookup"><span data-stu-id="6694a-134">device1</span></span>|<span data-ttu-id="6694a-135">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="6694a-135">2016-01-08T01:08:00Z</span></span>|

### <a name="sample-2"></a><span data-ttu-id="6694a-136">Пример 2</span><span class="sxs-lookup"><span data-stu-id="6694a-136">Sample 2</span></span>

#### <a name="input"></a><span data-ttu-id="6694a-137">Входные данные</span><span class="sxs-lookup"><span data-stu-id="6694a-137">Input</span></span>
<span data-ttu-id="6694a-138">Массив JSON с двумя объектами JSON.</span><span class="sxs-lookup"><span data-stu-id="6694a-138">A JSON array with two JSON objects.</span></span> <span data-ttu-id="6694a-139">Каждый объект JSON будет преобразованный tooan событий.</span><span class="sxs-lookup"><span data-stu-id="6694a-139">Each JSON object will be converted tooan event.</span></span>
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
#### <a name="output---2-events"></a><span data-ttu-id="6694a-140">Выходные данные, два события</span><span class="sxs-lookup"><span data-stu-id="6694a-140">Output - 2 Events</span></span>

|<span data-ttu-id="6694a-141">id</span><span class="sxs-lookup"><span data-stu-id="6694a-141">id</span></span>|<span data-ttu-id="6694a-142">Timestamp</span><span class="sxs-lookup"><span data-stu-id="6694a-142">timestamp</span></span>|
|--------|---------------|
|<span data-ttu-id="6694a-143">device1</span><span class="sxs-lookup"><span data-stu-id="6694a-143">device1</span></span>|<span data-ttu-id="6694a-144">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="6694a-144">2016-01-08T01:08:00Z</span></span>|
|<span data-ttu-id="6694a-145">device2</span><span class="sxs-lookup"><span data-stu-id="6694a-145">device2</span></span>|<span data-ttu-id="6694a-146">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="6694a-146">2016-01-08T01:17:00Z</span></span>|
### <a name="sample-3"></a><span data-ttu-id="6694a-147">Пример 3</span><span class="sxs-lookup"><span data-stu-id="6694a-147">Sample 3</span></span>

#### <a name="input"></a><span data-ttu-id="6694a-148">Входные данные</span><span class="sxs-lookup"><span data-stu-id="6694a-148">Input</span></span>

<span data-ttu-id="6694a-149">Объект JSON с вложенным массивом JSON, содержащий два объекта JSON.</span><span class="sxs-lookup"><span data-stu-id="6694a-149">A JSON object with a nested JSON array containing two JSON objects.</span></span>
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
#### <a name="output---2-events"></a><span data-ttu-id="6694a-150">Выходные данные, два события</span><span class="sxs-lookup"><span data-stu-id="6694a-150">Output - 2 Events</span></span>
<span data-ttu-id="6694a-151">Обратите внимание, что tooeach события hello копирования hello свойство «местоположение».</span><span class="sxs-lookup"><span data-stu-id="6694a-151">Note that hello property "location" is copied over tooeach of hello event.</span></span>

|<span data-ttu-id="6694a-152">location</span><span class="sxs-lookup"><span data-stu-id="6694a-152">location</span></span>|<span data-ttu-id="6694a-153">events.id</span><span class="sxs-lookup"><span data-stu-id="6694a-153">events.id</span></span>|<span data-ttu-id="6694a-154">events.timestamp</span><span class="sxs-lookup"><span data-stu-id="6694a-154">events.timestamp</span></span>|
|--------|---------------|----------------------|
|<span data-ttu-id="6694a-155">WestUs</span><span class="sxs-lookup"><span data-stu-id="6694a-155">WestUs</span></span>|<span data-ttu-id="6694a-156">device1</span><span class="sxs-lookup"><span data-stu-id="6694a-156">device1</span></span>|<span data-ttu-id="6694a-157">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="6694a-157">2016-01-08T01:08:00Z</span></span>|
|<span data-ttu-id="6694a-158">WestUs</span><span class="sxs-lookup"><span data-stu-id="6694a-158">WestUs</span></span>|<span data-ttu-id="6694a-159">device2</span><span class="sxs-lookup"><span data-stu-id="6694a-159">device2</span></span>|<span data-ttu-id="6694a-160">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="6694a-160">2016-01-08T01:17:00Z</span></span>|

### <a name="sample-4"></a><span data-ttu-id="6694a-161">Пример 4</span><span class="sxs-lookup"><span data-stu-id="6694a-161">Sample 4</span></span>

#### <a name="input"></a><span data-ttu-id="6694a-162">Входные данные</span><span class="sxs-lookup"><span data-stu-id="6694a-162">Input</span></span>

<span data-ttu-id="6694a-163">Объект JSON с вложенным массивом JSON, содержащий два объекта JSON.</span><span class="sxs-lookup"><span data-stu-id="6694a-163">A JSON object with a nested JSON array containing two JSON objects.</span></span> <span data-ttu-id="6694a-164">Этот входной демонстрирует, что hello глобальные свойства может быть представлен hello сложный объект JSON.</span><span class="sxs-lookup"><span data-stu-id="6694a-164">This input demonstrates that hello global properties may be represented by hello complex JSON object.</span></span>

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
#### <a name="output---2-events"></a><span data-ttu-id="6694a-165">Выходные данные, два события</span><span class="sxs-lookup"><span data-stu-id="6694a-165">Output - 2 Events</span></span>

|<span data-ttu-id="6694a-166">location</span><span class="sxs-lookup"><span data-stu-id="6694a-166">location</span></span>|<span data-ttu-id="6694a-167">manufacturer.name</span><span class="sxs-lookup"><span data-stu-id="6694a-167">manufacturer.name</span></span>|<span data-ttu-id="6694a-168">manufacturer.location</span><span class="sxs-lookup"><span data-stu-id="6694a-168">manufacturer.location</span></span>|<span data-ttu-id="6694a-169">events.id</span><span class="sxs-lookup"><span data-stu-id="6694a-169">events.id</span></span>|<span data-ttu-id="6694a-170">events.timestamp</span><span class="sxs-lookup"><span data-stu-id="6694a-170">events.timestamp</span></span>|<span data-ttu-id="6694a-171">events.data.type</span><span class="sxs-lookup"><span data-stu-id="6694a-171">events.data.type</span></span>|<span data-ttu-id="6694a-172">events.data.units</span><span class="sxs-lookup"><span data-stu-id="6694a-172">events.data.units</span></span>|<span data-ttu-id="6694a-173">events.data.value</span><span class="sxs-lookup"><span data-stu-id="6694a-173">events.data.value</span></span>|
|---|---|---|---|---|---|---|---|
|<span data-ttu-id="6694a-174">WestUs</span><span class="sxs-lookup"><span data-stu-id="6694a-174">WestUs</span></span>|<span data-ttu-id="6694a-175">manufacturer1</span><span class="sxs-lookup"><span data-stu-id="6694a-175">manufacturer1</span></span>|<span data-ttu-id="6694a-176">EastUs</span><span class="sxs-lookup"><span data-stu-id="6694a-176">EastUs</span></span>|<span data-ttu-id="6694a-177">device1</span><span class="sxs-lookup"><span data-stu-id="6694a-177">device1</span></span>|<span data-ttu-id="6694a-178">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="6694a-178">2016-01-08T01:08:00Z</span></span>|<span data-ttu-id="6694a-179">pressure</span><span class="sxs-lookup"><span data-stu-id="6694a-179">pressure</span></span>|<span data-ttu-id="6694a-180">psi</span><span class="sxs-lookup"><span data-stu-id="6694a-180">psi</span></span>|<span data-ttu-id="6694a-181">108.09</span><span class="sxs-lookup"><span data-stu-id="6694a-181">108.09</span></span>|
|<span data-ttu-id="6694a-182">WestUs</span><span class="sxs-lookup"><span data-stu-id="6694a-182">WestUs</span></span>|<span data-ttu-id="6694a-183">manufacturer1</span><span class="sxs-lookup"><span data-stu-id="6694a-183">manufacturer1</span></span>|<span data-ttu-id="6694a-184">EastUs</span><span class="sxs-lookup"><span data-stu-id="6694a-184">EastUs</span></span>|<span data-ttu-id="6694a-185">device2</span><span class="sxs-lookup"><span data-stu-id="6694a-185">device2</span></span>|<span data-ttu-id="6694a-186">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="6694a-186">2016-01-08T01:17:00Z</span></span>|<span data-ttu-id="6694a-187">vibration</span><span class="sxs-lookup"><span data-stu-id="6694a-187">vibration</span></span>|<span data-ttu-id="6694a-188">abs G</span><span class="sxs-lookup"><span data-stu-id="6694a-188">abs G</span></span>|<span data-ttu-id="6694a-189">217.09</span><span class="sxs-lookup"><span data-stu-id="6694a-189">217.09</span></span>|

## <a name="next-steps"></a><span data-ttu-id="6694a-190">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6694a-190">Next steps</span></span>

* <span data-ttu-id="6694a-191">Просмотрите свою среду на [портале Time Series Insights](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6694a-191">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
