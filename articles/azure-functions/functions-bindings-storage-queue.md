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
# <a name="azure-functions-queue-storage-bindings"></a>Привязки хранилища очередей для Функций Azure
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

В этой статье описывается как tooconfigure и код привязок хранилища очередей Azure в функциях Azure. Функции Azure поддерживают привязки триггера и выходные привязки для очередей Azure. Описание возможностей, доступных во всех привязках, см. в статье [Основные понятия триггеров и привязок в Функциях Azure](functions-triggers-bindings.md).

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="queue-storage-trigger"></a>Триггер хранилища очередей
триггер хранилища очередей Azure Hello позволяет toomonitor хранилища очередей для новых сообщений и реагировать toothem. 

Определение триггера очереди с помощью hello **Интеграция** вкладка на портале функции hello. Hello портал создает следующие определения в hello hello **привязки** раздел *function.json*:

```json
{
    "type": "queueTrigger",
    "direction": "in",
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "queueName": "<Name of queue toopoll>",
    "connection":"<Name of app setting - see below>"
}
```

* Hello `connection` свойство должно содержать имя hello Настройка приложения, содержащий строки подключения хранилища. В hello портал Azure, hello стандартного редактора в hello **Интеграция** настраивает этот параметр приложения автоматически при выборе учетной записи хранилища.

Дополнительные параметры могут быть предоставлены в [host.json файл](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) toofurther тонкой настройки триггеров очереди хранилища. Например можно изменить интервал опроса очереди hello в host.json.

<a name="triggerusage"></a>

## <a name="using-a-queue-trigger"></a>Использование триггера очереди
В функциях Node.js обращаться при помощи данных очереди hello `context.bindings.<name>`.


Функции .NET для получения доступа к очереди hello полезных данных, с помощью параметра метода, например `CloudQueueMessage paramName`. Здесь `paramName` hello значение, указанное в hello [конфигурация триггеров](#trigger). приветственное сообщение очереди может быть десериализованный tooany hello следующие типы:

* Объект POCO. Используйте, если полезные данные очереди hello объекта JSON. Среда выполнения функции Hello десериализует hello полезных данных в объект POCO hello. 
* `string`
* `byte[]`
* [`CloudQueueMessage`]

<a name="meta"></a>

### <a name="queue-trigger-metadata"></a>Метаданные триггера очереди
триггер Hello очередь предоставляет несколько свойств метаданных. Эти свойства можно использовать как часть выражений привязки в других привязках или как параметры в коде. Hello значения имеют hello совпадает с семантикой [ `CloudQueueMessage` ].

* **QueueTrigger** — полезные данные очереди (в случае, если это допустимая строка)
* **DequeueCount** — тип `int`. Здравствуйте, сколько раз сообщение было выведено из очереди.
* **ExpirationTime** — тип `DateTimeOffset?`. Hello время истечения срока действия сообщения hello.
* **Id** — тип `string`. Идентификатор сообщения в очереди.
* **InsertionTime** — тип `DateTimeOffset?`. время Hello, сообщение hello было добавлено toohello очереди.
* **NextVisibleTime** — введите `DateTimeOffset?`. время Hello сообщение hello, теперь будут видны.
* **PopReceipt** — тип `string`. приветственное сообщение подтверждения.

В разделе как toouse hello метаданных очереди в [пример триггера](#triggersample).

<a name="triggersample"></a>

## <a name="trigger-sample"></a>Пример триггера
Предположим, что у вас есть следующие function.json, которая определяет триггер очереди hello:

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

См. пример hello зависящие от языка, который загружает и регистрирует метаданные очереди.

* [C#](#triggercsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>Пример триггера на языке C# #
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

### <a name="trigger-sample-in-nodejs"></a>Пример триггера для Node.js

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

### <a name="handling-poison-queue-messages"></a>Обработка подозрительных сообщений очереди
Функция очереди триггера в случае сбоя функции Azure повторяет этой функции копирования toofive раз для данной очереди сообщения, включая hello сначала попробовать сделать. Если все пять попытки не удались, среда выполнения функции hello добавляет хранилища очереди сообщений tooa с именем  *&lt;originalqueuename >-подозрительных*. Можно написать tooprocess функция сообщения из очереди подозрительных сообщений hello ее регистрации или отправка уведомления о необходимости ручного вмешательства. 

toohandle опасных сообщений вручную, проверьте hello `dequeueCount` hello очереди сообщения (в разделе [метаданных очереди триггера](#meta)).

<a name="output"></a>

## <a name="queue-storage-output-binding"></a>Выходная привязка хранилища очередей
привязка позволяет toowrite сообщений в очереди tooa вывода Hello хранилища очередей Azure. 

Определение очереди привязка для вывода с помощью hello **Интеграция** вкладка на портале функции hello. Hello портал создает следующие определения в hello hello **привязки** раздел *function.json*:

```json
{
   "type": "queue",
   "direction": "out",
   "name": "<hello name used tooidentify hello trigger data in your code>",
   "queueName": "<Name of queue toowrite to>",
   "connection":"<Name of app setting - see below>"
}
```

* Hello `connection` свойство должно содержать имя hello Настройка приложения, содержащий строки подключения хранилища. В hello портал Azure, hello стандартного редактора в hello **Интеграция** настраивает этот параметр приложения автоматически при выборе учетной записи хранилища.

<a name="outputusage"></a>

## <a name="using-a-queue-output-binding"></a>Использование выходной привязки очереди
В функции Node.js, доступ к очереди вывода hello с помощью `context.bindings.<name>`.

В функциях .NET может выводить tooany из hello следующие типы. Если тип параметра `T`, `T` должен быть один из типов hello поддерживается выходных данных, например `string` или POCO.

* `out T` (сериализируется как JSON)
* `out string`
* `out byte[]`
* `out` [`CloudQueueMessage`] 
* `ICollector<T>`
* `IAsyncCollector<T>`
* [`CloudQueue`](/dotnet/api/microsoft.windowsazure.storage.queue.cloudqueue)

Можно также использовать тип возвращаемого значения метода hello как hello привязка для вывода.

<a name="outputsample"></a>

## <a name="queue-output-sample"></a>Пример вывода очереди
следующие Hello *function.json* определяет триггер HTTP с очередью привязка для вывода:

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

См. Образец hello конкретного языка, выводящий сообщение очереди с hello входящие полезные данные HTTP.

* [C#](#outcsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="queue-output-sample-in-c"></a>Пример вывода очереди на C# #

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

Используйте несколько сообщений toosend `ICollector`:

```cs
public static void Run(CustomQueueMessage input, ICollector<CustomQueueMessage> myQueueItem, TraceWriter log)
{
    myQueueItem.Add(input);
    myQueueItem.Add(new CustomQueueMessage { PersonName = "You", Title = "None" });
}
```

<a name="outnodejs"></a>

### <a name="queue-output-sample-in-nodejs"></a>Пример вывода очереди для Node.js

```javascript
module.exports = function (context, input) {
    context.done(null, input.body);
};
```

Или toosend несколько сообщений

```javascript
module.exports = function(context) {
    // Define a message array for hello myQueueItem output binding. 
    context.bindings.myQueueItem = ["message 1","message 2"];
    context.done();
};
```

## <a name="next-steps"></a>Дальнейшие действия

Пример функции, которая использует очереди хранилища триггеров и привязок см. в разделе [создания функции Azure подключен tooan службы Azure](functions-create-an-azure-connected-function.md).

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

<!-- LINKS -->

[`CloudQueueMessage`]: /dotnet/api/microsoft.windowsazure.storage.queue.cloudqueuemessage
