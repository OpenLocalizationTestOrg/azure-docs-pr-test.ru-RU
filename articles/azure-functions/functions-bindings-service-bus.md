---
title: "aaaAzure функций Service Bus триггеры и привязки | Документы Microsoft"
description: "Понять, как триггеры toouse Azure Service Bus и привязки в функциях Azure."
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
ms.openlocfilehash: dff9e89bd3840b8c11f91cae41e13502afc7aa60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-service-bus-bindings"></a><span data-ttu-id="1b63e-104">Привязки служебной шины в Функциях Azure</span><span class="sxs-lookup"><span data-stu-id="1b63e-104">Azure Functions Service Bus bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="1b63e-105">В этой статье объясняется, как tooconfigure и работать с Azure Service Bus привязок в функциях Azure.</span><span class="sxs-lookup"><span data-stu-id="1b63e-105">This article explains how tooconfigure and work with Azure Service Bus bindings in Azure Functions.</span></span> 

<span data-ttu-id="1b63e-106">Функции Azure поддерживают привязки триггера и выходные привязки для очередей и разделов служебной шины.</span><span class="sxs-lookup"><span data-stu-id="1b63e-106">Azure Functions supports trigger and output bindings for Service Bus queues and topics.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="service-bus-trigger"></a><span data-ttu-id="1b63e-107">Триггер служебной шины</span><span class="sxs-lookup"><span data-stu-id="1b63e-107">Service Bus trigger</span></span>
<span data-ttu-id="1b63e-108">Используйте toomessages toorespond hello Service Bus триггера из очереди служебной шины или раздела.</span><span class="sxs-lookup"><span data-stu-id="1b63e-108">Use hello Service Bus trigger toorespond toomessages from a Service Bus queue or topic.</span></span> 

<span data-ttu-id="1b63e-109">Hello триггеров очередей и разделов Service Bus определяются следующие объекты JSON в hello hello `bindings` массив function.json:</span><span class="sxs-lookup"><span data-stu-id="1b63e-109">hello Service Bus queue and topic triggers are defined by hello following JSON objects in hello `bindings` array of function.json:</span></span>

* <span data-ttu-id="1b63e-110">Триггер *очереди*:</span><span class="sxs-lookup"><span data-stu-id="1b63e-110">*queue* trigger:</span></span>

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "queueName" : "<Name of hello queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

* <span data-ttu-id="1b63e-111">Триггер *раздела*:</span><span class="sxs-lookup"><span data-stu-id="1b63e-111">*topic* trigger:</span></span>

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "topicName" : "<Name of hello topic>",
        "subscriptionName" : "<Name of hello subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

<span data-ttu-id="1b63e-112">Обратите внимание hello следующие:</span><span class="sxs-lookup"><span data-stu-id="1b63e-112">Note hello following:</span></span>

