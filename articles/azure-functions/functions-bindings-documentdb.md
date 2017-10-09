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
# <a name="azure-functions-cosmos-db-bindings"></a>Привязки Cosmos DB в Функциях Azure
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

В этой статье объясняется, как привязки Azure Cosmos DB tooconfigure и код в функциях Azure. Функции Azure поддерживают входные и выходные привязки для Cosmos DB.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Дополнительные сведения о Cosmos DB см. в разделе [tooCosmos введение DB](../documentdb/documentdb-introduction.md) и [построение консольного приложения Cosmos DB](../documentdb/documentdb-get-started.md).

<a id="docdbinput"></a>

## <a name="documentdb-api-input-binding"></a>Входная привязка API DocumentDB
Hello входной привязки DocumentDB API извлекает Cosmos DB документ и передает его toohello с именем входного параметра функции hello. можно определить идентификатор документа Hello на основании hello триггер, который вызывает функции hello. 

Hello DocumentDB API входной привязки имеет следующие свойства в hello *function.json*:

- `name`: Идентификатор имя, используемое в код функции для hello документа
- `type`: необходимо задать слишком «documentdb»
- `databaseName`: hello базы данных, содержащей документ hello
- `collectionName`: hello коллекцию, содержащую hello документа
- `id`: hello идентификатор hello tooretrieve документа. Это свойство поддерживает параметры привязки; в разделе [привязки входных свойств toocustom в выражение привязки](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) в статье hello [триггеры функций Azure и основные понятия привязки](functions-triggers-bindings.md).
- `sqlQuery` — SQL-запрос к Cosmos DB, используемый для извлечения нескольких документов. запрос Hello поддерживает привязки исполняющей среды. Например: `SELECT * FROM c where c.departmentId = {departmentId}`
- `connection`: hello имя параметра приложения hello, содержащий строки подключения Cosmos DB
- `direction`: необходимо задать слишком`"in"`.

Здравствуйте, свойства `id` и `sqlQuery` невозможно указать одновременно. Если ни одна из `id` , ни `sqlQuery` имеет значение, hello всего извлекается коллекция.

## <a name="using-a-documentdb-api-input-binding"></a>Использование входной привязки API DocumentDB

