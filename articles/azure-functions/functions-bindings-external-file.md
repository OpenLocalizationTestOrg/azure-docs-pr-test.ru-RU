---
title: "Привязки внешних файлов в Функциях Azure (предварительная версия) | Документация Майкрософт"
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
ms.openlocfilehash: 2082e4e9b23271be93f3e3ab43997c3243238da8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-functions-external-file-bindings-preview"></a><span data-ttu-id="e3650-103">Привязки внешних файлов в Функциях Azure (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="e3650-103">Azure Functions External File bindings (Preview)</span></span>
<span data-ttu-id="e3650-104">В этой статье показано, как управлять файлами различных поставщиков SaaS (например, OneDrive, Dropbox) внутри функции, использующей встроенные привязки.</span><span class="sxs-lookup"><span data-stu-id="e3650-104">This article shows how to manipulate files from different SaaS providers (e.g. OneDrive, Dropbox) within your function utilizing built-in bindings.</span></span> <span data-ttu-id="e3650-105">Функции Azure поддерживают привязки триггера, а также входные и выходные привязки для внешних файлов.</span><span class="sxs-lookup"><span data-stu-id="e3650-105">Azure functions supports trigger, input, and output bindings for external file.</span></span>

<span data-ttu-id="e3650-106">Привязка создает подключения API к поставщикам SaaS или использует существующие подключения API из группы ресурсов приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="e3650-106">This binding creates API connections to SaaS providers, or uses existing API connections from your Function App's resource group.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="supported-file-connections"></a><span data-ttu-id="e3650-107">Поддерживаемые подключения файлов</span><span class="sxs-lookup"><span data-stu-id="e3650-107">Supported File connections</span></span>

