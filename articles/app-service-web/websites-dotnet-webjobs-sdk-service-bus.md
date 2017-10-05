---
title: "Как использовать Azure Service Bus с пакетом SDK для WebJob"
description: "Информация об использовании очередей и разделов Azure Service Bus с пакетом SDK для WebJob"
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
ms.openlocfilehash: 7cec03cae5d20d1ead9eb24e99415c33d8b76f05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-service-bus-with-the-webjobs-sdk"></a><span data-ttu-id="6adb1-103">Как использовать Azure Service Bus с пакетом SDK для WebJob</span><span class="sxs-lookup"><span data-stu-id="6adb1-103">How to use Azure Service Bus with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="6adb1-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="6adb1-104">Overview</span></span>
<span data-ttu-id="6adb1-105">В этом руководстве приведены примеры кода C#, демонстрирующие активацию процесса при получении сообщения служебной шины Azure.</span><span class="sxs-lookup"><span data-stu-id="6adb1-105">This guide provides C# code samples that show how to trigger a process when an Azure Service Bus message is received.</span></span> <span data-ttu-id="6adb1-106">В примерах кода используется [пакет SDK для веб-заданий](websites-dotnet-webjobs-sdk.md) версии 1.x.</span><span class="sxs-lookup"><span data-stu-id="6adb1-106">The code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="6adb1-107">В этом руководстве предполагается, что вы уже знаете, [как создавать проект веб-заданий в Visual Studio со строками подключения, указывающими на учетную запись хранения](websites-dotnet-webjobs-sdk-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6adb1-107">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md).</span></span>

<span data-ttu-id="6adb1-108">В фрагментах кода показаны только функции, а не код, создающий объект `JobHost` , как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="6adb1-108">The code snippets only show functions, not the code that creates the `JobHost` object as in this example:</span></span>

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

<span data-ttu-id="6adb1-109">[Полный пример кода служебной шины](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) можно найти в репозитории azure-webjobs-sdk-samples на сайте GitHub.com.</span><span class="sxs-lookup"><span data-stu-id="6adb1-109">A [complete Service Bus code example](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) is in the azure-webjobs-sdk-samples repository on GitHub.com.</span></span>

