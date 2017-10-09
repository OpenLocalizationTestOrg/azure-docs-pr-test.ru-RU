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
# <a name="azure-functions-storage-table-bindings"></a><span data-ttu-id="0af5e-104">Привязки таблиц службы хранилища для Функций Azure</span><span class="sxs-lookup"><span data-stu-id="0af5e-104">Azure Functions Storage table bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="0af5e-105">В этой статье объясняется, как привязки в функциях Azure таблицу tooconfigure и код хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="0af5e-105">This article explains how tooconfigure and code Azure Storage table bindings in Azure Functions.</span></span> <span data-ttu-id="0af5e-106">Функции Azure поддерживают входные и выходные привязки для таблиц службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="0af5e-106">Azure Functions supports input and output bindings for Azure Storage tables.</span></span>

<span data-ttu-id="0af5e-107">Привязка таблицы хранилища Hello поддерживает hello следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="0af5e-107">hello Storage table binding supports hello following scenarios:</span></span>

* <span data-ttu-id="0af5e-108">**Чтение одной строкой в функции C# или Node.** Задайте свойства `partitionKey` и `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="0af5e-108">**Read a single row in a C# or Node.js function** - Set `partitionKey` and `rowKey`.</span></span> <span data-ttu-id="0af5e-109">Hello `filter` и `take` свойства не используются в этом сценарии.</span><span class="sxs-lookup"><span data-stu-id="0af5e-109">hello `filter` and `take` properties are not used in this scenario.</span></span>
* <span data-ttu-id="0af5e-110">**Чтение нескольких строк в функции C#** -среда выполнения функции hello предоставляет `IQueryable<T>` объект привязан toohello таблицы.</span><span class="sxs-lookup"><span data-stu-id="0af5e-110">**Read multiple rows in a C# function** - hello Functions runtime provides an `IQueryable<T>` object bound toohello table.</span></span> <span data-ttu-id="0af5e-111">Тип `T` должен быть производным от типа `TableEntity` или реализацией типа `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="0af5e-111">Type `T` must derive from `TableEntity` or implement `ITableEntity`.</span></span> <span data-ttu-id="0af5e-112">Hello `partitionKey`, `rowKey`, `filter`, и `take` свойства не используются в этом сценарии, вы можете использовать hello `IQueryable` объекта toodo требуется какой-либо фильтрации.</span><span class="sxs-lookup"><span data-stu-id="0af5e-112">hello `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario; you can use hello `IQueryable` object toodo any filtering required.</span></span> 
* <span data-ttu-id="0af5e-113">**Чтение нескольких строк в функции узел** — задайте hello `filter` и `take` свойства.</span><span class="sxs-lookup"><span data-stu-id="0af5e-113">**Read multiple rows in a Node function** - Set hello `filter` and `take` properties.</span></span> <span data-ttu-id="0af5e-114">Не определяйте свойства `partitionKey` и `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="0af5e-114">Don't set `partitionKey` or `rowKey`.</span></span>
* <span data-ttu-id="0af5e-115">**Запись одной или нескольких строк в функции C#** -среда выполнения функции hello предоставляет `ICollector<T>` или `IAsyncCollector<T>` toohello связанные таблицы, где `T` указывает схему hello сущностей hello требуется tooadd.</span><span class="sxs-lookup"><span data-stu-id="0af5e-115">**Write one or more rows in a C# function** - hello Functions runtime provides an `ICollector<T>` or `IAsyncCollector<T>` bound toohello table, where `T` specifies hello schema of hello entities you want tooadd.</span></span> <span data-ttu-id="0af5e-116">Как правило, тип `T` является производным от `TableEntity` или реализует `ITableEntity`, но это не обязательно.</span><span class="sxs-lookup"><span data-stu-id="0af5e-116">Typically, type `T` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="0af5e-117">Hello `partitionKey`, `rowKey`, `filter`, и `take` свойства не используются в этом сценарии.</span><span class="sxs-lookup"><span data-stu-id="0af5e-117">hello `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="storage-table-input-binding"></a><span data-ttu-id="0af5e-118">Входная привязка таблицы службы хранилища</span><span class="sxs-lookup"><span data-stu-id="0af5e-118">Storage table input binding</span></span>
<span data-ttu-id="0af5e-119">Hello входной привязки таблицы хранилища Azure позволяет toouse таблицы в функции хранилища.</span><span class="sxs-lookup"><span data-stu-id="0af5e-119">hello Azure Storage table input binding enables you toouse a storage table in your function.</span></span> 

