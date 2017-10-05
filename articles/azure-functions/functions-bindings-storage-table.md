---
title: "Привязки таблиц службы хранилища для Функций Azure | Документация Майкрософт"
description: "Узнайте, как использовать привязки службы хранилища Azure в Функциях Azure."
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
ms.openlocfilehash: bb01be3ee044f60376e0c9c2de7b3dd34f3b7aca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-storage-table-bindings"></a><span data-ttu-id="86cf8-104">Привязки таблиц службы хранилища для Функций Azure</span><span class="sxs-lookup"><span data-stu-id="86cf8-104">Azure Functions Storage table bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="86cf8-105">В этой статье поясняется, как настроить и запрограммировать привязки для таблиц службы хранилища Azure в Функциях Azure.</span><span class="sxs-lookup"><span data-stu-id="86cf8-105">This article explains how to configure and code Azure Storage table bindings in Azure Functions.</span></span> <span data-ttu-id="86cf8-106">Функции Azure поддерживают входные и выходные привязки для таблиц службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="86cf8-106">Azure Functions supports input and output bindings for Azure Storage tables.</span></span>

<span data-ttu-id="86cf8-107">Привязка таблицы службы хранилища применима в следующих сценариях:</span><span class="sxs-lookup"><span data-stu-id="86cf8-107">The Storage table binding supports the following scenarios:</span></span>

* <span data-ttu-id="86cf8-108">**Чтение одной строкой в функции C# или Node.** Задайте свойства `partitionKey` и `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="86cf8-108">**Read a single row in a C# or Node.js function** - Set `partitionKey` and `rowKey`.</span></span> <span data-ttu-id="86cf8-109">Свойства `filter` и `take` не используются в этом сценарии.</span><span class="sxs-lookup"><span data-stu-id="86cf8-109">The `filter` and `take` properties are not used in this scenario.</span></span>
* <span data-ttu-id="86cf8-110">**Чтение нескольких строк в функции C#.** Среда выполнения Функций предоставляет объект `IQueryable<T>`, привязанный к таблице.</span><span class="sxs-lookup"><span data-stu-id="86cf8-110">**Read multiple rows in a C# function** - The Functions runtime provides an `IQueryable<T>` object bound to the table.</span></span> <span data-ttu-id="86cf8-111">Тип `T` должен быть производным от типа `TableEntity` или реализацией типа `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="86cf8-111">Type `T` must derive from `TableEntity` or implement `ITableEntity`.</span></span> <span data-ttu-id="86cf8-112">Свойства `partitionKey`, `rowKey`, `filter` и `take` не используются в этом сценарии. Для фильтрации можно использовать объект `IQueryable`.</span><span class="sxs-lookup"><span data-stu-id="86cf8-112">The `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario; you can use the `IQueryable` object to do any filtering required.</span></span> 
* <span data-ttu-id="86cf8-113">**Чтение нескольких строк в функции Node.** Задайте свойства `filter` и `take`.</span><span class="sxs-lookup"><span data-stu-id="86cf8-113">**Read multiple rows in a Node function** - Set the `filter` and `take` properties.</span></span> <span data-ttu-id="86cf8-114">Не определяйте свойства `partitionKey` и `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="86cf8-114">Don't set `partitionKey` or `rowKey`.</span></span>
* <span data-ttu-id="86cf8-115">**Запись одной или нескольких строк в функции C#.** Среда выполнения Функций предоставляет объект `ICollector<T>` или `IAsyncCollector<T>`, привязанный к таблице, где `T` обозначает схему сущностей, которые нужно добавить.</span><span class="sxs-lookup"><span data-stu-id="86cf8-115">**Write one or more rows in a C# function** - The Functions runtime provides an `ICollector<T>` or `IAsyncCollector<T>` bound to the table, where `T` specifies the schema of the entities you want to add.</span></span> <span data-ttu-id="86cf8-116">Как правило, тип `T` является производным от `TableEntity` или реализует `ITableEntity`, но это не обязательно.</span><span class="sxs-lookup"><span data-stu-id="86cf8-116">Typically, type `T` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="86cf8-117">Свойства `partitionKey`, `rowKey`, `filter` и `take` не используются в этом сценарии.</span><span class="sxs-lookup"><span data-stu-id="86cf8-117">The `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="storage-table-input-binding"></a><span data-ttu-id="86cf8-118">Входная привязка таблицы службы хранилища</span><span class="sxs-lookup"><span data-stu-id="86cf8-118">Storage table input binding</span></span>
<span data-ttu-id="86cf8-119">Входная привязка таблицы службы хранилища Azure позволяет использовать таблицу хранилища в функции.</span><span class="sxs-lookup"><span data-stu-id="86cf8-119">The Azure Storage table input binding enables you to use a storage table in your function.</span></span> 