## <span data-ttu-id="6adb1-110"><a id="prerequisites"></a> Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6adb1-110"><a id="prerequisites"></a> Prerequisites</span></span>
<span data-ttu-id="6adb1-111">Для работы со служебной шиной необходимо установить пакет NuGet [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) , а также другие пакеты SDK для веб-заданий.</span><span class="sxs-lookup"><span data-stu-id="6adb1-111">To work with Service Bus you have to install the [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet package in addition to the other WebJobs SDK packages.</span></span> 

<span data-ttu-id="6adb1-112">Необходимо также задать строку подключения AzureWebJobsServiceBus и строки подключения для хранилища.</span><span class="sxs-lookup"><span data-stu-id="6adb1-112">You also have to set the AzureWebJobsServiceBus connection string in addition to the storage connection strings.</span></span>  <span data-ttu-id="6adb1-113">Это можно сделать в разделе `connectionStrings` файла App.config, как показано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="6adb1-113">You can do this in the `connectionStrings` section of the App.config file, as shown in the following example:</span></span>

        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsServiceBus" connectionString="Endpoint=sb://[yourServiceNamespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[yourKey]"/>
        </connectionStrings>

<span data-ttu-id="6adb1-114">Пример проекта, который содержит строку подключения служебной шины в файле App.config, доступен в разделе [Пример служебной шины](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span><span class="sxs-lookup"><span data-stu-id="6adb1-114">For a sample project that includes the Service Bus connection string setting in the App.config file, see [Service Bus example](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span></span> 

<span data-ttu-id="6adb1-115">Строки подключения также можно задать в среде выполнения Azure. Эти строки переопределят параметры App.config при выполнении веб-задания в Azure. Дополнительные сведения см. в разделе [Начало работы с пакетом SDK для Azure для веб-заданий](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span><span class="sxs-lookup"><span data-stu-id="6adb1-115">The connection strings can also be set in the Azure runtime environment, which then overrides the App.config settings when the WebJob runs in Azure; for more information, see [Get Started with the WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span></span>

## <span data-ttu-id="6adb1-116"><a id="trigger"></a> Как вызывать функцию при получении сообщения очереди служебной шины</span><span class="sxs-lookup"><span data-stu-id="6adb1-116"><a id="trigger"></a> How to trigger a function when a Service Bus queue message is received</span></span>
<span data-ttu-id="6adb1-117">Чтобы написать функцию, которую пакет SDK для веб-заданий будет вызывать при получении сообщения очереди, используйте атрибут `ServiceBusTrigger` .</span><span class="sxs-lookup"><span data-stu-id="6adb1-117">To write a function that the WebJobs SDK calls when a queue message is received, use the `ServiceBusTrigger` attribute.</span></span> <span data-ttu-id="6adb1-118">Конструктор атрибута принимает параметр, который указывает имя очереди для опроса.</span><span class="sxs-lookup"><span data-stu-id="6adb1-118">The attribute constructor takes a parameter that specifies the name of the queue to poll.</span></span>

### <a name="how-servicebustrigger-works"></a><span data-ttu-id="6adb1-119">Как действует ServicebusTrigger</span><span class="sxs-lookup"><span data-stu-id="6adb1-119">How ServiceBusTrigger works</span></span>
<span data-ttu-id="6adb1-120">Пакет SDK получает сообщение в режиме `PeekLock` и вызывает метод `Complete` для сообщения, если функция выполнена успешно, или `Abandon` в случае сбоя.</span><span class="sxs-lookup"><span data-stu-id="6adb1-120">The SDK receives a message in `PeekLock` mode and calls `Complete` on the message if the function finishes successfully, or calls `Abandon` if the function fails.</span></span> <span data-ttu-id="6adb1-121">Если функция выполняется дольше времени ожидания `PeekLock` , блокировка возобновляется автоматически.</span><span class="sxs-lookup"><span data-stu-id="6adb1-121">If the function runs longer than the `PeekLock` timeout, the lock is automatically renewed.</span></span>

<span data-ttu-id="6adb1-122">В служебной шине выполняется собственная обработка очереди подозрительных сообщений, которую нельзя контролировать или настраивать с помощью пакета SDK веб-заданий.</span><span class="sxs-lookup"><span data-stu-id="6adb1-122">Service Bus does its own poison queue handling which cannot be controlled or configured by the WebJobs SDK.</span></span> 

### <a name="string-queue-message"></a><span data-ttu-id="6adb1-123">Строковое сообщение очереди</span><span class="sxs-lookup"><span data-stu-id="6adb1-123">String queue message</span></span>
<span data-ttu-id="6adb1-124">Следующий пример кода считывает сообщение очереди, содержащее строку, и записывает строку на панель мониторинга пакета SDK для заданий WebJob.</span><span class="sxs-lookup"><span data-stu-id="6adb1-124">The following code sample reads a queue message that contains a string and writes the string to the WebJobs SDK dashboard.</span></span>

        public static void ProcessQueueMessage([ServiceBusTrigger("inputqueue")] string message, 
            TextWriter logger)
        {
            logger.WriteLine(message);
        }

<span data-ttu-id="6adb1-125">**Примечание.** При создании сообщений очереди в приложении, которое не использует пакет SDK для веб-заданий, обязательно задайте для параметра [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) значение text/plain.</span><span class="sxs-lookup"><span data-stu-id="6adb1-125">**Note:** If you are creating the queue messages in an application that doesn't use the WebJobs SDK, make sure to set [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) to "text/plain".</span></span>

### <a name="poco-queue-message"></a><span data-ttu-id="6adb1-126">Сообщения очереди POCO</span><span class="sxs-lookup"><span data-stu-id="6adb1-126">POCO queue message</span></span>
<span data-ttu-id="6adb1-127">Пакет SDK автоматически десериализует сообщение очереди, содержащее тип JSON для объекта типа [POCO](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object).</span><span class="sxs-lookup"><span data-stu-id="6adb1-127">The SDK will automatically deserialize a queue message that contains JSON for a POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) type.</span></span> <span data-ttu-id="6adb1-128">Следующий пример кода считывает сообщение очереди, которое содержит объект `BlobInformation` со свойством `BlobName`:</span><span class="sxs-lookup"><span data-stu-id="6adb1-128">The following code sample reads a queue message that contains a `BlobInformation` object which has a `BlobName` property:</span></span>

        public static void WriteLogPOCO([ServiceBusTrigger("inputqueue")] BlobInformation blobInfo,
            TextWriter logger)
        {
            logger.WriteLine("Queue message refers to blob: " + blobInfo.BlobName);
        }

<span data-ttu-id="6adb1-129">Примеры кода, в которых показано, как использовать POCO для работы с большими двоичными объектами и таблицами в одной функции, см. в [версии этой статьи для очередей хранилища](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span><span class="sxs-lookup"><span data-stu-id="6adb1-129">For code samples showing how to use properties of the POCO to work with blobs and tables in the same function, see the [storage queues version of this article](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span></span>

<span data-ttu-id="6adb1-130">Если ваш код, создающий сообщения очереди, основан не на пакете SDK для веб-заданий, используйте код, аналогичный приведенному ниже:</span><span class="sxs-lookup"><span data-stu-id="6adb1-130">If your code that creates the queue message doesn't use the WebJobs SDK, use code similar to the following example:</span></span>

        var client = QueueClient.CreateFromConnectionString(ConfigurationManager.ConnectionStrings["AzureWebJobsServiceBus"].ConnectionString, "blobadded");
        BlobInformation blobInformation = new BlobInformation () ;
        var message = new BrokeredMessage(blobInformation);
        client.Send(message);

### <a name="types-servicebustrigger-works-with"></a><span data-ttu-id="6adb1-131">Типы, с которыми работает атрибут ServiceBusTrigger</span><span class="sxs-lookup"><span data-stu-id="6adb1-131">Types ServiceBusTrigger works with</span></span>
<span data-ttu-id="6adb1-132">Помимо `string` и типов POCO атрибут `ServiceBusTrigger` можно использовать с массивом байтов или объектом `BrokeredMessage`.</span><span class="sxs-lookup"><span data-stu-id="6adb1-132">Besides `string` and POCO  types, you can use the `ServiceBusTrigger` attribute with a byte array or a `BrokeredMessage` object.</span></span>

## <span data-ttu-id="6adb1-133"><a id="create"></a> Как создавать сообщения очереди служебной шины</span><span class="sxs-lookup"><span data-stu-id="6adb1-133"><a id="create"></a> How to create Service Bus queue messages</span></span>
<span data-ttu-id="6adb1-134">Чтобы написать функцию, которая создает новое сообщение очереди, используйте атрибут `ServiceBus` и передайте имя очереди конструктору атрибута.</span><span class="sxs-lookup"><span data-stu-id="6adb1-134">To write a function that creates a new queue message use the `ServiceBus` attribute and pass in the queue name to the attribute constructor.</span></span> 

### <a name="create-a-single-queue-message-in-a-non-async-function"></a><span data-ttu-id="6adb1-135">Создание одного сообщения очереди в неасинхронной функции</span><span class="sxs-lookup"><span data-stu-id="6adb1-135">Create a single queue message in a non-async function</span></span>
<span data-ttu-id="6adb1-136">В следующем примере кода используется выходной параметр для создания нового сообщения в очереди с именем outputqueue с тем же содержимым, что и сообщение очереди, поступившее в очередь с именем inputqueue.</span><span class="sxs-lookup"><span data-stu-id="6adb1-136">The following code sample uses an output parameter to create a new message in the queue named "outputqueue" with the same content as the message received in the queue named "inputqueue".</span></span>

        public static void CreateQueueMessage(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] out string outputQueueMessage)
        {
            outputQueueMessage = queueMessage;
        }

<span data-ttu-id="6adb1-137">Выходной параметр для создания одного сообщения очереди может принадлежать к любому из следующих типов:</span><span class="sxs-lookup"><span data-stu-id="6adb1-137">The output parameter for creating a single queue message can be any of the following types:</span></span>

* `string`
* `byte[]`
* `BrokeredMessage`
* <span data-ttu-id="6adb1-138">Сериализуемый тип POCO, заданный вами</span><span class="sxs-lookup"><span data-stu-id="6adb1-138">A serializable POCO type that you define.</span></span> <span data-ttu-id="6adb1-139">Сериализируется как JSON автоматически.</span><span class="sxs-lookup"><span data-stu-id="6adb1-139">Automatically serialized as JSON.</span></span>

<span data-ttu-id="6adb1-140">Для параметров типа POCO сообщение очереди всегда создается при завершении функции. Если значение параметра — NULL, пакет SDK создает сообщение очереди, которое вернет значение NULL при получении и десериализации сообщения.</span><span class="sxs-lookup"><span data-stu-id="6adb1-140">For POCO type parameters, a queue message is always created when the function ends; if the parameter is null, the SDK creates a queue message that will return null when the message is received and deserialized.</span></span> <span data-ttu-id="6adb1-141">Если значение параметра другого типа — NULL, сообщение очереди не создается.</span><span class="sxs-lookup"><span data-stu-id="6adb1-141">For the other types, if the parameter is null no queue message is created.</span></span>

### <a name="create-multiple-queue-messages-or-in-async-functions"></a><span data-ttu-id="6adb1-142">Создание нескольких сообщений очереди или сообщений в асинхронных функциях</span><span class="sxs-lookup"><span data-stu-id="6adb1-142">Create multiple queue messages or in async functions</span></span>
<span data-ttu-id="6adb1-143">Чтобы создать несколько сообщений, используйте атрибут `ServiceBus` с `ICollector<T>` или `IAsyncCollector<T>`, как показано в следующем примере кода.</span><span class="sxs-lookup"><span data-stu-id="6adb1-143">To create multiple messages, use  the `ServiceBus` attribute with `ICollector<T>` or `IAsyncCollector<T>`, as shown in the following code sample:</span></span>

        public static void CreateQueueMessages(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="6adb1-144">Каждое сообщение очереди создается сразу после вызова метода `Add` .</span><span class="sxs-lookup"><span data-stu-id="6adb1-144">Each queue message is created immediately when the `Add` method is called.</span></span>

## <span data-ttu-id="6adb1-145"><a id="topics"></a>Как работать с разделами служебной шины</span><span class="sxs-lookup"><span data-stu-id="6adb1-145"><a id="topics"></a>How to work with Service Bus topics</span></span>
<span data-ttu-id="6adb1-146">Чтобы написать функцию, которую пакет SDK будет вызывать при получении сообщения в раздел служебной шины, используйте атрибут `ServiceBusTrigger` с конструктором, принимающим имя раздела и подписки, как показано в следующем примере кода:</span><span class="sxs-lookup"><span data-stu-id="6adb1-146">To write a function that the SDK calls when a message is received on a Service Bus topic, use the `ServiceBusTrigger` attribute with the constructor that takes topic name and subscription name, as shown in the following code sample:</span></span>

        public static void WriteLog([ServiceBusTrigger("outputtopic","subscription1")] string message,
            TextWriter logger)
        {
            logger.WriteLine("Topic message: " + message);
        }

<span data-ttu-id="6adb1-147">Чтобы создать сообщение для раздела, используйте атрибут `ServiceBus` с именем раздела также, как при использовании с именем очереди.</span><span class="sxs-lookup"><span data-stu-id="6adb1-147">To create a message on a topic, use the `ServiceBus` attribute with a topic name the same way you use it with a queue name.</span></span>

## <a name="features-added-in-release-11"></a><span data-ttu-id="6adb1-148">Функции, добавленные в версии 1.1</span><span class="sxs-lookup"><span data-stu-id="6adb1-148">Features added in release 1.1</span></span>
<span data-ttu-id="6adb1-149">В версии 1.1 были добавлены следующие возможности:</span><span class="sxs-lookup"><span data-stu-id="6adb1-149">The following features were added in release 1.1:</span></span>

* <span data-ttu-id="6adb1-150">Добавлена возможность обширной настройки обработки сообщений с помощью `ServiceBusConfiguration.MessagingProvider`.</span><span class="sxs-lookup"><span data-stu-id="6adb1-150">Allow deep customization of message processing via `ServiceBusConfiguration.MessagingProvider`.</span></span>
* <span data-ttu-id="6adb1-151">`MessagingProvider` поддерживает настройку `MessagingFactory` и `NamespaceManager` служебной шины.</span><span class="sxs-lookup"><span data-stu-id="6adb1-151">`MessagingProvider` supports customization of the Service Bus `MessagingFactory` and `NamespaceManager`.</span></span>
* <span data-ttu-id="6adb1-152">Шаблон стратегии `MessageProcessor` позволяет указать процессор для каждой очереди или раздела.</span><span class="sxs-lookup"><span data-stu-id="6adb1-152">A `MessageProcessor` strategy pattern allows you to specify a processor per queue/topic.</span></span>
* <span data-ttu-id="6adb1-153">По умолчанию поддерживается параллелизм обработки сообщений.</span><span class="sxs-lookup"><span data-stu-id="6adb1-153">Message processing concurrency is supported by default.</span></span> 
* <span data-ttu-id="6adb1-154">Упрощена настройка `OnMessageOptions` через `ServiceBusConfiguration.MessageOptions`.</span><span class="sxs-lookup"><span data-stu-id="6adb1-154">Easy customization of `OnMessageOptions` via `ServiceBusConfiguration.MessageOptions`.</span></span>
* <span data-ttu-id="6adb1-155">Для `ServiceBusTriggerAttribute`/`ServiceBusAttribute` необходимо предоставить разрешение [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) (для сценариев, в которых возможно управление правами).</span><span class="sxs-lookup"><span data-stu-id="6adb1-155">Allow [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) to be specified on `ServiceBusTriggerAttribute`/`ServiceBusAttribute` (for scenarios where you might not have Manage rights).</span></span> <span data-ttu-id="6adb1-156">Обратите внимание, что веб-задания Azure не могут автоматически подготавливать несуществующие очереди и разделы без управления правами AccessRights.</span><span class="sxs-lookup"><span data-stu-id="6adb1-156">Note that Azure WebJobs is unable to automatically provision non-existent queues and topics without Manage AccessRights.</span></span>

## <span data-ttu-id="6adb1-157"><a id="queues"></a>Связанные разделы, которые описаны в практическом руководстве по работе с очередями хранилища</span><span class="sxs-lookup"><span data-stu-id="6adb1-157"><a id="queues"></a>Related topics covered by the storage queues how-to article</span></span>
<span data-ttu-id="6adb1-158">Информацию о сценариях SDK для веб-заданий, которые не относятся к служебной шине, см. в статье [Использование пакета SDK веб-заданий для работы с хранилищем очередей Azure](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="6adb1-158">For information about WebJobs SDK scenarios not specific to Service Bus, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="6adb1-159">В этой статье рассматриваются следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="6adb1-159">Topics covered in that article include the following:</span></span>

* <span data-ttu-id="6adb1-160">Асинхронные функции</span><span class="sxs-lookup"><span data-stu-id="6adb1-160">Async functions</span></span>
* <span data-ttu-id="6adb1-161">Выполнение на нескольких экземплярах</span><span class="sxs-lookup"><span data-stu-id="6adb1-161">Multiple instances</span></span>
* <span data-ttu-id="6adb1-162">Корректное завершение работы</span><span class="sxs-lookup"><span data-stu-id="6adb1-162">Graceful shutdown</span></span>
* <span data-ttu-id="6adb1-163">Использование атрибутов пакета SDK для заданий WebJob очереди в теле функции</span><span class="sxs-lookup"><span data-stu-id="6adb1-163">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="6adb1-164">Установка строк подключения пакета SDK в коде.</span><span class="sxs-lookup"><span data-stu-id="6adb1-164">Set the SDK connection strings in code</span></span>
* <span data-ttu-id="6adb1-165">Установка значений параметров конструктора пакета SDK для заданий WebJob в коде</span><span class="sxs-lookup"><span data-stu-id="6adb1-165">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="6adb1-166">Вызов функции вручную</span><span class="sxs-lookup"><span data-stu-id="6adb1-166">Trigger a function manually</span></span>
* <span data-ttu-id="6adb1-167">Запись журналов</span><span class="sxs-lookup"><span data-stu-id="6adb1-167">Write logs</span></span>

## <span data-ttu-id="6adb1-168"><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6adb1-168"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="6adb1-169">В этом руководстве предоставлены примеры кода обработки обычных сценариев для работы со служебной шиной Azure.</span><span class="sxs-lookup"><span data-stu-id="6adb1-169">This guide has provided code samples that show how to handle common scenarios for working with Azure Service Bus.</span></span> <span data-ttu-id="6adb1-170">Дополнительную информацию об использовании веб-заданий Azure и пакета SDK для веб-заданий см. в [рекомендуемых ресурсах для веб-заданий Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="6adb1-170">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

