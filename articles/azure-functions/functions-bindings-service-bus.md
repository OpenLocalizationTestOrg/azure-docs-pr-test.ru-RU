---
title: "Триггеры и привязки служебной шины в Функциях Azure | Документация Майкрософт"
description: "Узнайте, как использовать триггеры и привязки служебной шины Azure в функциях Azure."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "функции azure, функции, обработка событий, динамические вычисления, независимая архитектура"
ms.assetid: daedacf0-6546-4355-a65c-50873e74f66b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/01/2017
ms.author: glenga
ms.openlocfilehash: b3ee306cd37ebf88dc9369ccc2dc6c670557fd5a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-service-bus-bindings"></a><span data-ttu-id="855d3-104">Привязки служебной шины в Функциях Azure</span><span class="sxs-lookup"><span data-stu-id="855d3-104">Azure Functions Service Bus bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="855d3-105">В этой статье рассматривается настройка привязок служебной шины Azure в Функциях Azure, а также работа с ними.</span><span class="sxs-lookup"><span data-stu-id="855d3-105">This article explains how to configure and work with Azure Service Bus bindings in Azure Functions.</span></span> 

<span data-ttu-id="855d3-106">Функции Azure поддерживают привязки триггера и выходные привязки для очередей и разделов служебной шины.</span><span class="sxs-lookup"><span data-stu-id="855d3-106">Azure Functions supports trigger and output bindings for Service Bus queues and topics.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="service-bus-trigger"></a><span data-ttu-id="855d3-107">Триггер служебной шины</span><span class="sxs-lookup"><span data-stu-id="855d3-107">Service Bus trigger</span></span>
<span data-ttu-id="855d3-108">Используйте триггер служебной шины для ответа на сообщения из очереди или раздела служебной шины.</span><span class="sxs-lookup"><span data-stu-id="855d3-108">Use the Service Bus trigger to respond to messages from a Service Bus queue or topic.</span></span> 

<span data-ttu-id="855d3-109">Триггеры очередей и разделов служебной шины определяются с помощью следующих объектов JSON в массиве `bindings` function.json:</span><span class="sxs-lookup"><span data-stu-id="855d3-109">The Service Bus queue and topic triggers are defined by the following JSON objects in the `bindings` array of function.json:</span></span>

* <span data-ttu-id="855d3-110">Триггер *очереди*:</span><span class="sxs-lookup"><span data-stu-id="855d3-110">*queue* trigger:</span></span>

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "queueName" : "<Name of the queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

* <span data-ttu-id="855d3-111">Триггер *раздела*:</span><span class="sxs-lookup"><span data-stu-id="855d3-111">*topic* trigger:</span></span>

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "topicName" : "<Name of the topic>",
        "subscriptionName" : "<Name of the subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

<span data-ttu-id="855d3-112">Обратите внимание на следующее.</span><span class="sxs-lookup"><span data-stu-id="855d3-112">Note the following:</span></span>

