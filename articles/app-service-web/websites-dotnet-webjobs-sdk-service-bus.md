---
title: "toouse aaaHow Azure Service Bus с hello SDK веб-заданий"
description: "Узнайте, как toouse Azure Service Bus очереди и разделы с описанием hello SDK веб-заданий."
services: app-service\web, service-bus
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 2114a934-135b-42b8-871c-6cc040214e76
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: cb801a9320a20c276da4f48c8941c09d3f09bb1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-service-bus-with-hello-webjobs-sdk"></a><span data-ttu-id="b8159-103">Как toouse шины обслуживания Azure с hello SDK веб-заданий</span><span class="sxs-lookup"><span data-stu-id="b8159-103">How toouse Azure Service Bus with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="b8159-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="b8159-104">Overview</span></span>
<span data-ttu-id="b8159-105">В этом руководстве содержатся C# образцы кода, Показать как tootrigger процесса при получении сообщения об Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="b8159-105">This guide provides C# code samples that show how tootrigger a process when an Azure Service Bus message is received.</span></span> <span data-ttu-id="b8159-106">Используйте образцы кода Hello [SDK веб-заданий](websites-dotnet-webjobs-sdk.md) версии 1.x.</span><span class="sxs-lookup"><span data-stu-id="b8159-106">hello code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="b8159-107">Hello руководстве предполагается, вы знаете [как проект веб-задания в Visual Studio с подключением toocreate строки этой учетной записи хранения tooyour точки](websites-dotnet-webjobs-sdk-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b8159-107">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md).</span></span>

<span data-ttu-id="b8159-108">фрагменты кода Hello Показывать только функции, не hello код, создающий hello `JobHost` объекта, как показано в примере:</span><span class="sxs-lookup"><span data-stu-id="b8159-108">hello code snippets only show functions, not hello code that creates hello `JobHost` object as in this example:</span></span>

```
public class Program
{
   public static void Main()
   {
      JobHostConfiguration config = new JobHostConfiguration();
      config.UseServiceBus();
      JobHost host = new JobHost(config);
      host.RunAndBlock();
   }
}
```

<span data-ttu-id="b8159-109">Объект [полный пример кода Service Bus](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) находится в хранилище azure — веб-заданий sdk примеры hello на GitHub.com.</span><span class="sxs-lookup"><span data-stu-id="b8159-109">A [complete Service Bus code example](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) is in hello azure-webjobs-sdk-samples repository on GitHub.com.</span></span>

