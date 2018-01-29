---
title: "Привязки концентраторов событий Azure для службы \"Функции Azure\""
description: "Узнайте, как использовать привязки концентраторов событий Azure в функциях Azure."
services: functions
documentationcenter: na
author: wesmc7777
manager: cfowler
editor: 
tags: 
keywords: "функции azure, функции, обработка событий, динамические вычисления, независимая архитектура"
ms.assetid: daf81798-7acc-419a-bc32-b5a41c6db56b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/08/2017
ms.author: wesmc
ms.openlocfilehash: 0d48d0b008d76cfb2d7d7815a69774976e184467
ms.sourcegitcommit: 85012dbead7879f1f6c2965daa61302eb78bd366
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/02/2018
---
# <a name="azure-event-hubs-bindings-for-azure-functions"></a>Привязки концентраторов событий Azure для службы "Функции Azure"

Здесь объясняется, как работать с привязками [концентраторов событий Azure](../event-hubs/event-hubs-what-is-event-hubs.md) для службы "Функции Azure". Функции Azure поддерживают привязки триггера и выходные привязки для концентраторов событий Azure.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="trigger"></a>Триггер

Используйте триггер концентраторов событий Azure для ответа на событие, отправленное в поток событий концентратора событий. Чтобы настроить триггер, необходимо иметь доступ для чтения к концентратору событий.

При активации функции триггера концентратора событий сообщение, вызвавшее активацию, передается в функцию в качестве строки.

## <a name="trigger---scaling"></a>Триггер: масштабирование

Каждый экземпляр функции триггера концентратора событий связан только с одним экземпляром EventProcessorHost (EPH). Концентраторы событий гарантируют, что определенный раздел может использоваться только одним экземпляром EPH.

Допустим, мы начинаем работу со следующей конфигурацией для концентратора событий:

1. 10 разделов;
1. 1000 событий, равномерно распределенных между всеми разделами, со 100 сообщениями в каждом разделе.

При включении функции может быть только 1 экземпляр функции. Назовем его Function_0. У экземпляра Function_0 будет один экземпляр EPH, который может использовать все десять разделов. Он начнет считывать события из разделов 0–9. При этом возможно следующее:

* **Требуется только один экземпляр функции**. Экземпляр Function_0 может обработать все 1000 событий, прежде чем запустится логика масштабирования службы "Функции Azure". Другими словами, все 1000 сообщений будут обрабатываться экземпляром Function_0.

* **Необходимо добавить еще один экземпляр функции**. Логика масштабирования службы "Функции Azure" определяет, что у экземпляра Function_0 сообщений больше, чем он может обработать, поэтому создается новый экземпляр Function_1. Концентраторы событий определяют, что новый экземпляр EPH пытается читать сообщения. Концентраторы событий выполнят балансировку нагрузки, распределяя разделы между экземплярами EPH. Например, разделы 0–4 будут присвоены экземпляру Function_0, а разделы 5–9 — экземпляру Function_1. 

* **Необходимо добавить еще несколько (N) экземпляров функции**. Логика масштабирования службы "Функции Azure" определяет, что у экземпляров функции Function_0 и Function_1 сообщений больше, чем они могут обработать. Она снова выполнит масштабирование, добавив экземпляры функции Function_2...N, где N — число, превышающее число разделов концентратора событий. Концентраторы событий выполнят балансировку нагрузки, распределив разделы между экземплярами функций Function_0...9.

Уникальным для текущей логики масштабирования службы "Функции Azure" является то, что N больше числа разделов. Это обеспечивает постоянное наличие экземпляров EPH, готовых к быстрому закреплению за освободившимися разделами. Пользователи платят только за ресурсы, используемые при выполнении экземпляров функции. Плата за подготовку избыточных экземпляров не взимается.

Если функция выполняется без ошибок, в связанную учетную запись хранения добавляются контрольные точки. После этого все 1000 сообщений больше не будут извлекаться.

