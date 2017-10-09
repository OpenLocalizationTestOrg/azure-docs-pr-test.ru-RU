---
title: "aaaUsing .NET класса библиотеки, используя функции Azure | Документы Microsoft"
description: "Узнайте, как использовать tooauthor библиотеки классов .NET для функций Azure"
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "функции azure, функции, обработка событий, динамические вычисления, независимая архитектура"
ms.assetid: 9f5db0c2-a88e-4fa8-9b59-37a7096fc828
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/09/2017
ms.author: donnam
ms.openlocfilehash: 4e0fd954b554006ba1d8ecc47403a9fb1c67c3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-net-class-libraries-with-azure-functions"></a>Использование библиотек классов .NET с помощью Функций Azure

Кроме файлов tooscript, функции Azure поддерживает публикацию hello реализацию одного или нескольких функций библиотеки классов. Мы рекомендуем использовать hello [Azure функции 2017 г. набор средств Visual Studio](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).

## <a name="prerequisites"></a>Предварительные требования 

В этой статье имеет hello следующие предварительные требования:

- [Предварительная версия Visual Studio 2017 15.3](https://www.visualstudio.com/vs/preview/). Установка рабочих нагрузок hello **ASP.NET и веб-разработки** и **разработки Azure**.
- [Инструменты Функций Azure для Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=AndrewBHall-MSFT.AzureFunctionToolsforVisualStudio2017).

## <a name="functions-class-library-project"></a>Проект библиотеки классов функций

Создайте проект Функций Azure в Visual Studio. Hello новый шаблон проекта создает файлы hello *host.json* и *local.settings.json*. Вы можете [настроить параметры среды выполнения Функций Azure в файле host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json). 

файл Hello *local.settings.json* сохраняют параметры приложения, строки подключения и параметры для средства основных функций Azure. toolearn Дополнительные сведения о его структуры, в разделе [кода и тестирования функций Azure локально](functions-run-local.md#local-settings).

### <a name="functionname-attribute"></a>Атрибут FunctionName

атрибут Hello [ `FunctionNameAttribute` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) помечает метод как точку входа функции. Он должен иметь только один триггер и 0 или более входных и выходных привязок.

### <a name="conversion-toofunctionjson"></a>Преобразование toofunction.json

При построении проекта служб Azure функции, он создает файл `function.json` в каталоге hello сопоставления имени функции hello определяется `[FunctionName]`. Указывает, триггеры и привязки и файл сборки проекта toohello точек.

Это преобразование выполняется пакет NuGet hello [Microsoft\.NET\.Sdk\.функции](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions). Источник Hello доступен в репозитории GitHub hello [azure\-функции\-vs\-построения\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).

## <a name="triggers-and-bindings"></a>Триггеры и привязки

Hello следующей таблице перечислены триггеры hello и привязок, доступных в проекте библиотеки классов функций Azure. Все атрибуты находятся в пространстве имен hello `Microsoft.Azure.WebJobs`.

| Привязка | Атрибут | Пакет NuGet |
|------   | ------    | ------        |
| [Привязки триггера, входные и выходные привязки для хранилища BLOB-объектов](#blob-storage) | [BlobAttribute], [StorageAccountAttribute] | [Microsoft.Azure.WebJobs] | [Хранилище BLOB-объектов] |
| [Входная и выходная привязка для Cosmos DB](#cosmos-db) | [DocumentDBAttribute] | [Microsoft.Azure.WebJobs.Extensions.DocumentDB] | 
| [Привязки триггера и выходные привязки для концентраторов событий](#event-hub) | [EventHubTriggerAttribute], [EventHubAttribute] | [Microsoft.Azure.WebJobs.ServiceBus] |
| [Входная и выходная привязка для внешнего файла](#api-hub) | [ApiHubFileAttribute] | [Microsoft.Azure.WebJobs.Extensions.ApiHub] |
| [Триггер HTTP и веб-перехватчика](#http) | [HttpTriggerAttribute] | [Microsoft.Azure.WebJobs.Extensions.Http] |
| [Входные и выходные привязки для мобильных приложений](#mobile-apps) | [MobileTableAttribute] | [Microsoft.Azure.WebJobs.Extensions.MobileApps] | 
| [Выходные привязки для Центров уведомлений](#nh) | [NotificationHubAttribute] | [Microsoft.Azure.WebJobs.Extensions.NotificationHubs] | 
| [Привязки триггера и выходные привязки для хранилища очередей](#queue) | [QueueAttribute], [StorageAccountAttribute] | [Microsoft.Azure.WebJobs] | 
| [Выходные привязки SendGrid](#sendgrid) | [SendGridAttribute] | [Microsoft.Azure.WebJobs.Extensions.SendGrid] | 
| [Привязки триггера и выходные привязки для служебной шины](#service-bus) | [ServiceBusAttribute], [ServiceBusAccountAttribute] | [Microsoft.Azure.WebJobs.ServiceBus]
| [Входные и выходные привязки для хранилища таблиц](#table) | [TableAttribute], [StorageAccountAttribute] | [Microsoft.Azure.WebJobs] | 
| [Триггер таймера](#timer) | [TimerTriggerAttribute] | [Microsoft.Azure.WebJobs.Extensions] | 
| [Выходные привязки Twilio](#twilio) | [TwilioSmsAttribute] | [Microsoft.Azure.WebJobs.Extensions.Twilio] | 

<a name="blob-storage"></a>

### <a name="blob-storage-trigger-input-and-output-bindings"></a>Привязки триггера, входные и выходные привязки для хранилища BLOB-объектов

Функции Azure поддерживают привязки триггера, а также входные и выходные привязки для хранилища BLOB-объектов Azure. Дополнительные сведения о выражениях привязки и метаданных см. в статье [Привязки хранилища BLOB-объектов для Функций Azure](functions-bindings-storage-blob.md).

Большой двоичный объект триггер определен с hello `[BlobTrigger]` атрибута. Можно использовать атрибут hello `[StorageAccount]` учетной записи хранилища toodefine hello, используемый всей функции или классом.

```csharp
[StorageAccount("AzureWebJobsStorage")]
[FunctionName("BlobTriggerCSharp")]        
public static void Run([BlobTrigger("samples-workitems/{name}")] Stream myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

BLOB-объектов входных и выходных данных определяются с помощью hello `[Blob]` атрибута вместе с `FileAccess` параметр, указывающий, чтения или записи. Здравствуйте, следующий пример использует триггер больших двоичных объектов и больших двоичных объектов выходной привязки.

```csharp
[FunctionName("ResizeImage")]
[StorageAccount("AzureWebJobsStorage")]
public static void Run(
    [BlobTrigger("sample-images/{name}")] Stream image, 
    [Blob("sample-images-sm/{name}", FileAccess.Write)] Stream imageSmall, 
    [Blob("sample-images-md/{name}", FileAccess.Write)] Stream imageMedium)
{
    var imageBuilder = ImageResizer.ImageBuilder.Current;
    var size = imageDimensionsTable[ImageSize.Small];

    imageBuilder.Build(image, imageSmall,
        new ResizeSettings(size.Item1, size.Item2, FitMode.Max, null), false);

    image.Position = 0;
    size = imageDimensionsTable[ImageSize.Medium];

    imageBuilder.Build(image, imageMedium,
        new ResizeSettings(size.Item1, size.Item2, FitMode.Max, null), false);
}

public enum ImageSize { ExtraSmall, Small, Medium }

private static Dictionary<ImageSize, (int, int)> imageDimensionsTable = new Dictionary<ImageSize, (int, int)>() {
    { ImageSize.ExtraSmall, (320, 200) },
    { ImageSize.Small,      (640, 400) },
    { ImageSize.Medium,     (800, 600) }
};
```        

<a name="cosmos-db"></a>

### <a name="cosmos-db-input-and-output-bindings"></a>Входная и выходная привязка для Cosmos DB

Функции Azure поддерживают входные и выходные привязки для Cosmos DB. toolearn Дополнительные сведения о функции hello привязки Cosmos DB hello, в разделе [Azure DB Cosmos функции привязки](functions-bindings-documentdb.md).

toobind tooa Cosmos DB документа, используйте атрибут hello `[DocumentDB]` в пакет NuGet hello [Microsoft.Azure.WebJobs.Extensions.DocumentDB]. Следующий пример Hello имеет триггер очереди и привязка для вывода API DocumentDB:

```csharp
[FunctionName("QueueToDocDB")]        
public static void Run(
    [QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, 
    [DocumentDB("ToDoList", "Items", ConnectionStringSetting = "DocDBConnection")] out dynamic document)
{
    document = new { Text = myQueueItem, id = Guid.NewGuid() };
}

```

<a name="event-hub"></a>

### <a name="event-hubs-trigger-and-output"></a>Привязки триггера и выходные привязки для концентраторов событий

Функции Azure поддерживают привязки триггера и выходные привязки для концентраторов событий Azure. Дополнительные сведения см. в статье [Привязки концентратора событий функций Azure](functions-bindings-event-hubs.md).

Здравствуйте, типы `[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` и `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]` в пакете NuGet hello [Microsoft.Azure.WebJobs.ServiceBus]. 

Hello следующем примере триггер концентратора событий:

```csharp
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

Hello следующий пример состоит из концентратора событий выходных данных, с помощью возвращаемого значения метода hello в качестве выходных данных hello.

```csharp
[FunctionName("EventHubOutput")]
[return: EventHub("outputEventHubMessage", Connection = "EventHubConnection")]
public static string Run([TimerTrigger("0 */5 * * * *")] TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
    return $"{DateTime.Now}";
}
```

<a name="api-hub"></a>

### <a name="external-file-input-and-output"></a>Входная и выходная привязка для внешнего файла

Функции Azure поддерживают привязки триггера, а также входные и выходные привязки для внешних файлов, таких как Google Drive, Dropbox и OneDrive. toolearn более, в разделе [привязки внешнего файла Azure функции](functions-bindings-external-file.md). Здравствуйте, атрибуты `[ExternalFileTrigger]` и `[ExternalFile]` в пакете NuGet hello [Microsoft.Azure.WebJobs.Extensions.ApiHub].

Hello в следующем примере C# демонстрируется внешний файл входной и выходной привязки. код копирует Hello hello входной файл toohello выходного файла.

```csharp
[StorageAccount("MyStorageConnection")]
[FunctionName("ExternalFile")]
[return: ApiHubFile("MyFileConnection", "samples-workitems/{queueTrigger}-Copy", FileAccess.Write)]
public static string Run([QueueTrigger("myqueue-items")] string myQueueItem, 
    [ApiHubFile("MyFileConnection", "samples-workitems/{queueTrigger}", FileAccess.Read)] string myInputFile, 
    TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    return myInputFile;
}
```

<a name="http"></a>

### <a name="http-and-webhooks"></a>HTTP и вызовы webhook

Используйте hello `HttpTrigger` атрибута toodefine HTTP триггер или веб-перехватчика. Этот атрибут определен в пакете NuGet hello [Microsoft.Azure.WebJobs.Extensions.Http]. Можно настроить уровень авторизации hello, тип веб-перехватчика, маршрута и методы. Hello следующий пример определяет триггер HTTP с анонимной проверкой подлинности и _genericJson_ тип веб-перехватчика.

```csharp
[FunctionName("HttpTriggerCSharp")]
public static HttpResponseMessage Run([HttpTrigger(AuthorizationLevel.Anonymous, WebHookType = "genericJson")] HttpRequestMessage req)
{
    return req.CreateResponse(HttpStatusCode.OK);
}
```

<a name="mobile-apps"></a>

### <a name="mobile-apps-input-and-output"></a>Входные и выходные привязки для мобильных приложений

Функции Azure поддерживают входные и выходные привязки для мобильных приложений. toolearn более, в разделе [мобильных приложений Azure функции привязки](functions-bindings-mobile-apps.md). атрибут Hello `[MobileTable]` определяется в пакет NuGet hello [Microsoft.Azure.WebJobs.Extensions.MobileApps].

Hello ниже приведен пример мобильные приложения привязка для вывода:

```csharp
[FunctionName("MobileAppsOutput")]        
[return: MobileTable(ApiKeySetting = "MyMobileAppKey", TableName = "MyTable", MobileAppUriSetting = "MyMobileAppUri")]
public static object Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, TraceWriter log)
{
    return new { Text = $"I'm running in a C# function! {myQueueItem}" };
}
```

<a name="nh"></a>

### <a name="notification-hubs-output"></a>Выходные привязки для Центров уведомлений

Функции Azure поддерживают выходную привязку для Центров уведомлений. toolearn более, в разделе [привязка для вывода концентратор уведомлений Azure функции](functions-bindings-notification-hubs.md). атрибут Hello `[NotificationHub]` определяется в пакет NuGet hello [Microsoft.Azure.WebJobs.Extensions.NotificationHubs].

<a name="queue"></a>

### <a name="queue-storage-trigger-and-output"></a>Привязки триггера и выходные привязки для хранилища очередей

Функции Azure поддерживают привязки триггера и выходные привязки для очередей Azure. Дополнительные сведения см. в статье [Привязки очередей службы хранилища для Функций Azure](functions-bindings-storage-queue.md).

Hello следующем примере показано, как toouse hello типа возвращаемого значения функции с выводом очереди привязки, с помощью hello `[Queue]` атрибута. использовать toodefine триггер очереди hello `[QueueTrigger]` атрибута.

```csharp
[StorageAccount("AzureWebJobsStorage")]
public static class QueueFunctions
{
    // HTTP trigger with queue output binding
    [FunctionName("QueueOutput")]
    [return: Queue("myqueue-items")]
    public static string QueueOutput([HttpTrigger] dynamic input,  TraceWriter log)
    {
        log.Info($"C# function processed: {input.Text}");
        return input.Text;
    }

    // Queue trigger
    [FunctionName("QueueTrigger")]
    [StorageAccount("AzureWebJobsStorage")]
    public static void QueueTrigger([QueueTrigger("myqueue-items")] string myQueueItem, TraceWriter log)
    {
        log.Info($"C# function processed: {myQueueItem}");
    }
}

```

<a name="sendgrid"></a>

### <a name="sendgrid-output"></a>Выходные привязки SendGrid

Функции Azure поддерживают выходную привязку SendGrid для отправки электронных сообщений программным способом. toolearn более, в разделе [SendGrid функции Azure привязки](functions-bindings-sendgrid.md).

атрибут Hello `[SendGrid]` определяется в пакет NuGet hello [Microsoft.Azure.WebJobs.Extensions.SendGrid].

Hello ниже приведен пример с помощью триггера очереди Service Bus и привязку выходных данных SendGrid с помощью `SendGridMessage`:

```csharp
[FunctionName("SendEmail")]
public static void Run(
    [ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] OutgoingEmail email,
    [SendGrid] out SendGridMessage message)
{
    message = new SendGridMessage();
    message.AddTo(email.To);
    message.AddContent("text/html", email.Body);
    message.SetFrom(new EmailAddress(email.From));
    message.SetSubject(email.Subject);
}

public class OutgoingEmail
{
    public string too{ get; set; }
    public string From { get; set; }
    public string Subject { get; set; }
    public string Body { get; set; }
}
```

<a name="service-bus"></a>

### <a name="service-bus-trigger-and-output"></a>Привязки триггера и выходные привязки для служебной шины

Функции Azure поддерживают привязки триггера и выходные привязки для очередей и разделов служебной шины. Дополнительные сведения о настройке привязок см. в статье [Привязки служебной шины в Функциях Azure](functions-bindings-service-bus.md).

Здравствуйте, атрибуты `[ServiceBusTrigger]` и `[ServiceBus]` в пакете NuGet hello [Microsoft.Azure.WebJobs.ServiceBus]. 

Hello ниже приведен пример триггера очереди служебной шины:

```csharp
[FunctionName("ServiceBusQueueTriggerCSharp")]                    
public static void Run([ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

Hello ниже приведен пример вывода Service Bus, привязка, с помощью типа возвращаемого значения метода hello в качестве выходных данных hello:

```csharp
[FunctionName("ServiceBusOutput")]
[return: ServiceBus("myqueue", Connection = "ServiceBusConnection")]
public static string ServiceBusOutput([HttpTrigger] dynamic input, TraceWriter log)
{
    log.Info($"C# function processed: {input.Text}");
    return input.Text;
}
```        

<a name="table"></a>

### <a name="table-storage-input-and-output"></a>Входные и выходные привязки для хранилища таблиц

Функции Azure поддерживают входные и выходные привязки для хранилища таблиц Azure. toolearn более, в разделе [привязки хранилища таблиц Azure функции](functions-bindings-storage-table.md).

Hello следующий пример — это класс с двумя функциями, демонстрирующий табличного вывода хранилища и привязок ввода. 

```csharp
[StorageAccount("AzureWebJobsStorage")]
public class TableStorage
{
    public class MyPoco
    {
        public string PartitionKey { get; set; }
        public string RowKey { get; set; }
        public string Text { get; set; }
    }

    [FunctionName("TableOutput")]
    [return: Table("MyTable")]
    public static MyPoco TableOutput([HttpTrigger] dynamic input, TraceWriter log)
    {
        log.Info($"C# http trigger function processed: {input.Text}");
        return new MyPoco { PartitionKey = "Http", RowKey = Guid.NewGuid().ToString(), Text = input.Text };
    }

    // use hello metadata parameter "queueTrigger" toobind hello queue payload
    [FunctionName("TableInput")]
    public static void TableInput([QueueTrigger("table-items")] string input, [Table("MyTable", "Http", "{queueTrigger}")] MyPoco poco, TraceWriter log)
    {
        log.Info($"C# function processed: {poco.Text}");
    }
}

```

<a name="timer"></a>

### <a name="timer-trigger"></a>Триггер таймера

Функции Azure поддерживают привязку триггеров к таймерам, благодаря чему вы можете выполнять код функции по определенному расписанию. toolearn Дополнительные сведения о функции hello привязки hello. в разделе [запланировать выполнение кода с помощью функций Azure](functions-bindings-timer.md).

В плане использования hello, можно определить расписание с [выражение CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression). Если используется план службы приложений, вы также можете использовать строку TimeSpan. 

Следующий пример Hello определяет триггер таймера, который запускается каждые 5 минут:

```csharp
[FunctionName("TimerTriggerCSharp")]
public static void Run([TimerTrigger("0 */5 * * * *")]TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
}
```

<a name="twilio"></a>

### <a name="twilio-output"></a>Выходные привязки Twilio

Azure поддерживает функции Twilio вывода tooenable привязки к функции toosend отправки SMS-сообщений. toolearn более, в разделе [привязка для вывода отправки SMS-сообщений от функций Azure с помощью hello Twilio](functions-bindings-twilio.md). 

атрибут Hello `[TwilioSms]` определен в пакете hello [Microsoft.Azure.WebJobs.Extensions.Twilio].

Hello следующий пример на C# использует очередь триггера и Twilio выходные данные привязки:

```csharp
[FunctionName("QueueTwilio")]
[return: TwilioSms(AccountSidSetting = "TwilioAccountSid", AuthTokenSetting = "TwilioAuthToken", From = "+1425XXXXXXX" )]
public static SMSMessage Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] JObject order, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {order}");

    var message = new SMSMessage()
    {
        Body = $"Hello {order["name"]}, thanks for your order!",
        too= order["mobileNumber"].ToString()
    };

    return message;
}
```

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения об использовании Функций Azure в написании сценариев C# см. в статье [Справочник разработчика C# по \#функциям Azure](functions-reference-csharp.md).

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]


<!-- NuGet packages --> 
[Microsoft.Azure.WebJobs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.DocumentDB]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DocumentDB/1.1.0-beta1
[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.MobileApps]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MobileApps/1.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.NotificationHubs/1.1.0-beta1
[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.SendGrid]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.SendGrid/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.Http]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Http/1.0.0-beta1
[Microsoft.Azure.WebJobs.Extensions.BotFramework]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.BotFramework/1.0.15-beta
[Microsoft.Azure.WebJobs.Extensions.ApiHub]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.ApiHub/1.0.0-beta4
[Microsoft.Azure.WebJobs.Extensions.Twilio]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Twilio/1.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions/2.1.0-beta1


<!-- Links toosource --> 
[DocumentDBAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs
[EventHubAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs
[EventHubTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubTriggerAttribute.cs
[MobileTableAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs
[NotificationHubAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs 
[ServiceBusAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs
[ServiceBusAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs
[QueueAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs
[StorageAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs
[BlobAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs
[TableAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs
[TwilioSmsAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs
[SendGridAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.SendGrid/SendGridAttribute.cs
[HttpTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/dev/src/WebJobs.Extensions.Http/HttpTriggerAttribute.cs
[ApiHubFileAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.ApiHub/ApiHubFileAttribute.cs
[TimerTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerTriggerAttribute.cs
