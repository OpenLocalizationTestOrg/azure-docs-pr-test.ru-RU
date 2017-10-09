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
# <a name="azure-functions-external-file-bindings-preview"></a><span data-ttu-id="d7da5-103">Привязки внешних файлов в Функциях Azure (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="d7da5-103">Azure Functions External File bindings (Preview)</span></span>
<span data-ttu-id="d7da5-104">В этой статье показано, как toomanipulate файлов из разных SaaS поставщиков (например, OneDrive, Dropbox) внутри функции использованием встроенных привязок.</span><span class="sxs-lookup"><span data-stu-id="d7da5-104">This article shows how toomanipulate files from different SaaS providers (e.g. OneDrive, Dropbox) within your function utilizing built-in bindings.</span></span> <span data-ttu-id="d7da5-105">Функции Azure поддерживают привязки триггера, а также входные и выходные привязки для внешних файлов.</span><span class="sxs-lookup"><span data-stu-id="d7da5-105">Azure functions supports trigger, input, and output bindings for external file.</span></span>

<span data-ttu-id="d7da5-106">Эта привязка создает подключений API tooSaaS поставщиков или использует существующие подключения API из группы ресурсов в приложении функции.</span><span class="sxs-lookup"><span data-stu-id="d7da5-106">This binding creates API connections tooSaaS providers, or uses existing API connections from your Function App's resource group.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="supported-file-connections"></a><span data-ttu-id="d7da5-107">Поддерживаемые подключения файлов</span><span class="sxs-lookup"><span data-stu-id="d7da5-107">Supported File connections</span></span>

