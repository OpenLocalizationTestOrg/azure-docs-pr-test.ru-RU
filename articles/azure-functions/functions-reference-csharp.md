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
# <a name="azure-functions-c-script-developer-reference"></a>Справочник разработчика скриптов C# по функциям Azure
> [!div class="op_single_selector"]
> * [Сценарий C#](functions-reference-csharp.md)
> * [Скрипт F#](functions-reference-fsharp.md)
> * [Node.js](functions-reference-node.md)
>
>

Hello качества скрипт C# для функций Azure основан на hello Azure SDK веб-заданий. Данные поступают в функцию C# через аргументы метода. Указанные имена аргументов в `function.json`, и предварительно определенных имен для доступа к, например hello функции ведения журнала и токены отмены.

В этой статье предполагается, что вы прочитали hello [Справочник разработчика Azure функции](functions-reference.md).

Дополнительные сведения об использовании библиотек классов C# с помощью Функций Azure см. в [этой статье](functions-dotnet-class-library.md).

## <a name="how-csx-works"></a>Как работает формат CSX
Hello `.csx` формат позволяет toowrite менее «стандартный» и сосредоточиться на запись только функции C#. Включить все ссылки на сборки и пространства имен в начале файла hello hello обычным образом. а затем вместо помещения всего кода в пространство имен и класс просто определите метод `Run`. Если вам требуется tooinclude всем классам для объектов объект среды CLR (POCO), можно включить класса внутри обычного toodefine экземпляр hello того же файла.   

## <a name="binding-tooarguments"></a>Tooarguments привязки
Hello различных привязок, связанных tooa C# функция через hello `name` свойство в hello *function.json* конфигурации. У каждой привязки есть собственные поддерживаемые типы. Например, триггер больших двоичных объектов может поддерживать строку, POCO или CloudBlockBlob. Hello поддерживаемые типы описаны в hello справочник для каждой привязки. Для каждого свойства объекта POCO нужно определить метод задания и считывания.

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

## <a name="using-method-return-value-for-output-binding"></a>Использование возвращаемого значения метода для выходной привязки

Возвращаемое значение метода можно использовать для привязки выходные данные с помощью имени hello `$return` в *function.json*:

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

## <a name="writing-multiple-output-values"></a>Написание нескольких значений выходных данных

Вывод нескольких значений tooan toowrite привязку, использовать hello [ `ICollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) или [ `IAsyncCollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) типов. Эти типы предназначены только для записи коллекции, записать toohello выходные данные привязки завершении метода hello.

В следующем примере записываются несколько сообщений очереди с помощью `ICollector`:

```csharp
public static void Run(ICollector<string> myQueueItem, TraceWriter log)
{
    myQueueItem.Add("Hello");
    myQueueItem.Add("World!");
}
```

## <a name="logging"></a>Ведение журналов
toolog выходные данные журналов потоковой передачи tooyour в C#, включите аргумент типа `TraceWriter`. Рекомендуем присвоить ему имя `log`. Не используйте `Console.Write` в Функциях Azure. 

`TraceWriter`определен в hello [SDK веб-заданий Azure](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs). Здравствуйте, уровень ведения журнала для `TraceWriter` можно настроить в [узла\.json].

```csharp
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

## <a name="async"></a>Асинхронный режим
использовать toomake асинхронно, функции hello `async` ключевое слово и возврат `Task` объекта.

```csharp
public async static Task ProcessQueueMessageAsync(
        string blobName,
        Stream blobInput,
        Stream blobOutput)
{
    await blobInput.CopyToAsync(blobOutput, 4096, token);
}
```

## <a name="cancellation-token"></a>Токен отмены
Для некоторых операций необходимо выполнить нормальное завершение работы. Хотя всегда наиболее toowrite код, который может обрабатывать аварийное завершение работы, в случаях, где нужно toohandle нормальное завершение работы запросов, определить [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) типом аргумента.  Объект `CancellationToken` предоставляется toosignal срабатывание завершение работы узла.

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

## <a name="importing-namespaces"></a>Импорт пространств имен
Если вам требуется tooimport пространства имен, это можно сделать как обычно с hello `using` предложения.

```csharp
using System.Net;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

Hello следующие пространства имен автоматически импортируются и поэтому являются необязательными:

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`

## <a name="referencing-external-assemblies"></a>Ссылки на внешние сборки
Для сборок framework добавить ссылки с помощью hello `#r "AssemblyName"` директивы.

```csharp
#r "System.Web.Http"

using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

Hello следующие сборки автоматически добавляются hello Azure функциями среды размещения.

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

Hello следующие сборки может быть ссылается простое имя (например, `#r "AssemblyName"`):

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNet.WebHooks.Common`
* `Microsoft.Azure.NotificationHubs`

## <a name="referencing-custom-assemblies"></a>Ссылки на пользовательские сборки

tooreference пользовательской сборки, можно использовать любой *общего* сборки или *закрытый* сборки:
- Общие сборки совместно используют все функции в приложении-функции. tooreference пользовательской сборки, отправка hello сборки tooyour функции приложения, такие как в `bin` папки в корневом каталоге приложения функции hello. 
- Закрытые сборки входят в контекст указанной функции и поддерживают загрузку неопубликованных приложений разных версий. Закрытые сборки должны быть отправлены в `bin` папку в каталоге функции hello. Ссылку можно с помощью имени файла hello, такие как `#r "MyAssembly.dll"`. 

Сведения о как tooyour функция папки с файлами tooupload hello в следующем разделе пакета управления см.

### <a name="watched-directories"></a>Каталоги отслеживания

tooassemblies изменения автоматически наступление Hello каталог, содержащий файл скрипта функции hello. toowatch изменить сборки в других каталогах, добавьте их toohello `watchDirectories` списка в [узла\.json].

## <a name="using-nuget-packages"></a>Использование пакетов NuGet
отправить пакеты NuGet toouse в функции C# *project.json* toohello функция папка файла в файловой системе функция приложение hello. Ниже приведен пример *project.json* файл, который добавляет ссылку tooMicrosoft.ProjectOxford.Face версии 1.1.0:

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

Только для hello .NET Framework 4.6 поддерживается, поэтому убедитесь, что ваш *project.json* файл определяет `net46` как показано ниже.

При отправке *project.json* файла, hello среда выполнения получает пакеты hello и автоматически добавляет ссылки на toohello пакет сборки. Не требуется tooadd `#r "AssemblyName"` директивы. toouse hello типы, определенные в пакетах NuGet hello, добавьте необходимые hello `using` tooyour инструкций *run.csx* файла 

В среде выполнения функции hello, восстановление NuGet работает путем сравнения `project.json` и `project.lock.json`. Если дата и время создания файлов hello hello **не** совпадение, выполняется восстановление NuGet и NuGet загружает обновленные пакеты. Тем не менее, если hello Дата и время создания файлов hello **сделать** соответствия NuGet не выполняет восстановление. Таким образом `project.lock.json` не следует развертывать как он вызывает восстановление пакета NuGet tooskip. tooavoid развертывание hello блокировки файлов, добавьте hello `project.lock.json` toohello `.gitignore` файла.

toouse настраиваемого канала NuGet, укажите hello веб-канала в *Nuget.Config* файл в корневом каталоге приложения функции hello. Дополнительные сведения см. в статье [Configuring NuGet behavior](/nuget/consume-packages/configuring-nuget-behavior) (Настройка поведения NuGet).

### <a name="using-a-projectjson-file"></a>Использование файла project.json
1. Откройте функции hello в hello портал Azure. Hello заносит в журнал выходные данные установки пакета вкладка отображает hello.
2. tooupload файл project.json, воспользуйтесь одним из описанных hello hello [как tooupdate функция файлов приложения](functions-reference.md#fileupdate) раздела Справочник разработчика Azure функции hello.
3. После hello *project.json* передачи файла см. в разделе, выходные данные как следующий пример в функции hello потоковая передача журналов:

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
tooget переменной среды или значение параметра приложения, используйте `System.Environment.GetEnvironmentVariable`, как показано в следующем примере кода hello:

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

## <a name="reusing-csx-code"></a>Повторное использование кода CSX
В файле *run.csx* можно использовать классы и методы, определенные в других *CSX*-файлах. toodo, использовать `#load` директивы в вашей *run.csx* файла. В следующем примере hello, подпрограмма ведения журнала с именем `MyLogger` совместно в *myLogger.csx* и загружаются в *run.csx* с помощью hello `#load` директиву:

Пример *run.csx*:

```csharp
#load "mylogger.csx"

public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Verbose($"Log by run.csx: {DateTime.Now}");
    MyLogger(log, $"Log by MyLogger: {DateTime.Now}");
}
```

Пример *mylogger.csx*:

```csharp
public static void MyLogger(TraceWriter log, string logtext)
{
    log.Verbose(logtext);
}
```

С помощью общего *.csx* распространенный подход при необходимости toostrongly ввести аргументов между функциями, используя объект POCO. В следующий упрощенный пример hello, триггер HTTP и очереди триггера используют объект POCO с именем `Order` hello порядок toostrongly тип данных:

Пример файла *run.csx* для триггера HTTP:

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

Пример файла *run.csx* для триггера очереди:

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

Пример файла *order.csx*:

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

Можно использовать относительный путь с hello `#load` директиву:

* `#load "mylogger.csx"`загружает файл, расположенный в папке функции hello.
* `#load "loadedfiles\mylogger.csx"`загружает файл, расположенный в папке в папке функции hello.
* `#load "..\shared\mylogger.csx"`загружает файл, расположенный в папке на hello же уровня, что и папка функции hello, т. е непосредственно под *wwwroot*.

Hello `#load` директива работает только с *.csx* (C#) в сценарии, не с *.cs* файлов.

<a name="imperative-bindings"></a> 

## <a name="binding-at-runtime-via-imperative-bindings"></a>Привязка в среде выполнения с помощью императивных привязок

В C# и других языков .NET, можно использовать [императивного](https://en.wikipedia.org/wiki/Imperative_programming) шаблон привязки, так как противоположность toohello [ *декларативный* ](https://en.wikipedia.org/wiki/Declarative_programming) привязок в *function.json*. Принудительный привязки полезно в том случае, если параметры привязки должны toobe вычислено во время выполнения, а не конструктора. С этим шаблоном можно привязать toosupported ввода и вывода привязки на лету в коде функции.

Определите принудительную привязку следующим образом.

- **Не** добавляйте запись для нужных императивных привязок в файл *function.json*.
- Передайте входной параметр [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) или [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).
- Используйте следующие C# шаблон tooperform hello привязки данных hello.

```cs
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
    ...
}
```

где `BindingTypeAttribute` является атрибутом hello .NET, который определяет пользовательскую привязку, и `T` является входной или выходной тип, поддерживаемый этим типом привязки "hello". `T` также не может быть параметром типа `out` (например, `out JObject`). Например, выходная привязка таблицы мобильных приложений поддерживает [шесть выходных типов](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), но для `T` можно использовать только [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) или [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs).

Привет, следующий пример кода создает [привязка для вывода BLOB-объекта хранилища](functions-bindings-storage-blob.md#using-a-blob-output-binding) с большим двоичным объектом путь, определенный во время выполнения, затем записывает большой двоичный объект toohello строки.

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

[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) определяет hello [BLOB-объекта хранилища](functions-bindings-storage-blob.md) входного или выходного привязки, и [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) является поддерживаемой выходной тип привязки.
Возвращает, hello кода hello приложения по умолчанию hello строка подключения учетной записи хранения (который является `AzureWebJobsStorage`). Можно указать toouse параметр пользовательского приложения путем добавления [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) и передачи массива атрибутов hello в `BindAsync<T>()`. Например,

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

Hello следующей таблице перечислены атрибуты hello .NET для каждой привязки тип и hello пакетов, в которых они определены.

> [!div class="mx-codeBreakAll"]
| Привязка | Атрибут | Ссылка, которую нужно добавить |
|------|------|------|
| Cosmos DB | [`Microsoft.Azure.WebJobs.DocumentDBAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.DocumentDB"` |
| Концентраторы событий | [`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs) | `#r "Microsoft.Azure.Jobs.ServiceBus"` |
| Мобильные приложения | [`Microsoft.Azure.WebJobs.MobileTableAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.MobileApps"` |
| Центры уведомлений | [`Microsoft.Azure.WebJobs.NotificationHubAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.NotificationHubs"` |
| Служебная шина | [`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs) | `#r "Microsoft.Azure.WebJobs.ServiceBus"` |
| Очередь службы хранилища | [`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) | |
| Большой двоичный объект службы хранилища | [`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) | |
| Таблица службы хранилища | [`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) | |
| Twilio | [`Microsoft.Azure.WebJobs.TwilioSmsAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.Twilio"` |



## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения см. в разделе hello следующие ресурсы:

* [Best Practices for Azure Functions](functions-best-practices.md) (Рекомендации по Функциям Azure)
* [Справочник разработчика по функциям Azure](functions-reference.md)
* [Справочник разработчика F# по функциям Azure](functions-reference-fsharp.md)
* [Справочник разработчика NodeJS по функциям Azure](functions-reference-node.md)
* [Azure Functions triggers and bindings (Триггеры и привязки в Функциях Azure)](functions-triggers-bindings.md)

[host\.json]: https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json
