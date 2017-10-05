---
title: "Azure Stream Analytics: оптимизация задания для эффективного использования единиц потоковой передачи | Документация Майкрософт"
description: "Рассматривайте рекомендации по масштабированию и производительности в Azure Stream Analytics."
keywords: "единица потоковой передачи, производительность запроса"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 1441a5df4fd92abf85763ca9a1512503b1a0da56
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="optimize-your-job-to-use-streaming-units-efficiently"></a><span data-ttu-id="0672a-104">Оптимизация задания для эффективного использования единиц потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="0672a-104">Optimize your job to use Streaming Units efficiently</span></span>

<span data-ttu-id="0672a-105">Azure Stream Analytics вычисляет показатель производительности при выполнении задания в единицах потоковой передачи,</span><span class="sxs-lookup"><span data-stu-id="0672a-105">Azure Stream Analytics aggregates the performance "weight" of running a job into Streaming Units (SUs).</span></span> <span data-ttu-id="0672a-106">представляющих вычислительные ресурсы, которые используются для выполнения заданий.</span><span class="sxs-lookup"><span data-stu-id="0672a-106">SUs represent the computing resources that are consumed to execute a job.</span></span> <span data-ttu-id="0672a-107">Единицы потоковой передачи предоставляют способ описания относительной мощности обработки события, основываясь на измерении загрузки ЦП, памяти и скорости чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="0672a-107">SUs provide a way to describe the relative event processing capacity based on a blended measure of CPU, memory, and read and write rates.</span></span> <span data-ttu-id="0672a-108">Эта емкость позволяет сосредоточиться на логике запросов. При этом вам не нужно знать рекомендации по производительности уровня хранилища, выделять память для задания вручную и определять приблизительное число ядер ЦП, необходимых для своевременного выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="0672a-108">This capacity lets you focus on the query logic and removes you from needing to know storage tier performance considerations, allocate memory for your job manually, and approximate the CPU core-count needed to run your job in a timely manner.</span></span>

## <a name="how-many-sus-are-required-for-a-job"></a><span data-ttu-id="0672a-109">Сколько единиц потоковой передачи требуется для задания?</span><span class="sxs-lookup"><span data-stu-id="0672a-109">How many SUs are required for a job?</span></span>

<span data-ttu-id="0672a-110">Выбор числа единиц потоковой передачи, требуемых для конкретного задания, зависит от конфигурации входных данных и запроса, определенного в задании.</span><span class="sxs-lookup"><span data-stu-id="0672a-110">Choosing the number of required SUs for a particular job depends on the partition configuration for the inputs and the query that's defined within the job.</span></span> <span data-ttu-id="0672a-111">В колонке **Масштаб** можно задать требуемое число единиц потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="0672a-111">The **Scale** blade allows you to set the right number of SUs.</span></span> <span data-ttu-id="0672a-112">Мы рекомендуем выделять больше единиц потоковой передачи, чем требуется.</span><span class="sxs-lookup"><span data-stu-id="0672a-112">It is a best practice to allocate more SUs than needed.</span></span> <span data-ttu-id="0672a-113">Модуль обработки Stream Analytics оптимизирует задержки и пропускную способность за счет выделения дополнительной памяти.</span><span class="sxs-lookup"><span data-stu-id="0672a-113">The Stream Analytics processing engine optimizes for latency and throughput at the cost of allocating additional memory.</span></span>

<span data-ttu-id="0672a-114">В общем лучше всего начать с 6 единиц потоковой передачи для запросов, не использующих *PARTITION BY*.</span><span class="sxs-lookup"><span data-stu-id="0672a-114">In general, the best practice is to start with 6 SUs for queries that don't use *PARTITION BY*.</span></span> <span data-ttu-id="0672a-115">Затем определите "золотую середину", используя метод проб и ошибок, при котором вы изменяете число единиц потоковой передачи после передачи репрезентативного объема данных и просмотра метрики процента использования единицы потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="0672a-115">Then determine the sweet spot by using a trial and error method in which you modify the number of SUs after you pass representative amounts of data and examine the SU %Utilization metric.</span></span>

