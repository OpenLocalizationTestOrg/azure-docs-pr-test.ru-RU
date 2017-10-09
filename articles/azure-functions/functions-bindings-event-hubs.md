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
# <a name="azure-functions-event-hubs-bindings"></a><span data-ttu-id="7cc0d-104">Привязки концентраторов событий функций Azure</span><span class="sxs-lookup"><span data-stu-id="7cc0d-104">Azure Functions Event Hubs bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="7cc0d-105">В этой статье объясняется, как tooconfigure и использовать [концентраторов событий Azure](../event-hubs/event-hubs-what-is-event-hubs.md) привязки для функций Azure.</span><span class="sxs-lookup"><span data-stu-id="7cc0d-105">This article explains how tooconfigure and use [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) bindings for Azure Functions.</span></span>
<span data-ttu-id="7cc0d-106">Функции Azure поддерживают привязки триггера и выходные привязки для концентраторов событий Azure.</span><span class="sxs-lookup"><span data-stu-id="7cc0d-106">Azure Functions supports trigger and output bindings for Event Hubs.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="7cc0d-107">При наличии новых концентраторов событий tooAzure разделе hello [Обзор концентраторов событий](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="7cc0d-107">If you are new tooAzure Event Hubs, see hello [Event Hubs overview](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

<a name="trigger"></a>

## <a name="event-hub-trigger"></a><span data-ttu-id="7cc0d-108">Триггер концентратора событий</span><span class="sxs-lookup"><span data-stu-id="7cc0d-108">Event hub trigger</span></span>
<span data-ttu-id="7cc0d-109">Концентраторы событий используйте hello Активация события tooan toorespond, отправленных поток tooan события концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="7cc0d-109">Use hello Event Hubs trigger toorespond tooan event sent tooan event hub event stream.</span></span> <span data-ttu-id="7cc0d-110">Необходимо иметь доступ на чтение toohello события концентратора tooset копирование триггера hello.</span><span class="sxs-lookup"><span data-stu-id="7cc0d-110">You must have read access toohello event hub tooset up hello trigger.</span></span>

<span data-ttu-id="7cc0d-111">триггер функции Hello концентраторов событий использует следующий объект JSON в hello hello `bindings` массив function.json:</span><span class="sxs-lookup"><span data-stu-id="7cc0d-111">hello Event Hubs function trigger uses hello following JSON object in hello `bindings` array of function.json:</span></span>

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

<span data-ttu-id="7cc0d-112">`consumerGroup`является hello необязательное свойство, используемое tooset [группы потребителей](../event-hubs/event-hubs-features.md#event-consumers) используется toosubscribe tooevents в концентраторе hello.</span><span class="sxs-lookup"><span data-stu-id="7cc0d-112">`consumerGroup` is an optional property used tooset hello [consumer group](../event-hubs/event-hubs-features.md#event-consumers) used toosubscribe tooevents in hello hub.</span></span> <span data-ttu-id="7cc0d-113">Если не указано, hello `$Default` используется группа потребителей.</span><span class="sxs-lookup"><span data-stu-id="7cc0d-113">If omitted, hello `$Default` consumer group is used.</span></span>  
<span data-ttu-id="7cc0d-114">`connection`должно быть именем hello Настройка приложения, содержащий пространство имен hello соединения строки toohello концентратора событий по.</span><span class="sxs-lookup"><span data-stu-id="7cc0d-114">`connection` must be hello name of an app setting that contains hello connection string toohello event hub's namespace.</span></span>
<span data-ttu-id="7cc0d-115">Скопируйте эту строку подключения, нажав hello **сведения о соединении** кнопки для hello *имен*, не hello концентратора событий сам.</span><span class="sxs-lookup"><span data-stu-id="7cc0d-115">Copy this connection string by clicking hello **Connection Information** button for hello *namespace*, not hello event hub itself.</span></span> <span data-ttu-id="7cc0d-116">Эта строка подключения должна иметь по крайней мере чтение разрешений tooactivate hello триггера.</span><span class="sxs-lookup"><span data-stu-id="7cc0d-116">This connection string must have at least read permissions tooactivate hello trigger.</span></span>

<span data-ttu-id="7cc0d-117">[Дополнительные параметры](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) могут предоставляться в host.json toofurther файл точной настройки триггеры концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="7cc0d-117">[Additional settings](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) can be provided in a host.json file toofurther fine tune Event Hubs triggers.</span></span>  

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="7cc0d-118">Использование триггера</span><span class="sxs-lookup"><span data-stu-id="7cc0d-118">Trigger usage</span></span>
<span data-ttu-id="7cc0d-119">При запуске функции концентраторов событий триггера приветственное сообщение, которое запускает его передается функции hello как строка.</span><span class="sxs-lookup"><span data-stu-id="7cc0d-119">When an Event Hubs trigger function is triggered, hello message that triggers it is passed into hello function as a string.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="7cc0d-120">Пример триггера</span><span class="sxs-lookup"><span data-stu-id="7cc0d-120">Trigger sample</span></span>
<span data-ttu-id="7cc0d-121">Предположим, что имеется следующий концентраторов событий триггера в hello hello `bindings` массив function.json:</span><span class="sxs-lookup"><span data-stu-id="7cc0d-121">Suppose you have hello following Event Hubs trigger in hello `bindings` array of function.json:</span></span>

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```

<span data-ttu-id="7cc0d-122">См. Образец hello конкретного языка, записывающий в журнал сообщения hello триггера концентратора событий hello.</span><span class="sxs-lookup"><span data-stu-id="7cc0d-122">See hello language-specific sample that logs hello message body of hello event hub trigger.</span></span>

* [<span data-ttu-id="7cc0d-123">C#</span><span class="sxs-lookup"><span data-stu-id="7cc0d-123">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="7cc0d-124">F#</span><span class="sxs-lookup"><span data-stu-id="7cc0d-124">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="7cc0d-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="7cc0d-125">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="7cc0d-126">Пример триггера на языке C#</span><span class="sxs-lookup"><span data-stu-id="7cc0d-126">Trigger sample in C#</span></span> #

```cs
using System;

public static void Run(string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

<span data-ttu-id="7cc0d-127">Вы также можете получать события hello в виде [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) объект, который предоставляет доступ к метаданным toohello событий.</span><span class="sxs-lookup"><span data-stu-id="7cc0d-127">You can also receive hello event as an [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) object, which gives you access toohello event metadata.</span></span>

```cs
#r "Microsoft.ServiceBus"
using System.Text;
using Microsoft.ServiceBus.Messaging;

public static void Run(EventData myEventHubMessage, TraceWriter log)
{
    log.Info($"{Encoding.UTF8.GetString(myEventHubMessage.GetBytes())}");
}
```

<span data-ttu-id="7cc0d-128">tooreceive событий в пакете, изменить сигнатуру метода hello слишком`string[]` или `EventData[]`.</span><span class="sxs-lookup"><span data-stu-id="7cc0d-128">tooreceive events in a batch, change hello method signature too`string[]` or `EventData[]`.</span></span>

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

### <a name="trigger-sample-in-f"></a><span data-ttu-id="7cc0d-129">Пример триггера на языке F#</span><span class="sxs-lookup"><span data-stu-id="7cc0d-129">Trigger sample in F#</span></span> #

```fsharp
let Run(myEventHubMessage: string, log: TraceWriter) =
    log.Info(sprintf "F# eventhub trigger function processed work item: %s" myEventHubMessage)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="7cc0d-130">Пример триггера для Node.js</span><span class="sxs-lookup"><span data-stu-id="7cc0d-130">Trigger sample in Node.js</span></span>

```javascript
module.exports = function (context, myEventHubMessage) {
    context.log('Node.js eventhub trigger function processed work item', myEventHubMessage);    
    context.done();
};
```

<a name="output"></a>

## <a name="event-hubs-output-binding"></a><span data-ttu-id="7cc0d-131">Выходная привязка концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="7cc0d-131">Event Hubs output binding</span></span>
<span data-ttu-id="7cc0d-132">Используйте hello концентраторов событий вывода toowrite привязки событий событие tooan концентратора поток событий.</span><span class="sxs-lookup"><span data-stu-id="7cc0d-132">Use hello Event Hubs output binding toowrite events tooan event hub event stream.</span></span> <span data-ttu-id="7cc0d-133">Необходимо иметь разрешение send tooan концентратора событий toowrite tooit события.</span><span class="sxs-lookup"><span data-stu-id="7cc0d-133">You must have send permission tooan event hub toowrite events tooit.</span></span>

<span data-ttu-id="7cc0d-134">Hello вывода привязка использует следующий объект JSON в hello hello `bindings` массив function.json:</span><span class="sxs-lookup"><span data-stu-id="7cc0d-134">hello output binding uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "<Name of output parameter in function signature>",
    "path": "<Name of event hub>",
    "connection": "<Name of app setting with connection string - see below>"
    "direction": "out"
}
```

<span data-ttu-id="7cc0d-135">`connection`должно быть именем hello Настройка приложения, содержащий пространство имен hello соединения строки toohello концентратора событий по.</span><span class="sxs-lookup"><span data-stu-id="7cc0d-135">`connection` must be hello name of an app setting that contains hello connection string toohello event hub's namespace.</span></span>
<span data-ttu-id="7cc0d-136">Скопируйте эту строку подключения, нажав hello **сведения о соединении** кнопки для hello *имен*, не hello концентратора событий сам.</span><span class="sxs-lookup"><span data-stu-id="7cc0d-136">Copy this connection string by clicking hello **Connection Information** button for hello *namespace*, not hello event hub itself.</span></span> <span data-ttu-id="7cc0d-137">Это строка соединения должна иметь разрешения send toosend сообщение hello toohello поток событий.</span><span class="sxs-lookup"><span data-stu-id="7cc0d-137">This connection string must have send permissions toosend hello message toohello event stream.</span></span>

## <a name="output-usage"></a><span data-ttu-id="7cc0d-138">Использование выходной привязки</span><span class="sxs-lookup"><span data-stu-id="7cc0d-138">Output usage</span></span>
<span data-ttu-id="7cc0d-139">В этом разделе показано, как toouse вывода привязки в коде функция концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="7cc0d-139">This section shows you how toouse your Event Hubs output binding in your function code.</span></span>

<span data-ttu-id="7cc0d-140">Концентратор событий toohello настроен сообщения могут выводиться с hello следующие типы параметров:</span><span class="sxs-lookup"><span data-stu-id="7cc0d-140">You can output messages toohello configured event hub with hello following parameter types:</span></span>

* `out string`
* <span data-ttu-id="7cc0d-141">`ICollector<string>`(toooutput несколько сообщений)</span><span class="sxs-lookup"><span data-stu-id="7cc0d-141">`ICollector<string>` (toooutput multiple messages)</span></span>
* <span data-ttu-id="7cc0d-142">`IAsyncCollector<string>` (асинхронная версия `ICollector<T>`).</span><span class="sxs-lookup"><span data-stu-id="7cc0d-142">`IAsyncCollector<string>` (async version of `ICollector<T>`)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="7cc0d-143">Пример выходной привязки</span><span class="sxs-lookup"><span data-stu-id="7cc0d-143">Output sample</span></span>
<span data-ttu-id="7cc0d-144">Предположим, что имеется следующее hello концентраторов событий вывода привязки в hello `bindings` массив function.json:</span><span class="sxs-lookup"><span data-stu-id="7cc0d-144">Suppose you have hello following Event Hubs output binding in hello `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

<span data-ttu-id="7cc0d-145">См. пример hello зависящие от языка, который записывает поток даже toohello событий.</span><span class="sxs-lookup"><span data-stu-id="7cc0d-145">See hello language-specific sample that writes an event toohello even stream.</span></span>

* [<span data-ttu-id="7cc0d-146">C#</span><span class="sxs-lookup"><span data-stu-id="7cc0d-146">C#</span></span>](#outcsharp)
* [<span data-ttu-id="7cc0d-147">F#</span><span class="sxs-lookup"><span data-stu-id="7cc0d-147">F#</span></span>](#outfsharp)
* [<span data-ttu-id="7cc0d-148">Node.js</span><span class="sxs-lookup"><span data-stu-id="7cc0d-148">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="7cc0d-149">Пример выходной привязки для языка C#</span><span class="sxs-lookup"><span data-stu-id="7cc0d-149">Output sample in C#</span></span> #

```cs
using System;

public static void Run(TimerInfo myTimer, out string outputEventHubMessage, TraceWriter log)
{
    String msg = $"TimerTriggerCSharp1 executed at: {DateTime.Now}";
    log.Verbose(msg);   
    outputEventHubMessage = msg;
}
```

<span data-ttu-id="7cc0d-150">Или toocreate несколько сообщений:</span><span class="sxs-lookup"><span data-stu-id="7cc0d-150">Or, toocreate multiple messages:</span></span>

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

### <a name="output-sample-in-f"></a><span data-ttu-id="7cc0d-151">Пример выходной привязки для языка F#</span><span class="sxs-lookup"><span data-stu-id="7cc0d-151">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, outputEventHubMessage: byref<string>, log: TraceWriter) =
    let msg = sprintf "TimerTriggerFSharp1 executed at: %s" DateTime.Now.ToString()
    log.Verbose(msg);
    outputEventHubMessage <- msg;
```

<a name="outnodejs"></a>

### <a name="output-sample-for-nodejs"></a><span data-ttu-id="7cc0d-152">Пример выходной привязки для Node.js</span><span class="sxs-lookup"><span data-stu-id="7cc0d-152">Output sample for Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();
    context.log('Event Hub message created at: ', timeStamp);   
    context.bindings.outputEventHubMessage = "Event Hub message created at: " + timeStamp;
    context.done();
};
```

<span data-ttu-id="7cc0d-153">Или toosend несколько сообщений</span><span class="sxs-lookup"><span data-stu-id="7cc0d-153">Or, toosend multiple messages,</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="7cc0d-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7cc0d-154">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
