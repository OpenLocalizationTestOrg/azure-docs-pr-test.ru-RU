---
title: "Справочник разработчика для языка F# по Функциям Azure | Документация Майкрософт"
description: "Узнайте, как разрабатывать Функции Azure с помощью F#."
services: functions
documentationcenter: fsharp
author: sylvanc
manager: jbronsk
editor: 
tags: 
keywords: "Azure функции, функции, для обработки событий, веб-перехватчиков, динамических вычислений, без сервера архитектуры, F #"
ms.assetid: e60226e5-2630-41d7-9e5b-9f9e5acc8e50
ms.service: functions
ms.devlang: fsharp
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/09/2016
ms.author: syclebsc
ms.openlocfilehash: 1691d378263f6b4ce5072f5c621d8db02f774b5f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-f-developer-reference"></a><span data-ttu-id="eb225-104">Справочник разработчика F# по Функциям Azure</span><span class="sxs-lookup"><span data-stu-id="eb225-104">Azure Functions F# Developer Reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="eb225-105">Сценарий C#</span><span class="sxs-lookup"><span data-stu-id="eb225-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="eb225-106">Скрипт F#</span><span class="sxs-lookup"><span data-stu-id="eb225-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="eb225-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="eb225-107">Node.js</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="eb225-108">F# для Функций Azure — это решение для быстрого запуска фрагментов кода (функций) в облаке.</span><span class="sxs-lookup"><span data-stu-id="eb225-108">F# for Azure Functions is a solution for easily running small pieces of code, or "functions," in the cloud.</span></span> <span data-ttu-id="eb225-109">Данные поступают в функцию F# через аргументы функции.</span><span class="sxs-lookup"><span data-stu-id="eb225-109">Data flows into your F# function via function arguments.</span></span> <span data-ttu-id="eb225-110">Имена аргументов указываются в `function.json`, и есть предварительно определенные имена для доступа к таким объектам, как средство ведения журнала функций и маркеры отмены.</span><span class="sxs-lookup"><span data-stu-id="eb225-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like the function logger and cancellation tokens.</span></span>

