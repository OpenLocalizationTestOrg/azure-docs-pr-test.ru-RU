---
title: "очереди хранилища aaaAzure функции привязок | Документы Microsoft"
description: "Понять, как триггеры toouse хранилища Azure и привязки в функциях Azure."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "функции azure, функции, обработка событий, динамические вычисления, независимая архитектура"
ms.assetid: 4e6a837d-e64f-45a0-87b7-aa02688a75f3
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: glenga
ms.openlocfilehash: 438b4f63e823149072c86fdefa7e15bfd2a2c4df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-queue-storage-bindings"></a><span data-ttu-id="b6158-104">Привязки хранилища очередей для Функций Azure</span><span class="sxs-lookup"><span data-stu-id="b6158-104">Azure Functions Queue Storage bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="b6158-105">В этой статье описывается как tooconfigure и код привязок хранилища очередей Azure в функциях Azure.</span><span class="sxs-lookup"><span data-stu-id="b6158-105">This article describes how tooconfigure and code Azure Queue storage bindings in Azure Functions.</span></span> <span data-ttu-id="b6158-106">Функции Azure поддерживают привязки триггера и выходные привязки для очередей Azure.</span><span class="sxs-lookup"><span data-stu-id="b6158-106">Azure Functions supports trigger and output bindings for Azure queues.</span></span> <span data-ttu-id="b6158-107">Описание возможностей, доступных во всех привязках, см. в статье [Основные понятия триггеров и привязок в Функциях Azure](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="b6158-107">For features that are available in all bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="queue-storage-trigger"></a><span data-ttu-id="b6158-108">Триггер хранилища очередей</span><span class="sxs-lookup"><span data-stu-id="b6158-108">Queue storage trigger</span></span>
<span data-ttu-id="b6158-109">триггер хранилища очередей Azure Hello позволяет toomonitor хранилища очередей для новых сообщений и реагировать toothem.</span><span class="sxs-lookup"><span data-stu-id="b6158-109">hello Azure Queue storage trigger enables you toomonitor a queue storage for new messages and react toothem.</span></span> 

<span data-ttu-id="b6158-110">Определение триггера очереди с помощью hello **Интеграция** вкладка на портале функции hello.</span><span class="sxs-lookup"><span data-stu-id="b6158-110">Define a queue trigger using hello **Integrate** tab in hello Functions portal.</span></span> <span data-ttu-id="b6158-111">Hello портал создает следующие определения в hello hello **привязки** раздел *function.json*:</span><span class="sxs-lookup"><span data-stu-id="b6158-111">hello portal creates hello following definition in hello  **bindings** section of *function.json*:</span></span>

```json
{
    "type": "queueTrigger",
    "direction": "in",
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "queueName": "<Name of queue toopoll>",
    "connection":"<Name of app setting - see below>"
}
```

* <span data-ttu-id="b6158-112">Hello `connection` свойство должно содержать имя hello Настройка приложения, содержащий строки подключения хранилища.</span><span class="sxs-lookup"><span data-stu-id="b6158-112">hello `connection` property must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="b6158-113">В hello портал Azure, hello стандартного редактора в hello **Интеграция** настраивает этот параметр приложения автоматически при выборе учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="b6158-113">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

<span data-ttu-id="b6158-114">Дополнительные параметры могут быть предоставлены в [host.json файл](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) toofurther тонкой настройки триггеров очереди хранилища.</span><span class="sxs-lookup"><span data-stu-id="b6158-114">Additional settings can be provided in a [host.json file](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) toofurther fine-tune queue storage triggers.</span></span> <span data-ttu-id="b6158-115">Например можно изменить интервал опроса очереди hello в host.json.</span><span class="sxs-lookup"><span data-stu-id="b6158-115">For example, you can change hello queue polling interval in host.json.</span></span>

<a name="triggerusage"></a>

