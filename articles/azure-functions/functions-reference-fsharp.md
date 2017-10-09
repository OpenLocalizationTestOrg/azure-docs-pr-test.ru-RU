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
# <a name="azure-functions-f-developer-reference"></a>Справочник разработчика F# по Функциям Azure
> [!div class="op_single_selector"]
> * [Сценарий C#](functions-reference-csharp.md)
> * [Скрипт F#](functions-reference-fsharp.md)
> * [Node.js](functions-reference-node.md)
> 
> 

F # для функций Azure — это решение для легко запуска небольшие части кода, или «функции», в облаке hello. Данные поступают в функцию F# через аргументы функции. Указанные имена аргументов в `function.json`, и предварительно определенных имен для доступа к, например hello функции ведения журнала и токены отмены.

В этой статье предполагается, что вы прочитали hello [Справочник разработчика Azure функции](functions-reference.md).

## <a name="how-fsx-works"></a>Принципы работы FSX-файла
Файл `.fsx` — это скрипт F#. Он может рассматриваться как проект F#, содержащийся в одном файле. Hello файл содержит оба hello код программы (в данном случае функция Azure) и директивы для управления зависимостями.

При использовании `.fsx` функцию Azure, обычно требуется для сборки являются автоматически включается автоматически, позволяя toofocus на функцию, а не «стандартный» кода hello.

## <a name="binding-tooarguments"></a>Tooarguments привязки
Каждая привязка поддерживает некоторые набор аргументов, как описано в hello [Справочник разработчика Azure функции триггеров и привязки](functions-triggers-bindings.md). Например одним из hello аргумент привязками, которые поддерживает триггер большой двоичный объект является POCO, который может быть выражен в записи F #. Например:

```fsharp
type Item = { Id: string }

let Run(blob: string, output: byref<Item>) =
    let item = { Id = "Some ID" }
    output <- item
```

Для функции Azure на F# понадобится один или несколько аргументов. Когда мы говорим о аргументы функции Azure, мы называем слишком*ввода* аргументы и *вывода* аргументы. Входной аргумент имеет точно соответствует своему названию: входной tooyour Azure функции F #. *Вывода* аргумент — изменяемые данные или `byref<>` аргумент, который служит в качестве как toopass данные обратно *out* этой функции.

В приведенном выше примере hello `blob` выступает в качестве входного аргумента и `output` — это выходной аргумент. Обратите внимание, что мы использовали `byref<>` для `output` (нет hello tooadd нет необходимости `[<Out>]` заметки). С помощью `byref<>` допускает вашей toochange функции, какой аргумент hello записи или объект ссылается на тип.

При записи F # используется в качестве входного типа, определение записей hello должен быть помечен атрибутом `[<CLIMutable>]` чтобы tooset framework Azure функции hello tooallow hello полей соответствующим образом перед передачи записей tooyour функции hello. Механизме hello `[<CLIMutable>]` приводит к возникновению ошибки задания для свойства записи hello. Например:

```fsharp
[<CLIMutable>]
type TestObject =
    { SenderName : string
      Greeting : string }

let Run(req: TestObject, log: TraceWriter) =
    { req with Greeting = sprintf "Hello, %s" req.SenderName }
```

Класс F# можно также использовать для входных и выходных аргументов. Для свойств класса обычно требуются методы получения и задания. Например:

```fsharp
type Item() =
    member val Id = "" with get,set
    member val Text = "" with get,set

let Run(input: string, item: byref<Item>) =
    let result = Item(Id = input, Text = "Hello from F#!")
    item <- result
```

## <a name="logging"></a>Ведение журналов
toolog вывода tooyour [журналы потоковой передачи](../app-service-web/web-sites-streaming-logs-and-console.md) в F #, функция займет аргумент типа `TraceWriter`. Для согласованности мы советуем назвать этот аргумент `log`. Например:

```fsharp
let Run(blob: string, output: byref<string>, log: TraceWriter) =
    log.Verbose(sprintf "F# Azure Function processed a blob: %s" blob)
    output <- input
```

## <a name="async"></a>Асинхронный режим
Hello `async` рабочего процесса может использоваться, но результат hello требуется tooreturn `Task`. Для этого нужно использовать `Async.StartAsTask`. Например:

```fsharp
let Run(req: HttpRequestMessage) =
    async {
        return new HttpResponseMessage(HttpStatusCode.OK)
    } |> Async.StartAsTask
```

## <a name="cancellation-token"></a>Токен отмены
Если функция должен toohandle shutdown надлежащим образом, ему можно присвоить [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) аргумент. При этом можно использовать `async`. Например:

```fsharp
let Run(req: HttpRequestMessage, token: CancellationToken)
    let f = async {
        do! Async.Sleep(10)
        return new HttpResponseMessage(HttpStatusCode.OK)
    }
    Async.StartAsTask(f, token)
```

## <a name="importing-namespaces"></a>Импорт пространств имен
Пространства имен может быть открыт в hello обычным способом:

```fsharp
open System.Net
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

автоматически открываются Hello следующие пространства имен:

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`.

## <a name="referencing-external-assemblies"></a>Ссылки на внешние сборки
Аналогичным образом framework сборки ссылки будут добавлены с hello `#r "AssemblyName"` директивы.

```fsharp
#r "System.Web.Http"

open System.Net
open System.Net.Http
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

Hello следующие сборки автоматически добавляются hello Azure функциями среды размещения.

* `mscorlib`,
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* `System.Net.Http.Formatting`.

Кроме того, hello следующие сборки являются особыми регистре и может быть связан с simplename (например `#r "AssemblyName"`):

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNEt.WebHooks.Common`.

Если вам требуется tooreference закрытой сборки, можно отправить файл сборки hello в `bin` функция относительный tooyour папки и ссылку, ее с помощью hello имя файла (например)  `#r "MyAssembly.dll"`). Сведения о как tooyour функция папки с файлами tooupload hello в следующем разделе пакета управления см.

## <a name="editor-prelude"></a>Вводная часть редактора
Редактор, который поддерживает службы компилятор F # не будет знать о выполняемой hello пространств имен и сборок, которые автоматически включает функции Azure. Таким образом это может быть полезно tooinclude prelude, которая помогает найти hello сборки, которую вы используете редактор hello и tooexplicitly открыть пространства имен. Например:

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

Когда функции Azure выполняет код, он обрабатывает hello источник с `COMPILED` определена, поиск prelude hello редактор будет игнорироваться.

<a name="package"></a>

## <a name="package-management"></a>Управление пакетами
Добавление пакетов NuGet toouse в функции F #, `project.json` функции hello toohello папка файла в файловой системе функция приложение hello. Ниже приведен пример `project.json` файл, который добавляет ссылку на пакет NuGet слишком`Microsoft.ProjectOxford.Face` версии 1.1.0:

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

Только для hello .NET Framework 4.6 поддерживается, поэтому убедитесь, что ваш `project.json` файл определяет `net46` как показано ниже.

При отправке `project.json` файла, hello среда выполнения получает пакеты hello и автоматически добавляет ссылки на toohello пакет сборки. Не требуется tooadd `#r "AssemblyName"` директивы. Просто добавьте необходимые hello `open` tooyour инструкций `.fsx` файла.

Вы хотите tooput автоматически ссылается на сборки в ваш редактор prelude, tooimprove в редакторе взаимодействие со службами компиляции F #.

### <a name="how-tooadd-a-projectjson-file-tooyour-azure-function"></a>Как tooadd `project.json` файл tooyour функция Azure
1. BEGIN, убедившись, что приложение функция выполняется, это можно сделать, открыв функции в hello портал Azure. Это также дает доступ журналы потоковой передачи toohello котором отображаются выходные данные пакета установки.
2. tooupload `project.json` файла следует использовать один из методов hello, описанных в [как tooupdate функция файлов приложения](functions-reference.md#fileupdate). Если вы используете [непрерывного развертывания для функций Azure](functions-continuous-deployment.md), можно добавить `project.json` файл tooyour промежуточных ветвь в порядке tooexperiment с ним перед добавлением его в ветвь tooyour развертывания.
3. После hello `project.json` будет добавлен файл, вы увидите примерно toohello вывода следующий пример в функции потоковая передача журнала:

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

## <a name="environment-variables"></a>Переменные среды
tooget переменной среды или значение параметра приложения, используйте `System.Environment.GetEnvironmentVariable`, например:

```fsharp
open System.Environment

let Run(timer: TimerInfo, log: TraceWriter) =
    log.Info("Storage = " + GetEnvironmentVariable("AzureWebJobsStorage"))
    log.Info("Site = " + GetEnvironmentVariable("WEBSITE_SITE_NAME"))
```

## <a name="reusing-fsx-code"></a>Повторное использование кода FSX-файла
Вы можете использовать код из других файлов `.fsx` с помощью директивы `#load`. Например:

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

Пути предоставляет toohello `#load` директива являются toohello относительное расположение вашей `.fsx` файла.

* `#load "logger.fsx"`загружает файл, расположенный в папке функции hello.
* `#load "package\logger.fsx"`загружает файл, расположенный в hello `package` папки в папке функции hello.
* `#load "..\shared\mylogger.fsx"`загружает файл, расположенный в hello `shared` hello же уровень, что и папка функции hello, перейдите в папку непосредственно под `wwwroot`.

Hello `#load` директива работает только с `.fsx` (F #) в сценарии, а не с `.fs` файлов.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения см. в разделе hello следующие ресурсы:

* [Руководство по F#](/dotnet/articles/fsharp/index)
* [Best Practices for Azure Functions](functions-best-practices.md) (Рекомендации по Функциям Azure)
* [Справочник разработчика по функциям Azure](functions-reference.md)
* [Справочник разработчика C# по функциям Azure](functions-reference-csharp.md)
* [Справочник разработчика NodeJS по функциям Azure](functions-reference-node.md)
* [Azure Functions triggers and bindings (Триггеры и привязки в Функциях Azure)](functions-triggers-bindings.md)
* [Тестирование Функций Azure](functions-test-a-function.md)
* [Масштабирование Функций Azure](functions-scale.md)

