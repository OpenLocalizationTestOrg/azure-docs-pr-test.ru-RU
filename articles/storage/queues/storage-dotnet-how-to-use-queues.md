---
title: "Приступая к работе с хранилищем очередей Azure с помощью .NET | Документация Майкрософт"
description: "Очереди хранилища обеспечивают надежный асинхронный обмен сообщениями между компонентами приложения. Обмен сообщениями в облаке позволяет масштабировать компоненты приложения независимо друг от друга."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: c0f82537-a613-4f01-b2ed-fc82e5eea2a7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: robinsh
ms.openlocfilehash: aa292c1eb048444f988a641df44183312cf39d28
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-queue-storage-using-net"></a><span data-ttu-id="3befc-104">Приступая к работе с хранилищем очередей Azure с помощью .NET</span><span class="sxs-lookup"><span data-stu-id="3befc-104">Get started with Azure Queue storage using .NET</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

## <a name="overview"></a><span data-ttu-id="3befc-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="3befc-105">Overview</span></span>
<span data-ttu-id="3befc-106">Хранилище очередей Azure — это служба, обеспечивающая обмен сообщениями в облаке между компонентами приложения.</span><span class="sxs-lookup"><span data-stu-id="3befc-106">Azure Queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="3befc-107">При разработке приложений для масштабирования компоненты приложения часто не связаны между собой, так что они могут масштабироваться независимо друг от друга.</span><span class="sxs-lookup"><span data-stu-id="3befc-107">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="3befc-108">Хранилище очередей обеспечивает асинхронный обмен сообщениями для взаимодействия между компонентами приложения независимо от того, где они выполняются: в облаке, на рабочем столе, локальном сервере или мобильном устройстве.</span><span class="sxs-lookup"><span data-stu-id="3befc-108">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in the cloud, on the desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="3befc-109">Хранилище очередей также поддерживает управление асинхронными задачами и создание рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="3befc-109">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="3befc-110">О данном учебнике</span><span class="sxs-lookup"><span data-stu-id="3befc-110">About this tutorial</span></span>
<span data-ttu-id="3befc-111">В этом руководстве показано, как написать код .NET для некоторых распространенных сценариев использования хранилища очередей Azure.</span><span class="sxs-lookup"><span data-stu-id="3befc-111">This tutorial shows how to write .NET code for some common scenarios using Azure Queue storage.</span></span> <span data-ttu-id="3befc-112">Эти сценарии включают создание и удаление очередей, а также добавление, чтение и удаление сообщений.</span><span class="sxs-lookup"><span data-stu-id="3befc-112">Scenarios covered include creating and deleting queues and adding, reading, and deleting queue messages.</span></span>

<span data-ttu-id="3befc-113">**Предполагаемое время выполнения:** 45 минут.</span><span class="sxs-lookup"><span data-stu-id="3befc-113">**Estimated time to complete:** 45 minutes</span></span>

<span data-ttu-id="3befc-114">**Предварительные требования**</span><span class="sxs-lookup"><span data-stu-id="3befc-114">**Prerequisities:**</span></span>

