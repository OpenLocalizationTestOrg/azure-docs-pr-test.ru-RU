---
title: "Справочник разработчика функции F # aaaAzure | Документы Microsoft"
description: "Понять, как toodevelop функции Azure с помощью F #."
services: functions
documentationcenter: fsharp
author: sylvanc
manager: jbronsk
editor: 
tags: 
keywords: "служба \"Функции Azure\", функции, обработка событий, веб-перехватчики, динамические вычисления, бессерверная архитектура, F#"
ms.assetid: e60226e5-2630-41d7-9e5b-9f9e5acc8e50
ms.service: functions
ms.devlang: fsharp
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/09/2016
ms.author: syclebsc
ms.openlocfilehash: 1ac366ba6f73d191c582dcd9214b688ef719617a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-f-developer-reference"></a><span data-ttu-id="74baf-104">Справочник разработчика F# по Функциям Azure</span><span class="sxs-lookup"><span data-stu-id="74baf-104">Azure Functions F# Developer Reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="74baf-105">Сценарий C#</span><span class="sxs-lookup"><span data-stu-id="74baf-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="74baf-106">Скрипт F#</span><span class="sxs-lookup"><span data-stu-id="74baf-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="74baf-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="74baf-107">Node.js</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="74baf-108">F # для функций Azure — это решение для легко запуска небольшие части кода, или «функции», в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="74baf-108">F# for Azure Functions is a solution for easily running small pieces of code, or "functions," in hello cloud.</span></span> <span data-ttu-id="74baf-109">Данные поступают в функцию F# через аргументы функции.</span><span class="sxs-lookup"><span data-stu-id="74baf-109">Data flows into your F# function via function arguments.</span></span> <span data-ttu-id="74baf-110">Указанные имена аргументов в `function.json`, и предварительно определенных имен для доступа к, например hello функции ведения журнала и токены отмены.</span><span class="sxs-lookup"><span data-stu-id="74baf-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like hello function logger and cancellation tokens.</span></span>