## <span data-ttu-id="b8159-110"><a id="prerequisites"></a> Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b8159-110"><a id="prerequisites"></a> Prerequisites</span></span>
<span data-ttu-id="b8159-111">toowork со служебной шиной имеют tooinstall hello [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet пакета Кроме toohello другие пакеты SDK веб-заданий.</span><span class="sxs-lookup"><span data-stu-id="b8159-111">toowork with Service Bus you have tooinstall hello [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet package in addition toohello other WebJobs SDK packages.</span></span> 

<span data-ttu-id="b8159-112">Также имеется строка подключения AzureWebJobsServiceBus tooset hello в строки подключения хранилища toohello сложения.</span><span class="sxs-lookup"><span data-stu-id="b8159-112">You also have tooset hello AzureWebJobsServiceBus connection string in addition toohello storage connection strings.</span></span>  <span data-ttu-id="b8159-113">Это можно сделать в hello `connectionStrings` раздел файла App.config hello, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="b8159-113">You can do this in hello `connectionStrings` section of hello App.config file, as shown in hello following example:</span></span>

        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsServiceBus" connectionString="Endpoint=sb://[yourServiceNamespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[yourKey]"/>
        </connectionStrings>

<span data-ttu-id="b8159-114">Пример проекта, который включает строку подключения Service Bus hello в файле App.config hello, в разделе [Service Bus пример](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span><span class="sxs-lookup"><span data-stu-id="b8159-114">For a sample project that includes hello Service Bus connection string setting in hello App.config file, see [Service Bus example](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span></span> 

<span data-ttu-id="b8159-115">также можно задать строки подключения Hello в среде выполнения Azure hello, которая затем перекрывает hello App.config при hello веб-задание в Azure; Дополнительные сведения см. в разделе [Приступая к работе с hello SDK веб-задания](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span><span class="sxs-lookup"><span data-stu-id="b8159-115">hello connection strings can also be set in hello Azure runtime environment, which then overrides hello App.config settings when hello WebJob runs in Azure; for more information, see [Get Started with hello WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span></span>

## <span data-ttu-id="b8159-116"><a id="trigger"></a>Как происходит получение tootrigger функции, если сообщение очереди Service Bus</span><span class="sxs-lookup"><span data-stu-id="b8159-116"><a id="trigger"></a> How tootrigger a function when a Service Bus queue message is received</span></span>
<span data-ttu-id="b8159-117">вызывает функцию, которая hello SDK веб-заданий toowrite при получении сообщения в очереди, используйте hello `ServiceBusTrigger` атрибута.</span><span class="sxs-lookup"><span data-stu-id="b8159-117">toowrite a function that hello WebJobs SDK calls when a queue message is received, use hello `ServiceBusTrigger` attribute.</span></span> <span data-ttu-id="b8159-118">Конструктор атрибута Hello принимает параметр, задающий имя hello toopoll очереди hello.</span><span class="sxs-lookup"><span data-stu-id="b8159-118">hello attribute constructor takes a parameter that specifies hello name of hello queue toopoll.</span></span>

### <a name="how-servicebustrigger-works"></a><span data-ttu-id="b8159-119">Как действует ServicebusTrigger</span><span class="sxs-lookup"><span data-stu-id="b8159-119">How ServiceBusTrigger works</span></span>
<span data-ttu-id="b8159-120">Hello пакет SDK получает сообщение в `PeekLock` режим и вызовы `Complete` на приветственное сообщение, если функции hello завершается успешно, или вызовы `Abandon` при сбое функции hello.</span><span class="sxs-lookup"><span data-stu-id="b8159-120">hello SDK receives a message in `PeekLock` mode and calls `Complete` on hello message if hello function finishes successfully, or calls `Abandon` if hello function fails.</span></span> <span data-ttu-id="b8159-121">Если функции hello выполняется дольше, чем hello `PeekLock` время ожидания блокировки hello автоматически обновляется.</span><span class="sxs-lookup"><span data-stu-id="b8159-121">If hello function runs longer than hello `PeekLock` timeout, hello lock is automatically renewed.</span></span>

<span data-ttu-id="b8159-122">Service Bus выполняет собственную обработку очереди подозрительных сообщений, который не может управлять или настройки hello SDK веб-заданий.</span><span class="sxs-lookup"><span data-stu-id="b8159-122">Service Bus does its own poison queue handling which cannot be controlled or configured by hello WebJobs SDK.</span></span> 

### <a name="string-queue-message"></a><span data-ttu-id="b8159-123">Строковое сообщение очереди</span><span class="sxs-lookup"><span data-stu-id="b8159-123">String queue message</span></span>
<span data-ttu-id="b8159-124">Hello следующий код считывает сообщение очереди, которое содержит строку и записывает строку hello toohello панели мониторинга пакета SDK веб-заданий.</span><span class="sxs-lookup"><span data-stu-id="b8159-124">hello following code sample reads a queue message that contains a string and writes hello string toohello WebJobs SDK dashboard.</span></span>

        public static void ProcessQueueMessage([ServiceBusTrigger("inputqueue")] string message, 
            TextWriter logger)
        {
            logger.WriteLine(message);
        }

<span data-ttu-id="b8159-125">**Примечание:** при создании hello очереди сообщений в приложении, которое не использует hello SDK веб-задания, убедитесь, что tooset [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) слишком «text/plain».</span><span class="sxs-lookup"><span data-stu-id="b8159-125">**Note:** If you are creating hello queue messages in an application that doesn't use hello WebJobs SDK, make sure tooset [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) too"text/plain".</span></span>

### <a name="poco-queue-message"></a><span data-ttu-id="b8159-126">Сообщения очереди POCO</span><span class="sxs-lookup"><span data-stu-id="b8159-126">POCO queue message</span></span>
<span data-ttu-id="b8159-127">пакет SDK для Hello автоматически выполнит десериализацию очереди сообщение, содержащее JSON для POCO [(обычный объект CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) типа.</span><span class="sxs-lookup"><span data-stu-id="b8159-127">hello SDK will automatically deserialize a queue message that contains JSON for a POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) type.</span></span> <span data-ttu-id="b8159-128">Hello следующий пример кода считывает очередь сообщение, содержащее `BlobInformation` объект, имеющий `BlobName` свойство:</span><span class="sxs-lookup"><span data-stu-id="b8159-128">hello following code sample reads a queue message that contains a `BlobInformation` object which has a `BlobName` property:</span></span>

        public static void WriteLogPOCO([ServiceBusTrigger("inputqueue")] BlobInformation blobInfo,
            TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

<span data-ttu-id="b8159-129">Образцы кода, показывающий, как же hello toouse свойства toowork POCO hello с BLOB-объектов и таблиц в см. в разделе hello [хранилища очередей версию этой статьи](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span><span class="sxs-lookup"><span data-stu-id="b8159-129">For code samples showing how toouse properties of hello POCO toowork with blobs and tables in hello same function, see hello [storage queues version of this article](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span></span>

<span data-ttu-id="b8159-130">Если код, создающий приветственных очереди сообщений не использует hello SDK веб-задания, используйте toohello аналогичный код, следующий пример:</span><span class="sxs-lookup"><span data-stu-id="b8159-130">If your code that creates hello queue message doesn't use hello WebJobs SDK, use code similar toohello following example:</span></span>

        var client = QueueClient.CreateFromConnectionString(ConfigurationManager.ConnectionStrings["AzureWebJobsServiceBus"].ConnectionString, "blobadded");
        BlobInformation blobInformation = new BlobInformation () ;
        var message = new BrokeredMessage(blobInformation);
        client.Send(message);

### <a name="types-servicebustrigger-works-with"></a><span data-ttu-id="b8159-131">Типы, с которыми работает атрибут ServiceBusTrigger</span><span class="sxs-lookup"><span data-stu-id="b8159-131">Types ServiceBusTrigger works with</span></span>
<span data-ttu-id="b8159-132">Помимо `string` и типами POCO, можно использовать hello `ServiceBusTrigger` атрибута с помощью байтового массива или `BrokeredMessage` объекта.</span><span class="sxs-lookup"><span data-stu-id="b8159-132">Besides `string` and POCO  types, you can use hello `ServiceBusTrigger` attribute with a byte array or a `BrokeredMessage` object.</span></span>

## <span data-ttu-id="b8159-133"><a id="create"></a>Как toocreate Service Bus очередь сообщений</span><span class="sxs-lookup"><span data-stu-id="b8159-133"><a id="create"></a> How toocreate Service Bus queue messages</span></span>
<span data-ttu-id="b8159-134">функция, которая создает новое сообщение очереди toowrite использовать hello `ServiceBus` атрибута и передайте в конструктор атрибута toohello имя очереди hello.</span><span class="sxs-lookup"><span data-stu-id="b8159-134">toowrite a function that creates a new queue message use hello `ServiceBus` attribute and pass in hello queue name toohello attribute constructor.</span></span> 

### <a name="create-a-single-queue-message-in-a-non-async-function"></a><span data-ttu-id="b8159-135">Создание одного сообщения очереди в неасинхронной функции</span><span class="sxs-lookup"><span data-stu-id="b8159-135">Create a single queue message in a non-async function</span></span>
<span data-ttu-id="b8159-136">Следующий образец кода Hello использует toocreate выходной параметр, новые сообщения в очереди hello с именем «outputqueue» с таким же содержимое, так как hello сообщения, полученного в очередь hello, с именем «inputqueue» hello.</span><span class="sxs-lookup"><span data-stu-id="b8159-136">hello following code sample uses an output parameter toocreate a new message in hello queue named "outputqueue" with hello same content as hello message received in hello queue named "inputqueue".</span></span>

        public static void CreateQueueMessage(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] out string outputQueueMessage)
        {
            outputQueueMessage = queueMessage;
        }

<span data-ttu-id="b8159-137">Hello выходной параметр для создания одной очереди сообщения может быть любой hello следующие типы:</span><span class="sxs-lookup"><span data-stu-id="b8159-137">hello output parameter for creating a single queue message can be any of hello following types:</span></span>

* `string`
* `byte[]`
* `BrokeredMessage`
* <span data-ttu-id="b8159-138">Сериализуемый тип POCO, заданный вами</span><span class="sxs-lookup"><span data-stu-id="b8159-138">A serializable POCO type that you define.</span></span> <span data-ttu-id="b8159-139">Сериализируется как JSON автоматически.</span><span class="sxs-lookup"><span data-stu-id="b8159-139">Automatically serialized as JSON.</span></span>

<span data-ttu-id="b8159-140">Для параметров типа POCO сообщения в очереди всегда создается при завершении функции hello; Если параметр hello имеет значение null, hello SDK создает очереди сообщение, которое будет возвращать значение null, при получении сообщения hello и десериализации.</span><span class="sxs-lookup"><span data-stu-id="b8159-140">For POCO type parameters, a queue message is always created when hello function ends; if hello parameter is null, hello SDK creates a queue message that will return null when hello message is received and deserialized.</span></span> <span data-ttu-id="b8159-141">Для Здравствуйте других типов, если параметр hello не определен создается сообщение в очереди.</span><span class="sxs-lookup"><span data-stu-id="b8159-141">For hello other types, if hello parameter is null no queue message is created.</span></span>

### <a name="create-multiple-queue-messages-or-in-async-functions"></a><span data-ttu-id="b8159-142">Создание нескольких сообщений очереди или сообщений в асинхронных функциях</span><span class="sxs-lookup"><span data-stu-id="b8159-142">Create multiple queue messages or in async functions</span></span>
<span data-ttu-id="b8159-143">toocreate использовать несколько сообщений hello `ServiceBus` атрибутом `ICollector<T>` или `IAsyncCollector<T>`, как показано в hello следующий образец кода:</span><span class="sxs-lookup"><span data-stu-id="b8159-143">toocreate multiple messages, use  hello `ServiceBus` attribute with `ICollector<T>` or `IAsyncCollector<T>`, as shown in hello following code sample:</span></span>

        public static void CreateQueueMessages(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="b8159-144">Каждое сообщение очереди создается сразу после hello `Add` вызывается метод.</span><span class="sxs-lookup"><span data-stu-id="b8159-144">Each queue message is created immediately when hello `Add` method is called.</span></span>

## <span data-ttu-id="b8159-145"><a id="topics"></a>Как toowork с разделы служебной шины</span><span class="sxs-lookup"><span data-stu-id="b8159-145"><a id="topics"></a>How toowork with Service Bus topics</span></span>
<span data-ttu-id="b8159-146">вызывает функцию, которая hello SDK toowrite при получении сообщения в раздел служебной шины, используйте hello `ServiceBusTrigger` атрибута с hello конструктор, который принимает имя раздела и имя подписки, как показано в hello следующий образец кода:</span><span class="sxs-lookup"><span data-stu-id="b8159-146">toowrite a function that hello SDK calls when a message is received on a Service Bus topic, use hello `ServiceBusTrigger` attribute with hello constructor that takes topic name and subscription name, as shown in hello following code sample:</span></span>

        public static void WriteLog([ServiceBusTrigger("outputtopic","subscription1")] string message,
            TextWriter logger)
        {
            logger.WriteLine("Topic message: " + message);
        }

<span data-ttu-id="b8159-147">toocreate сообщения по теме, используйте hello `ServiceBus` атрибутом типа hello имя раздела таким же, как используется с именем очереди.</span><span class="sxs-lookup"><span data-stu-id="b8159-147">toocreate a message on a topic, use hello `ServiceBus` attribute with a topic name hello same way you use it with a queue name.</span></span>

## <a name="features-added-in-release-11"></a><span data-ttu-id="b8159-148">Функции, добавленные в версии 1.1</span><span class="sxs-lookup"><span data-stu-id="b8159-148">Features added in release 1.1</span></span>
<span data-ttu-id="b8159-149">Привет, следующие атрибуты были добавлены в версии 1.1:</span><span class="sxs-lookup"><span data-stu-id="b8159-149">hello following features were added in release 1.1:</span></span>

* <span data-ttu-id="b8159-150">Добавлена возможность обширной настройки обработки сообщений с помощью `ServiceBusConfiguration.MessagingProvider`.</span><span class="sxs-lookup"><span data-stu-id="b8159-150">Allow deep customization of message processing via `ServiceBusConfiguration.MessagingProvider`.</span></span>
* <span data-ttu-id="b8159-151">`MessagingProvider`поддерживает настройку hello Service Bus `MessagingFactory` и `NamespaceManager`.</span><span class="sxs-lookup"><span data-stu-id="b8159-151">`MessagingProvider` supports customization of hello Service Bus `MessagingFactory` and `NamespaceManager`.</span></span>
* <span data-ttu-id="b8159-152">Объект `MessageProcessor` шаблон стратегии позволяет toospecify процессор на очереди или раздела.</span><span class="sxs-lookup"><span data-stu-id="b8159-152">A `MessageProcessor` strategy pattern allows you toospecify a processor per queue/topic.</span></span>
* <span data-ttu-id="b8159-153">По умолчанию поддерживается параллелизм обработки сообщений.</span><span class="sxs-lookup"><span data-stu-id="b8159-153">Message processing concurrency is supported by default.</span></span> 
* <span data-ttu-id="b8159-154">Упрощена настройка `OnMessageOptions` через `ServiceBusConfiguration.MessageOptions`.</span><span class="sxs-lookup"><span data-stu-id="b8159-154">Easy customization of `OnMessageOptions` via `ServiceBusConfiguration.MessageOptions`.</span></span>
* <span data-ttu-id="b8159-155">Разрешить [права](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) toobe, указанные на `ServiceBusTriggerAttribute` / `ServiceBusAttribute` (для сценариев, где возможно управление правами).</span><span class="sxs-lookup"><span data-stu-id="b8159-155">Allow [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) toobe specified on `ServiceBusTriggerAttribute`/`ServiceBusAttribute` (for scenarios where you might not have Manage rights).</span></span> <span data-ttu-id="b8159-156">Обратите внимание, что веб-заданий Azure не удается tooautomatically подготовки несуществующей очереди и разделы без права на управление.</span><span class="sxs-lookup"><span data-stu-id="b8159-156">Note that Azure WebJobs is unable tooautomatically provision non-existent queues and topics without Manage AccessRights.</span></span>

## <span data-ttu-id="b8159-157"><a id="queues"></a>Связанные разделы, охватываемых хранилища очередей hello как tooarticle</span><span class="sxs-lookup"><span data-stu-id="b8159-157"><a id="queues"></a>Related topics covered by hello storage queues how-tooarticle</span></span>
<span data-ttu-id="b8159-158">Сведения о сценариях SDK веб-заданий не только tooService шины см. в разделе [как хранилище с hello SDK веб-заданий очередей toouse Azure](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="b8159-158">For information about WebJobs SDK scenarios not specific tooService Bus, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="b8159-159">В этой статье рассматриваются следующие hello:</span><span class="sxs-lookup"><span data-stu-id="b8159-159">Topics covered in that article include hello following:</span></span>

* <span data-ttu-id="b8159-160">Асинхронные функции</span><span class="sxs-lookup"><span data-stu-id="b8159-160">Async functions</span></span>
* <span data-ttu-id="b8159-161">Выполнение на нескольких экземплярах</span><span class="sxs-lookup"><span data-stu-id="b8159-161">Multiple instances</span></span>
* <span data-ttu-id="b8159-162">Корректное завершение работы</span><span class="sxs-lookup"><span data-stu-id="b8159-162">Graceful shutdown</span></span>
* <span data-ttu-id="b8159-163">Использование пакета SDK веб-задания атрибутов в теле функции hello</span><span class="sxs-lookup"><span data-stu-id="b8159-163">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="b8159-164">Набор строк подключения пакета SDK для hello в коде</span><span class="sxs-lookup"><span data-stu-id="b8159-164">Set hello SDK connection strings in code</span></span>
* <span data-ttu-id="b8159-165">Установка значений параметров конструктора пакета SDK для заданий WebJob в коде</span><span class="sxs-lookup"><span data-stu-id="b8159-165">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="b8159-166">Вызов функции вручную</span><span class="sxs-lookup"><span data-stu-id="b8159-166">Trigger a function manually</span></span>
* <span data-ttu-id="b8159-167">Запись журналов</span><span class="sxs-lookup"><span data-stu-id="b8159-167">Write logs</span></span>

## <span data-ttu-id="b8159-168"><a id="nextsteps"></a> Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b8159-168"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="b8159-169">В этом руководстве предоставила код образцы где показано, как toohandle распространенные сценарии для работы с Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="b8159-169">This guide has provided code samples that show how toohandle common scenarios for working with Azure Service Bus.</span></span> <span data-ttu-id="b8159-170">Дополнительные сведения о статье toouse веб-заданий Azure и hello SDK веб-заданий [рекомендуется заданиям Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="b8159-170">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