## <a name="trigger---example"></a>Пример триггера

Языковой пример см. в разделах:

* [C#](#trigger---c-example)
* [Скрипт C# (.csx)](#trigger---c-script-example)
* [F#](#trigger---f-example)
* [JavaScript](#trigger---javascript-example)

### <a name="trigger---c-example"></a>Пример C# в триггере

В следующем примере показан [функции C#](functions-dotnet-class-library.md) , регистрирующее текста триггера концентратора событий.

```csharp
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

Чтобы получить доступ к метаданным события, создайте привязку к объекту [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) (требуется инструкция `using` для `Microsoft.ServiceBus.Messaging`).

```csharp
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] EventData myEventHubMessage, TraceWriter log)
{
    log.Info($"{Encoding.UTF8.GetString(myEventHubMessage.GetBytes())}");
}
```
Для пакетного получения событий создайте массив `string` или `EventData`.

```cs
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] string[] eventHubMessages, TraceWriter log)
{
    foreach (var message in eventHubMessages)
    {
        log.Info($"C# Event Hub trigger function processed a message: {message}");
    }
}
```

### <a name="trigger---c-script-example"></a>Пример скрипта C# в триггере

В следующем примере показаны привязка триггера концентратора событий в файле *function.json* и [функция сценария C#](functions-reference-csharp.md), которая использует эту привязку. Эта функция записывает в журнал текст сообщений триггера концентратора событий.

Данные привязки в файле *function.json*:

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```
Ниже приведен код скрипта C#.

```cs
using System;

public static void Run(string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

Чтобы получить доступ к метаданным события, создайте привязку к объекту [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) (требуется инструкция using для `Microsoft.ServiceBus.Messaging`).

```cs
#r "Microsoft.ServiceBus"
using System.Text;
using Microsoft.ServiceBus.Messaging;

public static void Run(EventData myEventHubMessage, TraceWriter log)
{
    log.Info($"{Encoding.UTF8.GetString(myEventHubMessage.GetBytes())}");
}
```

Для пакетного получения событий создайте массив `string` или `EventData`.

```cs
public static void Run(string[] eventHubMessages, TraceWriter log)
{
    foreach (var message in eventHubMessages)
    {
        log.Info($"C# Event Hub trigger function processed a message: {message}");
    }
}
```

### <a name="trigger---f-example"></a>Пример F# в триггере

В следующем примере показаны привязка триггера концентратора событий в файле *function.json* и [функция F#](functions-reference-fsharp.md), которая использует эту привязку. Эта функция записывает в журнал текст сообщений триггера концентратора событий.

Данные привязки в файле *function.json*:

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```

Ниже показан код F#.

```fsharp
let Run(myEventHubMessage: string, log: TraceWriter) =
    log.Info(sprintf "F# eventhub trigger function processed work item: %s" myEventHubMessage)
```

### <a name="trigger---javascript-example"></a>Пример JavaScript в триггере

В следующем примере показаны привязка триггера концентратора событий в файле *function.json* и [функция JavaScript](functions-reference-node.md), которая использует эту привязку. Эта функция записывает в журнал текст сообщений триггера концентратора событий.

Данные привязки в файле *function.json*:

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```

Ниже показан код JavaScript.

```javascript
module.exports = function (context, myEventHubMessage) {
    context.log('Node.js eventhub trigger function processed work item', myEventHubMessage);    
    context.done();
};
```

## <a name="trigger---attributes"></a>Атрибуты триггера

В [библиотеки классов C#](functions-dotnet-class-library.md), используйте [EventHubTriggerAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubTriggerAttribute.cs) атрибут, который определен в пакет NuGet [Microsoft.Azure.WebJobs.ServiceBus](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus).

Конструктор атрибута принимает имя концентратора событий, имя группы потребителей и имя параметра приложения, содержащего строку подключения. Дополнительные сведения об этих параметрах см. в разделе [Привязки концентраторов событий функций Azure](#trigger---configuration). Ниже приведен пример атрибута `EventHubTriggerAttribute`.

```csharp
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] string myEventHubMessage, TraceWriter log)
{
    ...
}
```

Полный пример см. в разделе [триггер - пример на C#](#trigger---c-example).

## <a name="trigger---configuration"></a>Конфигурация триггера

В следующей таблице описываются свойства конфигурации привязки, которые задаются в файле *function.json* и атрибуте `EventHubTrigger`.

|свойство function.json | Свойство атрибута |ОПИСАНИЕ|
|---------|---------|----------------------|
|**type** | Недоступно | Нужно задать значение `eventHubTrigger`. Это свойство задается автоматически при создании триггера на портале Azure.|
|**direction** | Недоступно | Нужно задать значение `in`. Это свойство задается автоматически при создании триггера на портале Azure. |
|**name** | Недоступно | Имя переменной, представляющей элемент события в коде функции. | 
|**path** |**EventHubName** | Имя концентратора событий. | 
|**consumerGroup** |**ConsumerGroup** | Необязательное свойство, которое используется для задания [группы потребителей](../event-hubs/event-hubs-features.md#event-consumers), используемой для подписки на события в концентраторе. Если аргумент опущен, используется группа потребителей `$Default`. | 
|**подключение** |**Connection** | Имя параметра приложения, содержащего строку подключения к пространству имен концентратора событий. Скопируйте эту строку подключения, нажав кнопку **Сведения о подключении** для *пространства имен*, а не сам концентратор событий. Для активации триггера эта строка подключения должна обладать, по крайней мере, правами на чтение.|

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

## <a name="trigger---hostjson-properties"></a>Свойства host.json в триггере

В файле [host.json](functions-host-json.md#eventhub) содержатся параметры, управляющие реакцией триггера концентраторов событий на событие.

[!INCLUDE [functions-host-json-event-hubs](../../includes/functions-host-json-event-hubs.md)]

## <a name="output"></a>Выходные данные

Используйте выходную привязку концентраторов событий для записи событий в поток событий. Чтобы записывать события в концентратор событий, необходимо иметь разрешение на оправку в него событий.

## <a name="output---example"></a>Пример выходных данных

Языковой пример см. в разделах:

* [C#](#output---c-example)
* [Скрипт C# (.csx)](#output---c-script-example)
* [F#](#output---f-example)
* [JavaScript](#output---javascript-example)

### <a name="output---c-example"></a>Пример выходных данных C#

В следующем примере показан [функции C#](functions-dotnet-class-library.md) , записывает сообщение в концентратор событий с помощью возвращаемого значения метода в качестве результата:

```csharp
[FunctionName("EventHubOutput")]
[return: EventHub("outputEventHubMessage", Connection = "EventHubConnection")]
public static string Run([TimerTrigger("0 */5 * * * *")] TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
    return $"{DateTime.Now}";
}
```

### <a name="output---c-script-example"></a>Пример выходных данных скрипта C#

В следующем примере показаны привязка триггера концентратора событий в файле *function.json* и [функция сценария C#](functions-reference-csharp.md), которая использует эту привязку. Эта функция записывает сообщение в концентратор событий.

Данные привязки в файле *function.json*:

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

Ниже приведен код сценария C#, который создает одно сообщение.

```cs
using System;

