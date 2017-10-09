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
# <a name="azure-functions-service-bus-bindings"></a>Привязки служебной шины в Функциях Azure
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

В этой статье объясняется, как tooconfigure и работать с Azure Service Bus привязок в функциях Azure. 

Функции Azure поддерживают привязки триггера и выходные привязки для очередей и разделов служебной шины.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="service-bus-trigger"></a>Триггер служебной шины
Используйте toomessages toorespond hello Service Bus триггера из очереди служебной шины или раздела. 

Hello триггеров очередей и разделов Service Bus определяются следующие объекты JSON в hello hello `bindings` массив function.json:

* Триггер *очереди*:

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

* Триггер *раздела*:

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

Обратите внимание hello следующие:

* Для `connection`, [создаются Настройка приложения в приложении функции](functions-how-to-use-azure-function-app-settings.md) , который содержит пространство имен служебной шины tooyour строку hello соединения, затем укажите имя параметра приложения hello hello в hello `connection` свойство в триггер. Получить строку подключения hello hello выполните действия, показанные на [получить учетные данные управления hello](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).
  Строка подключения Hello должна иметь для пространства имен Service Bus, не ограниченной tooa определенной очереди или раздела.
  Если оставить `connection` пустой, триггер hello предполагается, что строка подключения шины обслуживания по умолчанию указан в параметр приложения `AzureWebJobsServiceBus`.
* Для свойства `accessRights` возможны такие значения, как `manage` и `listen`. по умолчанию Hello — `manage`, указывающая, что hello `connection` имеет hello **управление** разрешение. При использовании строки подключения, которая не поддерживает hello **управление** набор разрешений, `accessRights` слишком`listen`. В противном случае среда выполнения может произойти сбой при toodo операций, требующих функций hello управление правами.

