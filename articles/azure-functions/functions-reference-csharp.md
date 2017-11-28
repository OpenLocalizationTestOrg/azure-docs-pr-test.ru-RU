---
title: "Справочник разработчика скриптов C# по Функциям Azure | Документация Майкрософт"
description: "Узнайте, как разрабатывать Функции Azure с помощью C#."
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
ms.openlocfilehash: 83a351ce0279ada8ce7fe0513497349471334a86
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-c-script-developer-reference"></a><span data-ttu-id="1eaee-104">Справочник разработчика скриптов C# по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="1eaee-104">Azure Functions C# script developer reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1eaee-105">Сценарий C#</span><span class="sxs-lookup"><span data-stu-id="1eaee-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="1eaee-106">Скрипт F#</span><span class="sxs-lookup"><span data-stu-id="1eaee-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="1eaee-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="1eaee-107">Node.js</span></span>](functions-reference-node.md)
>
>

<span data-ttu-id="1eaee-108">Взаимодействие со скриптом C# для Функций Azure основано на пакете SDK с веб-заданиями Azure.</span><span class="sxs-lookup"><span data-stu-id="1eaee-108">The C# script experience for Azure Functions is based on the Azure WebJobs SDK.</span></span> <span data-ttu-id="1eaee-109">Данные поступают в функцию C# через аргументы метода.</span><span class="sxs-lookup"><span data-stu-id="1eaee-109">Data flows into your C# function via method arguments.</span></span> <span data-ttu-id="1eaee-110">Имена аргументов указываются в `function.json`, и есть предварительно определенные имена для доступа к таким объектам, как средство ведения журнала функций и маркеры отмены.</span><span class="sxs-lookup"><span data-stu-id="1eaee-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like the function logger and cancellation tokens.</span></span>

