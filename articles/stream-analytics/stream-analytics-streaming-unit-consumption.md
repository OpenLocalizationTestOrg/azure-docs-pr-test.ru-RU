---
title: "Azure Stream Analytics: Эффективно оптимизировать вашей toouse задания единиц потоковой передачи | Документы Microsoft"
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
ms.openlocfilehash: 5ad98b34d625190a879260f54c9eff0294e230cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-job-toouse-streaming-units-efficiently"></a><span data-ttu-id="9e547-104">Эффективно оптимизировать вашей toouse задания единиц потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="9e547-104">Optimize your job toouse Streaming Units efficiently</span></span>

<span data-ttu-id="9e547-105">Azure Stream Analytics агрегирует hello производительности «вес» выполнения задания в единицы потоковой передачи (SUs).</span><span class="sxs-lookup"><span data-stu-id="9e547-105">Azure Stream Analytics aggregates hello performance "weight" of running a job into Streaming Units (SUs).</span></span> <span data-ttu-id="9e547-106">SUs представляют Привет вычислительных ресурсов, обрабатываемом tooexecute задания.</span><span class="sxs-lookup"><span data-stu-id="9e547-106">SUs represent hello computing resources that are consumed tooexecute a job.</span></span> <span data-ttu-id="9e547-107">SUs предоставляет способ toodescribe hello относительный событий производительности на основе на смешанном показателе ЦП, памяти, обработки и чтения, а также скорости записи.</span><span class="sxs-lookup"><span data-stu-id="9e547-107">SUs provide a way toodescribe hello relative event processing capacity based on a blended measure of CPU, memory, and read and write rates.</span></span> <span data-ttu-id="9e547-108">Этот емкость позволяет сосредоточиться на логику запроса hello и удаляет вас от необходимости tooknow вопросы производительности уровня хранилища, выделить память для своего задания вручную и приблизительное hello ЦП core-число необходимых toorun вашу работу своевременно.</span><span class="sxs-lookup"><span data-stu-id="9e547-108">This capacity lets you focus on hello query logic and removes you from needing tooknow storage tier performance considerations, allocate memory for your job manually, and approximate hello CPU core-count needed toorun your job in a timely manner.</span></span>

## <a name="how-many-sus-are-required-for-a-job"></a><span data-ttu-id="9e547-109">Сколько единиц потоковой передачи требуется для задания?</span><span class="sxs-lookup"><span data-stu-id="9e547-109">How many SUs are required for a job?</span></span>

<span data-ttu-id="9e547-110">Выбор hello количество необходимых SUs для конкретного задания зависит от конфигурации hello секции для входов hello и hello запрос, определенный в задании hello.</span><span class="sxs-lookup"><span data-stu-id="9e547-110">Choosing hello number of required SUs for a particular job depends on hello partition configuration for hello inputs and hello query that's defined within hello job.</span></span> <span data-ttu-id="9e547-111">Hello **шкалы** колонке позволяет tooset hello вправо на количество SUs.</span><span class="sxs-lookup"><span data-stu-id="9e547-111">hello **Scale** blade allows you tooset hello right number of SUs.</span></span> <span data-ttu-id="9e547-112">Это рекомендуется так сделать, tooallocate SUs больше, чем требуется.</span><span class="sxs-lookup"><span data-stu-id="9e547-112">It is a best practice tooallocate more SUs than needed.</span></span> <span data-ttu-id="9e547-113">Подсистема обработки Stream Analytics Hello выполняет оптимизацию для задержки и пропускной способности на стоимость hello выделения дополнительной памяти.</span><span class="sxs-lookup"><span data-stu-id="9e547-113">hello Stream Analytics processing engine optimizes for latency and throughput at hello cost of allocating additional memory.</span></span>

<span data-ttu-id="9e547-114">В общем случае hello рекомендуется toostart с 6 SUs для запросов, которые не используют *PARTITION BY*.</span><span class="sxs-lookup"><span data-stu-id="9e547-114">In general, hello best practice is toostart with 6 SUs for queries that don't use *PARTITION BY*.</span></span> <span data-ttu-id="9e547-115">Затем определите позицию sweet hello, используя метод проб и ошибок, внесения hello число SUs после передачи репрезентативных объемов данных и проверьте метрики использования % SU hello.</span><span class="sxs-lookup"><span data-stu-id="9e547-115">Then determine hello sweet spot by using a trial and error method in which you modify hello number of SUs after you pass representative amounts of data and examine hello SU %Utilization metric.</span></span>

