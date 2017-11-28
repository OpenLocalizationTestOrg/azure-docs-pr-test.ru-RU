---
title: "Привязки Cosmos DB в Функциях Azure | Документация Майкрософт"
description: "Узнайте, как использовать привязки Azure Cosmos DB в Функциях Azure."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "функции azure, функции, обработка событий, динамические вычисления, независимая архитектура"
ms.assetid: 3d8497f0-21f3-437d-ba24-5ece8c90ac85
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/18/2016
ms.author: glenga
ms.openlocfilehash: de95b0591eb95e76dbb7ba2382e9e14e1f66cda1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-cosmos-db-bindings"></a><span data-ttu-id="c277d-104">Привязки Cosmos DB в Функциях Azure</span><span class="sxs-lookup"><span data-stu-id="c277d-104">Azure Functions Cosmos DB bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="c277d-105">В этой статье объясняется, как настроить и запрограммировать привязки Azure Cosmos DB в Функциях Azure.</span><span class="sxs-lookup"><span data-stu-id="c277d-105">This article explains how to configure and code Azure Cosmos DB bindings in Azure Functions.</span></span> <span data-ttu-id="c277d-106">Функции Azure поддерживают входные и выходные привязки для Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c277d-106">Azure Functions supports input and output bindings for Cosmos DB.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="c277d-107">Дополнительные сведения о Cosmos DB см. в статьях [Знакомство с DocumentDB: база данных NoSQL JSON](../documentdb/documentdb-introduction.md) и [Руководство по NoSQL. Создание консольного приложения DocumentDB на языке C#](../documentdb/documentdb-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c277d-107">For more information on Cosmos DB, see [Introduction to Cosmos DB](../documentdb/documentdb-introduction.md) and [Build a Cosmos DB console application](../documentdb/documentdb-get-started.md).</span></span>

<a id="docdbinput"></a>

## <a name="documentdb-api-input-binding"></a><span data-ttu-id="c277d-108">Входная привязка API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="c277d-108">DocumentDB API input binding</span></span>
<span data-ttu-id="c277d-109">Входная привязка API DocumentDB получает документ Cosmos DB и передает его именованному входному параметру функции.</span><span class="sxs-lookup"><span data-stu-id="c277d-109">The DocumentDB API input binding retrieves a Cosmos DB document and passes it to the named input parameter of the function.</span></span> <span data-ttu-id="c277d-110">Идентификатор документа можно определить по триггеру, который вызывает функцию.</span><span class="sxs-lookup"><span data-stu-id="c277d-110">The document ID can be determined based on the trigger that invokes the function.</span></span> 

<span data-ttu-id="c277d-111">Входная привязка API DocumentDB имеет следующие свойства в *function.json*:</span><span class="sxs-lookup"><span data-stu-id="c277d-111">The DocumentDB API input binding has the following properties in *function.json*:</span></span>

- <span data-ttu-id="c277d-112">`name` — имя идентификатора, используемого в коде функции для документа.</span><span class="sxs-lookup"><span data-stu-id="c277d-112">`name` : Identifier name used in function code for the document</span></span>
- <span data-ttu-id="c277d-113">`type` — для этого свойства нужно задать значение "documentdb".</span><span class="sxs-lookup"><span data-stu-id="c277d-113">`type` : must be set to "documentdb"</span></span>
- <span data-ttu-id="c277d-114">`databaseName` — база данных, содержащая документ.</span><span class="sxs-lookup"><span data-stu-id="c277d-114">`databaseName` : The database containing the document</span></span>
- <span data-ttu-id="c277d-115">`collectionName` — коллекция, содержащая документ.</span><span class="sxs-lookup"><span data-stu-id="c277d-115">`collectionName` : The collection containing the document</span></span>
- <span data-ttu-id="c277d-116">`id` — идентификатор документа, который нужно получить.</span><span class="sxs-lookup"><span data-stu-id="c277d-116">`id` : The Id of the document to retrieve.</span></span> <span data-ttu-id="c277d-117">Это свойство поддерживает параметры привязки; см. раздел [Привязка к пользовательским входным свойствам в выражении привязки](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) статьи [Основные понятия триггеров и привязок в Функциях Azure](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="c277d-117">This property supports bindings parameters; see [Bind to custom input properties in a binding expression](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) in the article [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>
- <span data-ttu-id="c277d-118">`sqlQuery` — SQL-запрос к Cosmos DB, используемый для извлечения нескольких документов.</span><span class="sxs-lookup"><span data-stu-id="c277d-118">`sqlQuery` : A Cosmos DB SQL query used for retrieving multiple documents.</span></span> <span data-ttu-id="c277d-119">Запрос поддерживает привязки времени выполнения.</span><span class="sxs-lookup"><span data-stu-id="c277d-119">The query supports runtime bindings.</span></span> <span data-ttu-id="c277d-120">Например: `SELECT * FROM c where c.departmentId = {departmentId}`</span><span class="sxs-lookup"><span data-stu-id="c277d-120">For example: `SELECT * FROM c where c.departmentId = {departmentId}`</span></span>
- <span data-ttu-id="c277d-121">`connection` — имя параметра приложения, содержащего строку подключения к Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c277d-121">`connection` : The name of the app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="c277d-122">`direction` — для этого свойства нужно задать значение `"in"`.</span><span class="sxs-lookup"><span data-stu-id="c277d-122">`direction`  : must be set to `"in"`.</span></span>

<span data-ttu-id="c277d-123">Свойства `id` и `sqlQuery` невозможно указать одновременно.</span><span class="sxs-lookup"><span data-stu-id="c277d-123">The properties `id` and `sqlQuery` cannot both be specified.</span></span> <span data-ttu-id="c277d-124">Если не задано ни `id`, ни `sqlQuery`, извлекается вся коллекция.</span><span class="sxs-lookup"><span data-stu-id="c277d-124">If neither `id` nor `sqlQuery` is set, the entire collection is retrieved.</span></span>

## <a name="using-a-documentdb-api-input-binding"></a><span data-ttu-id="c277d-125">Использование входной привязки API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="c277d-125">Using a DocumentDB API input binding</span></span>

* <span data-ttu-id="c277d-126">В функциях C# и F# любые изменения, внесенные во входной документ посредством именованных входных параметров, сохраняются автоматически после успешного выхода из функции.</span><span class="sxs-lookup"><span data-stu-id="c277d-126">In C# and F# functions, when the function exits successfully, any changes made to the input document via named input parameters are automatically persisted.</span></span> 
* <span data-ttu-id="c277d-127">В функциях JavaScript изменения не обрабатываются автоматически при выходе из функции.</span><span class="sxs-lookup"><span data-stu-id="c277d-127">In JavaScript functions, updates are not made automatically upon function exit.</span></span> <span data-ttu-id="c277d-128">Для внесения изменений используйте `context.bindings.<documentName>In` и `context.bindings.<documentName>Out`.</span><span class="sxs-lookup"><span data-stu-id="c277d-128">Instead, use `context.bindings.<documentName>In` and `context.bindings.<documentName>Out` to make updates.</span></span> <span data-ttu-id="c277d-129">См. [пример JavaScript](#injavascript).</span><span class="sxs-lookup"><span data-stu-id="c277d-129">See the [JavaScript sample](#injavascript).</span></span>

<a name="inputsample"></a>

## <a name="input-sample-for-single-document"></a><span data-ttu-id="c277d-130">Пример входной привязки для отдельного документа</span><span class="sxs-lookup"><span data-stu-id="c277d-130">Input sample for single document</span></span>
<span data-ttu-id="c277d-131">Предположим, что у вас есть следующая входная привязка API DocumentDB в массиве `bindings` файла function.json:</span><span class="sxs-lookup"><span data-stu-id="c277d-131">Suppose you have the following DocumentDB API input binding in the `bindings` array of function.json:</span></span>

```json
{
  "name": "inputDocument",
  "type": "documentDB",
  "databaseName": "MyDatabase",
  "collectionName": "MyCollection",
  "id" : "{queueTrigger}",
  "connection": "MyAccount_COSMOSDB",     
  "direction": "in"
}
```

<span data-ttu-id="c277d-132">Чтобы обновить текстовое значение документа, см. пример для конкретного языка, использующий эту входную привязку.</span><span class="sxs-lookup"><span data-stu-id="c277d-132">See the language-specific sample that uses this input binding to update the document's text value.</span></span>

* [<span data-ttu-id="c277d-133">C#</span><span class="sxs-lookup"><span data-stu-id="c277d-133">C#</span></span>](#incsharp)
* [<span data-ttu-id="c277d-134">F#</span><span class="sxs-lookup"><span data-stu-id="c277d-134">F#</span></span>](#infsharp)
* [<span data-ttu-id="c277d-135">JavaScript</span><span class="sxs-lookup"><span data-stu-id="c277d-135">JavaScript</span></span>](#injavascript)

<a name="incsharp"></a>
### <a name="input-sample-in-c"></a><span data-ttu-id="c277d-136">Пример входной привязки для языка C#</span><span class="sxs-lookup"><span data-stu-id="c277d-136">Input sample in C#</span></span> #

```cs
// Change input document contents using DocumentDB API input binding 
public static void Run(string myQueueItem, dynamic inputDocument)
{   
  inputDocument.text = "This has changed.";
}
```
<a name="infsharp"></a>

### <a name="input-sample-in-f"></a><span data-ttu-id="c277d-137">Пример входной привязки для языка F#</span><span class="sxs-lookup"><span data-stu-id="c277d-137">Input sample in F#</span></span> #

```fsharp
(* Change input document contents using DocumentDB API input binding *)
open FSharp.Interop.Dynamic
let Run(myQueueItem: string, inputDocument: obj) =
  inputDocument?text <- "This has changed."
```

<span data-ttu-id="c277d-138">В этом примере нужен файл `project.json`, указывающий зависимости NuGet `FSharp.Interop.Dynamic` и `Dynamitey`:</span><span class="sxs-lookup"><span data-stu-id="c277d-138">This sample requires a `project.json` file that specifies the `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

```json
{
  "frameworks": {
    "net46": {
      "dependencies": {
        "Dynamitey": "1.0.2",
        "FSharp.Interop.Dynamic": "3.0.0"
      }
    }
  }
}
```

<span data-ttu-id="c277d-139">Чтобы добавить файл `project.json`, см. раздел [об управлении пакетом F#](functions-reference-fsharp.md#package).</span><span class="sxs-lookup"><span data-stu-id="c277d-139">To add a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="injavascript"></a>

### <a name="input-sample-in-javascript"></a><span data-ttu-id="c277d-140">Пример входной привязки для JavaScript</span><span class="sxs-lookup"><span data-stu-id="c277d-140">Input sample in JavaScript</span></span>

```javascript
// Change input document contents using DocumentDB API input binding, using context.bindings.inputDocumentOut
module.exports = function (context) {   
  context.bindings.inputDocumentOut = context.bindings.inputDocumentIn;
  context.bindings.inputDocumentOut.text = "This was updated!";
  context.done();
};
```

## <a name="input-sample-with-multiple-documents"></a><span data-ttu-id="c277d-141">Пример входной привязки с несколькими документами</span><span class="sxs-lookup"><span data-stu-id="c277d-141">Input sample with multiple documents</span></span>

<span data-ttu-id="c277d-142">Предположим, что нужно извлечь несколько документов, указанных SQL-запросом, используя триггер очереди для настройки параметров запроса.</span><span class="sxs-lookup"><span data-stu-id="c277d-142">Suppose that you wish to retrieve multiple documents specified by a SQL query, using a queue trigger to customize the query parameters.</span></span> 

<span data-ttu-id="c277d-143">В этом примере триггер очереди предоставляет параметр `departmentId`. Сообщение очереди `{ "departmentId" : "Finance" }` возвращает все записи для финансового отдела.</span><span class="sxs-lookup"><span data-stu-id="c277d-143">In this example, the queue trigger provides a parameter `departmentId`.A queue message of `{ "departmentId" : "Finance" }` would return all records for the finance department.</span></span> <span data-ttu-id="c277d-144">Используйте в *function.json* следующий код:</span><span class="sxs-lookup"><span data-stu-id="c277d-144">Use the following in *function.json*:</span></span>

```
{
    "name": "documents",
    "type": "documentdb",
    "direction": "in",
    "databaseName": "MyDb",
    "collectionName": "MyCollection",
    "sqlQuery": "SELECT * from c where c.departmentId = {departmentId}"
    "connection": "CosmosDBConnection"
}
```

### <a name="input-sample-with-multiple-documents-in-c"></a><span data-ttu-id="c277d-145">Пример входной привязки с несколькими документами для языка C#</span><span class="sxs-lookup"><span data-stu-id="c277d-145">Input sample with multiple documents in C#</span></span>

```csharp
public static void Run(QueuePayload myQueueItem, IEnumerable<dynamic> documents)
{   
    foreach (var doc in documents)
    {
        // operate on each document
    }    
}

public class QueuePayload
{
    public string departmentId { get; set; }
}
```

### <a name="input-sample-with-multiple-documents-in-javascript"></a><span data-ttu-id="c277d-146">Пример входной привязки с несколькими документами для JavaScript</span><span class="sxs-lookup"><span data-stu-id="c277d-146">Input sample with multiple documents in JavaScript</span></span>

```javascript
module.exports = function (context, input) {    
    var documents = context.bindings.documents;
    for (var i = 0; i < documents.length; i++) {
        var document = documents[i];
        // operate on each document
    }       
    context.done();
};
```

## <span data-ttu-id="c277d-147"><a id="docdboutput"></a>Выходная привязка API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="c277d-147"><a id="docdboutput"></a>DocumentDB API output binding</span></span>
<span data-ttu-id="c277d-148">Выходная привязка API DocumentDB позволяет записать новый документ в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c277d-148">The DocumentDB API output binding lets you write a new document to an Azure Cosmos DB database.</span></span> <span data-ttu-id="c277d-149">Он содержит следующие свойства в *function.json*:</span><span class="sxs-lookup"><span data-stu-id="c277d-149">It has the following properties in *function.json*:</span></span>

- <span data-ttu-id="c277d-150">`name` — идентификатор, используемый в коде функции для нового документа.</span><span class="sxs-lookup"><span data-stu-id="c277d-150">`name` : Identifier used in function code for the new document</span></span>
- <span data-ttu-id="c277d-151">`type` — для этого свойства нужно задать значение `"documentdb"`.</span><span class="sxs-lookup"><span data-stu-id="c277d-151">`type` : must be set to `"documentdb"`</span></span>
- <span data-ttu-id="c277d-152">`databaseName` — база данных, содержащая коллекцию, в которой будет создан документ.</span><span class="sxs-lookup"><span data-stu-id="c277d-152">`databaseName` : The database containing the collection where the new document will be created.</span></span>
- <span data-ttu-id="c277d-153">`collectionName` — коллекция, в которой будет создан документ.</span><span class="sxs-lookup"><span data-stu-id="c277d-153">`collectionName` : The collection where the new document will be created.</span></span>
- <span data-ttu-id="c277d-154">`createIfNotExists` — логическое значение, указывающее, будет ли создана коллекция при ее отсутствии.</span><span class="sxs-lookup"><span data-stu-id="c277d-154">`createIfNotExists` : A boolean value to indicate whether the collection will be created if it does not exist.</span></span> <span data-ttu-id="c277d-155">Значение по умолчанию — *false*.</span><span class="sxs-lookup"><span data-stu-id="c277d-155">The default is *false*.</span></span> <span data-ttu-id="c277d-156">Это вызвано тем, что коллекции создаются с использованием зарезервированной пропускной способности, с которой связаны ценовые требования.</span><span class="sxs-lookup"><span data-stu-id="c277d-156">The reason for this is new collections are created with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="c277d-157">Дополнительные сведения см. на [странице цен](https://azure.microsoft.com/pricing/details/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="c277d-157">For more details, please visit the [pricing page](https://azure.microsoft.com/pricing/details/documentdb/).</span></span>
- <span data-ttu-id="c277d-158">`connection` — имя параметра приложения, содержащего строку подключения к Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c277d-158">`connection` : The name of the app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="c277d-159">`direction` — для этого свойства нужно задать значение `"out"`.</span><span class="sxs-lookup"><span data-stu-id="c277d-159">`direction` : must be set to `"out"`</span></span>

## <a name="using-a-documentdb-api-output-binding"></a><span data-ttu-id="c277d-160">Использование выходной привязки API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="c277d-160">Using a DocumentDB API output binding</span></span>
<span data-ttu-id="c277d-161">В этом разделе показано, как использовать выходную привязку API DocumentDB в коде функции.</span><span class="sxs-lookup"><span data-stu-id="c277d-161">This section shows you how to use your DocumentDB API output binding in your function code.</span></span>

<span data-ttu-id="c277d-162">При записи в выходном параметре функции в базе данных по умолчанию создается документ, для которого автоматически создается GUID в качестве идентификатора документа.</span><span class="sxs-lookup"><span data-stu-id="c277d-162">When you write to the output parameter in your function, by default a new document is generated in your database, with an automatically generated GUID as the document ID.</span></span> <span data-ttu-id="c277d-163">Идентификатор выходного документа можно определить, указав свойство JSON `id` в выходном параметре.</span><span class="sxs-lookup"><span data-stu-id="c277d-163">You can specify the document ID of output document by specifying the `id` JSON property in the output parameter.</span></span> 

>[!Note]  
><span data-ttu-id="c277d-164">Если указать идентификатор существующего документа, он перезаписывается новым выходным документом.</span><span class="sxs-lookup"><span data-stu-id="c277d-164">When you specify the ID of an existing document, it gets overwritten by the new output document.</span></span> 

<span data-ttu-id="c277d-165">Для вывода в несколько документов можно также выполнить привязку к `ICollector<T>` или `IAsyncCollector<T>`, где `T` — любой из поддерживаемых типов.</span><span class="sxs-lookup"><span data-stu-id="c277d-165">To output multiple documents, you can also bind to `ICollector<T>` or `IAsyncCollector<T>` where `T` is one of the supported types.</span></span>

<a name="outputsample"></a>

## <a name="documentdb-api-output-binding-sample"></a><span data-ttu-id="c277d-166">Пример выходной привязки API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="c277d-166">DocumentDB API output binding sample</span></span>
<span data-ttu-id="c277d-167">Предположим, что у вас есть следующая выходная привязка API DocumentDB в массиве `bindings` файла function.json:</span><span class="sxs-lookup"><span data-stu-id="c277d-167">Suppose you have the following DocumentDB API output binding in the `bindings` array of function.json:</span></span>

```json
{
  "name": "employeeDocument",
  "type": "documentDB",
  "databaseName": "MyDatabase",
  "collectionName": "MyCollection",
  "createIfNotExists": true,
  "connection": "MyAccount_COSMOSDB",     
  "direction": "out"
}
```

<span data-ttu-id="c277d-168">Кроме того, у вас есть входная привязка очереди для очереди, которая получает JSON в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="c277d-168">And you have a queue input binding for a queue that receives JSON in the following format:</span></span>

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="c277d-169">При этом вам нужно создать документы Cosmos DB в следующем формате для каждой записи:</span><span class="sxs-lookup"><span data-stu-id="c277d-169">And you want to create Cosmos DB documents in the following format for each record:</span></span>

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="c277d-170">Чтобы добавить документы в базу данных, см. пример для конкретного языка, использующий эту выходную привязку.</span><span class="sxs-lookup"><span data-stu-id="c277d-170">See the language-specific sample that uses this output binding to add documents to your database.</span></span>

* [<span data-ttu-id="c277d-171">C#</span><span class="sxs-lookup"><span data-stu-id="c277d-171">C#</span></span>](#outcsharp)
* [<span data-ttu-id="c277d-172">F#</span><span class="sxs-lookup"><span data-stu-id="c277d-172">F#</span></span>](#outfsharp)
* [<span data-ttu-id="c277d-173">JavaScript</span><span class="sxs-lookup"><span data-stu-id="c277d-173">JavaScript</span></span>](#outjavascript)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="c277d-174">Пример выходной привязки для языка C#</span><span class="sxs-lookup"><span data-stu-id="c277d-174">Output sample in C#</span></span> #

```cs
#r "Newtonsoft.Json"

using System;
using Newtonsoft.Json;
using Newtonsoft.Json.Linq;

public static void Run(string myQueueItem, out object employeeDocument, TraceWriter log)
{
  log.Info($"C# Queue trigger function processed: {myQueueItem}");

  dynamic employee = JObject.Parse(myQueueItem);

  employeeDocument = new {
    id = employee.name + "-" + employee.employeeId,
    name = employee.name,
    employeeId = employee.employeeId,
    address = employee.address
  };
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a><span data-ttu-id="c277d-175">Пример выходной привязки для языка F#</span><span class="sxs-lookup"><span data-stu-id="c277d-175">Output sample in F#</span></span> #

```fsharp
open FSharp.Interop.Dynamic
open Newtonsoft.Json

type Employee = {
  id: string
  name: string
  employeeId: string
  address: string
}

let Run(myQueueItem: string, employeeDocument: byref<obj>, log: TraceWriter) =
  log.Info(sprintf "F# Queue trigger function processed: %s" myQueueItem)
  let employee = JObject.Parse(myQueueItem)
  employeeDocument <-
    { id = sprintf "%s-%s" employee?name employee?employeeId
      name = employee?name
      employeeId = employee?employeeId
      address = employee?address }
```

<span data-ttu-id="c277d-176">В этом примере нужен файл `project.json`, указывающий зависимости NuGet `FSharp.Interop.Dynamic` и `Dynamitey`:</span><span class="sxs-lookup"><span data-stu-id="c277d-176">This sample requires a `project.json` file that specifies the `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

```json
{
  "frameworks": {
    "net46": {
      "dependencies": {
        "Dynamitey": "1.0.2",
        "FSharp.Interop.Dynamic": "3.0.0"
      }
    }
  }
}
```

<span data-ttu-id="c277d-177">Чтобы добавить файл `project.json`, см. раздел [об управлении пакетом F#](functions-reference-fsharp.md#package).</span><span class="sxs-lookup"><span data-stu-id="c277d-177">To add a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="outjavascript"></a>

### <a name="output-sample-in-javascript"></a><span data-ttu-id="c277d-178">Пример выходной привязки для JavaScript</span><span class="sxs-lookup"><span data-stu-id="c277d-178">Output sample in JavaScript</span></span>

```javascript
module.exports = function (context) {

  context.bindings.employeeDocument = JSON.stringify({ 
    id: context.bindings.myQueueItem.name + "-" + context.bindings.myQueueItem.employeeId,
    name: context.bindings.myQueueItem.name,
    employeeId: context.bindings.myQueueItem.employeeId,
    address: context.bindings.myQueueItem.address
  });

  context.done();
};
```
