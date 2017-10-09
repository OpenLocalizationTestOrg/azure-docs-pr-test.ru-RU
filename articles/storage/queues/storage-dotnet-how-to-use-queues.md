---
title: "aaaGet работы с хранилищем очередей Azure, с помощью .NET | Документы Microsoft"
description: "Очереди хранилища обеспечивают надежный асинхронный обмен сообщениями между компонентами приложения. Облака обмена сообщениями позволяет tooscale компоненты вашего приложения независимо друг от друга."
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
ms.openlocfilehash: 0cf6a71392b2fe859c7c9a9898c1ec84bcab4b19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-using-net"></a><span data-ttu-id="a45e3-104">Приступая к работе с хранилищем очередей Azure с помощью .NET</span><span class="sxs-lookup"><span data-stu-id="a45e3-104">Get started with Azure Queue storage using .NET</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

## <a name="overview"></a><span data-ttu-id="a45e3-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="a45e3-105">Overview</span></span>
<span data-ttu-id="a45e3-106">Хранилище очередей Azure — это служба, обеспечивающая обмен сообщениями в облаке между компонентами приложения.</span><span class="sxs-lookup"><span data-stu-id="a45e3-106">Azure Queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="a45e3-107">При разработке приложений для масштабирования компоненты приложения часто не связаны между собой, так что они могут масштабироваться независимо друг от друга.</span><span class="sxs-lookup"><span data-stu-id="a45e3-107">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="a45e3-108">Хранилище очередей обеспечивает асинхронный обмен сообщениями для взаимодействия между компонентами приложения, ли они выполняются в облаке hello, на рабочем столе hello, на локальном сервере или на мобильном устройстве.</span><span class="sxs-lookup"><span data-stu-id="a45e3-108">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in hello cloud, on hello desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="a45e3-109">Хранилище очередей также поддерживает управление асинхронными задачами и создание рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="a45e3-109">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="a45e3-110">О данном учебнике</span><span class="sxs-lookup"><span data-stu-id="a45e3-110">About this tutorial</span></span>
<span data-ttu-id="a45e3-111">В этом учебнике показано, как toowrite .NET кода в некоторых распространенных сценариях, с помощью хранилища очередей Azure.</span><span class="sxs-lookup"><span data-stu-id="a45e3-111">This tutorial shows how toowrite .NET code for some common scenarios using Azure Queue storage.</span></span> <span data-ttu-id="a45e3-112">Эти сценарии включают создание и удаление очередей, а также добавление, чтение и удаление сообщений.</span><span class="sxs-lookup"><span data-stu-id="a45e3-112">Scenarios covered include creating and deleting queues and adding, reading, and deleting queue messages.</span></span>

<span data-ttu-id="a45e3-113">**Предполагаемое время toocomplete:** 45 минут</span><span class="sxs-lookup"><span data-stu-id="a45e3-113">**Estimated time toocomplete:** 45 minutes</span></span>

<span data-ttu-id="a45e3-114">**Предварительные требования**</span><span class="sxs-lookup"><span data-stu-id="a45e3-114">**Prerequisities:**</span></span>