## <a name="using-a-queue-trigger"></a><span data-ttu-id="b6158-116">Использование триггера очереди</span><span class="sxs-lookup"><span data-stu-id="b6158-116">Using a queue trigger</span></span>
<span data-ttu-id="b6158-117">В функциях Node.js обращаться при помощи данных очереди hello `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="b6158-117">In Node.js functions, access hello queue data using `context.bindings.<name>`.</span></span>


<span data-ttu-id="b6158-118">Функции .NET для получения доступа к очереди hello полезных данных, с помощью параметра метода, например `CloudQueueMessage paramName`.</span><span class="sxs-lookup"><span data-stu-id="b6158-118">In .NET functions, access hello queue payload using a method parameter such as `CloudQueueMessage paramName`.</span></span> <span data-ttu-id="b6158-119">Здесь `paramName` hello значение, указанное в hello [конфигурация триггеров](#trigger).</span><span class="sxs-lookup"><span data-stu-id="b6158-119">Here, `paramName` is hello value you specified in hello [trigger configuration](#trigger).</span></span> <span data-ttu-id="b6158-120">приветственное сообщение очереди может быть десериализованный tooany hello следующие типы:</span><span class="sxs-lookup"><span data-stu-id="b6158-120">hello queue message can be deserialized tooany of hello following types:</span></span>

* <span data-ttu-id="b6158-121">Объект POCO.</span><span class="sxs-lookup"><span data-stu-id="b6158-121">POCO object.</span></span> <span data-ttu-id="b6158-122">Используйте, если полезные данные очереди hello объекта JSON.</span><span class="sxs-lookup"><span data-stu-id="b6158-122">Use if hello queue payload is a JSON object.</span></span> <span data-ttu-id="b6158-123">Среда выполнения функции Hello десериализует hello полезных данных в объект POCO hello.</span><span class="sxs-lookup"><span data-stu-id="b6158-123">hello Functions runtime deserializes hello payload into hello POCO object.</span></span> 
* `string`
* `byte[]`
* [`CloudQueueMessage`]

<a name="meta"></a>

### <a name="queue-trigger-metadata"></a><span data-ttu-id="b6158-124">Метаданные триггера очереди</span><span class="sxs-lookup"><span data-stu-id="b6158-124">Queue trigger metadata</span></span>
<span data-ttu-id="b6158-125">триггер Hello очередь предоставляет несколько свойств метаданных.</span><span class="sxs-lookup"><span data-stu-id="b6158-125">hello queue trigger provides several metadata properties.</span></span> <span data-ttu-id="b6158-126">Эти свойства можно использовать как часть выражений привязки в других привязках или как параметры в коде.</span><span class="sxs-lookup"><span data-stu-id="b6158-126">These properties can be used as part of binding expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="b6158-127">Hello значения имеют hello совпадает с семантикой [ `CloudQueueMessage` ].</span><span class="sxs-lookup"><span data-stu-id="b6158-127">hello values have hello same semantics as [`CloudQueueMessage`].</span></span>

* <span data-ttu-id="b6158-128">**QueueTrigger** — полезные данные очереди (в случае, если это допустимая строка)</span><span class="sxs-lookup"><span data-stu-id="b6158-128">**QueueTrigger** - queue payload (if a valid string)</span></span>
* <span data-ttu-id="b6158-129">**DequeueCount** — тип `int`.</span><span class="sxs-lookup"><span data-stu-id="b6158-129">**DequeueCount** - Type `int`.</span></span> <span data-ttu-id="b6158-130">Здравствуйте, сколько раз сообщение было выведено из очереди.</span><span class="sxs-lookup"><span data-stu-id="b6158-130">hello number of times this message has been dequeued.</span></span>
* <span data-ttu-id="b6158-131">**ExpirationTime** — тип `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="b6158-131">**ExpirationTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="b6158-132">Hello время истечения срока действия сообщения hello.</span><span class="sxs-lookup"><span data-stu-id="b6158-132">hello time that hello message expires.</span></span>
* <span data-ttu-id="b6158-133">**Id** — тип `string`.</span><span class="sxs-lookup"><span data-stu-id="b6158-133">**Id** - Type `string`.</span></span> <span data-ttu-id="b6158-134">Идентификатор сообщения в очереди.</span><span class="sxs-lookup"><span data-stu-id="b6158-134">Queue message ID.</span></span>
* <span data-ttu-id="b6158-135">**InsertionTime** — тип `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="b6158-135">**InsertionTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="b6158-136">время Hello, сообщение hello было добавлено toohello очереди.</span><span class="sxs-lookup"><span data-stu-id="b6158-136">hello time that hello message was added toohello queue.</span></span>
* <span data-ttu-id="b6158-137">**NextVisibleTime** — введите `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="b6158-137">**NextVisibleTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="b6158-138">время Hello сообщение hello, теперь будут видны.</span><span class="sxs-lookup"><span data-stu-id="b6158-138">hello time that hello message will next be visible.</span></span>
* <span data-ttu-id="b6158-139">**PopReceipt** — тип `string`.</span><span class="sxs-lookup"><span data-stu-id="b6158-139">**PopReceipt** - Type `string`.</span></span> <span data-ttu-id="b6158-140">приветственное сообщение подтверждения.</span><span class="sxs-lookup"><span data-stu-id="b6158-140">hello message's pop receipt.</span></span>

