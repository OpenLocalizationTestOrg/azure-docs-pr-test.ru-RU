---
title: "aaaDebug Azure Stream Analytics с приемников концентратора событий | Документы Microsoft"
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
ms.openlocfilehash: 89821e6273151de43b5e42d907e547c939e24824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="debug-azure-stream-analytics-with-event-hub-receivers"></a><span data-ttu-id="28b81-104">Отладка Azure Stream Analytics с помощью приемников концентратора событий</span><span class="sxs-lookup"><span data-stu-id="28b81-104">Debug Azure Stream Analytics with event hub receivers</span></span>

<span data-ttu-id="28b81-105">Концентраторы событий Azure можно использовать в Azure Stream Analytics tooingest или выходных данных данные из задания.</span><span class="sxs-lookup"><span data-stu-id="28b81-105">You can use Azure Event Hubs in Azure Stream Analytics tooingest or output data from a job.</span></span> <span data-ttu-id="28b81-106">Для использования концентраторов событий рекомендуется toouse нескольких групп потребителей, tooensure задания масштабируемости.</span><span class="sxs-lookup"><span data-stu-id="28b81-106">A best practice for using Event Hubs is toouse multiple consumer groups, tooensure job scalability.</span></span> <span data-ttu-id="28b81-107">Одна из причин — что hello число читателей в задании Stream Analytics hello для определенных входных данных влияет на hello числа агентов чтения в группе одного получателя.</span><span class="sxs-lookup"><span data-stu-id="28b81-107">One reason is that hello number of readers in hello Stream Analytics job for a specific input affects hello number of readers in a single consumer group.</span></span> <span data-ttu-id="28b81-108">точное число приемников Hello основан на внутренние сведения для логики топологию hello.</span><span class="sxs-lookup"><span data-stu-id="28b81-108">hello precise number of receivers is based on internal implementation details for hello scale-out topology logic.</span></span> <span data-ttu-id="28b81-109">Hello количества получателей не предоставляется извне.</span><span class="sxs-lookup"><span data-stu-id="28b81-109">hello number of receivers is not exposed externally.</span></span> <span data-ttu-id="28b81-110">Hello числа агентов чтения можно изменить во время запуска задания hello или при обновлении задания.</span><span class="sxs-lookup"><span data-stu-id="28b81-110">hello number of readers can change either at hello job start time or during job upgrades.</span></span>

> [!NOTE]
> <span data-ttu-id="28b81-111">При изменении hello числа агентов чтения во время обновления задания tooaudit журналы записываются предупреждения об временной.</span><span class="sxs-lookup"><span data-stu-id="28b81-111">When hello number of readers changes during a job upgrade, transient warnings are written tooaudit logs.</span></span> <span data-ttu-id="28b81-112">Задания Stream Analytics восстанавливаются от этих временных сбоев автоматически.</span><span class="sxs-lookup"><span data-stu-id="28b81-112">Stream Analytics jobs automatically recover from these transient issues.</span></span>

## <a name="number-of-readers-per-partition-exceeds-event-hubs-limit-of-five"></a><span data-ttu-id="28b81-113">Число модулей чтения каждого раздела превышает предельно допустимое число концентраторов событий (пять)</span><span class="sxs-lookup"><span data-stu-id="28b81-113">Number of readers per partition exceeds Event Hubs limit of five</span></span>

<span data-ttu-id="28b81-114">Сценарии, в какие hello числа агентов чтения на каждую секцию превышает предел концентраторов событий hello пяти hello следующее:</span><span class="sxs-lookup"><span data-stu-id="28b81-114">Scenarios in which hello number of readers per partition exceeds hello Event Hubs limit of five include hello following:</span></span>

* <span data-ttu-id="28b81-115">Несколько инструкций SELECT: при использовании нескольких инструкций SELECT, которые ссылаются слишком**же** ввода концентратора событий, каждая инструкция SELECT вызывает новый приемник toobe создан.</span><span class="sxs-lookup"><span data-stu-id="28b81-115">Multiple SELECT statements: If you use multiple SELECT statements that refer too**same** event hub input, each SELECT statement causes a new receiver toobe created.</span></span>
* <span data-ttu-id="28b81-116">ОБЪЕДИНЕНИЕ: При использовании ОБЪЕДИНЕНИЯ является возможные toohave несколько входов, которые ссылаются toohello **же** концентратора и потребителем группы событий.</span><span class="sxs-lookup"><span data-stu-id="28b81-116">UNION: When you use a UNION, it's possible toohave multiple inputs that refer toohello **same** event hub and consumer group.</span></span>
* <span data-ttu-id="28b81-117">САМОСОЕДИНЕНИЕ: При использовании операции СОЕДИНЕНИЯ SELF, это возможно toorefer toohello **же** концентратора событий несколько раз.</span><span class="sxs-lookup"><span data-stu-id="28b81-117">SELF JOIN: When you use a SELF JOIN operation, it's possible toorefer toohello **same** event hub multiple times.</span></span>