* <span data-ttu-id="855d3-113">Для `connection` [создайте в приложении-функции параметр приложения](functions-how-to-use-azure-function-app-settings.md), содержащий строку подключения к пространству имен служебной шины, а затем укажите имя этого параметра в свойстве `connection` для триггера.</span><span class="sxs-lookup"><span data-stu-id="855d3-113">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains the connection string to your Service Bus namespace, then specify the name of the app setting in the `connection` property in your trigger.</span></span> <span data-ttu-id="855d3-114">Чтобы получить строку подключения, следуйте инструкциям, указанным в разделе [Получение учетных данных управления](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span><span class="sxs-lookup"><span data-stu-id="855d3-114">You obtain the connection string by following the steps shown at [Obtain the management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="855d3-115">Строка подключения указывается для пространства имен служебной шины, и она не должна ограничиваться определенной очередью или разделом.</span><span class="sxs-lookup"><span data-stu-id="855d3-115">The connection string must be for a Service Bus namespace, not limited to a specific queue or topic.</span></span>
  <span data-ttu-id="855d3-116">Если оставить свойство `connection` пустым, триггер предполагает, что в параметре приложения `AzureWebJobsServiceBus` указывается строка подключения служебной шины по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="855d3-116">If you leave `connection` empty, the trigger assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="855d3-117">Для свойства `accessRights` возможны такие значения, как `manage` и `listen`.</span><span class="sxs-lookup"><span data-stu-id="855d3-117">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="855d3-118">Значение по умолчанию — `manage`. Это означает, что у свойства `connection` есть разрешение на **управление**.</span><span class="sxs-lookup"><span data-stu-id="855d3-118">The default is `manage`, which indicates that the `connection` has the **Manage** permission.</span></span> <span data-ttu-id="855d3-119">При использовании строки подключения без разрешения на **управление**, задайте для свойства `accessRights` значение `listen`.</span><span class="sxs-lookup"><span data-stu-id="855d3-119">If you use a connection string that does not have the **Manage** permission, set `accessRights` to `listen`.</span></span> <span data-ttu-id="855d3-120">В противном случае выполнение операций, для которых требуются права на управление, в среде выполнения Функций Azure может завершиться ошибкой.</span><span class="sxs-lookup"><span data-stu-id="855d3-120">Otherwise, the Functions runtime might fail trying to do operations that require manage rights.</span></span>

## <a name="trigger-behavior"></a><span data-ttu-id="855d3-121">Поведение триггера</span><span class="sxs-lookup"><span data-stu-id="855d3-121">Trigger behavior</span></span>
* <span data-ttu-id="855d3-122">**Однопоточная обработка**. По умолчанию в среде выполнения Функций одновременно обрабатываются несколько сообщений очереди.</span><span class="sxs-lookup"><span data-stu-id="855d3-122">**Single-threading** - By default, the Functions runtime processes multiple messages concurrently.</span></span> <span data-ttu-id="855d3-123">Чтобы среда выполнения обрабатывала в любой момент времени только одно сообщение очереди или раздела, для свойства `serviceBus.maxConcurrentCalls` в файле *host.json* нужно задать значение 1.</span><span class="sxs-lookup"><span data-stu-id="855d3-123">To direct the runtime to process only a single queue or topic message at a time, set `serviceBus.maxConcurrentCalls` to 1 in *host.json*.</span></span> 
  <span data-ttu-id="855d3-124">Сведения о файле *host.json* см. в разделе [Структура папок](functions-reference.md#folder-structure) и статье [host.json](https://github .com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="855d3-124">For information about *host.json*, see [Folder Structure](functions-reference.md#folder-structure) and [host.json](https://github .com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>
* <span data-ttu-id="855d3-125">**Обработка подозрительных сообщений.** В служебной шине выполняется собственная обработка подозрительных сообщений, которую нельзя контролировать или настраивать с помощью конфигурации или кода Функций Azure.</span><span class="sxs-lookup"><span data-stu-id="855d3-125">**Poison message handling** - Service Bus does its own poison message handling, which can't be controlled or configured in Azure Functions configuration or code.</span></span> 
* <span data-ttu-id="855d3-126">**Поведение PeekLock.** Среда выполнения Функций получает сообщение в [режиме `PeekLock`](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) и вызывает для сообщения метод `Complete`, если функция выполнена успешно, или метод `Abandon` в случае сбоя.</span><span class="sxs-lookup"><span data-stu-id="855d3-126">**PeekLock behavior** - The Functions runtime receives a message in [`PeekLock` mode](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) and calls `Complete` on the message if the function finishes successfully, or calls `Abandon` if the function fails.</span></span> 
  <span data-ttu-id="855d3-127">Если функция выполняется дольше времени ожидания `PeekLock` , блокировка возобновляется автоматически.</span><span class="sxs-lookup"><span data-stu-id="855d3-127">If the function runs longer than the `PeekLock` timeout, the lock is automatically renewed.</span></span>

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="855d3-128">Использование триггера</span><span class="sxs-lookup"><span data-stu-id="855d3-128">Trigger usage</span></span>
<span data-ttu-id="855d3-129">В этом разделе показано, как использовать триггер служебной шины в коде функции.</span><span class="sxs-lookup"><span data-stu-id="855d3-129">This section shows you how to use your Service Bus trigger in your function code.</span></span> 

<span data-ttu-id="855d3-130">В языке C# и F# сообщение триггера служебной шины можно десериализировать в один из следующих входных типов:</span><span class="sxs-lookup"><span data-stu-id="855d3-130">In C# and F#, the Service Bus trigger message can be deserialized to any of the following input types:</span></span>

* <span data-ttu-id="855d3-131">`string` используется для строковых сообщений.</span><span class="sxs-lookup"><span data-stu-id="855d3-131">`string` - useful for string messages</span></span>
* <span data-ttu-id="855d3-132">`byte[]` используется для двоичных данных.</span><span class="sxs-lookup"><span data-stu-id="855d3-132">`byte[]` - useful for binary data</span></span>
* <span data-ttu-id="855d3-133">Любой [объект](https://msdn.microsoft.com/library/system.object.aspx) используется для сериализованных данных JSON.</span><span class="sxs-lookup"><span data-stu-id="855d3-133">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized data.</span></span>
  <span data-ttu-id="855d3-134">Если объявить пользовательский тип входных данных (например, `CustomType`), Функции Azure попытаются десериализировать данные JSON в указанный тип.</span><span class="sxs-lookup"><span data-stu-id="855d3-134">If you declare a custom input type, such as `CustomType`, Azure Functions tries to deserialize the JSON data into your specified type.</span></span>
* <span data-ttu-id="855d3-135">`BrokeredMessage` предоставляет десериализированное сообщение с методом [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx).</span><span class="sxs-lookup"><span data-stu-id="855d3-135">`BrokeredMessage` - gives you the deserialized message with the [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) method.</span></span>

<span data-ttu-id="855d3-136">В Node.js сообщение триггера служебной шины передается в функцию в качестве строки или объекта JSON.</span><span class="sxs-lookup"><span data-stu-id="855d3-136">In Node.js, the Service Bus trigger message is passed into the function as either a string or JSON object.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="855d3-137">Пример триггера</span><span class="sxs-lookup"><span data-stu-id="855d3-137">Trigger sample</span></span>
<span data-ttu-id="855d3-138">Предположим, что у вас есть следующий файл function.json:</span><span class="sxs-lookup"><span data-stu-id="855d3-138">Suppose you have the following function.json:</span></span>

```json
{
"bindings": [
    {
    "queueName": "testqueue",
    "connection": "MyServiceBusConnection",
    "name": "myQueueItem",
    "type": "serviceBusTrigger",
    "direction": "in"
    }
],
"disabled": false
}
```

<span data-ttu-id="855d3-139">Ознакомьтесь с примером для конкретного языка, обрабатывающим сообщение очереди служебной шины.</span><span class="sxs-lookup"><span data-stu-id="855d3-139">See the language-specific sample that processes a Service Bus queue message.</span></span>

* [<span data-ttu-id="855d3-140">C#</span><span class="sxs-lookup"><span data-stu-id="855d3-140">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="855d3-141">F#</span><span class="sxs-lookup"><span data-stu-id="855d3-141">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="855d3-142">Node.js</span><span class="sxs-lookup"><span data-stu-id="855d3-142">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="855d3-143">Пример триггера на языке C#</span><span class="sxs-lookup"><span data-stu-id="855d3-143">Trigger sample in C#</span></span> #

```cs
public static void Run(string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a><span data-ttu-id="855d3-144">Пример триггера на языке F#</span><span class="sxs-lookup"><span data-stu-id="855d3-144">Trigger sample in F#</span></span> #

```fsharp
let Run(myQueueItem: string, log: TraceWriter) =
    log.Info(sprintf "F# ServiceBus queue trigger function processed message: %s" myQueueItem)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="855d3-145">Пример триггера для Node.js</span><span class="sxs-lookup"><span data-stu-id="855d3-145">Trigger sample in Node.js</span></span>

```javascript
module.exports = function(context, myQueueItem) {
    context.log('Node.js ServiceBus queue trigger function processed message', myQueueItem);
    context.done();
};
```

<a name="output"></a>

## <a name="service-bus-output-binding"></a><span data-ttu-id="855d3-146">Выходная привязка служебной шины</span><span class="sxs-lookup"><span data-stu-id="855d3-146">Service Bus output binding</span></span>
<span data-ttu-id="855d3-147">Выходные данные очереди и раздела служебной шины для функции используют следующие объекты JSON в массиве `bindings` файла function.json:</span><span class="sxs-lookup"><span data-stu-id="855d3-147">The Service Bus queue and topic output for a function use the following JSON objects in the `bindings` array of function.json:</span></span>

* <span data-ttu-id="855d3-148">Выходные данные *очереди*:</span><span class="sxs-lookup"><span data-stu-id="855d3-148">*queue* output:</span></span>

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "queueName" : "<Name of the queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```
* <span data-ttu-id="855d3-149">Выходные данные *раздела*:</span><span class="sxs-lookup"><span data-stu-id="855d3-149">*topic* output:</span></span>

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "topicName" : "<Name of the topic>",
        "subscriptionName" : "<Name of the subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```

<span data-ttu-id="855d3-150">Обратите внимание на следующее.</span><span class="sxs-lookup"><span data-stu-id="855d3-150">Note the following:</span></span>

* <span data-ttu-id="855d3-151">Для `connection` [создайте в приложении-функции параметр приложения](functions-how-to-use-azure-function-app-settings.md), содержащий строку подключения к пространству имен служебной шины, а затем укажите имя этого параметра в свойстве `connection` для выходной привязки.</span><span class="sxs-lookup"><span data-stu-id="855d3-151">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains the connection string to your Service Bus namespace, then specify the name of the app setting in the `connection` property in your output binding.</span></span> <span data-ttu-id="855d3-152">Чтобы получить строку подключения, следуйте инструкциям, указанным в разделе [Получение учетных данных управления](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span><span class="sxs-lookup"><span data-stu-id="855d3-152">You obtain the connection string by following the steps shown at [Obtain the management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="855d3-153">Строка подключения указывается для пространства имен служебной шины, и она не должна ограничиваться определенной очередью или разделом.</span><span class="sxs-lookup"><span data-stu-id="855d3-153">The connection string must be for a Service Bus namespace, not limited to a specific queue or topic.</span></span>
  <span data-ttu-id="855d3-154">Если оставить параметр `connection` пустым, выходная привязка предполагает, что в параметре приложения `AzureWebJobsServiceBus` указывается строка подключения служебной шины по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="855d3-154">If you leave `connection` empty, the output binding assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="855d3-155">Для свойства `accessRights` возможны такие значения, как `manage` и `listen`.</span><span class="sxs-lookup"><span data-stu-id="855d3-155">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="855d3-156">Значение по умолчанию — `manage`. Это означает, что у свойства `connection` есть разрешение на **управление**.</span><span class="sxs-lookup"><span data-stu-id="855d3-156">The default is `manage`, which indicates that the `connection` has the **Manage** permission.</span></span> <span data-ttu-id="855d3-157">При использовании строки подключения без разрешения на **управление**, задайте для свойства `accessRights` значение `listen`.</span><span class="sxs-lookup"><span data-stu-id="855d3-157">If you use a connection string that does not have the **Manage** permission, set `accessRights` to `listen`.</span></span> <span data-ttu-id="855d3-158">В противном случае выполнение операций, для которых требуются права на управление, в среде выполнения Функций Azure может завершиться ошибкой.</span><span class="sxs-lookup"><span data-stu-id="855d3-158">Otherwise, the Functions runtime might fail trying to do operations that require manage rights.</span></span>

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="855d3-159">Использование выходной привязки</span><span class="sxs-lookup"><span data-stu-id="855d3-159">Output usage</span></span>
<span data-ttu-id="855d3-160">В языке C# и F# Функции Azure могут создать сообщение очереди служебной шины из следующих типов:</span><span class="sxs-lookup"><span data-stu-id="855d3-160">In C# and F#, Azure Functions can create a Service Bus queue message from any of the following types:</span></span>

* <span data-ttu-id="855d3-161">Любой [объект](https://msdn.microsoft.com/library/system.object.aspx). Определение параметра выглядит так: `out T paramName` (C#).</span><span class="sxs-lookup"><span data-stu-id="855d3-161">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - Parameter definition looks like `out T paramName` (C#).</span></span>
  <span data-ttu-id="855d3-162">Функции десериализируют объект в сообщение JSON.</span><span class="sxs-lookup"><span data-stu-id="855d3-162">Functions deserializes the object into a JSON message.</span></span> <span data-ttu-id="855d3-163">Если при выходе из функции выходное значение равно null, Функции создают сообщение с пустым объектом.</span><span class="sxs-lookup"><span data-stu-id="855d3-163">If the output value is null when the function exits, Functions creates the message with a null object.</span></span>
* <span data-ttu-id="855d3-164">`string`. Определение параметра выглядит так: `out string paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="855d3-164">`string` - Parameter definition looks like `out string paraName` (C#).</span></span> <span data-ttu-id="855d3-165">Если при выходе из функции значение параметра не равно null, Функции создают сообщение.</span><span class="sxs-lookup"><span data-stu-id="855d3-165">If the parameter value is non-null when the function exits, Functions creates a message.</span></span>
* <span data-ttu-id="855d3-166">`byte[]`. Определение параметра выглядит так: `out byte[] paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="855d3-166">`byte[]` - Parameter definition looks like `out byte[] paraName` (C#).</span></span> <span data-ttu-id="855d3-167">Если при выходе из функции значение параметра не равно null, Функции создают сообщение.</span><span class="sxs-lookup"><span data-stu-id="855d3-167">If the parameter value is non-null when the function exits, Functions creates a message.</span></span>
* <span data-ttu-id="855d3-168">`BrokeredMessage`. Определение параметра выглядит так: `out BrokeredMessage paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="855d3-168">`BrokeredMessage` Parameter definition looks like `out BrokeredMessage paraName` (C#).</span></span> <span data-ttu-id="855d3-169">Если при выходе из функции значение параметра не равно null, Функции создают сообщение.</span><span class="sxs-lookup"><span data-stu-id="855d3-169">If the parameter value is non-null when the function exits, Functions creates a message.</span></span>

<span data-ttu-id="855d3-170">Чтобы создать несколько сообщений в функции C#, можно использовать `ICollector<T>` или `IAsyncCollector<T>`.</span><span class="sxs-lookup"><span data-stu-id="855d3-170">For creating multiple messages in a C# function, you can use `ICollector<T>` or `IAsyncCollector<T>`.</span></span> <span data-ttu-id="855d3-171">Сообщение создается при вызове метода `Add` .</span><span class="sxs-lookup"><span data-stu-id="855d3-171">A message is created when you call the `Add` method.</span></span>

<span data-ttu-id="855d3-172">В Node.js для `context.binding.<paramName>` можно назначить строку, массив байтов или объект Javascript (десериализируется в JSON).</span><span class="sxs-lookup"><span data-stu-id="855d3-172">In Node.js, you can assign a string, a byte array, or a Javascript object (deserialized into JSON) to `context.binding.<paramName>`.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="855d3-173">Пример выходной привязки</span><span class="sxs-lookup"><span data-stu-id="855d3-173">Output sample</span></span>
<span data-ttu-id="855d3-174">Предположим, что у вас есть следующий файл function.json, определяющий выходные данные очереди служебной шины:</span><span class="sxs-lookup"><span data-stu-id="855d3-174">Suppose you have the following function.json, that defines a Service Bus queue output:</span></span>

```json
{
    "bindings": [
        {
            "schedule": "0/15 * * * * *",
            "name": "myTimer",
            "runsOnStartup": true,
            "type": "timerTrigger",
            "direction": "in"
        },
        {
            "name": "outputSbQueue",
            "type": "serviceBus",
            "queueName": "testqueue",
            "connection": "MyServiceBusConnection",
            "direction": "out"
        }
    ],
    "disabled": false
}
```

<span data-ttu-id="855d3-175">Ознакомьтесь с примером для конкретного языка, отправляющим сообщение в очередь служебной шины.</span><span class="sxs-lookup"><span data-stu-id="855d3-175">See the language-specific sample that sends a message to the service bus queue.</span></span>

* [<span data-ttu-id="855d3-176">C#</span><span class="sxs-lookup"><span data-stu-id="855d3-176">C#</span></span>](#outcsharp)
* [<span data-ttu-id="855d3-177">F#</span><span class="sxs-lookup"><span data-stu-id="855d3-177">F#</span></span>](#outfsharp)
* [<span data-ttu-id="855d3-178">Node.js</span><span class="sxs-lookup"><span data-stu-id="855d3-178">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="855d3-179">Пример выходной привязки для языка C#</span><span class="sxs-lookup"><span data-stu-id="855d3-179">Output sample in C#</span></span> #

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, out string outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue = message;
}
```

<span data-ttu-id="855d3-180">Создание нескольких сообщений:</span><span class="sxs-lookup"><span data-stu-id="855d3-180">Or, to create multiple messages:</span></span>

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, ICollector<string> outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue.Add("1 " + message);
    outputSbQueue.Add("2 " + message);
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a><span data-ttu-id="855d3-181">Пример выходной привязки для языка F#</span><span class="sxs-lookup"><span data-stu-id="855d3-181">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter, outputSbQueue: byref<string>) =
    let message = sprintf "Service Bus queue message created at: %s" (DateTime.Now.ToString())
    log.Info(message)
    outputSbQueue = message
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="855d3-182">Пример выходной привязки для Node.js</span><span class="sxs-lookup"><span data-stu-id="855d3-182">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = message;
    context.done();
};
```

<span data-ttu-id="855d3-183">Создание нескольких сообщений:</span><span class="sxs-lookup"><span data-stu-id="855d3-183">Or, to create multiple messages:</span></span>

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = [];
    context.bindings.outputSbQueueMsg.push("1 " + message);
    context.bindings.outputSbQueueMsg.push("2 " + message);
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="855d3-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="855d3-184">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

