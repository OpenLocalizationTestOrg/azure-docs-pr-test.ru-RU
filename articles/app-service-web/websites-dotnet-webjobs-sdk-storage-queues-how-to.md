---
title: "Использование пакета SDK веб-заданий для работы с хранилищем очередей Azure"
description: "Информация об использовании хранилища очередей Azure с пакетом SDK для WebJob Создание и удаление очередей; вставка, обзор, получение и удаление сообщений очереди, а также многое другое."
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
ms.openlocfilehash: 63b987a2c9471f2929b8d2dd605323910d2ad43b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-queue-storage-with-the-webjobs-sdk"></a><span data-ttu-id="44801-104">Использование пакета SDK веб-заданий для работы с хранилищем очередей Azure</span><span class="sxs-lookup"><span data-stu-id="44801-104">How to use Azure queue storage with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="44801-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="44801-105">Overview</span></span>
<span data-ttu-id="44801-106">Это руководство содержит примеры кода C#, в которых показано, как использовать пакет SDK для заданий Azure WebJob версии 1 и более поздней версии со службой хранения очередей Azure.</span><span class="sxs-lookup"><span data-stu-id="44801-106">This guide provides C# code samples that show how to use the Azure WebJobs SDK version 1.x with the Azure queue storage service.</span></span>