public static void Run(TimerInfo myTimer, out string outputEventHubMessage, TraceWriter log)
{
    String msg = $"TimerTriggerCSharp1 executed at: {DateTime.Now}";
    log.Verbose(msg);   
    outputEventHubMessage = msg;
}
```

Ниже приведен код сценария C#, который создает несколько сообщений.

```cs
public static void Run(TimerInfo myTimer, ICollector<string> outputEventHubMessage, TraceWriter log)
{
    string message = $"Event Hub message created at: {DateTime.Now}";
    log.Info(message);
    outputEventHubMessage.Add("1 " + message);
    outputEventHubMessage.Add("2 " + message);
}
```

### <a name="output---f-example"></a>Пример выходных данных F#

В следующем примере показаны привязка триггера концентратора событий в файле *function.json* и [функция F#](functions-reference-fsharp.md), которая использует эту привязку. Эта функция записывает сообщение в концентратор событий.

Данные привязки в файле *function.json*:

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

Ниже показан код F#.

```fsharp
let Run(myTimer: TimerInfo, outputEventHubMessage: byref<string>, log: TraceWriter) =
    let msg = sprintf "TimerTriggerFSharp1 executed at: %s" DateTime.Now.ToString()
    log.Verbose(msg);
    outputEventHubMessage <- msg;
