---
title: "Мониторинг заданий Stream Analytics aaaUnderstanding | Документы Microsoft"
description: "Основные сведения о мониторинге заданий в Stream Analytics"
keywords: "монитор запросов"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5f5cc00f-4a7b-491e-89e1-dbafea46d399
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 36819025c7b2ddbf4b9694522f1b4820407ca5f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="understand-stream-analytics-job-monitoring-and-how-toomonitor-queries"></a><span data-ttu-id="d0534-104">Понимать мониторинг заданий Stream Analytics и как toomonitor запросов</span><span class="sxs-lookup"><span data-stu-id="d0534-104">Understand Stream Analytics job monitoring and how toomonitor queries</span></span>

## <a name="introduction-hello-monitor-page"></a><span data-ttu-id="d0534-105">Введение: страница объектов наблюдения hello</span><span class="sxs-lookup"><span data-stu-id="d0534-105">Introduction: hello monitor page</span></span>
<span data-ttu-id="d0534-106">Здравствуйте, оба области основные показатели производительности, можно использовать toomonitor и устранение производительность запросов и задания портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d0534-106">hello Azure portal both surface key performance metrics that can be used toomonitor and troubleshoot your query and job performance.</span></span> <span data-ttu-id="d0534-107">toosee этих показателей Обзор вы заинтересованы в просмотре метрик для и hello представление задания Stream Analytics toohello **мониторинг** на странице Общие сведения о hello.</span><span class="sxs-lookup"><span data-stu-id="d0534-107">toosee these metrics, browse toohello Stream Analytics job you are interested in seeing metrics for and view hello **Monitoring** section on hello Overview page.</span></span>  

![Мониторинг связи](./media/stream-analytics-monitoring/02-stream-analytics-monitoring-block.png)

<span data-ttu-id="d0534-109">будет открыто окно приветствия, как показано:</span><span class="sxs-lookup"><span data-stu-id="d0534-109">hello window will appear as shown:</span></span>

![Панель мониторинга заданий](./media/stream-analytics-monitoring/01-stream-analytics-monitoring.png)  