<span data-ttu-id="86cf8-120">Входные данные таблицы службы хранилища для функции используют следующий объект JSON в массиве `bindings` файла function.json:</span><span class="sxs-lookup"><span data-stu-id="86cf8-120">The Storage table input to a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "in",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity to read - see below>",
    "rowKey": "<RowKey of table entity to read - see below>",
    "take": "<Maximum number of entities to read in Node.js - optional>",
    "filter": "<OData filter expression for table input in Node.js - optional>",
    "connection": "<Name of app setting - see below>",
}
```

<span data-ttu-id="86cf8-121">Обратите внимание на следующее.</span><span class="sxs-lookup"><span data-stu-id="86cf8-121">Note the following:</span></span> 

* <span data-ttu-id="86cf8-122">Используйте совместно свойства `partitionKey` и `rowKey` для чтения одной сущности.</span><span class="sxs-lookup"><span data-stu-id="86cf8-122">Use `partitionKey` and `rowKey` together to read a single entity.</span></span> <span data-ttu-id="86cf8-123">Эти свойства являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="86cf8-123">These properties are optional.</span></span> 
* <span data-ttu-id="86cf8-124">Свойство `connection` должно включать в себя имя параметра приложения, содержащего строку подключения к службе хранилища.</span><span class="sxs-lookup"><span data-stu-id="86cf8-124">`connection` must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="86cf8-125">На портале Azure стандартный редактор на вкладке **Интеграция** автоматически настраивает этот параметр приложения при создании учетной записи хранения или выборе одной из имеющихся.</span><span class="sxs-lookup"><span data-stu-id="86cf8-125">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="86cf8-126">Вы можете также [настроить этот параметр приложения вручную](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="86cf8-126">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span>  

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="86cf8-127">Использование входной привязки</span><span class="sxs-lookup"><span data-stu-id="86cf8-127">Input usage</span></span>
<span data-ttu-id="86cf8-128">В функциях C# можно выполнить привязку к сущности (или сущностям) входной таблицы, используя именованный параметр в сигнатуре функции, например `<T> <name>`,</span><span class="sxs-lookup"><span data-stu-id="86cf8-128">In C# functions, you bind to the input table entity (or entities) by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="86cf8-129">где `T` — это тип данных, в который требуется десериализировать данные, а `paramName` — это имя, указанное во [входной привязке](#input).</span><span class="sxs-lookup"><span data-stu-id="86cf8-129">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [input binding](#input).</span></span> <span data-ttu-id="86cf8-130">В функциях Node.js доступ к сущности (или сущностям) входной таблицы можно получить, используя `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="86cf8-130">In Node.js functions, you access the input table entity (or entities) using `context.bindings.<name>`.</span></span>

<span data-ttu-id="86cf8-131">Входные данные можно десериализировать в функции Node.js или C#.</span><span class="sxs-lookup"><span data-stu-id="86cf8-131">The input data can be deserialized in Node.js or C# functions.</span></span> <span data-ttu-id="86cf8-132">Десериализированный объект имеет свойства `RowKey` и `PartitionKey`.</span><span class="sxs-lookup"><span data-stu-id="86cf8-132">The deserialized objects have `RowKey` and `PartitionKey` properties.</span></span>

<span data-ttu-id="86cf8-133">В функциях C# также можно выполнить привязку к любому из следующих типов. Среда выполнения Функций попытается десериализировать данные таблицы, используя этот тип:</span><span class="sxs-lookup"><span data-stu-id="86cf8-133">In C# functions, you can also bind to any of the following types, and the Functions runtime will attempt to deserialize the table data using that type:</span></span>

