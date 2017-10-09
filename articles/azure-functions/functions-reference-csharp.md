---
title: "Справочник разработчика скрипт C# функции aaaAzure | Документы Microsoft"
description: "Понять, как toodevelop функции Azure с помощью C#."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "функции azure, функции, обработка событий, веб-перехватчики, динамические вычисления, независимая архитектура"
ms.assetid: f28cda01-15f3-4047-83f3-e89d5728301c
ms.service: functions
ms.devlang: dotnet
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/07/2017
ms.author: donnam
ms.openlocfilehash: 27a8f4eb77497a373ff4031539e2e930585e48e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-c-script-developer-reference"></a><span data-ttu-id="40486-104">Справочник разработчика скриптов C# по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="40486-104">Azure Functions C# script developer reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="40486-105">Сценарий C#</span><span class="sxs-lookup"><span data-stu-id="40486-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="40486-106">Скрипт F#</span><span class="sxs-lookup"><span data-stu-id="40486-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="40486-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="40486-107">Node.js</span></span>](functions-reference-node.md)
>
>

<span data-ttu-id="40486-108">Hello качества скрипт C# для функций Azure основан на hello Azure SDK веб-заданий.</span><span class="sxs-lookup"><span data-stu-id="40486-108">hello C# script experience for Azure Functions is based on hello Azure WebJobs SDK.</span></span> <span data-ttu-id="40486-109">Данные поступают в функцию C# через аргументы метода.</span><span class="sxs-lookup"><span data-stu-id="40486-109">Data flows into your C# function via method arguments.</span></span> <span data-ttu-id="40486-110">Указанные имена аргументов в `function.json`, и предварительно определенных имен для доступа к, например hello функции ведения журнала и токены отмены.</span><span class="sxs-lookup"><span data-stu-id="40486-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like hello function logger and cancellation tokens.</span></span>