## <a name="metrics-available-for-stream-analytics"></a><span data-ttu-id="d0534-111">Метрики, доступные в Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d0534-111">Metrics available for Stream Analytics</span></span>
| <span data-ttu-id="d0534-112">Метрика</span><span class="sxs-lookup"><span data-stu-id="d0534-112">Metric</span></span>                 | <span data-ttu-id="d0534-113">Определение</span><span class="sxs-lookup"><span data-stu-id="d0534-113">Definition</span></span>                               |
| ---------------------- | ---------------------------------------- |
| <span data-ttu-id="d0534-114">Использование единиц потоковой передачи (%)</span><span class="sxs-lookup"><span data-stu-id="d0534-114">SU % Utilization</span></span>       | <span data-ttu-id="d0534-115">Использование Hello hello единиц потоковой передачи присвоено задания tooa вкладку "масштабирование" hello hello задания.</span><span class="sxs-lookup"><span data-stu-id="d0534-115">hello utilization of hello Streaming Unit(s) assigned tooa job from hello Scale tab of hello job.</span></span> <span data-ttu-id="d0534-116">Как только этот индикатор достигнет 80 % и более существует высокая вероятность приостановки или отсрочки обработки события.</span><span class="sxs-lookup"><span data-stu-id="d0534-116">Should this indicator reach 80%, or above, there is high probability that event processing may be delayed or stopped making progress.</span></span> |
| <span data-ttu-id="d0534-117">Входные события</span><span class="sxs-lookup"><span data-stu-id="d0534-117">Input Events</span></span>           | <span data-ttu-id="d0534-118">Объем данных, полученных заданием Stream Analytics hello, в число событий.</span><span class="sxs-lookup"><span data-stu-id="d0534-118">Amount of data received by hello Stream Analytics job, in number of events.</span></span> <span data-ttu-id="d0534-119">Это может быть используется toovalidate, что события отправляются toohello источника входных данных.</span><span class="sxs-lookup"><span data-stu-id="d0534-119">This can be used toovalidate that events are being sent toohello input source.</span></span> |
| <span data-ttu-id="d0534-120">Выходные события</span><span class="sxs-lookup"><span data-stu-id="d0534-120">Output Events</span></span>          | <span data-ttu-id="d0534-121">Объем данных, посланных hello Stream Analytics задания toohello выходные данные целевого объекта, в число событий.</span><span class="sxs-lookup"><span data-stu-id="d0534-121">Amount of data sent by hello Stream Analytics job toohello output target, in number of events.</span></span> |
| <span data-ttu-id="d0534-122">Неупорядоченные события</span><span class="sxs-lookup"><span data-stu-id="d0534-122">Out-of-Order Events</span></span>    | <span data-ttu-id="d0534-123">Количество событий, полученных в неверном порядке, были удалены или получили скорректированную метку времени, основании hello политика порядок событий.</span><span class="sxs-lookup"><span data-stu-id="d0534-123">Number of events received out of order that were either dropped or given an adjusted timestamp, based on hello Event Ordering Policy.</span></span> <span data-ttu-id="d0534-124">Это могут быть затронуты hello настройку параметра hello неупорядоченная временной интервал.</span><span class="sxs-lookup"><span data-stu-id="d0534-124">This can be impacted by hello configuration of hello Out of Order Tolerance Window setting.</span></span> |
| <span data-ttu-id="d0534-125">Ошибки преобразования данных</span><span class="sxs-lookup"><span data-stu-id="d0534-125">Data Conversion Errors</span></span> | <span data-ttu-id="d0534-126">Количество ошибок преобразования данных, возникших в задании Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="d0534-126">Number of data conversion errors incurred by a Stream Analytics job.</span></span> |
| <span data-ttu-id="d0534-127">Ошибки среды выполнения</span><span class="sxs-lookup"><span data-stu-id="d0534-127">Runtime Errors</span></span>         | <span data-ttu-id="d0534-128">Общее количество ошибок, которые происходят во время выполнения задания Stream Analytics Hello.</span><span class="sxs-lookup"><span data-stu-id="d0534-128">hello total number of errors that happen during execution of a Stream Analytics job.</span></span> |
| <span data-ttu-id="d0534-129">События позднего ввода</span><span class="sxs-lookup"><span data-stu-id="d0534-129">Late Input Events</span></span>      | <span data-ttu-id="d0534-130">Число событий, позднее, поступающих от источника hello, которое либо был удален или их отметки времени было изменено, на основе конфигурации политики порядок событий hello позднее событий, Наступивших приветствия.</span><span class="sxs-lookup"><span data-stu-id="d0534-130">Number of events arriving late from hello source which have either been dropped or their timestamp has been adjusted, based on hello Event Ordering Policy configuration of hello Late Arrival Tolerance Window setting.</span></span> |
| <span data-ttu-id="d0534-131">Запросы функций</span><span class="sxs-lookup"><span data-stu-id="d0534-131">Function Requests</span></span>      | <span data-ttu-id="d0534-132">Количество вызовов toohello функции машинного обучения Azure (при его наличии).</span><span class="sxs-lookup"><span data-stu-id="d0534-132">Number of calls toohello Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="d0534-133">Неудачные запросы функций</span><span class="sxs-lookup"><span data-stu-id="d0534-133">Failed Function Requests</span></span> | <span data-ttu-id="d0534-134">Количество неудачных вызовов функции машинного обучения Azure (при наличии).</span><span class="sxs-lookup"><span data-stu-id="d0534-134">Number of failed Azure Machine Learning function calls (if present).</span></span> |
| <span data-ttu-id="d0534-135">События функций</span><span class="sxs-lookup"><span data-stu-id="d0534-135">Function Events</span></span>        | <span data-ttu-id="d0534-136">Количество событий, отправленных toohello функции машинного обучения Azure (при его наличии).</span><span class="sxs-lookup"><span data-stu-id="d0534-136">Number of events sent toohello Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="d0534-137">Байты входного события</span><span class="sxs-lookup"><span data-stu-id="d0534-137">Input Event Bytes</span></span>      | <span data-ttu-id="d0534-138">Объем данных, полученных заданием Stream Analytics hello, в байтах.</span><span class="sxs-lookup"><span data-stu-id="d0534-138">Amount of data received by hello Stream Analytics job, in bytes.</span></span> <span data-ttu-id="d0534-139">Это может быть используется toovalidate, что события отправляются toohello источника входных данных.</span><span class="sxs-lookup"><span data-stu-id="d0534-139">This can be used toovalidate that events are being sent toohello input source.</span></span> |


## <a name="customizing-monitoring-in-hello-azure-portal"></a><span data-ttu-id="d0534-140">Настройка мониторинга в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="d0534-140">Customizing Monitoring in hello Azure portal</span></span>
<span data-ttu-id="d0534-141">Можно настроить тип диаграммы метрик отображается, hello и временной диапазон в параметрах hello изменить диаграмму.</span><span class="sxs-lookup"><span data-stu-id="d0534-141">You can adjust hello type of chart, metrics shown, and time range in hello Edit Chart settings.</span></span> <span data-ttu-id="d0534-142">Дополнительные сведения см. в разделе [как tooCustomize мониторинг](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="d0534-142">For details, see [How tooCustomize Monitoring](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

  ![Диаграмма значений времени в мониторе запросов](./media/stream-analytics-monitoring/08-stream-analytics-monitoring.png)  


## <a name="get-help"></a><span data-ttu-id="d0534-144">Получение справки</span><span class="sxs-lookup"><span data-stu-id="d0534-144">Get help</span></span>
<span data-ttu-id="d0534-145">Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="d0534-145">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0534-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d0534-146">Next steps</span></span>
* [<span data-ttu-id="d0534-147">Введение tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d0534-147">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="d0534-148">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d0534-148">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="d0534-149">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d0534-149">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="d0534-150">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d0534-150">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="d0534-151">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d0534-151">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