* В C# и F # функции при выходе из функции hello, успешно, все изменения, внесенные toohello входного документа через именованный входных параметров, автоматически сохраняется. 
* В функциях JavaScript изменения не обрабатываются автоматически при выходе из функции. Вместо этого используйте `context.bindings.<documentName>In` и `context.bindings.<documentName>Out` toomake обновлений. В разделе hello [пример JavaScript](#injavascript).

<a name="inputsample"></a>

## <a name="input-sample-for-single-document"></a>Пример входной привязки для отдельного документа
Предположим, что имеется следующее hello DocumentDB API входной привязки в hello `bindings` массив function.json:

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

См. пример hello зависящие от языка, который использует этот входной привязки tooupdate hello документа текстовое значение.

* [C#](#incsharp)
* [F#](#infsharp)
* [JavaScript](#injavascript)

<a name="incsharp"></a>
### <a name="input-sample-in-c"></a>Пример входной привязки для языка C# #

```cs
// Change input document contents using DocumentDB API input binding 
public static void Run(string myQueueItem, dynamic inputDocument)
{   
  inputDocument.text = "This has changed.";
}
```
<a name="infsharp"></a>

### <a name="input-sample-in-f"></a>Пример входной привязки для языка F# #

```fsharp
(* Change input document contents using DocumentDB API input binding *)
open FSharp.Interop.Dynamic
let Run(myQueueItem: string, inputDocument: obj) =
  inputDocument?text <- "This has changed."
```

Для этого образца необходимо `project.json` файл, задающий hello `FSharp.Interop.Dynamic` и `Dynamitey` зависимостей NuGet:

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

tooadd `project.json` файла см. в разделе [пакета управления F #](functions-reference-fsharp.md#package).

<a name="injavascript"></a>

### <a name="input-sample-in-javascript"></a>Пример входной привязки для JavaScript

```javascript
// Change input document contents using DocumentDB API input binding, using context.bindings.inputDocumentOut
module.exports = function (context) {   
  context.bindings.inputDocumentOut = context.bindings.inputDocumentIn;
  context.bindings.inputDocumentOut.text = "This was updated!";
  context.done();
};
```

## <a name="input-sample-with-multiple-documents"></a>Пример входной привязки с несколькими документами

Предположим, что вы хотите tooretrieve несколько документов, указанный в запросе SQL с помощью параметров очереди триггера toocustomize hello запроса. 

В этом примере hello очереди триггера предоставляет параметр `departmentId`. Сообщение из очереди `{ "departmentId" : "Finance" }` возвратит все записи для hello финансового отдела. Используйте следующие hello в *function.json*:

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

### <a name="input-sample-with-multiple-documents-in-c"></a>Пример входной привязки с несколькими документами для языка C#

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

### <a name="input-sample-with-multiple-documents-in-javascript"></a>Пример входной привязки с несколькими документами для JavaScript

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

## <a id="docdboutput"></a>Выходная привязка API DocumentDB
привязка позволяет вам создавать новую базу данных Azure Cosmos DB документа tooan вывода Hello DocumentDB API. Он имеет следующие свойства в hello *function.json*:

- `name`: Идентификатор, используемый в коде функция для нового документа hello
- `type`: необходимо задать слишком`"documentdb"`
- `databaseName`: hello базы данных, содержащей коллекцию hello, где будет создан новый документ hello.
- `collectionName`: hello коллекции, где будет создан новый документ hello.
- `createIfNotExists`: Логическое значение tooindicate ли будет создана коллекция hello, если он не существует. по умолчанию Hello — *false*. Здравствуйте, поэтому для этой новой наборы создаются с зарезервированной пропускной способностью, имеющая цены последствия. Для получения дополнительных сведений посетите hello [странице цен](https://azure.microsoft.com/pricing/details/documentdb/).
- `connection`: hello имя параметра приложения hello, содержащий строки подключения Cosmos DB
- `direction`: необходимо задать слишком`"out"`

## <a name="using-a-documentdb-api-output-binding"></a>Использование выходной привязки API DocumentDB
В этом разделе показано, как toouse вывода привязки в коде функция DocumentDB API.

При написании toohello выходного параметра в функции, по умолчанию новый документ создается в базе данных, с автоматически созданным GUID, как hello документов идентификатор. Можно указать идентификатор hello документ выходной документ, указав hello `id` свойства JSON в hello выходной параметр. 

>[!Note]  
>При указании ID hello существующего документа заменяется hello новый выходной документ. 

toooutput несколько документов, можно также привязать слишком`ICollector<T>` или `IAsyncCollector<T>` где `T` является одним из типов hello поддерживается.

<a name="outputsample"></a>

## <a name="documentdb-api-output-binding-sample"></a>Пример выходной привязки API DocumentDB
Предположим, что имеется следующее hello DocumentDB API вывода привязки в hello `bindings` массив function.json:

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

И у вас есть привязка входной очереди для очереди, получающего hello следующая формата JSON:

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

И вы хотите toocreate Cosmos DB документы в кодировке для каждой записи hello:

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

См. пример hello зависящие от языка, который использует этот выходной привязки tooadd документы tooyour базы данных.

* [C#](#outcsharp)
* [F#](#outfsharp)
* [JavaScript](#outjavascript)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Пример выходной привязки для языка C# #

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

### <a name="output-sample-in-f"></a>Пример выходной привязки для языка F# #

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

Для этого образца необходимо `project.json` файл, задающий hello `FSharp.Interop.Dynamic` и `Dynamitey` зависимостей NuGet:

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

tooadd `project.json` файла см. в разделе [пакета управления F #](functions-reference-fsharp.md#package).

<a name="outjavascript"></a>

### <a name="output-sample-in-javascript"></a>Пример выходной привязки для JavaScript

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