## <a name="solution"></a><span data-ttu-id="28b81-118">Решение</span><span class="sxs-lookup"><span data-stu-id="28b81-118">Solution</span></span>

<span data-ttu-id="28b81-119">Hello следующие рекомендации могут помочь успешного выполнения сценариев, в которых hello числа агентов чтения на каждую секцию превышает предел концентраторов событий hello пяти.</span><span class="sxs-lookup"><span data-stu-id="28b81-119">hello following best practices can help mitigate scenarios in which hello number of readers per partition exceeds hello Event Hubs limit of five.</span></span>

### <a name="split-your-query-into-multiple-steps-by-using-a-with-clause"></a><span data-ttu-id="28b81-120">Разбиение запроса на несколько шагов с помощью предложения WITH</span><span class="sxs-lookup"><span data-stu-id="28b81-120">Split your query into multiple steps by using a WITH clause</span></span>

<span data-ttu-id="28b81-121">предложение WITH Hello указывает временный именованный результирующий набор, который может ссылаться предложение FROM в запросе hello.</span><span class="sxs-lookup"><span data-stu-id="28b81-121">hello WITH clause specifies a temporary named result set that can be referenced by a FROM clause in hello query.</span></span> <span data-ttu-id="28b81-122">Предложение WITH hello определить hello области выполнения одиночной инструкции SELECT.</span><span class="sxs-lookup"><span data-stu-id="28b81-122">You define hello WITH clause in hello execution scope of a single SELECT statement.</span></span>

<span data-ttu-id="28b81-123">Например, вместо этого запроса:</span><span class="sxs-lookup"><span data-stu-id="28b81-123">For example, instead of this query:</span></span>

```
SELECT foo 
INTO output1
FROM inputEventHub

SELECT bar
INTO output2
FROM inputEventHub 
…
```

<span data-ttu-id="28b81-124">Используйте этот:</span><span class="sxs-lookup"><span data-stu-id="28b81-124">Use this query:</span></span>

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

### <a name="ensure-that-inputs-bind-toodifferent-consumer-groups"></a><span data-ttu-id="28b81-125">Убедитесь, что входные данные привязки toodifferent групп потребителей</span><span class="sxs-lookup"><span data-stu-id="28b81-125">Ensure that inputs bind toodifferent consumer groups</span></span>

<span data-ttu-id="28b81-126">Для запросов, в которых три или более входов не подключенных toohello же потребителей концентраторов событий группы, создать отдельный потребителя группы.</span><span class="sxs-lookup"><span data-stu-id="28b81-126">For queries in which three or more inputs are connected toohello same Event Hubs consumer group, create separate consumer groups.</span></span> <span data-ttu-id="28b81-127">Это требует создания hello дополнительных входных данных Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="28b81-127">This requires hello creation of additional Stream Analytics inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="28b81-128">Получение справки</span><span class="sxs-lookup"><span data-stu-id="28b81-128">Get help</span></span>
<span data-ttu-id="28b81-129">Дополнительную помощь вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="28b81-129">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="28b81-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="28b81-130">Next steps</span></span>
* [<span data-ttu-id="28b81-131">Введение tooStream аналитика</span><span class="sxs-lookup"><span data-stu-id="28b81-131">Introduction tooStream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="28b81-132">Приступая к работе с Azure Stream Analytics: выявление мошенничества в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="28b81-132">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="28b81-133">Масштабирование заданий Azure Stream Analytics для повышения пропускной способности базы данных</span><span class="sxs-lookup"><span data-stu-id="28b81-133">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* <span data-ttu-id="28b81-134">[Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) (Справочник по языку запросов Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="28b81-134">[Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx)</span></span>
* <span data-ttu-id="28b81-135">[Stream Analytics management REST API reference](https://msdn.microsoft.com/library/azure/dn835031.aspx) (Справочник по API-интерфейсу REST для управления Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="28b81-135">[Stream Analytics management REST API reference](https://msdn.microsoft.com/library/azure/dn835031.aspx)</span></span>
