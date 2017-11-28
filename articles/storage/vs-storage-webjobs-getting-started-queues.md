---
title: "Приступая к работе с хранилищем очередей и подключенными службами Visual Studio (проекты веб-заданий) | Документация Майкрософт"
description: "Как приступить к работе, используя хранилище очередей Azure в проекте веб-задания после подключения к учетной записи хранения с использованием подключенных служб Visual Studio."
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 5c3ef267-2a67-44e9-ab4a-1edd7015034f
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: abd4814c099620345e04833e14dafd38432064e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="05d2b-103">Приступая к работе с подключенными службами хранилища очередей Azure и Visual Studio (проекты веб-заданий)</span><span class="sxs-lookup"><span data-stu-id="05d2b-103">Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="05d2b-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="05d2b-104">Overview</span></span>
<span data-ttu-id="05d2b-105">В этой статье описывается, как начать использовать хранилище очередей Azure в проекте веб-заданий Azure в Visual Studio после создания учетной записи хранения Azure или указания ссылки на нее с помощью диалогового окна **Добавление подключенных служб** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="05d2b-105">This article describes how get started using Azure Queue storage in a Visual Studio Azure WebJob project after you have created or referenced an Azure storage account by using the Visual Studio  **Add Connected Services** dialog box.</span></span> <span data-ttu-id="05d2b-106">Когда вы добавляете учетную запись хранения в проект веб-задания с помощью диалогового окна **Добавление подключенных служб** в Visual Studio, устанавливается соответствующий пакет NuGet службы хранилища Azure. Также в проект добавляются соответствующие ссылки .NET, а в файле App.config обновляются строки подключения для учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="05d2b-106">When you add a storage account to a WebJob project by using the Visual Studio **Add Connected Services** dialog, the appropriate Azure Storage NuGet packages are installed, the appropriate .NET references are added to the project, and connection strings for the storage account are updated in the App.config file.</span></span>  

<span data-ttu-id="05d2b-107">Эта статья содержит примеры кода C#, в которых показано, как использовать пакет SDK для веб-заданий Azure версии 1.x со службой хранилища очередей Azure.</span><span class="sxs-lookup"><span data-stu-id="05d2b-107">This article provides C# code samples that show how to use the Azure WebJobs SDK version 1.x with the Azure Queue storage service.</span></span>

