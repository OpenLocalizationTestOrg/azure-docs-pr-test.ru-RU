---
title: "aaaGetting работы с хранилищем очередей и Visual Studio подключенных служб (для проектов веб-задания) | Документы Microsoft"
description: "Как tooget запущена с помощью хранилища очередей Azure в проекте веб-задания после подключения tooa учетной записи хранилища с помощью Visual Studio подключения службы."
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
ms.openlocfilehash: 720e96fda734c31e1b1d68d4f95aa9531a20a3f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="72145-103">Приступая к работе с подключенными службами хранилища очередей Azure и Visual Studio (проекты веб-заданий)</span><span class="sxs-lookup"><span data-stu-id="72145-103">Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="72145-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="72145-104">Overview</span></span>
<span data-ttu-id="72145-105">В этой статье описывается, как получить работы с использованием очередей Azure hello хранилища в проект веб-задания Azure Visual Studio после создания или ссылка на учетную запись хранения Azure с помощью Visual Studio **Добавление подключенных служб** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="72145-105">This article describes how get started using Azure Queue storage in a Visual Studio Azure WebJob project after you have created or referenced an Azure storage account by using hello Visual Studio  **Add Connected Services** dialog box.</span></span> <span data-ttu-id="72145-106">При добавлении проекта веб-задания tooa учетной записи хранилища с помощью Visual Studio hello **Добавление подключенных служб** диалогового окна, установлены соответствующие пакеты NuGet хранилища Azure hello, соответствующие ссылки .NET hello будут добавлены toohello в файле App.config hello обновляются проекта и строки подключения для учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="72145-106">When you add a storage account tooa WebJob project by using hello Visual Studio **Add Connected Services** dialog, hello appropriate Azure Storage NuGet packages are installed, hello appropriate .NET references are added toohello project, and connection strings for hello storage account are updated in hello App.config file.</span></span>  

<span data-ttu-id="72145-107">Эта статья содержит примеры кода C#, которые показывают, как toouse hello веб-заданий Azure SDK версии 1.x hello службы хранилища очередей Azure.</span><span class="sxs-lookup"><span data-stu-id="72145-107">This article provides C# code samples that show how toouse hello Azure WebJobs SDK version 1.x with hello Azure Queue storage service.</span></span>