<span data-ttu-id="1eaee-111">В этой статье предполагается, что вы уже прочли [справочник разработчика по Функциям Azure](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="1eaee-111">This article assumes that you've already read the [Azure Functions developer reference](functions-reference.md).</span></span>

<span data-ttu-id="1eaee-112">Дополнительные сведения об использовании библиотек классов C# с помощью Функций Azure см. в [этой статье](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="1eaee-112">For information on using C# class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span>

## <a name="how-csx-works"></a><span data-ttu-id="1eaee-113">Как работает формат CSX</span><span class="sxs-lookup"><span data-stu-id="1eaee-113">How .csx works</span></span>
<span data-ttu-id="1eaee-114">Формат `.csx` позволяет писать меньше стандартного кода и сосредоточиться на написании только функции C#.</span><span class="sxs-lookup"><span data-stu-id="1eaee-114">The `.csx` format allows you to write less "boilerplate" and focus on writing just a C# function.</span></span> <span data-ttu-id="1eaee-115">Как обычно, укажите ссылки на необходимые сборки и пространства имен в начале файла,</span><span class="sxs-lookup"><span data-stu-id="1eaee-115">Include any assembly references and namespaces at the beginning of the file as usual.</span></span> <span data-ttu-id="1eaee-116">а затем вместо помещения всего кода в пространство имен и класс просто определите метод `Run`.</span><span class="sxs-lookup"><span data-stu-id="1eaee-116">Instead of wrapping everything in a namespace and class, just define a `Run` method.</span></span> <span data-ttu-id="1eaee-117">Если необходимо включить какие-либо классы, например для определения объектов POCO, можно включить класс в тот же файл.</span><span class="sxs-lookup"><span data-stu-id="1eaee-117">If you need to include any classes, for instance to define Plain Old CLR Object (POCO) objects, you can include a class inside the same file.</span></span>   

## <a name="binding-to-arguments"></a><span data-ttu-id="1eaee-118">Привязка к аргументам</span><span class="sxs-lookup"><span data-stu-id="1eaee-118">Binding to arguments</span></span>
<span data-ttu-id="1eaee-119">Различные привязки связываются с функцией C# через свойство `name` в файле конфигурации *function.json*.</span><span class="sxs-lookup"><span data-stu-id="1eaee-119">The various bindings are bound to a C# function via the `name` property in the *function.json* configuration.</span></span> <span data-ttu-id="1eaee-120">У каждой привязки есть собственные поддерживаемые типы. Например, триггер больших двоичных объектов может поддерживать строку, POCO или CloudBlockBlob.</span><span class="sxs-lookup"><span data-stu-id="1eaee-120">Each binding has its own supported types; for instance, a blob trigger can support a string, a POCO, or a CloudBlockBlob.</span></span> <span data-ttu-id="1eaee-121">Поддерживаемые типы описаны в документации для каждой привязки.</span><span class="sxs-lookup"><span data-stu-id="1eaee-121">The supported types are documented in the reference for each binding.</span></span> <span data-ttu-id="1eaee-122">Для каждого свойства объекта POCO нужно определить метод задания и считывания.</span><span class="sxs-lookup"><span data-stu-id="1eaee-122">A POCO object must have a getter and setter defined for each property.</span></span>

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

## <a name="using-method-return-value-for-output-binding"></a><span data-ttu-id="1eaee-123">Использование возвращаемого значения метода для выходной привязки</span><span class="sxs-lookup"><span data-stu-id="1eaee-123">Using method return value for output binding</span></span>

<span data-ttu-id="1eaee-124">Используйте возвращаемое значение метода для выходной привязки, указав имя `$return` в *function.json*:</span><span class="sxs-lookup"><span data-stu-id="1eaee-124">You can use a method return value for an output binding, by using the name `$return` in *function.json*:</span></span>

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

## <a name="writing-multiple-output-values"></a><span data-ttu-id="1eaee-125">Написание нескольких значений выходных данных</span><span class="sxs-lookup"><span data-stu-id="1eaee-125">Writing multiple output values</span></span>

<span data-ttu-id="1eaee-126">Чтобы записать несколько значений в выходную привязку, используйте тип [`ICollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) или [`IAsyncCollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs).</span><span class="sxs-lookup"><span data-stu-id="1eaee-126">To write multiple values to an output binding, use the [`ICollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [`IAsyncCollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) types.</span></span> <span data-ttu-id="1eaee-127">Эти типы представляют собой доступные только для записи коллекции, записываемые в выходную привязку по завершении метода.</span><span class="sxs-lookup"><span data-stu-id="1eaee-127">These types are write-only collections that are written to the output binding when the method completes.</span></span>

<span data-ttu-id="1eaee-128">В следующем примере записываются несколько сообщений очереди с помощью `ICollector`:</span><span class="sxs-lookup"><span data-stu-id="1eaee-128">This example writes multiple queue messages using `ICollector`:</span></span>

```csharp
public static void Run(ICollector<string> myQueueItem, TraceWriter log)
{
    myQueueItem.Add("Hello");
    myQueueItem.Add("World!");
}
```

## <a name="logging"></a><span data-ttu-id="1eaee-129">Ведение журналов</span><span class="sxs-lookup"><span data-stu-id="1eaee-129">Logging</span></span>
<span data-ttu-id="1eaee-130">Для записи выходных данных в потоковые журналы в C# включите аргумент с типом `TraceWriter`.</span><span class="sxs-lookup"><span data-stu-id="1eaee-130">To log output to your streaming logs in C#, include an argument of type `TraceWriter`.</span></span> <span data-ttu-id="1eaee-131">Рекомендуем присвоить ему имя `log`.</span><span class="sxs-lookup"><span data-stu-id="1eaee-131">We recommend that you name it `log`.</span></span> <span data-ttu-id="1eaee-132">Не используйте `Console.Write` в Функциях Azure.</span><span class="sxs-lookup"><span data-stu-id="1eaee-132">Avoid using `Console.Write` in Azure Functions.</span></span> 

<span data-ttu-id="1eaee-133">`TraceWriter` определяется в [пакете SDK веб-заданий Azure](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span><span class="sxs-lookup"><span data-stu-id="1eaee-133">`TraceWriter` is defined in the [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span></span> <span data-ttu-id="1eaee-134">Уровень ведения журнала для `TraceWriter` можно настроить в [host\.json].</span><span class="sxs-lookup"><span data-stu-id="1eaee-134">The log level for `TraceWriter` can be configured in [host\.json].</span></span>

```csharp
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

## <a name="async"></a><span data-ttu-id="1eaee-135">Асинхронный режим</span><span class="sxs-lookup"><span data-stu-id="1eaee-135">Async</span></span>
<span data-ttu-id="1eaee-136">Чтобы сделать функцию асинхронной, используйте ключевое слово `async` и верните объект `Task`.</span><span class="sxs-lookup"><span data-stu-id="1eaee-136">To make a function asynchronous, use the `async` keyword and return a `Task` object.</span></span>

```csharp
public async static Task ProcessQueueMessageAsync(
        string blobName,
        Stream blobInput,
        Stream blobOutput)
{
    await blobInput.CopyToAsync(blobOutput, 4096, token);
}
```

## <a name="cancellation-token"></a><span data-ttu-id="1eaee-137">Токен отмены</span><span class="sxs-lookup"><span data-stu-id="1eaee-137">Cancellation Token</span></span>
<span data-ttu-id="1eaee-138">Для некоторых операций необходимо выполнить нормальное завершение работы.</span><span class="sxs-lookup"><span data-stu-id="1eaee-138">Some operations require graceful shutdown.</span></span> <span data-ttu-id="1eaee-139">Всегда лучше написать код, который может обрабатывать сбои, однако в случаях, когда нужно обрабатывать запросы на нормальное завершение работы, можно определить аргумент с типом [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx).</span><span class="sxs-lookup"><span data-stu-id="1eaee-139">While it's always best to write code that can handle crashing,  in cases where you want to handle graceful shutdown requests, you define a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) typed argument.</span></span>  <span data-ttu-id="1eaee-140">В случае завершения работы узла будет предоставлен маркер `CancellationToken`.</span><span class="sxs-lookup"><span data-stu-id="1eaee-140">A `CancellationToken` is provided to signal that a host shutdown is triggered.</span></span>

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

## <a name="importing-namespaces"></a><span data-ttu-id="1eaee-141">Импорт пространств имен</span><span class="sxs-lookup"><span data-stu-id="1eaee-141">Importing namespaces</span></span>
<span data-ttu-id="1eaee-142">Если требуется импортировать пространства имен, это можно сделать как обычно — с помощью предложения `using` .</span><span class="sxs-lookup"><span data-stu-id="1eaee-142">If you need to import namespaces, you can do so as usual, with the `using` clause.</span></span>

```csharp
using System.Net;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="1eaee-143">Следующие пространства имен импортируются автоматически и поэтому являются необязательными:</span><span class="sxs-lookup"><span data-stu-id="1eaee-143">The following namespaces are automatically imported and are therefore optional:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`

## <a name="referencing-external-assemblies"></a><span data-ttu-id="1eaee-144">Ссылки на внешние сборки</span><span class="sxs-lookup"><span data-stu-id="1eaee-144">Referencing External Assemblies</span></span>
<span data-ttu-id="1eaee-145">Для сборок платформы добавьте ссылки с помощью директивы `#r "AssemblyName"` .</span><span class="sxs-lookup"><span data-stu-id="1eaee-145">For framework assemblies, add references by using the `#r "AssemblyName"` directive.</span></span>

```csharp
#r "System.Web.Http"

using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="1eaee-146">Следующие сборки автоматически добавляются средой внешнего размещения Функций Azure:</span><span class="sxs-lookup"><span data-stu-id="1eaee-146">The following assemblies are automatically added by the Azure Functions hosting environment:</span></span>

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

<span data-ttu-id="1eaee-147">К следующим сборкам можно обращаться по простому имени (например, `#r "AssemblyName"`):</span><span class="sxs-lookup"><span data-stu-id="1eaee-147">The following assemblies may be referenced by simple-name (for example, `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNet.WebHooks.Common`
* `Microsoft.Azure.NotificationHubs`

## <a name="referencing-custom-assemblies"></a><span data-ttu-id="1eaee-148">Ссылки на пользовательские сборки</span><span class="sxs-lookup"><span data-stu-id="1eaee-148">Referencing custom assemblies</span></span>

<span data-ttu-id="1eaee-149">Чтобы указать ссылку на пользовательские сборки, можно использовать *общую* или *закрытую* сборку.</span><span class="sxs-lookup"><span data-stu-id="1eaee-149">To reference a custom assembly, you can use either a *shared* assembly or a *private* assembly:</span></span>
- <span data-ttu-id="1eaee-150">Общие сборки совместно используют все функции в приложении-функции.</span><span class="sxs-lookup"><span data-stu-id="1eaee-150">Shared assemblies are shared across all functions within a function app.</span></span> <span data-ttu-id="1eaee-151">Чтобы указать ссылку на пользовательские сборки, отправьте сборку в приложение-функцию, например как в папке `bin` в корне приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="1eaee-151">To reference a custom assembly, upload the assembly to your function app, such as in a `bin` folder in the function app root.</span></span> 
- <span data-ttu-id="1eaee-152">Закрытые сборки входят в контекст указанной функции и поддерживают загрузку неопубликованных приложений разных версий.</span><span class="sxs-lookup"><span data-stu-id="1eaee-152">Private assemblies are part of a given function's context, and support side-loading of different versions.</span></span> <span data-ttu-id="1eaee-153">Закрытые сборки необходимо отправить в папку `bin` в каталоге функции.</span><span class="sxs-lookup"><span data-stu-id="1eaee-153">Private assemblies should be uploaded in a `bin` folder in the function directory.</span></span> <span data-ttu-id="1eaee-154">Укажите на них ссылки, используя имя файла, например `#r "MyAssembly.dll"`.</span><span class="sxs-lookup"><span data-stu-id="1eaee-154">Reference using the file name, such as  `#r "MyAssembly.dll"`.</span></span> 

<span data-ttu-id="1eaee-155">Дополнительные сведения о передаче файлов в папку функции см. в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="1eaee-155">For information on how to upload files to your function folder, see the following section on package management.</span></span>

### <a name="watched-directories"></a><span data-ttu-id="1eaee-156">Каталоги отслеживания</span><span class="sxs-lookup"><span data-stu-id="1eaee-156">Watched directories</span></span>

<span data-ttu-id="1eaee-157">Каталог, содержащий файл сценария функции, автоматически отслеживает изменения в сборках.</span><span class="sxs-lookup"><span data-stu-id="1eaee-157">The directory that contains the function script file is automatically watched for changes to assemblies.</span></span> <span data-ttu-id="1eaee-158">Чтобы отслеживать изменения сборки в других каталогах, добавьте их в список `watchDirectories` в [host\.json].</span><span class="sxs-lookup"><span data-stu-id="1eaee-158">To watch for assembly changes in other directories, add them to the `watchDirectories` list in [host\.json].</span></span>

## <a name="using-nuget-packages"></a><span data-ttu-id="1eaee-159">Использование пакетов NuGet</span><span class="sxs-lookup"><span data-stu-id="1eaee-159">Using NuGet packages</span></span>
<span data-ttu-id="1eaee-160">Чтобы использовать пакеты NuGet в функции C#, отправьте файл *project.json* в папку соответствующей функции в файловой системе приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="1eaee-160">To use NuGet packages in a C# function, upload a *project.json* file to the function's folder in the function app's file system.</span></span> <span data-ttu-id="1eaee-161">Ниже приведен пример файла *project.json* , который добавляет ссылку на Microsoft.ProjectOxford.Face версии 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="1eaee-161">Here is an example *project.json* file that adds a reference to Microsoft.ProjectOxford.Face version 1.1.0:</span></span>

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

<span data-ttu-id="1eaee-162">Поддерживается только версия платформы .NET Framework 4.6, поэтому убедитесь, что ваш файл *project.json* определяет `net46`, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="1eaee-162">Only the .NET Framework 4.6 is supported, so make sure that your *project.json* file specifies `net46` as shown here.</span></span>

<span data-ttu-id="1eaee-163">При отправке файла *project.json* среда выполнения получает пакеты и автоматически добавляет ссылки на сборки пакетов.</span><span class="sxs-lookup"><span data-stu-id="1eaee-163">When you upload a *project.json* file, the runtime gets the packages and automatically adds references to the package assemblies.</span></span> <span data-ttu-id="1eaee-164">Добавлять директивы `#r "AssemblyName"` не нужно.</span><span class="sxs-lookup"><span data-stu-id="1eaee-164">You don't need to add `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="1eaee-165">Для использования типов, определенных в пакетах NuGet, добавьте необходимые инструкции `using` в файл *run.csx*.</span><span class="sxs-lookup"><span data-stu-id="1eaee-165">To use the types defined in the NuGet packages, add the required `using` statements to your *run.csx* file</span></span> 

<span data-ttu-id="1eaee-166">В среде выполнения функций восстановление NuGet работает путем сравнения `project.json` и `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="1eaee-166">In the Functions runtime, NuGet restore works by comparing `project.json` and `project.lock.json`.</span></span> <span data-ttu-id="1eaee-167">Если метки даты и времени файлов **не** совпадают, выполняется восстановление NuGet и скачиваются обновленные пакеты.</span><span class="sxs-lookup"><span data-stu-id="1eaee-167">If the date and time stamps of the files **do not** match, a NuGet restore runs and NuGet downloads updated packages.</span></span> <span data-ttu-id="1eaee-168">Однако если дата и время создания файлов **совпадают**, NuGet не выполняет восстановление.</span><span class="sxs-lookup"><span data-stu-id="1eaee-168">However, if the date and time stamps of the files **do** match, NuGet does not perform a restore.</span></span> <span data-ttu-id="1eaee-169">Поэтому не следует развертывать `project.lock.json`, так как в результате NuGet пропустит восстановление пакета.</span><span class="sxs-lookup"><span data-stu-id="1eaee-169">Therefore, `project.lock.json` should not be deployed as it causes NuGet to skip package restore.</span></span> <span data-ttu-id="1eaee-170">Чтобы предотвратить развертывание блокирующего файла, добавьте `project.lock.json` в файл `.gitignore`.</span><span class="sxs-lookup"><span data-stu-id="1eaee-170">To avoid deploying the lock file, add the `project.lock.json` to the `.gitignore` file.</span></span>

<span data-ttu-id="1eaee-171">Чтобы использовать настраиваемые веб-каналы NuGet, укажите веб-канал в файле *Nuget.Config* в корне приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="1eaee-171">To use a custom NuGet feed, specify the feed in a *Nuget.Config* file in the Function App root.</span></span> <span data-ttu-id="1eaee-172">Дополнительные сведения см. в статье [Configuring NuGet behavior](/nuget/consume-packages/configuring-nuget-behavior) (Настройка поведения NuGet).</span><span class="sxs-lookup"><span data-stu-id="1eaee-172">For more information, see [Configuring NuGet behavior](/nuget/consume-packages/configuring-nuget-behavior).</span></span>

### <a name="using-a-projectjson-file"></a><span data-ttu-id="1eaee-173">Использование файла project.json</span><span class="sxs-lookup"><span data-stu-id="1eaee-173">Using a project.json file</span></span>
1. <span data-ttu-id="1eaee-174">Откройте функцию на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="1eaee-174">Open the function in the Azure portal.</span></span> <span data-ttu-id="1eaee-175">На вкладке "Журналы" отображаются выходные данные установки пакета.</span><span class="sxs-lookup"><span data-stu-id="1eaee-175">The logs tab displays the package installation output.</span></span>
2. <span data-ttu-id="1eaee-176">Чтобы отправить файл project.json, используйте один из методов, описанных в разделе [Как обновить файлы приложения-функции](functions-reference.md#fileupdate) статьи "Руководство для разработчиков по Функциям Azure".</span><span class="sxs-lookup"><span data-stu-id="1eaee-176">To upload a project.json file, use one of the methods described in the [How to update function app files](functions-reference.md#fileupdate) in the Azure Functions developer reference topic.</span></span>
3. <span data-ttu-id="1eaee-177">После отправки файла *project.json* в потоковом журнале функции отобразятся выходные данные, как в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="1eaee-177">After the *project.json* file is uploaded, you see output like the following example in your function's streaming log:</span></span>

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

## <a name="environment-variables"></a><span data-ttu-id="1eaee-178">Переменные среды</span><span class="sxs-lookup"><span data-stu-id="1eaee-178">Environment variables</span></span>
<span data-ttu-id="1eaee-179">Чтобы получить значение переменной среды или значение параметра приложения, используйте `System.Environment.GetEnvironmentVariable`, как показано в следующем примере кода.</span><span class="sxs-lookup"><span data-stu-id="1eaee-179">To get an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, as shown in the following code example:</span></span>

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

## <a name="reusing-csx-code"></a><span data-ttu-id="1eaee-180">Повторное использование кода CSX</span><span class="sxs-lookup"><span data-stu-id="1eaee-180">Reusing .csx code</span></span>
<span data-ttu-id="1eaee-181">В файле *run.csx* можно использовать классы и методы, определенные в других *CSX*-файлах.</span><span class="sxs-lookup"><span data-stu-id="1eaee-181">You can use classes and methods defined in other *.csx* files in your *run.csx* file.</span></span> <span data-ttu-id="1eaee-182">Для этого используйте директивы `#load` в файле *run.csx*.</span><span class="sxs-lookup"><span data-stu-id="1eaee-182">To do that, use `#load` directives in your *run.csx* file.</span></span> <span data-ttu-id="1eaee-183">В следующем примере к процедуре ведения журнала с именем `MyLogger` предоставляется общий доступ в файле *myLogger.csx*, а также она загружается в файл *run.csx*. Для этого используется директива `#load`:</span><span class="sxs-lookup"><span data-stu-id="1eaee-183">In the following example, a logging routine named `MyLogger` is shared in *myLogger.csx* and loaded into *run.csx* using the `#load` directive:</span></span>

<span data-ttu-id="1eaee-184">Пример *run.csx*:</span><span class="sxs-lookup"><span data-stu-id="1eaee-184">Example *run.csx*:</span></span>

```csharp
#load "mylogger.csx"

public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Verbose($"Log by run.csx: {DateTime.Now}");
    MyLogger(log, $"Log by MyLogger: {DateTime.Now}");
}
```

<span data-ttu-id="1eaee-185">Пример *mylogger.csx*:</span><span class="sxs-lookup"><span data-stu-id="1eaee-185">Example *mylogger.csx*:</span></span>

```csharp
public static void MyLogger(TraceWriter log, string logtext)
{
    log.Verbose(logtext);
}
```

<span data-ttu-id="1eaee-186">Обычно для задания строго типизированных аргументов в функциях с использованием объекта POCO применяется общий файл с расширением *CSX*.</span><span class="sxs-lookup"><span data-stu-id="1eaee-186">Using a shared *.csx* is a common pattern when you want to strongly type your arguments between functions using a POCO object.</span></span> <span data-ttu-id="1eaee-187">В указанном ниже упрощенном примере триггер HTTP и очереди совместно используют объект POCO с именем `Order` для задания строго типизированных данных о заказах.</span><span class="sxs-lookup"><span data-stu-id="1eaee-187">In the following simplified example, an HTTP trigger and queue trigger share a POCO object named `Order` to strongly type the order data:</span></span>

<span data-ttu-id="1eaee-188">Пример файла *run.csx* для триггера HTTP:</span><span class="sxs-lookup"><span data-stu-id="1eaee-188">Example *run.csx* for HTTP trigger:</span></span>

```cs
#load "..\shared\order.csx"

using System.Net;

public static async Task<HttpResponseMessage> Run(Order req, IAsyncCollector<Order> outputQueueItem, TraceWriter log)
{
    log.Info("C# HTTP trigger function received an order.");
    log.Info(req.ToString());
    log.Info("Submitting to processing queue.");

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

<span data-ttu-id="1eaee-189">Пример файла *run.csx* для триггера очереди:</span><span class="sxs-lookup"><span data-stu-id="1eaee-189">Example *run.csx* for queue trigger:</span></span>

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

<span data-ttu-id="1eaee-190">Пример файла *order.csx*:</span><span class="sxs-lookup"><span data-stu-id="1eaee-190">Example *order.csx*:</span></span>

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

<span data-ttu-id="1eaee-191">В директиве `#load` можно использовать относительный путь:</span><span class="sxs-lookup"><span data-stu-id="1eaee-191">You can use a relative path with the `#load` directive:</span></span>

* <span data-ttu-id="1eaee-192">`#load "mylogger.csx"` загружает файл, расположенный в папке функции.</span><span class="sxs-lookup"><span data-stu-id="1eaee-192">`#load "mylogger.csx"` loads a file located in the function folder.</span></span>
* <span data-ttu-id="1eaee-193">`#load "loadedfiles\mylogger.csx"` загружает файл, расположенный в папке, которая содержится в папке функции.</span><span class="sxs-lookup"><span data-stu-id="1eaee-193">`#load "loadedfiles\mylogger.csx"` loads a file located in a folder in the function folder.</span></span>
* <span data-ttu-id="1eaee-194">`#load "..\shared\mylogger.csx"` загружает файл, расположенный в папке на том же уровне, что и папка функции, то есть непосредственно в разделе *wwwroot*.</span><span class="sxs-lookup"><span data-stu-id="1eaee-194">`#load "..\shared\mylogger.csx"` loads a file located in a folder at the same level as the function folder, that is, directly under *wwwroot*.</span></span>

<span data-ttu-id="1eaee-195">Директива `#load` работает только с *CSX*-файлами (сценариями C#), но не с *CS*-файлами.</span><span class="sxs-lookup"><span data-stu-id="1eaee-195">The `#load` directive works only with *.csx* (C# script) files, not with *.cs* files.</span></span>

<a name="imperative-bindings"></a> 

## <a name="binding-at-runtime-via-imperative-bindings"></a><span data-ttu-id="1eaee-196">Привязка в среде выполнения с помощью императивных привязок</span><span class="sxs-lookup"><span data-stu-id="1eaee-196">Binding at runtime via imperative bindings</span></span>

<span data-ttu-id="1eaee-197">Для C# и других языков .NET можно использовать шаблон [императивной](https://en.wikipedia.org/wiki/Imperative_programming) привязки, которая отличается от [*декларативной*](https://en.wikipedia.org/wiki/Declarative_programming) привязки в файле *function.json*.</span><span class="sxs-lookup"><span data-stu-id="1eaee-197">In C# and other .NET languages, you can use an [imperative](https://en.wikipedia.org/wiki/Imperative_programming) binding pattern, as opposed to the [*declarative*](https://en.wikipedia.org/wiki/Declarative_programming) bindings in *function.json*.</span></span> <span data-ttu-id="1eaee-198">Императивную привязку удобно использовать, когда параметры привязки должны вычисляться не при проектировании, а во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="1eaee-198">Imperative binding is useful when binding parameters need to be computed at runtime rather than design time.</span></span> <span data-ttu-id="1eaee-199">С использованием такого шаблона можно на лету выполнить привязку к поддерживаемым входным и выходным привязкам в коде функции.</span><span class="sxs-lookup"><span data-stu-id="1eaee-199">With this pattern, you can bind to supported input and output binding on-the-fly in your function code.</span></span>

<span data-ttu-id="1eaee-200">Определите принудительную привязку следующим образом.</span><span class="sxs-lookup"><span data-stu-id="1eaee-200">Define an imperative binding as follows:</span></span>

- <span data-ttu-id="1eaee-201">**Не** добавляйте запись для нужных императивных привязок в файл *function.json*.</span><span class="sxs-lookup"><span data-stu-id="1eaee-201">**Do not** include an entry in *function.json* for your desired imperative bindings.</span></span>
- <span data-ttu-id="1eaee-202">Передайте входной параметр [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) или [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span><span class="sxs-lookup"><span data-stu-id="1eaee-202">Pass in an input parameter [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) or [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span></span>
- <span data-ttu-id="1eaee-203">Используйте следующий шаблон C# для привязки данных,</span><span class="sxs-lookup"><span data-stu-id="1eaee-203">Use the following C# pattern to perform the data binding.</span></span>

```cs
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
    ...
}
```

<span data-ttu-id="1eaee-204">где `BindingTypeAttribute` — атрибут .NET, определяющий пользовательскую привязку, а `T` — входной или выходной тип, поддерживаемый этим типом привязки.</span><span class="sxs-lookup"><span data-stu-id="1eaee-204">where `BindingTypeAttribute` is the .NET attribute that defines your binding and `T` is the input or output type that's supported by that binding type.</span></span> <span data-ttu-id="1eaee-205">`T` также не может быть параметром типа `out` (например, `out JObject`).</span><span class="sxs-lookup"><span data-stu-id="1eaee-205">`T` also cannot be an `out` parameter type (such as `out JObject`).</span></span> <span data-ttu-id="1eaee-206">Например, выходная привязка таблицы мобильных приложений поддерживает [шесть выходных типов](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), но для `T` можно использовать только [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) или [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs).</span><span class="sxs-lookup"><span data-stu-id="1eaee-206">For example, the Mobile Apps table output binding supports [six output types](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), but you can only use [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) for `T`.</span></span>

<span data-ttu-id="1eaee-207">В следующем примере кода создается [выходная привязка большого двоичного объекта службы хранилища](functions-bindings-storage-blob.md#using-a-blob-output-binding) с путем к большому двоичному объекту, определенному во время выполнения, а затем записывается строка в большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="1eaee-207">The following example code creates a [Storage blob output binding](functions-bindings-storage-blob.md#using-a-blob-output-binding) with blob path that's defined at run time, then writes a string to the blob.</span></span>

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

<span data-ttu-id="1eaee-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) определяет входную или выходную привязку [большого двоичного объекта службы хранилища](functions-bindings-storage-blob.md), а [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) представляет собой поддерживаемый тип выходной привязки.</span><span class="sxs-lookup"><span data-stu-id="1eaee-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) defines the [Storage blob](functions-bindings-storage-blob.md) input or output binding, and [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) is a supported output binding type.</span></span>
<span data-ttu-id="1eaee-209">Код возвращает параметр приложения по умолчанию для строки подключения к учетной записи службы хранилища (`AzureWebJobsStorage`).</span><span class="sxs-lookup"><span data-stu-id="1eaee-209">As is, the code gets the default app setting for the Storage account connection string (which is `AzureWebJobsStorage`).</span></span> <span data-ttu-id="1eaee-210">Вы можете указать пользовательский параметр приложения, который следует использовать, добавив [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) и передавая массив атрибутов в `BindAsync<T>()`.</span><span class="sxs-lookup"><span data-stu-id="1eaee-210">You can specify a custom app setting to use by adding the [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) and passing the attribute array into `BindAsync<T>()`.</span></span> <span data-ttu-id="1eaee-211">Например,</span><span class="sxs-lookup"><span data-stu-id="1eaee-211">For example,</span></span>

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

<span data-ttu-id="1eaee-212">В следующей таблице перечислены атрибуты .NET для каждого типа привязки и пакеты, в которых они определены.</span><span class="sxs-lookup"><span data-stu-id="1eaee-212">The following table lists the .NET attributes for each binding type and the packages in which they are defined.</span></span>

> [!div class="mx-codeBreakAll"]
| <span data-ttu-id="1eaee-213">Привязка</span><span class="sxs-lookup"><span data-stu-id="1eaee-213">Binding</span></span> | <span data-ttu-id="1eaee-214">Атрибут</span><span class="sxs-lookup"><span data-stu-id="1eaee-214">Attribute</span></span> | <span data-ttu-id="1eaee-215">Ссылка, которую нужно добавить</span><span class="sxs-lookup"><span data-stu-id="1eaee-215">Add reference</span></span> |
|------|------|------|
| <span data-ttu-id="1eaee-216">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1eaee-216">Cosmos DB</span></span> | [`Microsoft.Azure.WebJobs.DocumentDBAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.DocumentDB"` |
| <span data-ttu-id="1eaee-217">Концентраторы событий</span><span class="sxs-lookup"><span data-stu-id="1eaee-217">Event Hubs</span></span> | <span data-ttu-id="1eaee-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="1eaee-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.Jobs.ServiceBus"` |
| <span data-ttu-id="1eaee-219">Мобильные приложения</span><span class="sxs-lookup"><span data-stu-id="1eaee-219">Mobile Apps</span></span> | [`Microsoft.Azure.WebJobs.MobileTableAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.MobileApps"` |
| <span data-ttu-id="1eaee-220">Центры уведомлений</span><span class="sxs-lookup"><span data-stu-id="1eaee-220">Notification Hubs</span></span> | [`Microsoft.Azure.WebJobs.NotificationHubAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.NotificationHubs"` |
| <span data-ttu-id="1eaee-221">Служебная шина</span><span class="sxs-lookup"><span data-stu-id="1eaee-221">Service Bus</span></span> | <span data-ttu-id="1eaee-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="1eaee-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.WebJobs.ServiceBus"` |
| <span data-ttu-id="1eaee-223">Очередь службы хранилища</span><span class="sxs-lookup"><span data-stu-id="1eaee-223">Storage queue</span></span> | <span data-ttu-id="1eaee-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="1eaee-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="1eaee-225">Большой двоичный объект службы хранилища</span><span class="sxs-lookup"><span data-stu-id="1eaee-225">Storage blob</span></span> | <span data-ttu-id="1eaee-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="1eaee-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="1eaee-227">Таблица службы хранилища</span><span class="sxs-lookup"><span data-stu-id="1eaee-227">Storage table</span></span> | <span data-ttu-id="1eaee-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="1eaee-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="1eaee-229">Twilio</span><span class="sxs-lookup"><span data-stu-id="1eaee-229">Twilio</span></span> | [`Microsoft.Azure.WebJobs.TwilioSmsAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.Twilio"` |



## <a name="next-steps"></a><span data-ttu-id="1eaee-230">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1eaee-230">Next steps</span></span>
<span data-ttu-id="1eaee-231">Для получения дополнительных сведений см. следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="1eaee-231">For more information, see the following resources:</span></span>

* <span data-ttu-id="1eaee-232">[Best Practices for Azure Functions](functions-best-practices.md) (Рекомендации по Функциям Azure)</span><span class="sxs-lookup"><span data-stu-id="1eaee-232">[Best Practices for Azure Functions](functions-best-practices.md)</span></span>
* [<span data-ttu-id="1eaee-233">Справочник разработчика по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="1eaee-233">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="1eaee-234">Справочник разработчика F# по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="1eaee-234">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="1eaee-235">Справочник разработчика NodeJS по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="1eaee-235">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="1eaee-236">Azure Functions triggers and bindings (Триггеры и привязки в Функциях Azure)</span><span class="sxs-lookup"><span data-stu-id="1eaee-236">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

[host\.json]: https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json
