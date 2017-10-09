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
# <a name="using-net-class-libraries-with-azure-functions"></a><span data-ttu-id="05869-104">Использование библиотек классов .NET с помощью Функций Azure</span><span class="sxs-lookup"><span data-stu-id="05869-104">Using .NET class libraries with Azure Functions</span></span>

<span data-ttu-id="05869-105">Кроме файлов tooscript, функции Azure поддерживает публикацию hello реализацию одного или нескольких функций библиотеки классов.</span><span class="sxs-lookup"><span data-stu-id="05869-105">In addition tooscript files, Azure Functions supports publishing a class library as hello implementation for one or more functions.</span></span> <span data-ttu-id="05869-106">Мы рекомендуем использовать hello [Azure функции 2017 г. набор средств Visual Studio](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span><span class="sxs-lookup"><span data-stu-id="05869-106">We recommend that you use hello [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05869-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="05869-107">Prerequisites</span></span> 

<span data-ttu-id="05869-108">В этой статье имеет hello следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="05869-108">This article has hello following prerequisites:</span></span>

- <span data-ttu-id="05869-109">[Предварительная версия Visual Studio 2017 15.3](https://www.visualstudio.com/vs/preview/).</span><span class="sxs-lookup"><span data-stu-id="05869-109">[Visual Studio 2017 15.3 Preview](https://www.visualstudio.com/vs/preview/).</span></span> <span data-ttu-id="05869-110">Установка рабочих нагрузок hello **ASP.NET и веб-разработки** и **разработки Azure**.</span><span class="sxs-lookup"><span data-stu-id="05869-110">Install hello workloads **ASP.NET and web development** and **Azure development**.</span></span>
- <span data-ttu-id="05869-111">[Инструменты Функций Azure для Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=AndrewBHall-MSFT.AzureFunctionToolsforVisualStudio2017).</span><span class="sxs-lookup"><span data-stu-id="05869-111">[Azure Function Tools for Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=AndrewBHall-MSFT.AzureFunctionToolsforVisualStudio2017)</span></span>

## <a name="functions-class-library-project"></a><span data-ttu-id="05869-112">Проект библиотеки классов функций</span><span class="sxs-lookup"><span data-stu-id="05869-112">Functions class library project</span></span>

<span data-ttu-id="05869-113">Создайте проект Функций Azure в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="05869-113">From Visual Studio, create a new Azure Functions project.</span></span> <span data-ttu-id="05869-114">Hello новый шаблон проекта создает файлы hello *host.json* и *local.settings.json*.</span><span class="sxs-lookup"><span data-stu-id="05869-114">hello new project template creates hello files *host.json* and *local.settings.json*.</span></span> <span data-ttu-id="05869-115">Вы можете [настроить параметры среды выполнения Функций Azure в файле host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="05869-115">You can [customize Azure Functions runtime settings in host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span> 

<span data-ttu-id="05869-116">файл Hello *local.settings.json* сохраняют параметры приложения, строки подключения и параметры для средства основных функций Azure.</span><span class="sxs-lookup"><span data-stu-id="05869-116">hello file *local.settings.json* stores app settings, connection strings, and settings for Azure Functions Core Tools.</span></span> <span data-ttu-id="05869-117">toolearn Дополнительные сведения о его структуры, в разделе [кода и тестирования функций Azure локально](functions-run-local.md#local-settings).</span><span class="sxs-lookup"><span data-stu-id="05869-117">toolearn more about its structure, see [Code and test Azure functions locally](functions-run-local.md#local-settings).</span></span>

### <a name="functionname-attribute"></a><span data-ttu-id="05869-118">Атрибут FunctionName</span><span class="sxs-lookup"><span data-stu-id="05869-118">FunctionName attribute</span></span>

<span data-ttu-id="05869-119">атрибут Hello [ `FunctionNameAttribute` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) помечает метод как точку входа функции.</span><span class="sxs-lookup"><span data-stu-id="05869-119">hello attribute [`FunctionNameAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) marks a method as a function entry point.</span></span> <span data-ttu-id="05869-120">Он должен иметь только один триггер и 0 или более входных и выходных привязок.</span><span class="sxs-lookup"><span data-stu-id="05869-120">It must be used with exactly one trigger and 0 or more input and output bindings.</span></span>

### <a name="conversion-toofunctionjson"></a><span data-ttu-id="05869-121">Преобразование toofunction.json</span><span class="sxs-lookup"><span data-stu-id="05869-121">Conversion toofunction.json</span></span>

<span data-ttu-id="05869-122">При построении проекта служб Azure функции, он создает файл `function.json` в каталоге hello сопоставления имени функции hello определяется `[FunctionName]`.</span><span class="sxs-lookup"><span data-stu-id="05869-122">When an Azure Functions project is built, it produces a file `function.json` in hello directory matching hello function name defined by `[FunctionName]`.</span></span> <span data-ttu-id="05869-123">Указывает, триггеры и привязки и файл сборки проекта toohello точек.</span><span class="sxs-lookup"><span data-stu-id="05869-123">It specifies triggers and bindings and points toohello project assembly file.</span></span>

<span data-ttu-id="05869-124">Это преобразование выполняется пакет NuGet hello [Microsoft\.NET\.Sdk\.функции](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions).</span><span class="sxs-lookup"><span data-stu-id="05869-124">This conversion is performed by hello NuGet package [Microsoft\.NET\.Sdk\.Functions](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions).</span></span> <span data-ttu-id="05869-125">Источник Hello доступен в репозитории GitHub hello [azure\-функции\-vs\-построения\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).</span><span class="sxs-lookup"><span data-stu-id="05869-125">hello source is available in hello GitHub repo [azure\-functions\-vs\-build\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).</span></span>

## <a name="triggers-and-bindings"></a><span data-ttu-id="05869-126">Триггеры и привязки</span><span class="sxs-lookup"><span data-stu-id="05869-126">Triggers and bindings</span></span>

<span data-ttu-id="05869-127">Hello следующей таблице перечислены триггеры hello и привязок, доступных в проекте библиотеки классов функций Azure.</span><span class="sxs-lookup"><span data-stu-id="05869-127">hello following table lists hello triggers and bindings that are available in an Azure Functions class library project.</span></span> <span data-ttu-id="05869-128">Все атрибуты находятся в пространстве имен hello `Microsoft.Azure.WebJobs`.</span><span class="sxs-lookup"><span data-stu-id="05869-128">All attributes are in hello namespace `Microsoft.Azure.WebJobs`.</span></span>

| <span data-ttu-id="05869-129">Привязка</span><span class="sxs-lookup"><span data-stu-id="05869-129">Binding</span></span> | <span data-ttu-id="05869-130">Атрибут</span><span class="sxs-lookup"><span data-stu-id="05869-130">Attribute</span></span> | <span data-ttu-id="05869-131">Пакет NuGet</span><span class="sxs-lookup"><span data-stu-id="05869-131">NuGet package</span></span> |
|------   | ------    | ------        |
| [<span data-ttu-id="05869-132">Привязки триггера, входные и выходные привязки для хранилища BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="05869-132">Blob storage trigger, input, output</span></span>](#blob-storage) | <span data-ttu-id="05869-133">[BlobAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="05869-133">[BlobAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="05869-134">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="05869-134">[Microsoft.Azure.WebJobs]</span></span> | <span data-ttu-id="05869-135">[Хранилище BLOB-объектов]</span><span class="sxs-lookup"><span data-stu-id="05869-135">[Blob storage]</span></span> |
| [<span data-ttu-id="05869-136">Входная и выходная привязка для Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="05869-136">Cosmos DB input and output binding</span></span>](#cosmos-db) | <span data-ttu-id="05869-137">[DocumentDBAttribute]</span><span class="sxs-lookup"><span data-stu-id="05869-137">[DocumentDBAttribute]</span></span> | <span data-ttu-id="05869-138">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]</span><span class="sxs-lookup"><span data-stu-id="05869-138">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]</span></span> | 
| [<span data-ttu-id="05869-139">Привязки триггера и выходные привязки для концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="05869-139">Event Hubs trigger and output</span></span>](#event-hub) | <span data-ttu-id="05869-140">[EventHubTriggerAttribute], [EventHubAttribute]</span><span class="sxs-lookup"><span data-stu-id="05869-140">[EventHubTriggerAttribute], [EventHubAttribute]</span></span> | <span data-ttu-id="05869-141">[Microsoft.Azure.WebJobs.ServiceBus]</span><span class="sxs-lookup"><span data-stu-id="05869-141">[Microsoft.Azure.WebJobs.ServiceBus]</span></span> |
| [<span data-ttu-id="05869-142">Входная и выходная привязка для внешнего файла</span><span class="sxs-lookup"><span data-stu-id="05869-142">External file input and output</span></span>](#api-hub) | <span data-ttu-id="05869-143">[ApiHubFileAttribute]</span><span class="sxs-lookup"><span data-stu-id="05869-143">[ApiHubFileAttribute]</span></span> | <span data-ttu-id="05869-144">[Microsoft.Azure.WebJobs.Extensions.ApiHub]</span><span class="sxs-lookup"><span data-stu-id="05869-144">[Microsoft.Azure.WebJobs.Extensions.ApiHub]</span></span> |
| [<span data-ttu-id="05869-145">Триггер HTTP и веб-перехватчика</span><span class="sxs-lookup"><span data-stu-id="05869-145">HTTP and webhook trigger</span></span>](#http) | <span data-ttu-id="05869-146">[HttpTriggerAttribute]</span><span class="sxs-lookup"><span data-stu-id="05869-146">[HttpTriggerAttribute]</span></span> | <span data-ttu-id="05869-147">[Microsoft.Azure.WebJobs.Extensions.Http]</span><span class="sxs-lookup"><span data-stu-id="05869-147">[Microsoft.Azure.WebJobs.Extensions.Http]</span></span> |
| [<span data-ttu-id="05869-148">Входные и выходные привязки для мобильных приложений</span><span class="sxs-lookup"><span data-stu-id="05869-148">Mobile Apps input and output</span></span>](#mobile-apps) | <span data-ttu-id="05869-149">[MobileTableAttribute]</span><span class="sxs-lookup"><span data-stu-id="05869-149">[MobileTableAttribute]</span></span> | <span data-ttu-id="05869-150">[Microsoft.Azure.WebJobs.Extensions.MobileApps]</span><span class="sxs-lookup"><span data-stu-id="05869-150">[Microsoft.Azure.WebJobs.Extensions.MobileApps]</span></span> | 
| [<span data-ttu-id="05869-151">Выходные привязки для Центров уведомлений</span><span class="sxs-lookup"><span data-stu-id="05869-151">Notification Hubs output</span></span>](#nh) | <span data-ttu-id="05869-152">[NotificationHubAttribute]</span><span class="sxs-lookup"><span data-stu-id="05869-152">[NotificationHubAttribute]</span></span> | <span data-ttu-id="05869-153">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]</span><span class="sxs-lookup"><span data-stu-id="05869-153">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]</span></span> | 
| [<span data-ttu-id="05869-154">Привязки триггера и выходные привязки для хранилища очередей</span><span class="sxs-lookup"><span data-stu-id="05869-154">Queue storage trigger and output</span></span>](#queue) | <span data-ttu-id="05869-155">[QueueAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="05869-155">[QueueAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="05869-156">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="05869-156">[Microsoft.Azure.WebJobs]</span></span> | 
| [<span data-ttu-id="05869-157">Выходные привязки SendGrid</span><span class="sxs-lookup"><span data-stu-id="05869-157">SendGrid output</span></span>](#sendgrid) | <span data-ttu-id="05869-158">[SendGridAttribute]</span><span class="sxs-lookup"><span data-stu-id="05869-158">[SendGridAttribute]</span></span> | <span data-ttu-id="05869-159">[Microsoft.Azure.WebJobs.Extensions.SendGrid]</span><span class="sxs-lookup"><span data-stu-id="05869-159">[Microsoft.Azure.WebJobs.Extensions.SendGrid]</span></span> | 
| [<span data-ttu-id="05869-160">Привязки триггера и выходные привязки для служебной шины</span><span class="sxs-lookup"><span data-stu-id="05869-160">Service Bus trigger and output</span></span>](#service-bus) | <span data-ttu-id="05869-161">[ServiceBusAttribute], [ServiceBusAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="05869-161">[ServiceBusAttribute], [ServiceBusAccountAttribute]</span></span> | <span data-ttu-id="05869-162">[Microsoft.Azure.WebJobs.ServiceBus]</span><span class="sxs-lookup"><span data-stu-id="05869-162">[Microsoft.Azure.WebJobs.ServiceBus]</span></span>
| [<span data-ttu-id="05869-163">Входные и выходные привязки для хранилища таблиц</span><span class="sxs-lookup"><span data-stu-id="05869-163">Table storage input and output</span></span>](#table) | <span data-ttu-id="05869-164">[TableAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="05869-164">[TableAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="05869-165">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="05869-165">[Microsoft.Azure.WebJobs]</span></span> | 
| [<span data-ttu-id="05869-166">Триггер таймера</span><span class="sxs-lookup"><span data-stu-id="05869-166">Timer trigger</span></span>](#timer) | <span data-ttu-id="05869-167">[TimerTriggerAttribute]</span><span class="sxs-lookup"><span data-stu-id="05869-167">[TimerTriggerAttribute]</span></span> | <span data-ttu-id="05869-168">[Microsoft.Azure.WebJobs.Extensions]</span><span class="sxs-lookup"><span data-stu-id="05869-168">[Microsoft.Azure.WebJobs.Extensions]</span></span> | 
| [<span data-ttu-id="05869-169">Выходные привязки Twilio</span><span class="sxs-lookup"><span data-stu-id="05869-169">Twilio output</span></span>](#twilio) | <span data-ttu-id="05869-170">[TwilioSmsAttribute]</span><span class="sxs-lookup"><span data-stu-id="05869-170">[TwilioSmsAttribute]</span></span> | <span data-ttu-id="05869-171">[Microsoft.Azure.WebJobs.Extensions.Twilio]</span><span class="sxs-lookup"><span data-stu-id="05869-171">[Microsoft.Azure.WebJobs.Extensions.Twilio]</span></span> | 

<a name="blob-storage"></a>

### <a name="blob-storage-trigger-input-and-output-bindings"></a><span data-ttu-id="05869-172">Привязки триггера, входные и выходные привязки для хранилища BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="05869-172">Blob storage trigger, input, and output bindings</span></span>

<span data-ttu-id="05869-173">Функции Azure поддерживают привязки триггера, а также входные и выходные привязки для хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="05869-173">Azure Functions supports trigger, input, and output bindings for Azure Blob storage.</span></span> <span data-ttu-id="05869-174">Дополнительные сведения о выражениях привязки и метаданных см. в статье [Привязки хранилища BLOB-объектов для Функций Azure](functions-bindings-storage-blob.md).</span><span class="sxs-lookup"><span data-stu-id="05869-174">For more information on binding expressions and metadata, see [Azure Functions Blob storage bindings](functions-bindings-storage-blob.md).</span></span>

<span data-ttu-id="05869-175">Большой двоичный объект триггер определен с hello `[BlobTrigger]` атрибута.</span><span class="sxs-lookup"><span data-stu-id="05869-175">A blob trigger is defined with hello `[BlobTrigger]` attribute.</span></span> <span data-ttu-id="05869-176">Можно использовать атрибут hello `[StorageAccount]` учетной записи хранилища toodefine hello, используемый всей функции или классом.</span><span class="sxs-lookup"><span data-stu-id="05869-176">You can use hello attribute `[StorageAccount]` toodefine hello storage account that is used by an entire function or class.</span></span>

```csharp
[StorageAccount("AzureWebJobsStorage")]
[FunctionName("BlobTriggerCSharp")]        
public static void Run([BlobTrigger("samples-workitems/{name}")] Stream myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

<span data-ttu-id="05869-177">BLOB-объектов входных и выходных данных определяются с помощью hello `[Blob]` атрибута вместе с `FileAccess` параметр, указывающий, чтения или записи.</span><span class="sxs-lookup"><span data-stu-id="05869-177">Blob input and output are defined using hello `[Blob]` attribute, along with a `FileAccess` parameter indicating read or write.</span></span> <span data-ttu-id="05869-178">Здравствуйте, следующий пример использует триггер больших двоичных объектов и больших двоичных объектов выходной привязки.</span><span class="sxs-lookup"><span data-stu-id="05869-178">hello following example uses a blob trigger and blob output binding.</span></span>

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

### <a name="cosmos-db-input-and-output-bindings"></a><span data-ttu-id="05869-179">Входная и выходная привязка для Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="05869-179">Cosmos DB input and output bindings</span></span>

<span data-ttu-id="05869-180">Функции Azure поддерживают входные и выходные привязки для Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="05869-180">Azure Functions supports input and output bindings for Cosmos DB.</span></span> <span data-ttu-id="05869-181">toolearn Дополнительные сведения о функции hello привязки Cosmos DB hello, в разделе [Azure DB Cosmos функции привязки](functions-bindings-documentdb.md).</span><span class="sxs-lookup"><span data-stu-id="05869-181">toolearn more about hello features of hello Cosmos DB binding, see [Azure Functions Cosmos DB bindings](functions-bindings-documentdb.md).</span></span>

<span data-ttu-id="05869-182">toobind tooa Cosmos DB документа, используйте атрибут hello `[DocumentDB]` в пакет NuGet hello [Microsoft.Azure.WebJobs.Extensions.DocumentDB].</span><span class="sxs-lookup"><span data-stu-id="05869-182">toobind tooa Cosmos DB document, use hello attribute `[DocumentDB]` in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.DocumentDB].</span></span> <span data-ttu-id="05869-183">Следующий пример Hello имеет триггер очереди и привязка для вывода API DocumentDB:</span><span class="sxs-lookup"><span data-stu-id="05869-183">hello following example has a queue trigger and a DocumentDB API output binding:</span></span>

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

### <a name="event-hubs-trigger-and-output"></a><span data-ttu-id="05869-184">Привязки триггера и выходные привязки для концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="05869-184">Event Hubs trigger and output</span></span>

<span data-ttu-id="05869-185">Функции Azure поддерживают привязки триггера и выходные привязки для концентраторов событий Azure.</span><span class="sxs-lookup"><span data-stu-id="05869-185">Azure Functions supports trigger and output bindings for Event Hubs.</span></span> <span data-ttu-id="05869-186">Дополнительные сведения см. в статье [Привязки концентратора событий функций Azure](functions-bindings-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="05869-186">For more information, see  [Azure Functions Event Hub bindings](functions-bindings-event-hubs.md).</span></span>

<span data-ttu-id="05869-187">Здравствуйте, типы `[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` и `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]` в пакете NuGet hello [Microsoft.Azure.WebJobs.ServiceBus].</span><span class="sxs-lookup"><span data-stu-id="05869-187">hello types `[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` and `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]` are defined in hello NuGet package [Microsoft.Azure.WebJobs.ServiceBus].</span></span> 

<span data-ttu-id="05869-188">Hello следующем примере триггер концентратора событий:</span><span class="sxs-lookup"><span data-stu-id="05869-188">hello following example uses an Event Hub trigger:</span></span>

```csharp
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

<span data-ttu-id="05869-189">Hello следующий пример состоит из концентратора событий выходных данных, с помощью возвращаемого значения метода hello в качестве выходных данных hello.</span><span class="sxs-lookup"><span data-stu-id="05869-189">hello following example has an Event Hub output, using hello method return value as hello output:</span></span>

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

### <a name="external-file-input-and-output"></a><span data-ttu-id="05869-190">Входная и выходная привязка для внешнего файла</span><span class="sxs-lookup"><span data-stu-id="05869-190">External file input and output</span></span>

<span data-ttu-id="05869-191">Функции Azure поддерживают привязки триггера, а также входные и выходные привязки для внешних файлов, таких как Google Drive, Dropbox и OneDrive.</span><span class="sxs-lookup"><span data-stu-id="05869-191">Azure Functions supports trigger, input, and output bindings for external files, such as Google Drive, Dropbox, and OneDrive.</span></span> <span data-ttu-id="05869-192">toolearn более, в разделе [привязки внешнего файла Azure функции](functions-bindings-external-file.md).</span><span class="sxs-lookup"><span data-stu-id="05869-192">toolearn more, see [Azure Functions External File bindings](functions-bindings-external-file.md).</span></span> <span data-ttu-id="05869-193">Здравствуйте, атрибуты `[ExternalFileTrigger]` и `[ExternalFile]` в пакете NuGet hello [Microsoft.Azure.WebJobs.Extensions.ApiHub].</span><span class="sxs-lookup"><span data-stu-id="05869-193">hello attributes `[ExternalFileTrigger]` and `[ExternalFile]` are defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.ApiHub].</span></span>

<span data-ttu-id="05869-194">Hello в следующем примере C# демонстрируется внешний файл входной и выходной привязки.</span><span class="sxs-lookup"><span data-stu-id="05869-194">hello following C# example demonstrates an external file input and output binding.</span></span> <span data-ttu-id="05869-195">код копирует Hello hello входной файл toohello выходного файла.</span><span class="sxs-lookup"><span data-stu-id="05869-195">hello code copies hello input file toohello output file.</span></span>

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

### <a name="http-and-webhooks"></a><span data-ttu-id="05869-196">HTTP и вызовы webhook</span><span class="sxs-lookup"><span data-stu-id="05869-196">HTTP and webhooks</span></span>

<span data-ttu-id="05869-197">Используйте hello `HttpTrigger` атрибута toodefine HTTP триггер или веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="05869-197">Use hello `HttpTrigger` attribute toodefine an HTTP trigger or webhook.</span></span> <span data-ttu-id="05869-198">Этот атрибут определен в пакете NuGet hello [Microsoft.Azure.WebJobs.Extensions.Http].</span><span class="sxs-lookup"><span data-stu-id="05869-198">This attribute is defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.Http].</span></span> <span data-ttu-id="05869-199">Можно настроить уровень авторизации hello, тип веб-перехватчика, маршрута и методы.</span><span class="sxs-lookup"><span data-stu-id="05869-199">You can customize hello authorization level, webhook type, route, and methods.</span></span> <span data-ttu-id="05869-200">Hello следующий пример определяет триггер HTTP с анонимной проверкой подлинности и _genericJson_ тип веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="05869-200">hello following example defines an HTTP trigger with anonymous authentication and _genericJson_ webhook type.</span></span>

```csharp
[FunctionName("HttpTriggerCSharp")]
public static HttpResponseMessage Run([HttpTrigger(AuthorizationLevel.Anonymous, WebHookType = "genericJson")] HttpRequestMessage req)
{
    return req.CreateResponse(HttpStatusCode.OK);
}
```

<a name="mobile-apps"></a>

### <a name="mobile-apps-input-and-output"></a><span data-ttu-id="05869-201">Входные и выходные привязки для мобильных приложений</span><span class="sxs-lookup"><span data-stu-id="05869-201">Mobile Apps input and output</span></span>

<span data-ttu-id="05869-202">Функции Azure поддерживают входные и выходные привязки для мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="05869-202">Azure Functions supports input and output bindings for Mobile Apps.</span></span> <span data-ttu-id="05869-203">toolearn более, в разделе [мобильных приложений Azure функции привязки](functions-bindings-mobile-apps.md).</span><span class="sxs-lookup"><span data-stu-id="05869-203">toolearn more, see [Azure Functions Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span> <span data-ttu-id="05869-204">атрибут Hello `[MobileTable]` определяется в пакет NuGet hello [Microsoft.Azure.WebJobs.Extensions.MobileApps].</span><span class="sxs-lookup"><span data-stu-id="05869-204">hello attribute `[MobileTable]` is defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.MobileApps].</span></span>

<span data-ttu-id="05869-205">Hello ниже приведен пример мобильные приложения привязка для вывода:</span><span class="sxs-lookup"><span data-stu-id="05869-205">hello following example demonstrates a Mobile Apps output binding:</span></span>

```csharp
[FunctionName("MobileAppsOutput")]        
[return: MobileTable(ApiKeySetting = "MyMobileAppKey", TableName = "MyTable", MobileAppUriSetting = "MyMobileAppUri")]
public static object Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, TraceWriter log)
{
    return new { Text = $"I'm running in a C# function! {myQueueItem}" };
}
```

<a name="nh"></a>

### <a name="notification-hubs-output"></a><span data-ttu-id="05869-206">Выходные привязки для Центров уведомлений</span><span class="sxs-lookup"><span data-stu-id="05869-206">Notification Hubs output</span></span>

<span data-ttu-id="05869-207">Функции Azure поддерживают выходную привязку для Центров уведомлений.</span><span class="sxs-lookup"><span data-stu-id="05869-207">Azure Functions supports an output binding for Notification Hubs.</span></span> <span data-ttu-id="05869-208">toolearn более, в разделе [привязка для вывода концентратор уведомлений Azure функции](functions-bindings-notification-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="05869-208">toolearn more, see [Azure Functions Notification Hub output binding](functions-bindings-notification-hubs.md).</span></span> <span data-ttu-id="05869-209">атрибут Hello `[NotificationHub]` определяется в пакет NuGet hello [Microsoft.Azure.WebJobs.Extensions.NotificationHubs].</span><span class="sxs-lookup"><span data-stu-id="05869-209">hello attribute `[NotificationHub]` is defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.NotificationHubs].</span></span>

<a name="queue"></a>

### <a name="queue-storage-trigger-and-output"></a><span data-ttu-id="05869-210">Привязки триггера и выходные привязки для хранилища очередей</span><span class="sxs-lookup"><span data-stu-id="05869-210">Queue storage trigger and output</span></span>

<span data-ttu-id="05869-211">Функции Azure поддерживают привязки триггера и выходные привязки для очередей Azure.</span><span class="sxs-lookup"><span data-stu-id="05869-211">Azure Functions supports trigger and output bindings for Azure queues.</span></span> <span data-ttu-id="05869-212">Дополнительные сведения см. в статье [Привязки очередей службы хранилища для Функций Azure](functions-bindings-storage-queue.md).</span><span class="sxs-lookup"><span data-stu-id="05869-212">For more information, see [Azure Functions Queue Storage bindings](functions-bindings-storage-queue.md).</span></span>

<span data-ttu-id="05869-213">Hello следующем примере показано, как toouse hello типа возвращаемого значения функции с выводом очереди привязки, с помощью hello `[Queue]` атрибута.</span><span class="sxs-lookup"><span data-stu-id="05869-213">hello following example shows how toouse hello function return type with a queue output binding, using hello `[Queue]` attribute.</span></span> <span data-ttu-id="05869-214">использовать toodefine триггер очереди hello `[QueueTrigger]` атрибута.</span><span class="sxs-lookup"><span data-stu-id="05869-214">toodefine a queue trigger, use hello `[QueueTrigger]` attribute.</span></span>

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

### <a name="sendgrid-output"></a><span data-ttu-id="05869-215">Выходные привязки SendGrid</span><span class="sxs-lookup"><span data-stu-id="05869-215">SendGrid output</span></span>

<span data-ttu-id="05869-216">Функции Azure поддерживают выходную привязку SendGrid для отправки электронных сообщений программным способом.</span><span class="sxs-lookup"><span data-stu-id="05869-216">Azure Functions supports a SendGrid output binding for sending email programmatically.</span></span> <span data-ttu-id="05869-217">toolearn более, в разделе [SendGrid функции Azure привязки](functions-bindings-sendgrid.md).</span><span class="sxs-lookup"><span data-stu-id="05869-217">toolearn more, see [Azure Functions SendGrid bindings](functions-bindings-sendgrid.md).</span></span>

<span data-ttu-id="05869-218">атрибут Hello `[SendGrid]` определяется в пакет NuGet hello [Microsoft.Azure.WebJobs.Extensions.SendGrid].</span><span class="sxs-lookup"><span data-stu-id="05869-218">hello attribute `[SendGrid]` is defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.SendGrid].</span></span>

<span data-ttu-id="05869-219">Hello ниже приведен пример с помощью триггера очереди Service Bus и привязку выходных данных SendGrid с помощью `SendGridMessage`:</span><span class="sxs-lookup"><span data-stu-id="05869-219">hello following is an example of using a Service Bus queue trigger and a SendGrid output binding using `SendGridMessage`:</span></span>

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

### <a name="service-bus-trigger-and-output"></a><span data-ttu-id="05869-220">Привязки триггера и выходные привязки для служебной шины</span><span class="sxs-lookup"><span data-stu-id="05869-220">Service Bus trigger and output</span></span>

<span data-ttu-id="05869-221">Функции Azure поддерживают привязки триггера и выходные привязки для очередей и разделов служебной шины.</span><span class="sxs-lookup"><span data-stu-id="05869-221">Azure Functions supports trigger and output bindings for Service Bus queues and topics.</span></span> <span data-ttu-id="05869-222">Дополнительные сведения о настройке привязок см. в статье [Привязки служебной шины в Функциях Azure](functions-bindings-service-bus.md).</span><span class="sxs-lookup"><span data-stu-id="05869-222">For more information on configuring bindings, see [Azure Functions Service Bus bindings](functions-bindings-service-bus.md).</span></span>

<span data-ttu-id="05869-223">Здравствуйте, атрибуты `[ServiceBusTrigger]` и `[ServiceBus]` в пакете NuGet hello [Microsoft.Azure.WebJobs.ServiceBus].</span><span class="sxs-lookup"><span data-stu-id="05869-223">hello attributes `[ServiceBusTrigger]` and `[ServiceBus]` are defined in hello NuGet package [Microsoft.Azure.WebJobs.ServiceBus].</span></span> 

<span data-ttu-id="05869-224">Hello ниже приведен пример триггера очереди служебной шины:</span><span class="sxs-lookup"><span data-stu-id="05869-224">hello following is an example of a Service Bus queue trigger:</span></span>

```csharp
[FunctionName("ServiceBusQueueTriggerCSharp")]                    
public static void Run([ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<span data-ttu-id="05869-225">Hello ниже приведен пример вывода Service Bus, привязка, с помощью типа возвращаемого значения метода hello в качестве выходных данных hello:</span><span class="sxs-lookup"><span data-stu-id="05869-225">hello following is an example of a Service Bus output binding, using hello method return type as hello output:</span></span>

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

### <a name="table-storage-input-and-output"></a><span data-ttu-id="05869-226">Входные и выходные привязки для хранилища таблиц</span><span class="sxs-lookup"><span data-stu-id="05869-226">Table storage input and output</span></span>

<span data-ttu-id="05869-227">Функции Azure поддерживают входные и выходные привязки для хранилища таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="05869-227">Azure Functions supports input and output bindings for Azure Table storage.</span></span> <span data-ttu-id="05869-228">toolearn более, в разделе [привязки хранилища таблиц Azure функции](functions-bindings-storage-table.md).</span><span class="sxs-lookup"><span data-stu-id="05869-228">toolearn more, see [Azure Functions Table storage bindings](functions-bindings-storage-table.md).</span></span>

<span data-ttu-id="05869-229">Hello следующий пример — это класс с двумя функциями, демонстрирующий табличного вывода хранилища и привязок ввода.</span><span class="sxs-lookup"><span data-stu-id="05869-229">hello following example is a class with two functions, demonstrating table storage output and input bindings.</span></span> 

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

### <a name="timer-trigger"></a><span data-ttu-id="05869-230">Триггер таймера</span><span class="sxs-lookup"><span data-stu-id="05869-230">Timer trigger</span></span>

<span data-ttu-id="05869-231">Функции Azure поддерживают привязку триггеров к таймерам, благодаря чему вы можете выполнять код функции по определенному расписанию.</span><span class="sxs-lookup"><span data-stu-id="05869-231">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span></span> <span data-ttu-id="05869-232">toolearn Дополнительные сведения о функции hello привязки hello. в разделе [запланировать выполнение кода с помощью функций Azure](functions-bindings-timer.md).</span><span class="sxs-lookup"><span data-stu-id="05869-232">toolearn more about hello features of hello binding, see [Schedule code execution with Azure Functions](functions-bindings-timer.md).</span></span>

<span data-ttu-id="05869-233">В плане использования hello, можно определить расписание с [выражение CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression).</span><span class="sxs-lookup"><span data-stu-id="05869-233">On hello Consumption plan, you can define schedules with a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression).</span></span> <span data-ttu-id="05869-234">Если используется план службы приложений, вы также можете использовать строку TimeSpan.</span><span class="sxs-lookup"><span data-stu-id="05869-234">If you're using an App Service Plan, you can also use a TimeSpan string.</span></span> 

<span data-ttu-id="05869-235">Следующий пример Hello определяет триггер таймера, который запускается каждые 5 минут:</span><span class="sxs-lookup"><span data-stu-id="05869-235">hello following example defines a timer trigger that runs every 5 minutes:</span></span>

```csharp
[FunctionName("TimerTriggerCSharp")]
public static void Run([TimerTrigger("0 */5 * * * *")]TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
}
```

<a name="twilio"></a>

### <a name="twilio-output"></a><span data-ttu-id="05869-236">Выходные привязки Twilio</span><span class="sxs-lookup"><span data-stu-id="05869-236">Twilio output</span></span>

<span data-ttu-id="05869-237">Azure поддерживает функции Twilio вывода tooenable привязки к функции toosend отправки SMS-сообщений.</span><span class="sxs-lookup"><span data-stu-id="05869-237">Azure Functions supports Twilio output bindings tooenable your functions toosend SMS text messages.</span></span> <span data-ttu-id="05869-238">toolearn более, в разделе [привязка для вывода отправки SMS-сообщений от функций Azure с помощью hello Twilio](functions-bindings-twilio.md).</span><span class="sxs-lookup"><span data-stu-id="05869-238">toolearn more, see [Send SMS messages from Azure Functions using hello Twilio output binding](functions-bindings-twilio.md).</span></span> 

<span data-ttu-id="05869-239">атрибут Hello `[TwilioSms]` определен в пакете hello [Microsoft.Azure.WebJobs.Extensions.Twilio].</span><span class="sxs-lookup"><span data-stu-id="05869-239">hello attribute `[TwilioSms]` is defined in hello package [Microsoft.Azure.WebJobs.Extensions.Twilio].</span></span>

<span data-ttu-id="05869-240">Hello следующий пример на C# использует очередь триггера и Twilio выходные данные привязки:</span><span class="sxs-lookup"><span data-stu-id="05869-240">hello following C# example uses a queue trigger and a Twilio output binding:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="05869-241">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="05869-241">Next steps</span></span>

<span data-ttu-id="05869-242">Дополнительные сведения об использовании Функций Azure в написании сценариев C# см. в статье [Справочник разработчика C# по \#функциям Azure](functions-reference-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="05869-242">For more information on using Azure Functions in C# scripting, see [Azure Functions C\# script developer reference](functions-reference-csharp.md).</span></span>

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