<span data-ttu-id="0672a-116">Перед началом обработки в Azure Stream Analytics события находятся в окне буфера изменения порядка.</span><span class="sxs-lookup"><span data-stu-id="0672a-116">Azure Stream Analytics keeps events in a window called the “reorder buffer” before it starts any processing.</span></span> <span data-ttu-id="0672a-117">Внутри окна изменения порядка события сортируются по времени, и последующие операции выполняются с отсортированными событиями.</span><span class="sxs-lookup"><span data-stu-id="0672a-117">Events are sorted within the reorder window by time, and subsequent operations are performed on the temporally sorted events.</span></span> <span data-ttu-id="0672a-118">Изменение порядка событий по времени гарантирует, что оператор видит все события за установленный период времени.</span><span class="sxs-lookup"><span data-stu-id="0672a-118">Reordering events by time ensures that the operator has visibility into all the events in the stipulated timeframe.</span></span> <span data-ttu-id="0672a-119">Благодаря этому он выполняет необходимую обработку и выдает результат.</span><span class="sxs-lookup"><span data-stu-id="0672a-119">It also lets the operator perform the requisite processing and produce an output.</span></span> <span data-ttu-id="0672a-120">Побочный эффект этого механизма заключается в том, что обработка откладывается, пока события находятся в окне изменения порядка.</span><span class="sxs-lookup"><span data-stu-id="0672a-120">A side effect of this mechanism is that processing is delayed by the duration of the reorder window.</span></span> <span data-ttu-id="0672a-121">Объем памяти для задания (что влияет на использование единиц потоковой передачи) зависит от размера этого окна изменения порядка и числа событий в нем.</span><span class="sxs-lookup"><span data-stu-id="0672a-121">The memory footprint of the job (which affects SU consumption) is a function of the size of this reorder window and the number of events contained within it.</span></span>

> [!NOTE]
> <span data-ttu-id="0672a-122">При изменении числа модулей чтения во время обновления задания временные предупреждения записываются в журналы аудита.</span><span class="sxs-lookup"><span data-stu-id="0672a-122">When the number of readers changes during job upgrades, transient warnings are written to audit logs.</span></span> <span data-ttu-id="0672a-123">Задания Stream Analytics восстанавливаются от этих временных сбоев автоматически.</span><span class="sxs-lookup"><span data-stu-id="0672a-123">Stream Analytics jobs automatically recover from these transient issues.</span></span>

## <a name="common-high-memory-causes-for-high-su-usage-for-running-jobs"></a><span data-ttu-id="0672a-124">Наиболее частые причины большого объема памяти при интенсивном использовании единиц потоковой передачи для выполняющихся заданий</span><span class="sxs-lookup"><span data-stu-id="0672a-124">Common high-memory causes for high SU usage for running jobs</span></span>

### <a name="high-cardinality-for-group-by"></a><span data-ttu-id="0672a-125">Большое число элементов для выражения GROUP BY</span><span class="sxs-lookup"><span data-stu-id="0672a-125">High cardinality for GROUP BY</span></span>

<span data-ttu-id="0672a-126">Число элементов во входящих событиях влияет на использование памяти для задания.</span><span class="sxs-lookup"><span data-stu-id="0672a-126">The cardinality of incoming events dictates memory usage for the job.</span></span>

<span data-ttu-id="0672a-127">Например, в `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)` связанное с **кластером** число — это число элементов в запросе.</span><span class="sxs-lookup"><span data-stu-id="0672a-127">For example, in `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`, the number associated with **clustered** is the cardinality of the query.</span></span>

<span data-ttu-id="0672a-128">Для устранения проблем, вызванных большим количеством элементов, разверните запрос, увеличив число разделов с помощью **PARTITION BY**.</span><span class="sxs-lookup"><span data-stu-id="0672a-128">To mitigate issues that are caused by high cardinality, scale out the query by increasing partitions using **PARTITION BY**.</span></span>

```
Select count(*) from input
Partition By clusterid
GROUP BY clustered tumblingwindow (minutes, 5)
```

<span data-ttu-id="0672a-129">Число *кластеров* — это количество элементов GROUP BY.</span><span class="sxs-lookup"><span data-stu-id="0672a-129">The number of *clustered* is the cardinality of GROUP BY here.</span></span>

<span data-ttu-id="0672a-130">Секционированный запрос распределяется между несколькими узлами.</span><span class="sxs-lookup"><span data-stu-id="0672a-130">After the query is partitioned, it is spread out over multiple nodes.</span></span> <span data-ttu-id="0672a-131">В результате уменьшается не только число событий, поступающих на каждый узел, но и размер буфера изменения порядка.</span><span class="sxs-lookup"><span data-stu-id="0672a-131">As a result, the number of events coming into each node is reduced, which in turn reduces the size of the reorder buffer.</span></span> <span data-ttu-id="0672a-132">Кроме того, нужно секционировать разделы концентратора событий по идентификатору раздела.</span><span class="sxs-lookup"><span data-stu-id="0672a-132">You should also partition event hub partitions by partitionid.</span></span>

### <a name="high-unmatched-event-count-for-join"></a><span data-ttu-id="0672a-133">Большое число несопоставленных событий для JOIN</span><span class="sxs-lookup"><span data-stu-id="0672a-133">High unmatched event count for JOIN</span></span>

