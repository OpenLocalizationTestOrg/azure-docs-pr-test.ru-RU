---
title: "aaaGet работы с хранилищем очередей и Visual Studio подключенных служб (облачных служб) | Документы Microsoft"
description: "Как tooget запущена с помощью хранилища очередей Azure в проект облачной службы в Visual Studio после подключения tooa учетной записи хранилища с помощью Visual Studio подключенные службы"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: da587aac-5e64-4e9a-8405-44cc1924881d
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 8ba3d830cb83e3d75102b8a09363f1dc200ff1c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="79b26-103">Приступая к работе с подключенными службами хранилища очередей Azure и Visual Studio (проекты облачных служб)</span><span class="sxs-lookup"><span data-stu-id="79b26-103">Getting started with Azure Queue storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="79b26-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="79b26-104">Overview</span></span>
<span data-ttu-id="79b26-105">В этой статье описывается, как tooget запущена с помощью хранилища очередей Azure в Visual Studio после создания или ссылка на учетную запись хранилища Azure в проекте облачных служб с помощью Visual Studio hello **Добавление подключенных служб** диалоговое окно .</span><span class="sxs-lookup"><span data-stu-id="79b26-105">This article describes how tooget started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using hello  Visual Studio **Add Connected Services** dialog.</span></span>

<span data-ttu-id="79b26-106">Мы покажем, как toocreate очередь в коде.</span><span class="sxs-lookup"><span data-stu-id="79b26-106">We'll show you how toocreate a queue in code.</span></span> <span data-ttu-id="79b26-107">Мы также покажем, как tooperform basic очередь операций, таких как добавление, изменение, чтение и удаление сообщений очереди.</span><span class="sxs-lookup"><span data-stu-id="79b26-107">We'll also show you how tooperform basic queue operations, such as adding, modifying, reading and removing queue messages.</span></span> <span data-ttu-id="79b26-108">Hello примеры написаны на языке C# и использовать hello [клиентская библиотека хранилища Microsoft Azure для .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="79b26-108">hello samples are written in C# code and use hello [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="79b26-109">Hello **Добавление подключенных служб** операция устанавливает пакеты tooaccess hello соответствующие NuGet хранилища Azure в проекте и добавляет строку hello подключения для hello учетную запись хранилища, tooyour файлы конфигурации проекта.</span><span class="sxs-lookup"><span data-stu-id="79b26-109">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