* [<span data-ttu-id="3befc-115">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3befc-115">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="3befc-116">Клиентская библиотека хранилища Azure для .NET</span><span class="sxs-lookup"><span data-stu-id="3befc-116">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="3befc-117">Диспетчер конфигураций Azure для .NET</span><span class="sxs-lookup"><span data-stu-id="3befc-117">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="3befc-118">[учетная запись хранения Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="3befc-118">An [Azure storage account](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../../includes/storage-dotnet-client-library-version-include.md)]

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="3befc-119">Добавление директив using</span><span class="sxs-lookup"><span data-stu-id="3befc-119">Add using directives</span></span>
<span data-ttu-id="3befc-120">Добавьте в верхнюю часть файла `Program.cs` следующие директивы `using`:</span><span class="sxs-lookup"><span data-stu-id="3befc-120">Add the following `using` directives to the top of the `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Queue; // Namespace for Queue storage types
```

### <a name="parse-the-connection-string"></a><span data-ttu-id="3befc-121">Анализ строки подключения</span><span class="sxs-lookup"><span data-stu-id="3befc-121">Parse the connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-the-queue-service-client"></a><span data-ttu-id="3befc-122">Создание клиента службы очередей</span><span class="sxs-lookup"><span data-stu-id="3befc-122">Create the Queue service client</span></span>
<span data-ttu-id="3befc-123">Класс **CloudQueueClient** позволяет получать очереди, хранящиеся в хранилище очередей.</span><span class="sxs-lookup"><span data-stu-id="3befc-123">The **CloudQueueClient** class enables you to retrieve queues stored in Queue storage.</span></span> <span data-ttu-id="3befc-124">Вот один из способов создать клиента службы.</span><span class="sxs-lookup"><span data-stu-id="3befc-124">Here's one way to create the service client:</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
```
    
<span data-ttu-id="3befc-125">Теперь вы можете написать код, который считывает и записывает данные в хранилище очередей.</span><span class="sxs-lookup"><span data-stu-id="3befc-125">Now you are ready to write code that reads data from and writes data to Queue storage.</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="3befc-126">Создание очереди</span><span class="sxs-lookup"><span data-stu-id="3befc-126">Create a queue</span></span>
<span data-ttu-id="3befc-127">В этом примере показано, как создать очередь, если она не существует:</span><span class="sxs-lookup"><span data-stu-id="3befc-127">This example shows how to create a queue if it does not already exist:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a container.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create the queue if it doesn't already exist
queue.CreateIfNotExists();
```

## <a name="insert-a-message-into-a-queue"></a><span data-ttu-id="3befc-128">Вставка сообщения в очередь</span><span class="sxs-lookup"><span data-stu-id="3befc-128">Insert a message into a queue</span></span>
<span data-ttu-id="3befc-129">Чтобы вставить сообщение в существующую очередь, сначала создайте новый объект **CloudQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="3befc-129">To insert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="3befc-130">Затем вызовите метод **AddMessage**.</span><span class="sxs-lookup"><span data-stu-id="3befc-130">Next, call the **AddMessage** method.</span></span> <span data-ttu-id="3befc-131">Для создания объекта **CloudQueueMessage** можно использовать строку (в формате UTF-8) или массив **байтов**.</span><span class="sxs-lookup"><span data-stu-id="3befc-131">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a **byte** array.</span></span> <span data-ttu-id="3befc-132">Ниже приведен код, который создает очередь (если она отсутствует) и вставляет сообщение "Hello World".</span><span class="sxs-lookup"><span data-stu-id="3befc-132">Here is code which creates a queue (if it doesn't exist) and inserts the message 'Hello, World':</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create the queue if it doesn't already exist.
queue.CreateIfNotExists();

// Create a message and add it to the queue.
CloudQueueMessage message = new CloudQueueMessage("Hello, World");
queue.AddMessage(message);
```

## <a name="peek-at-the-next-message"></a><span data-ttu-id="3befc-133">Просмотр следующего сообщения</span><span class="sxs-lookup"><span data-stu-id="3befc-133">Peek at the next message</span></span>
<span data-ttu-id="3befc-134">Просмотреть сообщение в начале очереди, не удаляя его, можно с помощью метода **PeekMessage** .</span><span class="sxs-lookup"><span data-stu-id="3befc-134">You can peek at the message in the front of a queue without removing it from the queue by calling the **PeekMessage** method.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Peek at the next message
CloudQueueMessage peekedMessage = queue.PeekMessage();

// Display message.
Console.WriteLine(peekedMessage.AsString);
```

## <a name="change-the-contents-of-a-queued-message"></a><span data-ttu-id="3befc-135">Изменение содержимого сообщения в очереди</span><span class="sxs-lookup"><span data-stu-id="3befc-135">Change the contents of a queued message</span></span>
<span data-ttu-id="3befc-136">Вы можете изменить содержимое сообщения непосредственно в очереди.</span><span class="sxs-lookup"><span data-stu-id="3befc-136">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="3befc-137">Если сообщение представляет собой рабочую задачу, можно использовать эту функцию для обновления состояния рабочей задачи.</span><span class="sxs-lookup"><span data-stu-id="3befc-137">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="3befc-138">Следующий код добавляет новое содержимое в очередь сообщений и продлевает время ожидания видимости еще на 60 секунд.</span><span class="sxs-lookup"><span data-stu-id="3befc-138">The following code updates the queue message with new contents, and sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="3befc-139">Это сохраняет состояние работы, связанной с данным сообщением, и позволяет клиенту продолжить работу с сообщением на протяжении еще одной минуты.</span><span class="sxs-lookup"><span data-stu-id="3befc-139">This saves the state of work associated with the message, and gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="3befc-140">Этот метод можно использовать для отслеживания многошаговых рабочих процессов по сообщениям в очереди без необходимости начинать с самого начала в случае сбоя шага обработки в связи с ошибкой аппаратного или программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="3befc-140">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="3befc-141">Обычно также сохраняется счетчик повторов. Если количество повторов сообщения превысит *n* раз, его нужно удалить.</span><span class="sxs-lookup"><span data-stu-id="3befc-141">Typically, you would keep a retry count as well, and if the message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="3befc-142">Это обеспечивает защиту от сообщений, которые инициируют ошибку приложения при каждой попытке обработки.</span><span class="sxs-lookup"><span data-stu-id="3befc-142">This protects against a message that triggers an application error each time it is processed.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get the message from the queue and update the message contents.
CloudQueueMessage message = queue.GetMessage();
message.SetMessageContent("Updated contents.");
queue.UpdateMessage(message,
    TimeSpan.FromSeconds(60.0),  // Make it invisible for another 60 seconds.
    MessageUpdateFields.Content | MessageUpdateFields.Visibility);
```

## <a name="de-queue-the-next-message"></a><span data-ttu-id="3befc-143">Удаление следующего сообщения из очереди</span><span class="sxs-lookup"><span data-stu-id="3befc-143">De-queue the next message</span></span>
<span data-ttu-id="3befc-144">Код удаляет сообщение из очереди в два этапа.</span><span class="sxs-lookup"><span data-stu-id="3befc-144">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="3befc-145">При вызове метода **GetMessage**вы получаете следующее сообщение в очереди.</span><span class="sxs-lookup"><span data-stu-id="3befc-145">When you call **GetMessage**, you get the next message in a queue.</span></span> <span data-ttu-id="3befc-146">Сообщение, возвращаемое методом **GetMessage** , становится невидимым для другого кода, считывающего сообщения из этой очереди.</span><span class="sxs-lookup"><span data-stu-id="3befc-146">A message returned from **GetMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="3befc-147">По умолчанию это сообщение остается невидимым в течение 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="3befc-147">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="3befc-148">Чтобы завершить удаление сообщения из очереди, необходимо также вызвать метод **DeleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="3befc-148">To finish removing the message from the queue, you must also call **DeleteMessage**.</span></span> <span data-ttu-id="3befc-149">Этот двухэтапный процесс удаления сообщения позволяет удостовериться, что если коду не удастся обработать сообщение из-за сбоя оборудования или программного обеспечения, другой экземпляр кода сможет получить то же сообщение и повторить попытку.</span><span class="sxs-lookup"><span data-stu-id="3befc-149">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="3befc-150">Код вызывает метод **DeleteMessage** сразу после обработки сообщения.</span><span class="sxs-lookup"><span data-stu-id="3befc-150">Your code calls **DeleteMessage** right after the message has been processed.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get the next message
CloudQueueMessage retrievedMessage = queue.GetMessage();

//Process the message in less than 30 seconds, and then delete the message
queue.DeleteMessage(retrievedMessage);
```

## <a name="use-async-await-pattern-with-common-queue-storage-apis"></a><span data-ttu-id="3befc-151">Использование алгоритма Async-Await со стандартными интерфейсами API хранилища очередей</span><span class="sxs-lookup"><span data-stu-id="3befc-151">Use Async-Await pattern with common Queue storage APIs</span></span>
<span data-ttu-id="3befc-152">В этом примере показано использование алгоритма Async-Await со стандартными интерфейсами API хранилища очередей.</span><span class="sxs-lookup"><span data-stu-id="3befc-152">This example shows how to use the Async-Await pattern with common Queue storage APIs.</span></span> <span data-ttu-id="3befc-153">Вызывается асинхронная версия каждого из методов, на что указывает суффикс *Async* в их названиях.</span><span class="sxs-lookup"><span data-stu-id="3befc-153">The sample calls the asynchronous version of each of the given methods, as indicated by the *Async* suffix of each method.</span></span> <span data-ttu-id="3befc-154">При использовании асинхронного метода алгоритм Async-Await приостанавливает локальное выполнение процесса до завершения вызова.</span><span class="sxs-lookup"><span data-stu-id="3befc-154">When an async method is used, the async-await pattern suspends local execution until the call completes.</span></span> <span data-ttu-id="3befc-155">Благодаря этому текущий поток может выполнять другие задачи, что позволяет избежать возникновения узких мест и повысить общую скорость реагирования приложения.</span><span class="sxs-lookup"><span data-stu-id="3befc-155">This behavior allows the current thread to do other work, which helps avoid performance bottlenecks and improves the overall responsiveness of your application.</span></span> <span data-ttu-id="3befc-156">Дополнительные сведения об использовании алгоритма Async-Await в .NET см. в статье [Асинхронное программирование с использованием ключевых слов Async и Await (C# и Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).</span><span class="sxs-lookup"><span data-stu-id="3befc-156">For more details on using the Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

```csharp
// Create the queue if it doesn't already exist
if(await queue.CreateIfNotExistsAsync())
{
    Console.WriteLine("Queue '{0}' Created", queue.Name);
}
else
{
    Console.WriteLine("Queue '{0}' Exists", queue.Name);
}

// Create a message to put in the queue
CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

// Async enqueue the message
await queue.AddMessageAsync(cloudQueueMessage);
Console.WriteLine("Message added");

// Async dequeue the message
CloudQueueMessage retrievedMessage = await queue.GetMessageAsync();
Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

// Async delete the message
await queue.DeleteMessageAsync(retrievedMessage);
Console.WriteLine("Deleted message");
```
    
## <a name="leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="3befc-157">Дополнительные параметры для удаления сообщений из очереди</span><span class="sxs-lookup"><span data-stu-id="3befc-157">Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="3befc-158">Способ извлечения сообщения из очереди можно настроить двумя способами.</span><span class="sxs-lookup"><span data-stu-id="3befc-158">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="3befc-159">Во-первых, можно получить пакет сообщений (до 32 сообщений).</span><span class="sxs-lookup"><span data-stu-id="3befc-159">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="3befc-160">Во-вторых, можно задать более длительное или короткое время ожидания видимости, чтобы предоставить коду больше или меньше времени на полную обработку каждого сообщения.</span><span class="sxs-lookup"><span data-stu-id="3befc-160">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="3befc-161">В следующем примере кода метод **GetMessages** используется для получения 20 сообщений в одном вызове.</span><span class="sxs-lookup"><span data-stu-id="3befc-161">The following code example uses the **GetMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="3befc-162">Затем он обрабатывает каждое сообщение с помощью цикла **foreach** .</span><span class="sxs-lookup"><span data-stu-id="3befc-162">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="3befc-163">Он также задает время ожидания невидимости 5 минут для каждого сообщения.</span><span class="sxs-lookup"><span data-stu-id="3befc-163">It also sets the invisibility timeout to five minutes for each message.</span></span> <span data-ttu-id="3befc-164">Обратите внимание на то, что пятиминутный период начинается для всех сообщений одновременно, поэтому по прошествии пяти минут с момента вызова **GetMessages**все сообщения, которые не были удалены, снова становятся видимыми.</span><span class="sxs-lookup"><span data-stu-id="3befc-164">Note that the 5 minutes starts for all messages at the same time, so after 5 minutes have passed since the call to **GetMessages**, any messages which have not been deleted will become visible again.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

foreach (CloudQueueMessage message in queue.GetMessages(20, TimeSpan.FromMinutes(5)))
{
    // Process all messages in less than 5 minutes, deleting each message after processing.
    queue.DeleteMessage(message);
}
```

## <a name="get-the-queue-length"></a><span data-ttu-id="3befc-165">Получение длины очереди</span><span class="sxs-lookup"><span data-stu-id="3befc-165">Get the queue length</span></span>
<span data-ttu-id="3befc-166">Вы можете узнать приблизительное количество сообщений в очереди.</span><span class="sxs-lookup"><span data-stu-id="3befc-166">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="3befc-167">Метод **FetchAttributes** отправляет в службу очередей запрос на извлечение атрибутов очереди, включая количество сообщений.</span><span class="sxs-lookup"><span data-stu-id="3befc-167">The **FetchAttributes** method asks the Queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="3befc-168">Свойство **ApproximateMessageCount** возвращает последнее значение, полученное с использованием метода **FetchAttributes**, без обращения к службе очередей.</span><span class="sxs-lookup"><span data-stu-id="3befc-168">The **ApproximateMessageCount** property returns the last value retrieved by the **FetchAttributes** method, without calling the Queue service.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Fetch the queue attributes.
queue.FetchAttributes();

// Retrieve the cached approximate message count.
int? cachedMessageCount = queue.ApproximateMessageCount;

// Display number of messages.
Console.WriteLine("Number of messages in queue: " + cachedMessageCount);
```

## <a name="delete-a-queue"></a><span data-ttu-id="3befc-169">Удаление очереди</span><span class="sxs-lookup"><span data-stu-id="3befc-169">Delete a queue</span></span>
<span data-ttu-id="3befc-170">Чтобы удалить очередь и все сообщения в ней, вызовите метод **Delete** для объекта очереди.</span><span class="sxs-lookup"><span data-stu-id="3befc-170">To delete a queue and all the messages contained in it, call the **Delete** method on the queue object.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Delete the queue.
queue.Delete();
```
    

## <a name="next-steps"></a><span data-ttu-id="3befc-171">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3befc-171">Next steps</span></span>
<span data-ttu-id="3befc-172">Вы изучили основные сведения о хранилище очередей. Дополнительные сведения о более сложных задачах по использованию хранилища можно найти по следующим ссылкам.</span><span class="sxs-lookup"><span data-stu-id="3befc-172">Now that you've learned the basics of Queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="3befc-173">Дополнительные сведения о доступных API-интерфейсах см. в справочной документации по службе очередей:</span><span class="sxs-lookup"><span data-stu-id="3befc-173">View the Queue service reference documentation for complete details about available APIs:</span></span>
  * [<span data-ttu-id="3befc-174">Справочник по клиентской библиотеке хранилища для .NET</span><span class="sxs-lookup"><span data-stu-id="3befc-174">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
  * [<span data-ttu-id="3befc-175">Справочник по REST API</span><span class="sxs-lookup"><span data-stu-id="3befc-175">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="3befc-176">Узнайте, как упростить код, предназначенный для работы со службой хранилища Azure, с помощью [пакета SDK для веб-заданий Azure](../../app-service-web/websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="3befc-176">Learn how to simplify the code you write to work with Azure Storage by using the [Azure WebJobs SDK](../../app-service-web/websites-dotnet-webjobs-sdk.md).</span></span>
* <span data-ttu-id="3befc-177">Просмотрите дополнительные руководства, чтобы изучить дополнительные возможности хранения данных в Azure.</span><span class="sxs-lookup"><span data-stu-id="3befc-177">View more feature guides to learn about additional options for storing data in Azure.</span></span>
  * <span data-ttu-id="3befc-178">[Приступая к работе с хранилищем таблиц Azure с помощью .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md) .</span><span class="sxs-lookup"><span data-stu-id="3befc-178">[Get started with Azure Table storage using .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md) to store structured data.</span></span>
  * <span data-ttu-id="3befc-179">[Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](../blobs/storage-dotnet-how-to-use-blobs.md) .</span><span class="sxs-lookup"><span data-stu-id="3befc-179">[Get started with Azure Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) to store unstructured data.</span></span>
  * <span data-ttu-id="3befc-180">Информацию о хранении реляционных данных см. в статье [Подключение к базе данных SQL с помощью .NET (C#)](../../sql-database/sql-database-connect-query-dotnet-core.md).</span><span class="sxs-lookup"><span data-stu-id="3befc-180">[Connect to SQL Database by using .NET (C#)](../../sql-database/sql-database-connect-query-dotnet-core.md) to store relational data.</span></span>

[Download and install the Azure SDK for .NET]: /develop/net/
[.NET client library reference]: http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409
[Creating a Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[OData]: http://nuget.org/packages/Microsoft.Data.OData/5.0.2
[Edm]: http://nuget.org/packages/Microsoft.Data.Edm/5.0.2
[Spatial]: http://nuget.org/packages/System.Spatial/5.0.2
