---
title: "aaaWork триггеров и привязок в функциях Azure | Документы Microsoft"
description: "Узнайте, как триггеры toouse и привязки в tooconnect функции Azure вашей события tooonline выполнения кода и облачных служб."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "функции azure, функции, обработка событий, веб-перехватчики, динамические вычисления, независимая архитектура"
ms.assetid: cbc7460a-4d8a-423f-a63e-1cd33fef7252
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: donnam
ms.openlocfilehash: eb2ebfca172fcc8c0f479adbcfec99e90fc33615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-triggers-and-bindings-concepts"></a>Основные понятия триггеров и привязок в Функциях Azure
Функции Azure позволяет toowrite код в ответ tooevents Azure и другие службы через *триггеры* и *привязки*. В этой статье приведены общие сведения о триггерах и привязках для всех поддерживаемых языков программирования. Здесь описаны компоненты, общие tooall привязки.

## <a name="overview"></a>Обзор

Триггеры и привязки являются toodefine декларативным способом способ вызова функции и какие данные она работает с. *Триггер* определяет способ вызова функции. У функции должен быть только один триггер. Триггеры имеют связанные данные, которые обычно являются полезные данные hello, запустившего функции hello. 

Ввод и вывод *привязки* предоставляют toodata tooconnect декларативным способом из кода. Аналогичные tootriggers можно определить строки соединений и другие свойства в конфигурации функции. Привязки необязательны, а у функции может быть несколько входных и выходных привязок. 

С помощью триггеров и привязок, можно написать код, более универсален и выполняет не следует жестко кодировать hello сведения hello служб, с которыми он взаимодействует. Данные, поступающие из служб, становятся для кода вашей функции обычными входными значениями. Служба tooanother toooutput данных (например, для создания новой строки в таблице хранилища Azure), использовать возвращаемое значение метода hello hello. Также при необходимости toooutput несколько значений, можно использовать вспомогательный объект. Триггеры и привязки получают **имя** свойства, которое представляет собой идентификатор, который используется в привязке hello tooaccess кода.

Триггеры и привязки можно настроить в hello **Интеграция** вкладка на портале Azure функции hello. На деле hello hello пользовательского интерфейса изменяет файл с именем *function.json* файл в каталоге функции hello. Этот файл можно редактировать путем изменения toohello **расширенный редактор**.

Hello следующей таблице показаны триггеры hello и привязками, которые поддерживаются с помощью функций Azure. 

[!INCLUDE [Full bindings table](../../includes/functions-bindings.md)]

### <a name="example-queue-trigger-and-table-output-binding"></a>Пример. Триггер очередей и выходная привязка таблицы

Предположим, требуется toowrite новый tooAzure строки таблицы хранилища, при появлении нового сообщения в очередь хранилища Azure. Этот сценарий может быть реализован с помощью триггера очередей Azure и выходной привязки таблицы. 

Очередь триггера требуется hello следующую информацию в hello **Интеграция** вкладки:

* Имя параметра приложения hello, содержащий hello строка подключения учетной записи хранилища для очереди hello Hello
* Имя очереди Hello
* Здравствуйте, идентификатор в ваш код tooread hello содержимое сообщения hello очереди, такие как `order`.

toowrite tooAzure хранилище таблиц использовать привязку с возможностью вывода hello, приведенные ниже сведения:

* Имя параметра приложения hello, содержащий hello строка подключения учетной записи хранилища для таблицы hello Hello
* Имя таблицы Hello
* Идентификатор Hello в ваш код toocreate выходные элементы или возвращаемое значение функции hello hello.

Привязки использовать параметры приложения для практики наиболее hello tooenforce строки подключения, *function.json* не содержит секретные данные службы.

Затем с помощью идентификаторов hello вам предоставлены toointegrate хранилища Azure в коде.