|<span data-ttu-id="d7da5-108">Соединитель</span><span class="sxs-lookup"><span data-stu-id="d7da5-108">Connector</span></span>|<span data-ttu-id="d7da5-109">Триггер</span><span class="sxs-lookup"><span data-stu-id="d7da5-109">Trigger</span></span>|<span data-ttu-id="d7da5-110">Входные данные</span><span class="sxs-lookup"><span data-stu-id="d7da5-110">Input</span></span>|<span data-ttu-id="d7da5-111">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="d7da5-111">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="d7da5-112">Box</span><span class="sxs-lookup"><span data-stu-id="d7da5-112">Box</span></span>](https://www.box.com)|<span data-ttu-id="d7da5-113">x</span><span class="sxs-lookup"><span data-stu-id="d7da5-113">x</span></span>|<span data-ttu-id="d7da5-114">x</span><span class="sxs-lookup"><span data-stu-id="d7da5-114">x</span></span>|<span data-ttu-id="d7da5-115">x</span><span class="sxs-lookup"><span data-stu-id="d7da5-115">x</span></span>
|[<span data-ttu-id="d7da5-116">Dropbox</span><span class="sxs-lookup"><span data-stu-id="d7da5-116">Dropbox</span></span>](https://www.dropbox.com)|<span data-ttu-id="d7da5-117">x</span><span class="sxs-lookup"><span data-stu-id="d7da5-117">x</span></span>|<span data-ttu-id="d7da5-118">x</span><span class="sxs-lookup"><span data-stu-id="d7da5-118">x</span></span>|<span data-ttu-id="d7da5-119">x</span><span class="sxs-lookup"><span data-stu-id="d7da5-119">x</span></span>
|[<span data-ttu-id="d7da5-120">FTP</span><span class="sxs-lookup"><span data-stu-id="d7da5-120">FTP</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp)|<span data-ttu-id="d7da5-121">x</span><span class="sxs-lookup"><span data-stu-id="d7da5-121">x</span></span>|<span data-ttu-id="d7da5-122">x</span><span class="sxs-lookup"><span data-stu-id="d7da5-122">x</span></span>|<span data-ttu-id="d7da5-123">x</span><span class="sxs-lookup"><span data-stu-id="d7da5-123">x</span></span>
|[<span data-ttu-id="d7da5-124">OneDrive</span><span class="sxs-lookup"><span data-stu-id="d7da5-124">OneDrive</span></span>](https://onedrive.live.com)|<span data-ttu-id="d7da5-125">x</span><span class="sxs-lookup"><span data-stu-id="d7da5-125">x</span></span>|<span data-ttu-id="d7da5-126">x</span><span class="sxs-lookup"><span data-stu-id="d7da5-126">x</span></span>|<span data-ttu-id="d7da5-127">x</span><span class="sxs-lookup"><span data-stu-id="d7da5-127">x</span></span>
|[<span data-ttu-id="d7da5-128">OneDrive для бизнеса</span><span class="sxs-lookup"><span data-stu-id="d7da5-128">OneDrive for Business</span></span>](https://onedrive.live.com/about/business/)|<span data-ttu-id="d7da5-129">x</span><span class="sxs-lookup"><span data-stu-id="d7da5-129">x</span></span>|<span data-ttu-id="d7da5-130">x</span><span class="sxs-lookup"><span data-stu-id="d7da5-130">x</span></span>|<span data-ttu-id="d7da5-131">x</span><span class="sxs-lookup"><span data-stu-id="d7da5-131">x</span></span>
|[<span data-ttu-id="d7da5-132">SFTP</span><span class="sxs-lookup"><span data-stu-id="d7da5-132">SFTP</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sftp)|<span data-ttu-id="d7da5-133">x</span><span class="sxs-lookup"><span data-stu-id="d7da5-133">x</span></span>|<span data-ttu-id="d7da5-134">x</span><span class="sxs-lookup"><span data-stu-id="d7da5-134">x</span></span>|<span data-ttu-id="d7da5-135">x</span><span class="sxs-lookup"><span data-stu-id="d7da5-135">x</span></span>
|[<span data-ttu-id="d7da5-136">Диск Google</span><span class="sxs-lookup"><span data-stu-id="d7da5-136">Google Drive</span></span>](https://www.google.com/drive/)||<span data-ttu-id="d7da5-137">x</span><span class="sxs-lookup"><span data-stu-id="d7da5-137">x</span></span>|<span data-ttu-id="d7da5-138">x</span><span class="sxs-lookup"><span data-stu-id="d7da5-138">x</span></span>|

> [!NOTE]
> <span data-ttu-id="d7da5-139">В [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list) могут также использоваться подключения к внешним файлам.</span><span class="sxs-lookup"><span data-stu-id="d7da5-139">External File connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

## <a name="external-file-trigger-binding"></a><span data-ttu-id="d7da5-140">Привязка триггера внешнего файла</span><span class="sxs-lookup"><span data-stu-id="d7da5-140">External File trigger binding</span></span>

<span data-ttu-id="d7da5-141">Hello Azure внешнего файла триггер позволяет отслеживать удаленную папку и запуск кода функции при обнаружении изменений.</span><span class="sxs-lookup"><span data-stu-id="d7da5-141">hello Azure external file trigger lets you monitor a remote folder and run your function code when changes are detected.</span></span>

<span data-ttu-id="d7da5-142">используются следующие объекты JSON в hello hello триггером внешнего файла Hello `bindings` массив function.json</span><span class="sxs-lookup"><span data-stu-id="d7da5-142">hello external file trigger uses hello following JSON objects in hello `bindings` array of function.json</span></span>

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

### <a name="name-patterns"></a><span data-ttu-id="d7da5-143">Шаблоны имен</span><span class="sxs-lookup"><span data-stu-id="d7da5-143">Name patterns</span></span>
<span data-ttu-id="d7da5-144">Можно указать шаблон имени файла в hello `path` свойство.</span><span class="sxs-lookup"><span data-stu-id="d7da5-144">You can specify a file name pattern in hello `path` property.</span></span> <span data-ttu-id="d7da5-145">ссылка на папку Hello должен существовать в поставщик SaaS hello.</span><span class="sxs-lookup"><span data-stu-id="d7da5-145">hello folder referenced must exist in hello SaaS provider.</span></span>
<span data-ttu-id="d7da5-146">Примеры:</span><span class="sxs-lookup"><span data-stu-id="d7da5-146">Examples:</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="d7da5-147">Этот путь может найти файл с именем *исходный File1.txt* в hello *ввода* папки, а значение hello hello `name` переменной в коде функция будет `File1.txt`.</span><span class="sxs-lookup"><span data-stu-id="d7da5-147">This path would find a file named *original-File1.txt* in hello *input* folder, and hello value of hello `name` variable in function code would be `File1.txt`.</span></span>

<span data-ttu-id="d7da5-148">Другой пример:</span><span class="sxs-lookup"><span data-stu-id="d7da5-148">Another example:</span></span>

```json
"path": "input/{filename}.{fileextension}",
```

<span data-ttu-id="d7da5-149">Этот путь также найти файл с именем *исходный File1.txt*и значение hello hello `filename` и `fileextension` переменных в коде функция будет *исходной файл1* и  *txt*.</span><span class="sxs-lookup"><span data-stu-id="d7da5-149">This path would also find a file named *original-File1.txt*, and hello value of hello `filename` and `fileextension` variables in function code would be *original-File1* and *txt*.</span></span>

<span data-ttu-id="d7da5-150">Тип файла hello файлов можно ограничить с помощью фиксированное значение для расширения файла hello.</span><span class="sxs-lookup"><span data-stu-id="d7da5-150">You can restrict hello file type of files by using a fixed value for hello file extension.</span></span> <span data-ttu-id="d7da5-151">Например:</span><span class="sxs-lookup"><span data-stu-id="d7da5-151">For example:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="d7da5-152">В этом случае только *.png* файлы в hello *образцы* функции hello папку триггера.</span><span class="sxs-lookup"><span data-stu-id="d7da5-152">In this case, only *.png* files in hello *samples* folder trigger hello function.</span></span>

<span data-ttu-id="d7da5-153">Фигурные скобки используются в качестве специальных символов в шаблонах имен.</span><span class="sxs-lookup"><span data-stu-id="d7da5-153">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="d7da5-154">toospecify имена файлов, имеющих фигурные скобки в имени hello, hello двойные фигурные скобки.</span><span class="sxs-lookup"><span data-stu-id="d7da5-154">toospecify file names that have curly braces in hello name, double hello curly braces.</span></span>
<span data-ttu-id="d7da5-155">Например:</span><span class="sxs-lookup"><span data-stu-id="d7da5-155">For example:</span></span>

```json
"path": "images/{{20140101}}-{name}",
```

<span data-ttu-id="d7da5-156">Этот путь может найти файл с именем *{20140101}-soundfile.mp3* в hello *изображения* папки и hello `name` бы значение переменной в коде функции hello *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="d7da5-156">This path would find a file named *{20140101}-soundfile.mp3* in hello *images* folder, and hello `name` variable value in hello function code would be *soundfile.mp3*.</span></span>

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

### <a name="handling-poison-files"></a><span data-ttu-id="d7da5-157">Обработка подозрительных файлов</span><span class="sxs-lookup"><span data-stu-id="d7da5-157">Handling poison files</span></span>
<span data-ttu-id="d7da5-158">Когда функция триггера внешнего файла завершается сбоем, функции Azure повторяет этой функции too5 времени по умолчанию (включая первой попытки hello) для данного файла.</span><span class="sxs-lookup"><span data-stu-id="d7da5-158">When an external file trigger function fails, Azure Functions retries that function up too5 times by default (including hello first try) for a given file.</span></span>
<span data-ttu-id="d7da5-159">Добавляет при сбое на все 5 попыток функции с именем хранилища очереди сообщений tooa *веб-заданий apihubtrigger обработки подозрительных сообщений*.</span><span class="sxs-lookup"><span data-stu-id="d7da5-159">If all 5 tries fail, Functions adds a message tooa Storage queue named *webjobs-apihubtrigger-poison*.</span></span> <span data-ttu-id="d7da5-160">приветственное сообщение очереди подозрительных файлов является объект JSON, содержащий hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="d7da5-160">hello queue message for poison files is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="d7da5-161">Идентификатор FunctionId (в формате hello  *&lt;функция имя приложения >*. Функции.  *&lt;имя функции >*)</span><span class="sxs-lookup"><span data-stu-id="d7da5-161">FunctionId (in hello format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="d7da5-162">FileType</span><span class="sxs-lookup"><span data-stu-id="d7da5-162">FileType</span></span>
* <span data-ttu-id="d7da5-163">FolderName</span><span class="sxs-lookup"><span data-stu-id="d7da5-163">FolderName</span></span>
* <span data-ttu-id="d7da5-164">FileName</span><span class="sxs-lookup"><span data-stu-id="d7da5-164">FileName</span></span>
* <span data-ttu-id="d7da5-165">ETag (идентификатор версии файла, например 0x8D1DC6E70A277EF)</span><span class="sxs-lookup"><span data-stu-id="d7da5-165">ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")</span></span>


<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="d7da5-166">Использование триггера</span><span class="sxs-lookup"><span data-stu-id="d7da5-166">Trigger usage</span></span>
<span data-ttu-id="d7da5-167">В C# функции, привязать toohello входной файл данных с помощью именованного параметра в подписи функции, например `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="d7da5-167">In C# functions, you bind toohello input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="d7da5-168">Где `T` имеет тип данных hello нужных данных toodeserialize hello в, и `paramName` — hello имя, указанное в [триггера JSON](#trigger).</span><span class="sxs-lookup"><span data-stu-id="d7da5-168">Where `T` is hello data type that you want toodeserialize hello data into, and `paramName` is hello name you specified in the [trigger JSON](#trigger).</span></span> <span data-ttu-id="d7da5-169">В функции Node.js, доступ к hello входной файл данных с помощью `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="d7da5-169">In Node.js functions, you access hello input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="d7da5-170">можно выполнить десериализацию файла Hello в любые hello следующие типы:</span><span class="sxs-lookup"><span data-stu-id="d7da5-170">hello file can be deserialized into any of hello following types:</span></span>

* <span data-ttu-id="d7da5-171">Любой [объект](https://msdn.microsoft.com/library/system.object.aspx) используется для сериализованных данных JSON файла.</span><span class="sxs-lookup"><span data-stu-id="d7da5-171">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="d7da5-172">Если объявить пользовательский тип входных данных (например `FooType`), функции Azure пытается данных JSON toodeserialize hello в указанный тип.</span><span class="sxs-lookup"><span data-stu-id="d7da5-172">If you declare a custom input type (e.g. `FooType`), Azure Functions attempts toodeserialize hello JSON data into your specified type.</span></span>
* <span data-ttu-id="d7da5-173">Строка - используется для текстовых данных файла.</span><span class="sxs-lookup"><span data-stu-id="d7da5-173">String - useful for text file data.</span></span>

<span data-ttu-id="d7da5-174">В C# функции можно также привязать tooany из hello следующие типы и среды выполнения функции hello предпринимает попытку десериализовать hello файл данных с помощью этого типа:</span><span class="sxs-lookup"><span data-stu-id="d7da5-174">In C# functions, you can also bind tooany of hello following types, and hello Functions runtime attempts to deserialize hello file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`

## <a name="trigger-sample"></a><span data-ttu-id="d7da5-175">Пример триггера</span><span class="sxs-lookup"><span data-stu-id="d7da5-175">Trigger sample</span></span>
<span data-ttu-id="d7da5-176">Предположим, что имеется следующая function.json hello, который определяет триггер внешнего файла:</span><span class="sxs-lookup"><span data-stu-id="d7da5-176">Suppose you have hello following function.json, that defines an external file trigger:</span></span>

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

<span data-ttu-id="d7da5-177">См. Образец hello конкретного языка, записывает содержимое каждого файла, который добавляется в папку отслеживаемых toohello hello.</span><span class="sxs-lookup"><span data-stu-id="d7da5-177">See hello language-specific sample that logs hello contents of each file that is added toohello monitored folder.</span></span>

* [<span data-ttu-id="d7da5-178">C#</span><span class="sxs-lookup"><span data-stu-id="d7da5-178">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="d7da5-179">Node.js</span><span class="sxs-lookup"><span data-stu-id="d7da5-179">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-usage-in-c"></a><span data-ttu-id="d7da5-180">Использование триггера на языке C#</span><span class="sxs-lookup"><span data-stu-id="d7da5-180">Trigger usage in C#</span></span> #

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

### <a name="trigger-usage-in-nodejs"></a><span data-ttu-id="d7da5-181">Использование триггера для Node.js</span><span class="sxs-lookup"><span data-stu-id="d7da5-181">Trigger usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js File trigger function processed', context.bindings.myFile);
    context.done();
};
```

<a name="input"></a>

## <a name="external-file-input-binding"></a><span data-ttu-id="d7da5-182">Входная привязка внешнего файла</span><span class="sxs-lookup"><span data-stu-id="d7da5-182">External File input binding</span></span>
<span data-ttu-id="d7da5-183">Привязка ввода Hello Azure внешнего файла позволяет toouse файл из внешней папки в функции.</span><span class="sxs-lookup"><span data-stu-id="d7da5-183">hello Azure external file input binding enables you toouse a file from an external folder in your function.</span></span>

<span data-ttu-id="d7da5-184">Hello внешнего файла ввода tooa функция использует следующие объекты JSON в hello hello `bindings` массив function.json:</span><span class="sxs-lookup"><span data-stu-id="d7da5-184">hello external file input tooa function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of input parameter in function signature>",
  "type": "apiHubFile",
  "direction": "in",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
},
```

<span data-ttu-id="d7da5-185">Обратите внимание hello следующие:</span><span class="sxs-lookup"><span data-stu-id="d7da5-185">Note hello following:</span></span>

* <span data-ttu-id="d7da5-186">`path`должен содержать имя папки hello и имя файла hello.</span><span class="sxs-lookup"><span data-stu-id="d7da5-186">`path` must contain hello folder name and hello file name.</span></span> <span data-ttu-id="d7da5-187">Например, если у вас есть [очереди триггера](functions-bindings-storage-queue.md) в функции, можно использовать `"path": "samples-workitems/{queueTrigger}"` toopoint tooa файла в hello `samples-workitems` папки с именем, совпадающим с именем hello файл, указанный в сообщении hello триггера.</span><span class="sxs-lookup"><span data-stu-id="d7da5-187">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` toopoint tooa file in hello `samples-workitems` folder with a name that matches hello file name specified in hello trigger message.</span></span>   

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="d7da5-188">Использование входной привязки</span><span class="sxs-lookup"><span data-stu-id="d7da5-188">Input usage</span></span>
<span data-ttu-id="d7da5-189">В C# функции, привязать toohello входной файл данных с помощью именованного параметра в подписи функции, например `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="d7da5-189">In C# functions, you bind toohello input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="d7da5-190">Где `T` имеет тип данных hello нужных данных toodeserialize hello в, и `paramName` — hello имя, указанное в [входной привязки](#input).</span><span class="sxs-lookup"><span data-stu-id="d7da5-190">Where `T` is hello data type that you want toodeserialize hello data into, and `paramName` is hello name you specified in the [input binding](#input).</span></span> <span data-ttu-id="d7da5-191">В функции Node.js, доступ к hello входной файл данных с помощью `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="d7da5-191">In Node.js functions, you access hello input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="d7da5-192">можно выполнить десериализацию файла Hello в любые hello следующие типы:</span><span class="sxs-lookup"><span data-stu-id="d7da5-192">hello file can be deserialized into any of hello following types:</span></span>

* <span data-ttu-id="d7da5-193">Любой [объект](https://msdn.microsoft.com/library/system.object.aspx) используется для сериализованных данных JSON файла.</span><span class="sxs-lookup"><span data-stu-id="d7da5-193">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="d7da5-194">Если объявить пользовательский тип входных данных (например `InputType`), функции Azure пытается данных JSON toodeserialize hello в указанный тип.</span><span class="sxs-lookup"><span data-stu-id="d7da5-194">If you declare a custom input type (e.g. `InputType`), Azure Functions attempts toodeserialize hello JSON data into your specified type.</span></span>
* <span data-ttu-id="d7da5-195">Строка - используется для текстовых данных файла.</span><span class="sxs-lookup"><span data-stu-id="d7da5-195">String - useful for text file data.</span></span>

<span data-ttu-id="d7da5-196">В C# функции можно также привязать tooany из hello следующие типы и среды выполнения функции hello предпринимает попытку десериализовать hello файл данных с помощью этого типа:</span><span class="sxs-lookup"><span data-stu-id="d7da5-196">In C# functions, you can also bind tooany of hello following types, and hello Functions runtime attempts to deserialize hello file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`


<a name="output"></a>

## <a name="external-file-output-binding"></a><span data-ttu-id="d7da5-197">Выходная привязка внешнего файла</span><span class="sxs-lookup"><span data-stu-id="d7da5-197">External File output binding</span></span>
<span data-ttu-id="d7da5-198">Hello Azure внешний файл вывода привязка позволяет toowrite tooan внешних папку с файлами в функции.</span><span class="sxs-lookup"><span data-stu-id="d7da5-198">hello Azure external file output binding enables you toowrite files tooan external folder in your function.</span></span>

<span data-ttu-id="d7da5-199">выходные данные для функции используются следующие объекты JSON в hello hello внешнего файла Hello `bindings` массив function.json:</span><span class="sxs-lookup"><span data-stu-id="d7da5-199">hello external file output for a function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of output parameter in function signature>",
  "type": "apiHubFile",
  "direction": "out",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
}
```

<span data-ttu-id="d7da5-200">Обратите внимание hello следующие:</span><span class="sxs-lookup"><span data-stu-id="d7da5-200">Note hello following:</span></span>

* <span data-ttu-id="d7da5-201">`path`должен содержать имя папки hello и hello toowrite имя файла для.</span><span class="sxs-lookup"><span data-stu-id="d7da5-201">`path` must contain hello folder name and hello file name toowrite to.</span></span> <span data-ttu-id="d7da5-202">Например, если у вас есть [очереди триггера](functions-bindings-storage-queue.md) в функции, можно использовать `"path": "samples-workitems/{queueTrigger}"` toopoint tooa файла в hello `samples-workitems` папки с именем, совпадающим с именем hello файл, указанный в сообщении hello триггера.</span><span class="sxs-lookup"><span data-stu-id="d7da5-202">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` toopoint tooa file in hello `samples-workitems` folder with a name that matches hello file name specified in hello trigger message.</span></span>   

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="d7da5-203">Использование выходной привязки</span><span class="sxs-lookup"><span data-stu-id="d7da5-203">Output usage</span></span>
<span data-ttu-id="d7da5-204">В C# функции, можно привязать toohello выходной файл с помощью hello с именем `out` параметра в подписи функции, такие как `out <T> <name>`, где `T` имеет тип данных hello нужных данных tooserialize hello в, и `paramName` является hello имя указанный в [привязка для вывода](#output).</span><span class="sxs-lookup"><span data-stu-id="d7da5-204">In C# functions, you bind toohello output file by using hello named `out` parameter in your function signature, like `out <T> <name>`, where `T` is hello data type that you want tooserialize hello data into, and `paramName` is hello name you specified in the [output binding](#output).</span></span> <span data-ttu-id="d7da5-205">В функции Node.js, доступ к hello выходной файл с помощью `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="d7da5-205">In Node.js functions, you access hello output file using `context.bindings.<name>`.</span></span>

<span data-ttu-id="d7da5-206">Можно написать toohello выходной файл с помощью любого hello следующие типы:</span><span class="sxs-lookup"><span data-stu-id="d7da5-206">You can write toohello output file using any of hello following types:</span></span>

* <span data-ttu-id="d7da5-207">Любой [объект](https://msdn.microsoft.com/library/system.object.aspx) используется для сериализации JSON.</span><span class="sxs-lookup"><span data-stu-id="d7da5-207">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialization.</span></span>
  <span data-ttu-id="d7da5-208">При объявлении типа настраиваемые выходные данные (например `out OutputType paramName`), функции Azure пытается tooserialize объекта в JSON.</span><span class="sxs-lookup"><span data-stu-id="d7da5-208">If you declare a custom output type (e.g. `out OutputType paramName`), Azure Functions attempts tooserialize object into JSON.</span></span> <span data-ttu-id="d7da5-209">Если hello выходной параметр имеет значение null, при выходе из функции hello, среда выполнения функции hello создает файл как объект null.</span><span class="sxs-lookup"><span data-stu-id="d7da5-209">If hello output parameter is null when hello function exits, hello Functions runtime creates a file as a null object.</span></span>
* <span data-ttu-id="d7da5-210">Строка - (`out string paramName`) используется для текстовых данных файла.</span><span class="sxs-lookup"><span data-stu-id="d7da5-210">String - (`out string paramName`) useful for text file data.</span></span> <span data-ttu-id="d7da5-211">Среда выполнения функции Hello создает файл только в том случае, если параметр строки не равно null, при выходе из функции hello.</span><span class="sxs-lookup"><span data-stu-id="d7da5-211">hello Functions runtime creates a file only if the string parameter is non-null when hello function exits.</span></span>

<span data-ttu-id="d7da5-212">В C# функции также могут выводиться tooany из hello следующие типы:</span><span class="sxs-lookup"><span data-stu-id="d7da5-212">In C# functions you can also output tooany of hello following types:</span></span>

* `TextWriter`
* `Stream`
* `CloudFileStream`
* `ICloudFile`
* `CloudBlockFile`
* `CloudPageFile`

<a name="outputsample"></a>

<a name="sample"></a>

## <a name="input--output-sample"></a><span data-ttu-id="d7da5-213">Пример входных и выходных данных</span><span class="sxs-lookup"><span data-stu-id="d7da5-213">Input + Output sample</span></span>
<span data-ttu-id="d7da5-214">Предположим, что имеется следующая function.json hello, определяющий [хранилища очереди триггера](functions-bindings-storage-queue.md)внешнего файла ввода и вывода во внешний файл:</span><span class="sxs-lookup"><span data-stu-id="d7da5-214">Suppose you have hello following function.json, that defines a [Storage queue trigger](functions-bindings-storage-queue.md), an external file input, and an external file output:</span></span>

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

<span data-ttu-id="d7da5-215">См. пример hello зависящие от языка, который копирует hello входной файл toohello выходного файла.</span><span class="sxs-lookup"><span data-stu-id="d7da5-215">See hello language-specific sample that copies hello input file toohello output file.</span></span>

* [<span data-ttu-id="d7da5-216">C#</span><span class="sxs-lookup"><span data-stu-id="d7da5-216">C#</span></span>](#incsharp)
* [<span data-ttu-id="d7da5-217">Node.js</span><span class="sxs-lookup"><span data-stu-id="d7da5-217">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="usage-in-c"></a><span data-ttu-id="d7da5-218">Использование в языке C#</span><span class="sxs-lookup"><span data-stu-id="d7da5-218">Usage in C#</span></span> #

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

### <a name="usage-in-nodejs"></a><span data-ttu-id="d7da5-219">Использование для Node.js</span><span class="sxs-lookup"><span data-stu-id="d7da5-219">Usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="d7da5-220">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d7da5-220">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
