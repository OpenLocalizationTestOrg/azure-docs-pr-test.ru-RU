---
title: "Отладка Azure Stream Analytics с помощью приемников концентратора событий | Документация Майкрософт"
description: "Рассматривайте рекомендации по группам потребителей концентраторов событий в заданиях Stream Analytics."
keywords: "ограничение концентратора событий, группа потребителей"
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
ms.openlocfilehash: 145981d0b5eff0c574c5012c85f43a6318ba4126
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="debug-azure-stream-analytics-with-event-hub-receivers"></a><span data-ttu-id="bf0b2-104">Отладка Azure Stream Analytics с помощью приемников концентратора событий</span><span class="sxs-lookup"><span data-stu-id="bf0b2-104">Debug Azure Stream Analytics with event hub receivers</span></span>

<span data-ttu-id="bf0b2-105">Вы можете использовать концентраторы событий Azure в Azure Stream Analytics для приема или вывода данных в задании.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-105">You can use Azure Event Hubs in Azure Stream Analytics to ingest or output data from a job.</span></span> <span data-ttu-id="bf0b2-106">Мы рекомендуем использовать концентраторы событий с несколькими группами потребителей, чтобы обеспечить масштабируемость задания.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-106">A best practice for using Event Hubs is to use multiple consumer groups, to ensure job scalability.</span></span> <span data-ttu-id="bf0b2-107">Одной из причин является то, что число модулей чтения в задании Stream Analytics для определенных входных данных влияет на число модулей чтения в одной группе потребителей.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-107">One reason is that the number of readers in the Stream Analytics job for a specific input affects the number of readers in a single consumer group.</span></span> <span data-ttu-id="bf0b2-108">Точное число приемников зависит от сведений о внутренней реализации логики топологии развертывания.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-108">The precise number of receivers is based on internal implementation details for the scale-out topology logic.</span></span> <span data-ttu-id="bf0b2-109">Число приемников не предоставляется извне.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-109">The number of receivers is not exposed externally.</span></span> <span data-ttu-id="bf0b2-110">Число модулей чтения можно изменить во время запуска или обновления задания.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-110">The number of readers can change either at the job start time or during job upgrades.</span></span>

> [!NOTE]
> <span data-ttu-id="bf0b2-111">При изменении числа модулей чтения во время обновления задания временные предупреждения записываются в журналы аудита.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-111">When the number of readers changes during a job upgrade, transient warnings are written to audit logs.</span></span> <span data-ttu-id="bf0b2-112">Задания Stream Analytics восстанавливаются от этих временных сбоев автоматически.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-112">Stream Analytics jobs automatically recover from these transient issues.</span></span>

## <a name="number-of-readers-per-partition-exceeds-event-hubs-limit-of-five"></a><span data-ttu-id="bf0b2-113">Число модулей чтения каждого раздела превышает предельно допустимое число концентраторов событий (пять)</span><span class="sxs-lookup"><span data-stu-id="bf0b2-113">Number of readers per partition exceeds Event Hubs limit of five</span></span>

<span data-ttu-id="bf0b2-114">Ниже представлены сценарии, в которых число модулей чтения каждого раздела превышает предельно допустимое число концентраторов событий (пять).</span><span class="sxs-lookup"><span data-stu-id="bf0b2-114">Scenarios in which the number of readers per partition exceeds the Event Hubs limit of five include the following:</span></span>

* <span data-ttu-id="bf0b2-115">Несколько инструкций SELECT. При использовании нескольких инструкций SELECT, ссылающихся на **один** набор входных данных концентратора событий, каждая из них создает по приемнику.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-115">Multiple SELECT statements: If you use multiple SELECT statements that refer to **same** event hub input, each SELECT statement causes a new receiver to be created.</span></span>
* <span data-ttu-id="bf0b2-116">UNION. При использовании UNION несколько наборов входных данных могут ссылаться на **один** концентратор событий и на одну группу потребителей.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-116">UNION: When you use a UNION, it's possible to have multiple inputs that refer to the **same** event hub and consumer group.</span></span>
* <span data-ttu-id="bf0b2-117">SELF JOIN. При использовании операции SELF JOIN можно создать несколько ссылок на **один** концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-117">SELF JOIN: When you use a SELF JOIN operation, it's possible to refer to the **same** event hub multiple times.</span></span>

