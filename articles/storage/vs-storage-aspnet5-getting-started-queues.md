---
title: "aaaGet работы с хранилищем очередей и Visual Studio подключенных служб (ASP.NET Core) | Документы Microsoft"
description: "Как tooget запущена с помощью хранилища очереди Azure в проекте ASP.NET Core в Visual Studio"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 04977069-5b2d-4cba-84ae-9fb2f5eb1006
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 75adb7163827ab17ad89707051ff0e48dbae9c3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-queue-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="17d8e-103">Приступая к работе с хранилищем очередей и подключенными службами Visual Studio (ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="17d8e-103">Get started with queue storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="17d8e-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="17d8e-104">Overview</span></span>
<span data-ttu-id="17d8e-105">В этой статье описывается, как tooget запущена с помощью хранилища очередей Azure в Visual Studio после создания или ссылка на учетную запись хранилища Azure в проекте ASP.NET Core с помощью Visual Studio hello **Добавление подключенных служб** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="17d8e-105">This article describes how tooget started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using hello Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="17d8e-106">Hello **Добавление подключенных служб** операция устанавливает пакеты tooaccess hello соответствующие NuGet хранилища Azure в проекте и добавляет строку hello подключения для hello учетную запись хранилища, tooyour файлы конфигурации проекта.</span><span class="sxs-lookup"><span data-stu-id="17d8e-106">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

<span data-ttu-id="17d8e-107">Хранилище очередей Azure — это служба для хранения большого числа сообщений, которые может осуществляться из любого места в Здравствуй, мир! через вызовы прошедшего проверку подлинности, протокол HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="17d8e-107">Azure queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="17d8e-108">Сообщение одной очереди может быть вверх too64 килобайт (КБ), размер и очередь может содержать миллионы сообщений вверх toohello предел общая емкость учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="17d8e-108">A single queue message can be up too64 kilobytes (KB) in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span>

<span data-ttu-id="17d8e-109">tooget работы, необходимо сначала toocreate очереди Azure в вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="17d8e-109">tooget started, you first need toocreate an Azure queue in your storage account.</span></span> <span data-ttu-id="17d8e-110">Мы покажем, как toocreate очередь в коде.</span><span class="sxs-lookup"><span data-stu-id="17d8e-110">We'll show you how toocreate a queue in code.</span></span> <span data-ttu-id="17d8e-111">Мы также покажем, как tooperform basic очередь операций, таких как добавление, изменение, чтение и удаление сообщений очереди.</span><span class="sxs-lookup"><span data-stu-id="17d8e-111">We'll also show you how tooperform basic queue operations, such as adding, modifying, reading, and removing queue messages.</span></span> <span data-ttu-id="17d8e-112">Hello примеры на языке C\# кода и использовать hello клиентская библиотека хранилища Azure для .NET.</span><span class="sxs-lookup"><span data-stu-id="17d8e-112">hello samples are written in C\# code and use hello Azure Storage Client Library for .NET.</span></span> <span data-ttu-id="17d8e-113">Дополнительные сведения см. на сайте [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="17d8e-113">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

<span data-ttu-id="17d8e-114">**Примечание:** некоторые интерфейсы API, которые выполняют вызовы tooAzure хранилища в ASP.NET Core hello являются асинхронными.</span><span class="sxs-lookup"><span data-stu-id="17d8e-114">**NOTE:** Some of hello APIs that perform calls tooAzure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="17d8e-115">Дополнительные сведения см. в статье [Asynchronous Programming with async and await (C#)](http://msdn.microsoft.com/library/hh191443.aspx) (Асинхронное программирование с использованием ключевых слов Async и Await (C#)).</span><span class="sxs-lookup"><span data-stu-id="17d8e-115">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="17d8e-116">Приведенный ниже код Hello предполагается, что используются асинхронные методы программирования.</span><span class="sxs-lookup"><span data-stu-id="17d8e-116">hello code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="17d8e-117">Дополнительные сведения о выполнении программных операций с очередями см. в статье [Приступая к работе с хранилищем очередей Azure с помощью .NET](storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="17d8e-117">See [Get started with Azure Queue storage using .NET](storage-dotnet-how-to-use-queues.md) for more information on programmatically manipulating queues.</span></span>
* <span data-ttu-id="17d8e-118">Общие сведения о службе хранилища Azure см. в [документации по службе хранилища](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="17d8e-118">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="17d8e-119">Общие сведения об облачных службах Azure см. в [документации по облачным службам](https://azure.microsoft.com/documentation/services/cloud-services/).</span><span class="sxs-lookup"><span data-stu-id="17d8e-119">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="17d8e-120">Дополнительную информацию о программировании для ASP.NET см. в разделе [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="17d8e-120">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-queues-in-code"></a><span data-ttu-id="17d8e-121">Доступ к очередям в коде</span><span class="sxs-lookup"><span data-stu-id="17d8e-121">Access queues in code</span></span>
<span data-ttu-id="17d8e-122">tooaccess очереди в проектах ASP.NET Core, требуются следующие hello tooinclude элементы tooany C# исходного файла, который получает доступ к хранилищу очереди Azure.</span><span class="sxs-lookup"><span data-stu-id="17d8e-122">tooaccess queues in ASP.NET Core projects, you need tooinclude hello following items tooany C# source file that accesses Azure queue storage.</span></span>

1. <span data-ttu-id="17d8e-123">Убедитесь, что объявления пространств имен hello hello верхней части файла hello C# включить эти **с помощью** инструкции.</span><span class="sxs-lookup"><span data-stu-id="17d8e-123">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="17d8e-124">Получите объект **CloudStorageAccount** , представляющий данные учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="17d8e-124">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="17d8e-125">Hello используйте следующий код tooget hello хранения строки соединения и сведения об учетной записи хранилища из конфигурации службы Azure hello.</span><span class="sxs-lookup"><span data-stu-id="17d8e-125">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. <span data-ttu-id="17d8e-126">Получить **CloudQueueClient** объектов tooreference hello очереди в учетной записи.</span><span class="sxs-lookup"><span data-stu-id="17d8e-126">Get a **CloudQueueClient** object tooreference hello queue objects in your storage account.</span></span>  
   
        // Create hello CloudQueueClient object for hello storage account.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. <span data-ttu-id="17d8e-127">Получить **CloudQueue** объекта tooreference определенной очереди.</span><span class="sxs-lookup"><span data-stu-id="17d8e-127">Get a **CloudQueue** object tooreference a specific queue.</span></span>
   
        // Get a reference toohello CloudQueue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

<span data-ttu-id="17d8e-128">**Примечание:** используются hello над кодом перед кода hello из hello следующие примеры.</span><span class="sxs-lookup"><span data-stu-id="17d8e-128">**NOTE:** Use all of hello above code in front of hello code in hello following samples.</span></span>

### <a name="create-a-queue-in-code"></a><span data-ttu-id="17d8e-129">Создание очереди в коде</span><span class="sxs-lookup"><span data-stu-id="17d8e-129">Create a queue in code</span></span>
<span data-ttu-id="17d8e-130">hello toocreate очереди Azure в коде, просто добавьте вызов слишком**CreateIfNotExistsAsync**.</span><span class="sxs-lookup"><span data-stu-id="17d8e-130">toocreate hello Azure queue in code, just add a call too**CreateIfNotExistsAsync**.</span></span>

    // Create hello CloudQueue if it does not exist.
    await messageQueue.CreateIfNotExistsAsync();

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="17d8e-131">Добавить tooa очереди сообщений</span><span class="sxs-lookup"><span data-stu-id="17d8e-131">Add a message tooa queue</span></span>
<span data-ttu-id="17d8e-132">tooinsert сообщения в существующей очереди, создайте новый **CloudQueueMessage** объект, а затем вызов hello **AddMessageAsync** метод.</span><span class="sxs-lookup"><span data-stu-id="17d8e-132">tooinsert a message into an existing queue, create a new **CloudQueueMessage** object, then call hello **AddMessageAsync** method.</span></span>

<span data-ttu-id="17d8e-133">Для создания объекта **CloudQueueMessage** можно использовать либо строку (в формате UTF-8), либо массив типа byte.</span><span class="sxs-lookup"><span data-stu-id="17d8e-133">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="17d8e-134">Ниже приведен пример, который вставляет приветственное сообщение «Hello, World».</span><span class="sxs-lookup"><span data-stu-id="17d8e-134">Here is an example which inserts hello message 'Hello, World'.</span></span>

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    await messageQueue.AddMessageAsync(message);

## <a name="read-a-message-in-a-queue"></a><span data-ttu-id="17d8e-135">Чтение сообщения в очереди</span><span class="sxs-lookup"><span data-stu-id="17d8e-135">Read a message in a queue</span></span>
<span data-ttu-id="17d8e-136">Можно считывать сообщения hello в hello передней части очереди, не удаляя его из очереди hello, вызывающему Привет **PeekMessageAsync** метод.</span><span class="sxs-lookup"><span data-stu-id="17d8e-136">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **PeekMessageAsync** method.</span></span>

    // Peek hello next message in hello queue. 
    CloudQueueMessage peekedMessage = await messageQueue.PeekMessageAsync();


## <a name="read-and-remove-a-message-in-a-queue"></a><span data-ttu-id="17d8e-137">Чтение и удаление сообщения в очереди</span><span class="sxs-lookup"><span data-stu-id="17d8e-137">Read and remove a message in a queue</span></span>
<span data-ttu-id="17d8e-138">Ваш код может удалить сообщение из очереди в два этапа.</span><span class="sxs-lookup"><span data-stu-id="17d8e-138">Your code can remove (dequeue) a message from a queue in two steps.</span></span>

1. <span data-ttu-id="17d8e-139">Вызовите **GetMessageAsync** tooget hello следующего сообщения в очереди.</span><span class="sxs-lookup"><span data-stu-id="17d8e-139">Call **GetMessageAsync** tooget hello next message in a queue.</span></span> <span data-ttu-id="17d8e-140">Сообщение, возвращенное из **GetMessageAsync** становится невидимой tooany другой код, чтение сообщений из этой очереди.</span><span class="sxs-lookup"><span data-stu-id="17d8e-140">A message returned from **GetMessageAsync** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="17d8e-141">По умолчанию это сообщение остается невидимым в течение 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="17d8e-141">By default, this message stays invisible for 30 seconds.</span></span>
2. <span data-ttu-id="17d8e-142">Удаление приветственное сообщение из очереди hello, вызов toofinish **DeleteMessageAsync**.</span><span class="sxs-lookup"><span data-stu-id="17d8e-142">toofinish removing hello message from hello queue, call **DeleteMessageAsync**.</span></span>

<span data-ttu-id="17d8e-143">Это двухэтапный процесс удаления сообщения подтверждает, если tooprocess получит сообщение toohardware или ошибок программного обеспечения, другой экземпляр кода из-за сбоя программы hello одного сообщения и повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="17d8e-143">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="17d8e-144">Hello следующий код вызывает **DeleteMessageAsync** сразу после обработки сообщения hello.</span><span class="sxs-lookup"><span data-stu-id="17d8e-144">hello following code calls **DeleteMessageAsync** right after hello message has been processed.</span></span>

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();

    // Process hello message in less than 30 seconds.

    // Then delete hello message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);

## <a name="leverage-additional-options-for-dequeuing-messages"></a><span data-ttu-id="17d8e-145">Дополнительные варианты удаления сообщений из очереди</span><span class="sxs-lookup"><span data-stu-id="17d8e-145">Leverage additional options for dequeuing messages</span></span>
<span data-ttu-id="17d8e-146">Способ извлечения сообщения из очереди можно настроить двумя способами.</span><span class="sxs-lookup"><span data-stu-id="17d8e-146">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="17d8e-147">Во-первых можно получить пакет сообщений (вверх too32).</span><span class="sxs-lookup"><span data-stu-id="17d8e-147">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="17d8e-148">Во-вторых можно задать более длинный или короткий невидимости тайм-аута, позволяя вашему коду больше или меньше toofully времени обработки каждого сообщения.</span><span class="sxs-lookup"><span data-stu-id="17d8e-148">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="17d8e-149">Hello следующий пример кода использует **GetMessages** метод tooget 20 сообщений в одном вызове.</span><span class="sxs-lookup"><span data-stu-id="17d8e-149">hello following code example uses the **GetMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="17d8e-150">Затем он обрабатывает каждое сообщение с помощью цикла **foreach** .</span><span class="sxs-lookup"><span data-stu-id="17d8e-150">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="17d8e-151">Он также устанавливает минут too5 hello невидимости время ожидания для каждого сообщения.</span><span class="sxs-lookup"><span data-stu-id="17d8e-151">It also sets hello invisibility timeout too5 minutes for each message.</span></span> <span data-ttu-id="17d8e-152">Обратите внимание, что начала hello 5 минут для всех сообщений в hello же времени, поэтому после 5 минут после вызова hello слишком**GetMessages**, все сообщения, которые не были удалены становятся видимыми.</span><span class="sxs-lookup"><span data-stu-id="17d8e-152">Note that hello 5 minutes start for all messages at hello same time, so after 5 minutes have passed after hello call too**GetMessages**, any messages which have not been deleted become visible again.</span></span>

    // Retrieve 20 messages at a time, keeping those messages invisible for 5 minutes, 
    //   delete each message after processing.

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.
        queue.DeleteMessage(message);
    }

## <a name="get-hello-queue-length"></a><span data-ttu-id="17d8e-153">Получает длину очереди hello</span><span class="sxs-lookup"><span data-stu-id="17d8e-153">Get hello queue length</span></span>
<span data-ttu-id="17d8e-154">Можно получить оценку hello количество сообщений в очереди.</span><span class="sxs-lookup"><span data-stu-id="17d8e-154">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="17d8e-155">**FetchAttributes** метод запрашивает hello службы очередей для получения атрибутов hello очереди, включая количество сообщений hello.</span><span class="sxs-lookup"><span data-stu-id="17d8e-155">The **FetchAttributes** method asks hello queue service to retrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="17d8e-156">Hello **ApproximateMethodCount** свойство возвращает последнее значение hello извлекается с **FetchAttributes** метод без вызова службы очередей hello.</span><span class="sxs-lookup"><span data-stu-id="17d8e-156">hello **ApproximateMethodCount** property returns hello last value retrieved by the **FetchAttributes** method, without calling hello queue service.</span></span>

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display hello number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-queue-apis"></a><span data-ttu-id="17d8e-157">Использование шаблона hello Async-Await с очередь общих API-интерфейсов</span><span class="sxs-lookup"><span data-stu-id="17d8e-157">Use hello Async-Await pattern with common queue APIs</span></span>
<span data-ttu-id="17d8e-158">В этом примере показано, как toouse hello Async-Await шаблоном очередь общих интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="17d8e-158">This example shows how toouse hello Async-Await pattern with common queue APIs.</span></span> <span data-ttu-id="17d8e-159">Hello образец вызовы hello асинхронной версии каждого hello, учитывая методы.</span><span class="sxs-lookup"><span data-stu-id="17d8e-159">hello sample calls hello async version of each of hello given methods.</span></span> <span data-ttu-id="17d8e-160">Это можно заметить исправлением hello Async после каждого метода.</span><span class="sxs-lookup"><span data-stu-id="17d8e-160">This can be seen by hello Async post-fix of each method.</span></span> <span data-ttu-id="17d8e-161">При использовании асинхронного метода hello шаблон Async-Await приостанавливает локальное выполнение до завершения вызова hello.</span><span class="sxs-lookup"><span data-stu-id="17d8e-161">When an async method is used, hello Async-Await pattern suspends local execution until hello call is completed.</span></span> <span data-ttu-id="17d8e-162">Такое поведение позволяет hello текущий поток toodo другие типы работ, который позволяет избежать проблем с производительностью и повышает общую скорость реагирования приложения hello.</span><span class="sxs-lookup"><span data-stu-id="17d8e-162">This behavior allows hello current thread toodo other work which helps avoid performance bottlenecks and improves hello overall responsiveness of your application.</span></span> <span data-ttu-id="17d8e-163">Дополнительные сведения об использовании hello шаблон Async-Await в .NET, см. в разделе [Async и Await (C# и Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="17d8e-163">For more details on using hello Async-Await pattern in .NET, see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

    // Create a message tooadd toohello queue.
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Async enqueue hello message.
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue hello message.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Async delete hello message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");
## <a name="delete-a-queue"></a><span data-ttu-id="17d8e-164">Удаление очереди</span><span class="sxs-lookup"><span data-stu-id="17d8e-164">Delete a queue</span></span>
<span data-ttu-id="17d8e-165">toodelete все сообщения hello и очереди содержащиеся в нем, вызовите метод **удалить** метод hello объекта очереди.</span><span class="sxs-lookup"><span data-stu-id="17d8e-165">toodelete a queue and all hello messages contained in it, call the **Delete** method on hello queue object.</span></span>

    // Delete hello queue.
    messageQueue.Delete();


## <a name="next-steps"></a><span data-ttu-id="17d8e-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="17d8e-166">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

