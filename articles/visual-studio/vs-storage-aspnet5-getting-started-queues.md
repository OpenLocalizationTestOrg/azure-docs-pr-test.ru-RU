---
title: "Приступая к работе с хранилищем очередей и подключенными службами Visual Studio (ASP.NET Core) | Документация Майкрософт"
description: "Начало работы с хранилищем очередей Azure в проекте ASP.NET Core в Visual Studio."
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 04977069-5b2d-4cba-84ae-9fb2f5eb1006
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 394344c0e126472b97c2e8f721c8c8d6514a17dc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-queue-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="e680a-103">Приступая к работе с хранилищем очередей и подключенными службами Visual Studio (ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="e680a-103">Get started with queue storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="e680a-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="e680a-104">Overview</span></span>
<span data-ttu-id="e680a-105">В этой статье описывается, как приступить к использованию хранилища очередей Azure в Visual Studio после создания учетной записи хранения Azure или указания ссылки на нее в проекте ASP.NET Core с помощью диалогового окна **Добавление подключенных служб** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e680a-105">This article describes how to get started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using the Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="e680a-106">Операция **Добавить подключенные службы** устанавливает соответствующие пакеты NuGet для доступа к службе хранилища Azure в вашем проекте и добавляет строку подключения для учетной записи хранения в файлы конфигурации проекта.</span><span class="sxs-lookup"><span data-stu-id="e680a-106">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span></span>

<span data-ttu-id="e680a-107">Хранилище очередей Azure — это служба хранения большого количества сообщений, к которым можно получить доступ практически из любой точки мира с помощью вызовов с проверкой подлинности по протоколу HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e680a-107">Azure queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="e680a-108">Одно сообщение очереди может быть размером до 64 КБ, а очередь может содержать миллионы сообщений, ограничиваемых общей емкостью учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="e680a-108">A single queue message can be up to 64 kilobytes (KB) in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span></span>

<span data-ttu-id="e680a-109">Чтобы начать работу, сначала необходимо создать очередь Azure в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="e680a-109">To get started, you first need to create an Azure queue in your storage account.</span></span> <span data-ttu-id="e680a-110">Мы покажем, как создать очередь в коде.</span><span class="sxs-lookup"><span data-stu-id="e680a-110">We'll show you how to create a queue in code.</span></span> <span data-ttu-id="e680a-111">Кроме того, вы узнаете, как выполнять базовые операции с очередями, например добавлять, изменять, считывать и удалять сообщения в очередях.</span><span class="sxs-lookup"><span data-stu-id="e680a-111">We'll also show you how to perform basic queue operations, such as adding, modifying, reading, and removing queue messages.</span></span> <span data-ttu-id="e680a-112">Примеры написаны на C\#, и в них используется библиотека клиента службы хранилища Azure для .NET.</span><span class="sxs-lookup"><span data-stu-id="e680a-112">The samples are written in C\# code and use the Azure Storage Client Library for .NET.</span></span> <span data-ttu-id="e680a-113">Дополнительные сведения см. на сайте [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="e680a-113">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

<span data-ttu-id="e680a-114">**Примечание**. Некоторые интерфейсы API, которые выполняют вызовы к службе хранилища Azure в ASP.NET Core, являются асинхронными.</span><span class="sxs-lookup"><span data-stu-id="e680a-114">**NOTE:** Some of the APIs that perform calls to Azure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="e680a-115">Дополнительные сведения см. в статье [Asynchronous Programming with async and await (C#)](http://msdn.microsoft.com/library/hh191443.aspx) (Асинхронное программирование с использованием ключевых слов Async и Await (C#)).</span><span class="sxs-lookup"><span data-stu-id="e680a-115">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="e680a-116">В следующем примере кода предполагается, что используются асинхронные методы программирования.</span><span class="sxs-lookup"><span data-stu-id="e680a-116">The code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="e680a-117">Дополнительные сведения о выполнении программных операций с очередями см. в статье [Приступая к работе с хранилищем очередей Azure с помощью .NET](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="e680a-117">See [Get started with Azure Queue storage using .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) for more information on programmatically manipulating queues.</span></span>
* <span data-ttu-id="e680a-118">Общие сведения о службе хранилища Azure см. в [документации по службе хранилища](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="e680a-118">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="e680a-119">Общие сведения об облачных службах Azure см. в [документации по облачным службам](https://azure.microsoft.com/documentation/services/cloud-services/).</span><span class="sxs-lookup"><span data-stu-id="e680a-119">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="e680a-120">Дополнительную информацию о программировании для ASP.NET см. в разделе [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="e680a-120">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-queues-in-code"></a><span data-ttu-id="e680a-121">Доступ к очередям в коде</span><span class="sxs-lookup"><span data-stu-id="e680a-121">Access queues in code</span></span>
<span data-ttu-id="e680a-122">Для доступа к очередям в проектах ASP.NET Core необходимо добавить следующие элементы во все файлы исходного кода C#, которые обращаются к хранилищу очередей Azure.</span><span class="sxs-lookup"><span data-stu-id="e680a-122">To access queues in ASP.NET Core projects, you need to include the following items to any C# source file that accesses Azure queue storage.</span></span>

1. <span data-ttu-id="e680a-123">Убедитесь, что объявления пространств имен в верхней части файла C# содержат указанные ниже выражения **using** .</span><span class="sxs-lookup"><span data-stu-id="e680a-123">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="e680a-124">Получите объект **CloudStorageAccount** , представляющий данные учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="e680a-124">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="e680a-125">Используйте следующий код, чтобы получить строку подключения и сведения об учетной записи хранения из конфигурации службы Azure.</span><span class="sxs-lookup"><span data-stu-id="e680a-125">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. <span data-ttu-id="e680a-126">Используйте объект **CloudQueueClient** для ссылки на объекты очереди в вашей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="e680a-126">Get a **CloudQueueClient** object to reference the queue objects in your storage account.</span></span>  
   
        // Create the CloudQueueClient object for the storage account.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. <span data-ttu-id="e680a-127">Получите объект **CloudQueue** для ссылки на определенную очередь.</span><span class="sxs-lookup"><span data-stu-id="e680a-127">Get a **CloudQueue** object to reference a specific queue.</span></span>
   
        // Get a reference to the CloudQueue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

<span data-ttu-id="e680a-128">**ПРИМЕЧАНИЕ.** Вставьте весь код, представленный выше, перед кодом в следующих примерах.</span><span class="sxs-lookup"><span data-stu-id="e680a-128">**NOTE:** Use all of the above code in front of the code in the following samples.</span></span>

### <a name="create-a-queue-in-code"></a><span data-ttu-id="e680a-129">Создание очереди в коде</span><span class="sxs-lookup"><span data-stu-id="e680a-129">Create a queue in code</span></span>
<span data-ttu-id="e680a-130">Чтобы создать очередь Azure в коде, просто добавьте вызов **CreateIfNotExistsAsync**.</span><span class="sxs-lookup"><span data-stu-id="e680a-130">To create the Azure queue in code, just add a call to **CreateIfNotExistsAsync**.</span></span>

    // Create the CloudQueue if it does not exist.
    await messageQueue.CreateIfNotExistsAsync();

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="e680a-131">Добавление сообщения в очередь</span><span class="sxs-lookup"><span data-stu-id="e680a-131">Add a message to a queue</span></span>
<span data-ttu-id="e680a-132">Чтобы вставить сообщение в существующую очередь, создайте новый объект **CloudQueueMessage**, а затем вызовите метод **AddMessageAsync**.</span><span class="sxs-lookup"><span data-stu-id="e680a-132">To insert a message into an existing queue, create a new **CloudQueueMessage** object, then call the **AddMessageAsync** method.</span></span>

<span data-ttu-id="e680a-133">Для создания объекта **CloudQueueMessage** можно использовать либо строку (в формате UTF-8), либо массив типа byte.</span><span class="sxs-lookup"><span data-stu-id="e680a-133">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="e680a-134">Ниже приведен пример, который вставляет сообщение "Hello, World".</span><span class="sxs-lookup"><span data-stu-id="e680a-134">Here is an example which inserts the message 'Hello, World'.</span></span>

    // Create a message and add it to the queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    await messageQueue.AddMessageAsync(message);

## <a name="read-a-message-in-a-queue"></a><span data-ttu-id="e680a-135">Чтение сообщения в очереди</span><span class="sxs-lookup"><span data-stu-id="e680a-135">Read a message in a queue</span></span>
<span data-ttu-id="e680a-136">Вы можете просмотреть сообщение в начале очереди, не удаляя его из очереди, вызвав метод **PeekMessageAsync** .</span><span class="sxs-lookup"><span data-stu-id="e680a-136">You can peek at the message in the front of a queue without removing it from the queue by calling the **PeekMessageAsync** method.</span></span>

    // Peek the next message in the queue. 
    CloudQueueMessage peekedMessage = await messageQueue.PeekMessageAsync();


## <a name="read-and-remove-a-message-in-a-queue"></a><span data-ttu-id="e680a-137">Чтение и удаление сообщения в очереди</span><span class="sxs-lookup"><span data-stu-id="e680a-137">Read and remove a message in a queue</span></span>
<span data-ttu-id="e680a-138">Ваш код может удалить сообщение из очереди в два этапа.</span><span class="sxs-lookup"><span data-stu-id="e680a-138">Your code can remove (dequeue) a message from a queue in two steps.</span></span>

1. <span data-ttu-id="e680a-139">Вызовите **GetMessageAsync** , чтобы получить следующее сообщение в очереди.</span><span class="sxs-lookup"><span data-stu-id="e680a-139">Call **GetMessageAsync** to get the next message in a queue.</span></span> <span data-ttu-id="e680a-140">Сообщение, возвращаемое методом **GetMessageAsync** , становится невидимым для любого другого кода, считывающего сообщения из этой очереди.</span><span class="sxs-lookup"><span data-stu-id="e680a-140">A message returned from **GetMessageAsync** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="e680a-141">По умолчанию это сообщение остается невидимым в течение 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="e680a-141">By default, this message stays invisible for 30 seconds.</span></span>
2. <span data-ttu-id="e680a-142">Чтобы завершить удаление сообщения из очереди, вызовите **DeleteMessageAsync**.</span><span class="sxs-lookup"><span data-stu-id="e680a-142">To finish removing the message from the queue, call **DeleteMessageAsync**.</span></span>

<span data-ttu-id="e680a-143">Этот двухэтапный процесс удаления сообщения позволяет удостовериться, что если коду не удастся обработать сообщение из-за сбоя оборудования или программного обеспечения, другой экземпляр кода сможет получить то же сообщение и повторить попытку.</span><span class="sxs-lookup"><span data-stu-id="e680a-143">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="e680a-144">Следующий код вызывает метод **DeleteMessageAsync** сразу после обработки сообщения.</span><span class="sxs-lookup"><span data-stu-id="e680a-144">The following code calls **DeleteMessageAsync** right after the message has been processed.</span></span>

    // Get the next message in the queue.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();

    // Process the message in less than 30 seconds.

    // Then delete the message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);

## <a name="leverage-additional-options-for-dequeuing-messages"></a><span data-ttu-id="e680a-145">Дополнительные варианты удаления сообщений из очереди</span><span class="sxs-lookup"><span data-stu-id="e680a-145">Leverage additional options for dequeuing messages</span></span>
<span data-ttu-id="e680a-146">Способ извлечения сообщения из очереди можно настроить двумя способами.</span><span class="sxs-lookup"><span data-stu-id="e680a-146">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="e680a-147">Во-первых, можно получить пакет сообщений (до 32 сообщений).</span><span class="sxs-lookup"><span data-stu-id="e680a-147">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="e680a-148">Во-вторых, можно задать более длительное или короткое время ожидания видимости, чтобы предоставить коду больше или меньше времени на полную обработку каждого сообщения.</span><span class="sxs-lookup"><span data-stu-id="e680a-148">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="e680a-149">В следующем примере кода метод **GetMessages** используется для получения 20 сообщений в одном вызове.</span><span class="sxs-lookup"><span data-stu-id="e680a-149">The following code example uses the **GetMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="e680a-150">Затем он обрабатывает каждое сообщение с помощью цикла **foreach** .</span><span class="sxs-lookup"><span data-stu-id="e680a-150">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="e680a-151">Он также задает время ожидания невидимости 5 минут для каждого сообщения.</span><span class="sxs-lookup"><span data-stu-id="e680a-151">It also sets the invisibility timeout to 5 minutes for each message.</span></span> <span data-ttu-id="e680a-152">Обратите внимание, что пятиминутный период начинается для всех сообщений одновременно, поэтому по прошествии 5 минут с момента вызова **GetMessages**все сообщения, которые не были удалены, снова становятся видимыми.</span><span class="sxs-lookup"><span data-stu-id="e680a-152">Note that the 5 minutes start for all messages at the same time, so after 5 minutes have passed after the call to **GetMessages**, any messages which have not been deleted become visible again.</span></span>

    // Retrieve 20 messages at a time, keeping those messages invisible for 5 minutes, 
    //   delete each message after processing.

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.
        queue.DeleteMessage(message);
    }

## <a name="get-the-queue-length"></a><span data-ttu-id="e680a-153">Получение длины очереди</span><span class="sxs-lookup"><span data-stu-id="e680a-153">Get the queue length</span></span>
<span data-ttu-id="e680a-154">Вы можете узнать приблизительное количество сообщений в очереди.</span><span class="sxs-lookup"><span data-stu-id="e680a-154">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="e680a-155">Метод **FetchAttributes** отправляет в службу очередей запрос на извлечение атрибутов очереди, включая количество сообщений.</span><span class="sxs-lookup"><span data-stu-id="e680a-155">The **FetchAttributes** method asks the queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="e680a-156">Свойство **ApproximateMethodCount** возвращает последнее значение, полученное с использованием метода **FetchAttributes**, без вызова службы очередей.</span><span class="sxs-lookup"><span data-stu-id="e680a-156">The **ApproximateMethodCount** property returns the last value retrieved by the **FetchAttributes** method, without calling the queue service.</span></span>

    // Fetch the queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve the cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display the number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-the-async-await-pattern-with-common-queue-apis"></a><span data-ttu-id="e680a-157">Использование схемы Async-Await со стандартными API очереди</span><span class="sxs-lookup"><span data-stu-id="e680a-157">Use the Async-Await pattern with common queue APIs</span></span>
<span data-ttu-id="e680a-158">В этом примере показано использование алгоритма Async-Await со стандартными API очередей.</span><span class="sxs-lookup"><span data-stu-id="e680a-158">This example shows how to use the Async-Await pattern with common queue APIs.</span></span> <span data-ttu-id="e680a-159">Пример вызывает асинхронную версию каждого заданного метода.</span><span class="sxs-lookup"><span data-stu-id="e680a-159">The sample calls the async version of each of the given methods.</span></span> <span data-ttu-id="e680a-160">Это можно увидеть после исправления каждого метода для асинхронного использования.</span><span class="sxs-lookup"><span data-stu-id="e680a-160">This can be seen by the Async post-fix of each method.</span></span> <span data-ttu-id="e680a-161">При использовании асинхронного метода схема Async-Await приостанавливает локальное выполнение процесса до завершения вызова.</span><span class="sxs-lookup"><span data-stu-id="e680a-161">When an async method is used, the Async-Await pattern suspends local execution until the call is completed.</span></span> <span data-ttu-id="e680a-162">Благодаря этому текущий поток может выполнять другие задачи, что позволяет избежать возникновения узких мест и повысить общую скорость реагирования приложения.</span><span class="sxs-lookup"><span data-stu-id="e680a-162">This behavior allows the current thread to do other work which helps avoid performance bottlenecks and improves the overall responsiveness of your application.</span></span> <span data-ttu-id="e680a-163">Дополнительные сведения об использовании алгоритма Async-Await в .NET см. в статье [Асинхронное программирование с использованием ключевых слов Async и Await (C# и Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).</span><span class="sxs-lookup"><span data-stu-id="e680a-163">For more details on using the Async-Await pattern in .NET, see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

    // Create a message to add to the queue.
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Async enqueue the message.
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue the message.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Async delete the message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");
## <a name="delete-a-queue"></a><span data-ttu-id="e680a-164">Удаление очереди</span><span class="sxs-lookup"><span data-stu-id="e680a-164">Delete a queue</span></span>
<span data-ttu-id="e680a-165">Чтобы удалить очередь и все сообщения в ней, вызовите метод **Delete** для объекта очереди.</span><span class="sxs-lookup"><span data-stu-id="e680a-165">To delete a queue and all the messages contained in it, call the **Delete** method on the queue object.</span></span>

    // Delete the queue.
    messageQueue.Delete();


## <a name="next-steps"></a><span data-ttu-id="e680a-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e680a-166">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

