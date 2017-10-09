---
title: "привязки таблицы хранилища функции aaaAzure | Документы Microsoft"
description: "Понять, как привязки toouse хранилища Azure в функциях Azure."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "функции azure, функции, обработка событий, динамические вычисления, независимая архитектура"
ms.assetid: 65b3437e-2571-4d3f-a996-61a74b50a1c2
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/28/2016
ms.author: chrande
ms.openlocfilehash: 90c2a73329139d4ab3504bc0e2c90370133158bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-storage-table-bindings"></a>Привязки таблиц службы хранилища для Функций Azure
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

В этой статье объясняется, как привязки в функциях Azure таблицу tooconfigure и код хранилища Azure. Функции Azure поддерживают входные и выходные привязки для таблиц службы хранилища Azure.

Привязка таблицы хранилища Hello поддерживает hello следующие сценарии:

* **Чтение одной строкой в функции C# или Node.** Задайте свойства `partitionKey` и `rowKey`. Hello `filter` и `take` свойства не используются в этом сценарии.
* **Чтение нескольких строк в функции C#** -среда выполнения функции hello предоставляет `IQueryable<T>` объект привязан toohello таблицы. Тип `T` должен быть производным от типа `TableEntity` или реализацией типа `ITableEntity`. Hello `partitionKey`, `rowKey`, `filter`, и `take` свойства не используются в этом сценарии, вы можете использовать hello `IQueryable` объекта toodo требуется какой-либо фильтрации. 
* **Чтение нескольких строк в функции узел** — задайте hello `filter` и `take` свойства. Не определяйте свойства `partitionKey` и `rowKey`.
* **Запись одной или нескольких строк в функции C#** -среда выполнения функции hello предоставляет `ICollector<T>` или `IAsyncCollector<T>` toohello связанные таблицы, где `T` указывает схему hello сущностей hello требуется tooadd. Как правило, тип `T` является производным от `TableEntity` или реализует `ITableEntity`, но это не обязательно. Hello `partitionKey`, `rowKey`, `filter`, и `take` свойства не используются в этом сценарии.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="storage-table-input-binding"></a>Входная привязка таблицы службы хранилища
Hello входной привязки таблицы хранилища Azure позволяет toouse таблицы в функции хранилища. 

Hello функции tooa входной таблицы хранилища использует следующие объекты JSON в hello hello `bindings` массив function.json:

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "in",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity tooread - see below>",
    "rowKey": "<RowKey of table entity tooread - see below>",
    "take": "<Maximum number of entities tooread in Node.js - optional>",
    "filter": "<OData filter expression for table input in Node.js - optional>",
    "connection": "<Name of app setting - see below>",
}
```

Обратите внимание hello следующие: 

* Используйте `partitionKey` и `rowKey` вместе tooread одной сущности. Эти свойства являются необязательными. 
* `connection`должно содержать имя hello, содержащий строку соединения хранения параметра приложения. В hello портал Azure, hello стандартного редактора в hello **Интеграция** настраивает этот параметр приложения для вас при создании хранилища учетной записи или выбирает один из уже существующих. Вы можете также [настроить этот параметр приложения вручную](functions-how-to-use-azure-function-app-settings.md#settings).  

<a name="inputusage"></a>

## <a name="input-usage"></a>Использование входной привязки
В C# функции, привязка toohello входной таблицы сущности (или сущностей) с помощью именованного параметра в подписи функции, например `<T> <name>`.
Где `T` имеет тип данных hello нужных данных toodeserialize hello в, и `paramName` — hello имя, указанное в hello [входной привязки](#input). В функции Node.js, доступ к hello входной таблицы сущности (или сущностей) с помощью `context.bindings.<name>`.

Hello входные данные могут быть десериализованы в функциях, Node.js или C#. Hello десериализовать объекты имеют `RowKey` и `PartitionKey` свойства.

В C# функции можно также привязать tooany из hello следующие типы, а также функции hello, среда выполнения будет пытаться десериализовать слишком hello таблицы данных, с помощью этого типа:

* Любой тип, реализующий объект `ITableEntity`.
* `IQueryable<T>`

<a name="inputsample"></a>

## <a name="input-sample"></a>Пример входной привязки
Предположим, что у вас есть следующие function.json, использующий очереди триггера tooread одну строку hello. Hello JSON определяет `PartitionKey`  
 `RowKey`. `"rowKey": "{queueTrigger}"`Указывает, что этот ключ строки hello поступают из строки сообщения hello очереди.

```json
{
  "bindings": [
    {
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
      "name": "myQueueItem",
      "type": "queueTrigger",
      "direction": "in"
    },
    {
      "name": "personEntity",
      "type": "table",
      "tableName": "Person",
      "partitionKey": "Test",
      "rowKey": "{queueTrigger}",
      "connection": "MyStorageConnection",
      "direction": "in"
    }
  ],
  "disabled": false
}
```

См. пример hello зависящие от языка, который считывает сущности одной таблицы.

* [C#](#inputcsharp)
* [F#](#inputfsharp)
* [Node.js](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a>Пример входной привязки для языка C# #
```csharp
public static void Run(string myQueueItem, Person personEntity, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    log.Info($"Name in Person entity: {personEntity.Name}");
}

public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
}
```

<a name="inputfsharp"></a>

### <a name="input-sample-in-f"></a>Пример входной привязки для языка F# #
```fsharp
[<CLIMutable>]
type Person = {
  PartitionKey: string
  RowKey: string
  Name: string
}

