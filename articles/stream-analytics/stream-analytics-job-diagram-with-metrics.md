---
title: "AAA Azure Stream Analytics управляемых данными отладку с помощью схемы задания hello | Документы Microsoft"
description: "Устранение неполадок в задание Stream Analytics с помощью схемы задания hello и метрики."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/01/2017
ms.author: jeffstok
ms.openlocfilehash: 1af884d485bebb06b034da01a13f7f8240516571
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="data-driven-debugging-by-using-hello-job-diagram"></a><span data-ttu-id="2b5b8-103">Отладка с использованием схемы hello задания на основе данных</span><span class="sxs-lookup"><span data-stu-id="2b5b8-103">Data-driven debugging by using hello job diagram</span></span>

<span data-ttu-id="2b5b8-104">Задание Hello к схеме для hello **мониторинг** колонки в hello Azure портал позволяет наглядно представить конвейер задания.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-104">hello job diagram on hello **Monitoring** blade in hello Azure portal can help you visualize your job pipeline.</span></span> <span data-ttu-id="2b5b8-105">На ней представлены сведения о входных и выходных данных, а также о шагах запроса.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-105">It shows inputs, outputs, and query steps.</span></span> <span data-ttu-id="2b5b8-106">Можно использовать hello задания схемы tooexamine hello показатели для каждого шага, toomore быстро изолировать hello источник проблемы при устранении неполадок.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-106">You can use hello job diagram tooexamine hello metrics for each step, toomore quickly isolate hello source of a problem when you troubleshoot issues.</span></span>

## <a name="using-hello-job-diagram"></a><span data-ttu-id="2b5b8-107">С помощью схемы задания hello</span><span class="sxs-lookup"><span data-stu-id="2b5b8-107">Using hello job diagram</span></span>

<span data-ttu-id="2b5b8-108">В hello портал Azure при работе в задание Stream Analytics в группе **поддержки + Устранение неполадок**выберите **схема задания**:</span><span class="sxs-lookup"><span data-stu-id="2b5b8-108">In hello Azure portal, while in a Stream Analytics job, under **SUPPORT + TROUBLESHOOTING**, select **Job diagram**:</span></span>

![Схема заданий с метриками — расположение](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-1.png)

<span data-ttu-id="2b5b8-110">Выберите каждый шаг toosee hello соответствующего раздела запроса в запросе области редактирования.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-110">Select each query step toosee hello corresponding section in a query editing pane.</span></span> <span data-ttu-id="2b5b8-111">Диаграмма метрик для hello шаг отображается в нижней области на странице приветствия.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-111">A metric chart for hello step is displayed in a lower pane on hello page.</span></span>

![Схема заданий с метриками — базовое задание](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-2.png)

<span data-ttu-id="2b5b8-113">Выберите секции hello toosee входа hello концентраторов событий Azure **...**</span><span class="sxs-lookup"><span data-stu-id="2b5b8-113">toosee hello partitions of hello Azure Event Hubs input, select **. . .**</span></span> <span data-ttu-id="2b5b8-114">Откроется контекстное меню.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-114">A context menu appears.</span></span> <span data-ttu-id="2b5b8-115">Также можно просмотреть входные слияния hello.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-115">You also can see hello input merger.</span></span>

![Схема заданий с метриками — развертывание раздела](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-3.png)

<span data-ttu-id="2b5b8-117">toosee hello метрики диаграммы для только одной секции, узел раздела выберите hello.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-117">toosee hello metric chart for only a single partition, select hello partition node.</span></span> <span data-ttu-id="2b5b8-118">метрики Hello отображаются внизу hello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-118">hello metrics are shown at hello bottom of hello page.</span></span>

![Схема заданий с метриками — дополнительные метрики](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-4.png)

<span data-ttu-id="2b5b8-120">toosee hello диаграмма метрик для слияния, выберите hello узел слияния.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-120">toosee hello metrics chart for a merger, select hello merger node.</span></span> <span data-ttu-id="2b5b8-121">Hello, следующая диаграмма показывает, что события не были удалены или изменены.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-121">hello following chart shows that no events were dropped or adjusted.</span></span>

![Схема заданий с метриками — сетка](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-5.png)