<span data-ttu-id="74baf-111">В этой статье предполагается, что вы прочитали hello [Справочник разработчика Azure функции](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="74baf-111">This article assumes that you've already read hello [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="how-fsx-works"></a><span data-ttu-id="74baf-112">Принципы работы FSX-файла</span><span class="sxs-lookup"><span data-stu-id="74baf-112">How .fsx works</span></span>
<span data-ttu-id="74baf-113">Файл `.fsx` — это скрипт F#.</span><span class="sxs-lookup"><span data-stu-id="74baf-113">An `.fsx` file is an F# script.</span></span> <span data-ttu-id="74baf-114">Он может рассматриваться как проект F#, содержащийся в одном файле.</span><span class="sxs-lookup"><span data-stu-id="74baf-114">It can be thought of as an F# project that's contained in a single file.</span></span> <span data-ttu-id="74baf-115">Hello файл содержит оба hello код программы (в данном случае функция Azure) и директивы для управления зависимостями.</span><span class="sxs-lookup"><span data-stu-id="74baf-115">hello file contains both hello code for your program (in this case, your Azure Function) and directives for managing dependencies.</span></span>

<span data-ttu-id="74baf-116">При использовании `.fsx` функцию Azure, обычно требуется для сборки являются автоматически включается автоматически, позволяя toofocus на функцию, а не «стандартный» кода hello.</span><span class="sxs-lookup"><span data-stu-id="74baf-116">When you use an `.fsx` for an Azure Function, commonly required assemblies are automatically included for you, allowing you toofocus on hello function rather than "boilerplate" code.</span></span>

## <a name="binding-tooarguments"></a><span data-ttu-id="74baf-117">Tooarguments привязки</span><span class="sxs-lookup"><span data-stu-id="74baf-117">Binding tooarguments</span></span>
<span data-ttu-id="74baf-118">Каждая привязка поддерживает некоторые набор аргументов, как описано в hello [Справочник разработчика Azure функции триггеров и привязки](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="74baf-118">Each binding supports some set of arguments, as detailed in hello [Azure Functions triggers and bindings developer reference](functions-triggers-bindings.md).</span></span> <span data-ttu-id="74baf-119">Например одним из hello аргумент привязками, которые поддерживает триггер большой двоичный объект является POCO, который может быть выражен в записи F #.</span><span class="sxs-lookup"><span data-stu-id="74baf-119">For example, one of hello argument bindings a blob trigger supports is a POCO, which can be expressed using an F# record.</span></span> <span data-ttu-id="74baf-120">Например:</span><span class="sxs-lookup"><span data-stu-id="74baf-120">For example:</span></span>

```fsharp
type Item = { Id: string }

let Run(blob: string, output: byref<Item>) =
    let item = { Id = "Some ID" }
    output <- item
```

<span data-ttu-id="74baf-121">Для функции Azure на F# понадобится один или несколько аргументов.</span><span class="sxs-lookup"><span data-stu-id="74baf-121">Your F# Azure Function will take one or more arguments.</span></span> <span data-ttu-id="74baf-122">Когда мы говорим о аргументы функции Azure, мы называем слишком*ввода* аргументы и *вывода* аргументы.</span><span class="sxs-lookup"><span data-stu-id="74baf-122">When we talk about Azure Functions arguments, we refer too*input* arguments and *output* arguments.</span></span> <span data-ttu-id="74baf-123">Входной аргумент имеет точно соответствует своему названию: входной tooyour Azure функции F #.</span><span class="sxs-lookup"><span data-stu-id="74baf-123">An input argument is exactly what it sounds like: input tooyour F# Azure Function.</span></span> <span data-ttu-id="74baf-124">*Вывода* аргумент — изменяемые данные или `byref<>` аргумент, который служит в качестве как toopass данные обратно *out* этой функции.</span><span class="sxs-lookup"><span data-stu-id="74baf-124">An *output* argument is mutable data or a `byref<>` argument that serves as a way toopass data back *out* of your function.</span></span>

<span data-ttu-id="74baf-125">В приведенном выше примере hello `blob` выступает в качестве входного аргумента и `output` — это выходной аргумент.</span><span class="sxs-lookup"><span data-stu-id="74baf-125">In hello example above, `blob` is an input argument, and `output` is an output argument.</span></span> <span data-ttu-id="74baf-126">Обратите внимание, что мы использовали `byref<>` для `output` (нет hello tooadd нет необходимости `[<Out>]` заметки).</span><span class="sxs-lookup"><span data-stu-id="74baf-126">Notice that we used `byref<>` for `output` (there's no need tooadd hello `[<Out>]` annotation).</span></span> <span data-ttu-id="74baf-127">С помощью `byref<>` допускает вашей toochange функции, какой аргумент hello записи или объект ссылается на тип.</span><span class="sxs-lookup"><span data-stu-id="74baf-127">Using a `byref<>` type allows your function toochange which record or object hello argument refers to.</span></span>

<span data-ttu-id="74baf-128">При записи F # используется в качестве входного типа, определение записей hello должен быть помечен атрибутом `[<CLIMutable>]` чтобы tooset framework Azure функции hello tooallow hello полей соответствующим образом перед передачи записей tooyour функции hello.</span><span class="sxs-lookup"><span data-stu-id="74baf-128">When an F# record is used as an input type, hello record definition must be marked with `[<CLIMutable>]` in order tooallow hello Azure Functions framework tooset hello fields appropriately before passing hello record tooyour function.</span></span> <span data-ttu-id="74baf-129">Механизме hello `[<CLIMutable>]` приводит к возникновению ошибки задания для свойства записи hello.</span><span class="sxs-lookup"><span data-stu-id="74baf-129">Under hello hood, `[<CLIMutable>]` generates setters for hello record properties.</span></span> <span data-ttu-id="74baf-130">Например:</span><span class="sxs-lookup"><span data-stu-id="74baf-130">For example:</span></span>

```fsharp
[<CLIMutable>]
type TestObject =
    { SenderName : string
      Greeting : string }

let Run(req: TestObject, log: TraceWriter) =
    { req with Greeting = sprintf "Hello, %s" req.SenderName }
```

<span data-ttu-id="74baf-131">Класс F# можно также использовать для входных и выходных аргументов.</span><span class="sxs-lookup"><span data-stu-id="74baf-131">An F# class can also be used for both in and out arguments.</span></span> <span data-ttu-id="74baf-132">Для свойств класса обычно требуются методы получения и задания.</span><span class="sxs-lookup"><span data-stu-id="74baf-132">For a class, properties will usually need getters and setters.</span></span> <span data-ttu-id="74baf-133">Например:</span><span class="sxs-lookup"><span data-stu-id="74baf-133">For example:</span></span>

```fsharp
type Item() =
    member val Id = "" with get,set
    member val Text = "" with get,set

let Run(input: string, item: byref<Item>) =
    let result = Item(Id = input, Text = "Hello from F#!")
    item <- result
```

## <a name="logging"></a><span data-ttu-id="74baf-134">Ведение журналов</span><span class="sxs-lookup"><span data-stu-id="74baf-134">Logging</span></span>
<span data-ttu-id="74baf-135">toolog вывода tooyour [журналы потоковой передачи](../app-service-web/web-sites-streaming-logs-and-console.md) в F #, функция займет аргумент типа `TraceWriter`.</span><span class="sxs-lookup"><span data-stu-id="74baf-135">toolog output tooyour [streaming logs](../app-service-web/web-sites-streaming-logs-and-console.md) in F#, your function should take an argument of type `TraceWriter`.</span></span> <span data-ttu-id="74baf-136">Для согласованности мы советуем назвать этот аргумент `log`.</span><span class="sxs-lookup"><span data-stu-id="74baf-136">For consistency, we recommend this argument is named `log`.</span></span> <span data-ttu-id="74baf-137">Например:</span><span class="sxs-lookup"><span data-stu-id="74baf-137">For example:</span></span>

```fsharp
let Run(blob: string, output: byref<string>, log: TraceWriter) =
    log.Verbose(sprintf "F# Azure Function processed a blob: %s" blob)
    output <- input
```

## <a name="async"></a><span data-ttu-id="74baf-138">Асинхронный режим</span><span class="sxs-lookup"><span data-stu-id="74baf-138">Async</span></span>
<span data-ttu-id="74baf-139">Hello `async` рабочего процесса может использоваться, но результат hello требуется tooreturn `Task`.</span><span class="sxs-lookup"><span data-stu-id="74baf-139">hello `async` workflow can be used, but hello result needs tooreturn a `Task`.</span></span> <span data-ttu-id="74baf-140">Для этого нужно использовать `Async.StartAsTask`. Например:</span><span class="sxs-lookup"><span data-stu-id="74baf-140">This can be done with `Async.StartAsTask`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage) =
    async {
        return new HttpResponseMessage(HttpStatusCode.OK)
    } |> Async.StartAsTask
```

## <a name="cancellation-token"></a><span data-ttu-id="74baf-141">Токен отмены</span><span class="sxs-lookup"><span data-stu-id="74baf-141">Cancellation Token</span></span>
<span data-ttu-id="74baf-142">Если функция должен toohandle shutdown надлежащим образом, ему можно присвоить [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) аргумент.</span><span class="sxs-lookup"><span data-stu-id="74baf-142">If your function needs toohandle shutdown gracefully, you can give it a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argument.</span></span> <span data-ttu-id="74baf-143">При этом можно использовать `async`. Например:</span><span class="sxs-lookup"><span data-stu-id="74baf-143">This can be combined with `async`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage, token: CancellationToken)
    let f = async {
        do! Async.Sleep(10)
        return new HttpResponseMessage(HttpStatusCode.OK)
    }
    Async.StartAsTask(f, token)
```

## <a name="importing-namespaces"></a><span data-ttu-id="74baf-144">Импорт пространств имен</span><span class="sxs-lookup"><span data-stu-id="74baf-144">Importing namespaces</span></span>
<span data-ttu-id="74baf-145">Пространства имен может быть открыт в hello обычным способом:</span><span class="sxs-lookup"><span data-stu-id="74baf-145">Namespaces can be opened in hello usual way:</span></span>

```fsharp
open System.Net
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="74baf-146">автоматически открываются Hello следующие пространства имен:</span><span class="sxs-lookup"><span data-stu-id="74baf-146">hello following namespaces are automatically opened:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* <span data-ttu-id="74baf-147">`Microsoft.Azure.WebJobs.Host`.</span><span class="sxs-lookup"><span data-stu-id="74baf-147">`Microsoft.Azure.WebJobs.Host`.</span></span>

## <a name="referencing-external-assemblies"></a><span data-ttu-id="74baf-148">Ссылки на внешние сборки</span><span class="sxs-lookup"><span data-stu-id="74baf-148">Referencing External Assemblies</span></span>
<span data-ttu-id="74baf-149">Аналогичным образом framework сборки ссылки будут добавлены с hello `#r "AssemblyName"` директивы.</span><span class="sxs-lookup"><span data-stu-id="74baf-149">Similarly, framework assembly references be added with hello `#r "AssemblyName"` directive.</span></span>

```fsharp
#r "System.Web.Http"

open System.Net
open System.Net.Http
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="74baf-150">Hello следующие сборки автоматически добавляются hello Azure функциями среды размещения.</span><span class="sxs-lookup"><span data-stu-id="74baf-150">hello following assemblies are automatically added by hello Azure Functions hosting environment:</span></span>

* <span data-ttu-id="74baf-151">`mscorlib`,</span><span class="sxs-lookup"><span data-stu-id="74baf-151">`mscorlib`,</span></span>
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* <span data-ttu-id="74baf-152">`System.Net.Http.Formatting`.</span><span class="sxs-lookup"><span data-stu-id="74baf-152">`System.Net.Http.Formatting`.</span></span>

<span data-ttu-id="74baf-153">Кроме того, hello следующие сборки являются особыми регистре и может быть связан с simplename (например `#r "AssemblyName"`):</span><span class="sxs-lookup"><span data-stu-id="74baf-153">In addition, hello following assemblies are special cased and may be referenced by simplename (e.g. `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* <span data-ttu-id="74baf-154">`Microsoft.AspNEt.WebHooks.Common`.</span><span class="sxs-lookup"><span data-stu-id="74baf-154">`Microsoft.AspNEt.WebHooks.Common`.</span></span>

<span data-ttu-id="74baf-155">Если вам требуется tooreference закрытой сборки, можно отправить файл сборки hello в `bin` функция относительный tooyour папки и ссылку, ее с помощью hello имя файла (например)  `#r "MyAssembly.dll"`).</span><span class="sxs-lookup"><span data-stu-id="74baf-155">If you need tooreference a private assembly, you can upload hello assembly file into a `bin` folder relative tooyour function and reference it by using hello file name (e.g.  `#r "MyAssembly.dll"`).</span></span> <span data-ttu-id="74baf-156">Сведения о как tooyour функция папки с файлами tooupload hello в следующем разделе пакета управления см.</span><span class="sxs-lookup"><span data-stu-id="74baf-156">For information on how tooupload files tooyour function folder, see hello following section on package management.</span></span>

## <a name="editor-prelude"></a><span data-ttu-id="74baf-157">Вводная часть редактора</span><span class="sxs-lookup"><span data-stu-id="74baf-157">Editor Prelude</span></span>
<span data-ttu-id="74baf-158">Редактор, который поддерживает службы компилятор F # не будет знать о выполняемой hello пространств имен и сборок, которые автоматически включает функции Azure.</span><span class="sxs-lookup"><span data-stu-id="74baf-158">An editor that supports F# Compiler Services will not be aware of hello namespaces and assemblies that Azure Functions automatically includes.</span></span> <span data-ttu-id="74baf-159">Таким образом это может быть полезно tooinclude prelude, которая помогает найти hello сборки, которую вы используете редактор hello и tooexplicitly открыть пространства имен.</span><span class="sxs-lookup"><span data-stu-id="74baf-159">As such, it can be useful tooinclude a prelude that helps hello editor find hello assemblies you are using, and tooexplicitly open namespaces.</span></span> <span data-ttu-id="74baf-160">Например:</span><span class="sxs-lookup"><span data-stu-id="74baf-160">For example:</span></span>

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

<span data-ttu-id="74baf-161">Когда функции Azure выполняет код, он обрабатывает hello источник с `COMPILED` определена, поиск prelude hello редактор будет игнорироваться.</span><span class="sxs-lookup"><span data-stu-id="74baf-161">When Azure Functions executes your code, it processes hello source with `COMPILED` defined, so hello editor prelude will be ignored.</span></span>

<a name="package"></a>

## <a name="package-management"></a><span data-ttu-id="74baf-162">Управление пакетами</span><span class="sxs-lookup"><span data-stu-id="74baf-162">Package management</span></span>
<span data-ttu-id="74baf-163">Добавление пакетов NuGet toouse в функции F #, `project.json` функции hello toohello папка файла в файловой системе функция приложение hello.</span><span class="sxs-lookup"><span data-stu-id="74baf-163">toouse NuGet packages in an F# function, add a `project.json` file toohello hello function's folder in hello function app's file system.</span></span> <span data-ttu-id="74baf-164">Ниже приведен пример `project.json` файл, который добавляет ссылку на пакет NuGet слишком`Microsoft.ProjectOxford.Face` версии 1.1.0:</span><span class="sxs-lookup"><span data-stu-id="74baf-164">Here is an example `project.json` file that adds a NuGet package reference too`Microsoft.ProjectOxford.Face` version 1.1.0:</span></span>

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

<span data-ttu-id="74baf-165">Только для hello .NET Framework 4.6 поддерживается, поэтому убедитесь, что ваш `project.json` файл определяет `net46` как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="74baf-165">Only hello .NET Framework 4.6 is supported, so make sure that your `project.json` file specifies `net46` as shown here.</span></span>

<span data-ttu-id="74baf-166">При отправке `project.json` файла, hello среда выполнения получает пакеты hello и автоматически добавляет ссылки на toohello пакет сборки.</span><span class="sxs-lookup"><span data-stu-id="74baf-166">When you upload a `project.json` file, hello runtime gets hello packages and automatically adds references toohello package assemblies.</span></span> <span data-ttu-id="74baf-167">Не требуется tooadd `#r "AssemblyName"` директивы.</span><span class="sxs-lookup"><span data-stu-id="74baf-167">You don't need tooadd `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="74baf-168">Просто добавьте необходимые hello `open` tooyour инструкций `.fsx` файла.</span><span class="sxs-lookup"><span data-stu-id="74baf-168">Just add hello required `open` statements tooyour `.fsx` file.</span></span>

<span data-ttu-id="74baf-169">Вы хотите tooput автоматически ссылается на сборки в ваш редактор prelude, tooimprove в редакторе взаимодействие со службами компиляции F #.</span><span class="sxs-lookup"><span data-stu-id="74baf-169">You may wish tooput automatically references assemblies in your editor prelude, tooimprove your editor's interaction with F# Compile Services.</span></span>

### <a name="how-tooadd-a-projectjson-file-tooyour-azure-function"></a><span data-ttu-id="74baf-170">Как tooadd `project.json` файл tooyour функция Azure</span><span class="sxs-lookup"><span data-stu-id="74baf-170">How tooadd a `project.json` file tooyour Azure Function</span></span>
1. <span data-ttu-id="74baf-171">BEGIN, убедившись, что приложение функция выполняется, это можно сделать, открыв функции в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="74baf-171">Begin by making sure your function app is running, which you can do by opening your function in hello Azure portal.</span></span> <span data-ttu-id="74baf-172">Это также дает доступ журналы потоковой передачи toohello котором отображаются выходные данные пакета установки.</span><span class="sxs-lookup"><span data-stu-id="74baf-172">This also gives access toohello streaming logs where package installation output will be displayed.</span></span>
2. <span data-ttu-id="74baf-173">tooupload `project.json` файла следует использовать один из методов hello, описанных в [как tooupdate функция файлов приложения](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="74baf-173">tooupload a `project.json` file, use one of hello methods described in [how tooupdate function app files](functions-reference.md#fileupdate).</span></span> <span data-ttu-id="74baf-174">Если вы используете [непрерывного развертывания для функций Azure](functions-continuous-deployment.md), можно добавить `project.json` файл tooyour промежуточных ветвь в порядке tooexperiment с ним перед добавлением его в ветвь tooyour развертывания.</span><span class="sxs-lookup"><span data-stu-id="74baf-174">If you are using [Continuous Deployment for Azure Functions](functions-continuous-deployment.md), you can add a `project.json` file tooyour staging branch in order tooexperiment with it before adding it tooyour deployment branch.</span></span>
3. <span data-ttu-id="74baf-175">После hello `project.json` будет добавлен файл, вы увидите примерно toohello вывода следующий пример в функции потоковая передача журнала:</span><span class="sxs-lookup"><span data-stu-id="74baf-175">After hello `project.json` file is added, you will see output similar toohello following example in your function's streaming log:</span></span>

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

## <a name="environment-variables"></a><span data-ttu-id="74baf-176">Переменные среды</span><span class="sxs-lookup"><span data-stu-id="74baf-176">Environment variables</span></span>
<span data-ttu-id="74baf-177">tooget переменной среды или значение параметра приложения, используйте `System.Environment.GetEnvironmentVariable`, например:</span><span class="sxs-lookup"><span data-stu-id="74baf-177">tooget an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, for example:</span></span>

```fsharp
open System.Environment

let Run(timer: TimerInfo, log: TraceWriter) =
    log.Info("Storage = " + GetEnvironmentVariable("AzureWebJobsStorage"))
    log.Info("Site = " + GetEnvironmentVariable("WEBSITE_SITE_NAME"))
```

## <a name="reusing-fsx-code"></a><span data-ttu-id="74baf-178">Повторное использование кода FSX-файла</span><span class="sxs-lookup"><span data-stu-id="74baf-178">Reusing .fsx code</span></span>
<span data-ttu-id="74baf-179">Вы можете использовать код из других файлов `.fsx` с помощью директивы `#load`.</span><span class="sxs-lookup"><span data-stu-id="74baf-179">You can use code from other `.fsx` files by using a `#load` directive.</span></span> <span data-ttu-id="74baf-180">Например:</span><span class="sxs-lookup"><span data-stu-id="74baf-180">For example:</span></span>

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

<span data-ttu-id="74baf-181">Пути предоставляет toohello `#load` директива являются toohello относительное расположение вашей `.fsx` файла.</span><span class="sxs-lookup"><span data-stu-id="74baf-181">Paths provides toohello `#load` directive are relative toohello location of your `.fsx` file.</span></span>

* <span data-ttu-id="74baf-182">`#load "logger.fsx"`загружает файл, расположенный в папке функции hello.</span><span class="sxs-lookup"><span data-stu-id="74baf-182">`#load "logger.fsx"` loads a file located in hello function folder.</span></span>
* <span data-ttu-id="74baf-183">`#load "package\logger.fsx"`загружает файл, расположенный в hello `package` папки в папке функции hello.</span><span class="sxs-lookup"><span data-stu-id="74baf-183">`#load "package\logger.fsx"` loads a file located in hello `package` folder in hello function folder.</span></span>
* <span data-ttu-id="74baf-184">`#load "..\shared\mylogger.fsx"`загружает файл, расположенный в hello `shared` hello же уровень, что и папка функции hello, перейдите в папку непосредственно под `wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="74baf-184">`#load "..\shared\mylogger.fsx"` loads a file located in hello `shared` folder at hello same level as hello function folder, that is, directly under `wwwroot`.</span></span>

<span data-ttu-id="74baf-185">Hello `#load` директива работает только с `.fsx` (F #) в сценарии, а не с `.fs` файлов.</span><span class="sxs-lookup"><span data-stu-id="74baf-185">hello `#load` directive only works with `.fsx` (F# script) files, and not with `.fs` files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74baf-186">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="74baf-186">Next steps</span></span>
<span data-ttu-id="74baf-187">Дополнительные сведения см. в разделе hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="74baf-187">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="74baf-188">Руководство по F#</span><span class="sxs-lookup"><span data-stu-id="74baf-188">F# Guide</span></span>](/dotnet/articles/fsharp/index)
* <span data-ttu-id="74baf-189">[Best Practices for Azure Functions](functions-best-practices.md) (Рекомендации по Функциям Azure)</span><span class="sxs-lookup"><span data-stu-id="74baf-189">[Best Practices for Azure Functions](functions-best-practices.md)</span></span>
* [<span data-ttu-id="74baf-190">Справочник разработчика по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="74baf-190">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="74baf-191">Справочник разработчика C# по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="74baf-191">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="74baf-192">Справочник разработчика NodeJS по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="74baf-192">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="74baf-193">Azure Functions triggers and bindings (Триггеры и привязки в Функциях Azure)</span><span class="sxs-lookup"><span data-stu-id="74baf-193">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)
* [<span data-ttu-id="74baf-194">Тестирование Функций Azure</span><span class="sxs-lookup"><span data-stu-id="74baf-194">Azure Functions testing</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="74baf-195">Масштабирование Функций Azure</span><span class="sxs-lookup"><span data-stu-id="74baf-195">Azure Functions scaling</span></span>](functions-scale.md)