* [<span data-ttu-id="a45e3-115">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a45e3-115">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="a45e3-116">Клиентская библиотека хранилища Azure для .NET</span><span class="sxs-lookup"><span data-stu-id="a45e3-116">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="a45e3-117">Диспетчер конфигураций Azure для .NET</span><span class="sxs-lookup"><span data-stu-id="a45e3-117">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="a45e3-118">[учетная запись хранения Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="a45e3-118">An [Azure storage account](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../../includes/storage-dotnet-client-library-version-include.md)]

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="a45e3-119">Добавление директив using</span><span class="sxs-lookup"><span data-stu-id="a45e3-119">Add using directives</span></span>
<span data-ttu-id="a45e3-120">Добавьте следующее hello `using` директивы toohello вверху hello `Program.cs` файла:</span><span class="sxs-lookup"><span data-stu-id="a45e3-120">Add hello following `using` directives toohello top of hello `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Queue; // Namespace for Queue storage types
```

### <a name="parse-hello-connection-string"></a><span data-ttu-id="a45e3-121">Синтаксический анализ строки соединения hello</span><span class="sxs-lookup"><span data-stu-id="a45e3-121">Parse hello connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-queue-service-client"></a><span data-ttu-id="a45e3-122">Создание клиента службы очередей hello</span><span class="sxs-lookup"><span data-stu-id="a45e3-122">Create hello Queue service client</span></span>
<span data-ttu-id="a45e3-123">Hello **CloudQueueClient** класс позволяет вам tooretrieve очереди, хранящиеся в очереди хранилища.</span><span class="sxs-lookup"><span data-stu-id="a45e3-123">hello **CloudQueueClient** class enables you tooretrieve queues stored in Queue storage.</span></span> <span data-ttu-id="a45e3-124">Вот один из способов toocreate hello службы клиента.</span><span class="sxs-lookup"><span data-stu-id="a45e3-124">Here's one way toocreate hello service client:</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
```
    
<span data-ttu-id="a45e3-125">Теперь все готово toowrite код, который считывает и записывает tooQueue хранения данных.</span><span class="sxs-lookup"><span data-stu-id="a45e3-125">Now you are ready toowrite code that reads data from and writes data tooQueue storage.</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="a45e3-126">Создание очереди</span><span class="sxs-lookup"><span data-stu-id="a45e3-126">Create a queue</span></span>
<span data-ttu-id="a45e3-127">В этом примере показано, как toocreate очереди, если он еще не существует:</span><span class="sxs-lookup"><span data-stu-id="a45e3-127">This example shows how toocreate a queue if it does not already exist:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa container.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create hello queue if it doesn't already exist
queue.CreateIfNotExists();
```

## <a name="insert-a-message-into-a-queue"></a><span data-ttu-id="a45e3-128">Вставка сообщения в очередь</span><span class="sxs-lookup"><span data-stu-id="a45e3-128">Insert a message into a queue</span></span>
<span data-ttu-id="a45e3-129">tooinsert сообщения в существующую очередь, сначала создайте **CloudQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="a45e3-129">tooinsert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="a45e3-130">Затем вызовите hello **AddMessage** метод.</span><span class="sxs-lookup"><span data-stu-id="a45e3-130">Next, call hello **AddMessage** method.</span></span> <span data-ttu-id="a45e3-131">Для создания объекта **CloudQueueMessage** можно использовать строку (в формате UTF-8) или массив **байтов**.</span><span class="sxs-lookup"><span data-stu-id="a45e3-131">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a **byte** array.</span></span> <span data-ttu-id="a45e3-132">Ниже приведен код (если он не существует), который создает очередь и вставок приветственное сообщение «Hello, World»:</span><span class="sxs-lookup"><span data-stu-id="a45e3-132">Here is code which creates a queue (if it doesn't exist) and inserts hello message 'Hello, World':</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create hello queue if it doesn't already exist.
queue.CreateIfNotExists();

// Create a message and add it toohello queue.
CloudQueueMessage message = new CloudQueueMessage("Hello, World");
queue.AddMessage(message);
```

## <a name="peek-at-hello-next-message"></a><span data-ttu-id="a45e3-133">Просмотр следующего сообщения hello</span><span class="sxs-lookup"><span data-stu-id="a45e3-133">Peek at hello next message</span></span>
<span data-ttu-id="a45e3-134">Можно считывать сообщения hello в hello передней части очереди, не удаляя его из очереди hello, вызывающему Привет **PeekMessage** метод.</span><span class="sxs-lookup"><span data-stu-id="a45e3-134">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **PeekMessage** method.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Peek at hello next message
CloudQueueMessage peekedMessage = queue.PeekMessage();

// Display message.
Console.WriteLine(peekedMessage.AsString);
```

## <a name="change-hello-contents-of-a-queued-message"></a><span data-ttu-id="a45e3-135">Изменить содержимое hello сообщение из очереди</span><span class="sxs-lookup"><span data-stu-id="a45e3-135">Change hello contents of a queued message</span></span>
<span data-ttu-id="a45e3-136">Вы можете изменить содержимое сообщений на месте в очереди hello hello.</span><span class="sxs-lookup"><span data-stu-id="a45e3-136">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="a45e3-137">Если сообщение представляет рабочей задачи, можно использовать этот компонент tooupdate состояние hello рабочих задач.</span><span class="sxs-lookup"><span data-stu-id="a45e3-137">If the message represents a work task, you could use this feature tooupdate the status of hello work task.</span></span> <span data-ttu-id="a45e3-138">После кода Hello обновляется приветственное сообщение очереди новое содержимое и наборы hello tooextend время ожидания видимости другой 60 секунд.</span><span class="sxs-lookup"><span data-stu-id="a45e3-138">hello following code updates hello queue message with new contents, and sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="a45e3-139">Сохраняет состояние работ, сопряженные с приветственное сообщение hello и предоставляет другой минуты toocontinue работа на приветственное сообщение клиента hello.</span><span class="sxs-lookup"><span data-stu-id="a45e3-139">This saves hello state of work associated with hello message, and gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="a45e3-140">Можно использовать этот рабочих процессов способ tootrack многоэтапной для очереди сообщений без необходимости toostart через от начала hello при неудачном завершении шага обработки из-за toohardware или ошибок программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="a45e3-140">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="a45e3-141">Как правило, будет хранить значение числа повторов, и если hello сообщение повторяется более  *n*  раз, следует удалить его.</span><span class="sxs-lookup"><span data-stu-id="a45e3-141">Typically, you would keep a retry count as well, and if hello message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="a45e3-142">Это обеспечивает защиту от сообщений, которые инициируют ошибку приложения при каждой попытке обработки.</span><span class="sxs-lookup"><span data-stu-id="a45e3-142">This protects against a message that triggers an application error each time it is processed.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get hello message from hello queue and update hello message contents.
CloudQueueMessage message = queue.GetMessage();
message.SetMessageContent("Updated contents.");
queue.UpdateMessage(message,
    TimeSpan.FromSeconds(60.0),  // Make it invisible for another 60 seconds.
    MessageUpdateFields.Content | MessageUpdateFields.Visibility);
```

## <a name="de-queue-hello-next-message"></a><span data-ttu-id="a45e3-143">Отмена очередь следующего сообщения hello</span><span class="sxs-lookup"><span data-stu-id="a45e3-143">De-queue hello next message</span></span>
<span data-ttu-id="a45e3-144">Код удаляет сообщение из очереди в два этапа.</span><span class="sxs-lookup"><span data-stu-id="a45e3-144">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="a45e3-145">При вызове **GetMessage**, вы получаете следующее сообщение hello в очереди.</span><span class="sxs-lookup"><span data-stu-id="a45e3-145">When you call **GetMessage**, you get hello next message in a queue.</span></span> <span data-ttu-id="a45e3-146">Сообщение, возвращенное из **GetMessage** становится невидимой tooany другой код, чтение сообщений из этой очереди.</span><span class="sxs-lookup"><span data-stu-id="a45e3-146">A message returned from **GetMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="a45e3-147">По умолчанию это сообщение остается невидимым в течение 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="a45e3-147">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="a45e3-148">toofinish удаление приветственное сообщение из очереди hello, необходимо также вызвать **DeleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="a45e3-148">toofinish removing hello message from hello queue, you must also call **DeleteMessage**.</span></span> <span data-ttu-id="a45e3-149">Это двухэтапный процесс удаления сообщения подтверждает, если tooprocess получит сообщение toohardware или ошибок программного обеспечения, другой экземпляр кода из-за сбоя программы hello одного сообщения и повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="a45e3-149">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="a45e3-150">Вызовы кода **DeleteMessage** сразу после обработки сообщения hello.</span><span class="sxs-lookup"><span data-stu-id="a45e3-150">Your code calls **DeleteMessage** right after hello message has been processed.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get hello next message
CloudQueueMessage retrievedMessage = queue.GetMessage();

//Process hello message in less than 30 seconds, and then delete hello message
queue.DeleteMessage(retrievedMessage);
```

## <a name="use-async-await-pattern-with-common-queue-storage-apis"></a><span data-ttu-id="a45e3-151">Использование алгоритма Async-Await со стандартными интерфейсами API хранилища очередей</span><span class="sxs-lookup"><span data-stu-id="a45e3-151">Use Async-Await pattern with common Queue storage APIs</span></span>
<span data-ttu-id="a45e3-152">В этом примере показано, как hello toouse Async-Await шаблона с хранилищем общих очередей API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="a45e3-152">This example shows how toouse hello Async-Await pattern with common Queue storage APIs.</span></span> <span data-ttu-id="a45e3-153">Образец Hello вызывает hello асинхронную версию каждого hello, учитывая методы, как указано в hello *Async* суффикс каждого метода.</span><span class="sxs-lookup"><span data-stu-id="a45e3-153">hello sample calls hello asynchronous version of each of hello given methods, as indicated by hello *Async* suffix of each method.</span></span> <span data-ttu-id="a45e3-154">При использовании асинхронного метода hello async-await шаблон приостанавливает локальное выполнение до завершения вызова hello.</span><span class="sxs-lookup"><span data-stu-id="a45e3-154">When an async method is used, hello async-await pattern suspends local execution until hello call completes.</span></span> <span data-ttu-id="a45e3-155">Такое поведение позволяет hello текущий поток toodo другие типы работ, что позволяет избежать проблем с производительностью и повышает общую скорость реагирования приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a45e3-155">This behavior allows hello current thread toodo other work, which helps avoid performance bottlenecks and improves hello overall responsiveness of your application.</span></span> <span data-ttu-id="a45e3-156">Дополнительные сведения об использовании hello шаблон Async-Await в .NET см. в разделе [Async и Await (C# и Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="a45e3-156">For more details on using hello Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

```csharp
// Create hello queue if it doesn't already exist
if(await queue.CreateIfNotExistsAsync())
{
    Console.WriteLine("Queue '{0}' Created", queue.Name);
}
else
{
    Console.WriteLine("Queue '{0}' Exists", queue.Name);
}

// Create a message tooput in hello queue
CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

// Async enqueue hello message
await queue.AddMessageAsync(cloudQueueMessage);
Console.WriteLine("Message added");

// Async dequeue hello message
CloudQueueMessage retrievedMessage = await queue.GetMessageAsync();
Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

// Async delete hello message
await queue.DeleteMessageAsync(retrievedMessage);
Console.WriteLine("Deleted message");
```
    
## <a name="leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="a45e3-157">Дополнительные параметры для удаления сообщений из очереди</span><span class="sxs-lookup"><span data-stu-id="a45e3-157">Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="a45e3-158">Способ извлечения сообщения из очереди можно настроить двумя способами.</span><span class="sxs-lookup"><span data-stu-id="a45e3-158">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="a45e3-159">Во-первых можно получить пакет сообщений (вверх too32).</span><span class="sxs-lookup"><span data-stu-id="a45e3-159">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="a45e3-160">Во-вторых можно задать более длинный или короткий невидимости тайм-аута, позволяя вашему коду больше или меньше toofully времени обработки каждого сообщения.</span><span class="sxs-lookup"><span data-stu-id="a45e3-160">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="a45e3-161">Hello следующий пример кода использует **GetMessages** метод tooget 20 сообщений в одном вызове.</span><span class="sxs-lookup"><span data-stu-id="a45e3-161">hello following code example uses the **GetMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="a45e3-162">Затем он обрабатывает каждое сообщение с помощью цикла **foreach** .</span><span class="sxs-lookup"><span data-stu-id="a45e3-162">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="a45e3-163">Он также устанавливает минут toofive hello невидимости время ожидания для каждого сообщения.</span><span class="sxs-lookup"><span data-stu-id="a45e3-163">It also sets hello invisibility timeout toofive minutes for each message.</span></span> <span data-ttu-id="a45e3-164">Обратите внимание, что hello 5 минут запускается для всех сообщений в hello же время, поэтому после 5 минут с момента вызова hello слишком**GetMessages**, все сообщения, которые не были удалены становятся видимыми.</span><span class="sxs-lookup"><span data-stu-id="a45e3-164">Note that hello 5 minutes starts for all messages at hello same time, so after 5 minutes have passed since hello call too**GetMessages**, any messages which have not been deleted will become visible again.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

foreach (CloudQueueMessage message in queue.GetMessages(20, TimeSpan.FromMinutes(5)))
{
    // Process all messages in less than 5 minutes, deleting each message after processing.
    queue.DeleteMessage(message);
}
```

## <a name="get-hello-queue-length"></a><span data-ttu-id="a45e3-165">Получает длину очереди hello</span><span class="sxs-lookup"><span data-stu-id="a45e3-165">Get hello queue length</span></span>
<span data-ttu-id="a45e3-166">Можно получить оценку hello количество сообщений в очереди.</span><span class="sxs-lookup"><span data-stu-id="a45e3-166">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="a45e3-167">**FetchAttributes** метод запрашивает hello службы очередей для получения атрибутов hello очереди, включая количество сообщений hello.</span><span class="sxs-lookup"><span data-stu-id="a45e3-167">The **FetchAttributes** method asks hello Queue service to retrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="a45e3-168">Hello **ApproximateMessageCount** свойство возвращает последнее значение hello извлекается с **FetchAttributes** метод без вызова службы очередей hello.</span><span class="sxs-lookup"><span data-stu-id="a45e3-168">hello **ApproximateMessageCount** property returns hello last value retrieved by the **FetchAttributes** method, without calling hello Queue service.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Fetch hello queue attributes.
queue.FetchAttributes();

// Retrieve hello cached approximate message count.
int? cachedMessageCount = queue.ApproximateMessageCount;

// Display number of messages.
Console.WriteLine("Number of messages in queue: " + cachedMessageCount);
```

## <a name="delete-a-queue"></a><span data-ttu-id="a45e3-169">Удаление очереди</span><span class="sxs-lookup"><span data-stu-id="a45e3-169">Delete a queue</span></span>
<span data-ttu-id="a45e3-170">toodelete все сообщения hello и очереди содержащиеся в нем, вызовите метод **удалить** метод hello объекта очереди.</span><span class="sxs-lookup"><span data-stu-id="a45e3-170">toodelete a queue and all hello messages contained in it, call the **Delete** method on hello queue object.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Delete hello queue.
queue.Delete();
```
    

## <a name="next-steps"></a><span data-ttu-id="a45e3-171">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a45e3-171">Next steps</span></span>
<span data-ttu-id="a45e3-172">Теперь, когда вы узнали основы hello хранилища очередей, выполните эти ссылки toolearn о более сложных задач хранилища.</span><span class="sxs-lookup"><span data-stu-id="a45e3-172">Now that you've learned hello basics of Queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="a45e3-173">Просмотрите hello очереди службы справочной документации для получения подробной информации о доступных API-интерфейсы:</span><span class="sxs-lookup"><span data-stu-id="a45e3-173">View hello Queue service reference documentation for complete details about available APIs:</span></span>
  * [<span data-ttu-id="a45e3-174">Справочник по клиентской библиотеке хранилища для .NET</span><span class="sxs-lookup"><span data-stu-id="a45e3-174">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
  * [<span data-ttu-id="a45e3-175">Справочник по REST API</span><span class="sxs-lookup"><span data-stu-id="a45e3-175">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="a45e3-176">Узнайте, как код hello toosimplify создавать toowork со службой хранилища Azure с помощью hello [SDK веб-заданий Azure](../../app-service-web/websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="a45e3-176">Learn how toosimplify hello code you write toowork with Azure Storage by using hello [Azure WebJobs SDK](../../app-service-web/websites-dotnet-webjobs-sdk.md).</span></span>
* <span data-ttu-id="a45e3-177">Просмотрите дополнительные toolearn функция руководства о дополнительных параметрах для хранения данных в Azure.</span><span class="sxs-lookup"><span data-stu-id="a45e3-177">View more feature guides toolearn about additional options for storing data in Azure.</span></span>
  * <span data-ttu-id="a45e3-178">[Начало работы с хранилищем таблиц Azure, с помощью .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md) toostore структурированные данные.</span><span class="sxs-lookup"><span data-stu-id="a45e3-178">[Get started with Azure Table storage using .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md) toostore structured data.</span></span>
  * <span data-ttu-id="a45e3-179">[Начало работы с хранилищем больших двоичных объектов Azure с помощью .NET](../blobs/storage-dotnet-how-to-use-blobs.md) toostore неструктурированных данных.</span><span class="sxs-lookup"><span data-stu-id="a45e3-179">[Get started with Azure Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) toostore unstructured data.</span></span>
  * <span data-ttu-id="a45e3-180">[Подключение tooSQL базы данных с помощью .NET (C#)](../../sql-database/sql-database-connect-query-dotnet-core.md) toostore реляционных данных.</span><span class="sxs-lookup"><span data-stu-id="a45e3-180">[Connect tooSQL Database by using .NET (C#)](../../sql-database/sql-database-connect-query-dotnet-core.md) toostore relational data.</span></span>

[Download and install hello Azure SDK for .NET]: /develop/net/
[.NET client library reference]: http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409
[Creating a Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[OData]: http://nuget.org/packages/Microsoft.Data.OData/5.0.2
[Edm]: http://nuget.org/packages/Microsoft.Data.Edm/5.0.2
[Spatial]: http://nuget.org/packages/System.Spatial/5.0.2