<span data-ttu-id="2b5b8-123">сведения о hello toosee значение метрики hello и времени, toohello точки диаграммы.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-123">toosee hello details of hello metric value and time, point toohello chart.</span></span>

![Схема заданий с метриками — наведение](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-6.png)

## <a name="troubleshoot-by-using-metrics"></a><span data-ttu-id="2b5b8-125">Устранение неполадок с помощью метрик</span><span class="sxs-lookup"><span data-stu-id="2b5b8-125">Troubleshoot by using metrics</span></span>

<span data-ttu-id="2b5b8-126">Hello **QueryLastProcessedTime** Метрика показывает, когда конкретный шаг полученных данных.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-126">hello **QueryLastProcessedTime** metric indicates when a specific step received data.</span></span> <span data-ttu-id="2b5b8-127">Просмотрев hello топологии, можно работать назад от hello toosee процессора на выходные данные шага не получает данные.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-127">By looking at hello topology, you can work backward from hello output processor toosee which step is not receiving data.</span></span> <span data-ttu-id="2b5b8-128">Если шаг получает данные, перейдите toohello действия запроса перед его.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-128">If a step is not getting data, go toohello query step just before it.</span></span> <span data-ttu-id="2b5b8-129">Проверьте hello предыдущего действия запроса есть временное окно, и если прошло достаточно времени для него toooutput данных.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-129">Check whether hello preceding query step has a time window, and if enough time has passed for it toooutput data.</span></span> <span data-ttu-id="2b5b8-130">(Обратите внимание, времени пребывание час привязанных toohello windows.)</span><span class="sxs-lookup"><span data-stu-id="2b5b8-130">(Note that time windows are snapped toohello hour.)</span></span>
 
<span data-ttu-id="2b5b8-131">Если hello действия предыдущего запроса, процессор ввода используйте hello ввода метрики toohelp ответов hello следующие целевые вопросы.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-131">If hello preceding query step is an input processor, use hello input metrics toohelp answer hello following targeted questions.</span></span> <span data-ttu-id="2b5b8-132">о заданиях, получающих данные из источников входных данных.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-132">They can help you determine whether a job is getting data from its input sources.</span></span> <span data-ttu-id="2b5b8-133">Если запрос hello секционирована, изучите каждой секции.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-133">If hello query is partitioned, examine each partition.</span></span>
 
### <a name="how-much-data-is-being-read"></a><span data-ttu-id="2b5b8-134">Какой объем данных считывается?</span><span class="sxs-lookup"><span data-stu-id="2b5b8-134">How much data is being read?</span></span>

*   <span data-ttu-id="2b5b8-135">**InputEventsSourcesTotal** hello число единиц данных чтения.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-135">**InputEventsSourcesTotal** is hello number of data units read.</span></span> <span data-ttu-id="2b5b8-136">Например hello количество больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-136">For example, hello number of blobs.</span></span>
*   <span data-ttu-id="2b5b8-137">**InputEventsTotal** hello число событий, которые чтения.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-137">**InputEventsTotal** is hello number of events read.</span></span> <span data-ttu-id="2b5b8-138">Эта метрика доступна для каждого раздела.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-138">This metric is available per partition.</span></span>
*   <span data-ttu-id="2b5b8-139">**InputEventsInBytesTotal** hello число считанных байтов.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-139">**InputEventsInBytesTotal** is hello number of bytes read.</span></span>
*   <span data-ttu-id="2b5b8-140">Метрика **InputEventsLastArrivalTime** обновляется после размещения в очереди каждого полученного события.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-140">**InputEventsLastArrivalTime** is updated with every received event's enqueued time.</span></span>
 
### <a name="is-time-moving-forward-if-actual-events-are-read-punctuation-might-not-be-issued"></a><span data-ttu-id="2b5b8-141">Отсчитывается ли время?</span><span class="sxs-lookup"><span data-stu-id="2b5b8-141">Is time moving forward?</span></span> <span data-ttu-id="2b5b8-142">Если фактические события считываются, знаки препинания могут быть опущены.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-142">If actual events are read, punctuation might not be issued.</span></span>