* <span data-ttu-id="1b63e-113">Для `connection`, [создаются Настройка приложения в приложении функции](functions-how-to-use-azure-function-app-settings.md) , который содержит пространство имен служебной шины tooyour строку hello соединения, затем укажите имя параметра приложения hello hello в hello `connection` свойство в триггер.</span><span class="sxs-lookup"><span data-stu-id="1b63e-113">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains hello connection string tooyour Service Bus namespace, then specify hello name of hello app setting in hello `connection` property in your trigger.</span></span> <span data-ttu-id="1b63e-114">Получить строку подключения hello hello выполните действия, показанные на [получить учетные данные управления hello](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span><span class="sxs-lookup"><span data-stu-id="1b63e-114">You obtain hello connection string by following hello steps shown at [Obtain hello management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="1b63e-115">Строка подключения Hello должна иметь для пространства имен Service Bus, не ограниченной tooa определенной очереди или раздела.</span><span class="sxs-lookup"><span data-stu-id="1b63e-115">hello connection string must be for a Service Bus namespace, not limited tooa specific queue or topic.</span></span>
  <span data-ttu-id="1b63e-116">Если оставить `connection` пустой, триггер hello предполагается, что строка подключения шины обслуживания по умолчанию указан в параметр приложения `AzureWebJobsServiceBus`.</span><span class="sxs-lookup"><span data-stu-id="1b63e-116">If you leave `connection` empty, hello trigger assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="1b63e-117">Для свойства `accessRights` возможны такие значения, как `manage` и `listen`.</span><span class="sxs-lookup"><span data-stu-id="1b63e-117">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="1b63e-118">по умолчанию Hello — `manage`, указывающая, что hello `connection` имеет hello **управление** разрешение.</span><span class="sxs-lookup"><span data-stu-id="1b63e-118">hello default is `manage`, which indicates that hello `connection` has hello **Manage** permission.</span></span> <span data-ttu-id="1b63e-119">При использовании строки подключения, которая не поддерживает hello **управление** набор разрешений, `accessRights` слишком`listen`.</span><span class="sxs-lookup"><span data-stu-id="1b63e-119">If you use a connection string that does not have hello **Manage** permission, set `accessRights` too`listen`.</span></span> <span data-ttu-id="1b63e-120">В противном случае среда выполнения может произойти сбой при toodo операций, требующих функций hello управление правами.</span><span class="sxs-lookup"><span data-stu-id="1b63e-120">Otherwise, hello Functions runtime might fail trying toodo operations that require manage rights.</span></span>

## <a name="trigger-behavior"></a><span data-ttu-id="1b63e-121">Поведение триггера</span><span class="sxs-lookup"><span data-stu-id="1b63e-121">Trigger behavior</span></span>
* <span data-ttu-id="1b63e-122">**Однопоточную** — по умолчанию процессы среды выполнения функции hello, несколько сообщений параллельно.</span><span class="sxs-lookup"><span data-stu-id="1b63e-122">**Single-threading** - By default, hello Functions runtime processes multiple messages concurrently.</span></span> <span data-ttu-id="1b63e-123">задать toodirect hello среды выполнения tooprocess только одного очередь или раздел сообщения одновременно, `serviceBus.maxConcurrentCalls` too1 в *host.json*.</span><span class="sxs-lookup"><span data-stu-id="1b63e-123">toodirect hello runtime tooprocess only a single queue or topic message at a time, set `serviceBus.maxConcurrentCalls` too1 in *host.json*.</span></span> 
  <span data-ttu-id="1b63e-124">Сведения о файле *host.json* см. в разделе [Структура папок](functions-reference.md#folder-structure) и статье [host.json](https://github .com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="1b63e-124">For information about *host.json*, see [Folder Structure](functions-reference.md#folder-structure) and [host.json](https://github .com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>
* <span data-ttu-id="1b63e-125">**Обработка подозрительных сообщений.** В служебной шине выполняется собственная обработка подозрительных сообщений, которую нельзя контролировать или настраивать с помощью конфигурации или кода Функций Azure.</span><span class="sxs-lookup"><span data-stu-id="1b63e-125">**Poison message handling** - Service Bus does its own poison message handling, which can't be controlled or configured in Azure Functions configuration or code.</span></span> 
* <span data-ttu-id="1b63e-126">**Поведение PeekLock** -среда выполнения функции hello получает сообщение в [ `PeekLock` режим](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) и вызывает метод `Complete` на приветственное сообщение, если функции hello завершается успешно, или вызовы `Abandon` Если hello функция завершается с ошибкой.</span><span class="sxs-lookup"><span data-stu-id="1b63e-126">**PeekLock behavior** - hello Functions runtime receives a message in [`PeekLock` mode](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) and calls `Complete` on hello message if hello function finishes successfully, or calls `Abandon` if hello function fails.</span></span> 
  <span data-ttu-id="1b63e-127">Если функции hello выполняется дольше, чем hello `PeekLock` время ожидания блокировки hello автоматически обновляется.</span><span class="sxs-lookup"><span data-stu-id="1b63e-127">If hello function runs longer than hello `PeekLock` timeout, hello lock is automatically renewed.</span></span>

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="1b63e-128">Использование триггера</span><span class="sxs-lookup"><span data-stu-id="1b63e-128">Trigger usage</span></span>
<span data-ttu-id="1b63e-129">В этом разделе показано, как toouse Service Bus триггер в коде функции.</span><span class="sxs-lookup"><span data-stu-id="1b63e-129">This section shows you how toouse your Service Bus trigger in your function code.</span></span> 

<span data-ttu-id="1b63e-130">В C# и F # триггер Service Bus приветственное сообщение может быть десериализованный tooany hello следующие типы входных:</span><span class="sxs-lookup"><span data-stu-id="1b63e-130">In C# and F#, hello Service Bus trigger message can be deserialized tooany of hello following input types:</span></span>

* <span data-ttu-id="1b63e-131">`string` используется для строковых сообщений.</span><span class="sxs-lookup"><span data-stu-id="1b63e-131">`string` - useful for string messages</span></span>
* <span data-ttu-id="1b63e-132">`byte[]` используется для двоичных данных.</span><span class="sxs-lookup"><span data-stu-id="1b63e-132">`byte[]` - useful for binary data</span></span>
* <span data-ttu-id="1b63e-133">Любой [объект](https://msdn.microsoft.com/library/system.object.aspx) используется для сериализованных данных JSON.</span><span class="sxs-lookup"><span data-stu-id="1b63e-133">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized data.</span></span>
  <span data-ttu-id="1b63e-134">Если пользовательский тип входных данных, объявите например `CustomType`, функции Azure пытается данных JSON toodeserialize hello в указанный тип.</span><span class="sxs-lookup"><span data-stu-id="1b63e-134">If you declare a custom input type, such as `CustomType`, Azure Functions tries toodeserialize hello JSON data into your specified type.</span></span>
* <span data-ttu-id="1b63e-135">`BrokeredMessage`-предоставляет вам hello десериализовать сообщение hello [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) метод.</span><span class="sxs-lookup"><span data-stu-id="1b63e-135">`BrokeredMessage` - gives you hello deserialized message with hello [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) method.</span></span>

<span data-ttu-id="1b63e-136">В Node.js триггер Service Bus приветственное сообщение передается в функцию hello как строку или объект JSON.</span><span class="sxs-lookup"><span data-stu-id="1b63e-136">In Node.js, hello Service Bus trigger message is passed into hello function as either a string or JSON object.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="1b63e-137">Пример триггера</span><span class="sxs-lookup"><span data-stu-id="1b63e-137">Trigger sample</span></span>
<span data-ttu-id="1b63e-138">Предположим, что имеется следующая function.json hello:</span><span class="sxs-lookup"><span data-stu-id="1b63e-138">Suppose you have hello following function.json:</span></span>

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

<span data-ttu-id="1b63e-139">См. пример hello зависящие от языка, который обрабатывает сообщение очереди Service Bus.</span><span class="sxs-lookup"><span data-stu-id="1b63e-139">See hello language-specific sample that processes a Service Bus queue message.</span></span>

* [<span data-ttu-id="1b63e-140">C#</span><span class="sxs-lookup"><span data-stu-id="1b63e-140">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="1b63e-141">F#</span><span class="sxs-lookup"><span data-stu-id="1b63e-141">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="1b63e-142">Node.js</span><span class="sxs-lookup"><span data-stu-id="1b63e-142">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="1b63e-143">Пример триггера на языке C#</span><span class="sxs-lookup"><span data-stu-id="1b63e-143">Trigger sample in C#</span></span> #

```cs
public static void Run(string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a><span data-ttu-id="1b63e-144">Пример триггера на языке F#</span><span class="sxs-lookup"><span data-stu-id="1b63e-144">Trigger sample in F#</span></span> #

```fsharp
let Run(myQueueItem: string, log: TraceWriter) =
    log.Info(sprintf "F# ServiceBus queue trigger function processed message: %s" myQueueItem)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="1b63e-145">Пример триггера для Node.js</span><span class="sxs-lookup"><span data-stu-id="1b63e-145">Trigger sample in Node.js</span></span>

```javascript
module.exports = function(context, myQueueItem) {
    context.log('Node.js ServiceBus queue trigger function processed message', myQueueItem);
    context.done();
};
```

<a name="output"></a>

## <a name="service-bus-output-binding"></a><span data-ttu-id="1b63e-146">Выходная привязка служебной шины</span><span class="sxs-lookup"><span data-stu-id="1b63e-146">Service Bus output binding</span></span>
<span data-ttu-id="1b63e-147">выходные данные очередей и разделов Service Bus для функции Hello используйте следующие объекты JSON в hello hello `bindings` массив function.json:</span><span class="sxs-lookup"><span data-stu-id="1b63e-147">hello Service Bus queue and topic output for a function use hello following JSON objects in hello `bindings` array of function.json:</span></span>

* <span data-ttu-id="1b63e-148">Выходные данные *очереди*:</span><span class="sxs-lookup"><span data-stu-id="1b63e-148">*queue* output:</span></span>

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "queueName" : "<Name of hello queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```
* <span data-ttu-id="1b63e-149">Выходные данные *раздела*:</span><span class="sxs-lookup"><span data-stu-id="1b63e-149">*topic* output:</span></span>

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "topicName" : "<Name of hello topic>",
        "subscriptionName" : "<Name of hello subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```

<span data-ttu-id="1b63e-150">Обратите внимание hello следующие:</span><span class="sxs-lookup"><span data-stu-id="1b63e-150">Note hello following:</span></span>

* <span data-ttu-id="1b63e-151">Для `connection`, [создаются Настройка приложения в приложении функции](functions-how-to-use-azure-function-app-settings.md) , который содержит пространство имен служебной шины tooyour строку hello соединения, затем укажите имя параметра приложения hello hello в hello `connection` свойство в качестве выходных данных привязка.</span><span class="sxs-lookup"><span data-stu-id="1b63e-151">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains hello connection string tooyour Service Bus namespace, then specify hello name of hello app setting in hello `connection` property in your output binding.</span></span> <span data-ttu-id="1b63e-152">Получить строку подключения hello hello выполните действия, показанные на [получить учетные данные управления hello](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span><span class="sxs-lookup"><span data-stu-id="1b63e-152">You obtain hello connection string by following hello steps shown at [Obtain hello management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="1b63e-153">Строка подключения Hello должна иметь для пространства имен Service Bus, не ограниченной tooa определенной очереди или раздела.</span><span class="sxs-lookup"><span data-stu-id="1b63e-153">hello connection string must be for a Service Bus namespace, not limited tooa specific queue or topic.</span></span>
  <span data-ttu-id="1b63e-154">Если оставить `connection` пустой, hello привязка для вывода предполагается, что строка подключения шины обслуживания по умолчанию указан в параметр приложения `AzureWebJobsServiceBus`.</span><span class="sxs-lookup"><span data-stu-id="1b63e-154">If you leave `connection` empty, hello output binding assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="1b63e-155">Для свойства `accessRights` возможны такие значения, как `manage` и `listen`.</span><span class="sxs-lookup"><span data-stu-id="1b63e-155">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="1b63e-156">по умолчанию Hello — `manage`, указывающая, что hello `connection` имеет hello **управление** разрешение.</span><span class="sxs-lookup"><span data-stu-id="1b63e-156">hello default is `manage`, which indicates that hello `connection` has hello **Manage** permission.</span></span> <span data-ttu-id="1b63e-157">При использовании строки подключения, которая не поддерживает hello **управление** набор разрешений, `accessRights` слишком`listen`.</span><span class="sxs-lookup"><span data-stu-id="1b63e-157">If you use a connection string that does not have hello **Manage** permission, set `accessRights` too`listen`.</span></span> <span data-ttu-id="1b63e-158">В противном случае среда выполнения может произойти сбой при toodo операций, требующих функций hello управление правами.</span><span class="sxs-lookup"><span data-stu-id="1b63e-158">Otherwise, hello Functions runtime might fail trying toodo operations that require manage rights.</span></span>

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="1b63e-159">Использование выходной привязки</span><span class="sxs-lookup"><span data-stu-id="1b63e-159">Output usage</span></span>
<span data-ttu-id="1b63e-160">В C# и F # функции Azure можно создать сообщение очереди служебной шины из любого hello следующие типы:</span><span class="sxs-lookup"><span data-stu-id="1b63e-160">In C# and F#, Azure Functions can create a Service Bus queue message from any of hello following types:</span></span>

* <span data-ttu-id="1b63e-161">Любой [объект](https://msdn.microsoft.com/library/system.object.aspx). Определение параметра выглядит так: `out T paramName` (C#).</span><span class="sxs-lookup"><span data-stu-id="1b63e-161">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - Parameter definition looks like `out T paramName` (C#).</span></span>
  <span data-ttu-id="1b63e-162">Функции десериализует hello объекта в сообщение JSON.</span><span class="sxs-lookup"><span data-stu-id="1b63e-162">Functions deserializes hello object into a JSON message.</span></span> <span data-ttu-id="1b63e-163">Если при выходе из функции hello hello выходное значение равно null, функции создает приветственное сообщение с пустым объектом.</span><span class="sxs-lookup"><span data-stu-id="1b63e-163">If hello output value is null when hello function exits, Functions creates hello message with a null object.</span></span>
* <span data-ttu-id="1b63e-164">`string`. Определение параметра выглядит так: `out string paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="1b63e-164">`string` - Parameter definition looks like `out string paraName` (C#).</span></span> <span data-ttu-id="1b63e-165">Если значение параметра hello отлично от null, при выходе из функции hello, функции создает сообщение.</span><span class="sxs-lookup"><span data-stu-id="1b63e-165">If hello parameter value is non-null when hello function exits, Functions creates a message.</span></span>
* <span data-ttu-id="1b63e-166">`byte[]`. Определение параметра выглядит так: `out byte[] paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="1b63e-166">`byte[]` - Parameter definition looks like `out byte[] paraName` (C#).</span></span> <span data-ttu-id="1b63e-167">Если значение параметра hello отлично от null, при выходе из функции hello, функции создает сообщение.</span><span class="sxs-lookup"><span data-stu-id="1b63e-167">If hello parameter value is non-null when hello function exits, Functions creates a message.</span></span>
* <span data-ttu-id="1b63e-168">`BrokeredMessage`. Определение параметра выглядит так: `out BrokeredMessage paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="1b63e-168">`BrokeredMessage` Parameter definition looks like `out BrokeredMessage paraName` (C#).</span></span> <span data-ttu-id="1b63e-169">Если значение параметра hello отлично от null, при выходе из функции hello, функции создает сообщение.</span><span class="sxs-lookup"><span data-stu-id="1b63e-169">If hello parameter value is non-null when hello function exits, Functions creates a message.</span></span>

<span data-ttu-id="1b63e-170">Чтобы создать несколько сообщений в функции C#, можно использовать `ICollector<T>` или `IAsyncCollector<T>`.</span><span class="sxs-lookup"><span data-stu-id="1b63e-170">For creating multiple messages in a C# function, you can use `ICollector<T>` or `IAsyncCollector<T>`.</span></span> <span data-ttu-id="1b63e-171">Сообщение создается при вызове hello `Add` метод.</span><span class="sxs-lookup"><span data-stu-id="1b63e-171">A message is created when you call hello `Add` method.</span></span>

<span data-ttu-id="1b63e-172">В Node.js, можно назначить строку, байтовый массив или объект Javascript (десериализовать в JSON) слишком`context.binding.<paramName>`.</span><span class="sxs-lookup"><span data-stu-id="1b63e-172">In Node.js, you can assign a string, a byte array, or a Javascript object (deserialized into JSON) too`context.binding.<paramName>`.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="1b63e-173">Пример выходной привязки</span><span class="sxs-lookup"><span data-stu-id="1b63e-173">Output sample</span></span>
<span data-ttu-id="1b63e-174">Предположим, что имеется следующая function.json hello, определяющий выходной очереди служебной шины:</span><span class="sxs-lookup"><span data-stu-id="1b63e-174">Suppose you have hello following function.json, that defines a Service Bus queue output:</span></span>

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

<span data-ttu-id="1b63e-175">См. Образец hello конкретного языка, отправляет в очередь сообщение toohello служебной шины.</span><span class="sxs-lookup"><span data-stu-id="1b63e-175">See hello language-specific sample that sends a message toohello service bus queue.</span></span>

* [<span data-ttu-id="1b63e-176">C#</span><span class="sxs-lookup"><span data-stu-id="1b63e-176">C#</span></span>](#outcsharp)
* [<span data-ttu-id="1b63e-177">F#</span><span class="sxs-lookup"><span data-stu-id="1b63e-177">F#</span></span>](#outfsharp)
* [<span data-ttu-id="1b63e-178">Node.js</span><span class="sxs-lookup"><span data-stu-id="1b63e-178">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="1b63e-179">Пример выходной привязки для языка C#</span><span class="sxs-lookup"><span data-stu-id="1b63e-179">Output sample in C#</span></span> #

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, out string outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue = message;
}
```

<span data-ttu-id="1b63e-180">Или toocreate несколько сообщений:</span><span class="sxs-lookup"><span data-stu-id="1b63e-180">Or, toocreate multiple messages:</span></span>

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

### <a name="output-sample-in-f"></a><span data-ttu-id="1b63e-181">Пример выходной привязки для языка F#</span><span class="sxs-lookup"><span data-stu-id="1b63e-181">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter, outputSbQueue: byref<string>) =
    let message = sprintf "Service Bus queue message created at: %s" (DateTime.Now.ToString())
    log.Info(message)
    outputSbQueue = message
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="1b63e-182">Пример выходной привязки для Node.js</span><span class="sxs-lookup"><span data-stu-id="1b63e-182">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = message;
    context.done();
};
```

<span data-ttu-id="1b63e-183">Или toocreate несколько сообщений:</span><span class="sxs-lookup"><span data-stu-id="1b63e-183">Or, toocreate multiple messages:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="1b63e-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1b63e-184">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

