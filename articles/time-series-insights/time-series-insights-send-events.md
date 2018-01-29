---
title: "Как отправлять события в среду службы \"Аналитика временных рядов Azure\" | Документация Майкрософт"
description: "Это руководство содержит сведения о том, как создать и настроить концентратор событий и запустить пример приложения для передачи событий и их отображения в службе \"Аналитика временных рядов Azure\"."
services: time-series-insights
ms.service: time-series-insights
author: venkatgct
ms.author: venkatja
manager: jhubbard
editor: MarkMcGeeAtAquent
ms.reviewer: v-mamcge, jasonh, kfile, anshan
ms.devlang: csharp
ms.workload: big-data
ms.topic: article
ms.date: 11/15/2017
ms.openlocfilehash: 2c1b91fb87857eee8ca938be193b61e01bbdb886
ms.sourcegitcommit: afc78e4fdef08e4ef75e3456fdfe3709d3c3680b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/16/2017
---
# <a name="send-events-to-a-time-series-insights-environment-using-event-hub"></a>Отправка событий в среду Time Series Insights через концентратор событий
Это статья содержит сведения о том, как создать и настроить концентратор событий и запустить пример приложения для передачи событий. Если у вас уже есть концентратор событий, содержащий события в формате JSON, пропустите это руководство и просмотрите свою среду в службе [Аналитика временных рядов](https://insights.timeseries.azure.com).

## <a name="configure-an-event-hub"></a>Настройка концентратора событий
1. Чтобы создать концентратор событий, следуйте инструкциям из [документации](../event-hubs/event-hubs-create.md) по концентратору событий.

2. Выполните поиск **концентратора событий** в строке поиска. Выберите **Концентраторы событий** в возвращенном списке.

3. Выберите концентратор событий, щелкнув его имя.

4. В разделе **Сущности** в центре окна настройки снова выберите **Концентраторы событий**.

5. Выберите имя концентратора событий, чтобы настроить его.

  ![Выбор группы потребителей концентратора событий](media/send-events/consumer-group.png)

6. В разделе **Сущности** выберите **Группы потребителей**.
 
7. Создайте группу потребителей, которая используется исключительно источником событий Time Series Insights.

   > [!IMPORTANT]
   > Убедитесь, что эта группа потребителей не используется другой службой (например, заданием Stream Analytics или другой средой Time Series Insights). Если группа потребителей используется другими службами, это негативно скажется на операции чтения в этой среде и в других службах. Использование $Default в качестве группы потребителей может потенциально привести к ее повторному использованию другими читателями.

8. В разделе **Параметры** выберите **Share access policies** (Политики общего доступа).

9. В концентраторе событий создайте политику **MySendPolicy**, используемую для отправки событий в примере CSharp.

  ![Выбор "Политики общего доступа" и кнопка "Добавить"](media/send-events/shared-access-policy.png)  

  ![Добавление новой политики общего доступа](media/send-events/shared-access-policy-2.png)  

## <a name="create-time-series-insights-event-source"></a>Создание источника событий Time Series Insights
1. Если вы еще не создали источник событий, создайте его, [следуя инструкциям](time-series-insights-how-to-add-an-event-source-eventhub.md).

2. В качестве имени свойства метки времени укажите **deviceTimestamp**. Это свойство будет использоваться в качестве фактической метки времени в примере C#. Имя свойства метки времени чувствительно к регистру, поэтому при отправке в концентратор событий в формате JSON значения должны иметь формат __yyyy-MM-ddTHH:mm:ss.FFFFFFFK__. Если свойство не существует в событии, используется время размещения в очереди для концентратора событий.

  ![Создание источника событий](media/send-events/event-source-1.png)

## <a name="sample-code-to-push-events"></a>Пример кода для принудительной отправки событий
1. Перейдите к политике концентратора событий с именем **MySendPolicy**. Скопируйте **строку подключения** с ключом политики.

  ![Копирование строки подключения MySendPolicy](media/send-events/sample-code-connection-string.png)

2. Выполните следующий код, который будет отправлять 600 событий для каждого из трех устройств. Обновите `eventHubConnectionString` с помощью строки подключений.

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
## <a name="supported-json-shapes"></a>Поддерживаемые формы JSON
### <a name="sample-1"></a>Пример 1

#### <a name="input"></a>Входные данные

Простой объект JSON.

```json
{
    "id":"device1",
    "timestamp":"2016-01-08T01:08:00Z"
}
```
#### <a name="output---1-event"></a>Выходные данные, одно событие

|id|Timestamp|
|--------|---------------|
|device1|2016-01-08T01:08:00Z|

### <a name="sample-2"></a>Пример 2

#### <a name="input"></a>Входные данные
Массив JSON с двумя объектами JSON. Каждый объект JSON будет преобразован в событие.
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
#### <a name="output---2-events"></a>Выходные данные, два события

|id|Timestamp|
|--------|---------------|
|device1|2016-01-08T01:08:00Z|
|device2|2016-01-08T01:17:00Z|

### <a name="sample-3"></a>Пример 3

#### <a name="input"></a>Входные данные

Объект JSON с вложенным массивом JSON, содержащий два объекта JSON.
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
#### <a name="output---2-events"></a>Выходные данные, два события
Обратите внимание, что свойство location копируется для каждого события.

|location|events.id|events.timestamp|
|--------|---------------|----------------------|
|WestUs|device1|2016-01-08T01:08:00Z|
|WestUs|device2|2016-01-08T01:17:00Z|

### <a name="sample-4"></a>Пример 4

#### <a name="input"></a>Входные данные

Объект JSON с вложенным массивом JSON, содержащий два объекта JSON. Эти входные данные указывают на то, что глобальные свойства могут быть представлены сложным объектом JSON.

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
#### <a name="output---2-events"></a>Выходные данные, два события

|location|manufacturer.name|manufacturer.location|events.id|events.timestamp|events.data.type|events.data.units|events.data.value|
|---|---|---|---|---|---|---|---|
|WestUs|manufacturer1|EastUs|device1|2016-01-08T01:08:00Z|pressure|psi|108.09|
|WestUs|manufacturer1|EastUs|device2|2016-01-08T01:17:00Z|vibration|abs G|217.09|

## <a name="next-steps"></a>Дальнейшие действия
> [!div class="nextstepaction"]
> [Просмотрите свою среду в обозревателе службы "Аналитика временных рядов"](https://insights.timeseries.azure.com).