```

### <a name="output---javascript-example"></a>Пример выходных данных JavaScript

В следующем примере показаны привязка триггера концентратора событий в файле *function.json* и [функция JavaScript](functions-reference-node.md), которая использует эту привязку. Эта функция записывает сообщение в концентратор событий.

Данные привязки в файле *function.json*:

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

Ниже приведен код JavaScript, который отправляет отдельное сообщение.

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();
    context.log('Event Hub message created at: ', timeStamp);   
    context.bindings.outputEventHubMessage = "Event Hub message created at: " + timeStamp;
    context.done();
};
```

Ниже приведен код JavaScript, который отправляет несколько сообщений.

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

## <a name="output---attributes"></a>Выходные атрибуты

Для [библиотеки классов C#](functions-dotnet-class-library.md), используйте [EventHubAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs) атрибут, который определен в пакет NuGet [Microsoft.Azure.WebJobs.ServiceBus](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus).

Конструктор атрибута принимает имя концентратора событий и имя параметра приложения, содержащего строку подключения. Дополнительные сведения об этих параметрах см. в разделе [Привязки концентраторов событий функций Azure](#output---configuration). Ниже приведен пример атрибута `EventHub`.

```csharp
[FunctionName("EventHubOutput")]
[return: EventHub("outputEventHubMessage", Connection = "EventHubConnection")]
public static string Run([TimerTrigger("0 */5 * * * *")] TimerInfo myTimer, TraceWriter log)
{
    ...
}
```

Полный пример см. в разделе [выходные данные - пример на C#](#output---c-example).

## <a name="output---configuration"></a>Выходная конфигурация

В следующей таблице описываются свойства конфигурации привязки, которые задаются в файле *function.json* и атрибуте `EventHub`.

|свойство function.json | Свойство атрибута |ОПИСАНИЕ|
|---------|---------|----------------------|
|**type** | Недоступно | Для этого свойства необходимо задать значение "eventHub" |
|**direction** | Недоступно | Для этого свойства необходимо задать значение out. Этот параметр задается автоматически при создании привязки на портале Azure. |
|**name** | Недоступно | Имя переменной, используемое в коде функции, которая представляет событие. | 
|**path** |**EventHubName** | Имя концентратора событий. | 
|**подключение** |**Connection** | Имя параметра приложения, содержащего строку подключения к пространству имен концентратора событий. Скопируйте эту строку подключения, нажав кнопку **Сведения о подключении** для *пространства имен*, а не сам концентратор событий. Чтобы отправлять сообщения в поток событий, эта строка подключения должна иметь разрешения на отправку.|

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

## <a name="output---usage"></a>Использование выходной привязки

В коде C# и сценарии C# для отправки сообщений используйте параметр метода, например `out string paramName`. В скрипте C# `paramName` — это значение, заданное в свойстве `name` файла *function.json*. Для записи нескольких сообщений можно использовать `ICollector<string>` или `IAsyncCollector<string>` вместо `out string`.

В JavaScript для доступа к выходному событию можно использовать `context.bindings.<name>`. `<name>` — это значение, заданное в свойстве `name` файла *function.json*.

## <a name="next-steps"></a>Дальнейшие действия

> [!div class="nextstepaction"]
> [Основные понятия триггеров и привязок в Функциях Azure](functions-triggers-bindings.md)
