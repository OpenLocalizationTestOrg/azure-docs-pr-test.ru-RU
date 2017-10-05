---
title: "Задания по масштабированию в Azure Stream Analytics для увеличения пропускной способности | Документация Майкрософт"
description: "Узнайте, как масштабировать задания Stream Analytics с помощью настройки входных разделов, настройки определения запроса и определения единиц потоковой передачи."
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
ms.openlocfilehash: ab894976c72ea3785d7f58e51b3dd64511e1e8e3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="scale-azure-stream-analytics-jobs-to-increase-stream-data-processing-throughput"></a><span data-ttu-id="cc13f-104">Масштабирование заданий Azure Stream Analytics для повышения пропускной способности базы данных</span><span class="sxs-lookup"><span data-stu-id="cc13f-104">Scale Azure Stream Analytics jobs to increase stream data processing throughput</span></span>
<span data-ttu-id="cc13f-105">В этой статье описано, как настроить запрос Stream Analytics для увеличения пропускной способности заданий Streaming Analytics.</span><span class="sxs-lookup"><span data-stu-id="cc13f-105">This article shows you how to tune a Stream Analytics query to increase throughput for Streaming Analytics jobs.</span></span> <span data-ttu-id="cc13f-106">Узнайте, как масштабировать задания Stream Analytics путем настройки секций ввода, задания определения запроса аналитики, а также вычисления и определения *единиц потоковой передачи* задания.</span><span class="sxs-lookup"><span data-stu-id="cc13f-106">You learn how to scale Stream Analytics jobs by configuring input partitions, tuning the analytics query definition, and calculating and setting job *streaming units* (SUs).</span></span> 

## <a name="what-are-the-parts-of-a-stream-analytics-job"></a><span data-ttu-id="cc13f-107">Из каких частей состоит задание службы Stream Analytics?</span><span class="sxs-lookup"><span data-stu-id="cc13f-107">What are the parts of a Stream Analytics job?</span></span>
<span data-ttu-id="cc13f-108">Определение задания Stream Analytics включает запрос, а также входные и выходные данные.</span><span class="sxs-lookup"><span data-stu-id="cc13f-108">A Stream Analytics job definition includes inputs, a query, and output.</span></span> <span data-ttu-id="cc13f-109">Входные данные — это точки, откуда задания считывают данные из потока.</span><span class="sxs-lookup"><span data-stu-id="cc13f-109">Inputs are where the job reads the data stream from.</span></span> <span data-ttu-id="cc13f-110">Запрос используется для преобразования потока входных данных, а выходные данные являются точками, куда направляются результаты задания.</span><span class="sxs-lookup"><span data-stu-id="cc13f-110">The query is used to transform the data input stream, and the output is where the job sends the job results to.</span></span>  

<span data-ttu-id="cc13f-111">Задание требует по крайней мере один источник входных данных для потока данных.</span><span class="sxs-lookup"><span data-stu-id="cc13f-111">A job requires at least one input source for data streaming.</span></span> <span data-ttu-id="cc13f-112">Входной источник потока данных может храниться в концентраторе событий Azure или в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="cc13f-112">The data stream input source can be stored in an Azure event hub or in Azure blob storage.</span></span> <span data-ttu-id="cc13f-113">Дополнительные сведения см. в статьях [Что такое Stream Analytics?](stream-analytics-introduction.md) и [Приступая к работе с Azure Stream Analytics: выявление мошенничества в режиме реального времени](stream-analytics-real-time-fraud-detection.md).</span><span class="sxs-lookup"><span data-stu-id="cc13f-113">For more information, see [Introduction to Azure Stream Analytics](stream-analytics-introduction.md) and [Get started using Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md).</span></span>

## <a name="partitions-in-event-hubs-and-azure-storage"></a><span data-ttu-id="cc13f-114">Секции в концентраторах событий и в хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="cc13f-114">Partitions in event hubs and Azure storage</span></span>
<span data-ttu-id="cc13f-115">Масштабирование задания Stream Analytics реализует преимущества использования секций во входных или выходных данных.</span><span class="sxs-lookup"><span data-stu-id="cc13f-115">Scaling a Stream Analytics job takes advantage of partitions in the input or output.</span></span> <span data-ttu-id="cc13f-116">Секционирование позволяет разделить данные на подмножества на основе ключа секции.</span><span class="sxs-lookup"><span data-stu-id="cc13f-116">Partitioning lets you divide data into subsets based on a partition key.</span></span> <span data-ttu-id="cc13f-117">Процесс, который использует данные (например, задание Streaming Analytics), может получать и записывать различные секции параллельно, тем самым повышая пропускную способность.</span><span class="sxs-lookup"><span data-stu-id="cc13f-117">A process that consumes the data (such as a Streaming Analytics job) can consume and write different partitions in parallel, which increases throughput.</span></span> <span data-ttu-id="cc13f-118">При работе со Streaming Analytics можно воспользоваться преимуществами секционирования в концентраторах событий и в хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="cc13f-118">When you work with Streaming Analytics, you can take advantage of partitioning in event hubs and in Blob storage.</span></span> 

<span data-ttu-id="cc13f-119">Дополнительные сведения об этих секциях см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="cc13f-119">For more information about partitions, see the following articles:</span></span>