<span data-ttu-id="eb225-111">В этой статье предполагается, что вы уже прочли [справочник разработчика по Функциям Azure](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="eb225-111">This article assumes that you've already read the [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="how-fsx-works"></a><span data-ttu-id="eb225-112">Принципы работы FSX-файла</span><span class="sxs-lookup"><span data-stu-id="eb225-112">How .fsx works</span></span>
<span data-ttu-id="eb225-113">Файл `.fsx` — это скрипт F#.</span><span class="sxs-lookup"><span data-stu-id="eb225-113">An `.fsx` file is an F# script.</span></span> <span data-ttu-id="eb225-114">Он может рассматриваться как проект F#, содержащийся в одном файле.</span><span class="sxs-lookup"><span data-stu-id="eb225-114">It can be thought of as an F# project that's contained in a single file.</span></span> <span data-ttu-id="eb225-115">Этот файл содержит код для программы (в этом случае функция Azure) и директивы для управления зависимостями.</span><span class="sxs-lookup"><span data-stu-id="eb225-115">The file contains both the code for your program (in this case, your Azure Function) and directives for managing dependencies.</span></span>

<span data-ttu-id="eb225-116">При использовании `.fsx` для функции Azure обычно необходимые сборки добавляются автоматически, что позволяет сосредоточиться на функции, а не на стандартном коде.</span><span class="sxs-lookup"><span data-stu-id="eb225-116">When you use an `.fsx` for an Azure Function, commonly required assemblies are automatically included for you, allowing you to focus on the function rather than "boilerplate" code.</span></span>

## <a name="binding-to-arguments"></a><span data-ttu-id="eb225-117">Привязка к аргументам</span><span class="sxs-lookup"><span data-stu-id="eb225-117">Binding to arguments</span></span>
<span data-ttu-id="eb225-118">Каждая привязка поддерживает набор аргументов. Это подробно описано в [справочнике разработчика по триггерам и привязкам в Функциях Azure](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="eb225-118">Each binding supports some set of arguments, as detailed in the [Azure Functions triggers and bindings developer reference](functions-triggers-bindings.md).</span></span> <span data-ttu-id="eb225-119">Например, одной из привязок аргументов, поддерживаемых триггером больших двоичных объектов, выступает POCO. Эту привязку можно представить с помощью записи F#.</span><span class="sxs-lookup"><span data-stu-id="eb225-119">For example, one of the argument bindings a blob trigger supports is a POCO, which can be expressed using an F# record.</span></span> <span data-ttu-id="eb225-120">Например:</span><span class="sxs-lookup"><span data-stu-id="eb225-120">For example:</span></span>

```fsharp
type Item = { Id: string }

let Run(blob: string, output: byref<Item>) =
    let item = { Id = "Some ID" }
    output <- item
```

<span data-ttu-id="eb225-121">Для функции Azure на F# понадобится один или несколько аргументов.</span><span class="sxs-lookup"><span data-stu-id="eb225-121">Your F# Azure Function will take one or more arguments.</span></span> <span data-ttu-id="eb225-122">Говоря об аргументах Функций Azure, мы имеем в виду *входные* и *выходные* аргументы.</span><span class="sxs-lookup"><span data-stu-id="eb225-122">When we talk about Azure Functions arguments, we refer to *input* arguments and *output* arguments.</span></span> <span data-ttu-id="eb225-123">Входной аргумент соответствует своему названию, так как это входные данные для функции Azure F#.</span><span class="sxs-lookup"><span data-stu-id="eb225-123">An input argument is exactly what it sounds like: input to your F# Azure Function.</span></span> <span data-ttu-id="eb225-124">*Выходной* аргумент представлен изменяемыми данными или аргументом `byref<>`, который используется для передачи данных обратно *из* этой функции.</span><span class="sxs-lookup"><span data-stu-id="eb225-124">An *output* argument is mutable data or a `byref<>` argument that serves as a way to pass data back *out* of your function.</span></span>

<span data-ttu-id="eb225-125">В приведенном выше примере `blob` выступает в качестве входного аргумента, а `output` — выходного аргумента.</span><span class="sxs-lookup"><span data-stu-id="eb225-125">In the example above, `blob` is an input argument, and `output` is an output argument.</span></span> <span data-ttu-id="eb225-126">Обратите внимание, мы использовали `byref<>` для `output` (не нужно добавлять аннотацию `[<Out>]`).</span><span class="sxs-lookup"><span data-stu-id="eb225-126">Notice that we used `byref<>` for `output` (there's no need to add the `[<Out>]` annotation).</span></span> <span data-ttu-id="eb225-127">При использовании типа `byref<>` функция может изменять запись или объект, на который будет ссылаться аргумент.</span><span class="sxs-lookup"><span data-stu-id="eb225-127">Using a `byref<>` type allows your function to change which record or object the argument refers to.</span></span>

<span data-ttu-id="eb225-128">Если в качестве типа входных данных используется запись F#, определение записи необходимо пометить атрибутом `[<CLIMutable>]` , чтобы платформа Функций Azure могла установить поля соответствующим образом перед передачей записи в функцию.</span><span class="sxs-lookup"><span data-stu-id="eb225-128">When an F# record is used as an input type, the record definition must be marked with `[<CLIMutable>]` in order to allow the Azure Functions framework to set the fields appropriately before passing the record to your function.</span></span> <span data-ttu-id="eb225-129">"За кулисами" `[<CLIMutable>]` создает методы задания свойств записи.</span><span class="sxs-lookup"><span data-stu-id="eb225-129">Under the hood, `[<CLIMutable>]` generates setters for the record properties.</span></span> <span data-ttu-id="eb225-130">Например:</span><span class="sxs-lookup"><span data-stu-id="eb225-130">For example:</span></span>

```fsharp
[<CLIMutable>]
type TestObject =
    { SenderName : string
      Greeting : string }

let Run(req: TestObject, log: TraceWriter) =
    { req with Greeting = sprintf "Hello, %s" req.SenderName }
```

<span data-ttu-id="eb225-131">Класс F# можно также использовать для входных и выходных аргументов.</span><span class="sxs-lookup"><span data-stu-id="eb225-131">An F# class can also be used for both in and out arguments.</span></span> <span data-ttu-id="eb225-132">Для свойств класса обычно требуются методы получения и задания.</span><span class="sxs-lookup"><span data-stu-id="eb225-132">For a class, properties will usually need getters and setters.</span></span> <span data-ttu-id="eb225-133">Например:</span><span class="sxs-lookup"><span data-stu-id="eb225-133">For example:</span></span>

```fsharp
type Item() =
    member val Id = "" with get,set
    member val Text = "" with get,set

let Run(input: string, item: byref<Item>) =
    let result = Item(Id = input, Text = "Hello from F#!")
    item <- result
```

## <a name="logging"></a><span data-ttu-id="eb225-134">Ведение журналов</span><span class="sxs-lookup"><span data-stu-id="eb225-134">Logging</span></span>
<span data-ttu-id="eb225-135">Для записи выходных данных в [потоковые журналы](../app-service-web/web-sites-streaming-logs-and-console.md) в F# в функции следует использовать аргумент типа `TraceWriter`.</span><span class="sxs-lookup"><span data-stu-id="eb225-135">To log output to your [streaming logs](../app-service-web/web-sites-streaming-logs-and-console.md) in F#, your function should take an argument of type `TraceWriter`.</span></span> <span data-ttu-id="eb225-136">Для согласованности мы советуем назвать этот аргумент `log`.</span><span class="sxs-lookup"><span data-stu-id="eb225-136">For consistency, we recommend this argument is named `log`.</span></span> <span data-ttu-id="eb225-137">Например:</span><span class="sxs-lookup"><span data-stu-id="eb225-137">For example:</span></span>

```fsharp
let Run(blob: string, output: byref<string>, log: TraceWriter) =
    log.Verbose(sprintf "F# Azure Function processed a blob: %s" blob)
    output <- input
```

## <a name="async"></a><span data-ttu-id="eb225-138">Асинхронный режим</span><span class="sxs-lookup"><span data-stu-id="eb225-138">Async</span></span>
<span data-ttu-id="eb225-139">Рабочий процесс `async` можно использовать, но результат должен возвратить `Task`.</span><span class="sxs-lookup"><span data-stu-id="eb225-139">The `async` workflow can be used, but the result needs to return a `Task`.</span></span> <span data-ttu-id="eb225-140">Для этого нужно использовать `Async.StartAsTask`. Например:</span><span class="sxs-lookup"><span data-stu-id="eb225-140">This can be done with `Async.StartAsTask`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage) =
    async {
        return new HttpResponseMessage(HttpStatusCode.OK)
    } |> Async.StartAsTask
```

## <a name="cancellation-token"></a><span data-ttu-id="eb225-141">Токен отмены</span><span class="sxs-lookup"><span data-stu-id="eb225-141">Cancellation Token</span></span>
<span data-ttu-id="eb225-142">Если функция должна правильно обрабатывать завершение работы, ей можно присвоить аргумент [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx).</span><span class="sxs-lookup"><span data-stu-id="eb225-142">If your function needs to handle shutdown gracefully, you can give it a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argument.</span></span> <span data-ttu-id="eb225-143">При этом можно использовать `async`. Например:</span><span class="sxs-lookup"><span data-stu-id="eb225-143">This can be combined with `async`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage, token: CancellationToken)
    let f = async {
        do! Async.Sleep(10)
        return new HttpResponseMessage(HttpStatusCode.OK)
    }
    Async.StartAsTask(f, token)
```

## <a name="importing-namespaces"></a><span data-ttu-id="eb225-144">Импорт пространств имен</span><span class="sxs-lookup"><span data-stu-id="eb225-144">Importing namespaces</span></span>
<span data-ttu-id="eb225-145">Пространства имен можно открывать в обычном режиме.</span><span class="sxs-lookup"><span data-stu-id="eb225-145">Namespaces can be opened in the usual way:</span></span>

```fsharp
open System.Net
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="eb225-146">Следующие пространства имен открываются автоматически:</span><span class="sxs-lookup"><span data-stu-id="eb225-146">The following namespaces are automatically opened:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* <span data-ttu-id="eb225-147">`Microsoft.Azure.WebJobs.Host`.</span><span class="sxs-lookup"><span data-stu-id="eb225-147">`Microsoft.Azure.WebJobs.Host`.</span></span>

## <a name="referencing-external-assemblies"></a><span data-ttu-id="eb225-148">Ссылки на внешние сборки</span><span class="sxs-lookup"><span data-stu-id="eb225-148">Referencing External Assemblies</span></span>
<span data-ttu-id="eb225-149">Аналогичным образом ссылки на сборку платформы можно добавить с помощью директивы `#r "AssemblyName"` .</span><span class="sxs-lookup"><span data-stu-id="eb225-149">Similarly, framework assembly references be added with the `#r "AssemblyName"` directive.</span></span>

```fsharp
#r "System.Web.Http"

open System.Net
open System.Net.Http
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="eb225-150">Следующие сборки автоматически добавляются средой внешнего размещения Функций Azure:</span><span class="sxs-lookup"><span data-stu-id="eb225-150">The following assemblies are automatically added by the Azure Functions hosting environment:</span></span>

* <span data-ttu-id="eb225-151">`mscorlib`,</span><span class="sxs-lookup"><span data-stu-id="eb225-151">`mscorlib`,</span></span>
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* <span data-ttu-id="eb225-152">`System.Net.Http.Formatting`.</span><span class="sxs-lookup"><span data-stu-id="eb225-152">`System.Net.Http.Formatting`.</span></span>

<span data-ttu-id="eb225-153">Кроме того, следующие сборки представляют собой частные случаи, и к ним можно обращаться по простому имени (например, `#r "AssemblyName"`).</span><span class="sxs-lookup"><span data-stu-id="eb225-153">In addition, the following assemblies are special cased and may be referenced by simplename (e.g. `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* <span data-ttu-id="eb225-154">`Microsoft.AspNEt.WebHooks.Common`.</span><span class="sxs-lookup"><span data-stu-id="eb225-154">`Microsoft.AspNEt.WebHooks.Common`.</span></span>

<span data-ttu-id="eb225-155">Если необходимо указать ссылку на закрытую сборку, можно отправить файл сборки в папку `bin`, связанную с функцией, и указать его по имени файла (например, `#r "MyAssembly.dll"`).</span><span class="sxs-lookup"><span data-stu-id="eb225-155">If you need to reference a private assembly, you can upload the assembly file into a `bin` folder relative to your function and reference it by using the file name (e.g.  `#r "MyAssembly.dll"`).</span></span> <span data-ttu-id="eb225-156">Дополнительные сведения о передаче файлов в папку функции см. в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="eb225-156">For information on how to upload files to your function folder, see the following section on package management.</span></span>

## <a name="editor-prelude"></a><span data-ttu-id="eb225-157">Вводная часть редактора</span><span class="sxs-lookup"><span data-stu-id="eb225-157">Editor Prelude</span></span>
<span data-ttu-id="eb225-158">В редакторе, поддерживающем службы компиляции F#, не будут учитываться пространства имен и сборки, которые Функции Azure автоматически включают в себя.</span><span class="sxs-lookup"><span data-stu-id="eb225-158">An editor that supports F# Compiler Services will not be aware of the namespaces and assemblies that Azure Functions automatically includes.</span></span> <span data-ttu-id="eb225-159">Таким образом, может быть полезно включить вводную часть, которая помогает редактору найти используемые сборки и явным образом открыть пространства имен.</span><span class="sxs-lookup"><span data-stu-id="eb225-159">As such, it can be useful to include a prelude that helps the editor find the assemblies you are using, and to explicitly open namespaces.</span></span> <span data-ttu-id="eb225-160">Например:</span><span class="sxs-lookup"><span data-stu-id="eb225-160">For example:</span></span>

```fsharp
#if !COMPILED
#I "../../bin/Binaries/WebJobs.Script.Host"
#r "Microsoft.Azure.WebJobs.Host.dll"
#endif

open Sytem
open Microsoft.Azure.WebJobs.Host

let Run(blob: string, output: byref<string>, log: TraceWriter) =
    ...
```

<span data-ttu-id="eb225-161">При выполнении кода Функции Azure обрабатывают источник, для которого определено `COMPILED`. Таким образом, вводная часть редактора будет игнорироваться.</span><span class="sxs-lookup"><span data-stu-id="eb225-161">When Azure Functions executes your code, it processes the source with `COMPILED` defined, so the editor prelude will be ignored.</span></span>

<a name="package"></a>

## <a name="package-management"></a><span data-ttu-id="eb225-162">Управление пакетами</span><span class="sxs-lookup"><span data-stu-id="eb225-162">Package management</span></span>
<span data-ttu-id="eb225-163">Чтобы использовать пакеты NuGet в функции F#, добавьте файл `project.json` в папку соответствующей функции в файловой системе приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="eb225-163">To use NuGet packages in an F# function, add a `project.json` file to the the function's folder in the function app's file system.</span></span> <span data-ttu-id="eb225-164">Ниже приведен пример файла `project.json`, который добавляет ссылку на пакет NuGet в `Microsoft.ProjectOxford.Face` версии 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="eb225-164">Here is an example `project.json` file that adds a NuGet package reference to `Microsoft.ProjectOxford.Face` version 1.1.0:</span></span>

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

<span data-ttu-id="eb225-165">Поддерживается только версия .NET Framework 4.6, поэтому убедитесь, что ваш файл `project.json` определяет `net46`, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="eb225-165">Only the .NET Framework 4.6 is supported, so make sure that your `project.json` file specifies `net46` as shown here.</span></span>

<span data-ttu-id="eb225-166">При отправке файла `project.json` среда выполнения получает пакеты и автоматически добавляет ссылки на сборки пакетов.</span><span class="sxs-lookup"><span data-stu-id="eb225-166">When you upload a `project.json` file, the runtime gets the packages and automatically adds references to the package assemblies.</span></span> <span data-ttu-id="eb225-167">Добавлять директивы `#r "AssemblyName"` не нужно.</span><span class="sxs-lookup"><span data-stu-id="eb225-167">You don't need to add `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="eb225-168">Просто добавьте необходимые операторы `open` в свой файл `.fsx`.</span><span class="sxs-lookup"><span data-stu-id="eb225-168">Just add the required `open` statements to your `.fsx` file.</span></span>

<span data-ttu-id="eb225-169">Может потребоваться автоматически поместить ссылки на сборки во вводную часть редактора, чтобы улучшить взаимодействие редактора со службами компиляции F#.</span><span class="sxs-lookup"><span data-stu-id="eb225-169">You may wish to put automatically references assemblies in your editor prelude, to improve your editor's interaction with F# Compile Services.</span></span>

### <a name="how-to-add-a-projectjson-file-to-your-azure-function"></a><span data-ttu-id="eb225-170">Добавление файла `project.json` в функцию Azure</span><span class="sxs-lookup"><span data-stu-id="eb225-170">How to add a `project.json` file to your Azure Function</span></span>
1. <span data-ttu-id="eb225-171">Сначала убедитесь, что приложение функции запущено, для чего можно открыть эту функцию на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="eb225-171">Begin by making sure your function app is running, which you can do by opening your function in the Azure portal.</span></span> <span data-ttu-id="eb225-172">Это также обеспечивает доступ к потоковым журналам, где будут отображаться выходные данные установки пакета.</span><span class="sxs-lookup"><span data-stu-id="eb225-172">This also gives access to the streaming logs where package installation output will be displayed.</span></span>
2. <span data-ttu-id="eb225-173">Чтобы отправить файл `project.json` , воспользуйтесь одним из методов, описанных в разделе [Как обновить файлы приложения-функции](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="eb225-173">To upload a `project.json` file, use one of the methods described in [how to update function app files](functions-reference.md#fileupdate).</span></span> <span data-ttu-id="eb225-174">При использовании [непрерывного развертывания для Функций Azure](functions-continuous-deployment.md) можно добавить файл `project.json` в промежуточную ветвь, чтобы поэкспериментировать с ним, прежде чем добавлять в ветвь развертывания.</span><span class="sxs-lookup"><span data-stu-id="eb225-174">If you are using [Continuous Deployment for Azure Functions](functions-continuous-deployment.md), you can add a `project.json` file to your staging branch in order to experiment with it before adding it to your deployment branch.</span></span>
3. <span data-ttu-id="eb225-175">После добавления файла `project.json` в потоковом журнале функции отобразятся выходные данные, как в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="eb225-175">After the `project.json` file is added, you will see output similar to the following example in your function's streaming log:</span></span>

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

## <a name="environment-variables"></a><span data-ttu-id="eb225-176">Переменные среды</span><span class="sxs-lookup"><span data-stu-id="eb225-176">Environment variables</span></span>
<span data-ttu-id="eb225-177">Чтобы получить значение переменной среды или значение параметра приложения, используйте свойство `System.Environment.GetEnvironmentVariable`, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="eb225-177">To get an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, for example:</span></span>

```fsharp
open System.Environment

let Run(timer: TimerInfo, log: TraceWriter) =
    log.Info("Storage = " + GetEnvironmentVariable("AzureWebJobsStorage"))
    log.Info("Site = " + GetEnvironmentVariable("WEBSITE_SITE_NAME"))
```

## <a name="reusing-fsx-code"></a><span data-ttu-id="eb225-178">Повторное использование кода FSX-файла</span><span class="sxs-lookup"><span data-stu-id="eb225-178">Reusing .fsx code</span></span>
<span data-ttu-id="eb225-179">Вы можете использовать код из других файлов `.fsx` с помощью директивы `#load`.</span><span class="sxs-lookup"><span data-stu-id="eb225-179">You can use code from other `.fsx` files by using a `#load` directive.</span></span> <span data-ttu-id="eb225-180">Например:</span><span class="sxs-lookup"><span data-stu-id="eb225-180">For example:</span></span>

`run.fsx`

```fsharp
#load "logger.fsx"

let Run(timer: TimerInfo, log: TraceWriter) =
    mylog log (sprintf "Timer: %s" DateTime.Now.ToString())
```

`logger.fsx`

```fsharp
let mylog(log: TraceWriter, text: string) =
    log.Verbose(text);
```

<span data-ttu-id="eb225-181">Пути, передаваемые в директиве `#load`, определены относительно расположения вашего файла `.fsx`.</span><span class="sxs-lookup"><span data-stu-id="eb225-181">Paths provides to the `#load` directive are relative to the location of your `.fsx` file.</span></span>

* <span data-ttu-id="eb225-182">`#load "logger.fsx"` загружает файл, расположенный в папке функции.</span><span class="sxs-lookup"><span data-stu-id="eb225-182">`#load "logger.fsx"` loads a file located in the function folder.</span></span>
* <span data-ttu-id="eb225-183">`#load "package\logger.fsx"` загружает файл, расположенный в папке `package`, которая содержится в папке функции.</span><span class="sxs-lookup"><span data-stu-id="eb225-183">`#load "package\logger.fsx"` loads a file located in the `package` folder in the function folder.</span></span>
* <span data-ttu-id="eb225-184">`#load "..\shared\mylogger.fsx"` загружает файл, расположенный в папке `shared` на том же уровне, что и папка функции, то есть непосредственно в разделе `wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="eb225-184">`#load "..\shared\mylogger.fsx"` loads a file located in the `shared` folder at the same level as the function folder, that is, directly under `wwwroot`.</span></span>

<span data-ttu-id="eb225-185">Директива `#load` работает только с файлами `.fsx` (скрипт F#), а не с файлами `.fs`.</span><span class="sxs-lookup"><span data-stu-id="eb225-185">The `#load` directive only works with `.fsx` (F# script) files, and not with `.fs` files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb225-186">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="eb225-186">Next steps</span></span>
<span data-ttu-id="eb225-187">Для получения дополнительных сведений см. следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="eb225-187">For more information, see the following resources:</span></span>

* [<span data-ttu-id="eb225-188">Руководство по F#</span><span class="sxs-lookup"><span data-stu-id="eb225-188">F# Guide</span></span>](/dotnet/articles/fsharp/index)
* <span data-ttu-id="eb225-189">[Best Practices for Azure Functions](functions-best-practices.md) (Рекомендации по Функциям Azure)</span><span class="sxs-lookup"><span data-stu-id="eb225-189">[Best Practices for Azure Functions](functions-best-practices.md)</span></span>
* [<span data-ttu-id="eb225-190">Справочник разработчика по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="eb225-190">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="eb225-191">Справочник разработчика C# по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="eb225-191">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="eb225-192">Справочник разработчика NodeJS по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="eb225-192">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="eb225-193">Azure Functions triggers and bindings (Триггеры и привязки в Функциях Azure)</span><span class="sxs-lookup"><span data-stu-id="eb225-193">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)
* [<span data-ttu-id="eb225-194">Тестирование Функций Azure</span><span class="sxs-lookup"><span data-stu-id="eb225-194">Azure Functions testing</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="eb225-195">Масштабирование Функций Azure</span><span class="sxs-lookup"><span data-stu-id="eb225-195">Azure Functions scaling</span></span>](functions-scale.md)