<span data-ttu-id="72145-108">Хранилище Azure очереди — это служба для хранения большого количества сообщений, которые может осуществляться из любого места в Здравствуй, мир! через вызовы прошедшего проверку подлинности, протокол HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="72145-108">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="72145-109">Сообщение одной очереди может быть вверх too64 КБ и очередь может содержать миллионы сообщений вверх toohello предел общая емкость учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="72145-109">A single queue message can be up too64 KB in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span> <span data-ttu-id="72145-110">Дополнительные сведения см. в разделе [Приступая к работе с хранилищем очередей Azure с помощью .NET](storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="72145-110">See [Get started with Azure Queue Storage using .NET](storage-dotnet-how-to-use-queues.md) for more information.</span></span> <span data-ttu-id="72145-111">Дополнительные сведения см. на сайте [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="72145-111">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="how-tootrigger-a-function-when-a-queue-message-is-received"></a><span data-ttu-id="72145-112">Как tootrigger функции при получении сообщения в очереди</span><span class="sxs-lookup"><span data-stu-id="72145-112">How tootrigger a function when a queue message is received</span></span>
<span data-ttu-id="72145-113">вызывает функцию, которая hello SDK веб-заданий toowrite при получении сообщения в очереди, используйте hello **QueueTrigger** атрибута.</span><span class="sxs-lookup"><span data-stu-id="72145-113">toowrite a function that hello WebJobs SDK calls when a queue message is received, use hello **QueueTrigger** attribute.</span></span> <span data-ttu-id="72145-114">Конструктор атрибута Hello принимает строковый параметр, задающий имя hello toopoll очереди hello.</span><span class="sxs-lookup"><span data-stu-id="72145-114">hello attribute constructor takes a string parameter that specifies hello name of hello queue toopoll.</span></span> <span data-ttu-id="72145-115">toosee как tooset hello имя очереди динамически, извлечь [как tooset параметры конфигурации](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="72145-115">toosee how tooset hello queue name dynamically, check out [How tooset Configuration Options](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="72145-116">Строковые сообщения очереди</span><span class="sxs-lookup"><span data-stu-id="72145-116">String queue messages</span></span>
<span data-ttu-id="72145-117">В следующем примере hello, hello очередь содержит строковое сообщение, поэтому **QueueTrigger** будет применен tooa строковый параметр с именем **logMessage** , содержащее содержимое очереди приветственное сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="72145-117">In hello following example, hello queue contains a string message, so **QueueTrigger** is applied tooa string parameter named **logMessage** which contains hello content of hello queue message.</span></span> <span data-ttu-id="72145-118">Здравствуйте, функция [записывает toohello сообщение журнала мониторинга](#how-to-write-logs).</span><span class="sxs-lookup"><span data-stu-id="72145-118">hello function [writes a log message toohello Dashboard](#how-to-write-logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="72145-119">Помимо **строка**, hello параметр может быть массив байтов, **CloudQueueMessage** объекта или POCO, определяемому вами.</span><span class="sxs-lookup"><span data-stu-id="72145-119">Besides **string**, hello parameter may be a byte array, a **CloudQueueMessage** object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="72145-120">Сообщения очереди [POCO](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)</span><span class="sxs-lookup"><span data-stu-id="72145-120">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="72145-121">В следующем примере hello, сообщение hello очереди содержит JSON для **BlobInformation** объекта, который включает **BlobName** свойство.</span><span class="sxs-lookup"><span data-stu-id="72145-121">In hello following example, hello queue message contains JSON for a **BlobInformation** object which includes a **BlobName** property.</span></span> <span data-ttu-id="72145-122">пакет SDK для Hello автоматически десериализует hello объекта.</span><span class="sxs-lookup"><span data-stu-id="72145-122">hello SDK automatically deserializes hello object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

<span data-ttu-id="72145-123">Hello SDK использует hello [пакет Newtonsoft.Json NuGet](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize и десериализации сообщений.</span><span class="sxs-lookup"><span data-stu-id="72145-123">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="72145-124">При создании очереди сообщений в программе, которая не использует hello SDK веб-задания, можно написать код, как следующий пример toocreate POCO очереди сообщений hello приветствия, можно провести синтаксический анализ пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="72145-124">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="72145-125">Асинхронные функции</span><span class="sxs-lookup"><span data-stu-id="72145-125">Async functions</span></span>
<span data-ttu-id="72145-126">После асинхронного функции Hello [записывает журнал toohello мониторинга](#how-to-write-logs).</span><span class="sxs-lookup"><span data-stu-id="72145-126">hello following async function [writes a log toohello Dashboard](#how-to-write-logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="72145-127">Может потребоваться асинхронных функций [токен отмены](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), как показано в hello следующий пример, который копирует большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="72145-127">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in hello following example which copies a blob.</span></span> <span data-ttu-id="72145-128">(Объяснение hello **queueTrigger** заполнитель, в разделе hello [большие двоичные объекты](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) раздел.)</span><span class="sxs-lookup"><span data-stu-id="72145-128">(For an explanation of hello **queueTrigger** placeholder, see hello [Blobs](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

## <a name="types-hello-queuetrigger-attribute-works-with"></a><span data-ttu-id="72145-129">Атрибут QueueTrigger hello типы работает с</span><span class="sxs-lookup"><span data-stu-id="72145-129">Types hello QueueTrigger attribute works with</span></span>
<span data-ttu-id="72145-130">Можно использовать **QueueTrigger** с hello следующие типы:</span><span class="sxs-lookup"><span data-stu-id="72145-130">You can use **QueueTrigger** with hello following types:</span></span>

* <span data-ttu-id="72145-131">**string**</span><span class="sxs-lookup"><span data-stu-id="72145-131">**string**</span></span>
* <span data-ttu-id="72145-132">тип POCO, сериализованный как JSON;</span><span class="sxs-lookup"><span data-stu-id="72145-132">A POCO type serialized as JSON</span></span>
* <span data-ttu-id="72145-133">**byte[]**</span><span class="sxs-lookup"><span data-stu-id="72145-133">**byte[]**</span></span>
* <span data-ttu-id="72145-134">**CloudQueueMessage**</span><span class="sxs-lookup"><span data-stu-id="72145-134">**CloudQueueMessage**</span></span>

## <a name="polling-algorithm"></a><span data-ttu-id="72145-135">Алгоритм опроса</span><span class="sxs-lookup"><span data-stu-id="72145-135">Polling algorithm</span></span>
<span data-ttu-id="72145-136">Hello SDK реализует эффекта экспоненциальной отсрочки алгоритм случайных tooreduce hello простоя очереди опроса на транзакционные издержки хранения.</span><span class="sxs-lookup"><span data-stu-id="72145-136">hello SDK implements a random exponential back-off algorithm tooreduce hello effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="72145-137">При обнаружении сообщение hello SDK ожидает в течение двух секунд и затем проверяет наличие другого сообщения; Если сообщение не найдено он ожидает около четырех секунд перед повторной попыткой.</span><span class="sxs-lookup"><span data-stu-id="72145-137">When a message is found, hello SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="72145-138">После tooget последующих неудачных попытках сообщения в очереди, время ожидания hello продолжается tooincrease, пока не достигнет hello максимальное время ожидания, какие значения по умолчанию tooone минуты.</span><span class="sxs-lookup"><span data-stu-id="72145-138">After subsequent failed attempts tooget a queue message, hello wait time continues tooincrease until it reaches hello maximum wait time, which defaults tooone minute.</span></span> <span data-ttu-id="72145-139">[Hello максимальное время ожидания настраивается](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="72145-139">[hello maximum wait time is configurable](#how-to-set-configuration-options).</span></span>

## <a name="multiple-instances"></a><span data-ttu-id="72145-140">Выполнение на нескольких экземплярах</span><span class="sxs-lookup"><span data-stu-id="72145-140">Multiple instances</span></span>
<span data-ttu-id="72145-141">Если веб-приложение выполняется на нескольких экземплярах, непрерывные веб-задания выполняется на каждом компьютере, и каждой машины будет ожидать триггеры и повторите toorun функции.</span><span class="sxs-lookup"><span data-stu-id="72145-141">If your web app runs on multiple instances, a continuous WebJobs runs on each machine, and each machine will wait for triggers and attempt toorun functions.</span></span> <span data-ttu-id="72145-142">В некоторых случаях это может привести toosome функции обработки дважды, hello и те же данные, поэтому функции должны быть идемпотентными (написаны так, несколько раз вызывать их с приветствия же входных данных не может создать повторяющиеся результаты).</span><span class="sxs-lookup"><span data-stu-id="72145-142">In some scenarios this can lead toosome functions processing hello same data twice, so functions should be idempotent (written so that calling them repeatedly with hello same input data doesn't produce duplicate results).</span></span>  

## <a name="parallel-execution"></a><span data-ttu-id="72145-143">Параллельное выполнение</span><span class="sxs-lookup"><span data-stu-id="72145-143">Parallel execution</span></span>
<span data-ttu-id="72145-144">Если у вас есть несколько функций, которые прослушивают различные очереди, hello SDK вызывает их параллельно при получении сообщений одновременно.</span><span class="sxs-lookup"><span data-stu-id="72145-144">If you have multiple functions listening on different queues, hello SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="72145-145">Hello это верно и при получении нескольких сообщений для одной очереди.</span><span class="sxs-lookup"><span data-stu-id="72145-145">hello same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="72145-146">По умолчанию hello SDK получает пакет 16 очереди сообщений за раз и выполняет функции hello, обрабатывает их параллельно.</span><span class="sxs-lookup"><span data-stu-id="72145-146">By default, hello SDK gets a batch of 16 queue messages at a time and executes hello function that processes them in parallel.</span></span> <span data-ttu-id="72145-147">[размер пакета Hello настраивается](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="72145-147">[hello batch size is configurable](#how-to-set-configuration-options).</span></span> <span data-ttu-id="72145-148">При получении hello число обрабатываемых вниз toohalf размера пакета hello, hello SDK возвращает другой пакет и начинает обработку этих сообщений.</span><span class="sxs-lookup"><span data-stu-id="72145-148">When hello number being processed gets down toohalf of hello batch size, hello SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="72145-149">Поэтому hello максимальное количество одновременных сообщений, обрабатываемых каждой функции является размер пакета в полтора раза hello.</span><span class="sxs-lookup"><span data-stu-id="72145-149">Therefore hello maximum number of concurrent messages being processed per function is one and a half times hello batch size.</span></span> <span data-ttu-id="72145-150">Это ограничение применяется отдельно tooeach функции, которая имеет **QueueTrigger** атрибута.</span><span class="sxs-lookup"><span data-stu-id="72145-150">This limit applies separately tooeach function that has a **QueueTrigger** attribute.</span></span> <span data-ttu-id="72145-151">Если вы не хотите параллельного выполнения для сообщений, полученных на одну очередь, установите too1 размер пакета hello.</span><span class="sxs-lookup"><span data-stu-id="72145-151">If you don't want parallel execution for messages received on one queue, set hello batch size too1.</span></span>

## <a name="get-queue-or-queue-message-metadata"></a><span data-ttu-id="72145-152">Получение очереди или метаданных очереди сообщений</span><span class="sxs-lookup"><span data-stu-id="72145-152">Get queue or queue message metadata</span></span>
<span data-ttu-id="72145-153">Можно получить следующие свойства сообщения, добавив параметры сигнатуры метода toohello hello:</span><span class="sxs-lookup"><span data-stu-id="72145-153">You can get hello following message properties by adding parameters toohello method signature:</span></span>

* <span data-ttu-id="72145-154">**DateTimeOffset** expirationTime</span><span class="sxs-lookup"><span data-stu-id="72145-154">**DateTimeOffset** expirationTime</span></span>
* <span data-ttu-id="72145-155">**DateTimeOffset** insertionTime</span><span class="sxs-lookup"><span data-stu-id="72145-155">**DateTimeOffset** insertionTime</span></span>
* <span data-ttu-id="72145-156">**DateTimeOffset** nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="72145-156">**DateTimeOffset** nextVisibleTime</span></span>
* <span data-ttu-id="72145-157">**string** queueTrigger (содержит текст сообщения)</span><span class="sxs-lookup"><span data-stu-id="72145-157">**string** queueTrigger (contains message text)</span></span>
* <span data-ttu-id="72145-158">**string** id</span><span class="sxs-lookup"><span data-stu-id="72145-158">**string** id</span></span>
* <span data-ttu-id="72145-159">**string** popReceipt</span><span class="sxs-lookup"><span data-stu-id="72145-159">**string** popReceipt</span></span>
* <span data-ttu-id="72145-160">**int** dequeueCount</span><span class="sxs-lookup"><span data-stu-id="72145-160">**int** dequeueCount</span></span>

<span data-ttu-id="72145-161">Если требуется toowork непосредственно с hello хранилища Azure API, можно добавить **CloudStorageAccount** параметра.</span><span class="sxs-lookup"><span data-stu-id="72145-161">If you want toowork directly with hello Azure storage API, you can also add a **CloudStorageAccount** parameter.</span></span>

<span data-ttu-id="72145-162">Hello следующий пример записывает все журнал этого приложения tooan метаданных.</span><span class="sxs-lookup"><span data-stu-id="72145-162">hello following example writes all of this metadata tooan INFO application log.</span></span> <span data-ttu-id="72145-163">В примере hello logMessage и queueTrigger содержимым hello hello очереди сообщения.</span><span class="sxs-lookup"><span data-stu-id="72145-163">In hello example, both logMessage and queueTrigger contain hello content of hello queue message.</span></span>

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

<span data-ttu-id="72145-164">Ниже приведен пример журнала записываются в примере кода hello.</span><span class="sxs-lookup"><span data-stu-id="72145-164">Here is a sample log written by hello sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

## <a name="graceful-shutdown"></a><span data-ttu-id="72145-165">Корректное завершение работы</span><span class="sxs-lookup"><span data-stu-id="72145-165">Graceful shutdown</span></span>
<span data-ttu-id="72145-166">Функция, которая выполняется в непрерывных веб-задания может принимать **CancellationToken** параметр, который позволяет функции hello операционной системы toonotify hello при hello веб-задания — о toobe завершен.</span><span class="sxs-lookup"><span data-stu-id="72145-166">A function that runs in a continuous WebJob can accept a **CancellationToken** parameter which enables hello operating system toonotify hello function when hello WebJob is about toobe terminated.</span></span> <span data-ttu-id="72145-167">Можно использовать toomake это уведомление о том, что функции hello не привести к непредвиденному завершению способом, который оставляет данных в несогласованном состоянии.</span><span class="sxs-lookup"><span data-stu-id="72145-167">You can use this notification toomake sure hello function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="72145-168">Следующий пример показывает как Hello toocheck увольнения предстоящем веб-задания в функции.</span><span class="sxs-lookup"><span data-stu-id="72145-168">hello following example shows how toocheck for impending WebJob termination in a function.</span></span>

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

<span data-ttu-id="72145-169">**Примечание:** hello панели мониторинга может показывать правильно состояние hello и выходные данные функции, которые была завершена.</span><span class="sxs-lookup"><span data-stu-id="72145-169">**Note:** hello Dashboard might not correctly show hello status and output of functions that have been shut down.</span></span>

<span data-ttu-id="72145-170">Дополнительную информацию см. в статье [Нормальное завершение работы веб-заданий](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span><span class="sxs-lookup"><span data-stu-id="72145-170">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <a name="how-toocreate-a-queue-message-while-processing-a-queue-message"></a><span data-ttu-id="72145-171">Как toocreate очереди сообщений во время обработки сообщения в очереди</span><span class="sxs-lookup"><span data-stu-id="72145-171">How toocreate a queue message while processing a queue message</span></span>
<span data-ttu-id="72145-172">функция, которая создает новое сообщение очереди, используйте hello toowrite **очереди** атрибута.</span><span class="sxs-lookup"><span data-stu-id="72145-172">toowrite a function that creates a new queue message, use hello **Queue** attribute.</span></span> <span data-ttu-id="72145-173">Как **QueueTrigger**, передав имя очереди hello в виде строки, или вы можете [динамически задать имя очереди hello](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="72145-173">Like **QueueTrigger**, you pass in hello queue name as a string or you can [set hello queue name dynamically](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="72145-174">Строковые сообщения очереди</span><span class="sxs-lookup"><span data-stu-id="72145-174">String queue messages</span></span>
<span data-ttu-id="72145-175">Следующий образец кода синхронные Hello создает новое сообщение очереди в очередь hello, с именем «outputqueue» с таким же содержимое, так как очередь приветственное сообщение получено в hello очереди с именем «inputqueue» hello.</span><span class="sxs-lookup"><span data-stu-id="72145-175">hello following non-async code sample creates a new queue message in hello queue named "outputqueue" with hello same content as hello queue message received in hello queue named "inputqueue".</span></span> <span data-ttu-id="72145-176">(Для асинхронных функций используйте параметр **IAsyncCollector;<T>** , следуя указаниям далее в этом разделе.)</span><span class="sxs-lookup"><span data-stu-id="72145-176">(For async functions use **IAsyncCollector<T>** as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="72145-177">Сообщения очереди [POCO](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)</span><span class="sxs-lookup"><span data-stu-id="72145-177">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="72145-178">toocreate очереди сообщение, содержащее POCO, а не строкой, pass hello POCO тип в качестве выходного параметра toohello **очереди** конструктор атрибута.</span><span class="sxs-lookup"><span data-stu-id="72145-178">toocreate a queue message that contains a POCO rather than a string, pass hello POCO type as an output parameter toohello **Queue** attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="72145-179">пакет SDK для Hello автоматически сериализует tooJSON hello объекта.</span><span class="sxs-lookup"><span data-stu-id="72145-179">hello SDK automatically serializes hello object tooJSON.</span></span> <span data-ttu-id="72145-180">Очередь сообщений создается всегда, даже если hello объекта имеет значение null.</span><span class="sxs-lookup"><span data-stu-id="72145-180">A queue message is always created, even if hello object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="72145-181">Создание нескольких сообщений или сообщений в асинхронных функциях</span><span class="sxs-lookup"><span data-stu-id="72145-181">Create multiple messages or in async functions</span></span>
<span data-ttu-id="72145-182">toocreate несколько сообщений сделать hello тип параметра для очереди вывода hello **ICollector<T>**  или **IAsyncCollector<T>**, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="72145-182">toocreate multiple messages, make hello parameter type for hello output queue **ICollector<T>** or **IAsyncCollector<T>**, as shown in hello following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="72145-183">Каждое сообщение очереди создается сразу после hello **добавить** вызывается метод.</span><span class="sxs-lookup"><span data-stu-id="72145-183">Each queue message is created immediately when hello **Add** method is called.</span></span>

### <a name="types-that-hello-queue-attribute-works-with"></a><span data-ttu-id="72145-184">Типы атрибута очереди hello работает с</span><span class="sxs-lookup"><span data-stu-id="72145-184">Types that hello Queue attribute works with</span></span>
<span data-ttu-id="72145-185">Можно использовать hello **очереди** атрибутов на следующие типы параметра hello:</span><span class="sxs-lookup"><span data-stu-id="72145-185">You can use hello **Queue** attribute on hello following parameter types:</span></span>

* <span data-ttu-id="72145-186">**строки** (создает сообщения в очереди, если значение параметра не равно null, при завершении функции hello)</span><span class="sxs-lookup"><span data-stu-id="72145-186">**out string** (creates queue message if parameter value is non-null when hello function ends)</span></span>
* <span data-ttu-id="72145-187">**out byte[]** (работает как параметр **string**);</span><span class="sxs-lookup"><span data-stu-id="72145-187">**out byte[]** (works like **string**)</span></span>
* <span data-ttu-id="72145-188">**out CloudQueueMessage** (работает как параметр **string**);</span><span class="sxs-lookup"><span data-stu-id="72145-188">**out CloudQueueMessage** (works like **string**)</span></span>
* <span data-ttu-id="72145-189">**out POCO** (сериализуемый тип, создает сообщение с пустым объектом Если hello имеет значение null, при завершении функции hello)</span><span class="sxs-lookup"><span data-stu-id="72145-189">**out POCO** (a serializable type, creates a message with a null object if hello paramter is null when hello function ends)</span></span>
* <span data-ttu-id="72145-190">**ICollector;**</span><span class="sxs-lookup"><span data-stu-id="72145-190">**ICollector**</span></span>
* <span data-ttu-id="72145-191">**IAsyncCollector;**</span><span class="sxs-lookup"><span data-stu-id="72145-191">**IAsyncCollector**</span></span>
* <span data-ttu-id="72145-192">**CloudQueue** (для создания сообщений вручную с помощью hello API хранилища Azure непосредственно)</span><span class="sxs-lookup"><span data-stu-id="72145-192">**CloudQueue** (for creating messages manually using hello Azure Storage API directly)</span></span>

### <a name="use-webjobs-sdk-attributes-in-hello-body-of-a-function"></a><span data-ttu-id="72145-193">Использование пакета SDK веб-задания атрибутов в теле функции hello</span><span class="sxs-lookup"><span data-stu-id="72145-193">Use WebJobs SDK attributes in hello body of a function</span></span>
<span data-ttu-id="72145-194">Если вам требуется toodo некоторые работать в функции перед использованием атрибут SDK веб-заданий, таких как **очереди**, **большого двоичного объекта**, или **таблицы**, можно использовать hello **IBinder** интерфейса.</span><span class="sxs-lookup"><span data-stu-id="72145-194">If you need toodo some work in your function before using a WebJobs SDK attribute such as **Queue**, **Blob**, or **Table**, you can use hello **IBinder** interface.</span></span>

<span data-ttu-id="72145-195">Следующий пример Hello принимает сообщение входной очереди и создает новое сообщение с hello же содержимого, в очереди вывода.</span><span class="sxs-lookup"><span data-stu-id="72145-195">hello following example takes an input queue message and creates a new message with hello same content in an output queue.</span></span> <span data-ttu-id="72145-196">Имя очереди вывода Hello задается код в теле hello функции hello.</span><span class="sxs-lookup"><span data-stu-id="72145-196">hello output queue name is set by code in hello body of hello function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="72145-197">Hello **IBinder** интерфейс может также использоваться с hello **таблицы** и **большого двоичного объекта** атрибуты.</span><span class="sxs-lookup"><span data-stu-id="72145-197">hello **IBinder** interface can also be used with hello **Table** and **Blob** attributes.</span></span>

## <a name="how-tooread-and-write-blobs-and-tables-while-processing-a-queue-message"></a><span data-ttu-id="72145-198">Как tooread и записи больших двоичных объектов и таблиц во время обработки сообщения в очереди</span><span class="sxs-lookup"><span data-stu-id="72145-198">How tooread and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="72145-199">Hello **большого двоичного объекта** и **таблицы** атрибуты позволяют tooread и записи больших двоичных объектов и таблиц.</span><span class="sxs-lookup"><span data-stu-id="72145-199">hello **Blob** and **Table** attributes enable you tooread and write blobs and tables.</span></span> <span data-ttu-id="72145-200">Hello образцы в этом разделе применяются tooblobs.</span><span class="sxs-lookup"><span data-stu-id="72145-200">hello samples in this section apply tooblobs.</span></span> <span data-ttu-id="72145-201">Примеры кода, которые показывают, как tootrigger обрабатывает при создании или обновлении больших двоичных объектов см. в разделе [как toouse Azure хранилище больших двоичных объектов с hello SDK веб-заданий](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)и примеры кода, которые считывают и записывают таблиц см. в разделе [как toouse таблицы Azure хранилище с hello SDK веб-задания](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="72145-201">For code samples that show how tootrigger processes when blobs are created or updated, see [How toouse Azure blob storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How toouse Azure table storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="72145-202">Сообщения очереди строк, которые запускают операции с большими двоичными объектами</span><span class="sxs-lookup"><span data-stu-id="72145-202">String queue messages triggering blob operations</span></span>
<span data-ttu-id="72145-203">Для очереди сообщение, содержащее строку **queueTrigger** — это, можно использовать в hello **большого двоичного объекта** атрибута **blobPath** параметра, который содержит содержимое hello сообщение Hello.</span><span class="sxs-lookup"><span data-stu-id="72145-203">For a queue message that contains a string, **queueTrigger** is a placeholder you can use in hello **Blob** attribute's **blobPath** parameter that contains hello contents of hello message.</span></span>

<span data-ttu-id="72145-204">Hello следующий пример использует **поток** объектов tooread и записи больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="72145-204">hello following example uses **Stream** objects tooread and write blobs.</span></span> <span data-ttu-id="72145-205">приветственное сообщение очереди — hello имя BLOB-объектов, находящихся в контейнере textblobs hello.</span><span class="sxs-lookup"><span data-stu-id="72145-205">hello queue message is hello name of a blob located in hello textblobs container.</span></span> <span data-ttu-id="72145-206">Копия hello большой двоичный объект с «-новые» присоединенных toohello имя создается в hello же контейнер.</span><span class="sxs-lookup"><span data-stu-id="72145-206">A copy of hello blob with "-new" appended toohello name is created in hello same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="72145-207">Hello **большого двоичного объекта** атрибута конструктор принимает **blobPath** параметр, определяющий hello контейнера и имя большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="72145-207">hello **Blob** attribute constructor takes a **blobPath** parameter that specifies hello container and blob name.</span></span> <span data-ttu-id="72145-208">Дополнительные сведения об этом заполнитель см. в разделе [как toouse Azure хранилище больших двоичных объектов с hello SDK веб-задания](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="72145-208">For more information about this placeholder, see [How toouse Azure blob storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span></span>

<span data-ttu-id="72145-209">Если атрибут hello оформляет **поток** другой конструктор указывает hello объекта **FileAccess** режим чтения, записи или чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="72145-209">When hello attribute decorates a **Stream** object, another constructor parameter specifies hello **FileAccess** mode as read, write, or read/write.</span></span>

<span data-ttu-id="72145-210">Hello следующий пример использует **CloudBlockBlob** объекта toodelete большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="72145-210">hello following example uses a **CloudBlockBlob** object toodelete a blob.</span></span> <span data-ttu-id="72145-211">приветственное сообщение очереди является именем hello hello большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="72145-211">hello queue message is hello name of hello blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="72145-212">Сообщения очереди [POCO](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)</span><span class="sxs-lookup"><span data-stu-id="72145-212">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="72145-213">Для POCO, хранятся в очереди сообщение hello как JSON, можно использовать местозаполнители, имя свойства объекта hello в hello **очереди** атрибута **blobPath** параметра.</span><span class="sxs-lookup"><span data-stu-id="72145-213">For a POCO stored as JSON in hello queue message, you can use placeholders that name properties of hello object in hello **Queue** attribute's **blobPath** parameter.</span></span> <span data-ttu-id="72145-214">Можно также использовать имена свойства метаданных очереди в качестве заполнителей.</span><span class="sxs-lookup"><span data-stu-id="72145-214">You can also use queue metadata property names as placeholders.</span></span> <span data-ttu-id="72145-215">Ознакомьтесь с разделом [Получение метаданных очереди или сообщения в очереди](#get-queue-or-queue-message-metadata).</span><span class="sxs-lookup"><span data-stu-id="72145-215">See [Get queue or queue message metadata](#get-queue-or-queue-message-metadata).</span></span>

<span data-ttu-id="72145-216">Hello следующий пример копирует BLOB-объектов tooa новый большой двоичный объект с другим расширением.</span><span class="sxs-lookup"><span data-stu-id="72145-216">hello following example copies a blob tooa new blob with a different extension.</span></span> <span data-ttu-id="72145-217">сообщение Hello очереди **BlobInformation** объект, который содержит **BlobName** и **BlobNameWithoutExtension** свойства.</span><span class="sxs-lookup"><span data-stu-id="72145-217">hello queue message is a **BlobInformation** object that includes **BlobName** and **BlobNameWithoutExtension** properties.</span></span> <span data-ttu-id="72145-218">имена свойств Hello используются в качестве меток-заполнителей в пути hello больших двоичных объектов для hello **большого двоичного объекта** атрибуты.</span><span class="sxs-lookup"><span data-stu-id="72145-218">hello property names are used as placeholders in hello blob path for hello **Blob** attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="72145-219">Hello SDK использует hello [пакет Newtonsoft.Json NuGet](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize и десериализации сообщений.</span><span class="sxs-lookup"><span data-stu-id="72145-219">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="72145-220">При создании очереди сообщений в программе, которая не использует hello SDK веб-задания, можно написать код, как следующий пример toocreate POCO очереди сообщений hello приветствия, можно провести синтаксический анализ пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="72145-220">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="72145-221">Если вам требуется toodo некоторые работают в функции перед привязкой tooan большой двоичный объект, можно использовать атрибут hello в текст hello функции hello, как показано в [использовать пакет SDK веб-задания атрибутов в теле функции hello](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span><span class="sxs-lookup"><span data-stu-id="72145-221">If you need toodo some work in your function before binding a blob tooan object, you can use hello attribute in hello body of hello function, as shown in [Use WebJobs SDK attributes in hello body of a function](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span></span>

### <a name="types-you-can-use-hello-blob-attribute-with"></a><span data-ttu-id="72145-222">Типы, которые можно использовать hello атрибута с BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="72145-222">Types you can use hello Blob attribute with</span></span>
<span data-ttu-id="72145-223">Hello **большого двоичного объекта** атрибут может использоваться с hello следующие типы:</span><span class="sxs-lookup"><span data-stu-id="72145-223">hello **Blob** attribute can be used with hello following types:</span></span>

* <span data-ttu-id="72145-224">**Поток** (чтение или запись, указанный с помощью параметра конструктора hello FileAccess)</span><span class="sxs-lookup"><span data-stu-id="72145-224">**Stream** (read or write, specified by using hello FileAccess constructor parameter)</span></span>
* <span data-ttu-id="72145-225">**TextReader;**</span><span class="sxs-lookup"><span data-stu-id="72145-225">**TextReader**</span></span>
* <span data-ttu-id="72145-226">**TextWriter**</span><span class="sxs-lookup"><span data-stu-id="72145-226">**TextWriter**</span></span>
* <span data-ttu-id="72145-227">**string** (чтение);</span><span class="sxs-lookup"><span data-stu-id="72145-227">**string** (read)</span></span>
* <span data-ttu-id="72145-228">**строки** (записи; создает большой двоичный объект только в том случае, если параметр строки hello отлично от null, при возврате из функции hello)</span><span class="sxs-lookup"><span data-stu-id="72145-228">**out string** (write; creates a blob only if hello string parameter is non-null when hello function returns)</span></span>
* <span data-ttu-id="72145-229">POCO (чтение);</span><span class="sxs-lookup"><span data-stu-id="72145-229">POCO (read)</span></span>
* <span data-ttu-id="72145-230">out POCO (записи; всегда создает большой двоичный объект, создает как объект null, если параметр POCO имеет значение null, при возврате из функции hello)</span><span class="sxs-lookup"><span data-stu-id="72145-230">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when hello function returns)</span></span>
* <span data-ttu-id="72145-231">**CloudBlobStream** (запись);</span><span class="sxs-lookup"><span data-stu-id="72145-231">**CloudBlobStream** (write)</span></span>
* <span data-ttu-id="72145-232">**ICloudBlob** (чтение или запись);</span><span class="sxs-lookup"><span data-stu-id="72145-232">**ICloudBlob** (read or write)</span></span>
* <span data-ttu-id="72145-233">**CloudBlockBlob** (чтение или запись);</span><span class="sxs-lookup"><span data-stu-id="72145-233">**CloudBlockBlob** (read or write)</span></span>
* <span data-ttu-id="72145-234">**CloudPageBlob** (чтение или запись).</span><span class="sxs-lookup"><span data-stu-id="72145-234">**CloudPageBlob** (read or write)</span></span>

## <a name="how-toohandle-poison-messages"></a><span data-ttu-id="72145-235">Как toohandle подозрительные сообщения</span><span class="sxs-lookup"><span data-stu-id="72145-235">How toohandle poison messages</span></span>
<span data-ttu-id="72145-236">Сообщения, содержимое которого приводит toofail функции называются *сообщения о сбое*.</span><span class="sxs-lookup"><span data-stu-id="72145-236">Messages whose content causes a function toofail are called *poison messages*.</span></span> <span data-ttu-id="72145-237">При сбое функции hello, очередь приветственное сообщение не удаляется и в конечном счете передается еще раз, может вызвать toobe hello цикл повторяется.</span><span class="sxs-lookup"><span data-stu-id="72145-237">When hello function fails, hello queue message is not deleted and eventually is picked up again, causing hello cycle toobe repeated.</span></span> <span data-ttu-id="72145-238">Hello SDK можно прервать цикл hello автоматически после ограниченного числа итераций, или это можно сделать вручную.</span><span class="sxs-lookup"><span data-stu-id="72145-238">hello SDK can automatically interrupt hello cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="72145-239">Автоматическая обработка сообщений</span><span class="sxs-lookup"><span data-stu-id="72145-239">Automatic poison message handling</span></span>
<span data-ttu-id="72145-240">Hello SDK будет вызвать функцию копирования tooprocess раз too5 сообщения в очереди.</span><span class="sxs-lookup"><span data-stu-id="72145-240">hello SDK will call a function up too5 times tooprocess a queue message.</span></span> <span data-ttu-id="72145-241">При сбое hello пятый try, приветственное сообщение — перемещенный tooa очереди подозрительных сообщений.</span><span class="sxs-lookup"><span data-stu-id="72145-241">If hello fifth try fails, hello message is moved tooa poison queue.</span></span> <span data-ttu-id="72145-242">Вы увидите, как tooconfigure hello максимальное число повторных попыток в [как параметры конфигурации tooset](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="72145-242">You can see how tooconfigure hello maximum number of retries in [How tooset configuration options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="72145-243">очередь подозрительных сообщений Hello называется *{originalqueuename}*-подозрительное.</span><span class="sxs-lookup"><span data-stu-id="72145-243">hello poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="72145-244">Можно написать tooprocess функция сообщения из очереди подозрительных сообщений hello ее регистрации или отправка уведомления о необходимости ручного вмешательства.</span><span class="sxs-lookup"><span data-stu-id="72145-244">You can write a function tooprocess messages from hello poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="72145-245">В следующий пример hello hello **CopyBlob** функция завершится ошибкой, если сообщения в очереди содержит hello имя большого двоичного объекта, который не существует.</span><span class="sxs-lookup"><span data-stu-id="72145-245">In hello following example hello **CopyBlob** function will fail when a queue message contains hello name of a blob that doesn't exist.</span></span> <span data-ttu-id="72145-246">В этом случае приветственное сообщение перемещается из hello copyblobqueue очереди toohello copyblobqueue подозрительных очереди.</span><span class="sxs-lookup"><span data-stu-id="72145-246">When that happens, hello message is moved from hello copyblobqueue queue toohello copyblobqueue-poison queue.</span></span> <span data-ttu-id="72145-247">Hello **ProcessPoisonMessage** то подозрительное сообщение hello журналы.</span><span class="sxs-lookup"><span data-stu-id="72145-247">hello **ProcessPoisonMessage** then logs hello poison message.</span></span>

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
            logger.WriteLine("Failed toocopy blob, name=" + blobName);
        }

<span data-ttu-id="72145-248">Hello ниже показан вывод на консоль из этих функций при обработке подозрительных сообщений.</span><span class="sxs-lookup"><span data-stu-id="72145-248">hello following illustration shows console output from these functions when a poison message is processed.</span></span>

![Вывод консоли для обработки подозрительных сообщений](./media/vs-storage-webjobs-getting-started-queues/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="72145-250">Ручная обработка подозрительных сообщений</span><span class="sxs-lookup"><span data-stu-id="72145-250">Manual poison message handling</span></span>
<span data-ttu-id="72145-251">Hello количество обработки сообщения для обработки можно получить, добавив **int** параметр с именем **dequeueCount** tooyour функции.</span><span class="sxs-lookup"><span data-stu-id="72145-251">You can get hello number of times a message has been picked up for processing by adding an **int** parameter named **dequeueCount** tooyour function.</span></span> <span data-ttu-id="72145-252">После этого можно hello проверьте количество в коде функция вывода из очереди и выполнять собственные подозрительное сообщение обработки при hello число превышает пороговое значение, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="72145-252">You can then check hello dequeue count in function code and perform your own poison message handling when hello number exceeds a threshold, as shown in hello following example.</span></span>

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName, int dequeueCount,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput,
            TextWriter logger)
        {
            if (dequeueCount > 3)
            {
                logger.WriteLine("Failed toocopy blob, name=" + blobName);
            }
            else
            {
            blobInput.CopyTo(blobOutput, 4096);
            }
        }

## <a name="how-tooset-configuration-options"></a><span data-ttu-id="72145-253">Как параметры конфигурации tooset</span><span class="sxs-lookup"><span data-stu-id="72145-253">How tooset configuration options</span></span>
<span data-ttu-id="72145-254">Можно использовать hello **JobHostConfiguration** hello tooset тип следующие параметры конфигурации:</span><span class="sxs-lookup"><span data-stu-id="72145-254">You can use hello **JobHostConfiguration** type tooset hello following configuration options:</span></span>

* <span data-ttu-id="72145-255">Задать строки подключения пакета SDK для hello в коде.</span><span class="sxs-lookup"><span data-stu-id="72145-255">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="72145-256">Настройка таких параметров атрибута **QueueTrigger** , как максимальное значение счетчика вывода из очереди.</span><span class="sxs-lookup"><span data-stu-id="72145-256">Configure **QueueTrigger** settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="72145-257">Получение имен очередей из конфигурации</span><span class="sxs-lookup"><span data-stu-id="72145-257">Get queue names from configuration.</span></span>

### <a name="set-sdk-connection-strings-in-code"></a><span data-ttu-id="72145-258">Установка строк подключения пакета SDK в коде</span><span class="sxs-lookup"><span data-stu-id="72145-258">Set SDK connection strings in code</span></span>
<span data-ttu-id="72145-259">Задание строк подключения пакета SDK для hello в коде позволяет вы toouse собственные имена строку соединения в файлах конфигурации или переменные среды, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="72145-259">Setting hello SDK connection strings in code enables you toouse your own connection string names in configuration files or environment variables, as shown in hello following example.</span></span>

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

### <a name="configure-queuetrigger--settings"></a><span data-ttu-id="72145-260">Настройка параметров атрибута QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="72145-260">Configure QueueTrigger  settings</span></span>
<span data-ttu-id="72145-261">Можно настроить следующие параметры, которые применяются для обработки сообщений в очереди toohello hello.</span><span class="sxs-lookup"><span data-stu-id="72145-261">You can configure hello following settings that apply toohello queue message processing:</span></span>

* <span data-ttu-id="72145-262">Здравствуйте, максимальное количество сообщений, которые извлекаются одновременно toobe параллельного выполнения (по умолчанию — 16).</span><span class="sxs-lookup"><span data-stu-id="72145-262">hello maximum number of queue messages that are picked up simultaneously toobe executed in parallel (default is 16).</span></span>
* <span data-ttu-id="72145-263">Здравствуйте, максимальное число повторных попыток перед отправкой сообщения в очереди tooa очереди подозрительных сообщений (по умолчанию — 5).</span><span class="sxs-lookup"><span data-stu-id="72145-263">hello maximum number of retries before a queue message is sent tooa poison queue (default is 5).</span></span>
* <span data-ttu-id="72145-264">Hello максимальное время ожидания перед запросом еще раз, когда очередь пуста (по умолчанию — 1 минута).</span><span class="sxs-lookup"><span data-stu-id="72145-264">hello maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="72145-265">Следующий пример показывает как Hello tooconfigure эти параметры:</span><span class="sxs-lookup"><span data-stu-id="72145-265">hello following example shows how tooconfigure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="set-values-for-webjobs-sdk-constructor-parameters-in-code"></a><span data-ttu-id="72145-266">Установка значений параметров конструктора пакета SDK для заданий WebJob в коде</span><span class="sxs-lookup"><span data-stu-id="72145-266">Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="72145-267">Иногда требуется toospecify имя очереди, имя BLOB-объекта или контейнера, или имя таблицы, в коде, вместо жестко его.</span><span class="sxs-lookup"><span data-stu-id="72145-267">Sometimes you want toospecify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="72145-268">Например, может потребоваться имя очереди hello toospecify для **QueueTrigger** в переменной среде или файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="72145-268">For example, you might want toospecify hello queue name for **QueueTrigger** in a configuration file or environment variable.</span></span>

<span data-ttu-id="72145-269">Это можно сделать путем передачи **NameResolver** объекта toohello **JobHostConfiguration** типа.</span><span class="sxs-lookup"><span data-stu-id="72145-269">You can do that by passing in a **NameResolver** object toohello **JobHostConfiguration** type.</span></span> <span data-ttu-id="72145-270">Включает специальные заполнители, заключенная в символы процента (%) в конструктор атрибута SDK веб-задания параметров и **NameResolver** код задает toobe hello фактические значения, используемые вместо эти заполнители.</span><span class="sxs-lookup"><span data-stu-id="72145-270">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your **NameResolver** code specifies hello actual values toobe used in place of those placeholders.</span></span>

<span data-ttu-id="72145-271">Например предположим, что нужно toouse очереди с именем, logqueuetest в тестовой среде hello и один именованный logqueueprod в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="72145-271">For example, suppose you want toouse a queue named logqueuetest in hello test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="72145-272">Вместо жестко очереди, необходимо, чтобы имя hello toospecify записи в hello **appSettings** коллекцию, которая будет иметь имя фактического очереди hello.</span><span class="sxs-lookup"><span data-stu-id="72145-272">Instead of a hard-coded queue name, you want toospecify hello name of an entry in hello **appSettings** collection that would have hello actual queue name.</span></span> <span data-ttu-id="72145-273">Если hello **appSettings** ключа является logqueue, функция может выглядеть следующим образом hello в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="72145-273">If hello **appSettings** key is logqueue, your function could look like hello following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="72145-274">Ваш **NameResolver** класс затем удалось получить имя очереди hello из **appSettings** как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="72145-274">Your **NameResolver** class could then get hello queue name from **appSettings** as shown in hello following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="72145-275">Передайте hello **NameResolver** класса в toohello **JobHost** объекта, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="72145-275">You pass hello **NameResolver** class in toohello **JobHost** object as shown in hello following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="72145-276">**Примечание:** очередей, таблиц и имена больших двоичных объектов не будут разрешены при каждом вызове функции, но имена контейнеров больших двоичных объектов разрешаются только при запуске приложения hello.</span><span class="sxs-lookup"><span data-stu-id="72145-276">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when hello application starts.</span></span> <span data-ttu-id="72145-277">Невозможно изменить имя контейнера больших двоичных объектов, пока выполняется задание hello.</span><span class="sxs-lookup"><span data-stu-id="72145-277">You can't change blob container name while hello job is running.</span></span>

## <a name="how-tootrigger-a-function-manually"></a><span data-ttu-id="72145-278">Как tootrigger функции вручную</span><span class="sxs-lookup"><span data-stu-id="72145-278">How tootrigger a function manually</span></span>
<span data-ttu-id="72145-279">tootrigger функцию вручную, используйте hello **вызвать** или **CallAsync** метод hello **JobHost** объекта и hello **NoAutomaticTrigger** атрибут функции hello, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="72145-279">tootrigger a function manually, use hello **Call** or **CallAsync** method on hello **JobHost** object and hello **NoAutomaticTrigger** attribute on hello function, as shown in hello following example.</span></span>

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

## <a name="how-toowrite-logs"></a><span data-ttu-id="72145-280">Каким образом ведет журнал toowrite</span><span class="sxs-lookup"><span data-stu-id="72145-280">How toowrite logs</span></span>
<span data-ttu-id="72145-281">Hello панели мониторинга показывает журналы в двух местах: hello hello веб-задания и странице приветствия для конкретного вызова веб-задания.</span><span class="sxs-lookup"><span data-stu-id="72145-281">hello Dashboard shows logs in two places: hello page for hello WebJob, and hello page for a particular WebJob invocation.</span></span>

![Журналы на странице задания WebJob](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

![Журналы на странице вызова функций](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="72145-284">Выходные данные консоли методы, вызываемые в функции или hello **Main()** метод отображается в странице панели мониторинга hello hello веб-задания, а не в страницу приветствия для вызова определенного метода.</span><span class="sxs-lookup"><span data-stu-id="72145-284">Output from Console methods that you call in a function or in hello **Main()** method appears in hello Dashboard page for hello WebJob, not in hello page for a particular method invocation.</span></span> <span data-ttu-id="72145-285">Выходные данные из объекта TextWriter hello, которое получается из параметра в подписи метода отображается на странице панели мониторинга hello для вызова метода.</span><span class="sxs-lookup"><span data-stu-id="72145-285">Output from hello TextWriter object that you get from a parameter in your method signature appears in hello Dashboard page for a method invocation.</span></span>

<span data-ttu-id="72145-286">Вывод на консоль не может быть вызова определенного метода связанного tooa, поскольку hello консоли является однопоточным, хотя многие функции задания, запущенные на hello то же время.</span><span class="sxs-lookup"><span data-stu-id="72145-286">Console output can't be linked tooa particular method invocation because hello Console is single-threaded, while many job functions may be running at hello same time.</span></span> <span data-ttu-id="72145-287">Вот почему hello SDK предоставляет каждый вызов функции с свой собственный уникальный журнал объект модуля записи.</span><span class="sxs-lookup"><span data-stu-id="72145-287">That's why hello  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="72145-288">toowrite [журналы трассировки приложения](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), используйте **Console.Out** (создает журналы, которые помечены как информация) и **Console.Error** (создает журналы, которые помечены как ошибки).</span><span class="sxs-lookup"><span data-stu-id="72145-288">toowrite [application tracing logs](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use **Console.Out** (creates logs marked as INFO) and **Console.Error** (creates logs marked as ERROR).</span></span> <span data-ttu-id="72145-289">Альтернативным вариантом является toouse [трассировки или TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), который предоставляет подробные сведения, предупреждение, и критическое уровни tooInfo сложения и ошибки.</span><span class="sxs-lookup"><span data-stu-id="72145-289">An alternative is toouse [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition tooInfo and Error.</span></span> <span data-ttu-id="72145-290">Журналы трассировки приложения отображаются в файлах журналов приложения web hello, таблицы Azure или больших двоичных объектов Azure в зависимости от того, как настроить Azure веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="72145-290">Application tracing logs appear in hello web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="72145-291">Имеет значение true, если все вывода на консоль, самых последних журналов 100 приложения hello также отображаются в странице панели мониторинга hello hello веб-задания, не странице приветствия для вызова функции.</span><span class="sxs-lookup"><span data-stu-id="72145-291">As is true of all Console output, hello most recent 100 application logs also appear in hello Dashboard page for hello WebJob, not hello page for a function invocation.</span></span>

<span data-ttu-id="72145-292">Вывод на консоль будет hello панели мониторинга только в том случае, если программа hello выполняется в веб-задания Azure, не в том случае, если программа hello выполняется локально или в некоторых других условиях.</span><span class="sxs-lookup"><span data-stu-id="72145-292">Console output appears in hello Dashboard only if hello program is running in an Azure WebJob, not if hello program is running locally or in some other environment.</span></span>

<span data-ttu-id="72145-293">Ведение журнала можно отключить, установив подключение строку hello мониторинга toonull.</span><span class="sxs-lookup"><span data-stu-id="72145-293">You can disable logging by setting hello Dashboard connection string toonull.</span></span> <span data-ttu-id="72145-294">Дополнительные сведения см. в разделе [как tooset параметры конфигурации](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="72145-294">For more information, see [How tooset Configuration Options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="72145-295">Hello следующем примере показано несколько способов toowrite журналы:</span><span class="sxs-lookup"><span data-stu-id="72145-295">hello following example shows several ways toowrite logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="72145-296">Здравствуйте, выходные данные hello в hello мониторинга SDK веб-заданий, **TextWriter** объекта появляется при открытии страницы toohello для какого-либо вызов функции и выберите **переключить вывод**:</span><span class="sxs-lookup"><span data-stu-id="72145-296">In hello WebJobs SDK Dashboard, hello output from hello **TextWriter** object shows up when you go toohello page for a particular function invocation and select **Toggle Output**:</span></span>

![Ссылка для вызова](./media/vs-storage-webjobs-getting-started-queues/dashboardinvocations.png)

![Журналы на странице вызова функций](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="72145-299">В hello мониторинга SDK веб-заданий, hello последние 100 строк консоли вывода Показать вверх, если переход на страницу toohello для hello веб-задания (не для вызова функций hello) и выберите **переключить вывод**.</span><span class="sxs-lookup"><span data-stu-id="72145-299">In hello WebJobs SDK Dashboard, hello most recent 100 lines of Console output show up when you go toohello page for hello WebJob (not for hello function invocation) and select **Toggle Output**.</span></span>

![Переключить выходные данные](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

<span data-ttu-id="72145-301">В непрерывное веб-задание, журнал приложений отображаются в/данных/задания и непрерывной/*{webjobname}*/job_log.txt в hello web app файловой системы.</span><span class="sxs-lookup"><span data-stu-id="72145-301">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in hello web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="72145-302">В приложении hello BLOB-объектов Azure журналы будут выглядеть следующим образом: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Здравствуй, мир!, 2014-09-26T21:01:13 ошибки, contosoadsnew, 491e54, 635473620738373502,0,17404,19,Console.Error - Здравствуй, мир!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Здравствуй, мир!,</span><span class="sxs-lookup"><span data-stu-id="72145-302">In an Azure blob hello application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="72145-303">И в таблице Azure hello **Console.Out** и **Console.Error** журналы выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="72145-303">And in an Azure table hello **Console.Out** and **Console.Error** logs look like this:</span></span>

![Журнал Info в таблице](./media/vs-storage-webjobs-getting-started-queues/tableinfo.png)

![Журнал Error в таблице](./media/vs-storage-webjobs-getting-started-queues/tableerror.png)

## <a name="next-steps"></a><span data-ttu-id="72145-306">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="72145-306">Next steps</span></span>
<span data-ttu-id="72145-307">В этой статье был дан код образцы где показано, как toohandle распространенные сценарии для работы с очередями Azure.</span><span class="sxs-lookup"><span data-stu-id="72145-307">This article has provided code samples that show how toohandle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="72145-308">Дополнительные сведения о статье toouse веб-заданий Azure и hello SDK веб-заданий [ресурсы документации веб-заданий Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="72145-308">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