* <span data-ttu-id="86cf8-134">Любой тип, реализующий объект `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="86cf8-134">Any type that implements `ITableEntity`</span></span>
* `IQueryable<T>`

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="86cf8-135">Пример входной привязки</span><span class="sxs-lookup"><span data-stu-id="86cf8-135">Input sample</span></span>
<span data-ttu-id="86cf8-136">Предположим, что у вас есть следующий файл function.json, использующий триггер очереди для чтения одной строки таблицы.</span><span class="sxs-lookup"><span data-stu-id="86cf8-136">Supposed you have the following function.json, which uses a queue trigger to read a single table row.</span></span> <span data-ttu-id="86cf8-137">JSON указывает `PartitionKey` 
`RowKey`.</span><span class="sxs-lookup"><span data-stu-id="86cf8-137">The JSON specifies `PartitionKey` 
`RowKey`.</span></span> <span data-ttu-id="86cf8-138">`"rowKey": "{queueTrigger}"` указывает, что ключ строки получен из строки сообщения очереди.</span><span class="sxs-lookup"><span data-stu-id="86cf8-138">`"rowKey": "{queueTrigger}"` indicates that the row key comes from the queue message string.</span></span>

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

<span data-ttu-id="86cf8-139">Ознакомьтесь с примером для конкретного языка, считывающим одну сущность таблицы.</span><span class="sxs-lookup"><span data-stu-id="86cf8-139">See the language-specific sample that reads a single table entity.</span></span>

* [<span data-ttu-id="86cf8-140">C#</span><span class="sxs-lookup"><span data-stu-id="86cf8-140">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="86cf8-141">F#</span><span class="sxs-lookup"><span data-stu-id="86cf8-141">F#</span></span>](#inputfsharp)
* [<span data-ttu-id="86cf8-142">Node.js</span><span class="sxs-lookup"><span data-stu-id="86cf8-142">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="86cf8-143">Пример входной привязки для языка C#</span><span class="sxs-lookup"><span data-stu-id="86cf8-143">Input sample in C#</span></span> #
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

### <a name="input-sample-in-f"></a><span data-ttu-id="86cf8-144">Пример входной привязки для языка F#</span><span class="sxs-lookup"><span data-stu-id="86cf8-144">Input sample in F#</span></span> #
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

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="86cf8-145">Пример входной привязки для Node.js</span><span class="sxs-lookup"><span data-stu-id="86cf8-145">Input sample in Node.js</span></span>
```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);
    context.log('Person entity name: ' + context.bindings.personEntity.Name);
    context.done();
};
```

<a name="output"></a>

## <a name="storage-table-output-binding"></a><span data-ttu-id="86cf8-146">Выходная привязка таблицы службы хранилища</span><span class="sxs-lookup"><span data-stu-id="86cf8-146">Storage table output binding</span></span>
<span data-ttu-id="86cf8-147">Выходная привязка таблицы службы хранилища Azure позволяет записывать сущности в таблицу службы хранилища в функции.</span><span class="sxs-lookup"><span data-stu-id="86cf8-147">The Azure Storage table output binding enables you to write entities to a Storage table in your function.</span></span> 

<span data-ttu-id="86cf8-148">Выходные данные таблицы службы хранилища для функции используют следующий объект JSON в массиве `bindings` файла function.json:</span><span class="sxs-lookup"><span data-stu-id="86cf8-148">The Storage table output for a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "out",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity to write - see below>",
    "rowKey": "<RowKey of table entity to write - see below>",
    "connection": "<Name of app setting - see below>",
}
```

<span data-ttu-id="86cf8-149">Обратите внимание на следующее.</span><span class="sxs-lookup"><span data-stu-id="86cf8-149">Note the following:</span></span> 

* <span data-ttu-id="86cf8-150">Используйте совместно свойства `partitionKey` и `rowKey` для записи одной сущности.</span><span class="sxs-lookup"><span data-stu-id="86cf8-150">Use `partitionKey` and `rowKey` together to write a single entity.</span></span> <span data-ttu-id="86cf8-151">Эти свойства являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="86cf8-151">These properties are optional.</span></span> <span data-ttu-id="86cf8-152">При создании объектов сущностей в коде функции можно также указать `PartitionKey` и `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="86cf8-152">You can also specify `PartitionKey` and `RowKey` when you create the entity objects in your function code.</span></span>
* <span data-ttu-id="86cf8-153">Свойство `connection` должно включать в себя имя параметра приложения, содержащего строку подключения к службе хранилища.</span><span class="sxs-lookup"><span data-stu-id="86cf8-153">`connection` must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="86cf8-154">На портале Azure стандартный редактор на вкладке **Интеграция** автоматически настраивает этот параметр приложения при создании учетной записи хранения или выборе одной из имеющихся.</span><span class="sxs-lookup"><span data-stu-id="86cf8-154">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="86cf8-155">Вы можете также [настроить этот параметр приложения вручную](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="86cf8-155">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span> 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="86cf8-156">Использование выходной привязки</span><span class="sxs-lookup"><span data-stu-id="86cf8-156">Output usage</span></span>
<span data-ttu-id="86cf8-157">В функциях C# можно выполнить привязку к выходным данным таблицы, используя именованный параметр `out` в сигнатуре функции, например `out <T> <name>`, где `T` — это тип данных, в который нужно сериализовать данные, а `paramName` — это имя, указанное в [выходной привязке](#output).</span><span class="sxs-lookup"><span data-stu-id="86cf8-157">In C# functions, you bind to the table output by using the named `out` parameter in your function signature, like `out <T> <name>`, where `T` is the data type that you want to serialize the data into, and `paramName` is the name you specified in the [output binding](#output).</span></span> <span data-ttu-id="86cf8-158">В функциях Node.js доступ к выходным данным таблицы можно получить, используя `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="86cf8-158">In Node.js functions, you access the table output using `context.bindings.<name>`.</span></span>