* <span data-ttu-id="79b26-110">Дополнительные сведения о выполнении операций с очередями в коде см. в статье [Приступая к работе с хранилищем очередей Azure с помощью .NET](storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="79b26-110">See [Get started with Azure Queue storage using .NET](storage-dotnet-how-to-use-queues.md) for more information on manipulating queues in code.</span></span>
* <span data-ttu-id="79b26-111">Общие сведения о службе хранилища Azure см. в [документации по службе хранилища](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="79b26-111">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="79b26-112">Общие сведения об облачных службах Azure см. в [документации по облачным службам](https://azure.microsoft.com/documentation/services/cloud-services/).</span><span class="sxs-lookup"><span data-stu-id="79b26-112">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="79b26-113">Дополнительную информацию о программировании для ASP.NET см. в разделе [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="79b26-113">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

<span data-ttu-id="79b26-114">Хранилище Azure очереди — это служба для хранения большого количества сообщений, которые может осуществляться из любого места в Здравствуй, мир! через вызовы прошедшего проверку подлинности, протокол HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="79b26-114">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="79b26-115">Сообщение одной очереди может быть вверх too64 КБ и очередь может содержать миллионы сообщений вверх toohello предел общая емкость учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="79b26-115">A single queue message can be up too64 KB in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span>

## <a name="access-queues-in-code"></a><span data-ttu-id="79b26-116">Доступ к очередям в коде</span><span class="sxs-lookup"><span data-stu-id="79b26-116">Access queues in code</span></span>
<span data-ttu-id="79b26-117">tooaccess очереди в проектах Visual Studio облачные службы, необходимо следующее hello tooinclude элементы tooany C# исходный файл, доступ к хранилищу Azure очереди.</span><span class="sxs-lookup"><span data-stu-id="79b26-117">tooaccess queues in Visual Studio Cloud Services projects, you need tooinclude hello following items tooany C# source file that access Azure Queue storage.</span></span>

1. <span data-ttu-id="79b26-118">Убедитесь, что объявления пространств имен hello hello верхней части файла hello C# включить эти **с помощью** инструкции.</span><span class="sxs-lookup"><span data-stu-id="79b26-118">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
2. <span data-ttu-id="79b26-119">Получите объект **CloudStorageAccount** , представляющий данные учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="79b26-119">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="79b26-120">Hello используйте следующий код tooget hello хранения строки соединения и сведения об учетной записи хранилища из конфигурации службы Azure hello.</span><span class="sxs-lookup"><span data-stu-id="79b26-120">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. <span data-ttu-id="79b26-121">Получить **CloudQueueClient** объектов tooreference hello очереди в учетной записи.</span><span class="sxs-lookup"><span data-stu-id="79b26-121">Get a **CloudQueueClient** object tooreference hello queue objects in your storage account.</span></span>  
   
        // Create hello queue client.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. <span data-ttu-id="79b26-122">Получить **CloudQueue** объекта tooreference определенной очереди.</span><span class="sxs-lookup"><span data-stu-id="79b26-122">Get a **CloudQueue** object tooreference a specific queue.</span></span>
   
        // Get a reference tooa queue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

<span data-ttu-id="79b26-123">**Примечание:** используются hello над кодом перед кода hello из hello следующие примеры.</span><span class="sxs-lookup"><span data-stu-id="79b26-123">**NOTE:** Use all of hello above code in front of hello code in hello following samples.</span></span>

## <a name="create-a-queue-in-code"></a><span data-ttu-id="79b26-124">Создание очереди в коде</span><span class="sxs-lookup"><span data-stu-id="79b26-124">Create a queue in code</span></span>
<span data-ttu-id="79b26-125">очередь toocreate hello в коде, просто добавьте вызов слишком**CreateIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="79b26-125">toocreate hello queue in code, just add a call too**CreateIfNotExists**.</span></span>

    // Create hello CloudQueue if it does not exist
    messageQueue.CreateIfNotExists();

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="79b26-126">Добавить tooa очереди сообщений</span><span class="sxs-lookup"><span data-stu-id="79b26-126">Add a message tooa queue</span></span>
<span data-ttu-id="79b26-127">tooinsert сообщения в существующей очереди, создайте новый **CloudQueueMessage** объект, а затем вызов hello **AddMessage** метод.</span><span class="sxs-lookup"><span data-stu-id="79b26-127">tooinsert a message into an existing queue, create a new **CloudQueueMessage** object, then call hello **AddMessage** method.</span></span>

<span data-ttu-id="79b26-128">Для создания объекта **CloudQueueMessage** можно использовать либо строку (в формате UTF-8), либо массив типа byte.</span><span class="sxs-lookup"><span data-stu-id="79b26-128">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="79b26-129">Ниже приведен пример, который вставляет приветственное сообщение «Hello, World».</span><span class="sxs-lookup"><span data-stu-id="79b26-129">Here is an example which inserts hello message 'Hello, World'.</span></span>

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    messageQueue.AddMessage(message);

## <a name="read-a-message-in-a-queue"></a><span data-ttu-id="79b26-130">Чтение сообщения в очереди</span><span class="sxs-lookup"><span data-stu-id="79b26-130">Read a message in a queue</span></span>
<span data-ttu-id="79b26-131">Можно считывать сообщения hello в hello передней части очереди, не удаляя его из очереди hello, вызывающему Привет **PeekMessage** метод.</span><span class="sxs-lookup"><span data-stu-id="79b26-131">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **PeekMessage** method.</span></span>

    // Peek at hello next message
    CloudQueueMessage peekedMessage = messageQueue.PeekMessage();

## <a name="read-and-remove-a-message-in-a-queue"></a><span data-ttu-id="79b26-132">Чтение и удаление сообщения в очереди</span><span class="sxs-lookup"><span data-stu-id="79b26-132">Read and remove a message in a queue</span></span>
<span data-ttu-id="79b26-133">Ваш код может удалить сообщение из очереди в два этапа.</span><span class="sxs-lookup"><span data-stu-id="79b26-133">Your code can remove (de-queue) a message from a queue in two steps.</span></span>

1. <span data-ttu-id="79b26-134">Вызовите **GetMessage** tooget hello следующего сообщения в очереди.</span><span class="sxs-lookup"><span data-stu-id="79b26-134">Call **GetMessage** tooget hello next message in a queue.</span></span> <span data-ttu-id="79b26-135">Сообщение, возвращенное из **GetMessage** становится невидимой tooany другой код, чтение сообщений из этой очереди.</span><span class="sxs-lookup"><span data-stu-id="79b26-135">A message returned from **GetMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="79b26-136">По умолчанию это сообщение остается невидимым в течение 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="79b26-136">By default, this message stays invisible for 30 seconds.</span></span>
2. <span data-ttu-id="79b26-137">Удаление приветственное сообщение из очереди hello, вызов toofinish **DeleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="79b26-137">toofinish removing hello message from hello queue, call **DeleteMessage**.</span></span>

<span data-ttu-id="79b26-138">Это двухэтапный процесс удаления сообщения подтверждает, если tooprocess получит сообщение toohardware или ошибок программного обеспечения, другой экземпляр кода из-за сбоя программы hello одного сообщения и повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="79b26-138">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="79b26-139">Hello следующий код вызывает **DeleteMessage** сразу после обработки сообщения hello.</span><span class="sxs-lookup"><span data-stu-id="79b26-139">hello following code calls **DeleteMessage** right after hello message has been processed.</span></span>

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = messageQueue.GetMessage();

    // Process hello message in less than 30 seconds

    // Then delete hello message.
    await messageQueue.DeleteMessage(retrievedMessage);


## <a name="use-additional-options-tooprocess-and-remove-queue-messages"></a><span data-ttu-id="79b26-140">Используйте дополнительные параметры tooprocess и удаления очереди сообщений</span><span class="sxs-lookup"><span data-stu-id="79b26-140">Use additional options tooprocess and remove queue messages</span></span>
<span data-ttu-id="79b26-141">Способ извлечения сообщения из очереди можно настроить двумя способами.</span><span class="sxs-lookup"><span data-stu-id="79b26-141">There are two ways you can customize message retrieval from a queue.</span></span>

* <span data-ttu-id="79b26-142">Можно получить пакет сообщений (вверх too32).</span><span class="sxs-lookup"><span data-stu-id="79b26-142">You can get a batch of messages (up too32).</span></span>
* <span data-ttu-id="79b26-143">Можно задать более длинный или короткий невидимости тайм-аута, позволяя вашему коду больше или меньше toofully времени обработки каждого сообщения.</span><span class="sxs-lookup"><span data-stu-id="79b26-143">You can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="79b26-144">Hello следующий пример кода использует **GetMessages** метод tooget 20 сообщений в одном вызове.</span><span class="sxs-lookup"><span data-stu-id="79b26-144">hello following code example uses the **GetMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="79b26-145">Затем он обрабатывает каждое сообщение с помощью цикла **foreach** .</span><span class="sxs-lookup"><span data-stu-id="79b26-145">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="79b26-146">Он также устанавливает минут toofive hello невидимости время ожидания для каждого сообщения.</span><span class="sxs-lookup"><span data-stu-id="79b26-146">It also sets hello invisibility timeout toofive minutes for each message.</span></span> <span data-ttu-id="79b26-147">Обратите внимание, что hello 5 минут запускается для всех сообщений в hello же время, поэтому после 5 минут с момента вызова hello слишком**GetMessages**, все сообщения, которые не были удалены становятся видимыми.</span><span class="sxs-lookup"><span data-stu-id="79b26-147">Note that hello 5 minutes starts for all messages at hello same time, so after 5 minutes have passed since hello call too**GetMessages**, any messages which have not been deleted will become visible again.</span></span>

<span data-ttu-id="79b26-148">Ниже приведен пример:</span><span class="sxs-lookup"><span data-stu-id="79b26-148">Here's an example:</span></span>

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.

        // Then delete hello message after processing
        messageQueue.DeleteMessage(message);

    }

## <a name="get-hello-queue-length"></a><span data-ttu-id="79b26-149">Получает длину очереди hello</span><span class="sxs-lookup"><span data-stu-id="79b26-149">Get hello queue length</span></span>
<span data-ttu-id="79b26-150">Можно получить оценку hello количество сообщений в очереди.</span><span class="sxs-lookup"><span data-stu-id="79b26-150">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="79b26-151">**FetchAttributes** метод запрашивает hello службы очередей для получения атрибутов hello очереди, включая количество сообщений hello.</span><span class="sxs-lookup"><span data-stu-id="79b26-151">The **FetchAttributes** method asks hello Queue service to retrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="79b26-152">Hello **ApproximateMethodCount** свойство возвращает последнее значение hello извлекается с **FetchAttributes** метод без вызова службы очередей hello.</span><span class="sxs-lookup"><span data-stu-id="79b26-152">hello **ApproximateMethodCount** property returns hello last value retrieved by the **FetchAttributes** method, without calling hello Queue service.</span></span>

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-azure-queue-apis"></a><span data-ttu-id="79b26-153">Использовать hello Async-Await шаблон с общие интерфейсы API очереди Azure</span><span class="sxs-lookup"><span data-stu-id="79b26-153">Use hello Async-Await Pattern with common Azure Queue APIs</span></span>
<span data-ttu-id="79b26-154">Этот пример показывает, как шаблон toouse hello Async-Await с общие интерфейсы API очереди Azure.</span><span class="sxs-lookup"><span data-stu-id="79b26-154">This example shows how toouse hello Async-Await pattern with common Azure Queue APIs.</span></span> <span data-ttu-id="79b26-155">Образец Hello вызывает hello асинхронной версии каждого из заданного методы hello, это можно увидеть, hello **Async** исправления после каждого метода.</span><span class="sxs-lookup"><span data-stu-id="79b26-155">hello sample calls hello async version of each of hello given methods, this can be seen by hello **Async** post-fix of each method.</span></span> <span data-ttu-id="79b26-156">При асинхронного метода используется hello async-await шаблон приостанавливает локальное выполнение до завершения вызова hello.</span><span class="sxs-lookup"><span data-stu-id="79b26-156">When an async method is used hello async-await pattern suspends local execution until hello call completes.</span></span> <span data-ttu-id="79b26-157">Такое поведение позволяет hello текущий поток toodo другие типы работ, который позволяет избежать проблем с производительностью и повышает общую скорость реагирования приложения hello.</span><span class="sxs-lookup"><span data-stu-id="79b26-157">This behavior allows hello current thread toodo other work which helps avoid performance bottlenecks and improves hello overall responsiveness of your application.</span></span> <span data-ttu-id="79b26-158">Дополнительные сведения об использовании hello шаблон Async-Await в .NET см. в разделе [Async и Await (C# и Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="79b26-158">For more details on using hello Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

    // Create a message tooput in hello queue
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Add hello message asynchronously
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue hello message
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Delete hello message asynchronously
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");

## <a name="delete-a-queue"></a><span data-ttu-id="79b26-159">Удаление очереди</span><span class="sxs-lookup"><span data-stu-id="79b26-159">Delete a queue</span></span>
<span data-ttu-id="79b26-160">все сообщения hello и очереди, содержащиеся в нем, вызов hello toodelete **удалить** метод hello объекта очереди.</span><span class="sxs-lookup"><span data-stu-id="79b26-160">toodelete a queue and all hello messages contained in it, call hello **Delete** method on hello queue object.</span></span>

    // Delete hello queue.
    messageQueue.Delete();

## <a name="next-steps"></a><span data-ttu-id="79b26-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="79b26-161">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

