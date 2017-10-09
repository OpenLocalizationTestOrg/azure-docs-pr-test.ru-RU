---
title: "привязки функции концентраторов событий aaaAzure | Документы Microsoft"
description: "Понять, как привязки toouse концентраторов событий Azure в функциях Azure."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "функции azure, функции, обработка событий, динамические вычисления, независимая архитектура"
ms.assetid: daf81798-7acc-419a-bc32-b5a41c6db56b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/20/2017
ms.author: wesmc
ms.openlocfilehash: e864f032ad5ac58d318c9843c3844b5642733a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-event-hubs-bindings"></a>Привязки концентраторов событий функций Azure
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

В этой статье объясняется, как tooconfigure и использовать [концентраторов событий Azure](../event-hubs/event-hubs-what-is-event-hubs.md) привязки для функций Azure.
Функции Azure поддерживают привязки триггера и выходные привязки для концентраторов событий Azure.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

При наличии новых концентраторов событий tooAzure разделе hello [Обзор концентраторов событий](../event-hubs/event-hubs-what-is-event-hubs.md).

<a name="trigger"></a>

## <a name="event-hub-trigger"></a>Триггер концентратора событий
Концентраторы событий используйте hello Активация события tooan toorespond, отправленных поток tooan события концентратора событий. Необходимо иметь доступ на чтение toohello события концентратора tooset копирование триггера hello.

триггер функции Hello концентраторов событий использует следующий объект JSON в hello hello `bindings` массив function.json:

```json
{
    "type": "eventHubTrigger",
    "name": "<Name of trigger parameter in function signature>",
    "direction": "in",
    "path": "<Name of hello event hub>",
    "consumerGroup": "Consumer group toouse - see below",
    "connection": "<Name of app setting with connection string - see below>"
}
```

`consumerGroup`является hello необязательное свойство, используемое tooset [группы потребителей](../event-hubs/event-hubs-features.md#event-consumers) используется toosubscribe tooevents в концентраторе hello. Если не указано, hello `$Default` используется группа потребителей.  
`connection`должно быть именем hello Настройка приложения, содержащий пространство имен hello соединения строки toohello концентратора событий по.
Скопируйте эту строку подключения, нажав hello **сведения о соединении** кнопки для hello *имен*, не hello концентратора событий сам. Эта строка подключения должна иметь по крайней мере чтение разрешений tooactivate hello триггера.

[Дополнительные параметры](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) могут предоставляться в host.json toofurther файл точной настройки триггеры концентраторов событий.  

<a name="triggerusage"></a>

## <a name="trigger-usage"></a>Использование триггера
При запуске функции концентраторов событий триггера приветственное сообщение, которое запускает его передается функции hello как строка.

<a name="triggersample"></a>

## <a name="trigger-sample"></a>Пример триггера
Предположим, что имеется следующий концентраторов событий триггера в hello hello `bindings` массив function.json:

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```

См. Образец hello конкретного языка, записывающий в журнал сообщения hello триггера концентратора событий hello.

* [C#](#triggercsharp)
* [F#](#triggerfsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>Пример триггера на языке C# #

```cs
using System;

public static void Run(string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

Вы также можете получать события hello в виде [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) объект, который предоставляет доступ к метаданным toohello событий.

```cs
#r "Microsoft.ServiceBus"
using System.Text;
using Microsoft.ServiceBus.Messaging;

public static void Run(EventData myEventHubMessage, TraceWriter log)
{
    log.Info($"{Encoding.UTF8.GetString(myEventHubMessage.GetBytes())}");
}
```

tooreceive событий в пакете, изменить сигнатуру метода hello слишком`string[]` или `EventData[]`.

```cs
public static void Run(string[] eventHubMessages, TraceWriter log)
{
    foreach (var message in eventHubMessages)
    {
        log.Info($"C# Event Hub trigger function processed a message: {message}");
    }
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a>Пример триггера на языке F# #

```fsharp
let Run(myEventHubMessage: string, log: TraceWriter) =
    log.Info(sprintf "F# eventhub trigger function processed work item: %s" myEventHubMessage)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a>Пример триггера для Node.js

```javascript
module.exports = function (context, myEventHubMessage) {
    context.log('Node.js eventhub trigger function processed work item', myEventHubMessage);    
    context.done();
};
```

<a name="output"></a>

## <a name="event-hubs-output-binding"></a>Выходная привязка концентраторов событий
Используйте hello концентраторов событий вывода toowrite привязки событий событие tooan концентратора поток событий. Необходимо иметь разрешение send tooan концентратора событий toowrite tooit события.

Hello вывода привязка использует следующий объект JSON в hello hello `bindings` массив function.json:

```json
{
    "type": "eventHub",
    "name": "<Name of output parameter in function signature>",
    "path": "<Name of event hub>",
    "connection": "<Name of app setting with connection string - see below>"
    "direction": "out"
}
```

`connection`должно быть именем hello Настройка приложения, содержащий пространство имен hello соединения строки toohello концентратора событий по.
Скопируйте эту строку подключения, нажав hello **сведения о соединении** кнопки для hello *имен*, не hello концентратора событий сам. Это строка соединения должна иметь разрешения send toosend сообщение hello toohello поток событий.

## <a name="output-usage"></a>Использование выходной привязки
В этом разделе показано, как toouse вывода привязки в коде функция концентраторов событий.

Концентратор событий toohello настроен сообщения могут выводиться с hello следующие типы параметров:

* `out string`
* `ICollector<string>`(toooutput несколько сообщений)
* `IAsyncCollector<string>` (асинхронная версия `ICollector<T>`).

<a name="outputsample"></a>

## <a name="output-sample"></a>Пример выходной привязки
Предположим, что имеется следующее hello концентраторов событий вывода привязки в hello `bindings` массив function.json:

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

См. пример hello зависящие от языка, который записывает поток даже toohello событий.

* [C#](#outcsharp)
* [F#](#outfsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Пример выходной привязки для языка C# #

```cs
using System;

public static void Run(TimerInfo myTimer, out string outputEventHubMessage, TraceWriter log)
{
    String msg = $"TimerTriggerCSharp1 executed at: {DateTime.Now}";
    log.Verbose(msg);   
    outputEventHubMessage = msg;
}
```

Или toocreate несколько сообщений:

```cs
public static void Run(TimerInfo myTimer, ICollector<string> outputEventHubMessage, TraceWriter log)
{
    string message = $"Event Hub message created at: {DateTime.Now}";
    log.Info(message);
    outputEventHubMessage.Add("1 " + message);
    outputEventHubMessage.Add("2 " + message);
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a>Пример выходной привязки для языка F# #

```fsharp
let Run(myTimer: TimerInfo, outputEventHubMessage: byref<string>, log: TraceWriter) =
    let msg = sprintf "TimerTriggerFSharp1 executed at: %s" DateTime.Now.ToString()
    log.Verbose(msg);
    outputEventHubMessage <- msg;
```

<a name="outnodejs"></a>

### <a name="output-sample-for-nodejs"></a>Пример выходной привязки для Node.js

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();
    context.log('Event Hub message created at: ', timeStamp);   
    context.bindings.outputEventHubMessage = "Event Hub message created at: " + timeStamp;
    context.done();
};
```

Или toosend несколько сообщений

```javascript
module.exports = function(context) {
    var timeStamp = new Date().toISOString();
    var message = 'Event Hub message created at: ' + timeStamp;

    context.bindings.outputEventHubMessage = [];

    context.bindings.outputEventHubMessage.push("1 " + message);
    context.bindings.outputEventHubMessage.push("2 " + message);
    context.done();
};
```

## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