<span data-ttu-id="b6158-141">В разделе как toouse hello метаданных очереди в [пример триггера](#triggersample).</span><span class="sxs-lookup"><span data-stu-id="b6158-141">See how toouse hello queue metadata in [Trigger sample](#triggersample).</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="b6158-142">Пример триггера</span><span class="sxs-lookup"><span data-stu-id="b6158-142">Trigger sample</span></span>
<span data-ttu-id="b6158-143">Предположим, что у вас есть следующие function.json, которая определяет триггер очереди hello:</span><span class="sxs-lookup"><span data-stu-id="b6158-143">Suppose you have hello following function.json that defines a queue trigger:</span></span>

```json
{
    "disabled": false,
    "bindings": [
        {
            "type": "queueTrigger",
            "direction": "in",
            "name": "myQueueItem",
            "queueName": "myqueue-items",
            "connection":"MyStorageConnectionString"
        }
    ]
}
```

<span data-ttu-id="b6158-144">См. пример hello зависящие от языка, который загружает и регистрирует метаданные очереди.</span><span class="sxs-lookup"><span data-stu-id="b6158-144">See hello language-specific sample that retrieves and logs queue metadata.</span></span>

* [<span data-ttu-id="b6158-145">C#</span><span class="sxs-lookup"><span data-stu-id="b6158-145">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="b6158-146">Node.js</span><span class="sxs-lookup"><span data-stu-id="b6158-146">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="b6158-147">Пример триггера на языке C#</span><span class="sxs-lookup"><span data-stu-id="b6158-147">Trigger sample in C#</span></span> #
```csharp
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Queue;
using System;

public static void Run(CloudQueueMessage myQueueItem, 
    DateTimeOffset expirationTime, 
    DateTimeOffset insertionTime, 
    DateTimeOffset nextVisibleTime,
    string queueTrigger,
    string id,
    string popReceipt,
    int dequeueCount,
    TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem.AsString}\n" +
        $"queueTrigger={queueTrigger}\n" +
        $"expirationTime={expirationTime}\n" +
        $"insertionTime={insertionTime}\n" +
        $"nextVisibleTime={nextVisibleTime}\n" +
        $"id={id}\n" +
        $"popReceipt={popReceipt}\n" + 
        $"dequeueCount={dequeueCount}");
}
```

<!--
<a name="triggerfsharp"></a>
### Trigger sample in F# ## 
```fsharp

```
-->

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="b6158-148">Пример триггера для Node.js</span><span class="sxs-lookup"><span data-stu-id="b6158-148">Trigger sample in Node.js</span></span>

```javascript
module.exports = function (context) {
    context.log('Node.js queue trigger function processed work item', context.bindings.myQueueItem);
    context.log('queueTrigger =', context.bindingData.queueTrigger);
    context.log('expirationTime =', context.bindingData.expirationTime);
    context.log('insertionTime =', context.bindingData.insertionTime);
    context.log('nextVisibleTime =', context.bindingData.nextVisibleTime);
    context.log('id=', context.bindingData.id);
    context.log('popReceipt =', context.bindingData.popReceipt);
    context.log('dequeueCount =', context.bindingData.dequeueCount);
    context.done();
};
```

### <a name="handling-poison-queue-messages"></a><span data-ttu-id="b6158-149">Обработка подозрительных сообщений очереди</span><span class="sxs-lookup"><span data-stu-id="b6158-149">Handling poison queue messages</span></span>
<span data-ttu-id="b6158-150">Функция очереди триггера в случае сбоя функции Azure повторяет этой функции копирования toofive раз для данной очереди сообщения, включая hello сначала попробовать сделать.</span><span class="sxs-lookup"><span data-stu-id="b6158-150">When a queue trigger function fails, Azure Functions retries that function up toofive times for a given queue message, including hello first try.</span></span> <span data-ttu-id="b6158-151">Если все пять попытки не удались, среда выполнения функции hello добавляет хранилища очереди сообщений tooa с именем  *&lt;originalqueuename >-подозрительных*.</span><span class="sxs-lookup"><span data-stu-id="b6158-151">If all five attempts fail, hello functions runtime adds a message tooa queue storage named *&lt;originalqueuename>-poison*.</span></span> <span data-ttu-id="b6158-152">Можно написать tooprocess функция сообщения из очереди подозрительных сообщений hello ее регистрации или отправка уведомления о необходимости ручного вмешательства.</span><span class="sxs-lookup"><span data-stu-id="b6158-152">You can write a function tooprocess messages from hello poison queue by logging them or sending a  notification that manual attention is needed.</span></span> 

<span data-ttu-id="b6158-153">toohandle опасных сообщений вручную, проверьте hello `dequeueCount` hello очереди сообщения (в разделе [метаданных очереди триггера](#meta)).</span><span class="sxs-lookup"><span data-stu-id="b6158-153">toohandle poison messages manually, check hello `dequeueCount` of hello queue message (see [Queue trigger metadata](#meta)).</span></span>

<a name="output"></a>

## <a name="queue-storage-output-binding"></a><span data-ttu-id="b6158-154">Выходная привязка хранилища очередей</span><span class="sxs-lookup"><span data-stu-id="b6158-154">Queue storage output binding</span></span>
<span data-ttu-id="b6158-155">привязка позволяет toowrite сообщений в очереди tooa вывода Hello хранилища очередей Azure.</span><span class="sxs-lookup"><span data-stu-id="b6158-155">hello Azure queue storage output binding enables you toowrite messages tooa queue.</span></span> 

<span data-ttu-id="b6158-156">Определение очереди привязка для вывода с помощью hello **Интеграция** вкладка на портале функции hello.</span><span class="sxs-lookup"><span data-stu-id="b6158-156">Define a queue output binding using hello **Integrate** tab in hello Functions portal.</span></span> <span data-ttu-id="b6158-157">Hello портал создает следующие определения в hello hello **привязки** раздел *function.json*:</span><span class="sxs-lookup"><span data-stu-id="b6158-157">hello portal creates hello following definition in hello  **bindings** section of *function.json*:</span></span>

```json
{
   "type": "queue",
   "direction": "out",
   "name": "<hello name used tooidentify hello trigger data in your code>",
   "queueName": "<Name of queue toowrite to>",
   "connection":"<Name of app setting - see below>"
}
```

* <span data-ttu-id="b6158-158">Hello `connection` свойство должно содержать имя hello Настройка приложения, содержащий строки подключения хранилища.</span><span class="sxs-lookup"><span data-stu-id="b6158-158">hello `connection` property must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="b6158-159">В hello портал Azure, hello стандартного редактора в hello **Интеграция** настраивает этот параметр приложения автоматически при выборе учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="b6158-159">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

<a name="outputusage"></a>

## <a name="using-a-queue-output-binding"></a><span data-ttu-id="b6158-160">Использование выходной привязки очереди</span><span class="sxs-lookup"><span data-stu-id="b6158-160">Using a queue output binding</span></span>
<span data-ttu-id="b6158-161">В функции Node.js, доступ к очереди вывода hello с помощью `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="b6158-161">In Node.js functions, you access hello output queue using `context.bindings.<name>`.</span></span>

<span data-ttu-id="b6158-162">В функциях .NET может выводить tooany из hello следующие типы.</span><span class="sxs-lookup"><span data-stu-id="b6158-162">In .NET functions, you can output tooany of hello following types.</span></span> <span data-ttu-id="b6158-163">Если тип параметра `T`, `T` должен быть один из типов hello поддерживается выходных данных, например `string` или POCO.</span><span class="sxs-lookup"><span data-stu-id="b6158-163">When there is a type parameter `T`, `T` must be one of hello supported output types, such as `string` or a POCO.</span></span>

* <span data-ttu-id="b6158-164">`out T` (сериализируется как JSON)</span><span class="sxs-lookup"><span data-stu-id="b6158-164">`out T` (serialized as JSON)</span></span>
* `out string`
* `out byte[]`
* <span data-ttu-id="b6158-165">`out` [`CloudQueueMessage`]</span><span class="sxs-lookup"><span data-stu-id="b6158-165">`out` [`CloudQueueMessage`]</span></span> 
* `ICollector<T>`
* `IAsyncCollector<T>`
* [`CloudQueue`](/dotnet/api/microsoft.windowsazure.storage.queue.cloudqueue)

<span data-ttu-id="b6158-166">Можно также использовать тип возвращаемого значения метода hello как hello привязка для вывода.</span><span class="sxs-lookup"><span data-stu-id="b6158-166">You can also use hello method return type as hello output binding.</span></span>

<a name="outputsample"></a>

## <a name="queue-output-sample"></a><span data-ttu-id="b6158-167">Пример вывода очереди</span><span class="sxs-lookup"><span data-stu-id="b6158-167">Queue output sample</span></span>
<span data-ttu-id="b6158-168">следующие Hello *function.json* определяет триггер HTTP с очередью привязка для вывода:</span><span class="sxs-lookup"><span data-stu-id="b6158-168">hello following *function.json* defines an HTTP trigger with a queue output binding:</span></span>

```json
{
  "bindings": [
    {
      "type": "httpTrigger",
      "direction": "in",
      "authLevel": "function",
      "name": "input"
    },
    {
      "type": "http",
      "direction": "out",
      "name": "return"
    },
    {
      "type": "queue",
      "direction": "out",
      "name": "$return",
      "queueName": "outqueue",
      "connection": "MyStorageConnectionString",
    }
  ]
}
``` 

<span data-ttu-id="b6158-169">См. Образец hello конкретного языка, выводящий сообщение очереди с hello входящие полезные данные HTTP.</span><span class="sxs-lookup"><span data-stu-id="b6158-169">See hello language-specific sample that outputs a queue message with hello incoming HTTP payload.</span></span>

* [<span data-ttu-id="b6158-170">C#</span><span class="sxs-lookup"><span data-stu-id="b6158-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="b6158-171">Node.js</span><span class="sxs-lookup"><span data-stu-id="b6158-171">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="queue-output-sample-in-c"></a><span data-ttu-id="b6158-172">Пример вывода очереди на C#</span><span class="sxs-lookup"><span data-stu-id="b6158-172">Queue output sample in C#</span></span> #

```cs
// C# example of HTTP trigger binding tooa custom POCO, with a queue output binding
public class CustomQueueMessage
{
    public string PersonName { get; set; }
    public string Title { get; set; }
}

public static CustomQueueMessage Run(CustomQueueMessage input, TraceWriter log)
{
    return input;
}
```

<span data-ttu-id="b6158-173">Используйте несколько сообщений toosend `ICollector`:</span><span class="sxs-lookup"><span data-stu-id="b6158-173">toosend multiple messages, use an `ICollector`:</span></span>

```cs
public static void Run(CustomQueueMessage input, ICollector<CustomQueueMessage> myQueueItem, TraceWriter log)
{
    myQueueItem.Add(input);
    myQueueItem.Add(new CustomQueueMessage { PersonName = "You", Title = "None" });
}
```

<a name="outnodejs"></a>

### <a name="queue-output-sample-in-nodejs"></a><span data-ttu-id="b6158-174">Пример вывода очереди для Node.js</span><span class="sxs-lookup"><span data-stu-id="b6158-174">Queue output sample in Node.js</span></span>

```javascript
module.exports = function (context, input) {
    context.done(null, input.body);
};
```

<span data-ttu-id="b6158-175">Или toosend несколько сообщений</span><span class="sxs-lookup"><span data-stu-id="b6158-175">Or, toosend multiple messages,</span></span>

```javascript
module.exports = function(context) {
    // Define a message array for hello myQueueItem output binding. 
    context.bindings.myQueueItem = ["message 1","message 2"];
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="b6158-176">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b6158-176">Next steps</span></span>

<span data-ttu-id="b6158-177">Пример функции, которая использует очереди хранилища триггеров и привязок см. в разделе [создания функции Azure подключен tooan службы Azure](functions-create-an-azure-connected-function.md).</span><span class="sxs-lookup"><span data-stu-id="b6158-177">For an example of a function that uses queue storage triggers and bindings, see [Create an Azure Function connected tooan Azure service](functions-create-an-azure-connected-function.md).</span></span>

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

<!-- LINKS -->

[`CloudQueueMessage`]: /dotnet/api/microsoft.windowsazure.storage.queue.cloudqueuemessage