* [<span data-ttu-id="cc13f-120">Обзор функций концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="cc13f-120">Event Hubs features overview</span></span>](../event-hubs/event-hubs-features.md#partitions)
* [<span data-ttu-id="cc13f-121">Секционирование данных</span><span class="sxs-lookup"><span data-stu-id="cc13f-121">Data partitioning</span></span>](https://docs.microsoft.com/azure/architecture/best-practices/data-partitioning#partitioning-azure-blob-storage)


## <a name="streaming-units-sus"></a><span data-ttu-id="cc13f-122">Единицы потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="cc13f-122">Streaming units (SUs)</span></span>
<span data-ttu-id="cc13f-123">Единицы потоковой передачи представляют ресурсы и вычислительную мощность, необходимые для выполнения задания Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="cc13f-123">Streaming units (SUs) represent the resources and computing power that are required in order to execute an Azure Stream Analytics job.</span></span> <span data-ttu-id="cc13f-124">Единицы потоковой передачи предоставляют способ описания относительной мощности обработки события, основываясь на измерении загрузки ЦП, памяти и скорости чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="cc13f-124">SUs provide a way to describe the relative event processing capacity based on a blended measure of CPU, memory, and read and write rates.</span></span> <span data-ttu-id="cc13f-125">Каждая единица потоковой передачи соответствует пропускной способности около 1 МБ/с.</span><span class="sxs-lookup"><span data-stu-id="cc13f-125">Each SU corresponds to roughly 1 MB/second of throughput.</span></span> 

<span data-ttu-id="cc13f-126">Выбор необходимого количества единиц потоковой передачи для конкретного задания зависит от конфигурации секции для входных данных и запроса, определенного для задания.</span><span class="sxs-lookup"><span data-stu-id="cc13f-126">Choosing how many SUs are required for a particular job depends on the partition configuration for the inputs and on the query defined for the job.</span></span> <span data-ttu-id="cc13f-127">Вы можете выбрать для задания количество единиц потоковой передачи согласно указанной квоте.</span><span class="sxs-lookup"><span data-stu-id="cc13f-127">You can select up to your quota in SUs for a job.</span></span> <span data-ttu-id="cc13f-128">По умолчанию каждая подписка Azure включает в себя квоту до 50 единиц потоковой передачи для всех заданий аналитики в определенном регионе.</span><span class="sxs-lookup"><span data-stu-id="cc13f-128">By default, each Azure subscription has a quota of up to 50 SUs for all the analytics jobs in a specific region.</span></span> <span data-ttu-id="cc13f-129">Чтобы увеличить количество единиц потоковой передачи для своей подписки, свяжитесь со [службой технической поддержки Майкрософт](http://support.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="cc13f-129">To increase SUs for your subscriptions beyond this quota, contact [Microsoft Support](http://support.microsoft.com).</span></span> <span data-ttu-id="cc13f-130">Для задания допустимые значения количества начинаются с 1, 3, 6 и затем по возрастающей с шагом в 6.</span><span class="sxs-lookup"><span data-stu-id="cc13f-130">Valid values for SUs per job are 1, 3, 6, and up in increments of 6.</span></span>

## <a name="embarrassingly-parallel-jobs"></a><span data-ttu-id="cc13f-131">Задания с усложненным параллелизмом</span><span class="sxs-lookup"><span data-stu-id="cc13f-131">Embarrassingly parallel jobs</span></span>
<span data-ttu-id="cc13f-132">Задание с *усложненным параллелизмом* — это самый масштабируемый сценарий в Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="cc13f-132">An *embarrassingly parallel* job is the most scalable scenario we have in Azure Stream Analytics.</span></span> <span data-ttu-id="cc13f-133">Он соединяет один раздел входных данных с одним экземпляром запроса и одним разделом выходных данных.</span><span class="sxs-lookup"><span data-stu-id="cc13f-133">It connects one partition of the input to one instance of the query to one partition of the output.</span></span> <span data-ttu-id="cc13f-134">Такой параллелизм имеет следующие требования:</span><span class="sxs-lookup"><span data-stu-id="cc13f-134">This parallelism has the following requirements:</span></span>

1. <span data-ttu-id="cc13f-135">Если в логике запроса применяется ключ, который обрабатывается тем же экземпляром запроса, необходимо только проследить за тем, чтобы события попадали в ту же секцию входных данных.</span><span class="sxs-lookup"><span data-stu-id="cc13f-135">If your query logic depends on the same key being processed by the same query instance, you must make sure that the events go to the same partition of your input.</span></span> <span data-ttu-id="cc13f-136">При использовании концентраторов событий это означает, что для данных событий должно быть задано значение **PartitionKey**.</span><span class="sxs-lookup"><span data-stu-id="cc13f-136">For event hubs, this means that the event data must have the **PartitionKey** value set.</span></span> <span data-ttu-id="cc13f-137">Кроме того, можно использовать секционированные отправители.</span><span class="sxs-lookup"><span data-stu-id="cc13f-137">Alternatively, you can use partitioned senders.</span></span> <span data-ttu-id="cc13f-138">Для хранилища BLOB-объектов это означает, что события отправляются в папку той же секции.</span><span class="sxs-lookup"><span data-stu-id="cc13f-138">For blob storage, this means that the events are sent to the same partition folder.</span></span> <span data-ttu-id="cc13f-139">Если логика запроса не требует обработки ключа тем же экземпляром запроса, это требование можно проигнорировать.</span><span class="sxs-lookup"><span data-stu-id="cc13f-139">If your query logic does not require the same key to be processed by the same query instance, you can ignore this requirement.</span></span> <span data-ttu-id="cc13f-140">В качестве примера такой логики можно привести простой запрос select, project или filter.</span><span class="sxs-lookup"><span data-stu-id="cc13f-140">An example of this logic would be a simple select-project-filter query.</span></span>  

2. <span data-ttu-id="cc13f-141">После того как данные будут распределены в источнике данных, необходимо убедиться в том, что запрос разбит на секции.</span><span class="sxs-lookup"><span data-stu-id="cc13f-141">Once the data is laid out on the input side, you must make sure that your query is partitioned.</span></span> <span data-ttu-id="cc13f-142">Для этого на каждом этапе используется параметр **Partition By**.</span><span class="sxs-lookup"><span data-stu-id="cc13f-142">This requires you to use **Partition By** in all the steps.</span></span> <span data-ttu-id="cc13f-143">Этапов может быть несколько, но на каждом из них должен использоваться один и тот же ключ.</span><span class="sxs-lookup"><span data-stu-id="cc13f-143">Multiple steps are allowed, but they all must be partitioned by the same key.</span></span> <span data-ttu-id="cc13f-144">Сейчас для выполнения заданий с параллелизмом необходимо использовать значение **PartitionId** в качестве ключа секционирования.</span><span class="sxs-lookup"><span data-stu-id="cc13f-144">Currently, the partitioning key must be set to **PartitionId** in order for the job to be fully parallel.</span></span>  

3. <span data-ttu-id="cc13f-145">На данном этапе секционированные выходные данные поддерживаются только концентраторами событий и хранилищами BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="cc13f-145">Currently only event hubs and blob storage support partitioned output.</span></span> <span data-ttu-id="cc13f-146">Для выходных данных концентраторов событий необходимо указать значение **PartitionId** в качестве ключа секции.</span><span class="sxs-lookup"><span data-stu-id="cc13f-146">For event hub output, you must configure the partition key to be **PartitionId**.</span></span> <span data-ttu-id="cc13f-147">Для выходных данных хранилища BLOB-объектов ничего делать не нужно.</span><span class="sxs-lookup"><span data-stu-id="cc13f-147">For blob storage output, you don't have to do anything.</span></span>  

4. <span data-ttu-id="cc13f-148">Число секций входных данных должно совпадать с числом секций выходных данных.</span><span class="sxs-lookup"><span data-stu-id="cc13f-148">The number of input partitions must equal the number of output partitions.</span></span> <span data-ttu-id="cc13f-149">В настоящее время выходные данные хранилища BLOB-объектов не поддерживают секционирование.</span><span class="sxs-lookup"><span data-stu-id="cc13f-149">Blob storage output doesn't currently support partitions.</span></span> <span data-ttu-id="cc13f-150">В этом нет ничего страшного, так как они наследуют схему секционирования вышестоящего запроса.</span><span class="sxs-lookup"><span data-stu-id="cc13f-150">But that's okay, because it inherits the partitioning scheme of the upstream query.</span></span> <span data-ttu-id="cc13f-151">Примеры значений секций, позволяющие выполнять задания с полной параллельной обработкой:</span><span class="sxs-lookup"><span data-stu-id="cc13f-151">Here are examples of partition values that allow a fully parallel job:</span></span>  

   * <span data-ttu-id="cc13f-152">8 секций входных данных концентраторов событий и 8 секций выходных данных концентраторов событий;</span><span class="sxs-lookup"><span data-stu-id="cc13f-152">8 event hub input partitions and 8 event hub output partitions</span></span>
   * <span data-ttu-id="cc13f-153">8 секций входных данных концентраторов событий и выходные данные хранилища BLOB-объектов;</span><span class="sxs-lookup"><span data-stu-id="cc13f-153">8 event hub input partitions and blob storage output</span></span>  
   * <span data-ttu-id="cc13f-154">8 секций входных данных хранилища BLOB-объектов и выходные данные хранилища BLOB-объектов;</span><span class="sxs-lookup"><span data-stu-id="cc13f-154">8 blob storage input partitions and blob storage output</span></span>  
   * <span data-ttu-id="cc13f-155">8 секций входных данных хранилища BLOB-объектов и 8 секций выходных данных концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="cc13f-155">8 blob storage input partitions and 8 event hub output partitions</span></span>  

<span data-ttu-id="cc13f-156">Далее рассмотрим примеры сценариев с усложненным параллелизмом.</span><span class="sxs-lookup"><span data-stu-id="cc13f-156">The following sections discuss some example scenarios that are embarrassingly parallel.</span></span>

### <a name="simple-query"></a><span data-ttu-id="cc13f-157">Простой запрос</span><span class="sxs-lookup"><span data-stu-id="cc13f-157">Simple query</span></span>

* <span data-ttu-id="cc13f-158">Входные данные — концентратор событий с 8 секциями.</span><span class="sxs-lookup"><span data-stu-id="cc13f-158">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="cc13f-159">Выходные данные — концентратор событий с 8 секциями.</span><span class="sxs-lookup"><span data-stu-id="cc13f-159">Output: Event hub with 8 partitions</span></span>

<span data-ttu-id="cc13f-160">Запрос:</span><span class="sxs-lookup"><span data-stu-id="cc13f-160">Query:</span></span>

    SELECT TollBoothId
    FROM Input1 Partition By PartitionId
    WHERE TollBoothId > 100

<span data-ttu-id="cc13f-161">Этот запрос является простым фильтром.</span><span class="sxs-lookup"><span data-stu-id="cc13f-161">This query is a simple filter.</span></span> <span data-ttu-id="cc13f-162">Поэтому нам не нужно беспокоиться о секционировании входных данных, которые передаются в концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="cc13f-162">Therefore, we don't need to worry about partitioning the input that is being sent to the event hub.</span></span> <span data-ttu-id="cc13f-163">Обратите внимание, что запрос содержит значение **Partition By PartitionId**, поэтому он удовлетворяет требованию 2, указанному выше.</span><span class="sxs-lookup"><span data-stu-id="cc13f-163">Notice that the query includes **Partition By PartitionId**, so it fulfills requirement #2 from earlier.</span></span> <span data-ttu-id="cc13f-164">Выходные данные концентраторов событий необходимо настроить, указав значение **PartitionId** в качестве ключа секции.</span><span class="sxs-lookup"><span data-stu-id="cc13f-164">For the output, we need to configure the event hub output in the job to have the parition key set to **PartitionId**.</span></span> <span data-ttu-id="cc13f-165">Последняя проверка: число секций входных данных должно быть равно числу секций выходных данных.</span><span class="sxs-lookup"><span data-stu-id="cc13f-165">One last check is to make sure that the number of input partitions is equal to the number of output partitions.</span></span>

### <a name="query-with-a-grouping-key"></a><span data-ttu-id="cc13f-166">Запрос с ключом группирования</span><span class="sxs-lookup"><span data-stu-id="cc13f-166">Query with a grouping key</span></span>

* <span data-ttu-id="cc13f-167">Входные данные — концентратор событий с 8 секциями.</span><span class="sxs-lookup"><span data-stu-id="cc13f-167">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="cc13f-168">Выходные данные — хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="cc13f-168">Output: Blob storage</span></span>

<span data-ttu-id="cc13f-169">Запрос:</span><span class="sxs-lookup"><span data-stu-id="cc13f-169">Query:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="cc13f-170">Этот запрос содержит ключ группирования.</span><span class="sxs-lookup"><span data-stu-id="cc13f-170">This query has a grouping key.</span></span> <span data-ttu-id="cc13f-171">Поэтому этот ключ должен обрабатываться тем же экземпляром запроса. Это означает, что события нужно отправлять в концентраторы событий с делением на секции.</span><span class="sxs-lookup"><span data-stu-id="cc13f-171">Therefore, the same key needs to be processed by the same query instance, which means that events must be sent to the event hub in a partitioned manner.</span></span> <span data-ttu-id="cc13f-172">Какой ключ следует использовать?</span><span class="sxs-lookup"><span data-stu-id="cc13f-172">But which key should be used?</span></span> <span data-ttu-id="cc13f-173">Ключ **PartitionId** определяет логику задания.</span><span class="sxs-lookup"><span data-stu-id="cc13f-173">**PartitionId** is a job-logic concept.</span></span> <span data-ttu-id="cc13f-174">Лучше обратить внимание на ключ **TollBoothId**. В качестве значения ключа **PartitionKey** данных события должен быть указан **TollBoothId**.</span><span class="sxs-lookup"><span data-stu-id="cc13f-174">The key we actually care about is **TollBoothId**, so the **PartitionKey** value of the event data should be **TollBoothId**.</span></span> <span data-ttu-id="cc13f-175">В запросе задайте для параметра **Partition By** значение **PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="cc13f-175">We do this in the query by setting **Partition By** to **PartitionId**.</span></span> <span data-ttu-id="cc13f-176">Так как выходными данными является хранилище BLOB-объектов, не нужно беспокоиться о настройке значения ключа секции, как описано в требовании 4.</span><span class="sxs-lookup"><span data-stu-id="cc13f-176">Since the output is blob storage, we don't need to worry about configuring a partition key value, as per requirement #4.</span></span>

### <a name="multi-step-query-with-a-grouping-key"></a><span data-ttu-id="cc13f-177">Многоэтапный запрос с ключом группирования</span><span class="sxs-lookup"><span data-stu-id="cc13f-177">Multi-step query with a grouping key</span></span>
* <span data-ttu-id="cc13f-178">Входные данные — концентратор событий с 8 секциями.</span><span class="sxs-lookup"><span data-stu-id="cc13f-178">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="cc13f-179">Выходные данные — экземпляр концентратора событий с 8 секциями.</span><span class="sxs-lookup"><span data-stu-id="cc13f-179">Output: Event hub instance with 8 partitions</span></span>

<span data-ttu-id="cc13f-180">Запрос:</span><span class="sxs-lookup"><span data-stu-id="cc13f-180">Query:</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="cc13f-181">Этот запрос содержит ключ группирования, а значит, этот ключ должен обрабатываться тем же экземпляром запроса.</span><span class="sxs-lookup"><span data-stu-id="cc13f-181">This query has a grouping key, so the same key needs to be processed by the same query instance.</span></span> <span data-ttu-id="cc13f-182">Мы используем ту же стратегию, что и для предыдущего примера.</span><span class="sxs-lookup"><span data-stu-id="cc13f-182">We can use the same strategy as in the previous example.</span></span> <span data-ttu-id="cc13f-183">В данном случае запрос состоит из нескольких этапов.</span><span class="sxs-lookup"><span data-stu-id="cc13f-183">In this case, the query has multiple steps.</span></span> <span data-ttu-id="cc13f-184">Указан ли на каждом этапе параметр **Partition By PartitionId**?</span><span class="sxs-lookup"><span data-stu-id="cc13f-184">Does each step have **Partition By PartitionId**?</span></span> <span data-ttu-id="cc13f-185">Да, поэтому этот запрос удовлетворяет требование 3.</span><span class="sxs-lookup"><span data-stu-id="cc13f-185">Yes, so the query fulfills requirement #3.</span></span> <span data-ttu-id="cc13f-186">Для выходных данных нужно указать ключ секции **PartitionId**, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="cc13f-186">For the output, we need to set the partition key to **PartitionId**, as discussed earlier.</span></span> <span data-ttu-id="cc13f-187">Также можно увидеть, что они имеют то же количество секций, что и входные данные.</span><span class="sxs-lookup"><span data-stu-id="cc13f-187">We can also see that it has the same number of partitions as the input.</span></span>

## <a name="example-scenarios-that-are-not-embarrassingly-parallel"></a><span data-ttu-id="cc13f-188">Примеры сценариев *без* усложненного параллелизма</span><span class="sxs-lookup"><span data-stu-id="cc13f-188">Example scenarios that are *not* embarrassingly parallel</span></span>

<span data-ttu-id="cc13f-189">В предыдущем разделе мы рассмотрели сценарии с усложненным параллелизмом.</span><span class="sxs-lookup"><span data-stu-id="cc13f-189">In the previous section, we showed some embarrassingly parallel scenarios.</span></span> <span data-ttu-id="cc13f-190">В этом разделе обсуждаются сценарии, которые не соответствуют всем показателям усложненного параллелизма.</span><span class="sxs-lookup"><span data-stu-id="cc13f-190">In this section, we discuss scenarios that don't meet all the requirements to be embarrassingly parallel.</span></span> 

### <a name="mismatched-partition-count"></a><span data-ttu-id="cc13f-191">Несоответствие в числе секций</span><span class="sxs-lookup"><span data-stu-id="cc13f-191">Mismatched partition count</span></span>
* <span data-ttu-id="cc13f-192">Входные данные — концентратор событий с 8 секциями.</span><span class="sxs-lookup"><span data-stu-id="cc13f-192">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="cc13f-193">Выходные данные — концентратор событий с 32 секциями.</span><span class="sxs-lookup"><span data-stu-id="cc13f-193">Output: Event hub with 32 partitions</span></span>

<span data-ttu-id="cc13f-194">В этом случае тип запроса не имеет значения.</span><span class="sxs-lookup"><span data-stu-id="cc13f-194">In this case, it doesn't matter what the query is.</span></span> <span data-ttu-id="cc13f-195">Если число секций входных данных не совпадает с числом секций выходных данных, топология не является топологией с усложненным параллелизмом.</span><span class="sxs-lookup"><span data-stu-id="cc13f-195">If the input partition count doesn't match the output partition count, the topology isn't embarrassingly parallel.</span></span>

### <a name="not-using-event-hubs-or-blob-storage-as-output"></a><span data-ttu-id="cc13f-196">Для выходных данных не используются концентраторы событий или хранилище BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="cc13f-196">Not using event hubs or blob storage as output</span></span>
* <span data-ttu-id="cc13f-197">Входные данные — концентратор событий с 8 секциями.</span><span class="sxs-lookup"><span data-stu-id="cc13f-197">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="cc13f-198">Выходные данные — PowerBI.</span><span class="sxs-lookup"><span data-stu-id="cc13f-198">Output: PowerBI</span></span>

<span data-ttu-id="cc13f-199">В настоящее время выходные данные PowerBI не поддерживают секционирование.</span><span class="sxs-lookup"><span data-stu-id="cc13f-199">PowerBI output doesn't currently support partitioning.</span></span> <span data-ttu-id="cc13f-200">Таким образом этот сценарий не считается сценарием с усложненным параллелизмом.</span><span class="sxs-lookup"><span data-stu-id="cc13f-200">Therefore, this scenario is not embarrassingly parallel.</span></span>

### <a name="multi-step-query-with-different-partition-by-values"></a><span data-ttu-id="cc13f-201">Многоэтапный запрос с разными значениями параметра Partition By</span><span class="sxs-lookup"><span data-stu-id="cc13f-201">Multi-step query with different Partition By values</span></span>
* <span data-ttu-id="cc13f-202">Входные данные — концентратор событий с 8 секциями.</span><span class="sxs-lookup"><span data-stu-id="cc13f-202">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="cc13f-203">Выходные данные — концентратор событий с 8 секциями.</span><span class="sxs-lookup"><span data-stu-id="cc13f-203">Output: Event hub with 8 partitions</span></span>

<span data-ttu-id="cc13f-204">Запрос:</span><span class="sxs-lookup"><span data-stu-id="cc13f-204">Query:</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By TollBoothId
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="cc13f-205">Как видите, на втором этапе в качестве ключа секционирования используется **TollBoothId** .</span><span class="sxs-lookup"><span data-stu-id="cc13f-205">As you can see, the second step uses **TollBoothId** as the partitioning key.</span></span> <span data-ttu-id="cc13f-206">Он не совпадает с ключом в первом шаге, а значит, потребует перетасовки.</span><span class="sxs-lookup"><span data-stu-id="cc13f-206">This step is not the same as the first step, and it therefore requires us to do a shuffle.</span></span> 

<span data-ttu-id="cc13f-207">Мы рассмотрели несколько примеров заданий Stream Analytics, соответствующих и не соответствующих критериям топологии с усложненным параллелизмом.</span><span class="sxs-lookup"><span data-stu-id="cc13f-207">The preceding examples show some Stream Analytics jobs that conform to (or don't) an embarrassingly parallel topology.</span></span> <span data-ttu-id="cc13f-208">При соответствии, задания будут иметь максимально возможное для них масштабирование.</span><span class="sxs-lookup"><span data-stu-id="cc13f-208">If they do conform, they have the potential for maximum scale.</span></span> <span data-ttu-id="cc13f-209">Для заданий, не соответствующих ни одному из этих профилей, в дальнейшем будут выпущены обновления в отношении масштабирования.</span><span class="sxs-lookup"><span data-stu-id="cc13f-209">For jobs that don't fit one of these profiles, scaling guidance will be available in future updates.</span></span> <span data-ttu-id="cc13f-210">А пока придерживайтесь описанных ниже рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="cc13f-210">For now, use the general guidance in the following sections.</span></span>

## <a name="calculate-the-maximum-streaming-units-of-a-job"></a><span data-ttu-id="cc13f-211">Расчет максимального количества единиц потоковой передачи для задания</span><span class="sxs-lookup"><span data-stu-id="cc13f-211">Calculate the maximum streaming units of a job</span></span>
<span data-ttu-id="cc13f-212">Общее число единиц потоковой передачи, которое можно использовать заданием Stream Analytics, зависит от числа шагов в запросе, определенных для задания, и количества разделов для каждого шага.</span><span class="sxs-lookup"><span data-stu-id="cc13f-212">The total number of streaming units that can be used by a Stream Analytics job depends on the number of steps in the query defined for the job and the number of partitions for each step.</span></span>

### <a name="steps-in-a-query"></a><span data-ttu-id="cc13f-213">Шаги в запросе</span><span class="sxs-lookup"><span data-stu-id="cc13f-213">Steps in a query</span></span>
<span data-ttu-id="cc13f-214">Запрос может иметь один или несколько шагов.</span><span class="sxs-lookup"><span data-stu-id="cc13f-214">A query can have one or many steps.</span></span> <span data-ttu-id="cc13f-215">Каждый шаг — это вложенный запрос, определенный с помощью ключевого слова **WITH**.</span><span class="sxs-lookup"><span data-stu-id="cc13f-215">Each step is a subquery defined by the **WITH** keyword.</span></span> <span data-ttu-id="cc13f-216">Запрос за рамками ключевого слова **WITH** (только один запрос) также учитывается в качестве шага (например, инструкция **SELECT** в следующем запросе).</span><span class="sxs-lookup"><span data-stu-id="cc13f-216">The query that is outside the **WITH** keyword (one query only) is also counted as a step, such as the **SELECT** statement in the following query:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute,3), TollBoothId

<span data-ttu-id="cc13f-217">Этот запрос включает 2 шага.</span><span class="sxs-lookup"><span data-stu-id="cc13f-217">This query has two steps.</span></span>

> [!NOTE]
> <span data-ttu-id="cc13f-218">Этот запрос будет описан далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="cc13f-218">This query is discussed in more detail later in the article.</span></span>
>  

### <a name="partition-a-step"></a><span data-ttu-id="cc13f-219">Разделы шага</span><span class="sxs-lookup"><span data-stu-id="cc13f-219">Partition a step</span></span>
<span data-ttu-id="cc13f-220">Разделение шага требует наличия следующих условий.</span><span class="sxs-lookup"><span data-stu-id="cc13f-220">Partitioning a step requires the following conditions:</span></span>

* <span data-ttu-id="cc13f-221">Источник входных данных должен быть секционирован.</span><span class="sxs-lookup"><span data-stu-id="cc13f-221">The input source must be partitioned.</span></span> 
* <span data-ttu-id="cc13f-222">Инструкция **SELECT** запроса должна читаться из разделенного источника входных данных.</span><span class="sxs-lookup"><span data-stu-id="cc13f-222">The **SELECT** statement of the query must read from a partitioned input source.</span></span>
* <span data-ttu-id="cc13f-223">Запрос внутри шага должен включать ключевое слово **Partition By**.</span><span class="sxs-lookup"><span data-stu-id="cc13f-223">The query within the step must have the **Partition By** keyword.</span></span>

<span data-ttu-id="cc13f-224">Если запрос разделен, входные данные событий будут обработаны и объединены в отдельные группы секции, а выходные данные событий будут сгенерированы для каждой из групп.</span><span class="sxs-lookup"><span data-stu-id="cc13f-224">When a query is partitioned, the input events are processed and aggregated in separate partition groups, and outputs events are generated for each of the groups.</span></span> <span data-ttu-id="cc13f-225">Если желательно иметь объединенный запрос, необходимо создать второй неразделенный шаг для объединения.</span><span class="sxs-lookup"><span data-stu-id="cc13f-225">If you want a combined aggregate, you must create a second non-partitioned step to aggregate.</span></span>

### <a name="calculate-the-max-streaming-units-for-a-job"></a><span data-ttu-id="cc13f-226">Рассчитайте максимальное количество единиц потоковой передачи для задания</span><span class="sxs-lookup"><span data-stu-id="cc13f-226">Calculate the max streaming units for a job</span></span>
<span data-ttu-id="cc13f-227">Все несекционированные шаги можно масштабировать до шести единиц потоковой передачи для задания Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="cc13f-227">All non-partitioned steps together can scale up to six streaming units (SUs) for a Stream Analytics job.</span></span> <span data-ttu-id="cc13f-228">Для добавления дополнительных единиц потоковой передачи данных шаг должен быть секционирован.</span><span class="sxs-lookup"><span data-stu-id="cc13f-228">To add SUs, a step must be partitioned.</span></span> <span data-ttu-id="cc13f-229">Каждая секция может включать шесть единиц потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="cc13f-229">Each partition can have six SUs.</span></span>

<table border="1">
<tr><th><span data-ttu-id="cc13f-230">Запрос</span><span class="sxs-lookup"><span data-stu-id="cc13f-230">Query</span></span></th><th><span data-ttu-id="cc13f-231">Максимальное количество единиц потоковой передачи для задания</span><span class="sxs-lookup"><span data-stu-id="cc13f-231">Max SUs for the job</span></span></th></td>

<tr><td>
<ul>
<li><span data-ttu-id="cc13f-232">Запрос содержит один шаг.</span><span class="sxs-lookup"><span data-stu-id="cc13f-232">The query contains one step.</span></span></li>
<li><span data-ttu-id="cc13f-233">Шаг не секционирован.</span><span class="sxs-lookup"><span data-stu-id="cc13f-233">The step is not partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="cc13f-234">6</span><span class="sxs-lookup"><span data-stu-id="cc13f-234">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="cc13f-235">Поток входных данных секционирован по 3.</span><span class="sxs-lookup"><span data-stu-id="cc13f-235">The input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="cc13f-236">Запрос содержит один шаг.</span><span class="sxs-lookup"><span data-stu-id="cc13f-236">The query contains one step.</span></span></li>
<li><span data-ttu-id="cc13f-237">Шаг является секционированным.</span><span class="sxs-lookup"><span data-stu-id="cc13f-237">The step is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="cc13f-238">18</span><span class="sxs-lookup"><span data-stu-id="cc13f-238">18</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="cc13f-239">Запрос состоит из двух шагов.</span><span class="sxs-lookup"><span data-stu-id="cc13f-239">The query contains two steps.</span></span></li>
<li><span data-ttu-id="cc13f-240">Ни один из шагов не секционирован.</span><span class="sxs-lookup"><span data-stu-id="cc13f-240">Neither of the steps is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="cc13f-241">6</span><span class="sxs-lookup"><span data-stu-id="cc13f-241">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="cc13f-242">Поток входных данных секционирован по 3.</span><span class="sxs-lookup"><span data-stu-id="cc13f-242">The input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="cc13f-243">Запрос состоит из двух шагов.</span><span class="sxs-lookup"><span data-stu-id="cc13f-243">The query contains two steps.</span></span> <span data-ttu-id="cc13f-244">Входной шаг секционирован, а второй шаг — нет.</span><span class="sxs-lookup"><span data-stu-id="cc13f-244">The input step is partitioned and the second step is not.</span></span></li>
<li><span data-ttu-id="cc13f-245">Инструкция <strong>SELECT</strong> считывает из секционированных входных данных.</span><span class="sxs-lookup"><span data-stu-id="cc13f-245">The <strong>SELECT</strong> statement reads from the partitioned input.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="cc13f-246">24 (18 и 6 секционированных и несекционированных шагов соответственно)</span><span class="sxs-lookup"><span data-stu-id="cc13f-246">24 (18 for partitioned steps + 6 for non-partitioned steps)</span></span></td></tr>
</table>

### <a name="examples-of-scaling"></a><span data-ttu-id="cc13f-247">Примеры масштабирования</span><span class="sxs-lookup"><span data-stu-id="cc13f-247">Examples of scaling</span></span>

<span data-ttu-id="cc13f-248">Следующий запрос вычисляет количество машин, проходящих через пропускной пункт с тремя пунктами для оплаты и пропускной способности три минуты для каждого пункта.</span><span class="sxs-lookup"><span data-stu-id="cc13f-248">The following query calculates the number of cars within a three-minute window going through a toll station that has three tollbooths.</span></span> <span data-ttu-id="cc13f-249">Этот запрос можно масштабировать до шести единиц потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="cc13f-249">This query can be scaled up to six SUs.</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="cc13f-250">Чтобы использовать дополнительные единицы потоковой передачи для запроса, входной поток данных и запрос должны быть секционированы.</span><span class="sxs-lookup"><span data-stu-id="cc13f-250">To use more SUs for the query, both the input data stream and the query must be partitioned.</span></span> <span data-ttu-id="cc13f-251">При наличии секции потока данных, равной 3, следующий измененный запрос можно масштабировать до 18 единиц потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="cc13f-251">Since the data stream partition is set to 3, the following modified query can be scaled up to 18 SUs:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="cc13f-252">Если запрос секционирован, входные данные событий будут обработаны и объединены в отдельные группы секций.</span><span class="sxs-lookup"><span data-stu-id="cc13f-252">When a query is partitioned, the input events are processed and aggregated in separate partition groups.</span></span> <span data-ttu-id="cc13f-253">Кроме того, для каждой из групп будут сформированы выходные данные событий.</span><span class="sxs-lookup"><span data-stu-id="cc13f-253">Output events are also generated for each of the groups.</span></span> <span data-ttu-id="cc13f-254">Секционирование может вызвать некоторые непредвиденные результаты, если поле **GROUP BY** не является ключом секции во входном потоке данных.</span><span class="sxs-lookup"><span data-stu-id="cc13f-254">Partitioning can cause some unexpected results when the **GROUP BY** field is not the partition key in the input data stream.</span></span> <span data-ttu-id="cc13f-255">Например, поле **TollBoothId** в предыдущем запросе не является ключом секции **Input1**.</span><span class="sxs-lookup"><span data-stu-id="cc13f-255">For example, the **TollBoothId** field in the previous query is not the partition key of **Input1**.</span></span> <span data-ttu-id="cc13f-256">В результате данные из пункта 1 можно распределить между несколькими секциями.</span><span class="sxs-lookup"><span data-stu-id="cc13f-256">The result is that the data from TollBooth #1 can be spread in multiple partitions.</span></span>

<span data-ttu-id="cc13f-257">Каждая из секций **Input1** будет обрабатываться отдельно с помощью Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="cc13f-257">Each of the **Input1** partitions will be processed separately by Stream Analytics.</span></span> <span data-ttu-id="cc13f-258">В результате будет создаваться несколько записей для автомобиля, проходящего через один и тот же пункт.</span><span class="sxs-lookup"><span data-stu-id="cc13f-258">As a result, multiple records of the car count for the same tollbooth in the same Tumbling window will be created.</span></span> <span data-ttu-id="cc13f-259">Если нельзя изменить ключ секции ввода, эту проблему можно устранить, добавив несекционированные действия, например:</span><span class="sxs-lookup"><span data-stu-id="cc13f-259">If the input partition key can't be changed, this problem can be fixed by adding a non-partition step, as in the following example:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="cc13f-260">Этот запрос можно увеличить до 24 единиц потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="cc13f-260">This query can be scaled to 24 SUs.</span></span>

> [!NOTE]
> <span data-ttu-id="cc13f-261">При объединении двух потоков убедитесь, что потоки разделены с помощью ключа секции столбца, используемого для объединения.</span><span class="sxs-lookup"><span data-stu-id="cc13f-261">If you are joining two streams, make sure that the streams are partitioned by the partition key of the column that you use to create the joins.</span></span> <span data-ttu-id="cc13f-262">Также убедитесь, что количество секций в обоих потоках одинаковое.</span><span class="sxs-lookup"><span data-stu-id="cc13f-262">Also make sure that you have the same number of partitions in both streams.</span></span>
> 
> 

## <a name="configure-stream-analytics-streaming-units"></a><span data-ttu-id="cc13f-263">Настройка единиц потоковой передачи Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cc13f-263">Configure Stream Analytics streaming units</span></span>

1. <span data-ttu-id="cc13f-264">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cc13f-264">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="cc13f-265">В списке ресурсов найдите задание Stream Analytics для масштабирования и откройте его.</span><span class="sxs-lookup"><span data-stu-id="cc13f-265">In the list of resources, find the Stream Analytics job that you want to scale and then open it.</span></span>
3. <span data-ttu-id="cc13f-266">В колонке задания в разделе **Параметры** щелкните **Масштаб**.</span><span class="sxs-lookup"><span data-stu-id="cc13f-266">In the job blade, under **Configure**, click **Scale**.</span></span>

    ![Настройка задания Stream Analytics на портале Azure][img.stream.analytics.preview.portal.settings.scale]

4. <span data-ttu-id="cc13f-268">Используйте ползунок, чтобы задать количество единиц потоковой передачи для задания.</span><span class="sxs-lookup"><span data-stu-id="cc13f-268">Use the slider to set the SUs for the job.</span></span> <span data-ttu-id="cc13f-269">Обратите внимание, что существуют определенные ограничения параметров единиц потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="cc13f-269">Notice that you are limited to specific SU settings.</span></span>


## <a name="monitor-job-performance"></a><span data-ttu-id="cc13f-270">Мониторинг производительности задания</span><span class="sxs-lookup"><span data-stu-id="cc13f-270">Monitor job performance</span></span>
<span data-ttu-id="cc13f-271">На портале Azure можно отслеживать пропускную способность задания:</span><span class="sxs-lookup"><span data-stu-id="cc13f-271">Using the Azure portal, you can track the throughput of a job:</span></span>

![Отслеживание заданий Azure Stream Analytics][img.stream.analytics.monitor.job]

<span data-ttu-id="cc13f-273">Рассчитайте ожидаемую пропускную способность рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="cc13f-273">Calculate the expected throughput of the workload.</span></span> <span data-ttu-id="cc13f-274">Если пропускная способность меньше, чем ожидалось, настройте входную секцию и запрос, а также добавьте в задание дополнительные единицы потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="cc13f-274">If the throughput is less than expected, tune the input partition, tune the query, and add SUs to your job.</span></span>


## <a name="visualize-stream-analytics-throughput-at-scale-the-raspberry-pi-scenario"></a><span data-ttu-id="cc13f-275">Визуализация масштабирования пропускной способности службы Stream Analytics — сценарий для компьютера Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="cc13f-275">Visualize Stream Analytics throughput at scale: the Raspberry Pi scenario</span></span>
<span data-ttu-id="cc13f-276">Чтобы понять, как масштабируется пропускная способность заданий Stream Analytics, выполним эксперимент с использованием входных данных с устройства Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="cc13f-276">To help you understand how Stream Analytics jobs scale, we performed an experiment based on input from a Raspberry Pi device.</span></span> <span data-ttu-id="cc13f-277">Этот эксперимент поможет увидеть влияние на пропускную способность нескольких единиц потоковой передачи и секций.</span><span class="sxs-lookup"><span data-stu-id="cc13f-277">This experiment let us see the effect on throughput of multiple streaming units and partitions.</span></span>

<span data-ttu-id="cc13f-278">В этом случае устройство отправляет данные датчиков (клиентов) в концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="cc13f-278">In this scenario, the device sends sensor data (clients) to an event hub.</span></span> <span data-ttu-id="cc13f-279">Служба Streaming Analytics обрабатывает эти данные и отправляет предупреждение или статистические сведения в качестве выходных данных на другой концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="cc13f-279">Streaming Analytics processes the data and sends an alert or statistics as an output to another event hub.</span></span> 

<span data-ttu-id="cc13f-280">Клиент отправляет данные датчиков в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="cc13f-280">The client sends sensor data in JSON format.</span></span> <span data-ttu-id="cc13f-281">Выходные данные также находятся в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="cc13f-281">The data output is also in JSON format.</span></span> <span data-ttu-id="cc13f-282">Ниже приведен пример данных.</span><span class="sxs-lookup"><span data-stu-id="cc13f-282">The data looks like this:</span></span>

    {"devicetime":"2014-12-11T02:24:56.8850110Z","hmdt":42.7,"temp":72.6,"prss":98187.75,"lght":0.38,"dspl":"R-PI Olivier's Office"}

<span data-ttu-id="cc13f-283">Следующий запрос используется для отправки предупреждения при выключении света:</span><span class="sxs-lookup"><span data-stu-id="cc13f-283">The following query is used to send an alert when a light is switched off:</span></span>

    SELECT AVG(lght),
     "LightOff" as AlertText
    FROM input TIMESTAMP
    BY devicetime
     WHERE
        lght< 0.05 GROUP BY TumblingWindow(second, 1)

### <a name="measure-throughput"></a><span data-ttu-id="cc13f-284">Измерения пропускной способности</span><span class="sxs-lookup"><span data-stu-id="cc13f-284">Measure throughput</span></span>

<span data-ttu-id="cc13f-285">Пропускная способность в этом контексте — это объем входных данных, обрабатываемых службой Stream Analytics в определенный промежуток времени.</span><span class="sxs-lookup"><span data-stu-id="cc13f-285">In this context, throughput is the amount of input data processed by Stream Analytics in a fixed amount of time.</span></span> <span data-ttu-id="cc13f-286">(Мы измеряли за 10 минут.) Чтобы обеспечить оптимальную пропускную способность для обработки входных данных, поток входных данных и запрос должны были секционированы.</span><span class="sxs-lookup"><span data-stu-id="cc13f-286">(We measured for 10 minutes.) To achieve the best processing throughput for the input data, both the data stream input and the query were  partitioned.</span></span> <span data-ttu-id="cc13f-287">В запрос также включается **COUNT()**, что позволяет подсчитать число обработанных событий ввода.</span><span class="sxs-lookup"><span data-stu-id="cc13f-287">We included **COUNT()** in the query to measure how many input events were processed.</span></span> <span data-ttu-id="cc13f-288">Чтобы убедиться, что задание не просто ожидает поступления событий ввода, в каждую секцию концентратора событий ввода были предварительно загружены входные данные в объеме 300 МБ.</span><span class="sxs-lookup"><span data-stu-id="cc13f-288">To make sure the job was not simply waiting for input events to come, each partition of the input event hub was preloaded with about 300 MB of input data.</span></span>

<span data-ttu-id="cc13f-289">В следующей таблице приведены результаты с увеличением количества единиц потоковой передачи и соответствующие данные о числе секций в концентраторах событий.</span><span class="sxs-lookup"><span data-stu-id="cc13f-289">The following table shows the results we saw when we increased the number of streaming units and the corresponding partition counts in event hubs.</span></span>  

<table border="1">
<tr><th><span data-ttu-id="cc13f-290">Секции ввода</span><span class="sxs-lookup"><span data-stu-id="cc13f-290">Input Partitions</span></span></th><th><span data-ttu-id="cc13f-291">Секции вывода</span><span class="sxs-lookup"><span data-stu-id="cc13f-291">Output Partitions</span></span></th><th><span data-ttu-id="cc13f-292">Единицы потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="cc13f-292">Streaming Units</span></span></th><th><span data-ttu-id="cc13f-293">Поддерживаемая пропускная способность</span><span class="sxs-lookup"><span data-stu-id="cc13f-293">Sustained Throughput</span></span>
</th></td>

<tr><td><span data-ttu-id="cc13f-294">12</span><span class="sxs-lookup"><span data-stu-id="cc13f-294">12</span></span></td>
<td><span data-ttu-id="cc13f-295">12</span><span class="sxs-lookup"><span data-stu-id="cc13f-295">12</span></span></td>
<td><span data-ttu-id="cc13f-296">6</span><span class="sxs-lookup"><span data-stu-id="cc13f-296">6</span></span></td>
<td><span data-ttu-id="cc13f-297">4,06 МБ/с</span><span class="sxs-lookup"><span data-stu-id="cc13f-297">4.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="cc13f-298">12</span><span class="sxs-lookup"><span data-stu-id="cc13f-298">12</span></span></td>
<td><span data-ttu-id="cc13f-299">12</span><span class="sxs-lookup"><span data-stu-id="cc13f-299">12</span></span></td>
<td><span data-ttu-id="cc13f-300">12</span><span class="sxs-lookup"><span data-stu-id="cc13f-300">12</span></span></td>
<td><span data-ttu-id="cc13f-301">8,06 МБ/с</span><span class="sxs-lookup"><span data-stu-id="cc13f-301">8.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="cc13f-302">48</span><span class="sxs-lookup"><span data-stu-id="cc13f-302">48</span></span></td>
<td><span data-ttu-id="cc13f-303">48</span><span class="sxs-lookup"><span data-stu-id="cc13f-303">48</span></span></td>
<td><span data-ttu-id="cc13f-304">48</span><span class="sxs-lookup"><span data-stu-id="cc13f-304">48</span></span></td>
<td><span data-ttu-id="cc13f-305">38,32 МБ/с</span><span class="sxs-lookup"><span data-stu-id="cc13f-305">38.32 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="cc13f-306">192</span><span class="sxs-lookup"><span data-stu-id="cc13f-306">192</span></span></td>
<td><span data-ttu-id="cc13f-307">192</span><span class="sxs-lookup"><span data-stu-id="cc13f-307">192</span></span></td>
<td><span data-ttu-id="cc13f-308">192</span><span class="sxs-lookup"><span data-stu-id="cc13f-308">192</span></span></td>
<td><span data-ttu-id="cc13f-309">172,67 МБ/с</span><span class="sxs-lookup"><span data-stu-id="cc13f-309">172.67 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="cc13f-310">480</span><span class="sxs-lookup"><span data-stu-id="cc13f-310">480</span></span></td>
<td><span data-ttu-id="cc13f-311">480</span><span class="sxs-lookup"><span data-stu-id="cc13f-311">480</span></span></td>
<td><span data-ttu-id="cc13f-312">480</span><span class="sxs-lookup"><span data-stu-id="cc13f-312">480</span></span></td>
<td><span data-ttu-id="cc13f-313">454,27 МБ/с</span><span class="sxs-lookup"><span data-stu-id="cc13f-313">454.27 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="cc13f-314">720</span><span class="sxs-lookup"><span data-stu-id="cc13f-314">720</span></span></td>
<td><span data-ttu-id="cc13f-315">720</span><span class="sxs-lookup"><span data-stu-id="cc13f-315">720</span></span></td>
<td><span data-ttu-id="cc13f-316">720</span><span class="sxs-lookup"><span data-stu-id="cc13f-316">720</span></span></td>
<td><span data-ttu-id="cc13f-317">609,69 МБ/с</span><span class="sxs-lookup"><span data-stu-id="cc13f-317">609.69 MB/s</span></span></td>
</tr>
</table>

<span data-ttu-id="cc13f-318">На следующей диаграмме отображена визуализация связи между числом единиц пропускной способности и пропускной способностью.</span><span class="sxs-lookup"><span data-stu-id="cc13f-318">And the following graph shows a visualization of the relationship between SUs and throughput.</span></span>

![img.stream.analytics.perfgraph][img.stream.analytics.perfgraph]

## <a name="get-help"></a><span data-ttu-id="cc13f-320">Получение справки</span><span class="sxs-lookup"><span data-stu-id="cc13f-320">Get help</span></span>
<span data-ttu-id="cc13f-321">За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="cc13f-321">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc13f-322">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cc13f-322">Next steps</span></span>
* [<span data-ttu-id="cc13f-323">Введение в Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cc13f-323">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="cc13f-324">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cc13f-324">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="cc13f-325">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cc13f-325">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="cc13f-326">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cc13f-326">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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