<span data-ttu-id="9e547-116">В окне приветствия «переупорядочить буфер» перед началом обработки Azure Stream Analytics поддерживает события.</span><span class="sxs-lookup"><span data-stu-id="9e547-116">Azure Stream Analytics keeps events in a window called hello “reorder buffer” before it starts any processing.</span></span> <span data-ttu-id="9e547-117">События сортируются в окне приветствия переупорядочить по времени и последующих операций hello временно отсортированные события.</span><span class="sxs-lookup"><span data-stu-id="9e547-117">Events are sorted within hello reorder window by time, and subsequent operations are performed on hello temporally sorted events.</span></span> <span data-ttu-id="9e547-118">Изменение порядка событий по времени обеспечивает оператор hello видимость всех событий hello в hello заданного периода времени.</span><span class="sxs-lookup"><span data-stu-id="9e547-118">Reordering events by time ensures that hello operator has visibility into all hello events in hello stipulated timeframe.</span></span> <span data-ttu-id="9e547-119">Она также позволяет оператору hello выполнения необходимых hello и результат.</span><span class="sxs-lookup"><span data-stu-id="9e547-119">It also lets hello operator perform hello requisite processing and produce an output.</span></span> <span data-ttu-id="9e547-120">Побочный эффект этого механизма — отложена обработки hello продолжительность периода возобновления hello.</span><span class="sxs-lookup"><span data-stu-id="9e547-120">A side effect of this mechanism is that processing is delayed by hello duration of hello reorder window.</span></span> <span data-ttu-id="9e547-121">Hello объем памяти задания hello (который влияет на потребление SU) зависит от размера hello этого изменения порядка окна и hello число событий, содержащихся в нем.</span><span class="sxs-lookup"><span data-stu-id="9e547-121">hello memory footprint of hello job (which affects SU consumption) is a function of hello size of this reorder window and hello number of events contained within it.</span></span>

> [!NOTE]
> <span data-ttu-id="9e547-122">При изменении hello числа агентов чтения во время задания обновления tooaudit журналы записываются временных предупреждения.</span><span class="sxs-lookup"><span data-stu-id="9e547-122">When hello number of readers changes during job upgrades, transient warnings are written tooaudit logs.</span></span> <span data-ttu-id="9e547-123">Задания Stream Analytics восстанавливаются от этих временных сбоев автоматически.</span><span class="sxs-lookup"><span data-stu-id="9e547-123">Stream Analytics jobs automatically recover from these transient issues.</span></span>

## <a name="common-high-memory-causes-for-high-su-usage-for-running-jobs"></a><span data-ttu-id="9e547-124">Наиболее частые причины большого объема памяти при интенсивном использовании единиц потоковой передачи для выполняющихся заданий</span><span class="sxs-lookup"><span data-stu-id="9e547-124">Common high-memory causes for high SU usage for running jobs</span></span>

### <a name="high-cardinality-for-group-by"></a><span data-ttu-id="9e547-125">Большое число элементов для выражения GROUP BY</span><span class="sxs-lookup"><span data-stu-id="9e547-125">High cardinality for GROUP BY</span></span>

<span data-ttu-id="9e547-126">Hello количества входящих событий определяет объем памяти для задания hello.</span><span class="sxs-lookup"><span data-stu-id="9e547-126">hello cardinality of incoming events dictates memory usage for hello job.</span></span>

<span data-ttu-id="9e547-127">Например, в `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`, hello номер, связанный с **кластеризованный** — hello количеством запросов hello.</span><span class="sxs-lookup"><span data-stu-id="9e547-127">For example, in `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`, hello number associated with **clustered** is hello cardinality of hello query.</span></span>

<span data-ttu-id="9e547-128">toomitigate проблемы, вызванные большого количества элементов, горизонтальное масштабирование запросов hello увеличив секций с помощью **PARTITION BY**.</span><span class="sxs-lookup"><span data-stu-id="9e547-128">toomitigate issues that are caused by high cardinality, scale out hello query by increasing partitions using **PARTITION BY**.</span></span>

```
Select count(*) from input
Partition By clusterid
GROUP BY clustered tumblingwindow (minutes, 5)
```

<span data-ttu-id="9e547-129">Здравствуйте, число *кластеризованный* — hello количеством GROUP BY здесь.</span><span class="sxs-lookup"><span data-stu-id="9e547-129">hello number of *clustered* is hello cardinality of GROUP BY here.</span></span>

<span data-ttu-id="9e547-130">После запроса hello секционирована, оно распределяется по нескольким узлам.</span><span class="sxs-lookup"><span data-stu-id="9e547-130">After hello query is partitioned, it is spread out over multiple nodes.</span></span> <span data-ttu-id="9e547-131">В результате уменьшается hello число событий, поступающих в каждом узле, в свою очередь, что снижает hello размер буфера переупорядочить hello.</span><span class="sxs-lookup"><span data-stu-id="9e547-131">As a result, hello number of events coming into each node is reduced, which in turn reduces hello size of hello reorder buffer.</span></span> <span data-ttu-id="9e547-132">Кроме того, нужно секционировать разделы концентратора событий по идентификатору раздела.</span><span class="sxs-lookup"><span data-stu-id="9e547-132">You should also partition event hub partitions by partitionid.</span></span>

