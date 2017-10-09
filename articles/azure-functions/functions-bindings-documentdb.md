---
title: "привязки функции Cosmos DB aaaAzure | Документы Microsoft"
description: "Понять, как привязки toouse Azure Cosmos DB в функциях Azure."
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
ms.openlocfilehash: 76b89e8296db1dd28dff9528903b1f6a28f55232
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-cosmos-db-bindings"></a><span data-ttu-id="b0399-104">Привязки Cosmos DB в Функциях Azure</span><span class="sxs-lookup"><span data-stu-id="b0399-104">Azure Functions Cosmos DB bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="b0399-105">В этой статье объясняется, как привязки Azure Cosmos DB tooconfigure и код в функциях Azure.</span><span class="sxs-lookup"><span data-stu-id="b0399-105">This article explains how tooconfigure and code Azure Cosmos DB bindings in Azure Functions.</span></span> <span data-ttu-id="b0399-106">Функции Azure поддерживают входные и выходные привязки для Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b0399-106">Azure Functions supports input and output bindings for Cosmos DB.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="b0399-107">Дополнительные сведения о Cosmos DB см. в разделе [tooCosmos введение DB](../documentdb/documentdb-introduction.md) и [построение консольного приложения Cosmos DB](../documentdb/documentdb-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b0399-107">For more information on Cosmos DB, see [Introduction tooCosmos DB](../documentdb/documentdb-introduction.md) and [Build a Cosmos DB console application](../documentdb/documentdb-get-started.md).</span></span>

<a id="docdbinput"></a>

## <a name="documentdb-api-input-binding"></a><span data-ttu-id="b0399-108">Входная привязка API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="b0399-108">DocumentDB API input binding</span></span>
<span data-ttu-id="b0399-109">Hello входной привязки DocumentDB API извлекает Cosmos DB документ и передает его toohello с именем входного параметра функции hello.</span><span class="sxs-lookup"><span data-stu-id="b0399-109">hello DocumentDB API input binding retrieves a Cosmos DB document and passes it toohello named input parameter of hello function.</span></span> <span data-ttu-id="b0399-110">можно определить идентификатор документа Hello на основании hello триггер, который вызывает функции hello.</span><span class="sxs-lookup"><span data-stu-id="b0399-110">hello document ID can be determined based on hello trigger that invokes hello function.</span></span> 

<span data-ttu-id="b0399-111">Hello DocumentDB API входной привязки имеет следующие свойства в hello *function.json*:</span><span class="sxs-lookup"><span data-stu-id="b0399-111">hello DocumentDB API input binding has hello following properties in *function.json*:</span></span>

- <span data-ttu-id="b0399-112">`name`: Идентификатор имя, используемое в код функции для hello документа</span><span class="sxs-lookup"><span data-stu-id="b0399-112">`name` : Identifier name used in function code for hello document</span></span>
- <span data-ttu-id="b0399-113">`type`: необходимо задать слишком «documentdb»</span><span class="sxs-lookup"><span data-stu-id="b0399-113">`type` : must be set too"documentdb"</span></span>
- <span data-ttu-id="b0399-114">`databaseName`: hello базы данных, содержащей документ hello</span><span class="sxs-lookup"><span data-stu-id="b0399-114">`databaseName` : hello database containing hello document</span></span>
- <span data-ttu-id="b0399-115">`collectionName`: hello коллекцию, содержащую hello документа</span><span class="sxs-lookup"><span data-stu-id="b0399-115">`collectionName` : hello collection containing hello document</span></span>
- <span data-ttu-id="b0399-116">`id`: hello идентификатор hello tooretrieve документа.</span><span class="sxs-lookup"><span data-stu-id="b0399-116">`id` : hello Id of hello document tooretrieve.</span></span> <span data-ttu-id="b0399-117">Это свойство поддерживает параметры привязки; в разделе [привязки входных свойств toocustom в выражение привязки](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) в статье hello [триггеры функций Azure и основные понятия привязки](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="b0399-117">This property supports bindings parameters; see [Bind toocustom input properties in a binding expression](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) in hello article [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>
- <span data-ttu-id="b0399-118">`sqlQuery` — SQL-запрос к Cosmos DB, используемый для извлечения нескольких документов.</span><span class="sxs-lookup"><span data-stu-id="b0399-118">`sqlQuery` : A Cosmos DB SQL query used for retrieving multiple documents.</span></span> <span data-ttu-id="b0399-119">запрос Hello поддерживает привязки исполняющей среды.</span><span class="sxs-lookup"><span data-stu-id="b0399-119">hello query supports runtime bindings.</span></span> <span data-ttu-id="b0399-120">Например: `SELECT * FROM c where c.departmentId = {departmentId}`</span><span class="sxs-lookup"><span data-stu-id="b0399-120">For example: `SELECT * FROM c where c.departmentId = {departmentId}`</span></span>
- <span data-ttu-id="b0399-121">`connection`: hello имя параметра приложения hello, содержащий строки подключения Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b0399-121">`connection` : hello name of hello app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="b0399-122">`direction`: необходимо задать слишком`"in"`.</span><span class="sxs-lookup"><span data-stu-id="b0399-122">`direction`  : must be set too`"in"`.</span></span>

<span data-ttu-id="b0399-123">Здравствуйте, свойства `id` и `sqlQuery` невозможно указать одновременно.</span><span class="sxs-lookup"><span data-stu-id="b0399-123">hello properties `id` and `sqlQuery` cannot both be specified.</span></span> <span data-ttu-id="b0399-124">Если ни одна из `id` , ни `sqlQuery` имеет значение, hello всего извлекается коллекция.</span><span class="sxs-lookup"><span data-stu-id="b0399-124">If neither `id` nor `sqlQuery` is set, hello entire collection is retrieved.</span></span>

## <a name="using-a-documentdb-api-input-binding"></a><span data-ttu-id="b0399-125">Использование входной привязки API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="b0399-125">Using a DocumentDB API input binding</span></span>

* <span data-ttu-id="b0399-126">В C# и F # функции при выходе из функции hello, успешно, все изменения, внесенные toohello входного документа через именованный входных параметров, автоматически сохраняется.</span><span class="sxs-lookup"><span data-stu-id="b0399-126">In C# and F# functions, when hello function exits successfully, any changes made toohello input document via named input parameters are automatically persisted.</span></span> 
* <span data-ttu-id="b0399-127">В функциях JavaScript изменения не обрабатываются автоматически при выходе из функции.</span><span class="sxs-lookup"><span data-stu-id="b0399-127">In JavaScript functions, updates are not made automatically upon function exit.</span></span> <span data-ttu-id="b0399-128">Вместо этого используйте `context.bindings.<documentName>In` и `context.bindings.<documentName>Out` toomake обновлений.</span><span class="sxs-lookup"><span data-stu-id="b0399-128">Instead, use `context.bindings.<documentName>In` and `context.bindings.<documentName>Out` toomake updates.</span></span> <span data-ttu-id="b0399-129">В разделе hello [пример JavaScript](#injavascript).</span><span class="sxs-lookup"><span data-stu-id="b0399-129">See hello [JavaScript sample](#injavascript).</span></span>

<a name="inputsample"></a>

## <a name="input-sample-for-single-document"></a><span data-ttu-id="b0399-130">Пример входной привязки для отдельного документа</span><span class="sxs-lookup"><span data-stu-id="b0399-130">Input sample for single document</span></span>
<span data-ttu-id="b0399-131">Предположим, что имеется следующее hello DocumentDB API входной привязки в hello `bindings` массив function.json:</span><span class="sxs-lookup"><span data-stu-id="b0399-131">Suppose you have hello following DocumentDB API input binding in hello `bindings` array of function.json:</span></span>

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

<span data-ttu-id="b0399-132">См. пример hello зависящие от языка, который использует этот входной привязки tooupdate hello документа текстовое значение.</span><span class="sxs-lookup"><span data-stu-id="b0399-132">See hello language-specific sample that uses this input binding tooupdate hello document's text value.</span></span>

* [<span data-ttu-id="b0399-133">C#</span><span class="sxs-lookup"><span data-stu-id="b0399-133">C#</span></span>](#incsharp)
* [<span data-ttu-id="b0399-134">F#</span><span class="sxs-lookup"><span data-stu-id="b0399-134">F#</span></span>](#infsharp)
* [<span data-ttu-id="b0399-135">JavaScript</span><span class="sxs-lookup"><span data-stu-id="b0399-135">JavaScript</span></span>](#injavascript)

<a name="incsharp"></a>
### <a name="input-sample-in-c"></a><span data-ttu-id="b0399-136">Пример входной привязки для языка C#</span><span class="sxs-lookup"><span data-stu-id="b0399-136">Input sample in C#</span></span> #

```cs
// Change input document contents using DocumentDB API input binding 
public static void Run(string myQueueItem, dynamic inputDocument)
{   
  inputDocument.text = "This has changed.";
}
```
<a name="infsharp"></a>

### <a name="input-sample-in-f"></a><span data-ttu-id="b0399-137">Пример входной привязки для языка F#</span><span class="sxs-lookup"><span data-stu-id="b0399-137">Input sample in F#</span></span> #

```fsharp
(* Change input document contents using DocumentDB API input binding *)
open FSharp.Interop.Dynamic
let Run(myQueueItem: string, inputDocument: obj) =
  inputDocument?text <- "This has changed."
```

<span data-ttu-id="b0399-138">Для этого образца необходимо `project.json` файл, задающий hello `FSharp.Interop.Dynamic` и `Dynamitey` зависимостей NuGet:</span><span class="sxs-lookup"><span data-stu-id="b0399-138">This sample requires a `project.json` file that specifies hello `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

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

<span data-ttu-id="b0399-139">tooadd `project.json` файла см. в разделе [пакета управления F #](functions-reference-fsharp.md#package).</span><span class="sxs-lookup"><span data-stu-id="b0399-139">tooadd a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="injavascript"></a>

### <a name="input-sample-in-javascript"></a><span data-ttu-id="b0399-140">Пример входной привязки для JavaScript</span><span class="sxs-lookup"><span data-stu-id="b0399-140">Input sample in JavaScript</span></span>

```javascript
// Change input document contents using DocumentDB API input binding, using context.bindings.inputDocumentOut
module.exports = function (context) {   
  context.bindings.inputDocumentOut = context.bindings.inputDocumentIn;
  context.bindings.inputDocumentOut.text = "This was updated!";
  context.done();
};
```

## <a name="input-sample-with-multiple-documents"></a><span data-ttu-id="b0399-141">Пример входной привязки с несколькими документами</span><span class="sxs-lookup"><span data-stu-id="b0399-141">Input sample with multiple documents</span></span>

<span data-ttu-id="b0399-142">Предположим, что вы хотите tooretrieve несколько документов, указанный в запросе SQL с помощью параметров очереди триггера toocustomize hello запроса.</span><span class="sxs-lookup"><span data-stu-id="b0399-142">Suppose that you wish tooretrieve multiple documents specified by a SQL query, using a queue trigger toocustomize hello query parameters.</span></span> 

<span data-ttu-id="b0399-143">В этом примере hello очереди триггера предоставляет параметр `departmentId`. Сообщение из очереди `{ "departmentId" : "Finance" }` возвратит все записи для hello финансового отдела.</span><span class="sxs-lookup"><span data-stu-id="b0399-143">In this example, hello queue trigger provides a parameter `departmentId`.A queue message of `{ "departmentId" : "Finance" }` would return all records for hello finance department.</span></span> <span data-ttu-id="b0399-144">Используйте следующие hello в *function.json*:</span><span class="sxs-lookup"><span data-stu-id="b0399-144">Use hello following in *function.json*:</span></span>

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

### <a name="input-sample-with-multiple-documents-in-c"></a><span data-ttu-id="b0399-145">Пример входной привязки с несколькими документами для языка C#</span><span class="sxs-lookup"><span data-stu-id="b0399-145">Input sample with multiple documents in C#</span></span>

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

### <a name="input-sample-with-multiple-documents-in-javascript"></a><span data-ttu-id="b0399-146">Пример входной привязки с несколькими документами для JavaScript</span><span class="sxs-lookup"><span data-stu-id="b0399-146">Input sample with multiple documents in JavaScript</span></span>

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

## <span data-ttu-id="b0399-147"><a id="docdboutput"></a>Выходная привязка API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="b0399-147"><a id="docdboutput"></a>DocumentDB API output binding</span></span>
<span data-ttu-id="b0399-148">привязка позволяет вам создавать новую базу данных Azure Cosmos DB документа tooan вывода Hello DocumentDB API.</span><span class="sxs-lookup"><span data-stu-id="b0399-148">hello DocumentDB API output binding lets you write a new document tooan Azure Cosmos DB database.</span></span> <span data-ttu-id="b0399-149">Он имеет следующие свойства в hello *function.json*:</span><span class="sxs-lookup"><span data-stu-id="b0399-149">It has hello following properties in *function.json*:</span></span>

- <span data-ttu-id="b0399-150">`name`: Идентификатор, используемый в коде функция для нового документа hello</span><span class="sxs-lookup"><span data-stu-id="b0399-150">`name` : Identifier used in function code for hello new document</span></span>
- <span data-ttu-id="b0399-151">`type`: необходимо задать слишком`"documentdb"`</span><span class="sxs-lookup"><span data-stu-id="b0399-151">`type` : must be set too`"documentdb"`</span></span>
- <span data-ttu-id="b0399-152">`databaseName`: hello базы данных, содержащей коллекцию hello, где будет создан новый документ hello.</span><span class="sxs-lookup"><span data-stu-id="b0399-152">`databaseName` : hello database containing hello collection where hello new document will be created.</span></span>
- <span data-ttu-id="b0399-153">`collectionName`: hello коллекции, где будет создан новый документ hello.</span><span class="sxs-lookup"><span data-stu-id="b0399-153">`collectionName` : hello collection where hello new document will be created.</span></span>
- <span data-ttu-id="b0399-154">`createIfNotExists`: Логическое значение tooindicate ли будет создана коллекция hello, если он не существует.</span><span class="sxs-lookup"><span data-stu-id="b0399-154">`createIfNotExists` : A boolean value tooindicate whether hello collection will be created if it does not exist.</span></span> <span data-ttu-id="b0399-155">по умолчанию Hello — *false*.</span><span class="sxs-lookup"><span data-stu-id="b0399-155">hello default is *false*.</span></span> <span data-ttu-id="b0399-156">Здравствуйте, поэтому для этой новой наборы создаются с зарезервированной пропускной способностью, имеющая цены последствия.</span><span class="sxs-lookup"><span data-stu-id="b0399-156">hello reason for this is new collections are created with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="b0399-157">Для получения дополнительных сведений посетите hello [странице цен](https://azure.microsoft.com/pricing/details/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="b0399-157">For more details, please visit hello [pricing page](https://azure.microsoft.com/pricing/details/documentdb/).</span></span>
- <span data-ttu-id="b0399-158">`connection`: hello имя параметра приложения hello, содержащий строки подключения Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b0399-158">`connection` : hello name of hello app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="b0399-159">`direction`: необходимо задать слишком`"out"`</span><span class="sxs-lookup"><span data-stu-id="b0399-159">`direction` : must be set too`"out"`</span></span>

## <a name="using-a-documentdb-api-output-binding"></a><span data-ttu-id="b0399-160">Использование выходной привязки API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="b0399-160">Using a DocumentDB API output binding</span></span>
<span data-ttu-id="b0399-161">В этом разделе показано, как toouse вывода привязки в коде функция DocumentDB API.</span><span class="sxs-lookup"><span data-stu-id="b0399-161">This section shows you how toouse your DocumentDB API output binding in your function code.</span></span>

<span data-ttu-id="b0399-162">При написании toohello выходного параметра в функции, по умолчанию новый документ создается в базе данных, с автоматически созданным GUID, как hello документов идентификатор.</span><span class="sxs-lookup"><span data-stu-id="b0399-162">When you write toohello output parameter in your function, by default a new document is generated in your database, with an automatically generated GUID as hello document ID.</span></span> <span data-ttu-id="b0399-163">Можно указать идентификатор hello документ выходной документ, указав hello `id` свойства JSON в hello выходной параметр.</span><span class="sxs-lookup"><span data-stu-id="b0399-163">You can specify hello document ID of output document by specifying hello `id` JSON property in hello output parameter.</span></span> 

>[!Note]  
><span data-ttu-id="b0399-164">При указании ID hello существующего документа заменяется hello новый выходной документ.</span><span class="sxs-lookup"><span data-stu-id="b0399-164">When you specify hello ID of an existing document, it gets overwritten by hello new output document.</span></span> 

<span data-ttu-id="b0399-165">toooutput несколько документов, можно также привязать слишком`ICollector<T>` или `IAsyncCollector<T>` где `T` является одним из типов hello поддерживается.</span><span class="sxs-lookup"><span data-stu-id="b0399-165">toooutput multiple documents, you can also bind too`ICollector<T>` or `IAsyncCollector<T>` where `T` is one of hello supported types.</span></span>

<a name="outputsample"></a>

## <a name="documentdb-api-output-binding-sample"></a><span data-ttu-id="b0399-166">Пример выходной привязки API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="b0399-166">DocumentDB API output binding sample</span></span>
<span data-ttu-id="b0399-167">Предположим, что имеется следующее hello DocumentDB API вывода привязки в hello `bindings` массив function.json:</span><span class="sxs-lookup"><span data-stu-id="b0399-167">Suppose you have hello following DocumentDB API output binding in hello `bindings` array of function.json:</span></span>

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

<span data-ttu-id="b0399-168">И у вас есть привязка входной очереди для очереди, получающего hello следующая формата JSON:</span><span class="sxs-lookup"><span data-stu-id="b0399-168">And you have a queue input binding for a queue that receives JSON in hello following format:</span></span>

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="b0399-169">И вы хотите toocreate Cosmos DB документы в кодировке для каждой записи hello:</span><span class="sxs-lookup"><span data-stu-id="b0399-169">And you want toocreate Cosmos DB documents in hello following format for each record:</span></span>

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="b0399-170">См. пример hello зависящие от языка, который использует этот выходной привязки tooadd документы tooyour базы данных.</span><span class="sxs-lookup"><span data-stu-id="b0399-170">See hello language-specific sample that uses this output binding tooadd documents tooyour database.</span></span>

* [<span data-ttu-id="b0399-171">C#</span><span class="sxs-lookup"><span data-stu-id="b0399-171">C#</span></span>](#outcsharp)
* [<span data-ttu-id="b0399-172">F#</span><span class="sxs-lookup"><span data-stu-id="b0399-172">F#</span></span>](#outfsharp)
* [<span data-ttu-id="b0399-173">JavaScript</span><span class="sxs-lookup"><span data-stu-id="b0399-173">JavaScript</span></span>](#outjavascript)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="b0399-174">Пример выходной привязки для языка C#</span><span class="sxs-lookup"><span data-stu-id="b0399-174">Output sample in C#</span></span> #

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

### <a name="output-sample-in-f"></a><span data-ttu-id="b0399-175">Пример выходной привязки для языка F#</span><span class="sxs-lookup"><span data-stu-id="b0399-175">Output sample in F#</span></span> #

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

<span data-ttu-id="b0399-176">Для этого образца необходимо `project.json` файл, задающий hello `FSharp.Interop.Dynamic` и `Dynamitey` зависимостей NuGet:</span><span class="sxs-lookup"><span data-stu-id="b0399-176">This sample requires a `project.json` file that specifies hello `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

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

<span data-ttu-id="b0399-177">tooadd `project.json` файла см. в разделе [пакета управления F #](functions-reference-fsharp.md#package).</span><span class="sxs-lookup"><span data-stu-id="b0399-177">tooadd a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="outjavascript"></a>

### <a name="output-sample-in-javascript"></a><span data-ttu-id="b0399-178">Пример выходной привязки для JavaScript</span><span class="sxs-lookup"><span data-stu-id="b0399-178">Output sample in JavaScript</span></span>

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
