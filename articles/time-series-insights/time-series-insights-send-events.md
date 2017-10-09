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
# <a name="send-events-tooa-time-series-insights-environment-using-event-hub"></a>Отправка событий tooa аналитики ряда времени среды с помощью концентратора событий

В этом учебнике описано как toocreate и настройка концентратора событий и запустить образец приложения toopush событий. Если у вас уже есть концентратор событий, содержащий события в формате JSON, пропустите это руководство и просмотрите свою среду в [Time Series Insights](https://insights.timeseries.azure.com).

## <a name="configure-an-event-hub"></a>Настройка концентратора событий
1. toocreate концентратора событий, следуйте инструкциям из концентратора событий hello [документации](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).

2. Создайте группу потребителей, которая используется исключительно источником событий Time Series Insights.

  > [!IMPORTANT]
  > Убедитесь, что эта группа потребителей не используется другой службой (например, заданием Stream Analytics или другой средой Time Series Insights). Если группа потребителей используется другими службами, считать операции отрицательно влияет для этой среды и hello других служб. При использовании как hello группа потребителей «$Default» может привести toopotential повторного использования другими пользователями.

  ![Выбор группы потребителей концентратора событий](media/send-events/consumer-group.png)

3. На концентратор событий hello, создайте «MySendPolicy», используется toosend событий в c# образца hello.

  ![Выбор "Политики общего доступа" и кнопка "Добавить"](media/send-events/shared-access-policy.png)  

  ![Добавление новой политики общего доступа](media/send-events/shared-access-policy-2.png)  

## <a name="create-time-series-insights-event-source"></a>Создание источника событий Time Series Insights
1. Если вы еще не создали источник событий, выполните [эти инструкции](time-series-insights-add-event-source.md) toocreate источника события.

2. Укажите «deviceTimestamp» в качестве имени свойства hello отметка времени — это свойство используется как hello фактическое timestamp в образце hello csharp. Имя свойства timestamp Hello учитывается регистр, и значения должны иметь формат hello __гггг-мм-ДДТЧЧ. FFFFFFFK__ при отправке в качестве концентратора tooevent JSON. Если свойство hello не существует в событии hello, то hello время нахождения концентратора событий будет использоваться.

  ![Создание источника событий](media/send-events/event-source-1.png)

## <a name="sample-code-toopush-events"></a>Примеры кода toopush событий
1. Вернитесь к политики концентратора событий toohello «MySendPolicy» и скопируйте строку подключения hello с ключом политики hello.

  ![Копирование строки подключения MySendPolicy](media/send-events/sample-code-connection-string.png)

2. Запустите после кода hello toosend 600 событий для каждого из трех hello устройств. Обновите `eventHubConnectionString` с помощью строки подключений.

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
Массив JSON с двумя объектами JSON. Каждый объект JSON будет преобразованный tooan событий.
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
Обратите внимание, что tooeach события hello копирования hello свойство «местоположение».

|location|events.id|events.timestamp|
|--------|---------------|----------------------|
|WestUs|device1|2016-01-08T01:08:00Z|
|WestUs|device2|2016-01-08T01:17:00Z|

### <a name="sample-4"></a>Пример 4

#### <a name="input"></a>Входные данные

Объект JSON с вложенным массивом JSON, содержащий два объекта JSON. Этот входной демонстрирует, что hello глобальные свойства может быть представлен hello сложный объект JSON.

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

* Просмотрите свою среду на [портале Time Series Insights](https://insights.timeseries.azure.com).
