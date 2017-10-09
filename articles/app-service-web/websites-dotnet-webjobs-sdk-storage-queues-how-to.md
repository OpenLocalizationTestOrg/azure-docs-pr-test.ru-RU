---
title: "aaaHow toouse хранилища очереди Azure с hello SDK веб-заданий"
description: "Узнайте, как хранилище с hello SDK веб-заданий очередей toouse Azure. Создание и удаление очередей; вставка, обзор, получение и удаление сообщений очереди, а также многое другое."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: dbfac5d9-f4a0-4e3e-9ecc-af3d7bf80463
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 49f844436b0453489800b2762a5c7dc30b9db805
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-queue-storage-with-hello-webjobs-sdk"></a><span data-ttu-id="f5dca-104">Как toouse Azure очередь хранилища с hello SDK веб-заданий</span><span class="sxs-lookup"><span data-stu-id="f5dca-104">How toouse Azure queue storage with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="f5dca-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="f5dca-105">Overview</span></span>
<span data-ttu-id="f5dca-106">Это руководство содержит образцы кода C#, которые показывают, как toouse hello веб-заданий Azure SDK версии 1.x hello службы хранилища очередей Azure.</span><span class="sxs-lookup"><span data-stu-id="f5dca-106">This guide provides C# code samples that show how toouse hello Azure WebJobs SDK version 1.x with hello Azure queue storage service.</span></span>