<span data-ttu-id="86cf8-159">Вы можете сериализовать объекты в функциях Node.js или C#.</span><span class="sxs-lookup"><span data-stu-id="86cf8-159">You can serialize objects in Node.js or C# functions.</span></span> <span data-ttu-id="86cf8-160">В функции C# можно выполнить привязку следующих типов:</span><span class="sxs-lookup"><span data-stu-id="86cf8-160">In C# functions, you can also bind to the following types:</span></span>

* <span data-ttu-id="86cf8-161">Любой тип, реализующий объект `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="86cf8-161">Any type that implements `ITableEntity`</span></span>
* <span data-ttu-id="86cf8-162">`ICollector<T>` (Для вывода нескольких сущностей.</span><span class="sxs-lookup"><span data-stu-id="86cf8-162">`ICollector<T>` (to output multiple entities.</span></span> <span data-ttu-id="86cf8-163">Ознакомьтесь с [примером](#outcsharp).).</span><span class="sxs-lookup"><span data-stu-id="86cf8-163">See [sample](#outcsharp).)</span></span>
* <span data-ttu-id="86cf8-164">`IAsyncCollector<T>` (асинхронная версия `ICollector<T>`).</span><span class="sxs-lookup"><span data-stu-id="86cf8-164">`IAsyncCollector<T>` (async version of `ICollector<T>`)</span></span>
* <span data-ttu-id="86cf8-165">`CloudTable` (использование пакета SDK службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="86cf8-165">`CloudTable` (using the Azure Storage SDK.</span></span> <span data-ttu-id="86cf8-166">Ознакомьтесь с [примером](#readmulti).).</span><span class="sxs-lookup"><span data-stu-id="86cf8-166">See [sample](#readmulti).)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="86cf8-167">Пример выходной привязки</span><span class="sxs-lookup"><span data-stu-id="86cf8-167">Output sample</span></span>
<span data-ttu-id="86cf8-168">В следующем примере с файлами *function.json* и *run.csx* показано, как записать несколько сущностей таблицы.</span><span class="sxs-lookup"><span data-stu-id="86cf8-168">The following *function.json* and *run.csx* example shows how to write multiple table entities.</span></span>

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

<span data-ttu-id="86cf8-169">Ознакомьтесь с примером для конкретного языка, создающим несколько сущностей таблицы.</span><span class="sxs-lookup"><span data-stu-id="86cf8-169">See the language-specific sample that creates multiple table entities.</span></span>

* [<span data-ttu-id="86cf8-170">C#</span><span class="sxs-lookup"><span data-stu-id="86cf8-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="86cf8-171">F#</span><span class="sxs-lookup"><span data-stu-id="86cf8-171">F#</span></span>](#outfsharp)
* [<span data-ttu-id="86cf8-172">Node.js</span><span class="sxs-lookup"><span data-stu-id="86cf8-172">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="86cf8-173">Пример выходной привязки для языка C#</span><span class="sxs-lookup"><span data-stu-id="86cf8-173">Output sample in C#</span></span> #
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

### <a name="output-sample-in-f"></a><span data-ttu-id="86cf8-174">Пример выходной привязки для языка F#</span><span class="sxs-lookup"><span data-stu-id="86cf8-174">Output sample in F#</span></span> #
```fsharp
[<CLIMutable>]
type Person = {
  PartitionKey: string
  RowKey: string
  Name: string
}

let Run(input: string, tableBinding: ICollector<Person>, log: TraceWriter) =
    for i = 1 to 10 do
        log.Info(sprintf "Adding Person entity %d" i)
        tableBinding.Add(
            { PartitionKey = "Test"
              RowKey = i.ToString()
              Name = "Name" + i.ToString() })
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="86cf8-175">Пример выходной привязки для Node.js</span><span class="sxs-lookup"><span data-stu-id="86cf8-175">Output sample in Node.js</span></span>
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

## <a name="sample-read-multiple-table-entities-in-c"></a><span data-ttu-id="86cf8-176">Пример. Чтение нескольких сущностей таблицы на языке C#</span><span class="sxs-lookup"><span data-stu-id="86cf8-176">Sample: Read multiple table entities in C#</span></span>  #
<span data-ttu-id="86cf8-177">В этом примере с файлом *function.json* и кодом C# считываются сущности для ключа секции (определяется в сообщении очереди).</span><span class="sxs-lookup"><span data-stu-id="86cf8-177">The following *function.json* and C# code example reads entities for a partition key that is specified in the queue message.</span></span>

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

<span data-ttu-id="86cf8-178">В коде C# добавляется ссылка на пакет SDK для службы хранилища Azure, чтобы тип сущности мог быть производным от `TableEntity`.</span><span class="sxs-lookup"><span data-stu-id="86cf8-178">The C# code adds a reference to the Azure Storage SDK so that the entity type can derive from `TableEntity`.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="86cf8-179">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="86cf8-179">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

