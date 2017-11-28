---
title: "Привязки концентраторов событий Функций Azure | Документация Майкрософт"
description: "Узнайте, как использовать привязки концентраторов событий Azure в функциях Azure."
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
ms.openlocfilehash: 19021bef8b7156b3049f43b0275c0ed0c6b22514
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-event-hubs-bindings"></a><span data-ttu-id="59106-104">Привязки концентраторов событий функций Azure</span><span class="sxs-lookup"><span data-stu-id="59106-104">Azure Functions Event Hubs bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="59106-105">Здесь объясняется, как настроить и использовать привязки [концентраторов событий Azure](../event-hubs/event-hubs-what-is-event-hubs.md) для Функций Azure.</span><span class="sxs-lookup"><span data-stu-id="59106-105">This article explains how to configure and use [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) bindings for Azure Functions.</span></span>
<span data-ttu-id="59106-106">Функции Azure поддерживают привязки триггера и выходные привязки для концентраторов событий Azure.</span><span class="sxs-lookup"><span data-stu-id="59106-106">Azure Functions supports trigger and output bindings for Event Hubs.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="59106-107">Если вы еще не работали с концентраторами событий Azure, ознакомьтесь с [их обзором](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="59106-107">If you are new to Azure Event Hubs, see the [Event Hubs overview](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

<a name="trigger"></a>

## <a name="event-hub-trigger"></a><span data-ttu-id="59106-108">Триггер концентратора событий</span><span class="sxs-lookup"><span data-stu-id="59106-108">Event hub trigger</span></span>
<span data-ttu-id="59106-109">Используйте триггер концентраторов событий Azure для ответа на событие, отправленное в поток событий концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="59106-109">Use the Event Hubs trigger to respond to an event sent to an event hub event stream.</span></span> <span data-ttu-id="59106-110">Чтобы настроить триггер, необходимо иметь доступ для чтения к концентратору событий.</span><span class="sxs-lookup"><span data-stu-id="59106-110">You must have read access to the event hub to set up the trigger.</span></span>

<span data-ttu-id="59106-111">Триггер концентратора событий для функции использует следующий объект JSON в массиве `bindings` файла function.json:</span><span class="sxs-lookup"><span data-stu-id="59106-111">The Event Hubs function trigger uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHubTrigger",
    "name": "<Name of trigger parameter in function signature>",
    "direction": "in",
    "path": "<Name of the event hub>",
    "consumerGroup": "Consumer group to use - see below",
    "connection": "<Name of app setting with connection string - see below>"
}
```

<span data-ttu-id="59106-112">`consumerGroup` — необязательное свойство, которое используется для задания [группы потребителей](../event-hubs/event-hubs-features.md#event-consumers), используемой для подписки на события в концентраторе.</span><span class="sxs-lookup"><span data-stu-id="59106-112">`consumerGroup` is an optional property used to set the [consumer group](../event-hubs/event-hubs-features.md#event-consumers) used to subscribe to events in the hub.</span></span> <span data-ttu-id="59106-113">Если аргумент опущен, используется группа потребителей `$Default`.</span><span class="sxs-lookup"><span data-stu-id="59106-113">If omitted, the `$Default` consumer group is used.</span></span>  
<span data-ttu-id="59106-114">`connection` — имя параметра приложения, содержащего строку подключения к пространству имен концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="59106-114">`connection` must be the name of an app setting that contains the connection string to the event hub's namespace.</span></span>
<span data-ttu-id="59106-115">Скопируйте эту строку подключения, нажав кнопку **Сведения о подключении** для *пространства имен*, а не сам концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="59106-115">Copy this connection string by clicking the **Connection Information** button for the *namespace*, not the event hub itself.</span></span> <span data-ttu-id="59106-116">Для активации триггера эта строка подключения должна обладать, по крайней мере, правами на чтение.</span><span class="sxs-lookup"><span data-stu-id="59106-116">This connection string must have at least read permissions to activate the trigger.</span></span>

<span data-ttu-id="59106-117">[Дополнительные параметры](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) можно указать в файле host.json для дальнейшей настройки триггеров концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="59106-117">[Additional settings](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) can be provided in a host.json file to further fine tune Event Hubs triggers.</span></span>  

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="59106-118">Использование триггера</span><span class="sxs-lookup"><span data-stu-id="59106-118">Trigger usage</span></span>
<span data-ttu-id="59106-119">При активации функции триггера концентратора событий сообщение, вызвавшее активацию, передается в функцию в качестве строки.</span><span class="sxs-lookup"><span data-stu-id="59106-119">When an Event Hubs trigger function is triggered, the message that triggers it is passed into the function as a string.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="59106-120">Пример триггера</span><span class="sxs-lookup"><span data-stu-id="59106-120">Trigger sample</span></span>
<span data-ttu-id="59106-121">Предположим, что у вас есть следующий триггер концентраторов событий в массиве `bindings` файла function.json:</span><span class="sxs-lookup"><span data-stu-id="59106-121">Suppose you have the following Event Hubs trigger in the `bindings` array of function.json:</span></span>

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```

<span data-ttu-id="59106-122">Ознакомьтесь с примером для конкретного языка, записывающим текст сообщения триггера концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="59106-122">See the language-specific sample that logs the message body of the event hub trigger.</span></span>

* [<span data-ttu-id="59106-123">C#</span><span class="sxs-lookup"><span data-stu-id="59106-123">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="59106-124">F#</span><span class="sxs-lookup"><span data-stu-id="59106-124">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="59106-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="59106-125">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="59106-126">Пример триггера на языке C#</span><span class="sxs-lookup"><span data-stu-id="59106-126">Trigger sample in C#</span></span> #

```cs
using System;

public static void Run(string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

<span data-ttu-id="59106-127">Вы также можете получить событие как объект [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata), который предоставляет доступ к метаданным события.</span><span class="sxs-lookup"><span data-stu-id="59106-127">You can also receive the event as an [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) object, which gives you access to the event metadata.</span></span>

```cs
#r "Microsoft.ServiceBus"
using System.Text;
using Microsoft.ServiceBus.Messaging;

public static void Run(EventData myEventHubMessage, TraceWriter log)
{
    log.Info($"{Encoding.UTF8.GetString(myEventHubMessage.GetBytes())}");
}
```

<span data-ttu-id="59106-128">Чтобы получить пакет событий, измените сигнатуру метода на `string[]` или `EventData[]`.</span><span class="sxs-lookup"><span data-stu-id="59106-128">To receive events in a batch, change the method signature to `string[]` or `EventData[]`.</span></span>

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

### <a name="trigger-sample-in-f"></a><span data-ttu-id="59106-129">Пример триггера на языке F#</span><span class="sxs-lookup"><span data-stu-id="59106-129">Trigger sample in F#</span></span> #

```fsharp
let Run(myEventHubMessage: string, log: TraceWriter) =
    log.Info(sprintf "F# eventhub trigger function processed work item: %s" myEventHubMessage)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="59106-130">Пример триггера для Node.js</span><span class="sxs-lookup"><span data-stu-id="59106-130">Trigger sample in Node.js</span></span>

```javascript
module.exports = function (context, myEventHubMessage) {
    context.log('Node.js eventhub trigger function processed work item', myEventHubMessage);    
    context.done();
};
```

<a name="output"></a>

## <a name="event-hubs-output-binding"></a><span data-ttu-id="59106-131">Выходная привязка концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="59106-131">Event Hubs output binding</span></span>
<span data-ttu-id="59106-132">Используйте выходную привязку концентратора событий для записи событий в поток событий концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="59106-132">Use the Event Hubs output binding to write events to an event hub event stream.</span></span> <span data-ttu-id="59106-133">Чтобы записывать события в концентратор событий, необходимо иметь разрешение на оправку в него событий.</span><span class="sxs-lookup"><span data-stu-id="59106-133">You must have send permission to an event hub to write events to it.</span></span>

<span data-ttu-id="59106-134">Выходная привязка использует следующий объект JSON в массиве `bindings` файла function.json:</span><span class="sxs-lookup"><span data-stu-id="59106-134">The output binding uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "<Name of output parameter in function signature>",
    "path": "<Name of event hub>",
    "connection": "<Name of app setting with connection string - see below>"
    "direction": "out"
}
```

<span data-ttu-id="59106-135">`connection` — имя параметра приложения, содержащего строку подключения к пространству имен концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="59106-135">`connection` must be the name of an app setting that contains the connection string to the event hub's namespace.</span></span>
<span data-ttu-id="59106-136">Скопируйте эту строку подключения, нажав кнопку **Сведения о подключении** для *пространства имен*, а не сам концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="59106-136">Copy this connection string by clicking the **Connection Information** button for the *namespace*, not the event hub itself.</span></span> <span data-ttu-id="59106-137">Чтобы отправлять сообщения в поток событий, эта строка подключения должна иметь разрешения на отправку.</span><span class="sxs-lookup"><span data-stu-id="59106-137">This connection string must have send permissions to send the message to the event stream.</span></span>

## <a name="output-usage"></a><span data-ttu-id="59106-138">Использование выходной привязки</span><span class="sxs-lookup"><span data-stu-id="59106-138">Output usage</span></span>
<span data-ttu-id="59106-139">В этом разделе показано, как использовать выходную привязку концентраторов событий в коде функции.</span><span class="sxs-lookup"><span data-stu-id="59106-139">This section shows you how to use your Event Hubs output binding in your function code.</span></span>

<span data-ttu-id="59106-140">Можно выводить сообщения в настроенный концентратор событий со следующими типами параметров.</span><span class="sxs-lookup"><span data-stu-id="59106-140">You can output messages to the configured event hub with the following parameter types:</span></span>

* `out string`
* <span data-ttu-id="59106-141">`ICollector<string>` (для вывода нескольких сообщений).</span><span class="sxs-lookup"><span data-stu-id="59106-141">`ICollector<string>` (to output multiple messages)</span></span>
* <span data-ttu-id="59106-142">`IAsyncCollector<string>` (асинхронная версия `ICollector<T>`).</span><span class="sxs-lookup"><span data-stu-id="59106-142">`IAsyncCollector<string>` (async version of `ICollector<T>`)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="59106-143">Пример выходной привязки</span><span class="sxs-lookup"><span data-stu-id="59106-143">Output sample</span></span>
<span data-ttu-id="59106-144">Предположим, что у вас есть следующая выходная привязка концентраторов событий в массиве `bindings` файла function.json:</span><span class="sxs-lookup"><span data-stu-id="59106-144">Suppose you have the following Event Hubs output binding in the `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

<span data-ttu-id="59106-145">Ознакомьтесь с примером для конкретного языка, записывающим событие в поток событий.</span><span class="sxs-lookup"><span data-stu-id="59106-145">See the language-specific sample that writes an event to the even stream.</span></span>

* [<span data-ttu-id="59106-146">C#</span><span class="sxs-lookup"><span data-stu-id="59106-146">C#</span></span>](#outcsharp)
* [<span data-ttu-id="59106-147">F#</span><span class="sxs-lookup"><span data-stu-id="59106-147">F#</span></span>](#outfsharp)
* [<span data-ttu-id="59106-148">Node.js</span><span class="sxs-lookup"><span data-stu-id="59106-148">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="59106-149">Пример выходной привязки для языка C#</span><span class="sxs-lookup"><span data-stu-id="59106-149">Output sample in C#</span></span> #

```cs
using System;

public static void Run(TimerInfo myTimer, out string outputEventHubMessage, TraceWriter log)
{
    String msg = $"TimerTriggerCSharp1 executed at: {DateTime.Now}";
    log.Verbose(msg);   
    outputEventHubMessage = msg;
}
```

<span data-ttu-id="59106-150">Создание нескольких сообщений:</span><span class="sxs-lookup"><span data-stu-id="59106-150">Or, to create multiple messages:</span></span>

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

### <a name="output-sample-in-f"></a><span data-ttu-id="59106-151">Пример выходной привязки для языка F#</span><span class="sxs-lookup"><span data-stu-id="59106-151">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, outputEventHubMessage: byref<string>, log: TraceWriter) =
    let msg = sprintf "TimerTriggerFSharp1 executed at: %s" DateTime.Now.ToString()
    log.Verbose(msg);
    outputEventHubMessage <- msg;
```

<a name="outnodejs"></a>

### <a name="output-sample-for-nodejs"></a><span data-ttu-id="59106-152">Пример выходной привязки для Node.js</span><span class="sxs-lookup"><span data-stu-id="59106-152">Output sample for Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();
    context.log('Event Hub message created at: ', timeStamp);   
    context.bindings.outputEventHubMessage = "Event Hub message created at: " + timeStamp;
    context.done();
};
```

<span data-ttu-id="59106-153">Отправка нескольких сообщений:</span><span class="sxs-lookup"><span data-stu-id="59106-153">Or, to send multiple messages,</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="59106-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="59106-154">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