```cs
#r "Newtonsoft.Json"

using Newtonsoft.Json.Linq;

// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello method return value creates a new row in Table Storage
public static Person Run(JObject order, TraceWriter log)
{
    return new Person() { 
            PartitionKey = "Orders", 
            RowKey = Guid.NewGuid().ToString(),  
            Name = order["Name"].ToString(),
            MobileNumber = order["MobileNumber"].ToString() };  
}
 
public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
    public string MobileNumber { get; set; }
}
```

```javascript
// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello second parameter toocontext.done is used as hello value for hello new row
module.exports = function (context, order) {
    order.PartitionKey = "Orders";
    order.RowKey = generateRandomId(); 

    context.done(null, order);
};

function generateRandomId() {
    return Math.random().toString(36).substring(2, 15) +
        Math.random().toString(36).substring(2, 15);
}
```

Вот hello *function.json* , соответствующий toohello предшествующий код. Обратите внимание, что hello, можно использовать такую же настройку независимо от языка hello реализации функции hello.

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "myqueue-items",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    },
    {
      "name": "$return",
      "type": "table",
      "direction": "out",
      "tableName": "outTable",
      "connection": "MY_TABLE_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```
tooview и измените hello содержимое *function.json* в hello портал Azure, щелкните hello **расширенный редактор** параметр hello **Интеграция** вкладку этой функции.

Дополнительные примеры кода и сведения об интеграции со службой хранилища Azure см. в статье [Привязки больших двоичных объектов службы хранилища для Функций Azure](functions-bindings-storage.md).

### <a name="binding-direction"></a>Направление привязки

У всех триггеров и привязок есть направление (свойство `direction`):

- Для триггеров всегда является направление hello`in`
- Для входных и выходных привязок используется как входящее (`in`), так и исходящее (`out`) направление.
- Некоторые привязки поддерживают специальное направление `inout`. Если вы используете `inout`, только hello **расширенный редактор** доступен в hello **интеграции** вкладку.

## <a name="using-hello-function-return-type-tooreturn-a-single-output"></a>С помощью tooreturn тип возвращаемого значения функции hello один выход

Hello предыдущем примере показано, как tooprovide возвращаемое значение функции hello toouse вывода tooa привязку, что достигается с помощью параметра специальным именем hello `$return`. (Это поддерживается только в языках, у которых есть возвращаемое значение, например C#, JavaScript и F#.) Если функция имеет несколько привязок выходные данные, используйте `$return` только для одного из привязок выходного hello. 

```json
// excerpt of function.json
{
    "name": "$return",
    "type": "blob",
    "direction": "out",
    "path": "output-container/{id}"
}
```

Примеры Hello ниже показано как возвращаемые типы используются с привязками выходные данные в C#, JavaScript и F #.

```cs
// C# example: use method return value for output binding
public static string Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```cs
// C# example: async method, using return value for output binding
public static Task<string> Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```javascript
// JavaScript: return a value in hello second parameter toocontext.done
module.exports = function (context, input) {
    var json = JSON.stringify(input);
    context.log('Node.js script processed queue message', json);
    context.done(null, json);
}
```

```fsharp
// F# example: use return value for output binding
let Run(input: WorkItem, log: TraceWriter) =
    let json = String.Format("{{ \"id\": \"{0}\" }}", input.Id)   
    log.Info(sprintf "F# script processed queue message '%s'" json)
    json
```

## <a name="binding-datatype-property"></a>Свойство привязки dataType

В .NET используйте типы toodefine hello hello-тип данных для входных данных. Например, использовать `string` toobind toohello текст триггера очереди и tooread массива байтов в двоичном виде.

Для языков, которые вводятся динамически, таких как JavaScript, использовать hello `dataType` свойство в определении hello привязки. Например, tooread hello содержимого HTTP-запроса в двоичном формате, используйте тип hello `binary`:

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

Другие варианты для `dataType` — `stream` и `string`.

## <a name="resolving-app-settings"></a>Разрешение параметров приложения
Для управления секретами и строками подключения рекомендуется использовать параметры приложения, а не файлы конфигурации. Это ограничивает доступ toothese секреты и делает его безопасный toostore *function.json* в репозитории открытого исходного элемента управления.

Параметры приложения также полезны, когда захотите toochange конфигурации, в зависимости от среды hello. Например в тестовой среде, может потребоваться toomonitor в другой контейнер хранилища очереди или большого двоичного объекта.

Параметры приложения разрешаются, если значение заключено в знаки процента, например `%MyAppSetting%`. Обратите внимание, что hello `connection` свойства триггеров и привязки является особым случаем и автоматически разрешает значения как параметры приложения. 

Hello следующий пример является очередь триггер, который использует Настройка приложения `%input-queue-name%` tootrigger очереди toodefine hello на.

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "%input-queue-name%",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```

## <a name="trigger-metadata-properties"></a>Свойства метаданных триггера

В полезных данных toohello сложения, предоставляемые триггера (например приветственное сообщение очереди, вызвавшей функцию) многие триггеры предоставляют дополнительные метаданные значения. Эти значения можно использовать в качестве входных параметров в C# и F # или свойствам hello `context.bindings` в JavaScript. 

Например триггер очереди поддерживает hello следующие свойства:

* QueueTrigger (содержимое активирующего сообщения, если строка допустима)
* DequeueCount
* ExpirationTime
* Идентификатор
* InsertionTime
* NextVisibleTime
* PopReceipt

Подробные сведения о метаданных свойства для каждого триггера, описаны в hello соответствующие разделы справки. Документация доступна также в hello **Интеграция** вкладку портала hello в hello **документации** ниже hello область конфигурации привязки.  

Например, поскольку триггеры BLOB-объекта некоторое время, можно использовать очереди триггера toorun функции (см. [триггер хранилища больших двоичных объектов](functions-bindings-storage-blob.md#storage-blob-trigger). на приветственное сообщение очереди будет содержать tootrigger filename hello большого двоичного объекта. С помощью hello `queueTrigger` свойства метаданных, можно указать данное поведение в конфигурацию, а не в коде.

```json
  "bindings": [
    {
      "name": "myQueueItem",
      "type": "queueTrigger",
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
    },
    {
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "direction": "in",
      "connection": "MyStorageConnection"
    }
  ]
```

Свойства метаданных из триггера может также использоваться в *выражение привязки* для другой привязке, как описано в разделе hello в следующем разделе.

## <a name="binding-expressions-and-patterns"></a>Выражения привязки и шаблоны

Одним из наиболее мощных функций hello триггеров и привязки является *привязки выражений*. В привязке можно определить шаблоны выражений, которые затем можно использовать в других привязках или коде. Метаданные триггер также могут использоваться в привязке выражений, как показано в образце hello в предшествующих раздел hello.

Предположим, что вы хотите tooresize образы в контейнере отдельного большого двоичного объекта хранилища, аналогичные toohello **изменения размера изображения** шаблона в hello **новая функция** страницы. Go слишком**новая функция** -> язык **C#** -> сценарии **образцы** -> **ImageResizer CSharp**. 

Вот hello *function.json* определение:

```json
{
  "bindings": [
    {
      "name": "image",
      "type": "blobTrigger",
      "path": "sample-images/{filename}",
      "direction": "in",
      "connection": "MyStorageConnection"
    },
    {
      "name": "imageSmall",
      "type": "blob",
      "path": "sample-images-sm/{filename}",
      "direction": "out",
      "connection": "MyStorageConnection"
    }
  ],
}
```

Обратите внимание, что hello `filename` используется параметр в определение триггера hello большого двоичного объекта как, так и больших двоичных объектов hello привязка для вывода. Этот параметр можно также использовать в коде функции.

```csharp
// C# example of binding too{filename}
public static void Run(Stream image, string filename, Stream imageSmall, TraceWriter log)  
{
    log.Info($"Blob trigger processing: {filename}");
    // ...
} 
```

<!--TODO: add JavaScript example -->
<!-- Blocked by bug https://github.com/Azure/Azure-Functions/issues/248 -->


### <a name="random-guids"></a>Случайные значения GUID
Функции Azure предоставляет удобный синтаксис для формирования идентификаторов GUID в привязки, через hello `{rand-guid}` выражение привязки. Hello следующий пример использует этот toogenerate имя уникальным большого двоичного объекта. 

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{rand-guid}"
}
```

### <a name="current-time"></a>Текущее время

Можно использовать выражение привязки hello `DateTime`, который разрешается слишком`DateTime.UtcNow`.

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{DateTime}"
}
```

## <a name="bind-toocustom-input-properties-in-a-binding-expression"></a>Привязать свойства toocustom входа в выражение привязки

Привязки выражений может также ссылаться на свойства, определенные в полезных данных триггер hello сам. Например требуется файл toodynamically bind tooa BLOB-объекта хранилища из имени файла в веб-перехватчик.

Здравствуйте, например, следующая *function.json* использует свойство с именем `BlobName` из полезных данных триггер hello:

```json
{
  "bindings": [
    {
      "name": "info",
      "type": "httpTrigger",
      "direction": "in",
      "webHookType": "genericJson",
    },
    {
      "name": "blobContents",
      "type": "blob",
      "direction": "in",
      "path": "strings/{BlobName}",
      "connection": "AzureWebJobsStorage"
    },
    {
      "name": "res",
      "type": "http",
      "direction": "out"
    }
  ]
}
```

tooaccomplish этого в C# и F #, необходимо определить POCO, определяющая hello поля, которые будут десериализованы в полезных данных hello триггера.

```csharp
using System.Net;

public class BlobInfo
{
    public string BlobName { get; set; }
}
  
public static HttpResponseMessage Run(HttpRequestMessage req, BlobInfo info, string blobContents)
{
    if (blobContents == null) {
        return req.CreateResponse(HttpStatusCode.NotFound);
    } 

    return req.CreateResponse(HttpStatusCode.OK, new {
        data = $"{blobContents}"
    });
}
```

На языке JavaScript автоматически выполняется десериализация JSON и hello свойства можно использовать напрямую.

```javascript
module.exports = function (context, info) {
    if ('BlobName' in info) {
        context.res = {
            body: { 'data': context.bindings.blobContents }
        }
    }
    else {
        context.res = {
            status: 404
        };
    }
    context.done();
}
```

## <a name="configuring-binding-data-at-runtime"></a>Настройка данных привязки во время выполнения

В C# и других языков .NET, можно использовать шаблон императивного привязки как противоположность toohello декларативной привязки в *function.json*. Принудительный привязки полезно в том случае, если параметры привязки должны toobe вычислено во время выполнения, а не конструктора. toolearn более, в разделе [привязки во время выполнения с помощью императивного привязок](functions-reference-csharp.md#imperative-bindings) в Справочник разработчика hello C#.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о конкретной привязки см. следующие статьи hello.

- [HTTP и вызовы webhook](functions-bindings-http-webhook.md)
- [Таймер](functions-bindings-timer.md)
- [Хранилище очередей](functions-bindings-storage-queue.md)
- [Хранилище BLOB-объектов](functions-bindings-storage-blob.md)
- [Хранилище таблиц](functions-bindings-storage-table.md)
- [Концентратор событий](functions-bindings-event-hubs.md)
- [Служебная шина](functions-bindings-service-bus.md)
- [База данных Cosmos DB](functions-bindings-documentdb.md)
- [SendGrid](functions-bindings-sendgrid.md)
- [Twilio](functions-bindings-twilio.md)
- [Центры уведомлений](functions-bindings-notification-hubs.md)
- [Мобильные приложения](functions-bindings-mobile-apps.md)
- [Внешний файл](functions-bindings-external-file.md)
