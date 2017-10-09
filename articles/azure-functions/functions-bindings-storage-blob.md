---
title: "aaaAzure хранилища больших двоичных объектов функций привязки | Документы Microsoft"
description: "Понять, как триггеры toouse хранилища Azure и привязки в функциях Azure."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "функции azure, функции, обработка событий, динамические вычисления, независимая архитектура"
ms.assetid: aba8976c-6568-4ec7-86f5-410efd6b0fb9
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: cef44bd2154d0b97cca9220b6c5024a5b620c80d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-blob-storage-bindings"></a>Привязки хранилища BLOB-объектов для Функций Azure
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

В этой статье объясняется, как tooconfigure и работать с привязками хранилища больших двоичных объектов Azure в функции Azure. Функции Azure поддерживают привязки триггера, а также входные и выходные привязки для хранилища BLOB-объектов Azure. Описание возможностей, доступных во всех привязках, см. в статье [Основные понятия триггеров и привязок в Функциях Azure](functions-triggers-bindings.md).

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!NOTE]
> [Учетная запись хранения только для больших двоичных объектов](../storage/common/storage-create-storage-account.md#blob-storage-accounts) не поддерживается. Триггерам и привязкам хранилища BLOB-объектов требуется учетная запись хранения общего назначения. 
> 

<a name="trigger"></a>
<a name="storage-blob-trigger"></a>
## <a name="blob-storage-triggers-and-bindings"></a>Триггеры и привязки хранилища BLOB-объектов

Использование триггера хранилища больших двоичных объектов Azure hello, коде функция вызывается при обнаружении нового или обновленного большого двоичного объекта. содержимое большого двоичного объекта Hello предоставляются как функции ввода toohello.

Определение триггера хранилища больших двоичных объектов, с помощью hello **Интеграция** вкладка на портале функции hello. Hello портал создает следующие определения в hello hello **привязки** раздел *function.json*:

```json
{
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "type": "blobTrigger",
    "direction": "in",
    "path": "<container toomonitor, and optionally a blob name pattern - see below>",
    "connection": "<Name of app setting - see below>"
}
```

Входные данные большого двоичного объекта и привязок выходного определяются с помощью `blob` hello тип привязки:

```json
{
  "name": "<hello name used tooidentify hello blob input in your code>",
  "type": "blob",
  "direction": "in", // other supported directions are "inout" and "out"
  "path": "<Path of input blob - see below>",
  "connection":"<Name of app setting - see below>"
},
```

* Hello `path` поддерживает свойство привязки выражений и параметров фильтра. См. раздел [Шаблоны имен](#pattern).
* Hello `connection` свойство должно содержать имя hello Настройка приложения, содержащий строки подключения хранилища. В hello портал Azure, hello стандартного редактора в hello **Интеграция** настраивает этот параметр приложения автоматически при выборе учетной записи хранилища.

> [!NOTE]
> При использовании большого двоичного объекта триггера в плане использования, может быть вверх tooa 10 минут задержки в обработке новых больших двоичных объектов после приложения функции неактивными. После запуска приложение функции hello, большие двоичные объекты обрабатываются немедленно. tooavoid этом начальной задержки, рассмотрите одну из следующих вариантов hello:
> - Используйте план службы приложений с включенной функцией AlwaysOn.
> - Используйте другой механизм tootrigger hello большой двоичный объект обработка, например очереди сообщение, содержащее имя большого двоичного объекта hello. Пример см. в разделе [Пример входной привязки](#input-sample).

<a name="pattern"></a>

### <a name="name-patterns"></a>Шаблоны имен
Можно указать шаблон имени большого двоичного объекта в hello `path` свойство, которое может быть выражением фильтра или привязки. См. раздел [Выражения привязки и шаблоны](functions-triggers-bindings.md#binding-expressions-and-patterns).

Например tooblobs toofilter, начинающиеся с «исходный», строка hello использовать следующие определения hello. Этот путь находит большой двоичный объект с именем *исходный Blob1.txt* в hello *ввода* контейнера, а значение hello hello `name` является переменной в коде функция `Blob1`.

```json
"path": "input/original-{name}",
```

toobind toohello большого двоичного объекта имя и расширение файла отдельно, использовать два шаблона. Этот путь также находит большой двоичный объект с именем *исходный Blob1.txt*и значение hello hello `blobname` и `blobextension` переменные в код функции *Blob1 исходный* и *txt*.

```json
"path": "input/{blobname}.{blobextension}",
```

Тип файла hello больших двоичных объектов можно ограничить с помощью фиксированное значение для расширения файла hello. Например tootrigger только на файлы с расширением PNG hello используйте следующий шаблон:

```json
"path": "samples/{name}.png",
```

Фигурные скобки используются в качестве специальных символов в шаблонах имен. toospecify имена больших двоичных объектов, имеющих фигурные скобки в имени hello, escape hello фигурные скобки, с помощью двух фигурные скобки. Hello следующий пример находит большой двоичный объект с именем *{20140101}-soundfile.mp3* в hello *изображения* контейнера и hello `name` значение переменной в коде функции hello  *soundfile.mp3*. 

```json
"path": "images/{{20140101}}-{name}",
```

### <a name="trigger-metadata"></a>Метаданные триггера

триггер Hello больших двоичных объектов предоставляет несколько свойств метаданных. Эти свойства можно использовать как часть выражений привязки в других привязках или как параметры в коде. Эти значения имеют hello совпадает с семантикой [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).

- **BlobTrigger**. Введите `string`. Hello активации пути больших двоичных объектов
- **Uri** Введите `System.Uri`. URI Hello большого двоичного объекта для основного расположения hello.
- **Properties** Введите `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`. Здравствуйте, системные свойства большого двоичного объекта.
- **Metadata** Введите `IDictionary<string,string>`. Здравствуйте, определяемые пользователем метаданные для большого двоичного объекта hello.

<a name="receipts"></a>

### <a name="blob-receipts"></a>Уведомления о получении большого двоичного объекта
Hello Azure функции среды выполнения гарантирует, что функция триггера не большого двоичного объекта вызывается более одного раза для hello же нового или обновленного большого двоичного объекта. toodetermine, если версия данного большого двоичного объекта был обработан, это обеспечивает *большого двоичного объекта уведомления*.

Хранилища Azure функции уведомления в контейнер больших двоичных объектов *размещаемые на веб-заданий для azure* в учетной записи хранилища Azure для приложения функции hello (, заданному параметром приложения hello `AzureWebJobsStorage`). Получение большого двоичного объекта имеет hello следующую информацию:

* Hello запуска функции («*&lt;функция имя приложения >*. Функции.  *&lt;имя функции >*», например: «MyFunctionApp.Functions.CopyBlob»)
* Имя контейнера Hello
* Тип большого двоичного объекта Hello («BlockBlob» или «PageBlob»)
* Имя BLOB-объекта Hello
* Hello ETag (идентификатор версии большого двоичного объекта, например: «0x8D1DC6E70A277EF»)

Повторная обработка tooforce большого двоичного объекта, удалить уведомление о больших двоичных объектов hello для этого большого двоичного объекта из hello *размещаемые на веб-заданий для azure* контейнера вручную.

<a name="poison"></a>

### <a name="handling-poison-blobs"></a>Обработка подозрительных больших двоичных объектов
При сбое функции триггера BLOB-объекта Функции Azure по умолчанию выполняют ее для этого BLOB-объекта еще 5 раз. 

При сбое на все 5 попыток функции Azure добавляет с именем хранилища очереди сообщений tooa *веб-заданий blobtrigger обработки подозрительных сообщений*. приветственное сообщение очереди подозрительных больших двоичных объектов является объект JSON, содержащий hello следующие свойства:

* Идентификатор FunctionId (в формате hello  *&lt;функция имя приложения >*. Функции.  *&lt;имя функции >*)
* BlobType (BlockBlob или PageBlob);
* ContainerName;
* BlobName
* ETag (идентификатор версии BLOB-объектов, например 0x8D1DC6E70A277EF)

### <a name="blob-polling-for-large-containers"></a>Опрос больших двоичных объектов для больших контейнеров
Если контейнер больших двоичных объектов hello отслеживается содержит более 10 000 больших двоичных объектов, функции hello, среда выполнения просматривает журнала toowatch файлов для новых или измененных больших двоичных объектов. Это не происходит в режиме реального времени. Функция может не происходит до нескольких минут или больше после создания большого двоичного объекта hello. Кроме того, [журналы службы хранилища создаются по принципу лучшего из возможного](/rest/api/storageservices/About-Storage-Analytics-Logging), то есть не гарантируется регистрация всех событий. В некоторых случаях журналы могут пропускаться. Если требуется обработка большого двоичного объекта быстрее и надежнее, рассмотрите возможность создания [сообщения в очереди](../storage/queues/storage-dotnet-how-to-use-queues.md) при создании hello большого двоичного объекта. Затем с помощью [очереди триггера](functions-bindings-storage-queue.md) вместо триггер tooprocess hello больших двоичных объектов.

<a name="triggerusage"></a>

## <a name="using-a-blob-trigger-and-input-binding"></a>Использование триггера BLOB-объекта и привязки для ввода
В функциях .NET доступ к данным blob hello, с помощью параметра метода, например `Stream paramName`. Здесь `paramName` hello значение, указанное в hello [конфигурация триггеров](#trigger). В функциях Node.js доступа hello входных данных больших двоичных объектов с помощью `context.bindings.<name>`.

В .NET можно привязать tooany типов hello в расположенном ниже списке hello. При использовании в привязке для ввода некоторые из этих типов требуют направления привязки `inout` в файле *function.json*. Это направление не поддерживается стандартном редакторе hello, поэтому необходимо использовать расширенный редактор hello.

* `TextReader`
* `Stream`
* `ICloudBlob` (требует направления привязки inout)
* `CloudBlockBlob` (требует направления привязки inout)
* `CloudPageBlob` (требует направления привязки inout)
* `CloudAppendBlob` (требует направления привязки inout)

Если ожидаются текст больших двоичных объектов, можно также привязать tooa .NET `string` типа. Рекомендуется, только если размер большого двоичного объекта hello мал, как содержимое hello весь большой двоичный объект загружается в память. Как правило, он является более предпочтительным, чем toouse `Stream` или `CloudBlockBlob` типа.

## <a name="trigger-sample"></a>Пример триггера
Предположим, что имеется следующая function.json hello, определяющий триггер хранилища больших двоичных объектов:

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "myBlob",
            "type": "blobTrigger",
            "direction": "in",
            "path": "samples-workitems",
            "connection":"MyStorageAccount"
        }
    ]
}
```

См. Образец hello конкретного языка, зарегистрировавший hello содержимое каждого добавленного toohello отслеживаемых контейнера BLOB-объекта.

* [C#](#triggercsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="blob-trigger-examples-in-c"></a>Примеры триггеров BLOB-объектов на C# #

```cs
// Blob trigger sample using a Stream binding
public static void Run(Stream myBlob, TraceWriter log)
{
   log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

```cs
// Blob trigger binding tooa CloudBlockBlob
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Blob;

public static void Run(CloudBlockBlob myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name}\nURI:{myBlob.StorageUri}");
}
```

<a name="triggernodejs"></a>

### <a name="trigger-example-in-nodejs"></a>Пример триггера в Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js Blob trigger function processed', context.bindings.myBlob);
    context.done();
};
```
<a name="outputusage"></a>
<a name="storage-blob-output-binding"></a>

## <a name="using-a-blob-output-binding"></a>Использование привязки BLOB-объекта для вывода

В функциях .NET, следует использовать либо `out string` параметров в сигнатуры функции или использовать один из типов hello в hello после списка. В функции Node.js, доступ к hello вывода больших двоичных объектов с помощью `context.bindings.<name>`.

В функциях .NET могут выводиться tooany из hello следующие типы:

* `out string`
* `TextWriter`
* `Stream`
* `CloudBlobStream`
* `ICloudBlob`
* `CloudBlockBlob` 
* `CloudPageBlob` 

<a name="input-sample"></a>

## <a name="queue-trigger-with-blob-input-and-output-sample"></a>Пример триггера очереди с вводом и выводом BLOB-объекта
Предположим, что имеется следующая function.json hello, определяющий [хранилища очередей триггер](functions-bindings-storage-queue.md)входных данных в хранилище больших двоичных объектов и выходные данные в хранилище больших двоичных объектов. Использование уведомления hello hello `queueTrigger` свойства метаданных. в большом двоичном объекте hello входной и выходной `path` свойства:

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
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "MyStorageConnection",
      "direction": "in"
    },
    {
      "name": "myOutputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "MyStorageConnection",
      "direction": "out"
    }
  ],
  "disabled": false
}
``` 

См. пример hello зависящие от языка, который копирует hello ввода toohello выходные данные больших двоичных объектов.

* [C#](#incsharp)
* [Node.js](#innodejs)

<a name="incsharp"></a>

### <a name="blob-binding-example-in-c"></a>Пример привязки BLOB-объекта на C# #

```cs
// Copy blob from input toooutput, based on a queue trigger
public static void Run(string myQueueItem, Stream myInputBlob, out string myOutputBlob, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputBlob = myInputBlob;
}
```

<a name="innodejs"></a>

### <a name="blob-binding-example-in-nodejs"></a>Пример привязки BLOB-объекта в Node.js

```javascript
// Copy blob from input toooutput, based on a queue trigger
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputBlob = context.bindings.myInputBlob;
    context.done();
};
```

## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