## <a name="solution"></a><span data-ttu-id="bf0b2-118">Решение</span><span class="sxs-lookup"><span data-stu-id="bf0b2-118">Solution</span></span>

<span data-ttu-id="bf0b2-119">Следующие рекомендации могут помочь справиться со сценариями, в которых число модулей чтения каждого раздела превышает предельно допустимое число концентраторов событий (пять).</span><span class="sxs-lookup"><span data-stu-id="bf0b2-119">The following best practices can help mitigate scenarios in which the number of readers per partition exceeds the Event Hubs limit of five.</span></span>

### <a name="split-your-query-into-multiple-steps-by-using-a-with-clause"></a><span data-ttu-id="bf0b2-120">Разбиение запроса на несколько шагов с помощью предложения WITH</span><span class="sxs-lookup"><span data-stu-id="bf0b2-120">Split your query into multiple steps by using a WITH clause</span></span>

<span data-ttu-id="bf0b2-121">Предложение WITH задает временный именованный результирующий набор, на который можно создать ссылку в предложении FROM в запросе.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-121">The WITH clause specifies a temporary named result set that can be referenced by a FROM clause in the query.</span></span> <span data-ttu-id="bf0b2-122">Предложение WITH определяется в области выполнения одной инструкции SELECT.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-122">You define the WITH clause in the execution scope of a single SELECT statement.</span></span>

<span data-ttu-id="bf0b2-123">Например, вместо этого запроса:</span><span class="sxs-lookup"><span data-stu-id="bf0b2-123">For example, instead of this query:</span></span>

```
SELECT foo 
INTO output1
FROM inputEventHub

SELECT bar
INTO output2
FROM inputEventHub 
…
```

<span data-ttu-id="bf0b2-124">Используйте этот:</span><span class="sxs-lookup"><span data-stu-id="bf0b2-124">Use this query:</span></span>

```
WITH input (
   SELECT * FROM inputEventHub
) as data

SELECT foo
INTO output1
FROM data

SELECT bar
INTO output2
FROM data
…
```

### <a name="ensure-that-inputs-bind-to-different-consumer-groups"></a><span data-ttu-id="bf0b2-125">Привязка входных данных к разным группам потребителей</span><span class="sxs-lookup"><span data-stu-id="bf0b2-125">Ensure that inputs bind to different consumer groups</span></span>

<span data-ttu-id="bf0b2-126">Создайте отдельные группы потребителей для запросов, в которых три или более наборов входных данных подключены к одной группе потребителей концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-126">For queries in which three or more inputs are connected to the same Event Hubs consumer group, create separate consumer groups.</span></span> <span data-ttu-id="bf0b2-127">Для этого нужно создать дополнительные наборы входных данных Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="bf0b2-127">This requires the creation of additional Stream Analytics inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="bf0b2-128">Получение справки</span><span class="sxs-lookup"><span data-stu-id="bf0b2-128">Get help</span></span>
<span data-ttu-id="bf0b2-129">Дополнительную помощь вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="bf0b2-129">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf0b2-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bf0b2-130">Next steps</span></span>
* [<span data-ttu-id="bf0b2-131">Что такое Stream Analytics?</span><span class="sxs-lookup"><span data-stu-id="bf0b2-131">Introduction to Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="bf0b2-132">Приступая к работе с Azure Stream Analytics: выявление мошенничества в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="bf0b2-132">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="bf0b2-133">Масштабирование заданий Azure Stream Analytics для повышения пропускной способности базы данных</span><span class="sxs-lookup"><span data-stu-id="bf0b2-133">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* <span data-ttu-id="bf0b2-134">[Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) (Справочник по языку запросов Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="bf0b2-134">[Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx)</span></span>
* <span data-ttu-id="bf0b2-135">[Stream Analytics management REST API reference](https://msdn.microsoft.com/library/azure/dn835031.aspx) (Справочник по API-интерфейсу REST для управления Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="bf0b2-135">[Stream Analytics management REST API reference](https://msdn.microsoft.com/library/azure/dn835031.aspx)</span></span>