### <a name="high-unmatched-event-count-for-join"></a><span data-ttu-id="9e547-133">Большое число несопоставленных событий для JOIN</span><span class="sxs-lookup"><span data-stu-id="9e547-133">High unmatched event count for JOIN</span></span>

<span data-ttu-id="9e547-134">Использование памяти hello hello запроса влияет Hello число непарные события в СОЕДИНЕНИИ.</span><span class="sxs-lookup"><span data-stu-id="9e547-134">hello number of unmatched events in a JOIN affects hello memory utilization of hello query.</span></span> <span data-ttu-id="9e547-135">Например выполните запрос, который требуется toofind hello число просмотров ad, приводит к возникновению ошибки щелчков мыши.</span><span class="sxs-lookup"><span data-stu-id="9e547-135">For example, take a query that is looking toofind hello number of ad impressions that generates clicks:</span></span>

```
SELECT id from clicks INNER JOIN,
impressions on impressions.id = clicks.id AND DATEDIFF(hour, impressions, clicks) between 0 AND 10
```

<span data-ttu-id="9e547-136">В этом случае возможно, что отображается множество рекламных объявлений и выполняется несколько переходов.</span><span class="sxs-lookup"><span data-stu-id="9e547-136">In this scenario, it is possible that many ads are shown and few clicks are generated.</span></span> <span data-ttu-id="9e547-137">Это потребует hello задания tookeep все события hello в окне приветствия времени.</span><span class="sxs-lookup"><span data-stu-id="9e547-137">Such a result would require hello job tookeep all hello events within hello time window.</span></span> <span data-ttu-id="9e547-138">Hello объем используемой памяти — скорость, размер и события окна toohello пропорционально.</span><span class="sxs-lookup"><span data-stu-id="9e547-138">hello amount of memory consumed is proportional toohello window size and event rate.</span></span> 

<span data-ttu-id="9e547-139">toomitigate этой ситуации масштабирования hello запросов, увеличив секции с помощью PARTITION BY.</span><span class="sxs-lookup"><span data-stu-id="9e547-139">toomitigate this situation, scale out hello query by increasing partitions by using PARTITION BY.</span></span> 

<span data-ttu-id="9e547-140">После запроса hello секционирована, он распределяется по нескольким узлам обработки.</span><span class="sxs-lookup"><span data-stu-id="9e547-140">After hello query is partitioned, it is spread out over multiple processing nodes.</span></span> <span data-ttu-id="9e547-141">В результате уменьшается hello число событий, поступающих в каждом узле, в свою очередь, что снижает hello размер буфера переупорядочить hello.</span><span class="sxs-lookup"><span data-stu-id="9e547-141">As a result, hello number of events coming into each node is reduced, which in turn reduces hello size of hello reorder buffer.</span></span>

### <a name="large-number-of-out-of-order-events"></a><span data-ttu-id="9e547-142">Большое число неупорядоченных событий</span><span class="sxs-lookup"><span data-stu-id="9e547-142">Large number of out of order events</span></span> 

<span data-ttu-id="9e547-143">Большое количество неупорядоченные события в окне большое время вызывает hello размер hello «переупорядочить буфера» toobe большего размера.</span><span class="sxs-lookup"><span data-stu-id="9e547-143">A large number of out of order events within a large time window causes hello size of hello "reorder buffer" toobe larger.</span></span> <span data-ttu-id="9e547-144">toomitigate этой ситуации запрос hello масштабирование путем увеличения секции с помощью PARTITION BY.</span><span class="sxs-lookup"><span data-stu-id="9e547-144">toomitigate this situation, scale hello query by increasing partitions by using PARTITION BY.</span></span> <span data-ttu-id="9e547-145">После запроса hello секционирована, оно распределяется по нескольким узлам.</span><span class="sxs-lookup"><span data-stu-id="9e547-145">After hello query is partitioned, it is spread out over multiple nodes.</span></span> <span data-ttu-id="9e547-146">В результате уменьшается hello число событий, поступающих в каждом узле, в свою очередь, что снижает hello размер буфера переупорядочить hello.</span><span class="sxs-lookup"><span data-stu-id="9e547-146">As a result, hello number of events coming into each node is reduced, which in turn reduces hello size of hello reorder buffer.</span></span> 


## <a name="get-help"></a><span data-ttu-id="9e547-147">Получение справки</span><span class="sxs-lookup"><span data-stu-id="9e547-147">Get help</span></span>
<span data-ttu-id="9e547-148">За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="9e547-148">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e547-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9e547-149">Next steps</span></span>
* [<span data-ttu-id="9e547-150">Введение tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9e547-150">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="9e547-151">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9e547-151">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="9e547-152">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9e547-152">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* <span data-ttu-id="9e547-153">[Azure Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) (Справочник по языку запросов Azure Stream Analytics).</span><span class="sxs-lookup"><span data-stu-id="9e547-153">[Azure Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx)</span></span>
* [<span data-ttu-id="9e547-154">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9e547-154">Azure Stream Analytics Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
