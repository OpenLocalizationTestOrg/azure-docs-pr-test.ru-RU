---
title: "Введение в функции окна Stream Analytics | Документация Майкрософт"
description: "Узнайте о трех функциях окна в Stream Analytics (\"переворачивающееся\", \"прыгающее\" и \"скользящее\" окно)."
keywords: "\"переворачивающееся\" окно, \"скользящее\" окно, \"прыгающее\" окно"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0d8d8717-5d23-43f0-b475-af078ab4627d
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 09915ad747153210f655b152355c551046066a88
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-stream-analytics-window-functions"></a><span data-ttu-id="80861-104">Введение в функции окна Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="80861-104">Introduction to Stream Analytics Window functions</span></span>
<span data-ttu-id="80861-105">При использовании потоковой передачи во многих случаях необходимо выполнять операции только с теми данными, которые содержатся во временных окнах.</span><span class="sxs-lookup"><span data-stu-id="80861-105">In many real time streaming scenarios, it is necessary to perform operations only on the data contained in temporal windows.</span></span> <span data-ttu-id="80861-106">Ключевой возможностью Azure Stream Analytics является встроенная поддержка функций управления окнами, которая существенно повышает производительность разработчиков при создании сложных задач обработки потоков.</span><span class="sxs-lookup"><span data-stu-id="80861-106">Native support for windowing functions is a key feature of Azure Stream Analytics that moves the needle on developer productivity in authoring complex stream processing jobs.</span></span> <span data-ttu-id="80861-107">Stream Analytics позволяет разработчикам использовать [**"переворачивающиеся"**](https://msdn.microsoft.com/library/dn835055.aspx), [**"прыгающие"**](https://msdn.microsoft.com/library/dn835041.aspx) и [**"скользящие"**](https://msdn.microsoft.com/library/dn835051.aspx) окна для временных операций при потоковой передаче данных.</span><span class="sxs-lookup"><span data-stu-id="80861-107">Stream Analytics enables developers to use [**Tumbling**](https://msdn.microsoft.com/library/dn835055.aspx), [**Hopping**](https://msdn.microsoft.com/library/dn835041.aspx) and [**Sliding**](https://msdn.microsoft.com/library/dn835051.aspx) windows to perform temporal operations on streaming data.</span></span> <span data-ttu-id="80861-108">Следует отметить, что все операции с [окном](https://msdn.microsoft.com/library/dn835019.aspx) выводят результаты в **конце** этого окна.</span><span class="sxs-lookup"><span data-stu-id="80861-108">It is worth noting that all [Window](https://msdn.microsoft.com/library/dn835019.aspx) operations output results at the **end** of the window.</span></span> <span data-ttu-id="80861-109">Результатом для окна будет единичное событие, полученное на основе выбранной статистической функции.</span><span class="sxs-lookup"><span data-stu-id="80861-109">The output of the window will be single event based on the aggregate function used.</span></span> <span data-ttu-id="80861-110">Метка времени для этого события соответствует времени завершения окна, и все функции окна выполняются с фиксированной длительностью.</span><span class="sxs-lookup"><span data-stu-id="80861-110">The event will have the time stamp of the end of the window and all Window functions are defined with a fixed length.</span></span> <span data-ttu-id="80861-111">И последнее важное замечание: все функции окна следует использовать в предложении [**GROUP BY**](https://msdn.microsoft.com/library/dn835023.aspx).</span><span class="sxs-lookup"><span data-stu-id="80861-111">Lastly it is important to note that all Window functions should be used in a [**GROUP BY**](https://msdn.microsoft.com/library/dn835023.aspx) clause.</span></span>

![Концепции функций окна в Stream Analytics](media/stream-analytics-window-functions/stream-analytics-window-functions-conceptual.png)

## <a name="tumbling-window"></a><span data-ttu-id="80861-113">"Переворачивающееся" окно</span><span class="sxs-lookup"><span data-stu-id="80861-113">Tumbling Window</span></span>
<span data-ttu-id="80861-114">Функции "переворачивающегося" окна используются для разделения потока данных на отдельные сегменты времени, для которых и выполняются эти функции, как показано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="80861-114">Tumbling window functions are used to segment a data stream into distinct time segments and perform a function against them, such as the example below.</span></span> <span data-ttu-id="80861-115">"Переворачивающееся" окно характеризуется тем, что такие окна повторяются и не перекрываются, а любое событие может принадлежать только к одному "переворачивающемуся" окну.</span><span class="sxs-lookup"><span data-stu-id="80861-115">The key differentiators of a Tumbling window are that they repeat, do not overlap and an event cannot belong to more than one tumbling window.</span></span>

![Введение в функции "переворачивающегося" окна в Stream Analytics](media/stream-analytics-window-functions/stream-analytics-window-functions-tumbling-intro.png)

## <a name="hopping-window"></a><span data-ttu-id="80861-117">"Прыгающее" окно</span><span class="sxs-lookup"><span data-stu-id="80861-117">Hopping Window</span></span>
<span data-ttu-id="80861-118">Функции "прыгающего" окна смещаются вперед на фиксированный отрезок времени.</span><span class="sxs-lookup"><span data-stu-id="80861-118">Hopping window functions hop forward in time by a fixed period.</span></span> <span data-ttu-id="80861-119">Эта концепция аналогична переворачивающимся окнам с тем исключением, что "прыгающие" окна могут пересекаться, то есть события могут принадлежать сразу к нескольким окнам из набора "прыгающих" окон.</span><span class="sxs-lookup"><span data-stu-id="80861-119">It may be easy to think of them as Tumbling windows that can overlap, so events can belong to more than one Hopping window result set.</span></span> <span data-ttu-id="80861-120">Если для "прыгающего" окна указать длину прыжка, точно совпадающую с размером окна, оно будет полностью идентично "переворачивающемуся" окну.</span><span class="sxs-lookup"><span data-stu-id="80861-120">To make a Hopping window the same as a Tumbling window one would simply specify the hop size to be the same as the window size.</span></span> 

![Введение в функции "прыгающего" окна в Stream Analytics](media/stream-analytics-window-functions/stream-analytics-window-functions-hopping-intro.png)

## <a name="sliding-window"></a><span data-ttu-id="80861-122">"Скользящее" окно</span><span class="sxs-lookup"><span data-stu-id="80861-122">Sliding Window</span></span>
<span data-ttu-id="80861-123">Функции "скользящего" окна, в отличие от "переворачивающихся" или "прыгающих" окон, создают выходные данные **только** при наступлении определенного события.</span><span class="sxs-lookup"><span data-stu-id="80861-123">Sliding window functions, unlike Tumbling or Hopping windows, produce an output **only**  when an event occurs.</span></span> <span data-ttu-id="80861-124">Каждое такое окно имеет по меньшей мере одно событие, и это окно непрерывно перемещается вперед на период € (эпсилон).</span><span class="sxs-lookup"><span data-stu-id="80861-124">Every window will have at least one event and the window continuously moves forward by an € (epsilon).</span></span> <span data-ttu-id="80861-125">Как и случае с "прыгающими" окнами, каждое событие может принадлежать к нескольким "скользящим" окнам.</span><span class="sxs-lookup"><span data-stu-id="80861-125">Like Hopping Windows, events can belong to more than one Sliding Window.</span></span>

![Введение в функции "скользящего" окна в Stream Analytics](media/stream-analytics-window-functions/stream-analytics-window-functions-sliding-intro.png)

## <a name="getting-help-with-window-functions"></a><span data-ttu-id="80861-127">Справочные сведения по функциям окна</span><span class="sxs-lookup"><span data-stu-id="80861-127">Getting help with Window functions</span></span>
<span data-ttu-id="80861-128">Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="80861-128">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="80861-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="80861-129">Next steps</span></span>
* [<span data-ttu-id="80861-130">Введение в Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="80861-130">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="80861-131">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="80861-131">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="80861-132">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="80861-132">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="80861-133">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="80861-133">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="80861-134">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="80861-134">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