|<span data-ttu-id="e3650-108">Соединитель</span><span class="sxs-lookup"><span data-stu-id="e3650-108">Connector</span></span>|<span data-ttu-id="e3650-109">Триггер</span><span class="sxs-lookup"><span data-stu-id="e3650-109">Trigger</span></span>|<span data-ttu-id="e3650-110">Входные данные</span><span class="sxs-lookup"><span data-stu-id="e3650-110">Input</span></span>|<span data-ttu-id="e3650-111">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="e3650-111">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="e3650-112">Box</span><span class="sxs-lookup"><span data-stu-id="e3650-112">Box</span></span>](https://www.box.com)|<span data-ttu-id="e3650-113">x</span><span class="sxs-lookup"><span data-stu-id="e3650-113">x</span></span>|<span data-ttu-id="e3650-114">x</span><span class="sxs-lookup"><span data-stu-id="e3650-114">x</span></span>|<span data-ttu-id="e3650-115">x</span><span class="sxs-lookup"><span data-stu-id="e3650-115">x</span></span>
|[<span data-ttu-id="e3650-116">Dropbox</span><span class="sxs-lookup"><span data-stu-id="e3650-116">Dropbox</span></span>](https://www.dropbox.com)|<span data-ttu-id="e3650-117">x</span><span class="sxs-lookup"><span data-stu-id="e3650-117">x</span></span>|<span data-ttu-id="e3650-118">x</span><span class="sxs-lookup"><span data-stu-id="e3650-118">x</span></span>|<span data-ttu-id="e3650-119">x</span><span class="sxs-lookup"><span data-stu-id="e3650-119">x</span></span>
|[<span data-ttu-id="e3650-120">FTP</span><span class="sxs-lookup"><span data-stu-id="e3650-120">FTP</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp)|<span data-ttu-id="e3650-121">x</span><span class="sxs-lookup"><span data-stu-id="e3650-121">x</span></span>|<span data-ttu-id="e3650-122">x</span><span class="sxs-lookup"><span data-stu-id="e3650-122">x</span></span>|<span data-ttu-id="e3650-123">x</span><span class="sxs-lookup"><span data-stu-id="e3650-123">x</span></span>
|[<span data-ttu-id="e3650-124">OneDrive</span><span class="sxs-lookup"><span data-stu-id="e3650-124">OneDrive</span></span>](https://onedrive.live.com)|<span data-ttu-id="e3650-125">x</span><span class="sxs-lookup"><span data-stu-id="e3650-125">x</span></span>|<span data-ttu-id="e3650-126">x</span><span class="sxs-lookup"><span data-stu-id="e3650-126">x</span></span>|<span data-ttu-id="e3650-127">x</span><span class="sxs-lookup"><span data-stu-id="e3650-127">x</span></span>
|[<span data-ttu-id="e3650-128">OneDrive для бизнеса</span><span class="sxs-lookup"><span data-stu-id="e3650-128">OneDrive for Business</span></span>](https://onedrive.live.com/about/business/)|<span data-ttu-id="e3650-129">x</span><span class="sxs-lookup"><span data-stu-id="e3650-129">x</span></span>|<span data-ttu-id="e3650-130">x</span><span class="sxs-lookup"><span data-stu-id="e3650-130">x</span></span>|<span data-ttu-id="e3650-131">x</span><span class="sxs-lookup"><span data-stu-id="e3650-131">x</span></span>
|[<span data-ttu-id="e3650-132">SFTP</span><span class="sxs-lookup"><span data-stu-id="e3650-132">SFTP</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sftp)|<span data-ttu-id="e3650-133">x</span><span class="sxs-lookup"><span data-stu-id="e3650-133">x</span></span>|<span data-ttu-id="e3650-134">x</span><span class="sxs-lookup"><span data-stu-id="e3650-134">x</span></span>|<span data-ttu-id="e3650-135">x</span><span class="sxs-lookup"><span data-stu-id="e3650-135">x</span></span>
|[<span data-ttu-id="e3650-136">Диск Google</span><span class="sxs-lookup"><span data-stu-id="e3650-136">Google Drive</span></span>](https://www.google.com/drive/)||<span data-ttu-id="e3650-137">x</span><span class="sxs-lookup"><span data-stu-id="e3650-137">x</span></span>|<span data-ttu-id="e3650-138">x</span><span class="sxs-lookup"><span data-stu-id="e3650-138">x</span></span>|

> [!NOTE]
> <span data-ttu-id="e3650-139">В [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list) могут также использоваться подключения к внешним файлам.</span><span class="sxs-lookup"><span data-stu-id="e3650-139">External File connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

## <a name="external-file-trigger-binding"></a><span data-ttu-id="e3650-140">Привязка триггера внешнего файла</span><span class="sxs-lookup"><span data-stu-id="e3650-140">External File trigger binding</span></span>

<span data-ttu-id="e3650-141">Триггер внешнего файла Azure позволяет отслеживать удаленную папку и выполнять код функции при обнаружении изменений.</span><span class="sxs-lookup"><span data-stu-id="e3650-141">The Azure external file trigger lets you monitor a remote folder and run your function code when changes are detected.</span></span>

<span data-ttu-id="e3650-142">Триггер внешнего файла использует следующий объект JSON в массиве `bindings` файла function.json.</span><span class="sxs-lookup"><span data-stu-id="e3650-142">The external file trigger uses the following JSON objects in the `bindings` array of function.json</span></span>

```json
{
  "type": "apiHubFileTrigger",
  "name": "<Name of input parameter in function signature>",
  "direction": "in",
  "path": "<folder to monitor, and optionally a name pattern - see below>",
  "connection": "<name of external file connection - see above>"
}
```
<!---
See one of the following subheadings for more information:

* [Name patterns](#pattern)
* [File receipts](#receipts)
* [Handling poison files](#poison)
--->

<a name="pattern"></a>

### <a name="name-patterns"></a><span data-ttu-id="e3650-143">Шаблоны имен</span><span class="sxs-lookup"><span data-stu-id="e3650-143">Name patterns</span></span>
<span data-ttu-id="e3650-144">Шаблон имени файла можно указать в свойстве `path`.</span><span class="sxs-lookup"><span data-stu-id="e3650-144">You can specify a file name pattern in the `path` property.</span></span> <span data-ttu-id="e3650-145">Указанная папка должна существовать в поставщике SaaS.</span><span class="sxs-lookup"><span data-stu-id="e3650-145">The folder referenced must exist in the SaaS provider.</span></span>
<span data-ttu-id="e3650-146">Примеры:</span><span class="sxs-lookup"><span data-stu-id="e3650-146">Examples:</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="e3650-147">При использовании этого пути будет выполняться поиск файла с именем *original-File1.txt* в папке *input*. В этом примере переменная `name` в коде функции получит значение `File1.txt`.</span><span class="sxs-lookup"><span data-stu-id="e3650-147">This path would find a file named *original-File1.txt* in the *input* folder, and the value of the `name` variable in function code would be `File1.txt`.</span></span>

<span data-ttu-id="e3650-148">Другой пример:</span><span class="sxs-lookup"><span data-stu-id="e3650-148">Another example:</span></span>

```json
"path": "input/{filename}.{fileextension}",
```

<span data-ttu-id="e3650-149">При использовании этого пути также будет выполняться поиск с именем *original-File1.txt*, но в код функции будут переданы другие переменные: `filename` и `fileextension` со значениями *original-File1* и *txt* соответственно.</span><span class="sxs-lookup"><span data-stu-id="e3650-149">This path would also find a file named *original-File1.txt*, and the value of the `filename` and `fileextension` variables in function code would be *original-File1* and *txt*.</span></span>

<span data-ttu-id="e3650-150">Тип файлов можно ограничить, используя фиксированное значение для расширения файла.</span><span class="sxs-lookup"><span data-stu-id="e3650-150">You can restrict the file type of files by using a fixed value for the file extension.</span></span> <span data-ttu-id="e3650-151">Например:</span><span class="sxs-lookup"><span data-stu-id="e3650-151">For example:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="e3650-152">В этом случае функцию активируют только файлы в формате *PNG* в папке *samples*.</span><span class="sxs-lookup"><span data-stu-id="e3650-152">In this case, only *.png* files in the *samples* folder trigger the function.</span></span>

<span data-ttu-id="e3650-153">Фигурные скобки используются в качестве специальных символов в шаблонах имен.</span><span class="sxs-lookup"><span data-stu-id="e3650-153">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="e3650-154">Чтобы использовать в именах файлов фигурные скобки, нужно добавить две фигурные скобки вместо одной.</span><span class="sxs-lookup"><span data-stu-id="e3650-154">To specify file names that have curly braces in the name, double the curly braces.</span></span>
<span data-ttu-id="e3650-155">Например:</span><span class="sxs-lookup"><span data-stu-id="e3650-155">For example:</span></span>

```json
"path": "images/{{20140101}}-{name}",
```

<span data-ttu-id="e3650-156">При использовании этого пути будет выполняться поиск файла с именем *{20140101}-soundfile.mp3* в папке *images*, а для переменной `name` в коде функции будет задано значение *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="e3650-156">This path would find a file named *{20140101}-soundfile.mp3* in the *images* folder, and the `name` variable value in the function code would be *soundfile.mp3*.</span></span>

<a name="receipts"></a>

<!--- ### File receipts
The Azure Functions runtime makes sure that no external file trigger function gets called more than once for the same new or updated file.
It does so by maintaining *file receipts* to determine if a given file version has been processed.

File receipts are stored in a folder named *azure-webjobs-hosts* in the Azure storage account for your function app
(specified by the `AzureWebJobsStorage` app setting). A file receipt has the following information:

* The triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "functionsf74b96f7.Functions.CopyFile")
* The folder name
* The file type ("BlockFile" or "PageFile")
* The file name
* The ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")

To force reprocessing of a file, delete the file receipt for that file from the *azure-webjobs-hosts* folder manually.
--->
<a name="poison"></a>

### <a name="handling-poison-files"></a><span data-ttu-id="e3650-157">Обработка подозрительных файлов</span><span class="sxs-lookup"><span data-stu-id="e3650-157">Handling poison files</span></span>
<span data-ttu-id="e3650-158">При сбое функции триггера внешнего файла по умолчанию Функции Azure выполняют ее для заданного файла еще 5 раз (включая первую попытку).</span><span class="sxs-lookup"><span data-stu-id="e3650-158">When an external file trigger function fails, Azure Functions retries that function up to 5 times by default (including the first try) for a given file.</span></span>
<span data-ttu-id="e3650-159">В случае сбоя после 5 попыток запуска Функции добавляют сообщение в очередь службы хранилища с именем *webjobs-apihubtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="e3650-159">If all 5 tries fail, Functions adds a message to a Storage queue named *webjobs-apihubtrigger-poison*.</span></span> <span data-ttu-id="e3650-160">Сообщением очереди для подозрительных файлов является объект JSON, содержащий следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="e3650-160">The queue message for poison files is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="e3650-161">FunctionId (идентификатор функции в формате *&lt;имя_приложения-функции>*.Functions.*&lt;имя_функции>*);</span><span class="sxs-lookup"><span data-stu-id="e3650-161">FunctionId (in the format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="e3650-162">FileType</span><span class="sxs-lookup"><span data-stu-id="e3650-162">FileType</span></span>
* <span data-ttu-id="e3650-163">FolderName</span><span class="sxs-lookup"><span data-stu-id="e3650-163">FolderName</span></span>
* <span data-ttu-id="e3650-164">FileName</span><span class="sxs-lookup"><span data-stu-id="e3650-164">FileName</span></span>
* <span data-ttu-id="e3650-165">ETag (идентификатор версии файла, например 0x8D1DC6E70A277EF)</span><span class="sxs-lookup"><span data-stu-id="e3650-165">ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")</span></span>


<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="e3650-166">Использование триггера</span><span class="sxs-lookup"><span data-stu-id="e3650-166">Trigger usage</span></span>
<span data-ttu-id="e3650-167">В функциях C# можно выполнить привязку к данным входного файла, используя именованный параметр в сигнатуре функции, например `<T> <name>`,</span><span class="sxs-lookup"><span data-stu-id="e3650-167">In C# functions, you bind to the input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="e3650-168">где `T` — это тип данных, в который требуется десериализировать данные, а `paramName` — это имя, указанное в [JSON триггера](#trigger).</span><span class="sxs-lookup"><span data-stu-id="e3650-168">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [trigger JSON](#trigger).</span></span> <span data-ttu-id="e3650-169">В функциях Node.js доступ к данным входного файла можно получить, используя `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="e3650-169">In Node.js functions, you access the input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="e3650-170">Файл можно десериализировать в один из следующих типов:</span><span class="sxs-lookup"><span data-stu-id="e3650-170">The file can be deserialized into any of the following types:</span></span>

* <span data-ttu-id="e3650-171">Любой [объект](https://msdn.microsoft.com/library/system.object.aspx) используется для сериализованных данных JSON файла.</span><span class="sxs-lookup"><span data-stu-id="e3650-171">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="e3650-172">Если объявить пользовательский входной тип (например, `FooType`), Функции Azure попытаются десериализировать данные JSON в указанный тип.</span><span class="sxs-lookup"><span data-stu-id="e3650-172">If you declare a custom input type (e.g. `FooType`), Azure Functions attempts to deserialize the JSON data into your specified type.</span></span>
* <span data-ttu-id="e3650-173">Строка - используется для текстовых данных файла.</span><span class="sxs-lookup"><span data-stu-id="e3650-173">String - useful for text file data.</span></span>

<span data-ttu-id="e3650-174">В функциях C# также можно выполнить привязку к любому из следующих типов. Среда выполнения Функций попытается десериализировать данные файла, используя этот тип:</span><span class="sxs-lookup"><span data-stu-id="e3650-174">In C# functions, you can also bind to any of the following types, and the Functions runtime attempts to deserialize the file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`

## <a name="trigger-sample"></a><span data-ttu-id="e3650-175">Пример триггера</span><span class="sxs-lookup"><span data-stu-id="e3650-175">Trigger sample</span></span>
<span data-ttu-id="e3650-176">Предположим, что у вас есть следующий файл function.json, определяющий триггер внешнего файла:</span><span class="sxs-lookup"><span data-stu-id="e3650-176">Suppose you have the following function.json, that defines an external file trigger:</span></span>

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

<span data-ttu-id="e3650-177">Ознакомьтесь с примером для конкретного языка, регистрирующим содержимое каждого файла, который добавляется в отслеживаемую папку.</span><span class="sxs-lookup"><span data-stu-id="e3650-177">See the language-specific sample that logs the contents of each file that is added to the monitored folder.</span></span>

* [<span data-ttu-id="e3650-178">C#</span><span class="sxs-lookup"><span data-stu-id="e3650-178">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="e3650-179">Node.js</span><span class="sxs-lookup"><span data-stu-id="e3650-179">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-usage-in-c"></a><span data-ttu-id="e3650-180">Использование триггера на языке C#</span><span class="sxs-lookup"><span data-stu-id="e3650-180">Trigger usage in C#</span></span> #

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

### <a name="trigger-usage-in-nodejs"></a><span data-ttu-id="e3650-181">Использование триггера для Node.js</span><span class="sxs-lookup"><span data-stu-id="e3650-181">Trigger usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js File trigger function processed', context.bindings.myFile);
    context.done();
};
```

<a name="input"></a>

## <a name="external-file-input-binding"></a><span data-ttu-id="e3650-182">Входная привязка внешнего файла</span><span class="sxs-lookup"><span data-stu-id="e3650-182">External File input binding</span></span>
<span data-ttu-id="e3650-183">Входная привязка внешнего файла Azure позволяет использовать файл из внешней папки в функции.</span><span class="sxs-lookup"><span data-stu-id="e3650-183">The Azure external file input binding enables you to use a file from an external folder in your function.</span></span>

<span data-ttu-id="e3650-184">Входные данные внешнего файла для функции используют следующий объект JSON в массиве `bindings` файла function.json:</span><span class="sxs-lookup"><span data-stu-id="e3650-184">The external file input to a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of input parameter in function signature>",
  "type": "apiHubFile",
  "direction": "in",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
},
```

<span data-ttu-id="e3650-185">Обратите внимание на следующее.</span><span class="sxs-lookup"><span data-stu-id="e3650-185">Note the following:</span></span>

* <span data-ttu-id="e3650-186">Значение `path` должно содержать имя папки и имя файла.</span><span class="sxs-lookup"><span data-stu-id="e3650-186">`path` must contain the folder name and the file name.</span></span> <span data-ttu-id="e3650-187">Например, если в вашей функции есть [триггер очереди](functions-bindings-storage-queue.md), можно использовать `"path": "samples-workitems/{queueTrigger}"`, чтобы указать на файл в папке `samples-workitems` с именем, которое соответствует имени файла, определенного в сообщении триггера.</span><span class="sxs-lookup"><span data-stu-id="e3650-187">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` to point to a file in the `samples-workitems` folder with a name that matches the file name specified in the trigger message.</span></span>   

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="e3650-188">Использование входной привязки</span><span class="sxs-lookup"><span data-stu-id="e3650-188">Input usage</span></span>
<span data-ttu-id="e3650-189">В функциях C# можно выполнить привязку к данным входного файла, используя именованный параметр в сигнатуре функции, например `<T> <name>`,</span><span class="sxs-lookup"><span data-stu-id="e3650-189">In C# functions, you bind to the input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="e3650-190">где `T` — это тип данных, в который требуется десериализировать данные, а `paramName` — это имя, указанное во [входной привязке](#input).</span><span class="sxs-lookup"><span data-stu-id="e3650-190">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [input binding](#input).</span></span> <span data-ttu-id="e3650-191">В функциях Node.js доступ к данным входного файла можно получить, используя `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="e3650-191">In Node.js functions, you access the input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="e3650-192">Файл можно десериализировать в один из следующих типов:</span><span class="sxs-lookup"><span data-stu-id="e3650-192">The file can be deserialized into any of the following types:</span></span>

* <span data-ttu-id="e3650-193">Любой [объект](https://msdn.microsoft.com/library/system.object.aspx) используется для сериализованных данных JSON файла.</span><span class="sxs-lookup"><span data-stu-id="e3650-193">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="e3650-194">Если объявить пользовательский входной тип (например, `InputType`), Функции Azure попытаются десериализировать данные JSON в указанный тип.</span><span class="sxs-lookup"><span data-stu-id="e3650-194">If you declare a custom input type (e.g. `InputType`), Azure Functions attempts to deserialize the JSON data into your specified type.</span></span>
* <span data-ttu-id="e3650-195">Строка - используется для текстовых данных файла.</span><span class="sxs-lookup"><span data-stu-id="e3650-195">String - useful for text file data.</span></span>

<span data-ttu-id="e3650-196">В функциях C# также можно выполнить привязку к любому из следующих типов. Среда выполнения Функций попытается десериализировать данные файла, используя этот тип:</span><span class="sxs-lookup"><span data-stu-id="e3650-196">In C# functions, you can also bind to any of the following types, and the Functions runtime attempts to deserialize the file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`


<a name="output"></a>

## <a name="external-file-output-binding"></a><span data-ttu-id="e3650-197">Выходная привязка внешнего файла</span><span class="sxs-lookup"><span data-stu-id="e3650-197">External File output binding</span></span>
<span data-ttu-id="e3650-198">Выходная привязка внешнего файла Azure позволяет записывать файлы во внешнюю папку в функции.</span><span class="sxs-lookup"><span data-stu-id="e3650-198">The Azure external file output binding enables you to write files to an external folder in your function.</span></span>

<span data-ttu-id="e3650-199">Выходные данные внешнего файла для функции используют следующий объект JSON в массиве `bindings` файла function.json:</span><span class="sxs-lookup"><span data-stu-id="e3650-199">The external file output for a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of output parameter in function signature>",
  "type": "apiHubFile",
  "direction": "out",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
}
```

<span data-ttu-id="e3650-200">Обратите внимание на следующее.</span><span class="sxs-lookup"><span data-stu-id="e3650-200">Note the following:</span></span>

* <span data-ttu-id="e3650-201">Значение `path` должно содержать имя папки и имя файла, в который выполняется запись.</span><span class="sxs-lookup"><span data-stu-id="e3650-201">`path` must contain the folder name and the file name to write to.</span></span> <span data-ttu-id="e3650-202">Например, если в вашей функции есть [триггер очереди](functions-bindings-storage-queue.md), можно использовать `"path": "samples-workitems/{queueTrigger}"`, чтобы указать на файл в папке `samples-workitems` с именем, которое соответствует имени файла, определенного в сообщении триггера.</span><span class="sxs-lookup"><span data-stu-id="e3650-202">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` to point to a file in the `samples-workitems` folder with a name that matches the file name specified in the trigger message.</span></span>   

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="e3650-203">Использование выходной привязки</span><span class="sxs-lookup"><span data-stu-id="e3650-203">Output usage</span></span>
<span data-ttu-id="e3650-204">В функциях C# можно выполнить привязку к выходному файлу, используя именованный параметр `out` в сигнатуре функции, например `out <T> <name>`, где `T` — это тип данных, в который нужно сериализовать данные, а `paramName` — это имя, указанное в [выходной привязке](#output).</span><span class="sxs-lookup"><span data-stu-id="e3650-204">In C# functions, you bind to the output file by using the named `out` parameter in your function signature, like `out <T> <name>`, where `T` is the data type that you want to serialize the data into, and `paramName` is the name you specified in the [output binding](#output).</span></span> <span data-ttu-id="e3650-205">В функциях Node.js доступ к выходному файлу можно получить, используя `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="e3650-205">In Node.js functions, you access the output file using `context.bindings.<name>`.</span></span>

<span data-ttu-id="e3650-206">Запись в выходной файл можно выполнить, используя любой из следующих типов:</span><span class="sxs-lookup"><span data-stu-id="e3650-206">You can write to the output file using any of the following types:</span></span>

* <span data-ttu-id="e3650-207">Любой [объект](https://msdn.microsoft.com/library/system.object.aspx) используется для сериализации JSON.</span><span class="sxs-lookup"><span data-stu-id="e3650-207">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialization.</span></span>
  <span data-ttu-id="e3650-208">Если объявить пользовательский выходной тип (например, `out OutputType paramName`), Функции Azure попытаются сериализовать объект в JSON.</span><span class="sxs-lookup"><span data-stu-id="e3650-208">If you declare a custom output type (e.g. `out OutputType paramName`), Azure Functions attempts to serialize object into JSON.</span></span> <span data-ttu-id="e3650-209">Если при выходе из функции выходной параметр имеет значение null, среда выполнения Функций создает файл в качестве пустого объекта.</span><span class="sxs-lookup"><span data-stu-id="e3650-209">If the output parameter is null when the function exits, the Functions runtime creates a file as a null object.</span></span>
* <span data-ttu-id="e3650-210">Строка - (`out string paramName`) используется для текстовых данных файла.</span><span class="sxs-lookup"><span data-stu-id="e3650-210">String - (`out string paramName`) useful for text file data.</span></span> <span data-ttu-id="e3650-211">Среда выполнения Функций создает файл, только если при выходе из функции для параметра строки не задано значение null.</span><span class="sxs-lookup"><span data-stu-id="e3650-211">the Functions runtime creates a file only if the string parameter is non-null when the function exits.</span></span>

<span data-ttu-id="e3650-212">В функциях C# можно выполнить вывод одного из следующих типов:</span><span class="sxs-lookup"><span data-stu-id="e3650-212">In C# functions you can also output to any of the following types:</span></span>

* `TextWriter`
* `Stream`
* `CloudFileStream`
* `ICloudFile`
* `CloudBlockFile`
* `CloudPageFile`

<a name="outputsample"></a>

<a name="sample"></a>

## <a name="input--output-sample"></a><span data-ttu-id="e3650-213">Пример входных и выходных данных</span><span class="sxs-lookup"><span data-stu-id="e3650-213">Input + Output sample</span></span>
<span data-ttu-id="e3650-214">Предположим, у вас есть следующий файл function.json, определяющий [триггер очереди службы хранилища](functions-bindings-storage-queue.md), а также входные и выходные данные внешнего файла:</span><span class="sxs-lookup"><span data-stu-id="e3650-214">Suppose you have the following function.json, that defines a [Storage queue trigger](functions-bindings-storage-queue.md), an external file input, and an external file output:</span></span>

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

<span data-ttu-id="e3650-215">Ознакомьтесь с примером для конкретного языка, копирующим входной файл в выходной.</span><span class="sxs-lookup"><span data-stu-id="e3650-215">See the language-specific sample that copies the input file to the output file.</span></span>

* [<span data-ttu-id="e3650-216">C#</span><span class="sxs-lookup"><span data-stu-id="e3650-216">C#</span></span>](#incsharp)
* [<span data-ttu-id="e3650-217">Node.js</span><span class="sxs-lookup"><span data-stu-id="e3650-217">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="usage-in-c"></a><span data-ttu-id="e3650-218">Использование в языке C#</span><span class="sxs-lookup"><span data-stu-id="e3650-218">Usage in C#</span></span> #

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

### <a name="usage-in-nodejs"></a><span data-ttu-id="e3650-219">Использование для Node.js</span><span class="sxs-lookup"><span data-stu-id="e3650-219">Usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="e3650-220">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e3650-220">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