let Run(myQueueItem: string, personEntity: Person) =
    log.Info(sprintf "F# Queue trigger function processed: %s" myQueueItem)
    log.Info(sprintf "Name in Person entity: %s" personEntity.Name)
```

<a name="inputnodejs"></a>

### <a name="input-sample-in-nodejs"></a>Пример входной привязки для Node.js
```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);
    context.log('Person entity name: ' + context.bindings.personEntity.Name);
    context.done();
};
```

<a name="output"></a>

## <a name="storage-table-output-binding"></a>Выходная привязка таблицы службы хранилища
Привязка включает таблицу хранилища tooa toowrite сущностей в функции вывода Hello таблице хранилища Azure. 

Здравствуйте выходной таблицы хранилища для функции используются следующие объекты JSON в hello hello `bindings` массив function.json:

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "out",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity toowrite - see below>",
    "rowKey": "<RowKey of table entity toowrite - see below>",
    "connection": "<Name of app setting - see below>",
}
```

Обратите внимание hello следующие: 

* Используйте `partitionKey` и `rowKey` вместе toowrite одной сущности. Эти свойства являются необязательными. Можно также указать `PartitionKey` и `RowKey` при создании hello объектов сущностей в коде функции.
* `connection`должно содержать имя hello, содержащий строку соединения хранения параметра приложения. В hello портал Azure, hello стандартного редактора в hello **Интеграция** настраивает этот параметр приложения для вас при создании хранилища учетной записи или выбирает один из уже существующих. Вы можете также [настроить этот параметр приложения вручную](functions-how-to-use-azure-function-app-settings.md#settings). 

<a name="outputusage"></a>

## <a name="output-usage"></a>Использование выходной привязки
В C# функции, можно привязать toohello табличного вывода с помощью hello с именем `out` параметра в подписи функции, такие как `out <T> <name>`, где `T` имеет тип данных hello нужных данных tooserialize hello в, и `paramName` является hello имя указанный в hello [привязка для вывода](#output). В функции Node.js, доступ к выходных данных с помощью таблицы hello `context.bindings.<name>`.

Вы можете сериализовать объекты в функциях Node.js или C#. В C# функции можно также привязать toohello следующие типы:

* Любой тип, реализующий объект `ITableEntity`.
* `ICollector<T>`(toooutput нескольких сущностей. Ознакомьтесь с [примером](#outcsharp).).
* `IAsyncCollector<T>` (асинхронная версия `ICollector<T>`).
* `CloudTable`(с помощью hello пакет SDK хранилища Azure. Ознакомьтесь с [примером](#readmulti).).

<a name="outputsample"></a>

## <a name="output-sample"></a>Пример выходной привязки
следующие Hello *function.json* и *run.csx* примере показан как toowrite несколько сущностей в таблице.

```json
{
  "bindings": [
    {
      "name": "input",
      "type": "manualTrigger",
      "direction": "in"
    },
    {
      "tableName": "Person",
      "connection": "MyStorageConnection",
      "name": "tableBinding",
      "type": "table",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

См. Образец hello конкретного языка, создающий несколько сущностей в таблице.

* [C#](#outcsharp)
* [F#](#outfsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Пример выходной привязки для языка C# #
```csharp
public static void Run(string input, ICollector<Person> tableBinding, TraceWriter log)
{
    for (int i = 1; i < 10; i++)
        {
            log.Info($"Adding Person entity {i}");
            tableBinding.Add(
                new Person() { 
                    PartitionKey = "Test", 
                    RowKey = i.ToString(), 
                    Name = "Name" + i.ToString() }
                );
        }

}

public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
}

```
<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a>Пример выходной привязки для языка F# #
```fsharp
[<CLIMutable>]
type Person = {
  PartitionKey: string
  RowKey: string
  Name: string
}

let Run(input: string, tableBinding: ICollector<Person>, log: TraceWriter) =
    for i = 1 too10 do
        log.Info(sprintf "Adding Person entity %d" i)
        tableBinding.Add(
            { PartitionKey = "Test"
              RowKey = i.ToString()
              Name = "Name" + i.ToString() })
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a>Пример выходной привязки для Node.js
```javascript
module.exports = function (context) {

    context.bindings.tableBinding = [];

    for (var i = 1; i < 10; i++) {
        context.bindings.tableBinding.push({
            PartitionKey: "Test",
            RowKey: i.toString(),
            Name: "Name " + i
        });
    }
    
    context.done();
};
```

<a name="readmulti"></a>

## <a name="sample-read-multiple-table-entities-in-c"></a>Пример. Чтение нескольких сущностей таблицы на языке C#  #
следующие Hello *function.json* и пример кода C# считывает сущностей для ключа раздела, который указан в сообщении очереди hello.

```json
{
  "bindings": [
    {
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
      "name": "myQueueItem",
      "type": "queueTrigger",
      "direction": "in"
    },
    {
      "name": "tableBinding",
      "type": "table",
      "connection": "MyStorageConnection",
      "tableName": "Person",
      "direction": "in"
    }
  ],
  "disabled": false
}
```

Hello кода C# добавляет ссылку toohello пакет SDK хранилища Azure, позволяя hello объекта типа могут быть производными от `TableEntity`.

```csharp
#r "Microsoft.WindowsAzure.Storage"
using Microsoft.WindowsAzure.Storage.Table;

public static void Run(string myQueueItem, IQueryable<Person> tableBinding, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    foreach (Person person in tableBinding.Where(p => p.PartitionKey == myQueueItem).ToList())
    {
        log.Info($"Name: {person.Name}");
    }
}

public class Person : TableEntity
{
    public string Name { get; set; }
}
```

## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

