---
title: "пропускная способность для tooincrease заданий Stream Analytics aaaScale | Документы Microsoft"
description: "Узнайте, как tooscale заданий Stream Analytics, настроив входной секций, помощник по настройке определение запроса hello и установив задания единицы потоковой передачи."
keywords: "потоковая передача данных, обработка потоковой передачи данных, настройка аналитики"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 7e857ddb-71dd-4537-b7ab-4524335d7b35
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/22/2017
ms.author: jeffstok
ms.openlocfilehash: 4ba8f6b2f8bfebd52cfa07696b501b42cda21f75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scale-azure-stream-analytics-jobs-tooincrease-stream-data-processing-throughput"></a><span data-ttu-id="27083-104">Масштабирование Azure Stream Analytics задания tooincrease поток обработки данных пропускной способности</span><span class="sxs-lookup"><span data-stu-id="27083-104">Scale Azure Stream Analytics jobs tooincrease stream data processing throughput</span></span>
<span data-ttu-id="27083-105">В этой статье показано, как tootune Stream Analytics запрос tooincrease пропускной способности для задания Streaming Analytics.</span><span class="sxs-lookup"><span data-stu-id="27083-105">This article shows you how tootune a Stream Analytics query tooincrease throughput for Streaming Analytics jobs.</span></span> <span data-ttu-id="27083-106">Вы узнаете, как задания tooscale Stream Analytics, настроив входной секций, определение запроса настройки аналитики hello и расчета и задания задания *единицы потоковой передачи* (SUs).</span><span class="sxs-lookup"><span data-stu-id="27083-106">You learn how tooscale Stream Analytics jobs by configuring input partitions, tuning hello analytics query definition, and calculating and setting job *streaming units* (SUs).</span></span> 

## <a name="what-are-hello-parts-of-a-stream-analytics-job"></a><span data-ttu-id="27083-107">Что такое hello части задания Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="27083-107">What are hello parts of a Stream Analytics job?</span></span>
<span data-ttu-id="27083-108">Определение задания Stream Analytics включает запрос, а также входные и выходные данные.</span><span class="sxs-lookup"><span data-stu-id="27083-108">A Stream Analytics job definition includes inputs, a query, and output.</span></span> <span data-ttu-id="27083-109">Входные данные:, где задания hello считывает hello поток данных из.</span><span class="sxs-lookup"><span data-stu-id="27083-109">Inputs are where hello job reads hello data stream from.</span></span> <span data-ttu-id="27083-110">Hello запроса используется tootransform hello данных входной поток, который вывода hello где задания hello отправляет результаты задания hello.</span><span class="sxs-lookup"><span data-stu-id="27083-110">hello query is used tootransform hello data input stream, and hello output is where hello job sends hello job results to.</span></span>  

<span data-ttu-id="27083-111">Задание требует по крайней мере один источник входных данных для потока данных.</span><span class="sxs-lookup"><span data-stu-id="27083-111">A job requires at least one input source for data streaming.</span></span> <span data-ttu-id="27083-112">Hello источник входного потока данных могут храниться в концентратор событий Azure или в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="27083-112">hello data stream input source can be stored in an Azure event hub or in Azure blob storage.</span></span> <span data-ttu-id="27083-113">Дополнительные сведения см. в разделе [tooAzure введение Stream Analytics](stream-analytics-introduction.md) и [приступить к использованию Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md).</span><span class="sxs-lookup"><span data-stu-id="27083-113">For more information, see [Introduction tooAzure Stream Analytics](stream-analytics-introduction.md) and [Get started using Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md).</span></span>

## <a name="partitions-in-event-hubs-and-azure-storage"></a><span data-ttu-id="27083-114">Секции в концентраторах событий и в хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="27083-114">Partitions in event hubs and Azure storage</span></span>
<span data-ttu-id="27083-115">Масштабирование задания Stream Analytics использует секций в hello вход или выход.</span><span class="sxs-lookup"><span data-stu-id="27083-115">Scaling a Stream Analytics job takes advantage of partitions in hello input or output.</span></span> <span data-ttu-id="27083-116">Секционирование позволяет разделить данные на подмножества на основе ключа секции.</span><span class="sxs-lookup"><span data-stu-id="27083-116">Partitioning lets you divide data into subsets based on a partition key.</span></span> <span data-ttu-id="27083-117">Процесс, который использует данные hello (например, задание Streaming Analytics) можно использовать и записи различных секций параллельно, что повышает производительность.</span><span class="sxs-lookup"><span data-stu-id="27083-117">A process that consumes hello data (such as a Streaming Analytics job) can consume and write different partitions in parallel, which increases throughput.</span></span> <span data-ttu-id="27083-118">При работе со Streaming Analytics можно воспользоваться преимуществами секционирования в концентраторах событий и в хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="27083-118">When you work with Streaming Analytics, you can take advantage of partitioning in event hubs and in Blob storage.</span></span> 

<span data-ttu-id="27083-119">Дополнительные сведения о секциях см. в разделе hello в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="27083-119">For more information about partitions, see hello following articles:</span></span>