<span data-ttu-id="44801-107">В этом руководстве предполагается, что вы уже знаете, [как создать проект веб-задания в Visual Studio со строками подключения, указывающими на вашу учетную запись хранения](websites-dotnet-webjobs-sdk-get-started.md) или [несколько учетных записей хранения](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="44801-107">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md) or to [multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="44801-108">В большинстве фрагментов кода показаны только функции, а не код, создающий объект `JobHost` , как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="44801-108">Most of the code snippets only show functions, not the code that creates the `JobHost` object as in this example:</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

<span data-ttu-id="44801-109">Руководство включает в себя следующие разделы:</span><span class="sxs-lookup"><span data-stu-id="44801-109">The guide includes the following topics:</span></span>

* [<span data-ttu-id="44801-110">Как вызвать функцию при получении сообщения очереди</span><span class="sxs-lookup"><span data-stu-id="44801-110">How to trigger a function when a queue message is received</span></span>](#trigger)
  * <span data-ttu-id="44801-111">Строковые сообщения очереди</span><span class="sxs-lookup"><span data-stu-id="44801-111">String queue messages</span></span>
  * <span data-ttu-id="44801-112">Сообщения очереди POCO</span><span class="sxs-lookup"><span data-stu-id="44801-112">POCO queue messages</span></span>
  * <span data-ttu-id="44801-113">Асинхронные функции</span><span class="sxs-lookup"><span data-stu-id="44801-113">Async functions</span></span>
  * <span data-ttu-id="44801-114">Типы, с которыми используется атрибут QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="44801-114">Types the QueueTrigger attribute works with</span></span>
  * <span data-ttu-id="44801-115">Алгоритм опроса</span><span class="sxs-lookup"><span data-stu-id="44801-115">Polling algorithm</span></span>
  * <span data-ttu-id="44801-116">Выполнение на нескольких экземплярах</span><span class="sxs-lookup"><span data-stu-id="44801-116">Multiple instances</span></span>
  * <span data-ttu-id="44801-117">Параллельное выполнение</span><span class="sxs-lookup"><span data-stu-id="44801-117">Parallel execution</span></span>
  * <span data-ttu-id="44801-118">Получение очереди или метаданных очереди сообщений</span><span class="sxs-lookup"><span data-stu-id="44801-118">Get queue or queue message metadata</span></span>
  * <span data-ttu-id="44801-119">Корректное завершение работы</span><span class="sxs-lookup"><span data-stu-id="44801-119">Graceful shutdown</span></span>
* [<span data-ttu-id="44801-120">Как создать сообщение очереди во время обработки сообщения очереди</span><span class="sxs-lookup"><span data-stu-id="44801-120">How to create a queue message while processing a queue message</span></span>](#createqueue)
  * <span data-ttu-id="44801-121">Строковые сообщения очереди</span><span class="sxs-lookup"><span data-stu-id="44801-121">String queue messages</span></span>
  * <span data-ttu-id="44801-122">Сообщения очереди POCO</span><span class="sxs-lookup"><span data-stu-id="44801-122">POCO queue messages</span></span>
  * <span data-ttu-id="44801-123">Создание нескольких сообщений или сообщений в асинхронных функциях</span><span class="sxs-lookup"><span data-stu-id="44801-123">Create multiple messages or in async functions</span></span>
  * <span data-ttu-id="44801-124">Типы, с которыми используется атрибут Queue</span><span class="sxs-lookup"><span data-stu-id="44801-124">Types the Queue attribute works with</span></span>
  * <span data-ttu-id="44801-125">Использование атрибутов пакета SDK для заданий WebJob очереди в теле функции</span><span class="sxs-lookup"><span data-stu-id="44801-125">Use WebJobs SDK attributes in the body of a function</span></span>
* [<span data-ttu-id="44801-126">Как выполнить чтение и запись больших двоичных объектов во время обработки сообщения очереди</span><span class="sxs-lookup"><span data-stu-id="44801-126">How to read and write blobs while processing a queue message</span></span>](#blobs)
  * <span data-ttu-id="44801-127">Строковые сообщения очереди</span><span class="sxs-lookup"><span data-stu-id="44801-127">String queue messages</span></span>
  * <span data-ttu-id="44801-128">Сообщения очереди POCO</span><span class="sxs-lookup"><span data-stu-id="44801-128">POCO queue messages</span></span>
  * <span data-ttu-id="44801-129">Типы, с которыми используется атрибут Blob</span><span class="sxs-lookup"><span data-stu-id="44801-129">Types the Blob attribute works with</span></span>
* [<span data-ttu-id="44801-130">Как обработать подозрительные сообщения</span><span class="sxs-lookup"><span data-stu-id="44801-130">How to handle poison messages</span></span>](#poison)
  * <span data-ttu-id="44801-131">Автоматическая обработка сообщений</span><span class="sxs-lookup"><span data-stu-id="44801-131">Automatic poison message handling</span></span>
  * <span data-ttu-id="44801-132">Ручная обработка подозрительных сообщений</span><span class="sxs-lookup"><span data-stu-id="44801-132">Manual poison message handling</span></span>
* [<span data-ttu-id="44801-133">Как установить параметры конфигурации</span><span class="sxs-lookup"><span data-stu-id="44801-133">How to set configuration options</span></span>](#config)
  * <span data-ttu-id="44801-134">Установка строк подключения пакета SDK в коде</span><span class="sxs-lookup"><span data-stu-id="44801-134">Set SDK connection strings in code</span></span>
  * <span data-ttu-id="44801-135">Настройка параметров атрибута QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="44801-135">Configure QueueTrigger settings</span></span>
  * <span data-ttu-id="44801-136">Установка значений параметров конструктора пакета SDK для заданий WebJob в коде</span><span class="sxs-lookup"><span data-stu-id="44801-136">Set values for WebJobs SDK constructor parameters in code</span></span>
* [<span data-ttu-id="44801-137">Как вызвать функцию вручную</span><span class="sxs-lookup"><span data-stu-id="44801-137">How to trigger a function manually</span></span>](#manual)
* [<span data-ttu-id="44801-138">Как записать журналы</span><span class="sxs-lookup"><span data-stu-id="44801-138">How to write logs</span></span>](#logs)
* [<span data-ttu-id="44801-139">Как обрабатывать ошибки и как настроить время ожидания</span><span class="sxs-lookup"><span data-stu-id="44801-139">How to handle errors and configure timeouts</span></span>](#errors)
* [<span data-ttu-id="44801-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="44801-140">Next steps</span></span>](#nextsteps)

## <span data-ttu-id="44801-141"><a id="trigger"></a> Как вызвать функцию при получении сообщения очереди</span><span class="sxs-lookup"><span data-stu-id="44801-141"><a id="trigger"></a> How to trigger a function when a queue message is received</span></span>
<span data-ttu-id="44801-142">Чтобы написать функцию, которую пакет SDK для веб-заданий будет вызывать при получении сообщения очереди, используйте атрибут `QueueTrigger` .</span><span class="sxs-lookup"><span data-stu-id="44801-142">To write a function that the WebJobs SDK calls when a queue message is received, use the `QueueTrigger` attribute.</span></span> <span data-ttu-id="44801-143">Конструктор атрибута принимает строковый параметр, который указывает имя очереди для опроса.</span><span class="sxs-lookup"><span data-stu-id="44801-143">The attribute constructor takes a string parameter that specifies the name of the queue to poll.</span></span> <span data-ttu-id="44801-144">Также можно [задать имя очереди динамически](#config).</span><span class="sxs-lookup"><span data-stu-id="44801-144">You can also [set the queue name dynamically](#config).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="44801-145">Строковые сообщения очереди</span><span class="sxs-lookup"><span data-stu-id="44801-145">String queue messages</span></span>
<span data-ttu-id="44801-146">В следующем примере очередь содержит строковое сообщение, поэтому `QueueTrigger` применяется к строковому параметру с именем `logMessage`, в котором находится содержимое сообщения очереди.</span><span class="sxs-lookup"><span data-stu-id="44801-146">In the following example, the queue contains a string message, so `QueueTrigger` is applied to a string parameter named `logMessage` which contains the content of the queue message.</span></span> <span data-ttu-id="44801-147">Функция [записывает сообщение журнала на панель мониторинга](#logs).</span><span class="sxs-lookup"><span data-stu-id="44801-147">The function [writes a log message to the Dashboard](#logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="44801-148">Помимо значения `string` возможными значениями этого параметра являются массив байтов, объект `CloudQueueMessage` или заданный вами объект POCO.</span><span class="sxs-lookup"><span data-stu-id="44801-148">Besides `string`, the parameter may be a byte array, a `CloudQueueMessage` object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="44801-149">Сообщения очереди [POCO](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)</span><span class="sxs-lookup"><span data-stu-id="44801-149">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="44801-150">В следующем примере сообщения очереди содержат JSON для объекта `BlobInformation`, у которого есть свойство `BlobName`.</span><span class="sxs-lookup"><span data-stu-id="44801-150">In the following example, the queue message contains JSON for a `BlobInformation` object which includes a `BlobName` property.</span></span> <span data-ttu-id="44801-151">Пакет SDK автоматически выполняет десериализацию объекта.</span><span class="sxs-lookup"><span data-stu-id="44801-151">The SDK automatically deserializes the object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers to blob: " + blobInfo.BlobName);
        }

<span data-ttu-id="44801-152">Для сериализации и десериализации сообщений в пакете SDK используется [пакет NuGet Newtonsoft.Json](http://www.nuget.org/packages/Newtonsoft.Json) .</span><span class="sxs-lookup"><span data-stu-id="44801-152">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="44801-153">В случае создания сообщений очереди с помощью программы, которая не использует пакет SDK для заданий WebJob, чтобы создать сообщение очереди POCO, которое сможет проанализировать такой пакет, вы можете написать код по следующему образцу.</span><span class="sxs-lookup"><span data-stu-id="44801-153">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="44801-154">Асинхронные функции</span><span class="sxs-lookup"><span data-stu-id="44801-154">Async functions</span></span>
<span data-ttu-id="44801-155">Следующая асинхронная функция [записывает журнал на панель мониторинга](#logs).</span><span class="sxs-lookup"><span data-stu-id="44801-155">The following async function [writes a log to the Dashboard](#logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="44801-156">Асинхронные функции могут принимать [маркер отмены](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), как показано в следующем примере, который копирует большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="44801-156">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in the following example which copies a blob.</span></span> <span data-ttu-id="44801-157">(Описание заполнителя `queueTrigger` представлено в разделе [Большие двоичные объекты](#blobs).)</span><span class="sxs-lookup"><span data-stu-id="44801-157">(For an explanation of the `queueTrigger` placeholder, see the [Blobs](#blobs) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

### <span data-ttu-id="44801-158"><a id="qtattributetypes"></a> Типы, с которыми используется атрибут QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="44801-158"><a id="qtattributetypes"></a> Types the QueueTrigger attribute works with</span></span>
<span data-ttu-id="44801-159">Вы можете использовать `QueueTrigger` со следующими типами:</span><span class="sxs-lookup"><span data-stu-id="44801-159">You can use `QueueTrigger` with the following types:</span></span>

* `string`
* <span data-ttu-id="44801-160">тип POCO, сериализованный как JSON;</span><span class="sxs-lookup"><span data-stu-id="44801-160">A POCO type serialized as JSON</span></span>
* `byte[]`
* `CloudQueueMessage`

### <span data-ttu-id="44801-161"><a id="polling"></a> Алгоритм опроса</span><span class="sxs-lookup"><span data-stu-id="44801-161"><a id="polling"></a> Polling algorithm</span></span>
<span data-ttu-id="44801-162">В пакете SDK реализован алгоритм случайной экспоненциальной отсрочки, который позволяет уменьшить влияние опроса очереди ожидающих задач на затраты на транзакции хранилища.</span><span class="sxs-lookup"><span data-stu-id="44801-162">The SDK implements a random exponential back-off algorithm to reduce the effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="44801-163">При обнаружении сообщения пакет SDK ожидает в течение двух секунд и затем проверяет, не поступило ли еще одно сообщение; если сообщение не найдено, он ожидает около четырех секунд перед повторной попыткой.</span><span class="sxs-lookup"><span data-stu-id="44801-163">When a message is found, the SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="44801-164">После последующих неудачных попыток получения сообщения очереди время ожидания продолжает увеличиваться, пока не достигнет максимального времени ожидания, по умолчанию — одна минута.</span><span class="sxs-lookup"><span data-stu-id="44801-164">After subsequent failed attempts to get a queue message, the wait time continues to increase until it reaches the maximum wait time, which defaults to one minute.</span></span> <span data-ttu-id="44801-165">[Можно настроить максимальное время ожидания](#config).</span><span class="sxs-lookup"><span data-stu-id="44801-165">[The maximum wait time is configurable](#config).</span></span>

### <span data-ttu-id="44801-166"><a id="instances"></a> Выполнение на нескольких экземплярах</span><span class="sxs-lookup"><span data-stu-id="44801-166"><a id="instances"></a> Multiple instances</span></span>
<span data-ttu-id="44801-167">Если ваше веб-приложение работает на нескольких экземплярах, веб-задания непрерывно выполняются на каждом компьютере, и каждый компьютер будет ожидать триггеры и пытаться запустить функции.</span><span class="sxs-lookup"><span data-stu-id="44801-167">If your web app runs on multiple instances, a continuous WebJob runs on each machine, and each machine will wait for triggers and attempt to run functions.</span></span> <span data-ttu-id="44801-168">Очередь триггера пакета SDK веб-заданий автоматически предотвращает многократную обработку функцией сообщения из очереди. Не обязательно создавать идемпотентные функции.</span><span class="sxs-lookup"><span data-stu-id="44801-168">The WebJobs SDK queue trigger automatically prevents a function from processing a queue message multiple times; functions do not have to be written to be idempotent.</span></span> <span data-ttu-id="44801-169">Тем не менее, если вы хотите, чтобы выполнялся только один экземпляр функции, даже если существует несколько экземпляров несущего веб-приложения, можно использовать атрибут `Singleton`.</span><span class="sxs-lookup"><span data-stu-id="44801-169">However, if you want to ensure that only one instance of a function runs even when there are multiple instances of the host web app, you can use the `Singleton` attribute.</span></span>

### <span data-ttu-id="44801-170"><a id="parallel"></a> Параллельное выполнение</span><span class="sxs-lookup"><span data-stu-id="44801-170"><a id="parallel"></a> Parallel execution</span></span>
<span data-ttu-id="44801-171">Если имеется несколько функций, которые прослушивают различные очереди, при одновременном получении сообщений пакет SDK будет вызывать их параллельно.</span><span class="sxs-lookup"><span data-stu-id="44801-171">If you have multiple functions listening on different queues, the SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="44801-172">То же самое происходит при получении нескольких сообщений для одной очереди.</span><span class="sxs-lookup"><span data-stu-id="44801-172">The same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="44801-173">По умолчанию SDK одновременно получает пакет из 16 сообщений очереди и выполняет функцию, которая обрабатывает их параллельно.</span><span class="sxs-lookup"><span data-stu-id="44801-173">By default, the SDK gets a batch of 16 queue messages at a time and executes the function that processes them in parallel.</span></span> <span data-ttu-id="44801-174">[Можно настроить размер пакета](#config).</span><span class="sxs-lookup"><span data-stu-id="44801-174">[The batch size is configurable](#config).</span></span> <span data-ttu-id="44801-175">Когда число обрабатываемых сообщений достигает половины размера пакета, SDK запрашивает следующий пакет и начинает обработку содержащихся в нем сообщений.</span><span class="sxs-lookup"><span data-stu-id="44801-175">When the number being processed gets down to half of the batch size, the SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="44801-176">Поэтому максимальное количество сообщений, одновременно обрабатываемых каждой функцией, в полтора раза больше размера пакета.</span><span class="sxs-lookup"><span data-stu-id="44801-176">Therefore the maximum number of concurrent messages being processed per function is one and a half times the batch size.</span></span> <span data-ttu-id="44801-177">Это ограничение применяется отдельно к каждой функции с атрибутом `QueueTrigger` .</span><span class="sxs-lookup"><span data-stu-id="44801-177">This limit applies separately to each function that has a `QueueTrigger` attribute.</span></span>

<span data-ttu-id="44801-178">Если вы не хотите, чтобы сообщения из одной очереди обрабатывались параллельно, можно установить размер пакета равный 1.</span><span class="sxs-lookup"><span data-stu-id="44801-178">If you don't want parallel execution for messages received on one queue, you can set the batch size to 1.</span></span> <span data-ttu-id="44801-179">Ознакомьтесь также с подразделом **More control over Queue processing** (Больший контроль над обработкой очередей) в статье [Azure WebJobs SDK 1.1.0 RTM](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/) (Пакет SDK Azure для веб-заданий 1.1.0 RTM).</span><span class="sxs-lookup"><span data-stu-id="44801-179">See also **More control over Queue processing** in [Azure WebJobs SDK 1.1.0 RTM](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).</span></span>

### <span data-ttu-id="44801-180"><a id="queuemetadata"></a>Получение очереди или метаданных очереди сообщений</span><span class="sxs-lookup"><span data-stu-id="44801-180"><a id="queuemetadata"></a>Get queue or queue message metadata</span></span>
<span data-ttu-id="44801-181">Следующие свойства сообщений можно получить путем добавления параметров к сигнатуре метода:</span><span class="sxs-lookup"><span data-stu-id="44801-181">You can get the following message properties by adding parameters to the method signature:</span></span>

* <span data-ttu-id="44801-182">`DateTimeOffset` expirationTime;</span><span class="sxs-lookup"><span data-stu-id="44801-182">`DateTimeOffset` expirationTime</span></span>
* <span data-ttu-id="44801-183">`DateTimeOffset` insertionTime;</span><span class="sxs-lookup"><span data-stu-id="44801-183">`DateTimeOffset` insertionTime</span></span>
* <span data-ttu-id="44801-184">`DateTimeOffset` nextVisibleTime;</span><span class="sxs-lookup"><span data-stu-id="44801-184">`DateTimeOffset` nextVisibleTime</span></span>
* <span data-ttu-id="44801-185">`string` queueTrigger (содержит текст сообщения);</span><span class="sxs-lookup"><span data-stu-id="44801-185">`string` queueTrigger (contains message text)</span></span>
* <span data-ttu-id="44801-186">`string` id;</span><span class="sxs-lookup"><span data-stu-id="44801-186">`string` id</span></span>
* <span data-ttu-id="44801-187">`string` popReceipt;</span><span class="sxs-lookup"><span data-stu-id="44801-187">`string` popReceipt</span></span>
* <span data-ttu-id="44801-188">`int` dequeueCount.</span><span class="sxs-lookup"><span data-stu-id="44801-188">`int` dequeueCount</span></span>

<span data-ttu-id="44801-189">Если требуется работать непосредственно с API службы хранилища Azure, можно также добавить параметр `CloudStorageAccount` .</span><span class="sxs-lookup"><span data-stu-id="44801-189">If you want to work directly with the Azure storage API, you can also add a `CloudStorageAccount` parameter.</span></span>

<span data-ttu-id="44801-190">В следующем примере все эти метаданные записываются в журнал приложения INFO.</span><span class="sxs-lookup"><span data-stu-id="44801-190">The following example writes all of this metadata to an INFO application log.</span></span> <span data-ttu-id="44801-191">В примере содержимое сообщения очереди находится и в logMessage, и в queueTrigger.</span><span class="sxs-lookup"><span data-stu-id="44801-191">In the example, both logMessage and queueTrigger contain the content of the queue message.</span></span>

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

<span data-ttu-id="44801-192">Ниже приведен образец журнала, созданный с помощью кода из примера.</span><span class="sxs-lookup"><span data-stu-id="44801-192">Here is a sample log written by the sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

### <span data-ttu-id="44801-193"><a id="graceful"></a>Нормальное завершение работы</span><span class="sxs-lookup"><span data-stu-id="44801-193"><a id="graceful"></a>Graceful shutdown</span></span>
<span data-ttu-id="44801-194">Функция, которая запускается в постоянном веб-задании, может принимать параметр `CancellationToken` , который позволяет операционной системе уведомлять ее о том, что выполнение веб-задания будет завершено.</span><span class="sxs-lookup"><span data-stu-id="44801-194">A function that runs in a continuous WebJob can accept a `CancellationToken` parameter which enables the operating system to notify the function when the WebJob is about to be terminated.</span></span> <span data-ttu-id="44801-195">Это уведомление можно использовать для предотвращения ситуации, когда выполнение функции завершается неожиданно, оставляя данные в несогласованном состоянии.</span><span class="sxs-lookup"><span data-stu-id="44801-195">You can use this notification to make sure the function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="44801-196">Следующий пример показывает, как проверить функцию на наличие предстоящего завершения веб-задания.</span><span class="sxs-lookup"><span data-stu-id="44801-196">The following example shows how to check for impending WebJob termination in a function.</span></span>

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

<span data-ttu-id="44801-197">**Примечание.** Панель мониторинга может неправильно показывать состояние и выходные данные завершенных функций.</span><span class="sxs-lookup"><span data-stu-id="44801-197">**Note:** The Dashboard might not correctly show the status and output of functions that have been shut down.</span></span>

<span data-ttu-id="44801-198">Дополнительную информацию см. в статье [Нормальное завершение работы веб-заданий](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span><span class="sxs-lookup"><span data-stu-id="44801-198">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <span data-ttu-id="44801-199"><a id="createqueue"></a> Как создать сообщение очереди во время обработки сообщения очереди</span><span class="sxs-lookup"><span data-stu-id="44801-199"><a id="createqueue"></a> How to create a queue message while processing a queue message</span></span>
<span data-ttu-id="44801-200">Чтобы написать функцию, которая создает новое сообщение очереди, используйте атрибут `Queue` .</span><span class="sxs-lookup"><span data-stu-id="44801-200">To write a function that creates a new queue message, use the `Queue` attribute.</span></span> <span data-ttu-id="44801-201">Как и в случае с `QueueTrigger`, имя очереди можно передать в виде строки или [задать динамически](#config).</span><span class="sxs-lookup"><span data-stu-id="44801-201">Like `QueueTrigger`, you pass in the queue name as a string or you can [set the queue name dynamically](#config).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="44801-202">Строковые сообщения очереди</span><span class="sxs-lookup"><span data-stu-id="44801-202">String queue messages</span></span>
<span data-ttu-id="44801-203">Следующий пример неасинхронного кода создает новое сообщение очереди в очереди с именем «outputqueue» с тем же содержимым, что и сообщение очереди, поступившее в очередь с именем «inputqueue».</span><span class="sxs-lookup"><span data-stu-id="44801-203">The following non-async code sample creates a new queue message in the queue named "outputqueue" with the same content as the queue message received in the queue named "inputqueue".</span></span> <span data-ttu-id="44801-204">(Для асинхронных функций используйте `IAsyncCollector<T>` , следуя указаниям далее в этом разделе.)</span><span class="sxs-lookup"><span data-stu-id="44801-204">(For async functions use `IAsyncCollector<T>` as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="44801-205">Сообщения очереди [POCO](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)</span><span class="sxs-lookup"><span data-stu-id="44801-205">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="44801-206">Чтобы создать сообщение очереди, содержащее объект POCO, а не строку, передайте тип POCO в качестве выходного параметра конструктору атрибута `Queue` .</span><span class="sxs-lookup"><span data-stu-id="44801-206">To create a queue message that contains a POCO rather than a string, pass the POCO type as an output parameter to the `Queue` attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="44801-207">Пакет SDK автоматически выполняет сериализацию объекта в формат JSON.</span><span class="sxs-lookup"><span data-stu-id="44801-207">The SDK automatically serializes the object to JSON.</span></span> <span data-ttu-id="44801-208">Сообщение очереди создается всегда, даже если объект имеет значение null.</span><span class="sxs-lookup"><span data-stu-id="44801-208">A queue message is always created, even if the object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="44801-209">Создание нескольких сообщений или сообщений в асинхронных функциях</span><span class="sxs-lookup"><span data-stu-id="44801-209">Create multiple messages or in async functions</span></span>
<span data-ttu-id="44801-210">Чтобы создать несколько сообщений, установите для очереди вывода тип параметра `ICollector<T>` или `IAsyncCollector<T>`, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="44801-210">To create multiple messages, make the parameter type for the output queue `ICollector<T>` or `IAsyncCollector<T>`, as shown in the following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="44801-211">Каждое сообщение очереди создается сразу после вызова метода `Add` .</span><span class="sxs-lookup"><span data-stu-id="44801-211">Each queue message is created immediately when the `Add` method is called.</span></span>

### <a name="types-that-the-queue-attribute-works-with"></a><span data-ttu-id="44801-212">Типы, с которыми используется атрибут Queue</span><span class="sxs-lookup"><span data-stu-id="44801-212">Types that the Queue attribute works with</span></span>
<span data-ttu-id="44801-213">Атрибут `Queue` можно использовать со следующими типами параметров:</span><span class="sxs-lookup"><span data-stu-id="44801-213">You can use the `Queue` attribute on the following parameter types:</span></span>

* <span data-ttu-id="44801-214">`out string` (создает сообщение очереди, если по завершении вызова функции значение параметра не равно null);</span><span class="sxs-lookup"><span data-stu-id="44801-214">`out string` (creates queue message if parameter value is non-null when the function ends)</span></span>
* <span data-ttu-id="44801-215">`out byte[]` (действует как `string`);</span><span class="sxs-lookup"><span data-stu-id="44801-215">`out byte[]` (works like `string`)</span></span>
* <span data-ttu-id="44801-216">`out CloudQueueMessage` (действует как `string`);</span><span class="sxs-lookup"><span data-stu-id="44801-216">`out CloudQueueMessage` (works like `string`)</span></span>
* <span data-ttu-id="44801-217">`out POCO` (сериализуемый тип, создает сообщение с пустым объектом, если по завершении функции значение параметра — null);</span><span class="sxs-lookup"><span data-stu-id="44801-217">`out POCO` (a serializable type, creates a message with a null object if the paramter is null when the function ends)</span></span>
* `ICollector`
* `IAsyncCollector`
* <span data-ttu-id="44801-218">`CloudQueue` (позволяет создавать сообщения вручную и напрямую с помощью API службы хранилища Azure).</span><span class="sxs-lookup"><span data-stu-id="44801-218">`CloudQueue` (for creating messages manually using the Azure Storage API directly)</span></span>

### <span data-ttu-id="44801-219"><a id="ibinder"></a>Использование атрибутов пакета SDK для веб-заданий очереди в основном тексте функции</span><span class="sxs-lookup"><span data-stu-id="44801-219"><a id="ibinder"></a>Use WebJobs SDK attributes in the body of a function</span></span>
<span data-ttu-id="44801-220">Если перед использованием атрибута пакета SDK для веб-заданий, например `Queue`, `Blob` или `Table`, необходимо выполнить какие-либо действия с функцией, можно использовать интерфейс `IBinder`.</span><span class="sxs-lookup"><span data-stu-id="44801-220">If you need to do some work in your function before using a WebJobs SDK attribute such as `Queue`, `Blob`, or `Table`, you can use the `IBinder` interface.</span></span>

<span data-ttu-id="44801-221">В следующем примере в выходной очереди создается новое сообщение с тем же содержимым, что и в сообщении входной очереди.</span><span class="sxs-lookup"><span data-stu-id="44801-221">The following example takes an input queue message and creates a new message with the same content in an output queue.</span></span> <span data-ttu-id="44801-222">Имя очереди вывода определяется кодом в теле функции.</span><span class="sxs-lookup"><span data-stu-id="44801-222">The output queue name is set by code in the body of the function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="44801-223">Интерфейс `IBinder` также можно использовать при работе с атрибутами `Table` и `Blob`.</span><span class="sxs-lookup"><span data-stu-id="44801-223">The `IBinder` interface can also be used with the `Table` and `Blob` attributes.</span></span>

## <span data-ttu-id="44801-224"><a id="blobs"></a> Как выполнить чтение и запись больших двоичных объектов и таблиц во время обработки сообщения очереди</span><span class="sxs-lookup"><span data-stu-id="44801-224"><a id="blobs"></a> How to read and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="44801-225">Атрибуты `Blob` и `Table` позволяют осуществлять чтение и запись больших двоичных объектов и таблиц.</span><span class="sxs-lookup"><span data-stu-id="44801-225">The `Blob` and `Table` attributes enable you to read and write blobs and tables.</span></span> <span data-ttu-id="44801-226">Примеры в этом разделе применимы к BLOB-объектам.</span><span class="sxs-lookup"><span data-stu-id="44801-226">The samples in this section apply to blobs.</span></span> <span data-ttu-id="44801-227">Примеры кода, в которых показаны способы запуска процессов при создании или обновлении больших двоичных объектов, см. в статье [Как использовать хранилище больших двоичных объектов Azure с пакетом SDK для WebJob](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), а примеры кода для чтения и записи таблиц см. в статье [Как использовать табличное хранилище Azure с пакетом SDK для WebJob](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="44801-227">For code samples that show how to trigger processes when blobs are created or updated, see [How to use Azure blob storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How to use Azure table storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="44801-228">Сообщения очереди строк, которые запускают операции с большими двоичными объектами</span><span class="sxs-lookup"><span data-stu-id="44801-228">String queue messages triggering blob operations</span></span>
<span data-ttu-id="44801-229">Для сообщения очереди, содержащего строку, `queueTrigger` является заполнителем, который можно использовать в атрибуте `Blob` для параметра `blobPath`, в котором находится содержимое сообщения.</span><span class="sxs-lookup"><span data-stu-id="44801-229">For a queue message that contains a string, `queueTrigger` is a placeholder you can use in the `Blob` attribute's `blobPath` parameter that contains the contents of the message.</span></span>

<span data-ttu-id="44801-230">Следующий пример использует объекты `Stream` для чтения и записи больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="44801-230">The following example uses `Stream` objects to read and write blobs.</span></span> <span data-ttu-id="44801-231">Сообщение очереди — это имя большого двоичного объекта, размещенного в контейнере textblobs.</span><span class="sxs-lookup"><span data-stu-id="44801-231">The queue message is the name of a blob located in the textblobs container.</span></span> <span data-ttu-id="44801-232">Копия большого двоичного объекта с приставкой «-new», добавленной к имени, создается в том же контейнере.</span><span class="sxs-lookup"><span data-stu-id="44801-232">A copy of the blob with "-new" appended to the name is created in the same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="44801-233">Конструктор атрибута `Blob` учитывает параметр `blobPath`, который указывает имя контейнера и большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="44801-233">The `Blob` attribute constructor takes a `blobPath` parameter that specifies the container and blob name.</span></span> <span data-ttu-id="44801-234">Дополнительную информацию об этом заполнителе см. в статье [Как использовать хранилище больших двоичных объектов Azure с пакетом SDK для WebJob](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="44801-234">For more information about this placeholder, see [How to use Azure blob storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),</span></span>

<span data-ttu-id="44801-235">Если атрибут помечает объект `Stream`, другой параметр конструктора задает `FileAccess` в качестве режима чтения, записи или чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="44801-235">When the attribute decorates a `Stream` object, another constructor parameter specifies the `FileAccess` mode as read, write, or read/write.</span></span>

<span data-ttu-id="44801-236">Следующий пример использует объект `CloudBlockBlob` для удаления большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="44801-236">The following example uses a `CloudBlockBlob` object to delete a blob.</span></span> <span data-ttu-id="44801-237">Очередь сообщений — это имя большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="44801-237">The queue message is the name of the blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <span data-ttu-id="44801-238"><a id="pocoblobs"></a> Сообщения очереди [POCO](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)</span><span class="sxs-lookup"><span data-stu-id="44801-238"><a id="pocoblobs"></a> POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="44801-239">Для объектов POCO, сохраненных в формате JSON в сообщении очереди, можно использовать заполнители, которые называют свойства объектов в атрибуте `Queue` для параметра `blobPath`.</span><span class="sxs-lookup"><span data-stu-id="44801-239">For a POCO stored as JSON in the queue message, you can use placeholders that name properties of the object in the `Queue` attribute's `blobPath` parameter.</span></span> <span data-ttu-id="44801-240">Можно также использовать [имена свойства метаданных очереди](#queuemetadata) в качестве заполнителей.</span><span class="sxs-lookup"><span data-stu-id="44801-240">You can also use [queue metadata property names](#queuemetadata) as placeholders.</span></span>

<span data-ttu-id="44801-241">В следующем примере выполняется копирование большого двоичного объекта в новый большой двоичный объект с другим расширением.</span><span class="sxs-lookup"><span data-stu-id="44801-241">The following example copies a blob to a new blob with a different extension.</span></span> <span data-ttu-id="44801-242">Сообщение очереди представляет собой объект `BlobInformation` со свойствами `BlobName` и `BlobNameWithoutExtension`.</span><span class="sxs-lookup"><span data-stu-id="44801-242">The queue message is a `BlobInformation` object that includes `BlobName` and `BlobNameWithoutExtension` properties.</span></span> <span data-ttu-id="44801-243">В качестве заполнителей в пути к большому двоичному объекту используются имена свойств для атрибутов `Blob` .</span><span class="sxs-lookup"><span data-stu-id="44801-243">The property names are used as placeholders in the blob path for the `Blob` attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="44801-244">Для сериализации и десериализации сообщений в пакете SDK используется [пакет NuGet Newtonsoft.Json](http://www.nuget.org/packages/Newtonsoft.Json) .</span><span class="sxs-lookup"><span data-stu-id="44801-244">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="44801-245">В случае создания сообщений очереди с помощью программы, которая не использует пакет SDK для заданий WebJob, чтобы создать сообщение очереди POCO, которое сможет проанализировать такой пакет, вы можете написать код по следующему образцу.</span><span class="sxs-lookup"><span data-stu-id="44801-245">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="44801-246">Если необходимо выполнить некоторую работу в функции перед привязкой большого двоичного объекта к объекту, можно использовать атрибут в основном тексте функции, [как показано выше для атрибута Queue](#ibinder).</span><span class="sxs-lookup"><span data-stu-id="44801-246">If you need to do some work in your function before binding a blob to an object, you can use the attribute in the body of the function, [as shown earlier for the Queue attribute](#ibinder).</span></span>

### <span data-ttu-id="44801-247"><a id="blobattributetypes"></a> Типы, которые можно использовать с атрибутом Blob</span><span class="sxs-lookup"><span data-stu-id="44801-247"><a id="blobattributetypes"></a> Types you can use the Blob attribute with</span></span>
<span data-ttu-id="44801-248">Атрибут `Blob` можно использовать со следующими типами:</span><span class="sxs-lookup"><span data-stu-id="44801-248">The `Blob` attribute can be used with the following types:</span></span>

* <span data-ttu-id="44801-249">`Stream` (чтение или запись, указанные с помощью параметра конструктора FileAccess);</span><span class="sxs-lookup"><span data-stu-id="44801-249">`Stream` (read or write, specified by using the FileAccess constructor parameter)</span></span>
* `TextReader`
* `TextWriter`
* <span data-ttu-id="44801-250">`string` (чтение);</span><span class="sxs-lookup"><span data-stu-id="44801-250">`string` (read)</span></span>
* <span data-ttu-id="44801-251">`out string` (запись; создает большой двоичный объект, только если для параметра строки не задано значение null при возврате функции);</span><span class="sxs-lookup"><span data-stu-id="44801-251">`out string` (write; creates a blob only if the string parameter is non-null when the function returns)</span></span>
* <span data-ttu-id="44801-252">POCO (чтение);</span><span class="sxs-lookup"><span data-stu-id="44801-252">POCO (read)</span></span>
* <span data-ttu-id="44801-253">out POCO (запись; всегда создает пустой большой двоичный объект, если при возврате функции значение параметра POCO — null);</span><span class="sxs-lookup"><span data-stu-id="44801-253">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when the function returns)</span></span>
* <span data-ttu-id="44801-254">`CloudBlobStream` (запись);</span><span class="sxs-lookup"><span data-stu-id="44801-254">`CloudBlobStream` (write)</span></span>
* <span data-ttu-id="44801-255">`ICloudBlob` (чтение или запись);</span><span class="sxs-lookup"><span data-stu-id="44801-255">`ICloudBlob` (read or write)</span></span>
* <span data-ttu-id="44801-256">`CloudBlockBlob` (чтение или запись);</span><span class="sxs-lookup"><span data-stu-id="44801-256">`CloudBlockBlob` (read or write)</span></span>
* <span data-ttu-id="44801-257">`CloudPageBlob` (чтение или запись);</span><span class="sxs-lookup"><span data-stu-id="44801-257">`CloudPageBlob` (read or write)</span></span>

## <span data-ttu-id="44801-258"><a id="poison"></a> Как обработать подозрительные сообщения</span><span class="sxs-lookup"><span data-stu-id="44801-258"><a id="poison"></a> How to handle poison messages</span></span>
<span data-ttu-id="44801-259">Сообщения, содержимое которых вызывает сбой функции, называются *подозрительными сообщениями*.</span><span class="sxs-lookup"><span data-stu-id="44801-259">Messages whose content causes a function to fail are called *poison messages*.</span></span> <span data-ttu-id="44801-260">При сбое функции сообщение очереди не удаляется и в конечном итоге забирается снова, вызывая повтор цикла.</span><span class="sxs-lookup"><span data-stu-id="44801-260">When the function fails, the queue message is not deleted and eventually is picked up again, causing the cycle to be repeated.</span></span> <span data-ttu-id="44801-261">Пакет SDK может автоматически прервать цикл после ограниченного числа итераций или это можно сделать вручную.</span><span class="sxs-lookup"><span data-stu-id="44801-261">The SDK can automatically interrupt the cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="44801-262">Автоматическая обработка сообщений</span><span class="sxs-lookup"><span data-stu-id="44801-262">Automatic poison message handling</span></span>
<span data-ttu-id="44801-263">Пакет SDK вызывает функцию обработки сообщения очереди до 5 раз.</span><span class="sxs-lookup"><span data-stu-id="44801-263">The SDK will call a function up to 5 times to process a queue message.</span></span> <span data-ttu-id="44801-264">В случае сбоя во время пятой попытки сообщение перемещается в очередь подозрительных сообщений.</span><span class="sxs-lookup"><span data-stu-id="44801-264">If the fifth try fails, the message is moved to a poison queue.</span></span> <span data-ttu-id="44801-265">[Можно настроить максимальное количество попыток](#config).</span><span class="sxs-lookup"><span data-stu-id="44801-265">[The maximum number of retries is configurable](#config).</span></span>

<span data-ttu-id="44801-266">Очередь подозрительных сообщений называется *{originalqueuename}*-poison.</span><span class="sxs-lookup"><span data-stu-id="44801-266">The poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="44801-267">Можно написать функции для обработки сообщений из очереди подозрительных сообщений путем внесения их в журнал или отправки уведомления о необходимости ручного вмешательства.</span><span class="sxs-lookup"><span data-stu-id="44801-267">You can write a function to process messages from the poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="44801-268">В следующем примере функция `CopyBlob` завершится ошибкой, если сообщение очереди содержит имя несуществующего большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="44801-268">In the following example the `CopyBlob` function will fail when a queue message contains the name of a blob that doesn't exist.</span></span> <span data-ttu-id="44801-269">В таком случае сообщение перемещается из очереди copyblobqueue в очередь copyblobqueue-poison.</span><span class="sxs-lookup"><span data-stu-id="44801-269">When that happens, the message is moved from the copyblobqueue queue to the copyblobqueue-poison queue.</span></span> <span data-ttu-id="44801-270">Затем функция `ProcessPoisonMessage` записывает подозрительное сообщение в журнал.</span><span class="sxs-lookup"><span data-stu-id="44801-270">The `ProcessPoisonMessage` then logs the poison message.</span></span>

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

<span data-ttu-id="44801-271">На следующем рисунке показан вывод консоли при обработке этими функциями подозрительного сообщения.</span><span class="sxs-lookup"><span data-stu-id="44801-271">The following illustration shows console output from these functions when a poison message is processed.</span></span>

![Вывод консоли для обработки подозрительных сообщений](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="44801-273">Ручная обработка подозрительных сообщений</span><span class="sxs-lookup"><span data-stu-id="44801-273">Manual poison message handling</span></span>
<span data-ttu-id="44801-274">Чтобы узнать, сколько попыток обработки сообщения было совершено, добавьте к функции параметр `int` с именем `dequeueCount`.</span><span class="sxs-lookup"><span data-stu-id="44801-274">You can get the number of times a message has been picked up for processing by adding an `int` parameter named `dequeueCount` to your function.</span></span> <span data-ttu-id="44801-275">Затем можно проверить счетчик вывода из очереди в коде функции и выполнить собственную обработку подозрительных сообщений, если это число превышает пороговое значение, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="44801-275">You can then check the dequeue count in function code and perform your own poison message handling when the number exceeds a threshold, as shown in the following example.</span></span>

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

## <span data-ttu-id="44801-276"><a id="config"></a> Как установить параметры конфигурации</span><span class="sxs-lookup"><span data-stu-id="44801-276"><a id="config"></a> How to set configuration options</span></span>
<span data-ttu-id="44801-277">Чтобы задать следующие параметры конфигурации, можно использовать тип `JobHostConfiguration` :</span><span class="sxs-lookup"><span data-stu-id="44801-277">You can use the `JobHostConfiguration` type to set the following configuration options:</span></span>

* <span data-ttu-id="44801-278">Установка строк подключения пакета SDK в коде.</span><span class="sxs-lookup"><span data-stu-id="44801-278">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="44801-279">Настройка таких параметров атрибута `QueueTrigger` , как максимальное значение счетчика вывода из очереди.</span><span class="sxs-lookup"><span data-stu-id="44801-279">Configure `QueueTrigger` settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="44801-280">Получение имен очередей из конфигурации</span><span class="sxs-lookup"><span data-stu-id="44801-280">Get queue names from configuration.</span></span>

### <span data-ttu-id="44801-281"><a id="setconnstr"></a>Установка строк подключения пакета SDK в коде</span><span class="sxs-lookup"><span data-stu-id="44801-281"><a id="setconnstr"></a>Set SDK connection strings in code</span></span>
<span data-ttu-id="44801-282">Установка строк подключения пакета SDK в коде позволяет использовать собственные имена строк подключения в файлах конфигурации или переменных среды, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="44801-282">Setting the SDK connection strings in code enables you to use your own connection string names in configuration files or environment variables, as shown in the following example.</span></span>

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

### <span data-ttu-id="44801-283"><a id="configqueue"></a>Настройка параметров атрибута QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="44801-283"><a id="configqueue"></a>Configure QueueTrigger  settings</span></span>
<span data-ttu-id="44801-284">Можно настроить следующие параметры, которые применяются для обработки сообщений очереди:</span><span class="sxs-lookup"><span data-stu-id="44801-284">You can configure the following settings that apply to the queue message processing:</span></span>

* <span data-ttu-id="44801-285">Максимальное количество сообщений очереди, которые забираются одновременно для параллельной обработки (по умолчанию — 16).</span><span class="sxs-lookup"><span data-stu-id="44801-285">The maximum number of queue messages that are picked up simultaneously to be executed in parallel (default is 16).</span></span>
* <span data-ttu-id="44801-286">Максимальное число повторных попыток перед отправкой сообщения очереди в очередь подозрительных сообщений (по умолчанию — 5).</span><span class="sxs-lookup"><span data-stu-id="44801-286">The maximum number of retries before a queue message is sent to a poison queue (default is 5).</span></span>
* <span data-ttu-id="44801-287">Максимальное время ожидания перед повторным опросом, когда очередь пуста (по умолчанию — 1 минута).</span><span class="sxs-lookup"><span data-stu-id="44801-287">The maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="44801-288">В примере показано, как настроить эти параметры:</span><span class="sxs-lookup"><span data-stu-id="44801-288">The following example shows how to configure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <span data-ttu-id="44801-289"><a id="setnamesincode"></a>Установка значений параметров конструктора пакета SDK для веб-заданий в коде</span><span class="sxs-lookup"><span data-stu-id="44801-289"><a id="setnamesincode"></a>Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="44801-290">Иногда требуется указать в коде имя очереди, имя большого двоичного объекта, контейнера или таблицы, а не жестко задавать их.</span><span class="sxs-lookup"><span data-stu-id="44801-290">Sometimes you want to specify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="44801-291">Например, в некоторых случаях в файле конфигурации или в переменной среды необходимо указывать имя очереди для `QueueTrigger`.</span><span class="sxs-lookup"><span data-stu-id="44801-291">For example, you might want to specify the queue name for `QueueTrigger` in a configuration file or environment variable.</span></span>

<span data-ttu-id="44801-292">Вы можете сделать это, передав объект `NameResolver` типу `JobHostConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="44801-292">You can do that by passing in a `NameResolver` object to the `JobHostConfiguration` type.</span></span> <span data-ttu-id="44801-293">В параметрах конструктора атрибута пакета SDK для веб-заданий нужно указать специальные заполнители со знаками процента (%) с обеих сторон, тогда код `NameResolver` будет указывать фактические значения, которые следует использовать вместо этих заполнителей.</span><span class="sxs-lookup"><span data-stu-id="44801-293">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your `NameResolver` code specifies the actual values to be used in place of those placeholders.</span></span>

<span data-ttu-id="44801-294">Например, предположим, что вы хотите использовать очередь с именем logqueuetest в тестовой среде и очередь с именем logqueueprod в производственной среде.</span><span class="sxs-lookup"><span data-stu-id="44801-294">For example, suppose you want to use a queue named logqueuetest in the test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="44801-295">Вместо фиксированного имени очереди требуется указать имя элемента в коллекции `appSettings` с фактическим именем очереди.</span><span class="sxs-lookup"><span data-stu-id="44801-295">Instead of a hard-coded queue name, you want to specify the name of an entry in the `appSettings` collection that would have the actual queue name.</span></span> <span data-ttu-id="44801-296">Если logqueue — значение ключа `appSettings` , функция может выглядеть как в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="44801-296">If the `appSettings` key is logqueue, your function could look like the following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="44801-297">Затем класс `NameResolver` может получить имя очереди из `appSettings`, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="44801-297">Your `NameResolver` class could then get the queue name from `appSettings` as shown in the following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="44801-298">Необходимо передать класс `NameResolver` в объект `JobHost`, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="44801-298">You pass the `NameResolver` class in to the `JobHost` object as shown in the following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="44801-299">**Примечание.** Имена очередей, таблиц и больших двоичных объектов не разрешаются при каждом вызове функции, а имена контейнеров больших двоичных объектов разрешаются только при запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="44801-299">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when the application starts.</span></span> <span data-ttu-id="44801-300">Во время выполнения задания нельзя изменить имя контейнера больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="44801-300">You can't change blob container name while the job is running.</span></span>

## <span data-ttu-id="44801-301"><a id="manual"></a>Как вызвать функции вручную</span><span class="sxs-lookup"><span data-stu-id="44801-301"><a id="manual"></a>How to trigger a function manually</span></span>
<span data-ttu-id="44801-302">Чтобы вызвать функцию вручную, используйте метод `Call` или `CallAsync` объекта `JobHost` и атрибут `NoAutomaticTrigger` функции, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="44801-302">To trigger a function manually, use the `Call` or `CallAsync` method on the `JobHost` object and the `NoAutomaticTrigger` attribute on the function, as shown in the following example.</span></span>

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

## <span data-ttu-id="44801-303"><a id="logs"></a>Как записать журналы</span><span class="sxs-lookup"><span data-stu-id="44801-303"><a id="logs"></a>How to write logs</span></span>
<span data-ttu-id="44801-304">На панели мониторинга отображаются журналы: один на странице для заданий WebJob, а другой — на отдельной странице для определенного вызова задания WebJob.</span><span class="sxs-lookup"><span data-stu-id="44801-304">The Dashboard shows logs in two places: the page for the WebJob, and the page for a particular WebJob invocation.</span></span>

![Журналы на странице задания WebJob](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

![Журналы на странице вызова функций](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

<span data-ttu-id="44801-307">Выходные данные методов консоли, которые вызываются с помощью функции или метода `Main()` , отображаются на панели мониторинга на странице веб-задания, а не на странице для вызова определенного метода.</span><span class="sxs-lookup"><span data-stu-id="44801-307">Output from Console methods that you call in a function or in the `Main()` method appears in the Dashboard page for the WebJob, not in the page for a particular method invocation.</span></span> <span data-ttu-id="44801-308">Выходные данные объекта TextWriter, полученного из параметра в сигнатуре метода, отображаются на панели мониторинга на странице для вызова метода.</span><span class="sxs-lookup"><span data-stu-id="44801-308">Output from the TextWriter object that you get from a parameter in your method signature appears in the Dashboard page for a method invocation.</span></span>

<span data-ttu-id="44801-309">Выходные данные консоли нельзя связать с вызовом определенного метода, поскольку у консоли есть только один поток, хотя одновременно может выполняться сразу несколько функций.</span><span class="sxs-lookup"><span data-stu-id="44801-309">Console output can't be linked to a particular method invocation because the Console is single-threaded, while many job functions may be running at the same time.</span></span> <span data-ttu-id="44801-310">Поэтому пакет SDK обеспечивает вызов каждой функции с помощью уникального объекта модуля записи в журнал.</span><span class="sxs-lookup"><span data-stu-id="44801-310">That's why the  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="44801-311">Чтобы внести запись в [журналы трассировки приложений](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), используйте `Console.Out` (создает журналы с пометкой INFO) и `Console.Error` (создает журналы с пометкой ERROR).</span><span class="sxs-lookup"><span data-stu-id="44801-311">To write [application tracing logs](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use `Console.Out` (creates logs marked as INFO) and `Console.Error` (creates logs marked as ERROR).</span></span> <span data-ttu-id="44801-312">Кроме того, можно использовать [трассировку или TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), благодаря которым помимо информации и данных об ошибках можно получать подробные данные, предупреждения и оповещения о критическом уровне.</span><span class="sxs-lookup"><span data-stu-id="44801-312">An alternative is to use [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition to Info and Error.</span></span> <span data-ttu-id="44801-313">Журналы трассировки приложений отображаются в файлах журналов веб-приложения, таблицах Azure или больших двоичных объектах Azure, в зависимости от настроек вашего веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="44801-313">Application tracing logs appear in the web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="44801-314">Что касается всех выходных данных консоли, журналы последних 100 приложений отображаются на странице панели мониторинга для заданий WebJob, а не на странице для вызова функции.</span><span class="sxs-lookup"><span data-stu-id="44801-314">As is true of all Console output, the most recent 100 application logs also appear in the Dashboard page for the WebJob, not the page for a function invocation.</span></span>

<span data-ttu-id="44801-315">Выходные данные консоли отображаются на панели мониторинга, только если программа запущена в задании Azure WebJob, а не локально или в другой среде.</span><span class="sxs-lookup"><span data-stu-id="44801-315">Console output appears in the Dashboard only if the program is running in an Azure WebJob, not if the program is running locally or in some other environment.</span></span>

<span data-ttu-id="44801-316">Отключите ведение журнала панели мониторинга для сценариев с высокой пропускной способностью.</span><span class="sxs-lookup"><span data-stu-id="44801-316">Disable dashboard logging for high throughput scenarios.</span></span> <span data-ttu-id="44801-317">По умолчанию SDK записывает журналы в хранилище, и это действие может привести к снижению производительности при обработке большого числа сообщений.</span><span class="sxs-lookup"><span data-stu-id="44801-317">By default, the SDK writes logs to storage, and this activity could degrade performance when you are processing many messages.</span></span> <span data-ttu-id="44801-318">Чтобы отключить ведение журнала, задайте для строки подключения мониторинга значение null, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="44801-318">To disable logging, set the dashboard connection string to null as shown in the following example.</span></span>

        JobHostConfiguration config = new JobHostConfiguration();       
        config.DashboardConnectionString = "";        
        JobHost host = new JobHost(config);
        host.RunAndBlock();

<span data-ttu-id="44801-319">В следующем примере показано несколько способов записи журналов:</span><span class="sxs-lookup"><span data-stu-id="44801-319">The following example shows several ways to write logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="44801-320">Выходные данные из объекта `TextWriter` отобразятся на панели мониторинга SDK для веб-заданий, если перейти на страницу вызова определенной функции и нажать кнопку **Переключить вывод**:</span><span class="sxs-lookup"><span data-stu-id="44801-320">In the WebJobs SDK Dashboard, the output from the `TextWriter` object shows up when you go to the page for a particular function invocation and click **Toggle Output**:</span></span>

![Щелкнуть ссылку вызова функции](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardinvocations.png)

![Журналы на странице вызова функций](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

<span data-ttu-id="44801-323">Последние 100 строк вывода консоли отобразятся на панели мониторинга SDK для веб-заданий, если перейти на страницу для веб-задания (не для вызова функции) и нажать кнопку **Переключить вывод**.</span><span class="sxs-lookup"><span data-stu-id="44801-323">In the WebJobs SDK Dashboard, the most recent 100 lines of Console output show up when you go to the page for the WebJob (not for the function invocation) and click **Toggle Output**.</span></span>

![Нажать кнопку «Переключить вывод»](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

<span data-ttu-id="44801-325">Журналы приложений для непрерывных веб-заданий находятся по пути data/jobs/continuous/*{имя_веб-задания}*/job_log.txt в файловой системе веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="44801-325">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in the web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="44801-326">Вот как выглядят журналы приложений в большом двоичном объекте Azure: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span><span class="sxs-lookup"><span data-stu-id="44801-326">In an Azure blob the application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="44801-327">В таблице Azure журналы `Console.Out` и `Console.Error` выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="44801-327">And in an Azure table the `Console.Out` and `Console.Error` logs look like this:</span></span>

![Журнал Info в таблице](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableinfo.png)

![Журнал Error в таблице](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableerror.png)

<span data-ttu-id="44801-330">Если вы хотите подключить собственное средство ведения журнала, ознакомьтесь с [этим примером](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="44801-330">If you want to plug in your own logger, see [this example](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).</span></span>

## <span data-ttu-id="44801-331"><a id="errors"></a>Как обрабатывать ошибки и как настроить время ожидания</span><span class="sxs-lookup"><span data-stu-id="44801-331"><a id="errors"></a>How to handle errors and configure timeouts</span></span>
<span data-ttu-id="44801-332">Пакет SDK веб-заданий также включает в себя атрибут [Timeout](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) , который можно использовать для отмены функции, если ее выполнение не завершается в течение заданного времени.</span><span class="sxs-lookup"><span data-stu-id="44801-332">The WebJobs SDK also includes a [Timeout](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) attribute that you can use to cause a function to be canceled if doesn't complete within a specified amount of time.</span></span> <span data-ttu-id="44801-333">А если вы хотите создавать предупреждение, когда в течение указанного периода времени происходит слишком много ошибок, можно использовать атрибут `ErrorTrigger` .</span><span class="sxs-lookup"><span data-stu-id="44801-333">And if you want to raise an alert when too many errors happen within a specified period of time, you can use the `ErrorTrigger` attribute.</span></span> <span data-ttu-id="44801-334">Вот [пример ErrorTrigger](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).</span><span class="sxs-lookup"><span data-stu-id="44801-334">Here is an [ErrorTrigger example](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).</span></span>

```
public static void ErrorMonitor(
[ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
[SendGrid(
    To = "admin@emailaddress.com",
    Subject = "Error!")]
 SendGridMessage message)
{
    // log last 5 detailed errors to the Dashboard
   log.WriteLine(filter.GetDetailedMessage(5));
   message.Text = filter.GetDetailedMessage(1);
}
```

<span data-ttu-id="44801-335">Можно также динамически отключать и включать функции, чтобы управлять их активацией. Для вы можете использовать параметр конфигурации, который может быть параметром приложения или именем переменной среды.</span><span class="sxs-lookup"><span data-stu-id="44801-335">You can also dynamically disable and enable functions to control whether they can be triggered, by using a configuration switch that could be an app setting or environment variable name.</span></span> <span data-ttu-id="44801-336">Пример кода приведен в описании атрибута `Disable` в [репозитории примеров для пакета SDK для веб-заданий](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).</span><span class="sxs-lookup"><span data-stu-id="44801-336">For sample code, see the `Disable` attribute in [the WebJobs SDK samples repository](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).</span></span>

## <span data-ttu-id="44801-337"><a id="nextsteps"></a> Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="44801-337"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="44801-338">В этом руководстве предоставлены примеры кода обработки обычных сценариев для работы с очередями Azure.</span><span class="sxs-lookup"><span data-stu-id="44801-338">This guide has provided code samples that show how to handle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="44801-339">Дополнительную информацию об использовании веб-заданий Azure и пакета SDK для веб-заданий см. в [рекомендуемых ресурсах для веб-заданий Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="44801-339">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>