<span data-ttu-id="05d2b-108">Хранилище очередей Azure — это служба для хранения большого количества сообщений, к которым можно получить доступ практически из любой точки мира с помощью вызовов с проверкой подлинности по протоколам HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="05d2b-108">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="05d2b-109">Одно сообщение очереди может быть размером до 64 КБ, а очередь может содержать миллионы сообщений до общего ограничения емкости учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="05d2b-109">A single queue message can be up to 64 KB in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span></span> <span data-ttu-id="05d2b-110">Дополнительные сведения см. в разделе [Приступая к работе с хранилищем очередей Azure с помощью .NET](storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="05d2b-110">See [Get started with Azure Queue Storage using .NET](storage-dotnet-how-to-use-queues.md) for more information.</span></span> <span data-ttu-id="05d2b-111">Дополнительные сведения см. на сайте [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="05d2b-111">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="how-to-trigger-a-function-when-a-queue-message-is-received"></a><span data-ttu-id="05d2b-112">Вызов функции при получении сообщения очереди</span><span class="sxs-lookup"><span data-stu-id="05d2b-112">How to trigger a function when a queue message is received</span></span>
<span data-ttu-id="05d2b-113">Чтобы написать функцию, которую пакет SDK для веб-заданий будет вызывать при получении сообщения очереди, используйте атрибут **QueueTrigger** .</span><span class="sxs-lookup"><span data-stu-id="05d2b-113">To write a function that the WebJobs SDK calls when a queue message is received, use the **QueueTrigger** attribute.</span></span> <span data-ttu-id="05d2b-114">Конструктор атрибута принимает строковый параметр, который указывает имя очереди для опроса.</span><span class="sxs-lookup"><span data-stu-id="05d2b-114">The attribute constructor takes a string parameter that specifies the name of the queue to poll.</span></span> <span data-ttu-id="05d2b-115">Чтобы узнать, как динамически задать имя очереди, ознакомьтесь с разделом [Установка параметров конфигурации](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="05d2b-115">To see how to set the queue name dynamically, check out [How to set Configuration Options](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="05d2b-116">Строковые сообщения очереди</span><span class="sxs-lookup"><span data-stu-id="05d2b-116">String queue messages</span></span>
<span data-ttu-id="05d2b-117">В следующем примере очередь содержит строковое сообщение, поэтому атрибут **QueueTrigger** применяется к строковому параметру с именем **logMessage**, в котором находится содержимое сообщения очереди.</span><span class="sxs-lookup"><span data-stu-id="05d2b-117">In the following example, the queue contains a string message, so **QueueTrigger** is applied to a string parameter named **logMessage** which contains the content of the queue message.</span></span> <span data-ttu-id="05d2b-118">Функция [записывает сообщение журнала на панель мониторинга](#how-to-write-logs).</span><span class="sxs-lookup"><span data-stu-id="05d2b-118">The function [writes a log message to the Dashboard](#how-to-write-logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="05d2b-119">Помимо значения **string** возможными значениями этого параметра являются массив байтов, объект **CloudQueueMessage** или заданный вами объект POCO.</span><span class="sxs-lookup"><span data-stu-id="05d2b-119">Besides **string**, the parameter may be a byte array, a **CloudQueueMessage** object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="05d2b-120">Сообщения очереди [POCO](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)</span><span class="sxs-lookup"><span data-stu-id="05d2b-120">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="05d2b-121">В следующем примере сообщения очереди содержат JSON для объекта **BlobInformation**, который имеет свойство **BlobName**.</span><span class="sxs-lookup"><span data-stu-id="05d2b-121">In the following example, the queue message contains JSON for a **BlobInformation** object which includes a **BlobName** property.</span></span> <span data-ttu-id="05d2b-122">Пакет SDK автоматически выполняет десериализацию объекта.</span><span class="sxs-lookup"><span data-stu-id="05d2b-122">The SDK automatically deserializes the object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers to blob: " + blobInfo.BlobName);
        }

<span data-ttu-id="05d2b-123">Для сериализации и десериализации сообщений в пакете SDK используется [пакет NuGet Newtonsoft.Json](http://www.nuget.org/packages/Newtonsoft.Json) .</span><span class="sxs-lookup"><span data-stu-id="05d2b-123">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="05d2b-124">В случае создания сообщений очереди с помощью программы, которая не использует пакет SDK для заданий WebJob, чтобы создать сообщение очереди POCO, которое сможет проанализировать такой пакет, вы можете написать код по следующему образцу.</span><span class="sxs-lookup"><span data-stu-id="05d2b-124">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="05d2b-125">Асинхронные функции</span><span class="sxs-lookup"><span data-stu-id="05d2b-125">Async functions</span></span>
<span data-ttu-id="05d2b-126">Следующая асинхронная функция [записывает журнал на панель мониторинга](#how-to-write-logs).</span><span class="sxs-lookup"><span data-stu-id="05d2b-126">The following async function [writes a log to the Dashboard](#how-to-write-logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="05d2b-127">Асинхронные функции могут принимать [маркер отмены](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), как показано в следующем примере, который копирует большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="05d2b-127">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in the following example which copies a blob.</span></span> <span data-ttu-id="05d2b-128">(Описание заполнителя **queueTrigger** см. в статье [Большие двоичные объекты](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message).)</span><span class="sxs-lookup"><span data-stu-id="05d2b-128">(For an explanation of the **queueTrigger** placeholder, see the [Blobs](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

## <a name="types-the-queuetrigger-attribute-works-with"></a><span data-ttu-id="05d2b-129">Типы, с которыми используется атрибут QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="05d2b-129">Types the QueueTrigger attribute works with</span></span>
<span data-ttu-id="05d2b-130">Атрибут **QueueTrigger** можно использовать со следующими типами:</span><span class="sxs-lookup"><span data-stu-id="05d2b-130">You can use **QueueTrigger** with the following types:</span></span>

* <span data-ttu-id="05d2b-131">**string**</span><span class="sxs-lookup"><span data-stu-id="05d2b-131">**string**</span></span>
* <span data-ttu-id="05d2b-132">тип POCO, сериализованный как JSON;</span><span class="sxs-lookup"><span data-stu-id="05d2b-132">A POCO type serialized as JSON</span></span>
* <span data-ttu-id="05d2b-133">**byte[]**</span><span class="sxs-lookup"><span data-stu-id="05d2b-133">**byte[]**</span></span>
* <span data-ttu-id="05d2b-134">**CloudQueueMessage**</span><span class="sxs-lookup"><span data-stu-id="05d2b-134">**CloudQueueMessage**</span></span>

## <a name="polling-algorithm"></a><span data-ttu-id="05d2b-135">Алгоритм опроса</span><span class="sxs-lookup"><span data-stu-id="05d2b-135">Polling algorithm</span></span>
<span data-ttu-id="05d2b-136">В пакете SDK реализован алгоритм случайной экспоненциальной отсрочки, который позволяет уменьшить влияние опроса очереди ожидающих задач на затраты на транзакции хранилища.</span><span class="sxs-lookup"><span data-stu-id="05d2b-136">The SDK implements a random exponential back-off algorithm to reduce the effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="05d2b-137">При обнаружении сообщения пакет SDK ожидает в течение двух секунд и затем проверяет, не поступило ли еще одно сообщение; если сообщение не найдено, он ожидает около четырех секунд перед повторной попыткой.</span><span class="sxs-lookup"><span data-stu-id="05d2b-137">When a message is found, the SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="05d2b-138">После последующих неудачных попыток получения сообщения очереди время ожидания продолжает увеличиваться, пока не достигнет максимального времени ожидания, по умолчанию — одна минута.</span><span class="sxs-lookup"><span data-stu-id="05d2b-138">After subsequent failed attempts to get a queue message, the wait time continues to increase until it reaches the maximum wait time, which defaults to one minute.</span></span> <span data-ttu-id="05d2b-139">[Можно настроить максимальное время ожидания](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="05d2b-139">[The maximum wait time is configurable](#how-to-set-configuration-options).</span></span>

## <a name="multiple-instances"></a><span data-ttu-id="05d2b-140">Выполнение на нескольких экземплярах</span><span class="sxs-lookup"><span data-stu-id="05d2b-140">Multiple instances</span></span>
<span data-ttu-id="05d2b-141">Если ваше веб-приложение работает на нескольких экземплярах, веб-задания непрерывно выполняются на каждой машине, и каждая машина будет ожидать триггеры и пытаться запустить функции.</span><span class="sxs-lookup"><span data-stu-id="05d2b-141">If your web app runs on multiple instances, a continuous WebJobs runs on each machine, and each machine will wait for triggers and attempt to run functions.</span></span> <span data-ttu-id="05d2b-142">В некоторых сценариях это может привести к тому, что некоторые функции обработают часть данных дважды, поэтому функции должны быть идемпотентными (написанными так, чтобы их постоянный вызов с одинаковыми входными данными не создавал дублирующие результаты).</span><span class="sxs-lookup"><span data-stu-id="05d2b-142">In some scenarios this can lead to some functions processing the same data twice, so functions should be idempotent (written so that calling them repeatedly with the same input data doesn't produce duplicate results).</span></span>  

## <a name="parallel-execution"></a><span data-ttu-id="05d2b-143">Параллельное выполнение</span><span class="sxs-lookup"><span data-stu-id="05d2b-143">Parallel execution</span></span>
<span data-ttu-id="05d2b-144">Если имеется несколько функций, которые прослушивают различные очереди, при одновременном получении сообщений пакет SDK будет вызывать их параллельно.</span><span class="sxs-lookup"><span data-stu-id="05d2b-144">If you have multiple functions listening on different queues, the SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="05d2b-145">То же самое происходит при получении нескольких сообщений для одной очереди.</span><span class="sxs-lookup"><span data-stu-id="05d2b-145">The same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="05d2b-146">По умолчанию SDK одновременно получает пакет из 16 сообщений очереди и выполняет функцию, которая обрабатывает их параллельно.</span><span class="sxs-lookup"><span data-stu-id="05d2b-146">By default, the SDK gets a batch of 16 queue messages at a time and executes the function that processes them in parallel.</span></span> <span data-ttu-id="05d2b-147">[Можно настроить размер пакета](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="05d2b-147">[The batch size is configurable](#how-to-set-configuration-options).</span></span> <span data-ttu-id="05d2b-148">Когда число обрабатываемых сообщений достигает половины размера пакета, SDK запрашивает следующий пакет и начинает обработку содержащихся в нем сообщений.</span><span class="sxs-lookup"><span data-stu-id="05d2b-148">When the number being processed gets down to half of the batch size, the SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="05d2b-149">Поэтому максимальное количество сообщений, одновременно обрабатываемых каждой функцией, в полтора раза больше размера пакета.</span><span class="sxs-lookup"><span data-stu-id="05d2b-149">Therefore the maximum number of concurrent messages being processed per function is one and a half times the batch size.</span></span> <span data-ttu-id="05d2b-150">Это ограничение применяется отдельно к каждой функции с атрибутом **QueueTrigger** .</span><span class="sxs-lookup"><span data-stu-id="05d2b-150">This limit applies separately to each function that has a **QueueTrigger** attribute.</span></span> <span data-ttu-id="05d2b-151">Если вы не хотите, чтобы сообщения из одной очереди обрабатывались параллельно, установите размер пакета равный 1.</span><span class="sxs-lookup"><span data-stu-id="05d2b-151">If you don't want parallel execution for messages received on one queue, set the batch size to 1.</span></span>

## <a name="get-queue-or-queue-message-metadata"></a><span data-ttu-id="05d2b-152">Получение очереди или метаданных очереди сообщений</span><span class="sxs-lookup"><span data-stu-id="05d2b-152">Get queue or queue message metadata</span></span>
<span data-ttu-id="05d2b-153">Следующие свойства сообщений можно получить путем добавления параметров к сигнатуре метода:</span><span class="sxs-lookup"><span data-stu-id="05d2b-153">You can get the following message properties by adding parameters to the method signature:</span></span>

* <span data-ttu-id="05d2b-154">**DateTimeOffset** expirationTime</span><span class="sxs-lookup"><span data-stu-id="05d2b-154">**DateTimeOffset** expirationTime</span></span>
* <span data-ttu-id="05d2b-155">**DateTimeOffset** insertionTime</span><span class="sxs-lookup"><span data-stu-id="05d2b-155">**DateTimeOffset** insertionTime</span></span>
* <span data-ttu-id="05d2b-156">**DateTimeOffset** nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="05d2b-156">**DateTimeOffset** nextVisibleTime</span></span>
* <span data-ttu-id="05d2b-157">**string** queueTrigger (содержит текст сообщения)</span><span class="sxs-lookup"><span data-stu-id="05d2b-157">**string** queueTrigger (contains message text)</span></span>
* <span data-ttu-id="05d2b-158">**string** id</span><span class="sxs-lookup"><span data-stu-id="05d2b-158">**string** id</span></span>
* <span data-ttu-id="05d2b-159">**string** popReceipt</span><span class="sxs-lookup"><span data-stu-id="05d2b-159">**string** popReceipt</span></span>
* <span data-ttu-id="05d2b-160">**int** dequeueCount</span><span class="sxs-lookup"><span data-stu-id="05d2b-160">**int** dequeueCount</span></span>

<span data-ttu-id="05d2b-161">Если требуется работать непосредственно с API хранилища Azure, можно также добавить параметр **CloudStorageAccount** .</span><span class="sxs-lookup"><span data-stu-id="05d2b-161">If you want to work directly with the Azure storage API, you can also add a **CloudStorageAccount** parameter.</span></span>

<span data-ttu-id="05d2b-162">В следующем примере все эти метаданные записываются в журнал приложения INFO.</span><span class="sxs-lookup"><span data-stu-id="05d2b-162">The following example writes all of this metadata to an INFO application log.</span></span> <span data-ttu-id="05d2b-163">В примере содержимое сообщения очереди находится и в logMessage, и в queueTrigger.</span><span class="sxs-lookup"><span data-stu-id="05d2b-163">In the example, both logMessage and queueTrigger contain the content of the queue message.</span></span>

        public static void WriteLog([QueueTrigger("logqueue")] string logMessage,
            DateTimeOffset expirationTime,
            DateTimeOffset insertionTime,
            DateTimeOffset nextVisibleTime,
            string id,
            string popReceipt,
            int dequeueCount,
            string queueTrigger,
            CloudStorageAccount cloudStorageAccount,
            TextWriter logger)
        {
            logger.WriteLine(
                "logMessage={0}\n" +
            "expirationTime={1}\ninsertionTime={2}\n" +
                "nextVisibleTime={3}\n" +
                "id={4}\npopReceipt={5}\ndequeueCount={6}\n" +
                "queue endpoint={7} queueTrigger={8}",
                logMessage, expirationTime,
                insertionTime,
                nextVisibleTime, id,
                popReceipt, dequeueCount,
                cloudStorageAccount.QueueEndpoint,
                queueTrigger);
        }

<span data-ttu-id="05d2b-164">Ниже приведен образец журнала, созданный с помощью кода из примера.</span><span class="sxs-lookup"><span data-stu-id="05d2b-164">Here is a sample log written by the sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

## <a name="graceful-shutdown"></a><span data-ttu-id="05d2b-165">Корректное завершение работы</span><span class="sxs-lookup"><span data-stu-id="05d2b-165">Graceful shutdown</span></span>
<span data-ttu-id="05d2b-166">Функция, которая запускается в постоянном веб-задании, может принимать параметр **CancellationToken** , который позволяет операционной системе уведомлять ее о том, что выполнение веб-задания будет завершено.</span><span class="sxs-lookup"><span data-stu-id="05d2b-166">A function that runs in a continuous WebJob can accept a **CancellationToken** parameter which enables the operating system to notify the function when the WebJob is about to be terminated.</span></span> <span data-ttu-id="05d2b-167">Это уведомление можно использовать для предотвращения ситуации, когда выполнение функции завершается неожиданно, оставляя данные в несогласованном состоянии.</span><span class="sxs-lookup"><span data-stu-id="05d2b-167">You can use this notification to make sure the function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="05d2b-168">Следующий пример показывает, как проверить функцию на наличие предстоящего завершения веб-задания.</span><span class="sxs-lookup"><span data-stu-id="05d2b-168">The following example shows how to check for impending WebJob termination in a function.</span></span>

    public static void GracefulShutdownDemo(
                [QueueTrigger("inputqueue")] string inputText,
                TextWriter logger,
                CancellationToken token)
    {
        for (int i = 0; i < 100; i++)
        {
            if (token.IsCancellationRequested)
            {
                logger.WriteLine("Function was cancelled at iteration {0}", i);
                break;
            }
            Thread.Sleep(1000);
            logger.WriteLine("Normal processing for queue message={0}", inputText);
        }
    }

<span data-ttu-id="05d2b-169">**Примечание.** Панель мониторинга может неправильно показывать состояние и выходные данные завершенных функций.</span><span class="sxs-lookup"><span data-stu-id="05d2b-169">**Note:** The Dashboard might not correctly show the status and output of functions that have been shut down.</span></span>

<span data-ttu-id="05d2b-170">Дополнительную информацию см. в статье [Нормальное завершение работы веб-заданий](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span><span class="sxs-lookup"><span data-stu-id="05d2b-170">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <a name="how-to-create-a-queue-message-while-processing-a-queue-message"></a><span data-ttu-id="05d2b-171">Создание сообщения очереди во время обработки сообщения очереди</span><span class="sxs-lookup"><span data-stu-id="05d2b-171">How to create a queue message while processing a queue message</span></span>
<span data-ttu-id="05d2b-172">Чтобы написать функцию, которая создает новое сообщение очереди, используйте атрибут **Queue** .</span><span class="sxs-lookup"><span data-stu-id="05d2b-172">To write a function that creates a new queue message, use the **Queue** attribute.</span></span> <span data-ttu-id="05d2b-173">Как и в случае с **QueueTrigger**, имя очереди можно передать в виде строки или [задать динамически](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="05d2b-173">Like **QueueTrigger**, you pass in the queue name as a string or you can [set the queue name dynamically](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="05d2b-174">Строковые сообщения очереди</span><span class="sxs-lookup"><span data-stu-id="05d2b-174">String queue messages</span></span>
<span data-ttu-id="05d2b-175">Следующий пример неасинхронного кода создает новое сообщение очереди в очереди с именем «outputqueue» с тем же содержимым, что и сообщение очереди, поступившее в очередь с именем «inputqueue».</span><span class="sxs-lookup"><span data-stu-id="05d2b-175">The following non-async code sample creates a new queue message in the queue named "outputqueue" with the same content as the queue message received in the queue named "inputqueue".</span></span> <span data-ttu-id="05d2b-176">(Для асинхронных функций используйте параметр **IAsyncCollector;<T>** , следуя указаниям далее в этом разделе.)</span><span class="sxs-lookup"><span data-stu-id="05d2b-176">(For async functions use **IAsyncCollector<T>** as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="05d2b-177">Сообщения очереди [POCO](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)</span><span class="sxs-lookup"><span data-stu-id="05d2b-177">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="05d2b-178">Чтобы создать сообщение очереди, содержащее объект POCO, а не строку, передайте тип POCO в качестве выходного параметра конструктору атрибута **Queue** .</span><span class="sxs-lookup"><span data-stu-id="05d2b-178">To create a queue message that contains a POCO rather than a string, pass the POCO type as an output parameter to the **Queue** attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="05d2b-179">Пакет SDK автоматически выполняет сериализацию объекта в формат JSON.</span><span class="sxs-lookup"><span data-stu-id="05d2b-179">The SDK automatically serializes the object to JSON.</span></span> <span data-ttu-id="05d2b-180">Сообщение очереди создается всегда, даже если объект имеет значение null.</span><span class="sxs-lookup"><span data-stu-id="05d2b-180">A queue message is always created, even if the object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="05d2b-181">Создание нескольких сообщений или сообщений в асинхронных функциях</span><span class="sxs-lookup"><span data-stu-id="05d2b-181">Create multiple messages or in async functions</span></span>
<span data-ttu-id="05d2b-182">Чтобы создать несколько сообщений, установите для очереди вывода тип параметра **ICollector<T>** или **IAsyncCollector<T>**, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="05d2b-182">To create multiple messages, make the parameter type for the output queue **ICollector<T>** or **IAsyncCollector<T>**, as shown in the following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="05d2b-183">Каждое сообщение очереди создается сразу после вызова метода **Add** .</span><span class="sxs-lookup"><span data-stu-id="05d2b-183">Each queue message is created immediately when the **Add** method is called.</span></span>

### <a name="types-that-the-queue-attribute-works-with"></a><span data-ttu-id="05d2b-184">Типы, с которыми используется атрибут Queue</span><span class="sxs-lookup"><span data-stu-id="05d2b-184">Types that the Queue attribute works with</span></span>
<span data-ttu-id="05d2b-185">Атрибут **Queue** можно использовать со следующими типами параметров:</span><span class="sxs-lookup"><span data-stu-id="05d2b-185">You can use the **Queue** attribute on the following parameter types:</span></span>

* <span data-ttu-id="05d2b-186">**out string** (создает сообщение очереди, если по завершении вызова функции значение параметра не равно null);</span><span class="sxs-lookup"><span data-stu-id="05d2b-186">**out string** (creates queue message if parameter value is non-null when the function ends)</span></span>
* <span data-ttu-id="05d2b-187">**out byte[]** (работает как параметр **string**);</span><span class="sxs-lookup"><span data-stu-id="05d2b-187">**out byte[]** (works like **string**)</span></span>
* <span data-ttu-id="05d2b-188">**out CloudQueueMessage** (работает как параметр **string**);</span><span class="sxs-lookup"><span data-stu-id="05d2b-188">**out CloudQueueMessage** (works like **string**)</span></span>
* <span data-ttu-id="05d2b-189">**out POCO** (сериализуемый тип, создает сообщение с пустым объектом, если по завершении функции значение параметра — null);</span><span class="sxs-lookup"><span data-stu-id="05d2b-189">**out POCO** (a serializable type, creates a message with a null object if the paramter is null when the function ends)</span></span>
* <span data-ttu-id="05d2b-190">**ICollector;**</span><span class="sxs-lookup"><span data-stu-id="05d2b-190">**ICollector**</span></span>
* <span data-ttu-id="05d2b-191">**IAsyncCollector;**</span><span class="sxs-lookup"><span data-stu-id="05d2b-191">**IAsyncCollector**</span></span>
* <span data-ttu-id="05d2b-192">**CloudQueue** (позволяет создавать сообщения вручную непосредственно с помощью API службы хранилища Azure).</span><span class="sxs-lookup"><span data-stu-id="05d2b-192">**CloudQueue** (for creating messages manually using the Azure Storage API directly)</span></span>

### <a name="use-webjobs-sdk-attributes-in-the-body-of-a-function"></a><span data-ttu-id="05d2b-193">Использование атрибутов пакета SDK для заданий WebJob очереди в теле функции</span><span class="sxs-lookup"><span data-stu-id="05d2b-193">Use WebJobs SDK attributes in the body of a function</span></span>
<span data-ttu-id="05d2b-194">Если перед использованием атрибута пакета SDK для веб-заданий, например **Queue**, **Blob** или **Table**, необходимо выполнить какие-либо действия с функцией, то можно использовать интерфейс **IBinder**.</span><span class="sxs-lookup"><span data-stu-id="05d2b-194">If you need to do some work in your function before using a WebJobs SDK attribute such as **Queue**, **Blob**, or **Table**, you can use the **IBinder** interface.</span></span>

<span data-ttu-id="05d2b-195">В следующем примере в выходной очереди создается новое сообщение с тем же содержимым, что и в сообщении входной очереди.</span><span class="sxs-lookup"><span data-stu-id="05d2b-195">The following example takes an input queue message and creates a new message with the same content in an output queue.</span></span> <span data-ttu-id="05d2b-196">Имя очереди вывода определяется кодом в теле функции.</span><span class="sxs-lookup"><span data-stu-id="05d2b-196">The output queue name is set by code in the body of the function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="05d2b-197">Интерфейс **IBinder** можно также использовать при работе с атрибутами **Table** и **Blob**.</span><span class="sxs-lookup"><span data-stu-id="05d2b-197">The **IBinder** interface can also be used with the **Table** and **Blob** attributes.</span></span>

## <a name="how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message"></a><span data-ttu-id="05d2b-198">Чтение и запись больших двоичных объектов и таблиц во время обработки сообщения очереди</span><span class="sxs-lookup"><span data-stu-id="05d2b-198">How to read and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="05d2b-199">Атрибуты **Blob** и **Table** позволяют осуществлять чтение и запись больших двоичных объектов и таблиц.</span><span class="sxs-lookup"><span data-stu-id="05d2b-199">The **Blob** and **Table** attributes enable you to read and write blobs and tables.</span></span> <span data-ttu-id="05d2b-200">Примеры в этом разделе применимы к BLOB-объектам.</span><span class="sxs-lookup"><span data-stu-id="05d2b-200">The samples in this section apply to blobs.</span></span> <span data-ttu-id="05d2b-201">Примеры кода, в которых показаны способы запуска процессов при создании или обновлении больших двоичных объектов, см. в статье [Как использовать хранилище больших двоичных объектов Azure с пакетом SDK для WebJob](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), а примеры кода для чтения и записи таблиц см. в статье [Как использовать табличное хранилище Azure с пакетом SDK для WebJob](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="05d2b-201">For code samples that show how to trigger processes when blobs are created or updated, see [How to use Azure blob storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How to use Azure table storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="05d2b-202">Сообщения очереди строк, которые запускают операции с большими двоичными объектами</span><span class="sxs-lookup"><span data-stu-id="05d2b-202">String queue messages triggering blob operations</span></span>
<span data-ttu-id="05d2b-203">Для сообщения очереди, содержащего строку, **queueTrigger** является заполнителем, который можно использовать в параметре **blobPath** атрибута **Blob**, в котором находится содержимое сообщения.</span><span class="sxs-lookup"><span data-stu-id="05d2b-203">For a queue message that contains a string, **queueTrigger** is a placeholder you can use in the **Blob** attribute's **blobPath** parameter that contains the contents of the message.</span></span>

<span data-ttu-id="05d2b-204">Следующий пример использует объекты **Stream** для чтения и записи больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="05d2b-204">The following example uses **Stream** objects to read and write blobs.</span></span> <span data-ttu-id="05d2b-205">Сообщение очереди — это имя большого двоичного объекта, размещенного в контейнере textblobs.</span><span class="sxs-lookup"><span data-stu-id="05d2b-205">The queue message is the name of a blob located in the textblobs container.</span></span> <span data-ttu-id="05d2b-206">Копия большого двоичного объекта с приставкой «-new», добавленной к имени, создается в том же контейнере.</span><span class="sxs-lookup"><span data-stu-id="05d2b-206">A copy of the blob with "-new" appended to the name is created in the same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="05d2b-207">Конструктор атрибута **Blob** учитывает параметр **blobPath**, который указывает контейнер и имя большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="05d2b-207">The **Blob** attribute constructor takes a **blobPath** parameter that specifies the container and blob name.</span></span> <span data-ttu-id="05d2b-208">Дополнительную информацию об этом заполнителе см. в статье [Как использовать хранилище больших двоичных объектов Azure с пакетом SDK для WebJob](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="05d2b-208">For more information about this placeholder, see [How to use Azure blob storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span></span>

<span data-ttu-id="05d2b-209">Если атрибут декорирует объект **Stream**, другой параметр конструктора задает режим **FileAccess** как режим чтения, записи или чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="05d2b-209">When the attribute decorates a **Stream** object, another constructor parameter specifies the **FileAccess** mode as read, write, or read/write.</span></span>

<span data-ttu-id="05d2b-210">В следующем примере для удаления большого двоичного объекта используется объект **CloudBlockBlob** .</span><span class="sxs-lookup"><span data-stu-id="05d2b-210">The following example uses a **CloudBlockBlob** object to delete a blob.</span></span> <span data-ttu-id="05d2b-211">Очередь сообщений — это имя большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="05d2b-211">The queue message is the name of the blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="05d2b-212">Сообщения очереди [POCO](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)</span><span class="sxs-lookup"><span data-stu-id="05d2b-212">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="05d2b-213">Для объектов POCO, сохраненных в формате JSON в сообщении очереди, можно использовать заполнители, которые называют свойства объектов в параметре **blobPath** атрибута **Queue**.</span><span class="sxs-lookup"><span data-stu-id="05d2b-213">For a POCO stored as JSON in the queue message, you can use placeholders that name properties of the object in the **Queue** attribute's **blobPath** parameter.</span></span> <span data-ttu-id="05d2b-214">Можно также использовать имена свойства метаданных очереди в качестве заполнителей.</span><span class="sxs-lookup"><span data-stu-id="05d2b-214">You can also use queue metadata property names as placeholders.</span></span> <span data-ttu-id="05d2b-215">Ознакомьтесь с разделом [Получение метаданных очереди или сообщения в очереди](#get-queue-or-queue-message-metadata).</span><span class="sxs-lookup"><span data-stu-id="05d2b-215">See [Get queue or queue message metadata](#get-queue-or-queue-message-metadata).</span></span>

<span data-ttu-id="05d2b-216">В следующем примере выполняется копирование большого двоичного объекта в новый большой двоичный объект с другим расширением.</span><span class="sxs-lookup"><span data-stu-id="05d2b-216">The following example copies a blob to a new blob with a different extension.</span></span> <span data-ttu-id="05d2b-217">Сообщение очереди представляет собой объект **BlobInformation** со свойствами **BlobName** и **BlobNameWithoutExtension**.</span><span class="sxs-lookup"><span data-stu-id="05d2b-217">The queue message is a **BlobInformation** object that includes **BlobName** and **BlobNameWithoutExtension** properties.</span></span> <span data-ttu-id="05d2b-218">В качестве заполнителей в пути к большому двоичному объекту используются имена свойств для атрибутов **Blob** .</span><span class="sxs-lookup"><span data-stu-id="05d2b-218">The property names are used as placeholders in the blob path for the **Blob** attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="05d2b-219">Для сериализации и десериализации сообщений в пакете SDK используется [пакет NuGet Newtonsoft.Json](http://www.nuget.org/packages/Newtonsoft.Json) .</span><span class="sxs-lookup"><span data-stu-id="05d2b-219">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="05d2b-220">В случае создания сообщений очереди с помощью программы, которая не использует пакет SDK для заданий WebJob, чтобы создать сообщение очереди POCO, которое сможет проанализировать такой пакет, вы можете написать код по следующему образцу.</span><span class="sxs-lookup"><span data-stu-id="05d2b-220">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="05d2b-221">Если необходимо выполнить некоторую работу в функции перед привязкой большого двоичного объекта к объекту, можно использовать атрибут в основном тексте функции, как показано в разделе [Использование атрибутов пакета SDK для заданий WebJob очереди в теле функции](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span><span class="sxs-lookup"><span data-stu-id="05d2b-221">If you need to do some work in your function before binding a blob to an object, you can use the attribute in the body of the function, as shown in [Use WebJobs SDK attributes in the body of a function](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span></span>

### <a name="types-you-can-use-the-blob-attribute-with"></a><span data-ttu-id="05d2b-222">Типы, которые можно использовать с атрибутом Blob</span><span class="sxs-lookup"><span data-stu-id="05d2b-222">Types you can use the Blob attribute with</span></span>
<span data-ttu-id="05d2b-223">Атрибут **Blob** можно использовать со следующими типами:</span><span class="sxs-lookup"><span data-stu-id="05d2b-223">The **Blob** attribute can be used with the following types:</span></span>

* <span data-ttu-id="05d2b-224">**Stream** (чтение или запись, указанные с помощью параметра конструктора FileAccess);</span><span class="sxs-lookup"><span data-stu-id="05d2b-224">**Stream** (read or write, specified by using the FileAccess constructor parameter)</span></span>
* <span data-ttu-id="05d2b-225">**TextReader;**</span><span class="sxs-lookup"><span data-stu-id="05d2b-225">**TextReader**</span></span>
* <span data-ttu-id="05d2b-226">**TextWriter**</span><span class="sxs-lookup"><span data-stu-id="05d2b-226">**TextWriter**</span></span>
* <span data-ttu-id="05d2b-227">**string** (чтение);</span><span class="sxs-lookup"><span data-stu-id="05d2b-227">**string** (read)</span></span>
* <span data-ttu-id="05d2b-228">**out string** (запись; создает большой двоичный объект, только если для параметра строки не задано значение null при возврате функции);</span><span class="sxs-lookup"><span data-stu-id="05d2b-228">**out string** (write; creates a blob only if the string parameter is non-null when the function returns)</span></span>
* <span data-ttu-id="05d2b-229">POCO (чтение);</span><span class="sxs-lookup"><span data-stu-id="05d2b-229">POCO (read)</span></span>
* <span data-ttu-id="05d2b-230">out POCO (запись; всегда создает пустой большой двоичный объект, если при возврате функции значение параметра POCO — null);</span><span class="sxs-lookup"><span data-stu-id="05d2b-230">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when the function returns)</span></span>
* <span data-ttu-id="05d2b-231">**CloudBlobStream** (запись);</span><span class="sxs-lookup"><span data-stu-id="05d2b-231">**CloudBlobStream** (write)</span></span>
* <span data-ttu-id="05d2b-232">**ICloudBlob** (чтение или запись);</span><span class="sxs-lookup"><span data-stu-id="05d2b-232">**ICloudBlob** (read or write)</span></span>
* <span data-ttu-id="05d2b-233">**CloudBlockBlob** (чтение или запись);</span><span class="sxs-lookup"><span data-stu-id="05d2b-233">**CloudBlockBlob** (read or write)</span></span>
* <span data-ttu-id="05d2b-234">**CloudPageBlob** (чтение или запись).</span><span class="sxs-lookup"><span data-stu-id="05d2b-234">**CloudPageBlob** (read or write)</span></span>

## <a name="how-to-handle-poison-messages"></a><span data-ttu-id="05d2b-235">Способ обработки подозрительных сообщений</span><span class="sxs-lookup"><span data-stu-id="05d2b-235">How to handle poison messages</span></span>
<span data-ttu-id="05d2b-236">Сообщения, содержимое которых вызывает сбой функции, называются *подозрительными сообщениями*.</span><span class="sxs-lookup"><span data-stu-id="05d2b-236">Messages whose content causes a function to fail are called *poison messages*.</span></span> <span data-ttu-id="05d2b-237">При сбое функции сообщение очереди не удаляется и в конечном итоге забирается снова, вызывая повтор цикла.</span><span class="sxs-lookup"><span data-stu-id="05d2b-237">When the function fails, the queue message is not deleted and eventually is picked up again, causing the cycle to be repeated.</span></span> <span data-ttu-id="05d2b-238">Пакет SDK может автоматически прервать цикл после ограниченного числа итераций или это можно сделать вручную.</span><span class="sxs-lookup"><span data-stu-id="05d2b-238">The SDK can automatically interrupt the cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="05d2b-239">Автоматическая обработка сообщений</span><span class="sxs-lookup"><span data-stu-id="05d2b-239">Automatic poison message handling</span></span>
<span data-ttu-id="05d2b-240">Пакет SDK вызывает функцию обработки сообщения очереди до 5 раз.</span><span class="sxs-lookup"><span data-stu-id="05d2b-240">The SDK will call a function up to 5 times to process a queue message.</span></span> <span data-ttu-id="05d2b-241">В случае сбоя во время пятой попытки сообщение перемещается в очередь подозрительных сообщений.</span><span class="sxs-lookup"><span data-stu-id="05d2b-241">If the fifth try fails, the message is moved to a poison queue.</span></span> <span data-ttu-id="05d2b-242">Как настроить максимальное число повторных попыток описывается в разделе [Установка параметров конфигурации](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="05d2b-242">You can see how to configure the maximum number of retries in [How to set configuration options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="05d2b-243">Очередь подозрительных сообщений называется *{originalqueuename}*-poison.</span><span class="sxs-lookup"><span data-stu-id="05d2b-243">The poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="05d2b-244">Можно написать функции для обработки сообщений из очереди подозрительных сообщений путем внесения их в журнал или отправки уведомления о необходимости ручного вмешательства.</span><span class="sxs-lookup"><span data-stu-id="05d2b-244">You can write a function to process messages from the poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="05d2b-245">В следующем примере функция **CopyBlob** завершится ошибкой, если сообщение очереди содержит имя несуществующего большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="05d2b-245">In the following example the **CopyBlob** function will fail when a queue message contains the name of a blob that doesn't exist.</span></span> <span data-ttu-id="05d2b-246">В таком случае сообщение перемещается из очереди copyblobqueue в очередь copyblobqueue-poison.</span><span class="sxs-lookup"><span data-stu-id="05d2b-246">When that happens, the message is moved from the copyblobqueue queue to the copyblobqueue-poison queue.</span></span> <span data-ttu-id="05d2b-247">Затем функция **ProcessPoisonMessage** записывает подозрительное сообщение в журнал.</span><span class="sxs-lookup"><span data-stu-id="05d2b-247">The **ProcessPoisonMessage** then logs the poison message.</span></span>

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

        public static void ProcessPoisonMessage(
            [QueueTrigger("copyblobqueue-poison")] string blobName, TextWriter logger)
        {
            logger.WriteLine("Failed to copy blob, name=" + blobName);
        }

<span data-ttu-id="05d2b-248">На следующем рисунке показан вывод консоли при обработке этими функциями подозрительного сообщения.</span><span class="sxs-lookup"><span data-stu-id="05d2b-248">The following illustration shows console output from these functions when a poison message is processed.</span></span>

![Вывод консоли для обработки подозрительных сообщений](./media/vs-storage-webjobs-getting-started-queues/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="05d2b-250">Ручная обработка подозрительных сообщений</span><span class="sxs-lookup"><span data-stu-id="05d2b-250">Manual poison message handling</span></span>
<span data-ttu-id="05d2b-251">Чтобы узнать, сколько попыток обработки сообщения было совершено, добавьте в функцию параметр **int** с именем **dequeueCount**.</span><span class="sxs-lookup"><span data-stu-id="05d2b-251">You can get the number of times a message has been picked up for processing by adding an **int** parameter named **dequeueCount** to your function.</span></span> <span data-ttu-id="05d2b-252">Затем можно проверить счетчик вывода из очереди в коде функции и выполнить собственную обработку подозрительных сообщений, если это число превышает пороговое значение, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="05d2b-252">You can then check the dequeue count in function code and perform your own poison message handling when the number exceeds a threshold, as shown in the following example.</span></span>

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName, int dequeueCount,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput,
            TextWriter logger)
        {
            if (dequeueCount > 3)
            {
                logger.WriteLine("Failed to copy blob, name=" + blobName);
            }
            else
            {
            blobInput.CopyTo(blobOutput, 4096);
            }
        }

## <a name="how-to-set-configuration-options"></a><span data-ttu-id="05d2b-253">Установка параметров конфигурации</span><span class="sxs-lookup"><span data-stu-id="05d2b-253">How to set configuration options</span></span>
<span data-ttu-id="05d2b-254">Чтобы задать следующие параметры конфигурации, можно использовать тип **JobHostConfiguration** :</span><span class="sxs-lookup"><span data-stu-id="05d2b-254">You can use the **JobHostConfiguration** type to set the following configuration options:</span></span>

* <span data-ttu-id="05d2b-255">Установка строк подключения пакета SDK в коде.</span><span class="sxs-lookup"><span data-stu-id="05d2b-255">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="05d2b-256">Настройка таких параметров атрибута **QueueTrigger** , как максимальное значение счетчика вывода из очереди.</span><span class="sxs-lookup"><span data-stu-id="05d2b-256">Configure **QueueTrigger** settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="05d2b-257">Получение имен очередей из конфигурации</span><span class="sxs-lookup"><span data-stu-id="05d2b-257">Get queue names from configuration.</span></span>

### <a name="set-sdk-connection-strings-in-code"></a><span data-ttu-id="05d2b-258">Установка строк подключения пакета SDK в коде</span><span class="sxs-lookup"><span data-stu-id="05d2b-258">Set SDK connection strings in code</span></span>
<span data-ttu-id="05d2b-259">Установка строк подключения пакета SDK в коде позволяет использовать собственные имена строк подключения в файлах конфигурации или переменных среды, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="05d2b-259">Setting the SDK connection strings in code enables you to use your own connection string names in configuration files or environment variables, as shown in the following example.</span></span>

        static void Main(string[] args)
        {
            var _storageConn = ConfigurationManager
                .ConnectionStrings["MyStorageConnection"].ConnectionString;

            var _dashboardConn = ConfigurationManager
                .ConnectionStrings["MyDashboardConnection"].ConnectionString;

            var _serviceBusConn = ConfigurationManager
                .ConnectionStrings["MyServiceBusConnection"].ConnectionString;

            JobHostConfiguration config = new JobHostConfiguration();
            config.StorageConnectionString = _storageConn;
            config.DashboardConnectionString = _dashboardConn;
            config.ServiceBusConnectionString = _serviceBusConn;
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="configure-queuetrigger--settings"></a><span data-ttu-id="05d2b-260">Настройка параметров атрибута QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="05d2b-260">Configure QueueTrigger  settings</span></span>
<span data-ttu-id="05d2b-261">Можно настроить следующие параметры, которые применяются для обработки сообщений очереди:</span><span class="sxs-lookup"><span data-stu-id="05d2b-261">You can configure the following settings that apply to the queue message processing:</span></span>

* <span data-ttu-id="05d2b-262">Максимальное количество сообщений очереди, которые забираются одновременно для параллельной обработки (по умолчанию — 16).</span><span class="sxs-lookup"><span data-stu-id="05d2b-262">The maximum number of queue messages that are picked up simultaneously to be executed in parallel (default is 16).</span></span>
* <span data-ttu-id="05d2b-263">Максимальное число повторных попыток перед отправкой сообщения очереди в очередь подозрительных сообщений (по умолчанию — 5).</span><span class="sxs-lookup"><span data-stu-id="05d2b-263">The maximum number of retries before a queue message is sent to a poison queue (default is 5).</span></span>
* <span data-ttu-id="05d2b-264">Максимальное время ожидания перед повторным опросом, когда очередь пуста (по умолчанию — 1 минута).</span><span class="sxs-lookup"><span data-stu-id="05d2b-264">The maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="05d2b-265">В примере показано, как настроить эти параметры:</span><span class="sxs-lookup"><span data-stu-id="05d2b-265">The following example shows how to configure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="set-values-for-webjobs-sdk-constructor-parameters-in-code"></a><span data-ttu-id="05d2b-266">Установка значений параметров конструктора пакета SDK для заданий WebJob в коде</span><span class="sxs-lookup"><span data-stu-id="05d2b-266">Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="05d2b-267">Иногда требуется указать в коде имя очереди, имя большого двоичного объекта, контейнера или таблицы, а не жестко задавать их.</span><span class="sxs-lookup"><span data-stu-id="05d2b-267">Sometimes you want to specify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="05d2b-268">Например, в некоторых случаях в файле конфигурации или в переменной среды необходимо указывать имя очереди для **QueueTrigger** .</span><span class="sxs-lookup"><span data-stu-id="05d2b-268">For example, you might want to specify the queue name for **QueueTrigger** in a configuration file or environment variable.</span></span>

<span data-ttu-id="05d2b-269">Вы можете сделать это, передав объект **NameResolver** типу **JobHostConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="05d2b-269">You can do that by passing in a **NameResolver** object to the **JobHostConfiguration** type.</span></span> <span data-ttu-id="05d2b-270">В параметрах конструктора атрибута пакета SDK для веб-заданий нужно указать специальные заполнители со знаками процента (%) с обеих сторон, тогда код **NameResolver** будет указывать фактические значения, которые следует использовать вместо этих заполнителей.</span><span class="sxs-lookup"><span data-stu-id="05d2b-270">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your **NameResolver** code specifies the actual values to be used in place of those placeholders.</span></span>

<span data-ttu-id="05d2b-271">Например, предположим, что вы хотите использовать очередь с именем logqueuetest в тестовой среде и очередь с именем logqueueprod в производственной среде.</span><span class="sxs-lookup"><span data-stu-id="05d2b-271">For example, suppose you want to use a queue named logqueuetest in the test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="05d2b-272">Вместо фиксированного имени очереди требуется указать имя элемента в коллекции **appSettings** с фактическим именем очереди.</span><span class="sxs-lookup"><span data-stu-id="05d2b-272">Instead of a hard-coded queue name, you want to specify the name of an entry in the **appSettings** collection that would have the actual queue name.</span></span> <span data-ttu-id="05d2b-273">Если logqueue — значение ключа **appSettings** , функция может выглядеть как в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="05d2b-273">If the **appSettings** key is logqueue, your function could look like the following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="05d2b-274">Затем класс **NameResolver** может получить имя очереди из **appSettings**, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="05d2b-274">Your **NameResolver** class could then get the queue name from **appSettings** as shown in the following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="05d2b-275">Необходимо передать класс **NameResolver** в объект **JobHost**, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="05d2b-275">You pass the **NameResolver** class in to the **JobHost** object as shown in the following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="05d2b-276">**Примечание.** Имена очередей, таблиц и больших двоичных объектов не разрешаются при каждом вызове функции, а имена контейнеров больших двоичных объектов разрешаются только при запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="05d2b-276">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when the application starts.</span></span> <span data-ttu-id="05d2b-277">Во время выполнения задания нельзя изменить имя контейнера больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="05d2b-277">You can't change blob container name while the job is running.</span></span>

## <a name="how-to-trigger-a-function-manually"></a><span data-ttu-id="05d2b-278">Вызов функции вручную</span><span class="sxs-lookup"><span data-stu-id="05d2b-278">How to trigger a function manually</span></span>
<span data-ttu-id="05d2b-279">Чтобы вызвать функцию вручную, используйте метод **Call** или **CallAsync** объекта **JobHost** и атрибут функции **NoAutomaticTrigger**, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="05d2b-279">To trigger a function manually, use the **Call** or **CallAsync** method on the **JobHost** object and the **NoAutomaticTrigger** attribute on the function, as shown in the following example.</span></span>

        public class Program
        {
            static void Main(string[] args)
            {
                JobHost host = new JobHost();
                host.Call(typeof(Program).GetMethod("CreateQueueMessage"), new { value = "Hello world!" });
            }

            [NoAutomaticTrigger]
            public static void CreateQueueMessage(
                TextWriter logger,
                string value,
                [Queue("outputqueue")] out string message)
            {
                message = value;
                logger.WriteLine("Creating queue message: ", message);
            }
        }

## <a name="how-to-write-logs"></a><span data-ttu-id="05d2b-280">Запись журналов</span><span class="sxs-lookup"><span data-stu-id="05d2b-280">How to write logs</span></span>
<span data-ttu-id="05d2b-281">На панели мониторинга отображаются журналы: один на странице для заданий WebJob, а другой — на отдельной странице для определенного вызова задания WebJob.</span><span class="sxs-lookup"><span data-stu-id="05d2b-281">The Dashboard shows logs in two places: the page for the WebJob, and the page for a particular WebJob invocation.</span></span>

![Журналы на странице задания WebJob](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

![Журналы на странице вызова функций](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="05d2b-284">Выходные данные методов консоли, которые вызываются с помощью функции или метода **Main()** , отображаются на панели мониторинга на странице веб-задания, а не на странице для вызова определенного метода.</span><span class="sxs-lookup"><span data-stu-id="05d2b-284">Output from Console methods that you call in a function or in the **Main()** method appears in the Dashboard page for the WebJob, not in the page for a particular method invocation.</span></span> <span data-ttu-id="05d2b-285">Выходные данные объекта TextWriter, полученного из параметра в сигнатуре метода, отображаются на панели мониторинга на странице для вызова метода.</span><span class="sxs-lookup"><span data-stu-id="05d2b-285">Output from the TextWriter object that you get from a parameter in your method signature appears in the Dashboard page for a method invocation.</span></span>

<span data-ttu-id="05d2b-286">Выходные данные консоли нельзя связать с вызовом определенного метода, поскольку у консоли есть только один поток, хотя одновременно может выполняться сразу несколько функций.</span><span class="sxs-lookup"><span data-stu-id="05d2b-286">Console output can't be linked to a particular method invocation because the Console is single-threaded, while many job functions may be running at the same time.</span></span> <span data-ttu-id="05d2b-287">Поэтому пакет SDK обеспечивает вызов каждой функции с помощью уникального объекта модуля записи в журнал.</span><span class="sxs-lookup"><span data-stu-id="05d2b-287">That's why the  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="05d2b-288">Чтобы внести запись в [журналы трассировки приложений](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), используйте **Console.Out** (создает журналы с пометкой INFO) и **Console.Error** (создает журналы с пометкой ERROR).</span><span class="sxs-lookup"><span data-stu-id="05d2b-288">To write [application tracing logs](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use **Console.Out** (creates logs marked as INFO) and **Console.Error** (creates logs marked as ERROR).</span></span> <span data-ttu-id="05d2b-289">Кроме того, можно использовать [трассировку или TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), благодаря которым помимо информации и данных об ошибках можно получать подробные данные, предупреждения и оповещения о критическом уровне.</span><span class="sxs-lookup"><span data-stu-id="05d2b-289">An alternative is to use [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition to Info and Error.</span></span> <span data-ttu-id="05d2b-290">Журналы трассировки приложений отображаются в файлах журналов веб-приложения, таблицах Azure или больших двоичных объектах Azure, в зависимости от настроек вашего веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="05d2b-290">Application tracing logs appear in the web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="05d2b-291">Что касается всех выходных данных консоли, журналы последних 100 приложений отображаются на странице панели мониторинга для заданий WebJob, а не на странице для вызова функции.</span><span class="sxs-lookup"><span data-stu-id="05d2b-291">As is true of all Console output, the most recent 100 application logs also appear in the Dashboard page for the WebJob, not the page for a function invocation.</span></span>

<span data-ttu-id="05d2b-292">Выходные данные консоли отображаются на панели мониторинга, только если программа запущена в задании Azure WebJob, а не локально или в другой среде.</span><span class="sxs-lookup"><span data-stu-id="05d2b-292">Console output appears in the Dashboard only if the program is running in an Azure WebJob, not if the program is running locally or in some other environment.</span></span>

<span data-ttu-id="05d2b-293">Ведение журналов можно отключить с помощью элемента задание значения NULL для строки подключения панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="05d2b-293">You can disable logging by setting the Dashboard connection string to null.</span></span> <span data-ttu-id="05d2b-294">Дополнительную информацию см. в разделе [Установка параметров конфигурации](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="05d2b-294">For more information, see [How to set Configuration Options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="05d2b-295">В следующем примере показано несколько способов записи журналов:</span><span class="sxs-lookup"><span data-stu-id="05d2b-295">The following example shows several ways to write logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="05d2b-296">Выходные данные объекта **TextWriter** отобразятся на панели мониторинга пакета SDK для веб-заданий, если перейти на страницу вызова определенной функции и щелкнуть **Переключить выходные данные**.</span><span class="sxs-lookup"><span data-stu-id="05d2b-296">In the WebJobs SDK Dashboard, the output from the **TextWriter** object shows up when you go to the page for a particular function invocation and select **Toggle Output**:</span></span>

![Ссылка для вызова](./media/vs-storage-webjobs-getting-started-queues/dashboardinvocations.png)

![Журналы на странице вызова функций](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="05d2b-299">Последние 100 строк выходных данных консоли отобразятся на панели мониторинга пакета SDK веб-заданий, если перейти на страницу для веб-задания (не для вызова функции) и щелкнуть **Переключить выходные данные**.</span><span class="sxs-lookup"><span data-stu-id="05d2b-299">In the WebJobs SDK Dashboard, the most recent 100 lines of Console output show up when you go to the page for the WebJob (not for the function invocation) and select **Toggle Output**.</span></span>

![Переключить выходные данные](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

<span data-ttu-id="05d2b-301">Журналы приложений для непрерывных веб-заданий находятся по пути data/jobs/continuous/*{имя_веб-задания}*/job_log.txt в файловой системе веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="05d2b-301">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in the web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="05d2b-302">Вот как выглядят журналы приложений в большом двоичном объекте Azure: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span><span class="sxs-lookup"><span data-stu-id="05d2b-302">In an Azure blob the application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="05d2b-303">В таблице Azure журналы **Console.Out** и **Console.Error** выглядят следующим образом.</span><span class="sxs-lookup"><span data-stu-id="05d2b-303">And in an Azure table the **Console.Out** and **Console.Error** logs look like this:</span></span>

![Журнал Info в таблице](./media/vs-storage-webjobs-getting-started-queues/tableinfo.png)

![Журнал Error в таблице](./media/vs-storage-webjobs-getting-started-queues/tableerror.png)

## <a name="next-steps"></a><span data-ttu-id="05d2b-306">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="05d2b-306">Next steps</span></span>
<span data-ttu-id="05d2b-307">В этой статье предоставлены примеры кода обработки обычных сценариев для работы с очередями Azure.</span><span class="sxs-lookup"><span data-stu-id="05d2b-307">This article has provided code samples that show how to handle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="05d2b-308">Дополнительная информация об использовании веб-заданий Azure и пакета SDK для веб-заданий доступна в [ресурсах с документацией по веб-заданиям Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="05d2b-308">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