*   <span data-ttu-id="2b5b8-143">**InputEventsLastPunctuationTime** указывает выдачи знакам препинания tookeep время перемещение вперед.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-143">**InputEventsLastPunctuationTime** indicates when a punctuation was issued tookeep time moving forward.</span></span> <span data-ttu-id="2b5b8-144">Последовательность данных может быть заблокирована, если знаки препинания будут опущены.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-144">If punctuation is not issued, data flow can get blocked.</span></span>
 
### <a name="are-there-any-errors-in-hello-input"></a><span data-ttu-id="2b5b8-145">Существуют ли ошибки во входном файле hello?</span><span class="sxs-lookup"><span data-stu-id="2b5b8-145">Are there any errors in hello input?</span></span>

*   <span data-ttu-id="2b5b8-146">Метрика **InputEventsEventDataNullTotal** содержит число событий со значением null.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-146">**InputEventsEventDataNullTotal** is a count of events that have null data.</span></span>
*   <span data-ttu-id="2b5b8-147">Метрика **InputEventsSerializerErrorsTotal** содержит число событий, десериализацию которых удалось выполнить правильно.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-147">**InputEventsSerializerErrorsTotal** is a count of events that could not be deserialized correctly.</span></span>
*   <span data-ttu-id="2b5b8-148">Метрика **InputEventsDegradedTotal** содержит число событий, в которых возникла ошибка, не связанная с десериализацией.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-148">**InputEventsDegradedTotal** is a count of events that had an issue other than with deserialization.</span></span>
 
### <a name="are-events-being-dropped-or-adjusted"></a><span data-ttu-id="2b5b8-149">Были ли события удалены или скорректированы?</span><span class="sxs-lookup"><span data-stu-id="2b5b8-149">Are events being dropped or adjusted?</span></span>

*   <span data-ttu-id="2b5b8-150">**InputEventsEarlyTotal** hello число событий, которые имеют отметку времени приложения перед hello верхнего предела.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-150">**InputEventsEarlyTotal** is hello number of events that have an application timestamp before hello high watermark.</span></span>
*   <span data-ttu-id="2b5b8-151">**InputEventsLateTotal** hello число событий, которые имеют отметку времени приложения после hello верхнего предела.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-151">**InputEventsLateTotal** is hello number of events that have an application timestamp after hello high watermark.</span></span>
*   <span data-ttu-id="2b5b8-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** номер события hello удалена перед выполнением время начала задания hello.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** is hello number events dropped before hello job start time.</span></span>
 
### <a name="are-we-falling-behind-in-reading-data"></a><span data-ttu-id="2b5b8-153">Есть ли непрочитанные данные?</span><span class="sxs-lookup"><span data-stu-id="2b5b8-153">Are we falling behind in reading data?</span></span>

*   <span data-ttu-id="2b5b8-154">**InputEventsSourcesBackloggedTotal** сообщает, сколько дополнительные сообщения должны toobe чтения для концентраторов событий и центр IoT Azure входных данных.</span><span class="sxs-lookup"><span data-stu-id="2b5b8-154">**InputEventsSourcesBackloggedTotal** tells you how many more messages need toobe read for Event Hubs and Azure IoT Hub inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="2b5b8-155">Получение справки</span><span class="sxs-lookup"><span data-stu-id="2b5b8-155">Get help</span></span>
<span data-ttu-id="2b5b8-156">Дополнительную помощь вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="2b5b8-156">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b5b8-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2b5b8-157">Next steps</span></span>
* [<span data-ttu-id="2b5b8-158">Введение tooStream аналитика</span><span class="sxs-lookup"><span data-stu-id="2b5b8-158">Introduction tooStream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="2b5b8-159">Приступая к работе с Azure Stream Analytics: выявление мошенничества в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="2b5b8-159">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="2b5b8-160">Масштабирование заданий Azure Stream Analytics для повышения пропускной способности базы данных</span><span class="sxs-lookup"><span data-stu-id="2b5b8-160">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* <span data-ttu-id="2b5b8-161">[Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) (Справочник по языку запросов Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="2b5b8-161">[Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx)</span></span>
* <span data-ttu-id="2b5b8-162">[Stream Analytics management REST API reference](https://msdn.microsoft.com/library/azure/dn835031.aspx) (Справочник по API-интерфейсу REST для управления Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="2b5b8-162">[Stream Analytics management REST API reference](https://msdn.microsoft.com/library/azure/dn835031.aspx)</span></span>