<span data-ttu-id="0672a-134">Число несопоставленных событий в JOIN влияет на использование ресурсов памяти в запросе.</span><span class="sxs-lookup"><span data-stu-id="0672a-134">The number of unmatched events in a JOIN affects the memory utilization of the query.</span></span> <span data-ttu-id="0672a-135">Например давайте рассмотрим запрос на поиск просмотров рекламы, которые привели к переходам:</span><span class="sxs-lookup"><span data-stu-id="0672a-135">For example, take a query that is looking to find the number of ad impressions that generates clicks:</span></span>

```
SELECT id from clicks INNER JOIN,
impressions on impressions.id = clicks.id AND DATEDIFF(hour, impressions, clicks) between 0 AND 10
```

<span data-ttu-id="0672a-136">В этом случае возможно, что отображается множество рекламных объявлений и выполняется несколько переходов.</span><span class="sxs-lookup"><span data-stu-id="0672a-136">In this scenario, it is possible that many ads are shown and few clicks are generated.</span></span> <span data-ttu-id="0672a-137">С учетом такого результата заданию нужно сохранить все события в течение временного окна.</span><span class="sxs-lookup"><span data-stu-id="0672a-137">Such a result would require the job to keep all the events within the time window.</span></span> <span data-ttu-id="0672a-138">Объем используемой памяти пропорционален размеру окна и частоте событий.</span><span class="sxs-lookup"><span data-stu-id="0672a-138">The amount of memory consumed is proportional to the window size and event rate.</span></span> 

<span data-ttu-id="0672a-139">Во избежание такой ситуации разверните запрос, увеличив число разделов с помощью PARTITION BY.</span><span class="sxs-lookup"><span data-stu-id="0672a-139">To mitigate this situation, scale out the query by increasing partitions by using PARTITION BY.</span></span> 

<span data-ttu-id="0672a-140">Секционированный запрос распределяется между несколькими узлами обработки.</span><span class="sxs-lookup"><span data-stu-id="0672a-140">After the query is partitioned, it is spread out over multiple processing nodes.</span></span> <span data-ttu-id="0672a-141">В результате уменьшается не только число событий, поступающих на каждый узел, но и размер буфера изменения порядка.</span><span class="sxs-lookup"><span data-stu-id="0672a-141">As a result, the number of events coming into each node is reduced, which in turn reduces the size of the reorder buffer.</span></span>

### <a name="large-number-of-out-of-order-events"></a><span data-ttu-id="0672a-142">Большое число неупорядоченных событий</span><span class="sxs-lookup"><span data-stu-id="0672a-142">Large number of out of order events</span></span> 

<span data-ttu-id="0672a-143">Большое число неупорядоченных событий в большом временном окне еще больше увеличит окно буфера переупорядочения.</span><span class="sxs-lookup"><span data-stu-id="0672a-143">A large number of out of order events within a large time window causes the size of the "reorder buffer" to be larger.</span></span> <span data-ttu-id="0672a-144">Во избежание этого масштабируйте запрос, увеличивая число разделов с помощью PARTITION BY.</span><span class="sxs-lookup"><span data-stu-id="0672a-144">To mitigate this situation, scale the query by increasing partitions by using PARTITION BY.</span></span> <span data-ttu-id="0672a-145">Секционированный запрос распределяется между несколькими узлами.</span><span class="sxs-lookup"><span data-stu-id="0672a-145">After the query is partitioned, it is spread out over multiple nodes.</span></span> <span data-ttu-id="0672a-146">В результате уменьшается не только число событий, поступающих на каждый узел, но и размер буфера изменения порядка.</span><span class="sxs-lookup"><span data-stu-id="0672a-146">As a result, the number of events coming into each node is reduced, which in turn reduces the size of the reorder buffer.</span></span> 


## <a name="get-help"></a><span data-ttu-id="0672a-147">Получение справки</span><span class="sxs-lookup"><span data-stu-id="0672a-147">Get help</span></span>
<span data-ttu-id="0672a-148">За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="0672a-148">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0672a-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0672a-149">Next steps</span></span>
* [<span data-ttu-id="0672a-150">Введение в Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0672a-150">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="0672a-151">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0672a-151">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="0672a-152">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0672a-152">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* <span data-ttu-id="0672a-153">[Azure Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) (Справочник по языку запросов Azure Stream Analytics).</span><span class="sxs-lookup"><span data-stu-id="0672a-153">[Azure Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx)</span></span>
* [<span data-ttu-id="0672a-154">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0672a-154">Azure Stream Analytics Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