<span data-ttu-id="40486-111">В этой статье предполагается, что вы прочитали hello [Справочник разработчика Azure функции](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="40486-111">This article assumes that you've already read hello [Azure Functions developer reference](functions-reference.md).</span></span>

<span data-ttu-id="40486-112">Дополнительные сведения об использовании библиотек классов C# с помощью Функций Azure см. в [этой статье](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="40486-112">For information on using C# class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span>

## <a name="how-csx-works"></a><span data-ttu-id="40486-113">Как работает формат CSX</span><span class="sxs-lookup"><span data-stu-id="40486-113">How .csx works</span></span>
<span data-ttu-id="40486-114">Hello `.csx` формат позволяет toowrite менее «стандартный» и сосредоточиться на запись только функции C#.</span><span class="sxs-lookup"><span data-stu-id="40486-114">hello `.csx` format allows you toowrite less "boilerplate" and focus on writing just a C# function.</span></span> <span data-ttu-id="40486-115">Включить все ссылки на сборки и пространства имен в начале файла hello hello обычным образом.</span><span class="sxs-lookup"><span data-stu-id="40486-115">Include any assembly references and namespaces at hello beginning of hello file as usual.</span></span> <span data-ttu-id="40486-116">а затем вместо помещения всего кода в пространство имен и класс просто определите метод `Run`.</span><span class="sxs-lookup"><span data-stu-id="40486-116">Instead of wrapping everything in a namespace and class, just define a `Run` method.</span></span> <span data-ttu-id="40486-117">Если вам требуется tooinclude всем классам для объектов объект среды CLR (POCO), можно включить класса внутри обычного toodefine экземпляр hello того же файла.</span><span class="sxs-lookup"><span data-stu-id="40486-117">If you need tooinclude any classes, for instance toodefine Plain Old CLR Object (POCO) objects, you can include a class inside hello same file.</span></span>   

## <a name="binding-tooarguments"></a><span data-ttu-id="40486-118">Tooarguments привязки</span><span class="sxs-lookup"><span data-stu-id="40486-118">Binding tooarguments</span></span>
<span data-ttu-id="40486-119">Hello различных привязок, связанных tooa C# функция через hello `name` свойство в hello *function.json* конфигурации.</span><span class="sxs-lookup"><span data-stu-id="40486-119">hello various bindings are bound tooa C# function via hello `name` property in hello *function.json* configuration.</span></span> <span data-ttu-id="40486-120">У каждой привязки есть собственные поддерживаемые типы. Например, триггер больших двоичных объектов может поддерживать строку, POCO или CloudBlockBlob.</span><span class="sxs-lookup"><span data-stu-id="40486-120">Each binding has its own supported types; for instance, a blob trigger can support a string, a POCO, or a CloudBlockBlob.</span></span> <span data-ttu-id="40486-121">Hello поддерживаемые типы описаны в hello справочник для каждой привязки.</span><span class="sxs-lookup"><span data-stu-id="40486-121">hello supported types are documented in hello reference for each binding.</span></span> <span data-ttu-id="40486-122">Для каждого свойства объекта POCO нужно определить метод задания и считывания.</span><span class="sxs-lookup"><span data-stu-id="40486-122">A POCO object must have a getter and setter defined for each property.</span></span>

```csharp
public static void Run(string myBlob, out MyClass myQueueItem)
{
    log.Verbose($"C# Blob trigger function processed: {myBlob}");
    myQueueItem = new MyClass() { Id = "myid" };
}

public class MyClass
{
    public string Id { get; set; }
}
```

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="using-method-return-value-for-output-binding"></a><span data-ttu-id="40486-123">Использование возвращаемого значения метода для выходной привязки</span><span class="sxs-lookup"><span data-stu-id="40486-123">Using method return value for output binding</span></span>

<span data-ttu-id="40486-124">Возвращаемое значение метода можно использовать для привязки выходные данные с помощью имени hello `$return` в *function.json*:</span><span class="sxs-lookup"><span data-stu-id="40486-124">You can use a method return value for an output binding, by using hello name `$return` in *function.json*:</span></span>

```json
{
    "type": "queue",
    "direction": "out",
    "name": "$return",
    "queueName": "outqueue",
    "connection": "MyStorageConnectionString",
}
```

```csharp
public static string Run(string input, TraceWriter log)
{
    return input;
}
```

## <a name="writing-multiple-output-values"></a><span data-ttu-id="40486-125">Написание нескольких значений выходных данных</span><span class="sxs-lookup"><span data-stu-id="40486-125">Writing multiple output values</span></span>

<span data-ttu-id="40486-126">Вывод нескольких значений tooan toowrite привязку, использовать hello [ `ICollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) или [ `IAsyncCollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) типов.</span><span class="sxs-lookup"><span data-stu-id="40486-126">toowrite multiple values tooan output binding, use hello [`ICollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [`IAsyncCollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) types.</span></span> <span data-ttu-id="40486-127">Эти типы предназначены только для записи коллекции, записать toohello выходные данные привязки завершении метода hello.</span><span class="sxs-lookup"><span data-stu-id="40486-127">These types are write-only collections that are written toohello output binding when hello method completes.</span></span>

<span data-ttu-id="40486-128">В следующем примере записываются несколько сообщений очереди с помощью `ICollector`:</span><span class="sxs-lookup"><span data-stu-id="40486-128">This example writes multiple queue messages using `ICollector`:</span></span>

```csharp
public static void Run(ICollector<string> myQueueItem, TraceWriter log)
{
    myQueueItem.Add("Hello");
    myQueueItem.Add("World!");
}
```

## <a name="logging"></a><span data-ttu-id="40486-129">Ведение журналов</span><span class="sxs-lookup"><span data-stu-id="40486-129">Logging</span></span>
<span data-ttu-id="40486-130">toolog выходные данные журналов потоковой передачи tooyour в C#, включите аргумент типа `TraceWriter`.</span><span class="sxs-lookup"><span data-stu-id="40486-130">toolog output tooyour streaming logs in C#, include an argument of type `TraceWriter`.</span></span> <span data-ttu-id="40486-131">Рекомендуем присвоить ему имя `log`.</span><span class="sxs-lookup"><span data-stu-id="40486-131">We recommend that you name it `log`.</span></span> <span data-ttu-id="40486-132">Не используйте `Console.Write` в Функциях Azure.</span><span class="sxs-lookup"><span data-stu-id="40486-132">Avoid using `Console.Write` in Azure Functions.</span></span> 

<span data-ttu-id="40486-133">`TraceWriter`определен в hello [SDK веб-заданий Azure](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span><span class="sxs-lookup"><span data-stu-id="40486-133">`TraceWriter` is defined in hello [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span></span> <span data-ttu-id="40486-134">Здравствуйте, уровень ведения журнала для `TraceWriter` можно настроить в [узла\.json].</span><span class="sxs-lookup"><span data-stu-id="40486-134">hello log level for `TraceWriter` can be configured in [host\.json].</span></span>

```csharp
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

## <a name="async"></a><span data-ttu-id="40486-135">Асинхронный режим</span><span class="sxs-lookup"><span data-stu-id="40486-135">Async</span></span>
<span data-ttu-id="40486-136">использовать toomake асинхронно, функции hello `async` ключевое слово и возврат `Task` объекта.</span><span class="sxs-lookup"><span data-stu-id="40486-136">toomake a function asynchronous, use hello `async` keyword and return a `Task` object.</span></span>

```csharp
public async static Task ProcessQueueMessageAsync(
        string blobName,
        Stream blobInput,
        Stream blobOutput)
{
    await blobInput.CopyToAsync(blobOutput, 4096, token);
}
```

## <a name="cancellation-token"></a><span data-ttu-id="40486-137">Токен отмены</span><span class="sxs-lookup"><span data-stu-id="40486-137">Cancellation Token</span></span>
<span data-ttu-id="40486-138">Для некоторых операций необходимо выполнить нормальное завершение работы.</span><span class="sxs-lookup"><span data-stu-id="40486-138">Some operations require graceful shutdown.</span></span> <span data-ttu-id="40486-139">Хотя всегда наиболее toowrite код, который может обрабатывать аварийное завершение работы, в случаях, где нужно toohandle нормальное завершение работы запросов, определить [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) типом аргумента.</span><span class="sxs-lookup"><span data-stu-id="40486-139">While it's always best toowrite code that can handle crashing,  in cases where you want toohandle graceful shutdown requests, you define a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) typed argument.</span></span>  <span data-ttu-id="40486-140">Объект `CancellationToken` предоставляется toosignal срабатывание завершение работы узла.</span><span class="sxs-lookup"><span data-stu-id="40486-140">A `CancellationToken` is provided toosignal that a host shutdown is triggered.</span></span>

```csharp
public async static Task ProcessQueueMessageAsyncCancellationToken(
        string blobName,
        Stream blobInput,
        Stream blobOutput,
        CancellationToken token)
    {
        await blobInput.CopyToAsync(blobOutput, 4096, token);
    }
```

## <a name="importing-namespaces"></a><span data-ttu-id="40486-141">Импорт пространств имен</span><span class="sxs-lookup"><span data-stu-id="40486-141">Importing namespaces</span></span>
<span data-ttu-id="40486-142">Если вам требуется tooimport пространства имен, это можно сделать как обычно с hello `using` предложения.</span><span class="sxs-lookup"><span data-stu-id="40486-142">If you need tooimport namespaces, you can do so as usual, with hello `using` clause.</span></span>

```csharp
using System.Net;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="40486-143">Hello следующие пространства имен автоматически импортируются и поэтому являются необязательными:</span><span class="sxs-lookup"><span data-stu-id="40486-143">hello following namespaces are automatically imported and are therefore optional:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`

## <a name="referencing-external-assemblies"></a><span data-ttu-id="40486-144">Ссылки на внешние сборки</span><span class="sxs-lookup"><span data-stu-id="40486-144">Referencing External Assemblies</span></span>
<span data-ttu-id="40486-145">Для сборок framework добавить ссылки с помощью hello `#r "AssemblyName"` директивы.</span><span class="sxs-lookup"><span data-stu-id="40486-145">For framework assemblies, add references by using hello `#r "AssemblyName"` directive.</span></span>

```csharp
#r "System.Web.Http"

using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="40486-146">Hello следующие сборки автоматически добавляются hello Azure функциями среды размещения.</span><span class="sxs-lookup"><span data-stu-id="40486-146">hello following assemblies are automatically added by hello Azure Functions hosting environment:</span></span>

* `mscorlib`
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* `System.Net.Http.Formatting`

<span data-ttu-id="40486-147">Hello следующие сборки может быть ссылается простое имя (например, `#r "AssemblyName"`):</span><span class="sxs-lookup"><span data-stu-id="40486-147">hello following assemblies may be referenced by simple-name (for example, `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNet.WebHooks.Common`
* `Microsoft.Azure.NotificationHubs`

## <a name="referencing-custom-assemblies"></a><span data-ttu-id="40486-148">Ссылки на пользовательские сборки</span><span class="sxs-lookup"><span data-stu-id="40486-148">Referencing custom assemblies</span></span>

<span data-ttu-id="40486-149">tooreference пользовательской сборки, можно использовать любой *общего* сборки или *закрытый* сборки:</span><span class="sxs-lookup"><span data-stu-id="40486-149">tooreference a custom assembly, you can use either a *shared* assembly or a *private* assembly:</span></span>
- <span data-ttu-id="40486-150">Общие сборки совместно используют все функции в приложении-функции.</span><span class="sxs-lookup"><span data-stu-id="40486-150">Shared assemblies are shared across all functions within a function app.</span></span> <span data-ttu-id="40486-151">tooreference пользовательской сборки, отправка hello сборки tooyour функции приложения, такие как в `bin` папки в корневом каталоге приложения функции hello.</span><span class="sxs-lookup"><span data-stu-id="40486-151">tooreference a custom assembly, upload hello assembly tooyour function app, such as in a `bin` folder in hello function app root.</span></span> 
- <span data-ttu-id="40486-152">Закрытые сборки входят в контекст указанной функции и поддерживают загрузку неопубликованных приложений разных версий.</span><span class="sxs-lookup"><span data-stu-id="40486-152">Private assemblies are part of a given function's context, and support side-loading of different versions.</span></span> <span data-ttu-id="40486-153">Закрытые сборки должны быть отправлены в `bin` папку в каталоге функции hello.</span><span class="sxs-lookup"><span data-stu-id="40486-153">Private assemblies should be uploaded in a `bin` folder in hello function directory.</span></span> <span data-ttu-id="40486-154">Ссылку можно с помощью имени файла hello, такие как `#r "MyAssembly.dll"`.</span><span class="sxs-lookup"><span data-stu-id="40486-154">Reference using hello file name, such as  `#r "MyAssembly.dll"`.</span></span> 

<span data-ttu-id="40486-155">Сведения о как tooyour функция папки с файлами tooupload hello в следующем разделе пакета управления см.</span><span class="sxs-lookup"><span data-stu-id="40486-155">For information on how tooupload files tooyour function folder, see hello following section on package management.</span></span>

### <a name="watched-directories"></a><span data-ttu-id="40486-156">Каталоги отслеживания</span><span class="sxs-lookup"><span data-stu-id="40486-156">Watched directories</span></span>

<span data-ttu-id="40486-157">tooassemblies изменения автоматически наступление Hello каталог, содержащий файл скрипта функции hello.</span><span class="sxs-lookup"><span data-stu-id="40486-157">hello directory that contains hello function script file is automatically watched for changes tooassemblies.</span></span> <span data-ttu-id="40486-158">toowatch изменить сборки в других каталогах, добавьте их toohello `watchDirectories` списка в [узла\.json].</span><span class="sxs-lookup"><span data-stu-id="40486-158">toowatch for assembly changes in other directories, add them toohello `watchDirectories` list in [host\.json].</span></span>

## <a name="using-nuget-packages"></a><span data-ttu-id="40486-159">Использование пакетов NuGet</span><span class="sxs-lookup"><span data-stu-id="40486-159">Using NuGet packages</span></span>
<span data-ttu-id="40486-160">отправить пакеты NuGet toouse в функции C# *project.json* toohello функция папка файла в файловой системе функция приложение hello.</span><span class="sxs-lookup"><span data-stu-id="40486-160">toouse NuGet packages in a C# function, upload a *project.json* file toohello function's folder in hello function app's file system.</span></span> <span data-ttu-id="40486-161">Ниже приведен пример *project.json* файл, который добавляет ссылку tooMicrosoft.ProjectOxford.Face версии 1.1.0:</span><span class="sxs-lookup"><span data-stu-id="40486-161">Here is an example *project.json* file that adds a reference tooMicrosoft.ProjectOxford.Face version 1.1.0:</span></span>

```json
{
  "frameworks": {
    "net46":{
      "dependencies": {
        "Microsoft.ProjectOxford.Face": "1.1.0"
      }
    }
   }
}
```

<span data-ttu-id="40486-162">Только для hello .NET Framework 4.6 поддерживается, поэтому убедитесь, что ваш *project.json* файл определяет `net46` как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="40486-162">Only hello .NET Framework 4.6 is supported, so make sure that your *project.json* file specifies `net46` as shown here.</span></span>

<span data-ttu-id="40486-163">При отправке *project.json* файла, hello среда выполнения получает пакеты hello и автоматически добавляет ссылки на toohello пакет сборки.</span><span class="sxs-lookup"><span data-stu-id="40486-163">When you upload a *project.json* file, hello runtime gets hello packages and automatically adds references toohello package assemblies.</span></span> <span data-ttu-id="40486-164">Не требуется tooadd `#r "AssemblyName"` директивы.</span><span class="sxs-lookup"><span data-stu-id="40486-164">You don't need tooadd `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="40486-165">toouse hello типы, определенные в пакетах NuGet hello, добавьте необходимые hello `using` tooyour инструкций *run.csx* файла</span><span class="sxs-lookup"><span data-stu-id="40486-165">toouse hello types defined in hello NuGet packages, add hello required `using` statements tooyour *run.csx* file</span></span> 

<span data-ttu-id="40486-166">В среде выполнения функции hello, восстановление NuGet работает путем сравнения `project.json` и `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="40486-166">In hello Functions runtime, NuGet restore works by comparing `project.json` and `project.lock.json`.</span></span> <span data-ttu-id="40486-167">Если дата и время создания файлов hello hello **не** совпадение, выполняется восстановление NuGet и NuGet загружает обновленные пакеты.</span><span class="sxs-lookup"><span data-stu-id="40486-167">If hello date and time stamps of hello files **do not** match, a NuGet restore runs and NuGet downloads updated packages.</span></span> <span data-ttu-id="40486-168">Тем не менее, если hello Дата и время создания файлов hello **сделать** соответствия NuGet не выполняет восстановление.</span><span class="sxs-lookup"><span data-stu-id="40486-168">However, if hello date and time stamps of hello files **do** match, NuGet does not perform a restore.</span></span> <span data-ttu-id="40486-169">Таким образом `project.lock.json` не следует развертывать как он вызывает восстановление пакета NuGet tooskip.</span><span class="sxs-lookup"><span data-stu-id="40486-169">Therefore, `project.lock.json` should not be deployed as it causes NuGet tooskip package restore.</span></span> <span data-ttu-id="40486-170">tooavoid развертывание hello блокировки файлов, добавьте hello `project.lock.json` toohello `.gitignore` файла.</span><span class="sxs-lookup"><span data-stu-id="40486-170">tooavoid deploying hello lock file, add hello `project.lock.json` toohello `.gitignore` file.</span></span>

<span data-ttu-id="40486-171">toouse настраиваемого канала NuGet, укажите hello веб-канала в *Nuget.Config* файл в корневом каталоге приложения функции hello.</span><span class="sxs-lookup"><span data-stu-id="40486-171">toouse a custom NuGet feed, specify hello feed in a *Nuget.Config* file in hello Function App root.</span></span> <span data-ttu-id="40486-172">Дополнительные сведения см. в статье [Configuring NuGet behavior](/nuget/consume-packages/configuring-nuget-behavior) (Настройка поведения NuGet).</span><span class="sxs-lookup"><span data-stu-id="40486-172">For more information, see [Configuring NuGet behavior](/nuget/consume-packages/configuring-nuget-behavior).</span></span>

### <a name="using-a-projectjson-file"></a><span data-ttu-id="40486-173">Использование файла project.json</span><span class="sxs-lookup"><span data-stu-id="40486-173">Using a project.json file</span></span>
1. <span data-ttu-id="40486-174">Откройте функции hello в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="40486-174">Open hello function in hello Azure portal.</span></span> <span data-ttu-id="40486-175">Hello заносит в журнал выходные данные установки пакета вкладка отображает hello.</span><span class="sxs-lookup"><span data-stu-id="40486-175">hello logs tab displays hello package installation output.</span></span>
2. <span data-ttu-id="40486-176">tooupload файл project.json, воспользуйтесь одним из описанных hello hello [как tooupdate функция файлов приложения](functions-reference.md#fileupdate) раздела Справочник разработчика Azure функции hello.</span><span class="sxs-lookup"><span data-stu-id="40486-176">tooupload a project.json file, use one of hello methods described in hello [How tooupdate function app files](functions-reference.md#fileupdate) in hello Azure Functions developer reference topic.</span></span>
3. <span data-ttu-id="40486-177">После hello *project.json* передачи файла см. в разделе, выходные данные как следующий пример в функции hello потоковая передача журналов:</span><span class="sxs-lookup"><span data-stu-id="40486-177">After hello *project.json* file is uploaded, you see output like hello following example in your function's streaming log:</span></span>

```
2016-04-04T19:02:48.745 Restoring packages.
2016-04-04T19:02:48.745 Starting NuGet restore
2016-04-04T19:02:50.183 MSBuild auto-detection: using msbuild version '14.0' from 'D:\Program Files (x86)\MSBuild\14.0\bin'.
2016-04-04T19:02:50.261 Feeds used:
2016-04-04T19:02:50.261 C:\DWASFiles\Sites\facavalfunctest\LocalAppData\NuGet\Cache
2016-04-04T19:02:50.261 https://api.nuget.org/v3/index.json
2016-04-04T19:02:50.261
2016-04-04T19:02:50.511 Restoring packages for D:\home\site\wwwroot\HttpTriggerCSharp1\Project.json...
2016-04-04T19:02:52.800 Installing Newtonsoft.Json 6.0.8.
2016-04-04T19:02:52.800 Installing Microsoft.ProjectOxford.Face 1.1.0.
2016-04-04T19:02:57.095 All packages are compatible with .NETFramework,Version=v4.6.
2016-04-04T19:02:57.189
2016-04-04T19:02:57.189
2016-04-04T19:02:57.455 Packages restored.
```

## <a name="environment-variables"></a><span data-ttu-id="40486-178">Переменные среды</span><span class="sxs-lookup"><span data-stu-id="40486-178">Environment variables</span></span>
<span data-ttu-id="40486-179">tooget переменной среды или значение параметра приложения, используйте `System.Environment.GetEnvironmentVariable`, как показано в следующем примере кода hello:</span><span class="sxs-lookup"><span data-stu-id="40486-179">tooget an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, as shown in hello following code example:</span></span>

```csharp
public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
    log.Info(GetEnvironmentVariable("AzureWebJobsStorage"));
    log.Info(GetEnvironmentVariable("WEBSITE_SITE_NAME"));
}

public static string GetEnvironmentVariable(string name)
{
    return name + ": " +
        System.Environment.GetEnvironmentVariable(name, EnvironmentVariableTarget.Process);
}
```

## <a name="reusing-csx-code"></a><span data-ttu-id="40486-180">Повторное использование кода CSX</span><span class="sxs-lookup"><span data-stu-id="40486-180">Reusing .csx code</span></span>
<span data-ttu-id="40486-181">В файле *run.csx* можно использовать классы и методы, определенные в других *CSX*-файлах.</span><span class="sxs-lookup"><span data-stu-id="40486-181">You can use classes and methods defined in other *.csx* files in your *run.csx* file.</span></span> <span data-ttu-id="40486-182">toodo, использовать `#load` директивы в вашей *run.csx* файла.</span><span class="sxs-lookup"><span data-stu-id="40486-182">toodo that, use `#load` directives in your *run.csx* file.</span></span> <span data-ttu-id="40486-183">В следующем примере hello, подпрограмма ведения журнала с именем `MyLogger` совместно в *myLogger.csx* и загружаются в *run.csx* с помощью hello `#load` директиву:</span><span class="sxs-lookup"><span data-stu-id="40486-183">In hello following example, a logging routine named `MyLogger` is shared in *myLogger.csx* and loaded into *run.csx* using hello `#load` directive:</span></span>

<span data-ttu-id="40486-184">Пример *run.csx*:</span><span class="sxs-lookup"><span data-stu-id="40486-184">Example *run.csx*:</span></span>

```csharp
#load "mylogger.csx"

public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Verbose($"Log by run.csx: {DateTime.Now}");
    MyLogger(log, $"Log by MyLogger: {DateTime.Now}");
}
```

<span data-ttu-id="40486-185">Пример *mylogger.csx*:</span><span class="sxs-lookup"><span data-stu-id="40486-185">Example *mylogger.csx*:</span></span>

```csharp
public static void MyLogger(TraceWriter log, string logtext)
{
    log.Verbose(logtext);
}
```

<span data-ttu-id="40486-186">С помощью общего *.csx* распространенный подход при необходимости toostrongly ввести аргументов между функциями, используя объект POCO.</span><span class="sxs-lookup"><span data-stu-id="40486-186">Using a shared *.csx* is a common pattern when you want toostrongly type your arguments between functions using a POCO object.</span></span> <span data-ttu-id="40486-187">В следующий упрощенный пример hello, триггер HTTP и очереди триггера используют объект POCO с именем `Order` hello порядок toostrongly тип данных:</span><span class="sxs-lookup"><span data-stu-id="40486-187">In hello following simplified example, an HTTP trigger and queue trigger share a POCO object named `Order` toostrongly type hello order data:</span></span>

<span data-ttu-id="40486-188">Пример файла *run.csx* для триггера HTTP:</span><span class="sxs-lookup"><span data-stu-id="40486-188">Example *run.csx* for HTTP trigger:</span></span>

```cs
#load "..\shared\order.csx"

using System.Net;

public static async Task<HttpResponseMessage> Run(Order req, IAsyncCollector<Order> outputQueueItem, TraceWriter log)
{
    log.Info("C# HTTP trigger function received an order.");
    log.Info(req.ToString());
    log.Info("Submitting tooprocessing queue.");

    if (req.orderId == null)
    {
        return new HttpResponseMessage(HttpStatusCode.BadRequest);
    }
    else
    {
        await outputQueueItem.AddAsync(req);
        return new HttpResponseMessage(HttpStatusCode.OK);
    }
}
```

<span data-ttu-id="40486-189">Пример файла *run.csx* для триггера очереди:</span><span class="sxs-lookup"><span data-stu-id="40486-189">Example *run.csx* for queue trigger:</span></span>

```cs
#load "..\shared\order.csx"

using System;

public static void Run(Order myQueueItem, out Order outputQueueItem,TraceWriter log)
{
    log.Info($"C# Queue trigger function processed order...");
    log.Info(myQueueItem.ToString());

    outputQueueItem = myQueueItem;
}
```

<span data-ttu-id="40486-190">Пример файла *order.csx*:</span><span class="sxs-lookup"><span data-stu-id="40486-190">Example *order.csx*:</span></span>

```cs
public class Order
{
    public string orderId {get; set; }
    public string custName {get; set;}
    public string custAddress {get; set;}
    public string custEmail {get; set;}
    public string cartId {get; set; }

    public override String ToString()
    {
        return "\n{\n\torderId : " + orderId +
                  "\n\tcustName : " + custName +             
                  "\n\tcustAddress : " + custAddress +             
                  "\n\tcustEmail : " + custEmail +             
                  "\n\tcartId : " + cartId + "\n}";             
    }
}
```

<span data-ttu-id="40486-191">Можно использовать относительный путь с hello `#load` директиву:</span><span class="sxs-lookup"><span data-stu-id="40486-191">You can use a relative path with hello `#load` directive:</span></span>

* <span data-ttu-id="40486-192">`#load "mylogger.csx"`загружает файл, расположенный в папке функции hello.</span><span class="sxs-lookup"><span data-stu-id="40486-192">`#load "mylogger.csx"` loads a file located in hello function folder.</span></span>
* <span data-ttu-id="40486-193">`#load "loadedfiles\mylogger.csx"`загружает файл, расположенный в папке в папке функции hello.</span><span class="sxs-lookup"><span data-stu-id="40486-193">`#load "loadedfiles\mylogger.csx"` loads a file located in a folder in hello function folder.</span></span>
* <span data-ttu-id="40486-194">`#load "..\shared\mylogger.csx"`загружает файл, расположенный в папке на hello же уровня, что и папка функции hello, т. е непосредственно под *wwwroot*.</span><span class="sxs-lookup"><span data-stu-id="40486-194">`#load "..\shared\mylogger.csx"` loads a file located in a folder at hello same level as hello function folder, that is, directly under *wwwroot*.</span></span>

<span data-ttu-id="40486-195">Hello `#load` директива работает только с *.csx* (C#) в сценарии, не с *.cs* файлов.</span><span class="sxs-lookup"><span data-stu-id="40486-195">hello `#load` directive works only with *.csx* (C# script) files, not with *.cs* files.</span></span>

<a name="imperative-bindings"></a> 

## <a name="binding-at-runtime-via-imperative-bindings"></a><span data-ttu-id="40486-196">Привязка в среде выполнения с помощью императивных привязок</span><span class="sxs-lookup"><span data-stu-id="40486-196">Binding at runtime via imperative bindings</span></span>

<span data-ttu-id="40486-197">В C# и других языков .NET, можно использовать [императивного](https://en.wikipedia.org/wiki/Imperative_programming) шаблон привязки, так как противоположность toohello [ *декларативный* ](https://en.wikipedia.org/wiki/Declarative_programming) привязок в *function.json*.</span><span class="sxs-lookup"><span data-stu-id="40486-197">In C# and other .NET languages, you can use an [imperative](https://en.wikipedia.org/wiki/Imperative_programming) binding pattern, as opposed toohello [*declarative*](https://en.wikipedia.org/wiki/Declarative_programming) bindings in *function.json*.</span></span> <span data-ttu-id="40486-198">Принудительный привязки полезно в том случае, если параметры привязки должны toobe вычислено во время выполнения, а не конструктора.</span><span class="sxs-lookup"><span data-stu-id="40486-198">Imperative binding is useful when binding parameters need toobe computed at runtime rather than design time.</span></span> <span data-ttu-id="40486-199">С этим шаблоном можно привязать toosupported ввода и вывода привязки на лету в коде функции.</span><span class="sxs-lookup"><span data-stu-id="40486-199">With this pattern, you can bind toosupported input and output binding on-the-fly in your function code.</span></span>

<span data-ttu-id="40486-200">Определите принудительную привязку следующим образом.</span><span class="sxs-lookup"><span data-stu-id="40486-200">Define an imperative binding as follows:</span></span>

- <span data-ttu-id="40486-201">**Не** добавляйте запись для нужных императивных привязок в файл *function.json*.</span><span class="sxs-lookup"><span data-stu-id="40486-201">**Do not** include an entry in *function.json* for your desired imperative bindings.</span></span>
- <span data-ttu-id="40486-202">Передайте входной параметр [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) или [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span><span class="sxs-lookup"><span data-stu-id="40486-202">Pass in an input parameter [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) or [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span></span>
- <span data-ttu-id="40486-203">Используйте следующие C# шаблон tooperform hello привязки данных hello.</span><span class="sxs-lookup"><span data-stu-id="40486-203">Use hello following C# pattern tooperform hello data binding.</span></span>

```cs
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
    ...
}
```

<span data-ttu-id="40486-204">где `BindingTypeAttribute` является атрибутом hello .NET, который определяет пользовательскую привязку, и `T` является входной или выходной тип, поддерживаемый этим типом привязки "hello".</span><span class="sxs-lookup"><span data-stu-id="40486-204">where `BindingTypeAttribute` is hello .NET attribute that defines your binding and `T` is hello input or output type that's supported by that binding type.</span></span> <span data-ttu-id="40486-205">`T` также не может быть параметром типа `out` (например, `out JObject`).</span><span class="sxs-lookup"><span data-stu-id="40486-205">`T` also cannot be an `out` parameter type (such as `out JObject`).</span></span> <span data-ttu-id="40486-206">Например, выходная привязка таблицы мобильных приложений поддерживает [шесть выходных типов](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), но для `T` можно использовать только [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) или [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs).</span><span class="sxs-lookup"><span data-stu-id="40486-206">For example, the Mobile Apps table output binding supports [six output types](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), but you can only use [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) for `T`.</span></span>

<span data-ttu-id="40486-207">Привет, следующий пример кода создает [привязка для вывода BLOB-объекта хранилища](functions-bindings-storage-blob.md#using-a-blob-output-binding) с большим двоичным объектом путь, определенный во время выполнения, затем записывает большой двоичный объект toohello строки.</span><span class="sxs-lookup"><span data-stu-id="40486-207">hello following example code creates a [Storage blob output binding](functions-bindings-storage-blob.md#using-a-blob-output-binding) with blob path that's defined at run time, then writes a string toohello blob.</span></span>

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host.Bindings.Runtime;

public static async Task Run(string input, Binder binder)
{
    using (var writer = await binder.BindAsync<TextWriter>(new BlobAttribute("samples-output/path")))
    {
        writer.Write("Hello World!!");
    }
}
```

<span data-ttu-id="40486-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) определяет hello [BLOB-объекта хранилища](functions-bindings-storage-blob.md) входного или выходного привязки, и [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) является поддерживаемой выходной тип привязки.</span><span class="sxs-lookup"><span data-stu-id="40486-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) defines hello [Storage blob](functions-bindings-storage-blob.md) input or output binding, and [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) is a supported output binding type.</span></span>
<span data-ttu-id="40486-209">Возвращает, hello кода hello приложения по умолчанию hello строка подключения учетной записи хранения (который является `AzureWebJobsStorage`).</span><span class="sxs-lookup"><span data-stu-id="40486-209">As is, hello code gets hello default app setting for hello Storage account connection string (which is `AzureWebJobsStorage`).</span></span> <span data-ttu-id="40486-210">Можно указать toouse параметр пользовательского приложения путем добавления [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) и передачи массива атрибутов hello в `BindAsync<T>()`.</span><span class="sxs-lookup"><span data-stu-id="40486-210">You can specify a custom app setting toouse by adding the [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) and passing hello attribute array into `BindAsync<T>()`.</span></span> <span data-ttu-id="40486-211">Например,</span><span class="sxs-lookup"><span data-stu-id="40486-211">For example,</span></span>

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host.Bindings.Runtime;

public static async Task Run(string input, Binder binder)
{
    var attributes = new Attribute[]
    {    
        new BlobAttribute("samples-output/path"),
        new StorageAccountAttribute("MyStorageAccount")
    };

    using (var writer = await binder.BindAsync<TextWriter>(attributes))
    {
        writer.Write("Hello World!");
    }
}
```

<span data-ttu-id="40486-212">Hello следующей таблице перечислены атрибуты hello .NET для каждой привязки тип и hello пакетов, в которых они определены.</span><span class="sxs-lookup"><span data-stu-id="40486-212">hello following table lists hello .NET attributes for each binding type and hello packages in which they are defined.</span></span>

> [!div class="mx-codeBreakAll"]
| <span data-ttu-id="40486-213">Привязка</span><span class="sxs-lookup"><span data-stu-id="40486-213">Binding</span></span> | <span data-ttu-id="40486-214">Атрибут</span><span class="sxs-lookup"><span data-stu-id="40486-214">Attribute</span></span> | <span data-ttu-id="40486-215">Ссылка, которую нужно добавить</span><span class="sxs-lookup"><span data-stu-id="40486-215">Add reference</span></span> |
|------|------|------|
| <span data-ttu-id="40486-216">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="40486-216">Cosmos DB</span></span> | [`Microsoft.Azure.WebJobs.DocumentDBAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.DocumentDB"` |
| <span data-ttu-id="40486-217">Концентраторы событий</span><span class="sxs-lookup"><span data-stu-id="40486-217">Event Hubs</span></span> | <span data-ttu-id="40486-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="40486-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.Jobs.ServiceBus"` |
| <span data-ttu-id="40486-219">Мобильные приложения</span><span class="sxs-lookup"><span data-stu-id="40486-219">Mobile Apps</span></span> | [`Microsoft.Azure.WebJobs.MobileTableAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.MobileApps"` |
| <span data-ttu-id="40486-220">Центры уведомлений</span><span class="sxs-lookup"><span data-stu-id="40486-220">Notification Hubs</span></span> | [`Microsoft.Azure.WebJobs.NotificationHubAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.NotificationHubs"` |
| <span data-ttu-id="40486-221">Служебная шина</span><span class="sxs-lookup"><span data-stu-id="40486-221">Service Bus</span></span> | <span data-ttu-id="40486-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="40486-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.WebJobs.ServiceBus"` |
| <span data-ttu-id="40486-223">Очередь службы хранилища</span><span class="sxs-lookup"><span data-stu-id="40486-223">Storage queue</span></span> | <span data-ttu-id="40486-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="40486-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="40486-225">Большой двоичный объект службы хранилища</span><span class="sxs-lookup"><span data-stu-id="40486-225">Storage blob</span></span> | <span data-ttu-id="40486-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="40486-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="40486-227">Таблица службы хранилища</span><span class="sxs-lookup"><span data-stu-id="40486-227">Storage table</span></span> | <span data-ttu-id="40486-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="40486-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="40486-229">Twilio</span><span class="sxs-lookup"><span data-stu-id="40486-229">Twilio</span></span> | [`Microsoft.Azure.WebJobs.TwilioSmsAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.Twilio"` |



## <a name="next-steps"></a><span data-ttu-id="40486-230">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="40486-230">Next steps</span></span>
<span data-ttu-id="40486-231">Дополнительные сведения см. в разделе hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="40486-231">For more information, see hello following resources:</span></span>

* <span data-ttu-id="40486-232">[Best Practices for Azure Functions](functions-best-practices.md) (Рекомендации по Функциям Azure)</span><span class="sxs-lookup"><span data-stu-id="40486-232">[Best Practices for Azure Functions](functions-best-practices.md)</span></span>
* [<span data-ttu-id="40486-233">Справочник разработчика по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="40486-233">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="40486-234">Справочник разработчика F# по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="40486-234">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="40486-235">Справочник разработчика NodeJS по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="40486-235">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="40486-236">Azure Functions triggers and bindings (Триггеры и привязки в Функциях Azure)</span><span class="sxs-lookup"><span data-stu-id="40486-236">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

[host\.json]: https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json