<span data-ttu-id="f5dca-107">Hello руководстве предполагается, вы знаете [как toocreate проект веб-задания в Visual Studio с подключением строки этой учетной записи хранения точки tooyour](websites-dotnet-webjobs-sdk-get-started.md) или слишком[нескольких учетных записей хранения](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="f5dca-107">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md) or too[multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="f5dca-108">Большинство фрагментов кода hello Показывать только функции, не hello код, создающий hello `JobHost` объекта, как показано в примере:</span><span class="sxs-lookup"><span data-stu-id="f5dca-108">Most of hello code snippets only show functions, not hello code that creates hello `JobHost` object as in this example:</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

<span data-ttu-id="f5dca-109">Hello руководство включает hello следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="f5dca-109">hello guide includes hello following topics:</span></span>

* [<span data-ttu-id="f5dca-110">Как tootrigger функции при получении сообщения в очереди</span><span class="sxs-lookup"><span data-stu-id="f5dca-110">How tootrigger a function when a queue message is received</span></span>](#trigger)
  * <span data-ttu-id="f5dca-111">Строковые сообщения очереди</span><span class="sxs-lookup"><span data-stu-id="f5dca-111">String queue messages</span></span>
  * <span data-ttu-id="f5dca-112">Сообщения очереди POCO</span><span class="sxs-lookup"><span data-stu-id="f5dca-112">POCO queue messages</span></span>
  * <span data-ttu-id="f5dca-113">Асинхронные функции</span><span class="sxs-lookup"><span data-stu-id="f5dca-113">Async functions</span></span>
  * <span data-ttu-id="f5dca-114">Атрибут QueueTrigger hello типы работает с</span><span class="sxs-lookup"><span data-stu-id="f5dca-114">Types hello QueueTrigger attribute works with</span></span>
  * <span data-ttu-id="f5dca-115">Алгоритм опроса</span><span class="sxs-lookup"><span data-stu-id="f5dca-115">Polling algorithm</span></span>
  * <span data-ttu-id="f5dca-116">Выполнение на нескольких экземплярах</span><span class="sxs-lookup"><span data-stu-id="f5dca-116">Multiple instances</span></span>
  * <span data-ttu-id="f5dca-117">Параллельное выполнение</span><span class="sxs-lookup"><span data-stu-id="f5dca-117">Parallel execution</span></span>
  * <span data-ttu-id="f5dca-118">Получение очереди или метаданных очереди сообщений</span><span class="sxs-lookup"><span data-stu-id="f5dca-118">Get queue or queue message metadata</span></span>
  * <span data-ttu-id="f5dca-119">Корректное завершение работы</span><span class="sxs-lookup"><span data-stu-id="f5dca-119">Graceful shutdown</span></span>
* [<span data-ttu-id="f5dca-120">Как toocreate очереди сообщений во время обработки сообщения в очереди</span><span class="sxs-lookup"><span data-stu-id="f5dca-120">How toocreate a queue message while processing a queue message</span></span>](#createqueue)
  * <span data-ttu-id="f5dca-121">Строковые сообщения очереди</span><span class="sxs-lookup"><span data-stu-id="f5dca-121">String queue messages</span></span>
  * <span data-ttu-id="f5dca-122">Сообщения очереди POCO</span><span class="sxs-lookup"><span data-stu-id="f5dca-122">POCO queue messages</span></span>
  * <span data-ttu-id="f5dca-123">Создание нескольких сообщений или сообщений в асинхронных функциях</span><span class="sxs-lookup"><span data-stu-id="f5dca-123">Create multiple messages or in async functions</span></span>
  * <span data-ttu-id="f5dca-124">Атрибут очереди hello типы работает с</span><span class="sxs-lookup"><span data-stu-id="f5dca-124">Types hello Queue attribute works with</span></span>
  * <span data-ttu-id="f5dca-125">Использование пакета SDK веб-задания атрибутов в теле функции hello</span><span class="sxs-lookup"><span data-stu-id="f5dca-125">Use WebJobs SDK attributes in hello body of a function</span></span>
* [<span data-ttu-id="f5dca-126">Как tooread и записи больших двоичных объектов при обработке сообщения в очереди</span><span class="sxs-lookup"><span data-stu-id="f5dca-126">How tooread and write blobs while processing a queue message</span></span>](#blobs)
  * <span data-ttu-id="f5dca-127">Строковые сообщения очереди</span><span class="sxs-lookup"><span data-stu-id="f5dca-127">String queue messages</span></span>
  * <span data-ttu-id="f5dca-128">Сообщения очереди POCO</span><span class="sxs-lookup"><span data-stu-id="f5dca-128">POCO queue messages</span></span>
  * <span data-ttu-id="f5dca-129">Типы hello большого двоичного объекта атрибута работает с</span><span class="sxs-lookup"><span data-stu-id="f5dca-129">Types hello Blob attribute works with</span></span>
* [<span data-ttu-id="f5dca-130">Как toohandle подозрительные сообщения</span><span class="sxs-lookup"><span data-stu-id="f5dca-130">How toohandle poison messages</span></span>](#poison)
  * <span data-ttu-id="f5dca-131">Автоматическая обработка сообщений</span><span class="sxs-lookup"><span data-stu-id="f5dca-131">Automatic poison message handling</span></span>
  * <span data-ttu-id="f5dca-132">Ручная обработка подозрительных сообщений</span><span class="sxs-lookup"><span data-stu-id="f5dca-132">Manual poison message handling</span></span>
* [<span data-ttu-id="f5dca-133">Как параметры конфигурации tooset</span><span class="sxs-lookup"><span data-stu-id="f5dca-133">How tooset configuration options</span></span>](#config)
  * <span data-ttu-id="f5dca-134">Установка строк подключения пакета SDK в коде</span><span class="sxs-lookup"><span data-stu-id="f5dca-134">Set SDK connection strings in code</span></span>
  * <span data-ttu-id="f5dca-135">Настройка параметров атрибута QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="f5dca-135">Configure QueueTrigger settings</span></span>
  * <span data-ttu-id="f5dca-136">Установка значений параметров конструктора пакета SDK для заданий WebJob в коде</span><span class="sxs-lookup"><span data-stu-id="f5dca-136">Set values for WebJobs SDK constructor parameters in code</span></span>
* [<span data-ttu-id="f5dca-137">Как tootrigger функции вручную</span><span class="sxs-lookup"><span data-stu-id="f5dca-137">How tootrigger a function manually</span></span>](#manual)
* [<span data-ttu-id="f5dca-138">Каким образом ведет журнал toowrite</span><span class="sxs-lookup"><span data-stu-id="f5dca-138">How toowrite logs</span></span>](#logs)
* [<span data-ttu-id="f5dca-139">Как toohandle ошибки и настроить время ожидания</span><span class="sxs-lookup"><span data-stu-id="f5dca-139">How toohandle errors and configure timeouts</span></span>](#errors)
* [<span data-ttu-id="f5dca-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f5dca-140">Next steps</span></span>](#nextsteps)

## <span data-ttu-id="f5dca-141"><a id="trigger"></a>Как tootrigger функции при получении сообщения в очереди</span><span class="sxs-lookup"><span data-stu-id="f5dca-141"><a id="trigger"></a> How tootrigger a function when a queue message is received</span></span>
<span data-ttu-id="f5dca-142">вызывает функцию, которая hello SDK веб-заданий toowrite при получении сообщения в очереди, используйте hello `QueueTrigger` атрибута.</span><span class="sxs-lookup"><span data-stu-id="f5dca-142">toowrite a function that hello WebJobs SDK calls when a queue message is received, use hello `QueueTrigger` attribute.</span></span> <span data-ttu-id="f5dca-143">Конструктор атрибута Hello принимает строковый параметр, задающий имя hello toopoll очереди hello.</span><span class="sxs-lookup"><span data-stu-id="f5dca-143">hello attribute constructor takes a string parameter that specifies hello name of hello queue toopoll.</span></span> <span data-ttu-id="f5dca-144">Вы также можете [динамически задать имя очереди hello](#config).</span><span class="sxs-lookup"><span data-stu-id="f5dca-144">You can also [set hello queue name dynamically](#config).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="f5dca-145">Строковые сообщения очереди</span><span class="sxs-lookup"><span data-stu-id="f5dca-145">String queue messages</span></span>
<span data-ttu-id="f5dca-146">В следующем примере hello, hello очередь содержит строковое сообщение, поэтому `QueueTrigger` будет применен tooa строковый параметр с именем `logMessage` , содержащее содержимое очереди приветственное сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="f5dca-146">In hello following example, hello queue contains a string message, so `QueueTrigger` is applied tooa string parameter named `logMessage` which contains hello content of hello queue message.</span></span> <span data-ttu-id="f5dca-147">Здравствуйте, функция [записывает toohello сообщение журнала мониторинга](#logs).</span><span class="sxs-lookup"><span data-stu-id="f5dca-147">hello function [writes a log message toohello Dashboard](#logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="f5dca-148">Помимо `string`, hello параметр может быть массив байтов `CloudQueueMessage` объекта или POCO, определяемому вами.</span><span class="sxs-lookup"><span data-stu-id="f5dca-148">Besides `string`, hello parameter may be a byte array, a `CloudQueueMessage` object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="f5dca-149">Сообщения очереди [POCO](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)</span><span class="sxs-lookup"><span data-stu-id="f5dca-149">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="f5dca-150">В следующем примере hello, сообщение hello очереди содержит JSON для `BlobInformation` объекта, который включает `BlobName` свойство.</span><span class="sxs-lookup"><span data-stu-id="f5dca-150">In hello following example, hello queue message contains JSON for a `BlobInformation` object which includes a `BlobName` property.</span></span> <span data-ttu-id="f5dca-151">пакет SDK для Hello автоматически десериализует hello объекта.</span><span class="sxs-lookup"><span data-stu-id="f5dca-151">hello SDK automatically deserializes hello object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

<span data-ttu-id="f5dca-152">Hello SDK использует hello [пакет Newtonsoft.Json NuGet](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize и десериализации сообщений.</span><span class="sxs-lookup"><span data-stu-id="f5dca-152">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="f5dca-153">При создании очереди сообщений в программе, которая не использует hello SDK веб-задания, можно написать код, как следующий пример toocreate POCO очереди сообщений hello приветствия, можно провести синтаксический анализ пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="f5dca-153">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="f5dca-154">Асинхронные функции</span><span class="sxs-lookup"><span data-stu-id="f5dca-154">Async functions</span></span>
<span data-ttu-id="f5dca-155">После асинхронного функции Hello [записывает журнал toohello мониторинга](#logs).</span><span class="sxs-lookup"><span data-stu-id="f5dca-155">hello following async function [writes a log toohello Dashboard](#logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="f5dca-156">Может потребоваться асинхронных функций [токен отмены](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), как показано в hello следующий пример, который копирует большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="f5dca-156">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in hello following example which copies a blob.</span></span> <span data-ttu-id="f5dca-157">(Объяснение hello `queueTrigger` заполнитель, в разделе hello [большие двоичные объекты](#blobs) раздел.)</span><span class="sxs-lookup"><span data-stu-id="f5dca-157">(For an explanation of hello `queueTrigger` placeholder, see hello [Blobs](#blobs) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

### <span data-ttu-id="f5dca-158"><a id="qtattributetypes"></a>Атрибут QueueTrigger hello типы работает с</span><span class="sxs-lookup"><span data-stu-id="f5dca-158"><a id="qtattributetypes"></a> Types hello QueueTrigger attribute works with</span></span>
<span data-ttu-id="f5dca-159">Можно использовать `QueueTrigger` с hello следующие типы:</span><span class="sxs-lookup"><span data-stu-id="f5dca-159">You can use `QueueTrigger` with hello following types:</span></span>

* `string`
* <span data-ttu-id="f5dca-160">тип POCO, сериализованный как JSON;</span><span class="sxs-lookup"><span data-stu-id="f5dca-160">A POCO type serialized as JSON</span></span>
* `byte[]`
* `CloudQueueMessage`

### <span data-ttu-id="f5dca-161"><a id="polling"></a> Алгоритм опроса</span><span class="sxs-lookup"><span data-stu-id="f5dca-161"><a id="polling"></a> Polling algorithm</span></span>
<span data-ttu-id="f5dca-162">Hello SDK реализует эффекта экспоненциальной отсрочки алгоритм случайных tooreduce hello простоя очереди опроса на транзакционные издержки хранения.</span><span class="sxs-lookup"><span data-stu-id="f5dca-162">hello SDK implements a random exponential back-off algorithm tooreduce hello effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="f5dca-163">При обнаружении сообщение hello SDK ожидает в течение двух секунд и затем проверяет наличие другого сообщения; Если сообщение не найдено он ожидает около четырех секунд перед повторной попыткой.</span><span class="sxs-lookup"><span data-stu-id="f5dca-163">When a message is found, hello SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="f5dca-164">После tooget последующих неудачных попытках сообщения в очереди, время ожидания hello продолжается tooincrease, пока не достигнет hello максимальное время ожидания, какие значения по умолчанию tooone минуты.</span><span class="sxs-lookup"><span data-stu-id="f5dca-164">After subsequent failed attempts tooget a queue message, hello wait time continues tooincrease until it reaches hello maximum wait time, which defaults tooone minute.</span></span> <span data-ttu-id="f5dca-165">[Hello максимальное время ожидания настраивается](#config).</span><span class="sxs-lookup"><span data-stu-id="f5dca-165">[hello maximum wait time is configurable](#config).</span></span>

### <span data-ttu-id="f5dca-166"><a id="instances"></a> Выполнение на нескольких экземплярах</span><span class="sxs-lookup"><span data-stu-id="f5dca-166"><a id="instances"></a> Multiple instances</span></span>
<span data-ttu-id="f5dca-167">Если веб-приложение выполняется на нескольких экземплярах, непрерывное веб-задание выполняется на каждом компьютере, и каждой машины будет ожидать триггеры и повторите toorun функции.</span><span class="sxs-lookup"><span data-stu-id="f5dca-167">If your web app runs on multiple instances, a continuous WebJob runs on each machine, and each machine will wait for triggers and attempt toorun functions.</span></span> <span data-ttu-id="f5dca-168">Hello SDK веб-задания очереди триггера автоматически предотвращает функции обработки сообщения в очереди несколько раз. функции не имеют toobe записи toobe идемпотентными.</span><span class="sxs-lookup"><span data-stu-id="f5dca-168">hello WebJobs SDK queue trigger automatically prevents a function from processing a queue message multiple times; functions do not have toobe written toobe idempotent.</span></span> <span data-ttu-id="f5dca-169">Тем не менее, если требуется tooensure только одного экземпляра функции выполняется даже в том случае, если существует несколько экземпляров веб-приложения hello узла, можно использовать hello `Singleton` атрибута.</span><span class="sxs-lookup"><span data-stu-id="f5dca-169">However, if you want tooensure that only one instance of a function runs even when there are multiple instances of hello host web app, you can use hello `Singleton` attribute.</span></span>

### <span data-ttu-id="f5dca-170"><a id="parallel"></a> Параллельное выполнение</span><span class="sxs-lookup"><span data-stu-id="f5dca-170"><a id="parallel"></a> Parallel execution</span></span>
<span data-ttu-id="f5dca-171">Если у вас есть несколько функций, которые прослушивают различные очереди, hello SDK вызывает их параллельно при получении сообщений одновременно.</span><span class="sxs-lookup"><span data-stu-id="f5dca-171">If you have multiple functions listening on different queues, hello SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="f5dca-172">Hello это верно и при получении нескольких сообщений для одной очереди.</span><span class="sxs-lookup"><span data-stu-id="f5dca-172">hello same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="f5dca-173">По умолчанию hello SDK получает пакет 16 очереди сообщений за раз и выполняет функции hello, обрабатывает их параллельно.</span><span class="sxs-lookup"><span data-stu-id="f5dca-173">By default, hello SDK gets a batch of 16 queue messages at a time and executes hello function that processes them in parallel.</span></span> <span data-ttu-id="f5dca-174">[размер пакета Hello настраивается](#config).</span><span class="sxs-lookup"><span data-stu-id="f5dca-174">[hello batch size is configurable](#config).</span></span> <span data-ttu-id="f5dca-175">При получении hello число обрабатываемых вниз toohalf размера пакета hello, hello SDK возвращает другой пакет и начинает обработку этих сообщений.</span><span class="sxs-lookup"><span data-stu-id="f5dca-175">When hello number being processed gets down toohalf of hello batch size, hello SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="f5dca-176">Поэтому hello максимальное количество одновременных сообщений, обрабатываемых каждой функции является размер пакета в полтора раза hello.</span><span class="sxs-lookup"><span data-stu-id="f5dca-176">Therefore hello maximum number of concurrent messages being processed per function is one and a half times hello batch size.</span></span> <span data-ttu-id="f5dca-177">Это ограничение применяется отдельно tooeach функции, которая имеет `QueueTrigger` атрибута.</span><span class="sxs-lookup"><span data-stu-id="f5dca-177">This limit applies separately tooeach function that has a `QueueTrigger` attribute.</span></span>

<span data-ttu-id="f5dca-178">Если вы не хотите параллельного выполнения для сообщений, полученных на одну очередь, можно задать размер too1 hello пакета.</span><span class="sxs-lookup"><span data-stu-id="f5dca-178">If you don't want parallel execution for messages received on one queue, you can set hello batch size too1.</span></span> <span data-ttu-id="f5dca-179">Ознакомьтесь также с подразделом **More control over Queue processing** (Больший контроль над обработкой очередей) в статье [Azure WebJobs SDK 1.1.0 RTM](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/) (Пакет SDK Azure для веб-заданий 1.1.0 RTM).</span><span class="sxs-lookup"><span data-stu-id="f5dca-179">See also **More control over Queue processing** in [Azure WebJobs SDK 1.1.0 RTM](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).</span></span>

### <span data-ttu-id="f5dca-180"><a id="queuemetadata"></a>Получение очереди или метаданных очереди сообщений</span><span class="sxs-lookup"><span data-stu-id="f5dca-180"><a id="queuemetadata"></a>Get queue or queue message metadata</span></span>
<span data-ttu-id="f5dca-181">Можно получить следующие свойства сообщения, добавив параметры сигнатуры метода toohello hello:</span><span class="sxs-lookup"><span data-stu-id="f5dca-181">You can get hello following message properties by adding parameters toohello method signature:</span></span>

* <span data-ttu-id="f5dca-182">`DateTimeOffset` expirationTime;</span><span class="sxs-lookup"><span data-stu-id="f5dca-182">`DateTimeOffset` expirationTime</span></span>
* <span data-ttu-id="f5dca-183">`DateTimeOffset` insertionTime;</span><span class="sxs-lookup"><span data-stu-id="f5dca-183">`DateTimeOffset` insertionTime</span></span>
* <span data-ttu-id="f5dca-184">`DateTimeOffset` nextVisibleTime;</span><span class="sxs-lookup"><span data-stu-id="f5dca-184">`DateTimeOffset` nextVisibleTime</span></span>
* <span data-ttu-id="f5dca-185">`string` queueTrigger (содержит текст сообщения);</span><span class="sxs-lookup"><span data-stu-id="f5dca-185">`string` queueTrigger (contains message text)</span></span>
* <span data-ttu-id="f5dca-186">`string` id;</span><span class="sxs-lookup"><span data-stu-id="f5dca-186">`string` id</span></span>
* <span data-ttu-id="f5dca-187">`string` popReceipt;</span><span class="sxs-lookup"><span data-stu-id="f5dca-187">`string` popReceipt</span></span>
* <span data-ttu-id="f5dca-188">`int` dequeueCount.</span><span class="sxs-lookup"><span data-stu-id="f5dca-188">`int` dequeueCount</span></span>

<span data-ttu-id="f5dca-189">Если требуется toowork непосредственно с hello хранилища Azure API, можно добавить `CloudStorageAccount` параметра.</span><span class="sxs-lookup"><span data-stu-id="f5dca-189">If you want toowork directly with hello Azure storage API, you can also add a `CloudStorageAccount` parameter.</span></span>

<span data-ttu-id="f5dca-190">Hello следующий пример записывает все журнал этого приложения tooan метаданных.</span><span class="sxs-lookup"><span data-stu-id="f5dca-190">hello following example writes all of this metadata tooan INFO application log.</span></span> <span data-ttu-id="f5dca-191">В примере hello logMessage и queueTrigger содержимым hello hello очереди сообщения.</span><span class="sxs-lookup"><span data-stu-id="f5dca-191">In hello example, both logMessage and queueTrigger contain hello content of hello queue message.</span></span>

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

<span data-ttu-id="f5dca-192">Ниже приведен пример журнала записываются в примере кода hello.</span><span class="sxs-lookup"><span data-stu-id="f5dca-192">Here is a sample log written by hello sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

### <span data-ttu-id="f5dca-193"><a id="graceful"></a>Нормальное завершение работы</span><span class="sxs-lookup"><span data-stu-id="f5dca-193"><a id="graceful"></a>Graceful shutdown</span></span>
<span data-ttu-id="f5dca-194">Функция, которая выполняется в непрерывных веб-задания может принимать `CancellationToken` параметр, который позволяет функции hello операционной системы toonotify hello при hello веб-задания — о toobe завершен.</span><span class="sxs-lookup"><span data-stu-id="f5dca-194">A function that runs in a continuous WebJob can accept a `CancellationToken` parameter which enables hello operating system toonotify hello function when hello WebJob is about toobe terminated.</span></span> <span data-ttu-id="f5dca-195">Можно использовать toomake это уведомление о том, что функции hello не привести к непредвиденному завершению способом, который оставляет данных в несогласованном состоянии.</span><span class="sxs-lookup"><span data-stu-id="f5dca-195">You can use this notification toomake sure hello function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="f5dca-196">Следующий пример показывает как Hello toocheck увольнения предстоящем веб-задания в функции.</span><span class="sxs-lookup"><span data-stu-id="f5dca-196">hello following example shows how toocheck for impending WebJob termination in a function.</span></span>

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

<span data-ttu-id="f5dca-197">**Примечание:** hello панели мониторинга может показывать правильно состояние hello и выходные данные функции, которые была завершена.</span><span class="sxs-lookup"><span data-stu-id="f5dca-197">**Note:** hello Dashboard might not correctly show hello status and output of functions that have been shut down.</span></span>

<span data-ttu-id="f5dca-198">Дополнительную информацию см. в статье [Нормальное завершение работы веб-заданий](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span><span class="sxs-lookup"><span data-stu-id="f5dca-198">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <span data-ttu-id="f5dca-199"><a id="createqueue"></a>Как toocreate очереди сообщений во время обработки сообщения в очереди</span><span class="sxs-lookup"><span data-stu-id="f5dca-199"><a id="createqueue"></a> How toocreate a queue message while processing a queue message</span></span>
<span data-ttu-id="f5dca-200">функция, которая создает новое сообщение очереди, используйте hello toowrite `Queue` атрибута.</span><span class="sxs-lookup"><span data-stu-id="f5dca-200">toowrite a function that creates a new queue message, use hello `Queue` attribute.</span></span> <span data-ttu-id="f5dca-201">Как `QueueTrigger`, передав имя очереди hello в виде строки, или вы можете [динамически задать имя очереди hello](#config).</span><span class="sxs-lookup"><span data-stu-id="f5dca-201">Like `QueueTrigger`, you pass in hello queue name as a string or you can [set hello queue name dynamically](#config).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="f5dca-202">Строковые сообщения очереди</span><span class="sxs-lookup"><span data-stu-id="f5dca-202">String queue messages</span></span>
<span data-ttu-id="f5dca-203">Следующий образец кода синхронные Hello создает новое сообщение очереди в очередь hello, с именем «outputqueue» с таким же содержимое, так как очередь приветственное сообщение получено в hello очереди с именем «inputqueue» hello.</span><span class="sxs-lookup"><span data-stu-id="f5dca-203">hello following non-async code sample creates a new queue message in hello queue named "outputqueue" with hello same content as hello queue message received in hello queue named "inputqueue".</span></span> <span data-ttu-id="f5dca-204">(Для асинхронных функций используйте `IAsyncCollector<T>` , следуя указаниям далее в этом разделе.)</span><span class="sxs-lookup"><span data-stu-id="f5dca-204">(For async functions use `IAsyncCollector<T>` as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="f5dca-205">Сообщения очереди [POCO](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)</span><span class="sxs-lookup"><span data-stu-id="f5dca-205">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="f5dca-206">toocreate очереди сообщение, содержащее POCO, а не строкой, pass hello POCO тип в качестве выходного параметра toohello `Queue` конструктор атрибута.</span><span class="sxs-lookup"><span data-stu-id="f5dca-206">toocreate a queue message that contains a POCO rather than a string, pass hello POCO type as an output parameter toohello `Queue` attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="f5dca-207">пакет SDK для Hello автоматически сериализует tooJSON hello объекта.</span><span class="sxs-lookup"><span data-stu-id="f5dca-207">hello SDK automatically serializes hello object tooJSON.</span></span> <span data-ttu-id="f5dca-208">Очередь сообщений создается всегда, даже если hello объекта имеет значение null.</span><span class="sxs-lookup"><span data-stu-id="f5dca-208">A queue message is always created, even if hello object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="f5dca-209">Создание нескольких сообщений или сообщений в асинхронных функциях</span><span class="sxs-lookup"><span data-stu-id="f5dca-209">Create multiple messages or in async functions</span></span>
<span data-ttu-id="f5dca-210">toocreate несколько сообщений сделать hello тип параметра для очереди вывода hello `ICollector<T>` или `IAsyncCollector<T>`, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="f5dca-210">toocreate multiple messages, make hello parameter type for hello output queue `ICollector<T>` or `IAsyncCollector<T>`, as shown in hello following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="f5dca-211">Каждое сообщение очереди создается сразу после hello `Add` вызывается метод.</span><span class="sxs-lookup"><span data-stu-id="f5dca-211">Each queue message is created immediately when hello `Add` method is called.</span></span>

### <a name="types-that-hello-queue-attribute-works-with"></a><span data-ttu-id="f5dca-212">Типы атрибута очереди hello работает с</span><span class="sxs-lookup"><span data-stu-id="f5dca-212">Types that hello Queue attribute works with</span></span>
<span data-ttu-id="f5dca-213">Можно использовать hello `Queue` атрибутов на следующие типы параметра hello:</span><span class="sxs-lookup"><span data-stu-id="f5dca-213">You can use hello `Queue` attribute on hello following parameter types:</span></span>

* <span data-ttu-id="f5dca-214">`out string`(если значение параметра не равно null, при завершении функции hello создает сообщения в очереди)</span><span class="sxs-lookup"><span data-stu-id="f5dca-214">`out string` (creates queue message if parameter value is non-null when hello function ends)</span></span>
* <span data-ttu-id="f5dca-215">`out byte[]` (действует как `string`);</span><span class="sxs-lookup"><span data-stu-id="f5dca-215">`out byte[]` (works like `string`)</span></span>
* <span data-ttu-id="f5dca-216">`out CloudQueueMessage` (действует как `string`);</span><span class="sxs-lookup"><span data-stu-id="f5dca-216">`out CloudQueueMessage` (works like `string`)</span></span>
* <span data-ttu-id="f5dca-217">`out POCO`(сериализуемый тип, создает сообщение с пустым объектом Если hello имеет значение null, при завершении функции hello)</span><span class="sxs-lookup"><span data-stu-id="f5dca-217">`out POCO` (a serializable type, creates a message with a null object if hello paramter is null when hello function ends)</span></span>
* `ICollector`
* `IAsyncCollector`
* <span data-ttu-id="f5dca-218">`CloudQueue`(для создания сообщений вручную с помощью API хранилища Azure hello непосредственно)</span><span class="sxs-lookup"><span data-stu-id="f5dca-218">`CloudQueue` (for creating messages manually using hello Azure Storage API directly)</span></span>

### <span data-ttu-id="f5dca-219"><a id="ibinder"></a>Использование пакета SDK веб-задания атрибутов в теле функции hello</span><span class="sxs-lookup"><span data-stu-id="f5dca-219"><a id="ibinder"></a>Use WebJobs SDK attributes in hello body of a function</span></span>
<span data-ttu-id="f5dca-220">Если вам требуется toodo некоторые работать в функции перед использованием атрибут SDK веб-заданий, таких как `Queue`, `Blob`, или `Table`, можно использовать hello `IBinder` интерфейса.</span><span class="sxs-lookup"><span data-stu-id="f5dca-220">If you need toodo some work in your function before using a WebJobs SDK attribute such as `Queue`, `Blob`, or `Table`, you can use hello `IBinder` interface.</span></span>

<span data-ttu-id="f5dca-221">Следующий пример Hello принимает сообщение входной очереди и создает новое сообщение с hello же содержимого, в очереди вывода.</span><span class="sxs-lookup"><span data-stu-id="f5dca-221">hello following example takes an input queue message and creates a new message with hello same content in an output queue.</span></span> <span data-ttu-id="f5dca-222">Имя очереди вывода Hello задается код в теле hello функции hello.</span><span class="sxs-lookup"><span data-stu-id="f5dca-222">hello output queue name is set by code in hello body of hello function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="f5dca-223">Hello `IBinder` интерфейс может также использоваться с hello `Table` и `Blob` атрибуты.</span><span class="sxs-lookup"><span data-stu-id="f5dca-223">hello `IBinder` interface can also be used with hello `Table` and `Blob` attributes.</span></span>

## <span data-ttu-id="f5dca-224"><a id="blobs"></a>Как tooread и записи больших двоичных объектов и таблиц во время обработки сообщения в очереди</span><span class="sxs-lookup"><span data-stu-id="f5dca-224"><a id="blobs"></a> How tooread and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="f5dca-225">Hello `Blob` и `Table` атрибуты позволяют tooread и записи больших двоичных объектов и таблиц.</span><span class="sxs-lookup"><span data-stu-id="f5dca-225">hello `Blob` and `Table` attributes enable you tooread and write blobs and tables.</span></span> <span data-ttu-id="f5dca-226">Hello образцы в этом разделе применяются tooblobs.</span><span class="sxs-lookup"><span data-stu-id="f5dca-226">hello samples in this section apply tooblobs.</span></span> <span data-ttu-id="f5dca-227">Примеры кода, которые показывают, как tootrigger обрабатывает при создании или обновлении больших двоичных объектов см. в разделе [как toouse Azure хранилище больших двоичных объектов с hello SDK веб-заданий](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)и примеры кода, которые считывают и записывают таблиц см. в разделе [как toouse таблицы Azure хранилище с hello SDK веб-задания](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="f5dca-227">For code samples that show how tootrigger processes when blobs are created or updated, see [How toouse Azure blob storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How toouse Azure table storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="f5dca-228">Сообщения очереди строк, которые запускают операции с большими двоичными объектами</span><span class="sxs-lookup"><span data-stu-id="f5dca-228">String queue messages triggering blob operations</span></span>
<span data-ttu-id="f5dca-229">Для очереди сообщение, содержащее строку `queueTrigger` — это, можно использовать в hello `Blob` атрибута `blobPath` параметра, который содержит содержимое приветственное сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="f5dca-229">For a queue message that contains a string, `queueTrigger` is a placeholder you can use in hello `Blob` attribute's `blobPath` parameter that contains hello contents of hello message.</span></span>

<span data-ttu-id="f5dca-230">Hello следующий пример использует `Stream` объектов tooread и записи больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="f5dca-230">hello following example uses `Stream` objects tooread and write blobs.</span></span> <span data-ttu-id="f5dca-231">приветственное сообщение очереди — hello имя BLOB-объектов, находящихся в контейнере textblobs hello.</span><span class="sxs-lookup"><span data-stu-id="f5dca-231">hello queue message is hello name of a blob located in hello textblobs container.</span></span> <span data-ttu-id="f5dca-232">Копия hello большой двоичный объект с «-новые» присоединенных toohello имя создается в hello же контейнер.</span><span class="sxs-lookup"><span data-stu-id="f5dca-232">A copy of hello blob with "-new" appended toohello name is created in hello same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="f5dca-233">Hello `Blob` атрибута конструктор принимает `blobPath` параметр, определяющий hello контейнера и имя большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="f5dca-233">hello `Blob` attribute constructor takes a `blobPath` parameter that specifies hello container and blob name.</span></span> <span data-ttu-id="f5dca-234">Дополнительные сведения об этом заполнитель см. в разделе [как toouse Azure хранилище больших двоичных объектов с hello SDK веб-заданий](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),</span><span class="sxs-lookup"><span data-stu-id="f5dca-234">For more information about this placeholder, see [How toouse Azure blob storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),</span></span>

<span data-ttu-id="f5dca-235">Если атрибут hello оформляет `Stream` другой конструктор указывает hello объекта `FileAccess` режим чтения, записи или чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="f5dca-235">When hello attribute decorates a `Stream` object, another constructor parameter specifies hello `FileAccess` mode as read, write, or read/write.</span></span>

<span data-ttu-id="f5dca-236">Hello следующий пример использует `CloudBlockBlob` объекта toodelete большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="f5dca-236">hello following example uses a `CloudBlockBlob` object toodelete a blob.</span></span> <span data-ttu-id="f5dca-237">приветственное сообщение очереди является именем hello hello большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="f5dca-237">hello queue message is hello name of hello blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <span data-ttu-id="f5dca-238"><a id="pocoblobs"></a> Сообщения очереди [POCO](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)</span><span class="sxs-lookup"><span data-stu-id="f5dca-238"><a id="pocoblobs"></a> POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="f5dca-239">Для POCO, хранятся в очереди сообщение hello как JSON, можно использовать местозаполнители, имя свойства объекта hello в hello `Queue` атрибута `blobPath` параметра.</span><span class="sxs-lookup"><span data-stu-id="f5dca-239">For a POCO stored as JSON in hello queue message, you can use placeholders that name properties of hello object in hello `Queue` attribute's `blobPath` parameter.</span></span> <span data-ttu-id="f5dca-240">Можно также использовать [имена свойства метаданных очереди](#queuemetadata) в качестве заполнителей.</span><span class="sxs-lookup"><span data-stu-id="f5dca-240">You can also use [queue metadata property names](#queuemetadata) as placeholders.</span></span>

<span data-ttu-id="f5dca-241">Hello следующий пример копирует BLOB-объектов tooa новый большой двоичный объект с другим расширением.</span><span class="sxs-lookup"><span data-stu-id="f5dca-241">hello following example copies a blob tooa new blob with a different extension.</span></span> <span data-ttu-id="f5dca-242">сообщение Hello очереди `BlobInformation` объект, который содержит `BlobName` и `BlobNameWithoutExtension` свойства.</span><span class="sxs-lookup"><span data-stu-id="f5dca-242">hello queue message is a `BlobInformation` object that includes `BlobName` and `BlobNameWithoutExtension` properties.</span></span> <span data-ttu-id="f5dca-243">имена свойств Hello используются в качестве меток-заполнителей в пути hello больших двоичных объектов для hello `Blob` атрибуты.</span><span class="sxs-lookup"><span data-stu-id="f5dca-243">hello property names are used as placeholders in hello blob path for hello `Blob` attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="f5dca-244">Hello SDK использует hello [пакет Newtonsoft.Json NuGet](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize и десериализации сообщений.</span><span class="sxs-lookup"><span data-stu-id="f5dca-244">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="f5dca-245">При создании очереди сообщений в программе, которая не использует hello SDK веб-задания, можно написать код, как следующий пример toocreate POCO очереди сообщений hello приветствия, можно провести синтаксический анализ пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="f5dca-245">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="f5dca-246">Если вам требуется toodo некоторые работают в функции перед привязкой tooan большой двоичный объект, можно использовать атрибут hello в тексте hello функции hello [как показано выше, для атрибута очереди hello](#ibinder).</span><span class="sxs-lookup"><span data-stu-id="f5dca-246">If you need toodo some work in your function before binding a blob tooan object, you can use hello attribute in hello body of hello function, [as shown earlier for hello Queue attribute](#ibinder).</span></span>

### <span data-ttu-id="f5dca-247"><a id="blobattributetypes"></a>Типы, которые можно использовать hello атрибута с BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="f5dca-247"><a id="blobattributetypes"></a> Types you can use hello Blob attribute with</span></span>
<span data-ttu-id="f5dca-248">Hello `Blob` атрибут может использоваться с hello следующие типы:</span><span class="sxs-lookup"><span data-stu-id="f5dca-248">hello `Blob` attribute can be used with hello following types:</span></span>

* <span data-ttu-id="f5dca-249">`Stream`(чтение или запись, указанный с помощью параметра конструктора hello FileAccess)</span><span class="sxs-lookup"><span data-stu-id="f5dca-249">`Stream` (read or write, specified by using hello FileAccess constructor parameter)</span></span>
* `TextReader`
* `TextWriter`
* <span data-ttu-id="f5dca-250">`string` (чтение);</span><span class="sxs-lookup"><span data-stu-id="f5dca-250">`string` (read)</span></span>
* <span data-ttu-id="f5dca-251">`out string`(записи; создает большой двоичный объект только в том случае, если параметр строки hello отлично от null, при возврате из функции hello)</span><span class="sxs-lookup"><span data-stu-id="f5dca-251">`out string` (write; creates a blob only if hello string parameter is non-null when hello function returns)</span></span>
* <span data-ttu-id="f5dca-252">POCO (чтение);</span><span class="sxs-lookup"><span data-stu-id="f5dca-252">POCO (read)</span></span>
* <span data-ttu-id="f5dca-253">out POCO (записи; всегда создает большой двоичный объект, создает как объект null, если параметр POCO имеет значение null, при возврате из функции hello)</span><span class="sxs-lookup"><span data-stu-id="f5dca-253">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when hello function returns)</span></span>
* <span data-ttu-id="f5dca-254">`CloudBlobStream` (запись);</span><span class="sxs-lookup"><span data-stu-id="f5dca-254">`CloudBlobStream` (write)</span></span>
* <span data-ttu-id="f5dca-255">`ICloudBlob` (чтение или запись);</span><span class="sxs-lookup"><span data-stu-id="f5dca-255">`ICloudBlob` (read or write)</span></span>
* <span data-ttu-id="f5dca-256">`CloudBlockBlob` (чтение или запись);</span><span class="sxs-lookup"><span data-stu-id="f5dca-256">`CloudBlockBlob` (read or write)</span></span>
* <span data-ttu-id="f5dca-257">`CloudPageBlob` (чтение или запись);</span><span class="sxs-lookup"><span data-stu-id="f5dca-257">`CloudPageBlob` (read or write)</span></span>

## <span data-ttu-id="f5dca-258"><a id="poison"></a>Как toohandle подозрительные сообщения</span><span class="sxs-lookup"><span data-stu-id="f5dca-258"><a id="poison"></a> How toohandle poison messages</span></span>
<span data-ttu-id="f5dca-259">Сообщения, содержимое которого приводит toofail функции называются *сообщения о сбое*.</span><span class="sxs-lookup"><span data-stu-id="f5dca-259">Messages whose content causes a function toofail are called *poison messages*.</span></span> <span data-ttu-id="f5dca-260">При сбое функции hello, очередь приветственное сообщение не удаляется и в конечном счете передается еще раз, может вызвать toobe hello цикл повторяется.</span><span class="sxs-lookup"><span data-stu-id="f5dca-260">When hello function fails, hello queue message is not deleted and eventually is picked up again, causing hello cycle toobe repeated.</span></span> <span data-ttu-id="f5dca-261">Hello SDK можно прервать цикл hello автоматически после ограниченного числа итераций, или это можно сделать вручную.</span><span class="sxs-lookup"><span data-stu-id="f5dca-261">hello SDK can automatically interrupt hello cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="f5dca-262">Автоматическая обработка сообщений</span><span class="sxs-lookup"><span data-stu-id="f5dca-262">Automatic poison message handling</span></span>
<span data-ttu-id="f5dca-263">Hello SDK будет вызвать функцию копирования tooprocess раз too5 сообщения в очереди.</span><span class="sxs-lookup"><span data-stu-id="f5dca-263">hello SDK will call a function up too5 times tooprocess a queue message.</span></span> <span data-ttu-id="f5dca-264">При сбое hello пятый try, приветственное сообщение — перемещенный tooa очереди подозрительных сообщений.</span><span class="sxs-lookup"><span data-stu-id="f5dca-264">If hello fifth try fails, hello message is moved tooa poison queue.</span></span> <span data-ttu-id="f5dca-265">[Максимальное число повторных попыток для Hello настраивается](#config).</span><span class="sxs-lookup"><span data-stu-id="f5dca-265">[hello maximum number of retries is configurable](#config).</span></span>

<span data-ttu-id="f5dca-266">очередь подозрительных сообщений Hello называется *{originalqueuename}*-подозрительное.</span><span class="sxs-lookup"><span data-stu-id="f5dca-266">hello poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="f5dca-267">Можно написать tooprocess функция сообщения из очереди подозрительных сообщений hello ее регистрации или отправка уведомления о необходимости ручного вмешательства.</span><span class="sxs-lookup"><span data-stu-id="f5dca-267">You can write a function tooprocess messages from hello poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="f5dca-268">В следующий пример hello hello `CopyBlob` функция завершится ошибкой, если сообщения в очереди содержит hello имя большого двоичного объекта, который не существует.</span><span class="sxs-lookup"><span data-stu-id="f5dca-268">In hello following example hello `CopyBlob` function will fail when a queue message contains hello name of a blob that doesn't exist.</span></span> <span data-ttu-id="f5dca-269">В этом случае приветственное сообщение перемещается из hello copyblobqueue очереди toohello copyblobqueue подозрительных очереди.</span><span class="sxs-lookup"><span data-stu-id="f5dca-269">When that happens, hello message is moved from hello copyblobqueue queue toohello copyblobqueue-poison queue.</span></span> <span data-ttu-id="f5dca-270">Hello `ProcessPoisonMessage` то подозрительное сообщение hello журналы.</span><span class="sxs-lookup"><span data-stu-id="f5dca-270">hello `ProcessPoisonMessage` then logs hello poison message.</span></span>

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

<span data-ttu-id="f5dca-271">Hello ниже показан вывод на консоль из этих функций при обработке подозрительных сообщений.</span><span class="sxs-lookup"><span data-stu-id="f5dca-271">hello following illustration shows console output from these functions when a poison message is processed.</span></span>

![Вывод консоли для обработки подозрительных сообщений](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="f5dca-273">Ручная обработка подозрительных сообщений</span><span class="sxs-lookup"><span data-stu-id="f5dca-273">Manual poison message handling</span></span>
<span data-ttu-id="f5dca-274">Hello количество обработки сообщения для обработки можно получить, добавив `int` параметр с именем `dequeueCount` tooyour функции.</span><span class="sxs-lookup"><span data-stu-id="f5dca-274">You can get hello number of times a message has been picked up for processing by adding an `int` parameter named `dequeueCount` tooyour function.</span></span> <span data-ttu-id="f5dca-275">После этого можно hello проверьте количество в коде функция вывода из очереди и выполнять собственные подозрительное сообщение обработки при hello число превышает пороговое значение, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="f5dca-275">You can then check hello dequeue count in function code and perform your own poison message handling when hello number exceeds a threshold, as shown in hello following example.</span></span>

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

## <span data-ttu-id="f5dca-276"><a id="config"></a>Как параметры конфигурации tooset</span><span class="sxs-lookup"><span data-stu-id="f5dca-276"><a id="config"></a> How tooset configuration options</span></span>
<span data-ttu-id="f5dca-277">Можно использовать hello `JobHostConfiguration` hello tooset тип следующие параметры конфигурации:</span><span class="sxs-lookup"><span data-stu-id="f5dca-277">You can use hello `JobHostConfiguration` type tooset hello following configuration options:</span></span>

* <span data-ttu-id="f5dca-278">Задать строки подключения пакета SDK для hello в коде.</span><span class="sxs-lookup"><span data-stu-id="f5dca-278">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="f5dca-279">Настройка таких параметров атрибута `QueueTrigger` , как максимальное значение счетчика вывода из очереди.</span><span class="sxs-lookup"><span data-stu-id="f5dca-279">Configure `QueueTrigger` settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="f5dca-280">Получение имен очередей из конфигурации</span><span class="sxs-lookup"><span data-stu-id="f5dca-280">Get queue names from configuration.</span></span>

### <span data-ttu-id="f5dca-281"><a id="setconnstr"></a>Установка строк подключения пакета SDK в коде</span><span class="sxs-lookup"><span data-stu-id="f5dca-281"><a id="setconnstr"></a>Set SDK connection strings in code</span></span>
<span data-ttu-id="f5dca-282">Задание строк подключения пакета SDK для hello в коде позволяет вы toouse собственные имена строку соединения в файлах конфигурации или переменные среды, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="f5dca-282">Setting hello SDK connection strings in code enables you toouse your own connection string names in configuration files or environment variables, as shown in hello following example.</span></span>

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

### <span data-ttu-id="f5dca-283"><a id="configqueue"></a>Настройка параметров атрибута QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="f5dca-283"><a id="configqueue"></a>Configure QueueTrigger  settings</span></span>
<span data-ttu-id="f5dca-284">Можно настроить следующие параметры, которые применяются для обработки сообщений в очереди toohello hello.</span><span class="sxs-lookup"><span data-stu-id="f5dca-284">You can configure hello following settings that apply toohello queue message processing:</span></span>

* <span data-ttu-id="f5dca-285">Здравствуйте, максимальное количество сообщений, которые извлекаются одновременно toobe параллельного выполнения (по умолчанию — 16).</span><span class="sxs-lookup"><span data-stu-id="f5dca-285">hello maximum number of queue messages that are picked up simultaneously toobe executed in parallel (default is 16).</span></span>
* <span data-ttu-id="f5dca-286">Здравствуйте, максимальное число повторных попыток перед отправкой сообщения в очереди tooa очереди подозрительных сообщений (по умолчанию — 5).</span><span class="sxs-lookup"><span data-stu-id="f5dca-286">hello maximum number of retries before a queue message is sent tooa poison queue (default is 5).</span></span>
* <span data-ttu-id="f5dca-287">Hello максимальное время ожидания перед запросом еще раз, когда очередь пуста (по умолчанию — 1 минута).</span><span class="sxs-lookup"><span data-stu-id="f5dca-287">hello maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="f5dca-288">Следующий пример показывает как Hello tooconfigure эти параметры:</span><span class="sxs-lookup"><span data-stu-id="f5dca-288">hello following example shows how tooconfigure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <span data-ttu-id="f5dca-289"><a id="setnamesincode"></a>Установка значений параметров конструктора пакета SDK для веб-заданий в коде</span><span class="sxs-lookup"><span data-stu-id="f5dca-289"><a id="setnamesincode"></a>Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="f5dca-290">Иногда требуется toospecify имя очереди, имя BLOB-объекта или контейнера, или имя таблицы, в коде, вместо жестко его.</span><span class="sxs-lookup"><span data-stu-id="f5dca-290">Sometimes you want toospecify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="f5dca-291">Например, может потребоваться имя очереди hello toospecify для `QueueTrigger` в переменной среде или файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f5dca-291">For example, you might want toospecify hello queue name for `QueueTrigger` in a configuration file or environment variable.</span></span>

<span data-ttu-id="f5dca-292">Это можно сделать путем передачи `NameResolver` объекта toohello `JobHostConfiguration` типа.</span><span class="sxs-lookup"><span data-stu-id="f5dca-292">You can do that by passing in a `NameResolver` object toohello `JobHostConfiguration` type.</span></span> <span data-ttu-id="f5dca-293">Включает специальные заполнители, заключенная в символы процента (%) в конструктор атрибута SDK веб-задания параметров и `NameResolver` кода задается toobe hello фактические значения, используемые вместо эти заполнители.</span><span class="sxs-lookup"><span data-stu-id="f5dca-293">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your `NameResolver` code specifies hello actual values toobe used in place of those placeholders.</span></span>

<span data-ttu-id="f5dca-294">Например предположим, что нужно toouse очереди с именем, logqueuetest в тестовой среде hello и один именованный logqueueprod в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="f5dca-294">For example, suppose you want toouse a queue named logqueuetest in hello test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="f5dca-295">Вместо жестко очереди, необходимо, чтобы имя hello toospecify записи в hello `appSettings` коллекцию, которая будет иметь имя фактического очереди hello.</span><span class="sxs-lookup"><span data-stu-id="f5dca-295">Instead of a hard-coded queue name, you want toospecify hello name of an entry in hello `appSettings` collection that would have hello actual queue name.</span></span> <span data-ttu-id="f5dca-296">Если hello `appSettings` ключа является logqueue, функция может выглядеть следующим образом hello в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="f5dca-296">If hello `appSettings` key is logqueue, your function could look like hello following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="f5dca-297">Ваш `NameResolver` класс затем удалось получить имя очереди hello из `appSettings` как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="f5dca-297">Your `NameResolver` class could then get hello queue name from `appSettings` as shown in hello following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="f5dca-298">Передайте hello `NameResolver` класса в toohello `JobHost` объекта, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="f5dca-298">You pass hello `NameResolver` class in toohello `JobHost` object as shown in hello following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="f5dca-299">**Примечание:** очередей, таблиц и имена больших двоичных объектов не будут разрешены при каждом вызове функции, но имена контейнеров больших двоичных объектов разрешаются только при запуске приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f5dca-299">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when hello application starts.</span></span> <span data-ttu-id="f5dca-300">Невозможно изменить имя контейнера больших двоичных объектов, пока выполняется задание hello.</span><span class="sxs-lookup"><span data-stu-id="f5dca-300">You can't change blob container name while hello job is running.</span></span>

## <span data-ttu-id="f5dca-301"><a id="manual"></a>Как tootrigger функции вручную</span><span class="sxs-lookup"><span data-stu-id="f5dca-301"><a id="manual"></a>How tootrigger a function manually</span></span>
<span data-ttu-id="f5dca-302">tootrigger функцию вручную, используйте hello `Call` или `CallAsync` метод hello `JobHost` объекта и hello `NoAutomaticTrigger` атрибут функции hello, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="f5dca-302">tootrigger a function manually, use hello `Call` or `CallAsync` method on hello `JobHost` object and hello `NoAutomaticTrigger` attribute on hello function, as shown in hello following example.</span></span>

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

## <span data-ttu-id="f5dca-303"><a id="logs"></a>Каким образом ведет журнал toowrite</span><span class="sxs-lookup"><span data-stu-id="f5dca-303"><a id="logs"></a>How toowrite logs</span></span>
<span data-ttu-id="f5dca-304">Hello панели мониторинга показывает журналы в двух местах: hello hello веб-задания и странице приветствия для конкретного вызова веб-задания.</span><span class="sxs-lookup"><span data-stu-id="f5dca-304">hello Dashboard shows logs in two places: hello page for hello WebJob, and hello page for a particular WebJob invocation.</span></span>

![Журналы на странице задания WebJob](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

![Журналы на странице вызова функций](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

<span data-ttu-id="f5dca-307">Выходные данные консоли методы, вызываемые в функции или hello `Main()` метод отображается в странице панели мониторинга hello hello веб-задания, а не в страницу приветствия для вызова определенного метода.</span><span class="sxs-lookup"><span data-stu-id="f5dca-307">Output from Console methods that you call in a function or in hello `Main()` method appears in hello Dashboard page for hello WebJob, not in hello page for a particular method invocation.</span></span> <span data-ttu-id="f5dca-308">Выходные данные из объекта TextWriter hello, которое получается из параметра в подписи метода отображается на странице панели мониторинга hello для вызова метода.</span><span class="sxs-lookup"><span data-stu-id="f5dca-308">Output from hello TextWriter object that you get from a parameter in your method signature appears in hello Dashboard page for a method invocation.</span></span>

<span data-ttu-id="f5dca-309">Вывод на консоль не может быть вызова определенного метода связанного tooa, поскольку hello консоли является однопоточным, хотя многие функции задания, запущенные на hello то же время.</span><span class="sxs-lookup"><span data-stu-id="f5dca-309">Console output can't be linked tooa particular method invocation because hello Console is single-threaded, while many job functions may be running at hello same time.</span></span> <span data-ttu-id="f5dca-310">Вот почему hello SDK предоставляет каждый вызов функции с свой собственный уникальный журнал объект модуля записи.</span><span class="sxs-lookup"><span data-stu-id="f5dca-310">That's why hello  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="f5dca-311">toowrite [журналы трассировки приложения](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), используйте `Console.Out` (создает журналы, которые помечены как информация) и `Console.Error` (создает журналы, которые помечены как ошибки).</span><span class="sxs-lookup"><span data-stu-id="f5dca-311">toowrite [application tracing logs](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use `Console.Out` (creates logs marked as INFO) and `Console.Error` (creates logs marked as ERROR).</span></span> <span data-ttu-id="f5dca-312">Альтернативным вариантом является toouse [трассировки или TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), который предоставляет подробные сведения, предупреждение, и критическое уровни tooInfo сложения и ошибки.</span><span class="sxs-lookup"><span data-stu-id="f5dca-312">An alternative is toouse [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition tooInfo and Error.</span></span> <span data-ttu-id="f5dca-313">Журналы трассировки приложения отображаются в файлах журналов приложения web hello, таблицы Azure или больших двоичных объектов Azure в зависимости от того, как настроить Azure веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="f5dca-313">Application tracing logs appear in hello web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="f5dca-314">Имеет значение true, если все вывода на консоль, самых последних журналов 100 приложения hello также отображаются в странице панели мониторинга hello hello веб-задания, не странице приветствия для вызова функции.</span><span class="sxs-lookup"><span data-stu-id="f5dca-314">As is true of all Console output, hello most recent 100 application logs also appear in hello Dashboard page for hello WebJob, not hello page for a function invocation.</span></span>

<span data-ttu-id="f5dca-315">Вывод на консоль будет hello панели мониторинга только в том случае, если программа hello выполняется в веб-задания Azure, не в том случае, если программа hello выполняется локально или в некоторых других условиях.</span><span class="sxs-lookup"><span data-stu-id="f5dca-315">Console output appears in hello Dashboard only if hello program is running in an Azure WebJob, not if hello program is running locally or in some other environment.</span></span>

<span data-ttu-id="f5dca-316">Отключите ведение журнала панели мониторинга для сценариев с высокой пропускной способностью.</span><span class="sxs-lookup"><span data-stu-id="f5dca-316">Disable dashboard logging for high throughput scenarios.</span></span> <span data-ttu-id="f5dca-317">По умолчанию hello SDK записывает журналы toostorage, и это действие может привести к снижению производительности при обработке большого числа сообщений.</span><span class="sxs-lookup"><span data-stu-id="f5dca-317">By default, hello SDK writes logs toostorage, and this activity could degrade performance when you are processing many messages.</span></span> <span data-ttu-id="f5dca-318">toodisable ведения журнала, задайте соединение строку hello мониторинга toonull, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="f5dca-318">toodisable logging, set hello dashboard connection string toonull as shown in hello following example.</span></span>

        JobHostConfiguration config = new JobHostConfiguration();       
        config.DashboardConnectionString = "";        
        JobHost host = new JobHost(config);
        host.RunAndBlock();

<span data-ttu-id="f5dca-319">Hello следующем примере показано несколько способов toowrite журналы:</span><span class="sxs-lookup"><span data-stu-id="f5dca-319">hello following example shows several ways toowrite logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="f5dca-320">Здравствуйте, выходные данные hello в hello мониторинга SDK веб-заданий, `TextWriter` объектов появляется при открытии страницы toohello для какого-либо вызов функции и нажмите кнопку **переключить вывод**:</span><span class="sxs-lookup"><span data-stu-id="f5dca-320">In hello WebJobs SDK Dashboard, hello output from hello `TextWriter` object shows up when you go toohello page for a particular function invocation and click **Toggle Output**:</span></span>

![Щелкнуть ссылку вызова функции](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardinvocations.png)

![Журналы на странице вызова функций](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

<span data-ttu-id="f5dca-323">В hello мониторинга SDK веб-заданий, hello последние 100 строк консоли вывода Показать вверх, если переход на страницу toohello для hello веб-задания (не для вызова функций hello) и нажмите кнопку **переключить вывод**.</span><span class="sxs-lookup"><span data-stu-id="f5dca-323">In hello WebJobs SDK Dashboard, hello most recent 100 lines of Console output show up when you go toohello page for hello WebJob (not for hello function invocation) and click **Toggle Output**.</span></span>

![Нажать кнопку «Переключить вывод»](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

<span data-ttu-id="f5dca-325">В непрерывное веб-задание, журнал приложений отображаются в/данных/задания и непрерывной/*{webjobname}*/job_log.txt в hello web app файловой системы.</span><span class="sxs-lookup"><span data-stu-id="f5dca-325">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in hello web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="f5dca-326">В приложении hello BLOB-объектов Azure журналы будут выглядеть следующим образом: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Здравствуй, мир!, 2014-09-26T21:01:13 ошибки, contosoadsnew, 491e54, 635473620738373502,0,17404,19,Console.Error - Здравствуй, мир!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Здравствуй, мир!,</span><span class="sxs-lookup"><span data-stu-id="f5dca-326">In an Azure blob hello application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="f5dca-327">И в таблице Azure hello `Console.Out` и `Console.Error` журналы выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f5dca-327">And in an Azure table hello `Console.Out` and `Console.Error` logs look like this:</span></span>

![Журнал Info в таблице](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableinfo.png)

![Журнал Error в таблице](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableerror.png)

<span data-ttu-id="f5dca-330">Если требуется tooplug в собственные средства ведения журнала, см. раздел [в этом примере](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="f5dca-330">If you want tooplug in your own logger, see [this example](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).</span></span>

## <span data-ttu-id="f5dca-331"><a id="errors"></a>Как toohandle ошибки и настроить время ожидания</span><span class="sxs-lookup"><span data-stu-id="f5dca-331"><a id="errors"></a>How toohandle errors and configure timeouts</span></span>
<span data-ttu-id="f5dca-332">Hello веб-заданий SDK также включает [время ожидания](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) атрибут, который можно использовать toocause toobe функция отменен, если не завершилось в течение указанного промежутка времени.</span><span class="sxs-lookup"><span data-stu-id="f5dca-332">hello WebJobs SDK also includes a [Timeout](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) attribute that you can use toocause a function toobe canceled if doesn't complete within a specified amount of time.</span></span> <span data-ttu-id="f5dca-333">Если требуется tooraise оповещение, когда происходит слишком много ошибок в течение указанного периода времени, можно использовать hello `ErrorTrigger` атрибута.</span><span class="sxs-lookup"><span data-stu-id="f5dca-333">And if you want tooraise an alert when too many errors happen within a specified period of time, you can use hello `ErrorTrigger` attribute.</span></span> <span data-ttu-id="f5dca-334">Вот [пример ErrorTrigger](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).</span><span class="sxs-lookup"><span data-stu-id="f5dca-334">Here is an [ErrorTrigger example](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).</span></span>

```
public static void ErrorMonitor(
[ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
[SendGrid(
    too= "admin@emailaddress.com",
    Subject = "Error!")]
 SendGridMessage message)
{
    // log last 5 detailed errors toohello Dashboard
   log.WriteLine(filter.GetDetailedMessage(5));
   message.Text = filter.GetDetailedMessage(1);
}
```

<span data-ttu-id="f5dca-335">Можно также динамически отключить и включить функции toocontrol ли они можно запустить, используя параметр конфигурации, который может быть параметра приложения или имя переменной среды.</span><span class="sxs-lookup"><span data-stu-id="f5dca-335">You can also dynamically disable and enable functions toocontrol whether they can be triggered, by using a configuration switch that could be an app setting or environment variable name.</span></span> <span data-ttu-id="f5dca-336">Пример кода, в разделе hello `Disable` атрибута в [hello SDK веб-заданий образцы репозитория](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).</span><span class="sxs-lookup"><span data-stu-id="f5dca-336">For sample code, see hello `Disable` attribute in [hello WebJobs SDK samples repository](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).</span></span>

## <span data-ttu-id="f5dca-337"><a id="nextsteps"></a> Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f5dca-337"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="f5dca-338">В этом руководстве предоставила код образцы где показано, как toohandle распространенные сценарии для работы с очередями Azure.</span><span class="sxs-lookup"><span data-stu-id="f5dca-338">This guide has provided code samples that show how toohandle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="f5dca-339">Дополнительные сведения о статье toouse веб-заданий Azure и hello SDK веб-заданий [рекомендуется заданиям Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="f5dca-339">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>