## <a name="trigger-behavior"></a>Поведение триггера
* **Однопоточную** — по умолчанию процессы среды выполнения функции hello, несколько сообщений параллельно. задать toodirect hello среды выполнения tooprocess только одного очередь или раздел сообщения одновременно, `serviceBus.maxConcurrentCalls` too1 в *host.json*. 
  Сведения о файле *host.json* см. в разделе [Структура папок](functions-reference.md#folder-structure) и статье [host.json](https://github .com/Azure/azure-webjobs-sdk-script/wiki/host.json).
* **Обработка подозрительных сообщений.** В служебной шине выполняется собственная обработка подозрительных сообщений, которую нельзя контролировать или настраивать с помощью конфигурации или кода Функций Azure. 
* **Поведение PeekLock** -среда выполнения функции hello получает сообщение в [ `PeekLock` режим](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) и вызывает метод `Complete` на приветственное сообщение, если функции hello завершается успешно, или вызовы `Abandon` Если hello функция завершается с ошибкой. 
  Если функции hello выполняется дольше, чем hello `PeekLock` время ожидания блокировки hello автоматически обновляется.

<a name="triggerusage"></a>

## <a name="trigger-usage"></a>Использование триггера
В этом разделе показано, как toouse Service Bus триггер в коде функции. 

В C# и F # триггер Service Bus приветственное сообщение может быть десериализованный tooany hello следующие типы входных:

* `string` используется для строковых сообщений.
* `byte[]` используется для двоичных данных.
* Любой [объект](https://msdn.microsoft.com/library/system.object.aspx) используется для сериализованных данных JSON.
  Если пользовательский тип входных данных, объявите например `CustomType`, функции Azure пытается данных JSON toodeserialize hello в указанный тип.
* `BrokeredMessage`-предоставляет вам hello десериализовать сообщение hello [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) метод.

В Node.js триггер Service Bus приветственное сообщение передается в функцию hello как строку или объект JSON.

<a name="triggersample"></a>

## <a name="trigger-sample"></a>Пример триггера
Предположим, что имеется следующая function.json hello:

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

См. пример hello зависящие от языка, который обрабатывает сообщение очереди Service Bus.

* [C#](#triggercsharp)
* [F#](#triggerfsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>Пример триггера на языке C# #

```cs
public static void Run(string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a>Пример триггера на языке F# #

```fsharp
let Run(myQueueItem: string, log: TraceWriter) =
    log.Info(sprintf "F# ServiceBus queue trigger function processed message: %s" myQueueItem)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a>Пример триггера для Node.js

```javascript
module.exports = function(context, myQueueItem) {
    context.log('Node.js ServiceBus queue trigger function processed message', myQueueItem);
    context.done();
};
```

<a name="output"></a>

## <a name="service-bus-output-binding"></a>Выходная привязка служебной шины
выходные данные очередей и разделов Service Bus для функции Hello используйте следующие объекты JSON в hello hello `bindings` массив function.json:

* Выходные данные *очереди*:

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
* Выходные данные *раздела*:

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

Обратите внимание hello следующие:

* Для `connection`, [создаются Настройка приложения в приложении функции](functions-how-to-use-azure-function-app-settings.md) , который содержит пространство имен служебной шины tooyour строку hello соединения, затем укажите имя параметра приложения hello hello в hello `connection` свойство в качестве выходных данных привязка. Получить строку подключения hello hello выполните действия, показанные на [получить учетные данные управления hello](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).
  Строка подключения Hello должна иметь для пространства имен Service Bus, не ограниченной tooa определенной очереди или раздела.
  Если оставить `connection` пустой, hello привязка для вывода предполагается, что строка подключения шины обслуживания по умолчанию указан в параметр приложения `AzureWebJobsServiceBus`.
* Для свойства `accessRights` возможны такие значения, как `manage` и `listen`. по умолчанию Hello — `manage`, указывающая, что hello `connection` имеет hello **управление** разрешение. При использовании строки подключения, которая не поддерживает hello **управление** набор разрешений, `accessRights` слишком`listen`. В противном случае среда выполнения может произойти сбой при toodo операций, требующих функций hello управление правами.

<a name="outputusage"></a>

## <a name="output-usage"></a>Использование выходной привязки
В C# и F # функции Azure можно создать сообщение очереди служебной шины из любого hello следующие типы:

* Любой [объект](https://msdn.microsoft.com/library/system.object.aspx). Определение параметра выглядит так: `out T paramName` (C#).
  Функции десериализует hello объекта в сообщение JSON. Если при выходе из функции hello hello выходное значение равно null, функции создает приветственное сообщение с пустым объектом.
* `string`. Определение параметра выглядит так: `out string paraName` (C#). Если значение параметра hello отлично от null, при выходе из функции hello, функции создает сообщение.
* `byte[]`. Определение параметра выглядит так: `out byte[] paraName` (C#). Если значение параметра hello отлично от null, при выходе из функции hello, функции создает сообщение.
* `BrokeredMessage`. Определение параметра выглядит так: `out BrokeredMessage paraName` (C#). Если значение параметра hello отлично от null, при выходе из функции hello, функции создает сообщение.

Чтобы создать несколько сообщений в функции C#, можно использовать `ICollector<T>` или `IAsyncCollector<T>`. Сообщение создается при вызове hello `Add` метод.

В Node.js, можно назначить строку, байтовый массив или объект Javascript (десериализовать в JSON) слишком`context.binding.<paramName>`.

<a name="outputsample"></a>

## <a name="output-sample"></a>Пример выходной привязки
Предположим, что имеется следующая function.json hello, определяющий выходной очереди служебной шины:

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

См. Образец hello конкретного языка, отправляет в очередь сообщение toohello служебной шины.

* [C#](#outcsharp)
* [F#](#outfsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Пример выходной привязки для языка C# #

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, out string outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue = message;
}
```

Или toocreate несколько сообщений:

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

### <a name="output-sample-in-f"></a>Пример выходной привязки для языка F# #

```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter, outputSbQueue: byref<string>) =
    let message = sprintf "Service Bus queue message created at: %s" (DateTime.Now.ToString())
    log.Info(message)
    outputSbQueue = message
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a>Пример выходной привязки для Node.js

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = message;
    context.done();
};
```

Или toocreate несколько сообщений:

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

## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

