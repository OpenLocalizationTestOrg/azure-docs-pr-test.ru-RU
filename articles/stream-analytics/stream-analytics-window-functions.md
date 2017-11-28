---
title: "функции аналитики окна tooStream aaaIntroduction | Документы Microsoft"
description: "Дополнительные сведения о трех Оконные функции hello в Stream Analytics («переворачивающееся», «прыгающее», перемещая)."
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
ms.openlocfilehash: 7fc36eb9afb2b28e2791d925d26923145eb38074
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toostream-analytics-window-functions"></a><span data-ttu-id="10af0-104">Введение tooStream Analytics Оконные функции</span><span class="sxs-lookup"><span data-stu-id="10af0-104">Introduction tooStream Analytics Window functions</span></span>
<span data-ttu-id="10af0-105">Многие реального времени сценариев потоковой передачи при необходимости tooperform операции только с hello данные, содержащиеся в темпоральных windows.</span><span class="sxs-lookup"><span data-stu-id="10af0-105">In many real time streaming scenarios, it is necessary tooperform operations only on hello data contained in temporal windows.</span></span> <span data-ttu-id="10af0-106">Собственная поддержка для функций управления окнами является ключевой компонент Azure Stream Analytics, перемещающего hello стрелки на производительность разработчика в разработке задания по обработке сложных потока.</span><span class="sxs-lookup"><span data-stu-id="10af0-106">Native support for windowing functions is a key feature of Azure Stream Analytics that moves hello needle on developer productivity in authoring complex stream processing jobs.</span></span> <span data-ttu-id="10af0-107">Stream Analytics дает разработчикам toouse [ **Переворачивающееся**](https://msdn.microsoft.com/library/dn835055.aspx), [ **«прыгающие» окна** ](https://msdn.microsoft.com/library/dn835041.aspx) и [ **скользящий** ](https://msdn.microsoft.com/library/dn835051.aspx) windows tooperform операции со временем потоковой передачи данных.</span><span class="sxs-lookup"><span data-stu-id="10af0-107">Stream Analytics enables developers toouse [**Tumbling**](https://msdn.microsoft.com/library/dn835055.aspx), [**Hopping**](https://msdn.microsoft.com/library/dn835041.aspx) and [**Sliding**](https://msdn.microsoft.com/library/dn835051.aspx) windows tooperform temporal operations on streaming data.</span></span> <span data-ttu-id="10af0-108">Стоит отметить, что все [окна](https://msdn.microsoft.com/library/dn835019.aspx) операции выводить результаты в hello **окончания** окна hello.</span><span class="sxs-lookup"><span data-stu-id="10af0-108">It is worth noting that all [Window](https://msdn.microsoft.com/library/dn835019.aspx) operations output results at hello **end** of hello window.</span></span> <span data-ttu-id="10af0-109">выходные данные Hello hello окна будут основании hello агрегатной функции, используемой одно событие.</span><span class="sxs-lookup"><span data-stu-id="10af0-109">hello output of hello window will be single event based on hello aggregate function used.</span></span> <span data-ttu-id="10af0-110">событие Hello будет иметь отметку времени hello hello окончания периода hello и все Оконные функции определены с фиксированной длиной.</span><span class="sxs-lookup"><span data-stu-id="10af0-110">hello event will have hello time stamp of hello end of hello window and all Window functions are defined with a fixed length.</span></span> <span data-ttu-id="10af0-111">Наконец он является важным toonote, который следует использовать все функции окна в [ **GROUP BY** ](https://msdn.microsoft.com/library/dn835023.aspx) предложения.</span><span class="sxs-lookup"><span data-stu-id="10af0-111">Lastly it is important toonote that all Window functions should be used in a [**GROUP BY**](https://msdn.microsoft.com/library/dn835023.aspx) clause.</span></span>

![Концепции функций окна в Stream Analytics](media/stream-analytics-window-functions/stream-analytics-window-functions-conceptual.png)

## <a name="tumbling-window"></a><span data-ttu-id="10af0-113">"Переворачивающееся" окно</span><span class="sxs-lookup"><span data-stu-id="10af0-113">Tumbling Window</span></span>
<span data-ttu-id="10af0-114">Функции «переворачивающегося» окна используется toosegment потока данных на фрагменты отдельных времени и выполняет функцию с ними, например hello приведенном ниже примере.</span><span class="sxs-lookup"><span data-stu-id="10af0-114">Tumbling window functions are used toosegment a data stream into distinct time segments and perform a function against them, such as hello example below.</span></span> <span data-ttu-id="10af0-115">Hello ключа признаком «переворачивающегося» окна, что они повторяется, не будут перекрываться и события не может принадлежать toomore, чем один «переворачивающееся» окно.</span><span class="sxs-lookup"><span data-stu-id="10af0-115">hello key differentiators of a Tumbling window are that they repeat, do not overlap and an event cannot belong toomore than one tumbling window.</span></span>

![Введение в функции "переворачивающегося" окна в Stream Analytics](media/stream-analytics-window-functions/stream-analytics-window-functions-tumbling-intro.png)

## <a name="hopping-window"></a><span data-ttu-id="10af0-117">"Прыгающее" окно</span><span class="sxs-lookup"><span data-stu-id="10af0-117">Hopping Window</span></span>
<span data-ttu-id="10af0-118">Функции "прыгающего" окна смещаются вперед на фиксированный отрезок времени.</span><span class="sxs-lookup"><span data-stu-id="10af0-118">Hopping window functions hop forward in time by a fixed period.</span></span> <span data-ttu-id="10af0-119">Он может быть легко toothink их как Переворачивающиеся окна, которые могут перекрываться, поэтому события могут принадлежать toomore более одного результирующего набора окна «прыгающие» окна.</span><span class="sxs-lookup"><span data-stu-id="10af0-119">It may be easy toothink of them as Tumbling windows that can overlap, so events can belong toomore than one Hopping window result set.</span></span> <span data-ttu-id="10af0-120">toomake окна «прыгающие» окна hello же, как «переворачивающегося» окна одно просто указать toobe размер прыжка hello Здравствуйте таким же, как размер окна hello.</span><span class="sxs-lookup"><span data-stu-id="10af0-120">toomake a Hopping window hello same as a Tumbling window one would simply specify hello hop size toobe hello same as hello window size.</span></span> 

![Введение в функции "прыгающего" окна в Stream Analytics](media/stream-analytics-window-functions/stream-analytics-window-functions-hopping-intro.png)

## <a name="sliding-window"></a><span data-ttu-id="10af0-122">"Скользящее" окно</span><span class="sxs-lookup"><span data-stu-id="10af0-122">Sliding Window</span></span>
<span data-ttu-id="10af0-123">Функции "скользящего" окна, в отличие от "переворачивающихся" или "прыгающих" окон, создают выходные данные **только** при наступлении определенного события.</span><span class="sxs-lookup"><span data-stu-id="10af0-123">Sliding window functions, unlike Tumbling or Hopping windows, produce an output **only**  when an event occurs.</span></span> <span data-ttu-id="10af0-124">Каждое окно будет иметь по крайней мере одно событие и окно hello постоянно перемещается вперед по € (epsilon).</span><span class="sxs-lookup"><span data-stu-id="10af0-124">Every window will have at least one event and hello window continuously moves forward by an € (epsilon).</span></span> <span data-ttu-id="10af0-125">Как «прыгающих» окнах событий могут принадлежать toomore от одного скользящего окна.</span><span class="sxs-lookup"><span data-stu-id="10af0-125">Like Hopping Windows, events can belong toomore than one Sliding Window.</span></span>

![Введение в функции "скользящего" окна в Stream Analytics](media/stream-analytics-window-functions/stream-analytics-window-functions-sliding-intro.png)

## <a name="getting-help-with-window-functions"></a><span data-ttu-id="10af0-127">Справочные сведения по функциям окна</span><span class="sxs-lookup"><span data-stu-id="10af0-127">Getting help with Window functions</span></span>
<span data-ttu-id="10af0-128">Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="10af0-128">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="10af0-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="10af0-129">Next steps</span></span>
* [<span data-ttu-id="10af0-130">Введение tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="10af0-130">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="10af0-131">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="10af0-131">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="10af0-132">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="10af0-132">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="10af0-133">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="10af0-133">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="10af0-134">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="10af0-134">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

