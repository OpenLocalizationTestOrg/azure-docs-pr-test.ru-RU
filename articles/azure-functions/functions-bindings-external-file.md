---
title: "aaaAzure функции внешний файл привязки (Предварительная версия) | Документы Microsoft"
description: "Использование привязок внешних файлов в Функциях Azure"
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/12/2017
ms.author: alkarche
ms.openlocfilehash: 583d9c0b871dc68a79614749ba6ac6711fa820fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-external-file-bindings-preview"></a>Привязки внешних файлов в Функциях Azure (предварительная версия)
В этой статье показано, как toomanipulate файлов из разных SaaS поставщиков (например, OneDrive, Dropbox) внутри функции использованием встроенных привязок. Функции Azure поддерживают привязки триггера, а также входные и выходные привязки для внешних файлов.

Эта привязка создает подключений API tooSaaS поставщиков или использует существующие подключения API из группы ресурсов в приложении функции.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="supported-file-connections"></a>Поддерживаемые подключения файлов

|Соединитель|Триггер|Входные данные|Выходные данные|
|:-----|:---:|:---:|:---:|
|[Box](https://www.box.com)|x|x|x
|[Dropbox](https://www.dropbox.com)|x|x|x
|[FTP](https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp)|x|x|x
|[OneDrive](https://onedrive.live.com)|x|x|x
|[OneDrive для бизнеса](https://onedrive.live.com/about/business/)|x|x|x
|[SFTP](https://docs.microsoft.com/azure/connectors/connectors-create-api-sftp)|x|x|x
|[Диск Google](https://www.google.com/drive/)||x|x|

> [!NOTE]
> В [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list) могут также использоваться подключения к внешним файлам.

## <a name="external-file-trigger-binding"></a>Привязка триггера внешнего файла

Hello Azure внешнего файла триггер позволяет отслеживать удаленную папку и запуск кода функции при обнаружении изменений.

используются следующие объекты JSON в hello hello триггером внешнего файла Hello `bindings` массив function.json

```json
{
  "type": "apiHubFileTrigger",
  "name": "<Name of input parameter in function signature>",
  "direction": "in",
  "path": "<folder toomonitor, and optionally a name pattern - see below>",
  "connection": "<name of external file connection - see above>"
}
```
<!---
See one of hello following subheadings for more information:

* [Name patterns](#pattern)
* [File receipts](#receipts)
* [Handling poison files](#poison)
--->

<a name="pattern"></a>

### <a name="name-patterns"></a>Шаблоны имен
Можно указать шаблон имени файла в hello `path` свойство. ссылка на папку Hello должен существовать в поставщик SaaS hello.
Примеры:

```json
"path": "input/original-{name}",
```

Этот путь может найти файл с именем *исходный File1.txt* в hello *ввода* папки, а значение hello hello `name` переменной в коде функция будет `File1.txt`.

Другой пример:

```json
"path": "input/{filename}.{fileextension}",
```

Этот путь также найти файл с именем *исходный File1.txt*и значение hello hello `filename` и `fileextension` переменных в коде функция будет *исходной файл1* и  *txt*.

Тип файла hello файлов можно ограничить с помощью фиксированное значение для расширения файла hello. Например:

```json
"path": "samples/{name}.png",
```

В этом случае только *.png* файлы в hello *образцы* функции hello папку триггера.

Фигурные скобки используются в качестве специальных символов в шаблонах имен. toospecify имена файлов, имеющих фигурные скобки в имени hello, hello двойные фигурные скобки.
Например:

```json
"path": "images/{{20140101}}-{name}",
```

Этот путь может найти файл с именем *{20140101}-soundfile.mp3* в hello *изображения* папки и hello `name` бы значение переменной в коде функции hello *soundfile.mp3*.

<a name="receipts"></a>

<!--- ### File receipts
hello Azure Functions runtime makes sure that no external file trigger function gets called more than once for hello same new or updated file.
It does so by maintaining *file receipts* toodetermine if a given file version has been processed.

File receipts are stored in a folder named *azure-webjobs-hosts* in hello Azure storage account for your function app
(specified by hello `AzureWebJobsStorage` app setting). A file receipt has hello following information:

* hello triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "functionsf74b96f7.Functions.CopyFile")
* hello folder name
* hello file type ("BlockFile" or "PageFile")
* hello file name
* hello ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")

tooforce reprocessing of a file, delete hello file receipt for that file from hello *azure-webjobs-hosts* folder manually.
--->
<a name="poison"></a>

### <a name="handling-poison-files"></a>Обработка подозрительных файлов
Когда функция триггера внешнего файла завершается сбоем, функции Azure повторяет этой функции too5 времени по умолчанию (включая первой попытки hello) для данного файла.
Добавляет при сбое на все 5 попыток функции с именем хранилища очереди сообщений tooa *веб-заданий apihubtrigger обработки подозрительных сообщений*. приветственное сообщение очереди подозрительных файлов является объект JSON, содержащий hello следующие свойства:

* Идентификатор FunctionId (в формате hello  *&lt;функция имя приложения >*. Функции.  *&lt;имя функции >*)
* FileType
* FolderName
* FileName
* ETag (идентификатор версии файла, например 0x8D1DC6E70A277EF)


<a name="triggerusage"></a>

## <a name="trigger-usage"></a>Использование триггера
В C# функции, привязать toohello входной файл данных с помощью именованного параметра в подписи функции, например `<T> <name>`.
Где `T` имеет тип данных hello нужных данных toodeserialize hello в, и `paramName` — hello имя, указанное в [триггера JSON](#trigger). В функции Node.js, доступ к hello входной файл данных с помощью `context.bindings.<name>`.

можно выполнить десериализацию файла Hello в любые hello следующие типы:

* Любой [объект](https://msdn.microsoft.com/library/system.object.aspx) используется для сериализованных данных JSON файла.
  Если объявить пользовательский тип входных данных (например `FooType`), функции Azure пытается данных JSON toodeserialize hello в указанный тип.
* Строка - используется для текстовых данных файла.

В C# функции можно также привязать tooany из hello следующие типы и среды выполнения функции hello предпринимает попытку десериализовать hello файл данных с помощью этого типа:

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`

## <a name="trigger-sample"></a>Пример триггера
Предположим, что имеется следующая function.json hello, который определяет триггер внешнего файла:

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "myFile",
            "type": "apiHubFileTrigger",
            "direction": "in",
            "path": "samples-workitems",
            "connection": "<name of external file connection>"
        }
    ]
}
```

См. Образец hello конкретного языка, записывает содержимое каждого файла, который добавляется в папку отслеживаемых toohello hello.

* [C#](#triggercsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-usage-in-c"></a>Использование триггера на языке C# #

```cs
public static void Run(string myFile, TraceWriter log)
{
    log.Info($"C# File trigger function processed: {myFile}");
}
```

<!--
<a name="triggerfsharp"></a>
### Trigger usage in F# ##
```fsharp

```
-->

<a name="triggernodejs"></a>

### <a name="trigger-usage-in-nodejs"></a>Использование триггера для Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js File trigger function processed', context.bindings.myFile);
    context.done();
};
```

<a name="input"></a>

## <a name="external-file-input-binding"></a>Входная привязка внешнего файла
Привязка ввода Hello Azure внешнего файла позволяет toouse файл из внешней папки в функции.

Hello внешнего файла ввода tooa функция использует следующие объекты JSON в hello hello `bindings` массив function.json:

```json
{
  "name": "<Name of input parameter in function signature>",
  "type": "apiHubFile",
  "direction": "in",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
},
```

Обратите внимание hello следующие:

* `path`должен содержать имя папки hello и имя файла hello. Например, если у вас есть [очереди триггера](functions-bindings-storage-queue.md) в функции, можно использовать `"path": "samples-workitems/{queueTrigger}"` toopoint tooa файла в hello `samples-workitems` папки с именем, совпадающим с именем hello файл, указанный в сообщении hello триггера.   

<a name="inputusage"></a>

## <a name="input-usage"></a>Использование входной привязки
В C# функции, привязать toohello входной файл данных с помощью именованного параметра в подписи функции, например `<T> <name>`.
Где `T` имеет тип данных hello нужных данных toodeserialize hello в, и `paramName` — hello имя, указанное в [входной привязки](#input). В функции Node.js, доступ к hello входной файл данных с помощью `context.bindings.<name>`.

можно выполнить десериализацию файла Hello в любые hello следующие типы:

* Любой [объект](https://msdn.microsoft.com/library/system.object.aspx) используется для сериализованных данных JSON файла.
  Если объявить пользовательский тип входных данных (например `InputType`), функции Azure пытается данных JSON toodeserialize hello в указанный тип.
* Строка - используется для текстовых данных файла.

В C# функции можно также привязать tooany из hello следующие типы и среды выполнения функции hello предпринимает попытку десериализовать hello файл данных с помощью этого типа:

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`


<a name="output"></a>

## <a name="external-file-output-binding"></a>Выходная привязка внешнего файла
Hello Azure внешний файл вывода привязка позволяет toowrite tooan внешних папку с файлами в функции.

выходные данные для функции используются следующие объекты JSON в hello hello внешнего файла Hello `bindings` массив function.json:

```json
{
  "name": "<Name of output parameter in function signature>",
  "type": "apiHubFile",
  "direction": "out",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
}
```

Обратите внимание hello следующие:

* `path`должен содержать имя папки hello и hello toowrite имя файла для. Например, если у вас есть [очереди триггера](functions-bindings-storage-queue.md) в функции, можно использовать `"path": "samples-workitems/{queueTrigger}"` toopoint tooa файла в hello `samples-workitems` папки с именем, совпадающим с именем hello файл, указанный в сообщении hello триггера.   

<a name="outputusage"></a>

## <a name="output-usage"></a>Использование выходной привязки
В C# функции, можно привязать toohello выходной файл с помощью hello с именем `out` параметра в подписи функции, такие как `out <T> <name>`, где `T` имеет тип данных hello нужных данных tooserialize hello в, и `paramName` является hello имя указанный в [привязка для вывода](#output). В функции Node.js, доступ к hello выходной файл с помощью `context.bindings.<name>`.

Можно написать toohello выходной файл с помощью любого hello следующие типы:

* Любой [объект](https://msdn.microsoft.com/library/system.object.aspx) используется для сериализации JSON.
  При объявлении типа настраиваемые выходные данные (например `out OutputType paramName`), функции Azure пытается tooserialize объекта в JSON. Если hello выходной параметр имеет значение null, при выходе из функции hello, среда выполнения функции hello создает файл как объект null.
* Строка - (`out string paramName`) используется для текстовых данных файла. Среда выполнения функции Hello создает файл только в том случае, если параметр строки не равно null, при выходе из функции hello.

В C# функции также могут выводиться tooany из hello следующие типы:

* `TextWriter`
* `Stream`
* `CloudFileStream`
* `ICloudFile`
* `CloudBlockFile`
* `CloudPageFile`

<a name="outputsample"></a>

<a name="sample"></a>

## <a name="input--output-sample"></a>Пример входных и выходных данных
Предположим, что имеется следующая function.json hello, определяющий [хранилища очереди триггера](functions-bindings-storage-queue.md)внешнего файла ввода и вывода во внешний файл:

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
      "name": "myInputFile",
      "type": "apiHubFile",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "<name of external file connection>",
      "direction": "in"
    },
    {
      "name": "myOutputFile",
      "type": "apiHubFile",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "<name of external file connection>",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

См. пример hello зависящие от языка, который копирует hello входной файл toohello выходного файла.

* [C#](#incsharp)
* [Node.js](#innodejs)

<a name="incsharp"></a>

### <a name="usage-in-c"></a>Использование в языке C# #

```cs
public static void Run(string myQueueItem, string myInputFile, out string myOutputFile, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputFile = myInputFile;
}
```

<!--
<a name="infsharp"></a>
### Input usage in F# ##
```fsharp

```
-->

<a name="innodejs"></a>

### <a name="usage-in-nodejs"></a>Использование для Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```

## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