<span data-ttu-id="0af5e-120">Hello функции tooa входной таблицы хранилища использует следующие объекты JSON в hello hello `bindings` массив function.json:</span><span class="sxs-lookup"><span data-stu-id="0af5e-120">hello Storage table input tooa function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

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

<span data-ttu-id="0af5e-121">Обратите внимание hello следующие:</span><span class="sxs-lookup"><span data-stu-id="0af5e-121">Note hello following:</span></span> 

* <span data-ttu-id="0af5e-122">Используйте `partitionKey` и `rowKey` вместе tooread одной сущности.</span><span class="sxs-lookup"><span data-stu-id="0af5e-122">Use `partitionKey` and `rowKey` together tooread a single entity.</span></span> <span data-ttu-id="0af5e-123">Эти свойства являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="0af5e-123">These properties are optional.</span></span> 
* <span data-ttu-id="0af5e-124">`connection`должно содержать имя hello, содержащий строку соединения хранения параметра приложения.</span><span class="sxs-lookup"><span data-stu-id="0af5e-124">`connection` must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="0af5e-125">В hello портал Azure, hello стандартного редактора в hello **Интеграция** настраивает этот параметр приложения для вас при создании хранилища учетной записи или выбирает один из уже существующих.</span><span class="sxs-lookup"><span data-stu-id="0af5e-125">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="0af5e-126">Вы можете также [настроить этот параметр приложения вручную](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="0af5e-126">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span>  

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="0af5e-127">Использование входной привязки</span><span class="sxs-lookup"><span data-stu-id="0af5e-127">Input usage</span></span>
<span data-ttu-id="0af5e-128">В C# функции, привязка toohello входной таблицы сущности (или сущностей) с помощью именованного параметра в подписи функции, например `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="0af5e-128">In C# functions, you bind toohello input table entity (or entities) by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="0af5e-129">Где `T` имеет тип данных hello нужных данных toodeserialize hello в, и `paramName` — hello имя, указанное в hello [входной привязки](#input).</span><span class="sxs-lookup"><span data-stu-id="0af5e-129">Where `T` is hello data type that you want toodeserialize hello data into, and `paramName` is hello name you specified in hello [input binding](#input).</span></span> <span data-ttu-id="0af5e-130">В функции Node.js, доступ к hello входной таблицы сущности (или сущностей) с помощью `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="0af5e-130">In Node.js functions, you access hello input table entity (or entities) using `context.bindings.<name>`.</span></span>

<span data-ttu-id="0af5e-131">Hello входные данные могут быть десериализованы в функциях, Node.js или C#.</span><span class="sxs-lookup"><span data-stu-id="0af5e-131">hello input data can be deserialized in Node.js or C# functions.</span></span> <span data-ttu-id="0af5e-132">Hello десериализовать объекты имеют `RowKey` и `PartitionKey` свойства.</span><span class="sxs-lookup"><span data-stu-id="0af5e-132">hello deserialized objects have `RowKey` and `PartitionKey` properties.</span></span>

<span data-ttu-id="0af5e-133">В C# функции можно также привязать tooany из hello следующие типы, а также функции hello, среда выполнения будет пытаться десериализовать слишком hello таблицы данных, с помощью этого типа:</span><span class="sxs-lookup"><span data-stu-id="0af5e-133">In C# functions, you can also bind tooany of hello following types, and hello Functions runtime will attempt too deserialize hello table data using that type:</span></span>

* <span data-ttu-id="0af5e-134">Любой тип, реализующий объект `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="0af5e-134">Any type that implements `ITableEntity`</span></span>
* `IQueryable<T>`

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="0af5e-135">Пример входной привязки</span><span class="sxs-lookup"><span data-stu-id="0af5e-135">Input sample</span></span>
<span data-ttu-id="0af5e-136">Предположим, что у вас есть следующие function.json, использующий очереди триггера tooread одну строку hello.</span><span class="sxs-lookup"><span data-stu-id="0af5e-136">Supposed you have hello following function.json, which uses a queue trigger tooread a single table row.</span></span> <span data-ttu-id="0af5e-137">Hello JSON определяет `PartitionKey`  
 `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="0af5e-137">hello JSON specifies `PartitionKey` 
`RowKey`.</span></span> <span data-ttu-id="0af5e-138">`"rowKey": "{queueTrigger}"`Указывает, что этот ключ строки hello поступают из строки сообщения hello очереди.</span><span class="sxs-lookup"><span data-stu-id="0af5e-138">`"rowKey": "{queueTrigger}"` indicates that hello row key comes from hello queue message string.</span></span>

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

<span data-ttu-id="0af5e-139">См. пример hello зависящие от языка, который считывает сущности одной таблицы.</span><span class="sxs-lookup"><span data-stu-id="0af5e-139">See hello language-specific sample that reads a single table entity.</span></span>

* [<span data-ttu-id="0af5e-140">C#</span><span class="sxs-lookup"><span data-stu-id="0af5e-140">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="0af5e-141">F#</span><span class="sxs-lookup"><span data-stu-id="0af5e-141">F#</span></span>](#inputfsharp)
* [<span data-ttu-id="0af5e-142">Node.js</span><span class="sxs-lookup"><span data-stu-id="0af5e-142">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="0af5e-143">Пример входной привязки для языка C#</span><span class="sxs-lookup"><span data-stu-id="0af5e-143">Input sample in C#</span></span> #
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

### <a name="input-sample-in-f"></a><span data-ttu-id="0af5e-144">Пример входной привязки для языка F#</span><span class="sxs-lookup"><span data-stu-id="0af5e-144">Input sample in F#</span></span> #
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

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="0af5e-145">Пример входной привязки для Node.js</span><span class="sxs-lookup"><span data-stu-id="0af5e-145">Input sample in Node.js</span></span>
```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);
    context.log('Person entity name: ' + context.bindings.personEntity.Name);
    context.done();
};
```

<a name="output"></a>

## <a name="storage-table-output-binding"></a><span data-ttu-id="0af5e-146">Выходная привязка таблицы службы хранилища</span><span class="sxs-lookup"><span data-stu-id="0af5e-146">Storage table output binding</span></span>
<span data-ttu-id="0af5e-147">Привязка включает таблицу хранилища tooa toowrite сущностей в функции вывода Hello таблице хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="0af5e-147">hello Azure Storage table output binding enables you toowrite entities tooa Storage table in your function.</span></span> 

<span data-ttu-id="0af5e-148">Здравствуйте выходной таблицы хранилища для функции используются следующие объекты JSON в hello hello `bindings` массив function.json:</span><span class="sxs-lookup"><span data-stu-id="0af5e-148">hello Storage table output for a function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

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

<span data-ttu-id="0af5e-149">Обратите внимание hello следующие:</span><span class="sxs-lookup"><span data-stu-id="0af5e-149">Note hello following:</span></span> 

* <span data-ttu-id="0af5e-150">Используйте `partitionKey` и `rowKey` вместе toowrite одной сущности.</span><span class="sxs-lookup"><span data-stu-id="0af5e-150">Use `partitionKey` and `rowKey` together toowrite a single entity.</span></span> <span data-ttu-id="0af5e-151">Эти свойства являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="0af5e-151">These properties are optional.</span></span> <span data-ttu-id="0af5e-152">Можно также указать `PartitionKey` и `RowKey` при создании hello объектов сущностей в коде функции.</span><span class="sxs-lookup"><span data-stu-id="0af5e-152">You can also specify `PartitionKey` and `RowKey` when you create hello entity objects in your function code.</span></span>
* <span data-ttu-id="0af5e-153">`connection`должно содержать имя hello, содержащий строку соединения хранения параметра приложения.</span><span class="sxs-lookup"><span data-stu-id="0af5e-153">`connection` must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="0af5e-154">В hello портал Azure, hello стандартного редактора в hello **Интеграция** настраивает этот параметр приложения для вас при создании хранилища учетной записи или выбирает один из уже существующих.</span><span class="sxs-lookup"><span data-stu-id="0af5e-154">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="0af5e-155">Вы можете также [настроить этот параметр приложения вручную](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="0af5e-155">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span> 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="0af5e-156">Использование выходной привязки</span><span class="sxs-lookup"><span data-stu-id="0af5e-156">Output usage</span></span>
<span data-ttu-id="0af5e-157">В C# функции, можно привязать toohello табличного вывода с помощью hello с именем `out` параметра в подписи функции, такие как `out <T> <name>`, где `T` имеет тип данных hello нужных данных tooserialize hello в, и `paramName` является hello имя указанный в hello [привязка для вывода](#output).</span><span class="sxs-lookup"><span data-stu-id="0af5e-157">In C# functions, you bind toohello table output by using hello named `out` parameter in your function signature, like `out <T> <name>`, where `T` is hello data type that you want tooserialize hello data into, and `paramName` is hello name you specified in hello [output binding](#output).</span></span> <span data-ttu-id="0af5e-158">В функции Node.js, доступ к выходных данных с помощью таблицы hello `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="0af5e-158">In Node.js functions, you access hello table output using `context.bindings.<name>`.</span></span>

<span data-ttu-id="0af5e-159">Вы можете сериализовать объекты в функциях Node.js или C#.</span><span class="sxs-lookup"><span data-stu-id="0af5e-159">You can serialize objects in Node.js or C# functions.</span></span> <span data-ttu-id="0af5e-160">В C# функции можно также привязать toohello следующие типы:</span><span class="sxs-lookup"><span data-stu-id="0af5e-160">In C# functions, you can also bind toohello following types:</span></span>

* <span data-ttu-id="0af5e-161">Любой тип, реализующий объект `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="0af5e-161">Any type that implements `ITableEntity`</span></span>
* <span data-ttu-id="0af5e-162">`ICollector<T>`(toooutput нескольких сущностей.</span><span class="sxs-lookup"><span data-stu-id="0af5e-162">`ICollector<T>` (toooutput multiple entities.</span></span> <span data-ttu-id="0af5e-163">Ознакомьтесь с [примером](#outcsharp).).</span><span class="sxs-lookup"><span data-stu-id="0af5e-163">See [sample](#outcsharp).)</span></span>
* <span data-ttu-id="0af5e-164">`IAsyncCollector<T>` (асинхронная версия `ICollector<T>`).</span><span class="sxs-lookup"><span data-stu-id="0af5e-164">`IAsyncCollector<T>` (async version of `ICollector<T>`)</span></span>
* <span data-ttu-id="0af5e-165">`CloudTable`(с помощью hello пакет SDK хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="0af5e-165">`CloudTable` (using hello Azure Storage SDK.</span></span> <span data-ttu-id="0af5e-166">Ознакомьтесь с [примером](#readmulti).).</span><span class="sxs-lookup"><span data-stu-id="0af5e-166">See [sample](#readmulti).)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="0af5e-167">Пример выходной привязки</span><span class="sxs-lookup"><span data-stu-id="0af5e-167">Output sample</span></span>
<span data-ttu-id="0af5e-168">следующие Hello *function.json* и *run.csx* примере показан как toowrite несколько сущностей в таблице.</span><span class="sxs-lookup"><span data-stu-id="0af5e-168">hello following *function.json* and *run.csx* example shows how toowrite multiple table entities.</span></span>

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

<span data-ttu-id="0af5e-169">См. Образец hello конкретного языка, создающий несколько сущностей в таблице.</span><span class="sxs-lookup"><span data-stu-id="0af5e-169">See hello language-specific sample that creates multiple table entities.</span></span>

* [<span data-ttu-id="0af5e-170">C#</span><span class="sxs-lookup"><span data-stu-id="0af5e-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="0af5e-171">F#</span><span class="sxs-lookup"><span data-stu-id="0af5e-171">F#</span></span>](#outfsharp)
* [<span data-ttu-id="0af5e-172">Node.js</span><span class="sxs-lookup"><span data-stu-id="0af5e-172">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="0af5e-173">Пример выходной привязки для языка C#</span><span class="sxs-lookup"><span data-stu-id="0af5e-173">Output sample in C#</span></span> #
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

### <a name="output-sample-in-f"></a><span data-ttu-id="0af5e-174">Пример выходной привязки для языка F#</span><span class="sxs-lookup"><span data-stu-id="0af5e-174">Output sample in F#</span></span> #
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

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="0af5e-175">Пример выходной привязки для Node.js</span><span class="sxs-lookup"><span data-stu-id="0af5e-175">Output sample in Node.js</span></span>
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

## <a name="sample-read-multiple-table-entities-in-c"></a><span data-ttu-id="0af5e-176">Пример. Чтение нескольких сущностей таблицы на языке C#</span><span class="sxs-lookup"><span data-stu-id="0af5e-176">Sample: Read multiple table entities in C#</span></span>  #
<span data-ttu-id="0af5e-177">следующие Hello *function.json* и пример кода C# считывает сущностей для ключа раздела, который указан в сообщении очереди hello.</span><span class="sxs-lookup"><span data-stu-id="0af5e-177">hello following *function.json* and C# code example reads entities for a partition key that is specified in hello queue message.</span></span>

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

<span data-ttu-id="0af5e-178">Hello кода C# добавляет ссылку toohello пакет SDK хранилища Azure, позволяя hello объекта типа могут быть производными от `TableEntity`.</span><span class="sxs-lookup"><span data-stu-id="0af5e-178">hello C# code adds a reference toohello Azure Storage SDK so that hello entity type can derive from `TableEntity`.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0af5e-179">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0af5e-179">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