* [<span data-ttu-id="27083-120">Обзор функций концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="27083-120">Event Hubs features overview</span></span>](../event-hubs/event-hubs-features.md#partitions)
* [<span data-ttu-id="27083-121">Секционирование данных</span><span class="sxs-lookup"><span data-stu-id="27083-121">Data partitioning</span></span>](https://docs.microsoft.com/azure/architecture/best-practices/data-partitioning#partitioning-azure-blob-storage)


## <a name="streaming-units-sus"></a><span data-ttu-id="27083-122">Единицы потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="27083-122">Streaming units (SUs)</span></span>
<span data-ttu-id="27083-123">Единицы (SUs) представляют Привет ресурсов потоковой передачи и вычислительной мощности, которые требуются в порядок tooexecute задание Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="27083-123">Streaming units (SUs) represent hello resources and computing power that are required in order tooexecute an Azure Stream Analytics job.</span></span> <span data-ttu-id="27083-124">SUs предоставляет способ toodescribe hello относительный событий производительности на основе на смешанном показателе ЦП, памяти, обработки и чтения, а также скорости записи.</span><span class="sxs-lookup"><span data-stu-id="27083-124">SUs provide a way toodescribe hello relative event processing capacity based on a blended measure of CPU, memory, and read and write rates.</span></span> <span data-ttu-id="27083-125">Каждый SU соответствует tooroughly 1 МБ/с пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="27083-125">Each SU corresponds tooroughly 1 MB/second of throughput.</span></span> 

<span data-ttu-id="27083-126">Выбор количества SUs необходимы для конкретного задания зависит от конфигурации hello секции для входных данных hello и hello запрос, определенный для задания hello.</span><span class="sxs-lookup"><span data-stu-id="27083-126">Choosing how many SUs are required for a particular job depends on hello partition configuration for hello inputs and on hello query defined for hello job.</span></span> <span data-ttu-id="27083-127">Можно выбрать копирование tooyour квоты в SUs для задания.</span><span class="sxs-lookup"><span data-stu-id="27083-127">You can select up tooyour quota in SUs for a job.</span></span> <span data-ttu-id="27083-128">По умолчанию каждая подписка Azure имеет квоту копирование SUs too50 для всех заданий analytics hello в определенном регионе.</span><span class="sxs-lookup"><span data-stu-id="27083-128">By default, each Azure subscription has a quota of up too50 SUs for all hello analytics jobs in a specific region.</span></span> <span data-ttu-id="27083-129">tooincrease SUs для ваших подписок за эту квоту, обратитесь к [поддержки Майкрософт](http://support.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="27083-129">tooincrease SUs for your subscriptions beyond this quota, contact [Microsoft Support](http://support.microsoft.com).</span></span> <span data-ttu-id="27083-130">Для задания допустимые значения количества начинаются с 1, 3, 6 и затем по возрастающей с шагом в 6.</span><span class="sxs-lookup"><span data-stu-id="27083-130">Valid values for SUs per job are 1, 3, 6, and up in increments of 6.</span></span>

## <a name="embarrassingly-parallel-jobs"></a><span data-ttu-id="27083-131">Задания с усложненным параллелизмом</span><span class="sxs-lookup"><span data-stu-id="27083-131">Embarrassingly parallel jobs</span></span>
<span data-ttu-id="27083-132">*Неудобно параллельные* задания является сценарием максимально масштабируемые hello, у нас есть в Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="27083-132">An *embarrassingly parallel* job is hello most scalable scenario we have in Azure Stream Analytics.</span></span> <span data-ttu-id="27083-133">Подключение одной секции экземпляр входной tooone hello раздела tooone запроса hello hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="27083-133">It connects one partition of hello input tooone instance of hello query tooone partition of hello output.</span></span> <span data-ttu-id="27083-134">Это параллелизм имеет hello следующие требования:</span><span class="sxs-lookup"><span data-stu-id="27083-134">This parallelism has hello following requirements:</span></span>

1. <span data-ttu-id="27083-135">Если логику запроса зависит от hello ключ обрабатывается по hello же экземпляр запроса, необходимо убедиться, что события hello проходят toohello одной секции входные данные.</span><span class="sxs-lookup"><span data-stu-id="27083-135">If your query logic depends on hello same key being processed by hello same query instance, you must make sure that hello events go toohello same partition of your input.</span></span> <span data-ttu-id="27083-136">Для концентраторов событий, это означает, что данные события hello должен иметь hello **PartitionKey** заданным значением.</span><span class="sxs-lookup"><span data-stu-id="27083-136">For event hubs, this means that hello event data must have hello **PartitionKey** value set.</span></span> <span data-ttu-id="27083-137">Кроме того, можно использовать секционированные отправители.</span><span class="sxs-lookup"><span data-stu-id="27083-137">Alternatively, you can use partitioned senders.</span></span> <span data-ttu-id="27083-138">Для хранилища больших двоичных объектов, это означает, что события hello отправляются toohello папке секции.</span><span class="sxs-lookup"><span data-stu-id="27083-138">For blob storage, this means that hello events are sent toohello same partition folder.</span></span> <span data-ttu-id="27083-139">Если логику запроса требует hello ключ toobe обработки по hello же экземпляр запроса, можно игнорировать это требование.</span><span class="sxs-lookup"><span data-stu-id="27083-139">If your query logic does not require hello same key toobe processed by hello same query instance, you can ignore this requirement.</span></span> <span data-ttu-id="27083-140">В качестве примера такой логики можно привести простой запрос select, project или filter.</span><span class="sxs-lookup"><span data-stu-id="27083-140">An example of this logic would be a simple select-project-filter query.</span></span>  

2. <span data-ttu-id="27083-141">После размещения hello данных на стороне входной hello, необходимо убедиться, что запрос является секционированной.</span><span class="sxs-lookup"><span data-stu-id="27083-141">Once hello data is laid out on hello input side, you must make sure that your query is partitioned.</span></span> <span data-ttu-id="27083-142">Для этого необходимо toouse **Partition By** на всех этапах hello.</span><span class="sxs-lookup"><span data-stu-id="27083-142">This requires you toouse **Partition By** in all hello steps.</span></span> <span data-ttu-id="27083-143">Несколько шагов являются допустимыми, но все они должны быть секционированы по hello таким же ключом.</span><span class="sxs-lookup"><span data-stu-id="27083-143">Multiple steps are allowed, but they all must be partitioned by hello same key.</span></span> <span data-ttu-id="27083-144">В настоящее время hello ключ разделов необходимо задать слишком**PartitionId** в порядке для полностью параллельных toobe задания hello.</span><span class="sxs-lookup"><span data-stu-id="27083-144">Currently, hello partitioning key must be set too**PartitionId** in order for hello job toobe fully parallel.</span></span>  

3. <span data-ttu-id="27083-145">На данном этапе секционированные выходные данные поддерживаются только концентраторами событий и хранилищами BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="27083-145">Currently only event hubs and blob storage support partitioned output.</span></span> <span data-ttu-id="27083-146">Для выходных данных концентратора событий, необходимо настроить toobe ключа секции hello **PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="27083-146">For event hub output, you must configure hello partition key toobe **PartitionId**.</span></span> <span data-ttu-id="27083-147">Для вывода хранилища больших двоичных объектов у вас нет toodo ничего.</span><span class="sxs-lookup"><span data-stu-id="27083-147">For blob storage output, you don't have toodo anything.</span></span>  

4. <span data-ttu-id="27083-148">Hello количество входных секций должно быть равно hello количество секций выходных данных.</span><span class="sxs-lookup"><span data-stu-id="27083-148">hello number of input partitions must equal hello number of output partitions.</span></span> <span data-ttu-id="27083-149">В настоящее время выходные данные хранилища BLOB-объектов не поддерживают секционирование.</span><span class="sxs-lookup"><span data-stu-id="27083-149">Blob storage output doesn't currently support partitions.</span></span> <span data-ttu-id="27083-150">Но это неважно, он наследует hello схему запроса вышестоящего hello секционирования.</span><span class="sxs-lookup"><span data-stu-id="27083-150">But that's okay, because it inherits hello partitioning scheme of hello upstream query.</span></span> <span data-ttu-id="27083-151">Примеры значений секций, позволяющие выполнять задания с полной параллельной обработкой:</span><span class="sxs-lookup"><span data-stu-id="27083-151">Here are examples of partition values that allow a fully parallel job:</span></span>  

   * <span data-ttu-id="27083-152">8 секций входных данных концентраторов событий и 8 секций выходных данных концентраторов событий;</span><span class="sxs-lookup"><span data-stu-id="27083-152">8 event hub input partitions and 8 event hub output partitions</span></span>
   * <span data-ttu-id="27083-153">8 секций входных данных концентраторов событий и выходные данные хранилища BLOB-объектов;</span><span class="sxs-lookup"><span data-stu-id="27083-153">8 event hub input partitions and blob storage output</span></span>  
   * <span data-ttu-id="27083-154">8 секций входных данных хранилища BLOB-объектов и выходные данные хранилища BLOB-объектов;</span><span class="sxs-lookup"><span data-stu-id="27083-154">8 blob storage input partitions and blob storage output</span></span>  
   * <span data-ttu-id="27083-155">8 секций входных данных хранилища BLOB-объектов и 8 секций выходных данных концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="27083-155">8 blob storage input partitions and 8 event hub output partitions</span></span>  

<span data-ttu-id="27083-156">Hello следующих разделах рассматриваются некоторые примеры сценариев, которые являются неудобно параллельные.</span><span class="sxs-lookup"><span data-stu-id="27083-156">hello following sections discuss some example scenarios that are embarrassingly parallel.</span></span>

### <a name="simple-query"></a><span data-ttu-id="27083-157">Простой запрос</span><span class="sxs-lookup"><span data-stu-id="27083-157">Simple query</span></span>

* <span data-ttu-id="27083-158">Входные данные — концентратор событий с 8 секциями.</span><span class="sxs-lookup"><span data-stu-id="27083-158">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="27083-159">Выходные данные — концентратор событий с 8 секциями.</span><span class="sxs-lookup"><span data-stu-id="27083-159">Output: Event hub with 8 partitions</span></span>

<span data-ttu-id="27083-160">Запрос:</span><span class="sxs-lookup"><span data-stu-id="27083-160">Query:</span></span>

    SELECT TollBoothId
    FROM Input1 Partition By PartitionId
    WHERE TollBoothId > 100

<span data-ttu-id="27083-161">Этот запрос является простым фильтром.</span><span class="sxs-lookup"><span data-stu-id="27083-161">This query is a simple filter.</span></span> <span data-ttu-id="27083-162">Таким образом нам не нужен tooworry о секционировании hello входные данные, которые передаются toohello концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="27083-162">Therefore, we don't need tooworry about partitioning hello input that is being sent toohello event hub.</span></span> <span data-ttu-id="27083-163">Обратите внимание, что hello запрос включает **секции с PartitionId**, поэтому он удовлетворяет требованию #2 из более ранних версий.</span><span class="sxs-lookup"><span data-stu-id="27083-163">Notice that hello query includes **Partition By PartitionId**, so it fulfills requirement #2 from earlier.</span></span> <span data-ttu-id="27083-164">Для вывода hello, нам необходимо tooconfigure выходных данных концентратора hello событий в hello задания toohave hello разбиения набор ключей слишком**PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="27083-164">For hello output, we need tooconfigure hello event hub output in hello job toohave hello parition key set too**PartitionId**.</span></span> <span data-ttu-id="27083-165">Один последней проверке — toomake, убедитесь, что hello количество входных секций равно toohello количество секций выходных данных.</span><span class="sxs-lookup"><span data-stu-id="27083-165">One last check is toomake sure that hello number of input partitions is equal toohello number of output partitions.</span></span>

### <a name="query-with-a-grouping-key"></a><span data-ttu-id="27083-166">Запрос с ключом группирования</span><span class="sxs-lookup"><span data-stu-id="27083-166">Query with a grouping key</span></span>

* <span data-ttu-id="27083-167">Входные данные — концентратор событий с 8 секциями.</span><span class="sxs-lookup"><span data-stu-id="27083-167">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="27083-168">Выходные данные — хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="27083-168">Output: Blob storage</span></span>

<span data-ttu-id="27083-169">Запрос:</span><span class="sxs-lookup"><span data-stu-id="27083-169">Query:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="27083-170">Этот запрос содержит ключ группирования.</span><span class="sxs-lookup"><span data-stu-id="27083-170">This query has a grouping key.</span></span> <span data-ttu-id="27083-171">Таким образом hello же toobe основных требований, обрабатываемых hello же экземпляр, это означает, что события должны быть отправлены концентратора событий toohello секционированных образом запроса.</span><span class="sxs-lookup"><span data-stu-id="27083-171">Therefore, hello same key needs toobe processed by hello same query instance, which means that events must be sent toohello event hub in a partitioned manner.</span></span> <span data-ttu-id="27083-172">Какой ключ следует использовать?</span><span class="sxs-lookup"><span data-stu-id="27083-172">But which key should be used?</span></span> <span data-ttu-id="27083-173">Ключ **PartitionId** определяет логику задания.</span><span class="sxs-lookup"><span data-stu-id="27083-173">**PartitionId** is a job-logic concept.</span></span> <span data-ttu-id="27083-174">Мы стремимся фактически ключ Hello **TollBoothId**, Здравствуйте, поэтому **PartitionKey** значение данных о событиях hello следует **TollBoothId**.</span><span class="sxs-lookup"><span data-stu-id="27083-174">hello key we actually care about is **TollBoothId**, so hello **PartitionKey** value of hello event data should be **TollBoothId**.</span></span> <span data-ttu-id="27083-175">Это делается в запросе hello, задав **Partition By** слишком**PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="27083-175">We do this in hello query by setting **Partition By** too**PartitionId**.</span></span> <span data-ttu-id="27083-176">Поскольку выходные данные hello хранилища больших двоичных объектов, нам не нужен tooworry о настройке значения ключа раздела, согласно требование #4.</span><span class="sxs-lookup"><span data-stu-id="27083-176">Since hello output is blob storage, we don't need tooworry about configuring a partition key value, as per requirement #4.</span></span>

### <a name="multi-step-query-with-a-grouping-key"></a><span data-ttu-id="27083-177">Многоэтапный запрос с ключом группирования</span><span class="sxs-lookup"><span data-stu-id="27083-177">Multi-step query with a grouping key</span></span>
* <span data-ttu-id="27083-178">Входные данные — концентратор событий с 8 секциями.</span><span class="sxs-lookup"><span data-stu-id="27083-178">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="27083-179">Выходные данные — экземпляр концентратора событий с 8 секциями.</span><span class="sxs-lookup"><span data-stu-id="27083-179">Output: Event hub instance with 8 partitions</span></span>

<span data-ttu-id="27083-180">Запрос:</span><span class="sxs-lookup"><span data-stu-id="27083-180">Query:</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="27083-181">Этот запрос содержит ключ группирования, поэтому hello же toobe основных требований, обрабатываемых hello того же экземпляра запроса.</span><span class="sxs-lookup"><span data-stu-id="27083-181">This query has a grouping key, so hello same key needs toobe processed by hello same query instance.</span></span> <span data-ttu-id="27083-182">Мы используем hello же стратегии, как показано в предыдущем примере hello.</span><span class="sxs-lookup"><span data-stu-id="27083-182">We can use hello same strategy as in hello previous example.</span></span> <span data-ttu-id="27083-183">В этом случае запрос hello состоит из нескольких шагов.</span><span class="sxs-lookup"><span data-stu-id="27083-183">In this case, hello query has multiple steps.</span></span> <span data-ttu-id="27083-184">Указан ли на каждом этапе параметр **Partition By PartitionId**?</span><span class="sxs-lookup"><span data-stu-id="27083-184">Does each step have **Partition By PartitionId**?</span></span> <span data-ttu-id="27083-185">Да, поэтому запрос hello удовлетворяет требованию #3.</span><span class="sxs-lookup"><span data-stu-id="27083-185">Yes, so hello query fulfills requirement #3.</span></span> <span data-ttu-id="27083-186">Для вывода hello, нам необходимо ключ раздела hello tooset слишком**PartitionId**, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="27083-186">For hello output, we need tooset hello partition key too**PartitionId**, as discussed earlier.</span></span> <span data-ttu-id="27083-187">Также можно увидеть, что она имеет hello одинаковое количество секций в качестве входного hello.</span><span class="sxs-lookup"><span data-stu-id="27083-187">We can also see that it has hello same number of partitions as hello input.</span></span>

## <a name="example-scenarios-that-are-not-embarrassingly-parallel"></a><span data-ttu-id="27083-188">Примеры сценариев *без* усложненного параллелизма</span><span class="sxs-lookup"><span data-stu-id="27083-188">Example scenarios that are *not* embarrassingly parallel</span></span>

<span data-ttu-id="27083-189">В предыдущем разделе hello мы показали некоторые неудобно параллельные сценарии.</span><span class="sxs-lookup"><span data-stu-id="27083-189">In hello previous section, we showed some embarrassingly parallel scenarios.</span></span> <span data-ttu-id="27083-190">В этом разделе обсуждаются сценарии, которые не соответствуют всем hello требования toobe неудобно параллельные.</span><span class="sxs-lookup"><span data-stu-id="27083-190">In this section, we discuss scenarios that don't meet all hello requirements toobe embarrassingly parallel.</span></span> 

### <a name="mismatched-partition-count"></a><span data-ttu-id="27083-191">Несоответствие в числе секций</span><span class="sxs-lookup"><span data-stu-id="27083-191">Mismatched partition count</span></span>
* <span data-ttu-id="27083-192">Входные данные — концентратор событий с 8 секциями.</span><span class="sxs-lookup"><span data-stu-id="27083-192">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="27083-193">Выходные данные — концентратор событий с 32 секциями.</span><span class="sxs-lookup"><span data-stu-id="27083-193">Output: Event hub with 32 partitions</span></span>

<span data-ttu-id="27083-194">В этом случае неважно, какой запрос hello.</span><span class="sxs-lookup"><span data-stu-id="27083-194">In this case, it doesn't matter what hello query is.</span></span> <span data-ttu-id="27083-195">Если количество входных разделов hello не совпадает количество разделов hello выходные данные, не неудобно параллельные hello топологии.</span><span class="sxs-lookup"><span data-stu-id="27083-195">If hello input partition count doesn't match hello output partition count, hello topology isn't embarrassingly parallel.</span></span>

### <a name="not-using-event-hubs-or-blob-storage-as-output"></a><span data-ttu-id="27083-196">Для выходных данных не используются концентраторы событий или хранилище BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="27083-196">Not using event hubs or blob storage as output</span></span>
* <span data-ttu-id="27083-197">Входные данные — концентратор событий с 8 секциями.</span><span class="sxs-lookup"><span data-stu-id="27083-197">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="27083-198">Выходные данные — PowerBI.</span><span class="sxs-lookup"><span data-stu-id="27083-198">Output: PowerBI</span></span>

<span data-ttu-id="27083-199">В настоящее время выходные данные PowerBI не поддерживают секционирование.</span><span class="sxs-lookup"><span data-stu-id="27083-199">PowerBI output doesn't currently support partitioning.</span></span> <span data-ttu-id="27083-200">Таким образом этот сценарий не считается сценарием с усложненным параллелизмом.</span><span class="sxs-lookup"><span data-stu-id="27083-200">Therefore, this scenario is not embarrassingly parallel.</span></span>

### <a name="multi-step-query-with-different-partition-by-values"></a><span data-ttu-id="27083-201">Многоэтапный запрос с разными значениями параметра Partition By</span><span class="sxs-lookup"><span data-stu-id="27083-201">Multi-step query with different Partition By values</span></span>
* <span data-ttu-id="27083-202">Входные данные — концентратор событий с 8 секциями.</span><span class="sxs-lookup"><span data-stu-id="27083-202">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="27083-203">Выходные данные — концентратор событий с 8 секциями.</span><span class="sxs-lookup"><span data-stu-id="27083-203">Output: Event hub with 8 partitions</span></span>

<span data-ttu-id="27083-204">Запрос:</span><span class="sxs-lookup"><span data-stu-id="27083-204">Query:</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By TollBoothId
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="27083-205">Как видно, второй шаг hello использует **TollBoothId** как hello ключ секционирования.</span><span class="sxs-lookup"><span data-stu-id="27083-205">As you can see, hello second step uses **TollBoothId** as hello partitioning key.</span></span> <span data-ttu-id="27083-206">Этот шаг не является hello же в качестве первого шага hello и поэтому требует нам toodo в случайном порядке.</span><span class="sxs-lookup"><span data-stu-id="27083-206">This step is not hello same as hello first step, and it therefore requires us toodo a shuffle.</span></span> 

<span data-ttu-id="27083-207">Hello выше примерах некоторых заданий Stream Analytics, которые соответствуют слишком (или не) неудобно параллельные топологии.</span><span class="sxs-lookup"><span data-stu-id="27083-207">hello preceding examples show some Stream Analytics jobs that conform too(or don't) an embarrassingly parallel topology.</span></span> <span data-ttu-id="27083-208">Если они соответствуют, они имеют возможность hello максимальный масштаб.</span><span class="sxs-lookup"><span data-stu-id="27083-208">If they do conform, they have hello potential for maximum scale.</span></span> <span data-ttu-id="27083-209">Для заданий, не соответствующих ни одному из этих профилей, в дальнейшем будут выпущены обновления в отношении масштабирования.</span><span class="sxs-lookup"><span data-stu-id="27083-209">For jobs that don't fit one of these profiles, scaling guidance will be available in future updates.</span></span> <span data-ttu-id="27083-210">Теперь используйте hello Общие рекомендации в следующих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="27083-210">For now, use hello general guidance in hello following sections.</span></span>

## <a name="calculate-hello-maximum-streaming-units-of-a-job"></a><span data-ttu-id="27083-211">Вычислить максимальное число единиц потоковой передачи hello задания</span><span class="sxs-lookup"><span data-stu-id="27083-211">Calculate hello maximum streaming units of a job</span></span>
<span data-ttu-id="27083-212">Общее число единиц потоковой передачи, которые могут использоваться в задании Stream Analytics Hello зависит от hello число шагов в hello запрос, определенный для задания hello и hello число разделов для каждого шага.</span><span class="sxs-lookup"><span data-stu-id="27083-212">hello total number of streaming units that can be used by a Stream Analytics job depends on hello number of steps in hello query defined for hello job and hello number of partitions for each step.</span></span>

### <a name="steps-in-a-query"></a><span data-ttu-id="27083-213">Шаги в запросе</span><span class="sxs-lookup"><span data-stu-id="27083-213">Steps in a query</span></span>
<span data-ttu-id="27083-214">Запрос может иметь один или несколько шагов.</span><span class="sxs-lookup"><span data-stu-id="27083-214">A query can have one or many steps.</span></span> <span data-ttu-id="27083-215">Каждый шаг — вложенный запрос, определяется hello **WITH** ключевое слово.</span><span class="sxs-lookup"><span data-stu-id="27083-215">Each step is a subquery defined by hello **WITH** keyword.</span></span> <span data-ttu-id="27083-216">Hello запрос, который находится за пределами hello **WITH** ключевое слово (только для одного запроса) также считаются шага, например hello **ВЫБЕРИТЕ** инструкции в следующем запросе hello:</span><span class="sxs-lookup"><span data-stu-id="27083-216">hello query that is outside hello **WITH** keyword (one query only) is also counted as a step, such as hello **SELECT** statement in hello following query:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute,3), TollBoothId

<span data-ttu-id="27083-217">Этот запрос включает 2 шага.</span><span class="sxs-lookup"><span data-stu-id="27083-217">This query has two steps.</span></span>

> [!NOTE]
> <span data-ttu-id="27083-218">Этот запрос является более подробно далее в статье hello.</span><span class="sxs-lookup"><span data-stu-id="27083-218">This query is discussed in more detail later in hello article.</span></span>
>  

### <a name="partition-a-step"></a><span data-ttu-id="27083-219">Разделы шага</span><span class="sxs-lookup"><span data-stu-id="27083-219">Partition a step</span></span>
<span data-ttu-id="27083-220">Секционирование шаг требует hello следующие условия:</span><span class="sxs-lookup"><span data-stu-id="27083-220">Partitioning a step requires hello following conditions:</span></span>

* <span data-ttu-id="27083-221">Hello источника входных данных должны быть секционированы.</span><span class="sxs-lookup"><span data-stu-id="27083-221">hello input source must be partitioned.</span></span> 
* <span data-ttu-id="27083-222">Hello **ВЫБЕРИТЕ** инструкции запроса hello должны считать из секционированной входного источника.</span><span class="sxs-lookup"><span data-stu-id="27083-222">hello **SELECT** statement of hello query must read from a partitioned input source.</span></span>
* <span data-ttu-id="27083-223">запрос Hello в пределах шага hello должен иметь hello **Partition By** ключевое слово.</span><span class="sxs-lookup"><span data-stu-id="27083-223">hello query within hello step must have hello **Partition By** keyword.</span></span>

<span data-ttu-id="27083-224">При секционировании запроса hello входного события, обработанные и обработанные статистически в отдельной секции группы и выходные данные события создаются для каждой из групп hello.</span><span class="sxs-lookup"><span data-stu-id="27083-224">When a query is partitioned, hello input events are processed and aggregated in separate partition groups, and outputs events are generated for each of hello groups.</span></span> <span data-ttu-id="27083-225">Объединенный агрегат, создать второй tooaggregate несекционированного шаг.</span><span class="sxs-lookup"><span data-stu-id="27083-225">If you want a combined aggregate, you must create a second non-partitioned step tooaggregate.</span></span>

### <a name="calculate-hello-max-streaming-units-for-a-job"></a><span data-ttu-id="27083-226">Вычислить максимальный hello единицы для задания потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="27083-226">Calculate hello max streaming units for a job</span></span>
<span data-ttu-id="27083-227">Все шаги несекционированного вместе можно увеличивать масштаб toosix единицы (SUs) для задания Stream Analytics потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="27083-227">All non-partitioned steps together can scale up toosix streaming units (SUs) for a Stream Analytics job.</span></span> <span data-ttu-id="27083-228">SUs tooadd, шаг должны быть секционированы.</span><span class="sxs-lookup"><span data-stu-id="27083-228">tooadd SUs, a step must be partitioned.</span></span> <span data-ttu-id="27083-229">Каждая секция может включать шесть единиц потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="27083-229">Each partition can have six SUs.</span></span>

<table border="1">
<tr><th><span data-ttu-id="27083-230">Запрос</span><span class="sxs-lookup"><span data-stu-id="27083-230">Query</span></span></th><th><span data-ttu-id="27083-231">SUs Max для задания hello</span><span class="sxs-lookup"><span data-stu-id="27083-231">Max SUs for hello job</span></span></th></td>

<tr><td>
<ul>
<li><span data-ttu-id="27083-232">запрос Hello содержит один шаг.</span><span class="sxs-lookup"><span data-stu-id="27083-232">hello query contains one step.</span></span></li>
<li><span data-ttu-id="27083-233">шаг Hello не секционирована.</span><span class="sxs-lookup"><span data-stu-id="27083-233">hello step is not partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="27083-234">6</span><span class="sxs-lookup"><span data-stu-id="27083-234">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="27083-235">поток входных данных Hello секционируется по 3.</span><span class="sxs-lookup"><span data-stu-id="27083-235">hello input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="27083-236">запрос Hello содержит один шаг.</span><span class="sxs-lookup"><span data-stu-id="27083-236">hello query contains one step.</span></span></li>
<li><span data-ttu-id="27083-237">шаг Hello секционирована.</span><span class="sxs-lookup"><span data-stu-id="27083-237">hello step is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="27083-238">18</span><span class="sxs-lookup"><span data-stu-id="27083-238">18</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="27083-239">Hello запросов содержит два шага.</span><span class="sxs-lookup"><span data-stu-id="27083-239">hello query contains two steps.</span></span></li>
<li><span data-ttu-id="27083-240">Ни один из шагов hello секционирована.</span><span class="sxs-lookup"><span data-stu-id="27083-240">Neither of hello steps is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="27083-241">6</span><span class="sxs-lookup"><span data-stu-id="27083-241">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="27083-242">поток входных данных Hello секционируется по 3.</span><span class="sxs-lookup"><span data-stu-id="27083-242">hello input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="27083-243">Hello запросов содержит два шага.</span><span class="sxs-lookup"><span data-stu-id="27083-243">hello query contains two steps.</span></span> <span data-ttu-id="27083-244">шаг ввода Hello секционирована и второй шаг hello не.</span><span class="sxs-lookup"><span data-stu-id="27083-244">hello input step is partitioned and hello second step is not.</span></span></li>
<li><span data-ttu-id="27083-245">Hello <strong>ВЫБЕРИТЕ</strong> считывает инструкции hello секционированы входных данных.</span><span class="sxs-lookup"><span data-stu-id="27083-245">hello <strong>SELECT</strong> statement reads from hello partitioned input.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="27083-246">24 (18 и 6 секционированных и несекционированных шагов соответственно)</span><span class="sxs-lookup"><span data-stu-id="27083-246">24 (18 for partitioned steps + 6 for non-partitioned steps)</span></span></td></tr>
</table>

### <a name="examples-of-scaling"></a><span data-ttu-id="27083-247">Примеры масштабирования</span><span class="sxs-lookup"><span data-stu-id="27083-247">Examples of scaling</span></span>

<span data-ttu-id="27083-248">Hello следующий запрос вычисляет hello количество машин в окне три минуты, через платный станции, которая имеет три tollbooths.</span><span class="sxs-lookup"><span data-stu-id="27083-248">hello following query calculates hello number of cars within a three-minute window going through a toll station that has three tollbooths.</span></span> <span data-ttu-id="27083-249">Этот запрос можно масштабировать в сторону toosix SUs.</span><span class="sxs-lookup"><span data-stu-id="27083-249">This query can be scaled up toosix SUs.</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="27083-250">Дополнительные toouse SUs для hello запроса, оба hello потока входных данных и hello запроса должны быть секционированы.</span><span class="sxs-lookup"><span data-stu-id="27083-250">toouse more SUs for hello query, both hello input data stream and hello query must be partitioned.</span></span> <span data-ttu-id="27083-251">Поскольку раздел потока данных hello устанавливается too3, hello следующем измененном запросе можно масштабировать в сторону too18 SUs:</span><span class="sxs-lookup"><span data-stu-id="27083-251">Since hello data stream partition is set too3, hello following modified query can be scaled up too18 SUs:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="27083-252">При секционировании запроса hello входные события обрабатываются и объединяются в отдельный раздел групп.</span><span class="sxs-lookup"><span data-stu-id="27083-252">When a query is partitioned, hello input events are processed and aggregated in separate partition groups.</span></span> <span data-ttu-id="27083-253">События выхода также создаются для каждой из групп hello.</span><span class="sxs-lookup"><span data-stu-id="27083-253">Output events are also generated for each of hello groups.</span></span> <span data-ttu-id="27083-254">Секционирование может вызвать некоторые непредвиденные результаты, если hello **GROUP BY** поле не является ключом секции hello hello потока входных данных.</span><span class="sxs-lookup"><span data-stu-id="27083-254">Partitioning can cause some unexpected results when hello **GROUP BY** field is not hello partition key in hello input data stream.</span></span> <span data-ttu-id="27083-255">Например, hello **TollBoothId** поля в предыдущем запросе hello не является ключом секции hello **Input1**.</span><span class="sxs-lookup"><span data-stu-id="27083-255">For example, hello **TollBoothId** field in hello previous query is not hello partition key of **Input1**.</span></span> <span data-ttu-id="27083-256">результат Hello — приветствия, данные из пропускного пункта #1 могут быть распределены в нескольких секциях.</span><span class="sxs-lookup"><span data-stu-id="27083-256">hello result is that hello data from TollBooth #1 can be spread in multiple partitions.</span></span>

<span data-ttu-id="27083-257">Каждый из hello **Input1** секций будет обрабатываться отдельно Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="27083-257">Each of hello **Input1** partitions will be processed separately by Stream Analytics.</span></span> <span data-ttu-id="27083-258">В результате нескольких записей количества car hello для hello же пропускного пункта в hello же «переворачивающееся» окно будет создан.</span><span class="sxs-lookup"><span data-stu-id="27083-258">As a result, multiple records of hello car count for hello same tollbooth in hello same Tumbling window will be created.</span></span> <span data-ttu-id="27083-259">Если невозможно изменить ключ секции входной hello, эту проблему можно устранить путем добавления шага не раздела, как следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="27083-259">If hello input partition key can't be changed, this problem can be fixed by adding a non-partition step, as in hello following example:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="27083-260">Этот запрос может быть SUs масштабированный too24.</span><span class="sxs-lookup"><span data-stu-id="27083-260">This query can be scaled too24 SUs.</span></span>

> [!NOTE]
> <span data-ttu-id="27083-261">При объединении двух потоков, убедитесь, что потоки hello секционируются ключом секции hello столбца hello использовать toocreate hello соединения.</span><span class="sxs-lookup"><span data-stu-id="27083-261">If you are joining two streams, make sure that hello streams are partitioned by hello partition key of hello column that you use toocreate hello joins.</span></span> <span data-ttu-id="27083-262">Также убедитесь, что hello одинаковое количество секций в обоих потоках.</span><span class="sxs-lookup"><span data-stu-id="27083-262">Also make sure that you have hello same number of partitions in both streams.</span></span>
> 
> 

## <a name="configure-stream-analytics-streaming-units"></a><span data-ttu-id="27083-263">Настройка единиц потоковой передачи Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="27083-263">Configure Stream Analytics streaming units</span></span>

1. <span data-ttu-id="27083-264">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="27083-264">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="27083-265">Найдите задание Stream Analytics hello tooscale и затем откройте его в список hello ресурсов.</span><span class="sxs-lookup"><span data-stu-id="27083-265">In hello list of resources, find hello Stream Analytics job that you want tooscale and then open it.</span></span>
3. <span data-ttu-id="27083-266">В hello задания колонке в разделе **Настройка**, нажмите кнопку **шкалы**.</span><span class="sxs-lookup"><span data-stu-id="27083-266">In hello job blade, under **Configure**, click **Scale**.</span></span>

    ![Настройка задания Stream Analytics на портале Azure][img.stream.analytics.preview.portal.settings.scale]

4. <span data-ttu-id="27083-268">Используйте hello ползунок tooset hello SUs для задания hello.</span><span class="sxs-lookup"><span data-stu-id="27083-268">Use hello slider tooset hello SUs for hello job.</span></span> <span data-ttu-id="27083-269">Обратите внимание, что вы ограниченный toospecific SU параметры.</span><span class="sxs-lookup"><span data-stu-id="27083-269">Notice that you are limited toospecific SU settings.</span></span>


## <a name="monitor-job-performance"></a><span data-ttu-id="27083-270">Мониторинг производительности задания</span><span class="sxs-lookup"><span data-stu-id="27083-270">Monitor job performance</span></span>
<span data-ttu-id="27083-271">Hello портала Azure вы можете отслеживать пропускную способность hello задания:</span><span class="sxs-lookup"><span data-stu-id="27083-271">Using hello Azure portal, you can track hello throughput of a job:</span></span>

![Отслеживание заданий Azure Stream Analytics][img.stream.analytics.monitor.job]

<span data-ttu-id="27083-273">Расчет hello ожидается пропускной способности hello рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="27083-273">Calculate hello expected throughput of hello workload.</span></span> <span data-ttu-id="27083-274">Если пропускная способность hello меньше ожидаемого, настраивать раздел ввода hello, настройки запросов hello и добавить задание tooyour SUs.</span><span class="sxs-lookup"><span data-stu-id="27083-274">If hello throughput is less than expected, tune hello input partition, tune hello query, and add SUs tooyour job.</span></span>


## <a name="visualize-stream-analytics-throughput-at-scale-hello-raspberry-pi-scenario"></a><span data-ttu-id="27083-275">Визуализация пропускной способности Stream Analytics в масштабе: hello Raspberry Pi сценария</span><span class="sxs-lookup"><span data-stu-id="27083-275">Visualize Stream Analytics throughput at scale: hello Raspberry Pi scenario</span></span>
<span data-ttu-id="27083-276">toohelp понять, как масштабировать заданий Stream Analytics, мы выполнили эксперимента, на основе введенных данных с устройства Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="27083-276">toohelp you understand how Stream Analytics jobs scale, we performed an experiment based on input from a Raspberry Pi device.</span></span> <span data-ttu-id="27083-277">Этом эксперименте сообщить нам увидеть эффект hello пропускной способности нескольких потоковой передачи единиц измерения и секции.</span><span class="sxs-lookup"><span data-stu-id="27083-277">This experiment let us see hello effect on throughput of multiple streaming units and partitions.</span></span>

<span data-ttu-id="27083-278">В этом сценарии hello устройство отправляет концентратора событий tooan датчиков данных (клиенты).</span><span class="sxs-lookup"><span data-stu-id="27083-278">In this scenario, hello device sends sensor data (clients) tooan event hub.</span></span> <span data-ttu-id="27083-279">Streaming Analytics обрабатывает данные hello и отправляет предупреждение или статистические данные в качестве концентратора событий tooanother выходных данных.</span><span class="sxs-lookup"><span data-stu-id="27083-279">Streaming Analytics processes hello data and sends an alert or statistics as an output tooanother event hub.</span></span> 

<span data-ttu-id="27083-280">Hello клиент отправляет данные датчиков в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="27083-280">hello client sends sensor data in JSON format.</span></span> <span data-ttu-id="27083-281">выходные данные Hello также находится в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="27083-281">hello data output is also in JSON format.</span></span> <span data-ttu-id="27083-282">Hello данных выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="27083-282">hello data looks like this:</span></span>

    {"devicetime":"2014-12-11T02:24:56.8850110Z","hmdt":42.7,"temp":72.6,"prss":98187.75,"lght":0.38,"dspl":"R-PI Olivier's Office"}

<span data-ttu-id="27083-283">приветствия при следующем запросе является используется toosend оповещение, если индикатор отключена:</span><span class="sxs-lookup"><span data-stu-id="27083-283">hello following query is used toosend an alert when a light is switched off:</span></span>

    SELECT AVG(lght),
     "LightOff" as AlertText
    FROM input TIMESTAMP
    BY devicetime
     WHERE
        lght< 0.05 GROUP BY TumblingWindow(second, 1)

### <a name="measure-throughput"></a><span data-ttu-id="27083-284">Измерения пропускной способности</span><span class="sxs-lookup"><span data-stu-id="27083-284">Measure throughput</span></span>

<span data-ttu-id="27083-285">В этом контексте пропускная способность — hello набора входных данных, обрабатываемых Stream Analytics в определенный промежуток времени.</span><span class="sxs-lookup"><span data-stu-id="27083-285">In this context, throughput is hello amount of input data processed by Stream Analytics in a fixed amount of time.</span></span> <span data-ttu-id="27083-286">(Мы измеряется на 10 минут). tooachieve hello лучшей обработки пропускной способности для hello входные данные, как данные hello потока входных данных и секционирование hello запроса.</span><span class="sxs-lookup"><span data-stu-id="27083-286">(We measured for 10 minutes.) tooachieve hello best processing throughput for hello input data, both hello data stream input and hello query were  partitioned.</span></span> <span data-ttu-id="27083-287">Мы включили **COUNT()** в toomeasure запрос hello обрабатывались сколько входных событий.</span><span class="sxs-lookup"><span data-stu-id="27083-287">We included **COUNT()** in hello query toomeasure how many input events were processed.</span></span> <span data-ttu-id="27083-288">убедиться, что задание hello toomake не ожидала просто toocome события ввода, каждой секции концентратора событий ввода hello была предварительно загружена с 300 МБ входных данных.</span><span class="sxs-lookup"><span data-stu-id="27083-288">toomake sure hello job was not simply waiting for input events toocome, each partition of hello input event hub was preloaded with about 300 MB of input data.</span></span>

<span data-ttu-id="27083-289">Hello следующей таблице показаны результаты hello, который мы видели, когда мы увеличили hello число единиц потоковой передачи и соответствующая секция hello учитывается в концентраторы событий.</span><span class="sxs-lookup"><span data-stu-id="27083-289">hello following table shows hello results we saw when we increased hello number of streaming units and hello corresponding partition counts in event hubs.</span></span>  

<table border="1">
<tr><th><span data-ttu-id="27083-290">Секции ввода</span><span class="sxs-lookup"><span data-stu-id="27083-290">Input Partitions</span></span></th><th><span data-ttu-id="27083-291">Секции вывода</span><span class="sxs-lookup"><span data-stu-id="27083-291">Output Partitions</span></span></th><th><span data-ttu-id="27083-292">Единицы потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="27083-292">Streaming Units</span></span></th><th><span data-ttu-id="27083-293">Поддерживаемая пропускная способность</span><span class="sxs-lookup"><span data-stu-id="27083-293">Sustained Throughput</span></span>
</th></td>

<tr><td><span data-ttu-id="27083-294">12</span><span class="sxs-lookup"><span data-stu-id="27083-294">12</span></span></td>
<td><span data-ttu-id="27083-295">12</span><span class="sxs-lookup"><span data-stu-id="27083-295">12</span></span></td>
<td><span data-ttu-id="27083-296">6</span><span class="sxs-lookup"><span data-stu-id="27083-296">6</span></span></td>
<td><span data-ttu-id="27083-297">4,06 МБ/с</span><span class="sxs-lookup"><span data-stu-id="27083-297">4.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="27083-298">12</span><span class="sxs-lookup"><span data-stu-id="27083-298">12</span></span></td>
<td><span data-ttu-id="27083-299">12</span><span class="sxs-lookup"><span data-stu-id="27083-299">12</span></span></td>
<td><span data-ttu-id="27083-300">12</span><span class="sxs-lookup"><span data-stu-id="27083-300">12</span></span></td>
<td><span data-ttu-id="27083-301">8,06 МБ/с</span><span class="sxs-lookup"><span data-stu-id="27083-301">8.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="27083-302">48</span><span class="sxs-lookup"><span data-stu-id="27083-302">48</span></span></td>
<td><span data-ttu-id="27083-303">48</span><span class="sxs-lookup"><span data-stu-id="27083-303">48</span></span></td>
<td><span data-ttu-id="27083-304">48</span><span class="sxs-lookup"><span data-stu-id="27083-304">48</span></span></td>
<td><span data-ttu-id="27083-305">38,32 МБ/с</span><span class="sxs-lookup"><span data-stu-id="27083-305">38.32 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="27083-306">192</span><span class="sxs-lookup"><span data-stu-id="27083-306">192</span></span></td>
<td><span data-ttu-id="27083-307">192</span><span class="sxs-lookup"><span data-stu-id="27083-307">192</span></span></td>
<td><span data-ttu-id="27083-308">192</span><span class="sxs-lookup"><span data-stu-id="27083-308">192</span></span></td>
<td><span data-ttu-id="27083-309">172,67 МБ/с</span><span class="sxs-lookup"><span data-stu-id="27083-309">172.67 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="27083-310">480</span><span class="sxs-lookup"><span data-stu-id="27083-310">480</span></span></td>
<td><span data-ttu-id="27083-311">480</span><span class="sxs-lookup"><span data-stu-id="27083-311">480</span></span></td>
<td><span data-ttu-id="27083-312">480</span><span class="sxs-lookup"><span data-stu-id="27083-312">480</span></span></td>
<td><span data-ttu-id="27083-313">454,27 МБ/с</span><span class="sxs-lookup"><span data-stu-id="27083-313">454.27 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="27083-314">720</span><span class="sxs-lookup"><span data-stu-id="27083-314">720</span></span></td>
<td><span data-ttu-id="27083-315">720</span><span class="sxs-lookup"><span data-stu-id="27083-315">720</span></span></td>
<td><span data-ttu-id="27083-316">720</span><span class="sxs-lookup"><span data-stu-id="27083-316">720</span></span></td>
<td><span data-ttu-id="27083-317">609,69 МБ/с</span><span class="sxs-lookup"><span data-stu-id="27083-317">609.69 MB/s</span></span></td>
</tr>
</table>

<span data-ttu-id="27083-318">И hello следующей диаграмме показано hello отношения между SUs и пропускной способности визуализации.</span><span class="sxs-lookup"><span data-stu-id="27083-318">And hello following graph shows a visualization of hello relationship between SUs and throughput.</span></span>

![img.stream.analytics.perfgraph][img.stream.analytics.perfgraph]

## <a name="get-help"></a><span data-ttu-id="27083-320">Получение справки</span><span class="sxs-lookup"><span data-stu-id="27083-320">Get help</span></span>
<span data-ttu-id="27083-321">За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="27083-321">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="27083-322">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="27083-322">Next steps</span></span>
* [<span data-ttu-id="27083-323">Введение tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="27083-323">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="27083-324">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="27083-324">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="27083-325">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="27083-325">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="27083-326">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="27083-326">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Image references-->

[img.stream.analytics.monitor.job]: ./media/stream-analytics-scale-jobs/StreamAnalytics.job.monitor-NewPortal.png
[img.stream.analytics.configure.scale]: ./media/stream-analytics-scale-jobs/StreamAnalytics.configure.scale.png
[img.stream.analytics.perfgraph]: ./media/stream-analytics-scale-jobs/perf.png
[img.stream.analytics.streaming.units.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsStreamingUnitsExample.jpg
[img.stream.analytics.preview.portal.settings.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsPreviewPortalJobSettings-NewPortal.png   

<!--Link references-->

[microsoft.support]: http://support.microsoft.com
[azure.management.portal]: http://manage.windowsazure.com
[azure.event.hubs.developer.guide]: http://msdn.microsoft.com/library/azure/dn789972.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

