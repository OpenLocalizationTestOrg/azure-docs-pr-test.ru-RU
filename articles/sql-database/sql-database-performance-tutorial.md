---
title: "производительность aaaTroubleshoot проблемы и оптимизации базы данных | Документы Microsoft"
description: "Применить tooyour рекомендации по производительности базы данных SQL, а также чистить как toogain ценной информации о hello производительность hello запросы, выполняемые для базы данных"
metakeywords: azure sql database performance monitoring recommendation
services: sql-database
documentationcenter: 
manager: jhubbard
author: jan-eng
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,monitor & tune
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: janeng
ms.openlocfilehash: e948d30ac74eecf45420d5d77ef55e3c0b6f3f47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-performance-issues-and-optimize-your-database"></a><span data-ttu-id="b2b64-103">Устранение проблем с производительностью и оптимизация базы данных</span><span class="sxs-lookup"><span data-stu-id="b2b64-103">Troubleshoot performance issues and optimize your database</span></span>

<span data-ttu-id="b2b64-104">Отсутствующие индексы и плохо оптимизированные запросы — распространенные причины низкой производительности баз данных.</span><span class="sxs-lookup"><span data-stu-id="b2b64-104">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="b2b64-105">Из этого руководства вы узнаете, как выполнять такие задачи.</span><span class="sxs-lookup"><span data-stu-id="b2b64-105">In this tutorial you learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="b2b64-106">Просмотр и применение рекомендаций по улучшению производительности и их отмена.</span><span class="sxs-lookup"><span data-stu-id="b2b64-106">Review, apply and revert performance improvement recommendations</span></span>
> * <span data-ttu-id="b2b64-107">Поиск ресурсоемких запросов.</span><span class="sxs-lookup"><span data-stu-id="b2b64-107">Find queries with high resource utilization</span></span>
> * <span data-ttu-id="b2b64-108">Поиск долго выполняющихся запросов.</span><span class="sxs-lookup"><span data-stu-id="b2b64-108">Find long running queries</span></span>

> <span data-ttu-id="b2b64-109">Необходимо непрерывного рабочей нагрузки на базу данных с проблемами производительности — отсутствующих в индексе, например tooreceive рекомендации.</span><span class="sxs-lookup"><span data-stu-id="b2b64-109">You need a continuous workload on a database with performance issues – missing an index for example tooreceive a recommendation.</span></span>
>

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="b2b64-110">Войдите в toohello портал Azure</span><span class="sxs-lookup"><span data-stu-id="b2b64-110">Log in toohello Azure portal</span></span>

<span data-ttu-id="b2b64-111">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b2b64-111">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="review-and-apply-a-recommendation"></a><span data-ttu-id="b2b64-112">Просмотр и применение рекомендации</span><span class="sxs-lookup"><span data-stu-id="b2b64-112">Review and apply a recommendation</span></span>

<span data-ttu-id="b2b64-113">Выполните эти шаги tooapply рекомендации из системы hello для базы данных.</span><span class="sxs-lookup"><span data-stu-id="b2b64-113">Follow these steps tooapply a recommendation from hello system for your database:</span></span>

1. <span data-ttu-id="b2b64-114">Нажмите кнопку hello **рекомендации по повышению производительности** меню в колонке базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="b2b64-114">Click hello **Performance recommendations** menu in hello database blade.</span></span>

    ![рекомендации по производительности](./media/sql-database-performance-tutorial/perf_recommendations.png)

2. <span data-ttu-id="b2b64-116">Выберите из списка hello рекомендаций active рекомендации.</span><span class="sxs-lookup"><span data-stu-id="b2b64-116">From hello list of recommendations, select an active recommendation.</span></span> <span data-ttu-id="b2b64-117">В нашем примере это "Создание индекса".</span><span class="sxs-lookup"><span data-stu-id="b2b64-117">In this example, Create Index.</span></span>

    ![выбор рекомендации](./media/sql-database-performance-tutorial/create_index.png)

3. <span data-ttu-id="b2b64-119">Примените рекомендацию hello, щелкнув hello **применить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="b2b64-119">Apply hello recommendation by clicking hello **Apply** button.</span></span> <span data-ttu-id="b2b64-120">При необходимости просмотрите сведения о рекомендация hello и просмотреть скрипт hello T-SQL, щелкнув выполняться слишком **просмотреть скрипт** кнопки.</span><span class="sxs-lookup"><span data-stu-id="b2b64-120">Optionally, review hello recommendation details and see hello T-SQL script too be executed by clicking on **View Script** button.</span></span>

    ![применение рекомендации](./media/sql-database-performance-tutorial/apply.png)

4. <span data-ttu-id="b2b64-122">[Необязательно] Включение автоматической настройки для toobe рекомендации применяются автоматически.</span><span class="sxs-lookup"><span data-stu-id="b2b64-122">[Optional] Enable automatic tuning for recommendations toobe applied automatically.</span></span>

    ![автоматическая настройка](./media/sql-database-performance-tutorial/auto_tuning.png)

## <a name="revert-a-recommendation"></a><span data-ttu-id="b2b64-124">Отмена рекомендации</span><span class="sxs-lookup"><span data-stu-id="b2b64-124">Revert a recommendation</span></span>

<span data-ttu-id="b2b64-125">Hello ядра СУБД отслеживает каждой рекомендации по реализации.</span><span class="sxs-lookup"><span data-stu-id="b2b64-125">hello Database Advisor monitors every recommendation implemented.</span></span> <span data-ttu-id="b2b64-126">Если рекомендации не повысить hello рабочей нагрузки, которые будут автоматически отменены.</span><span class="sxs-lookup"><span data-stu-id="b2b64-126">If a recommendation doesn't improve hello workload it will be automatically reverted.</span></span> <span data-ttu-id="b2b64-127">Рекомендацию также можно отменить вручную, но в большинстве случаев это не требуется.</span><span class="sxs-lookup"><span data-stu-id="b2b64-127">Manually reverting a recommendation is possible, but not necessary in most cases.</span></span> <span data-ttu-id="b2b64-128">toorevert рекомендации:</span><span class="sxs-lookup"><span data-stu-id="b2b64-128">toorevert a recommendation:</span></span>

1. <span data-ttu-id="b2b64-129">Перейдите в меню рекомендации toohello производительности и выберите один из hello применения рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="b2b64-129">Go toohello performance recommendations menu and select one of hello applied recommendations.</span></span>

    ![выбор рекомендации](./media/sql-database-performance-tutorial/select.png)

2. <span data-ttu-id="b2b64-131">В представлении details hello, нажмите кнопку **Revert**.</span><span class="sxs-lookup"><span data-stu-id="b2b64-131">In hello details view, click **Revert**.</span></span>

    ![отмена рекомендации](./media/sql-database-performance-tutorial/revert.png)

## <a name="find-hello-query-that-consumes-hello-most-resources"></a><span data-ttu-id="b2b64-133">Найти hello запроса, использующего hello больше всего ресурсов</span><span class="sxs-lookup"><span data-stu-id="b2b64-133">Find hello query that consumes hello most resources</span></span>

<span data-ttu-id="b2b64-134">Выполните эти шаги toofind hello запрос использует hello больше всего ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b2b64-134">Follow these steps toofind hello query consuming hello most resources:</span></span>

1. <span data-ttu-id="b2b64-135">Щелкните hello **анализ производительности запросов** меню в колонке базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="b2b64-135">Click on hello **Query Performance Insight** menu in hello database blade.</span></span>

    ![анализ запросов](./media/sql-database-performance-tutorial/query_perf_insights.png)

2. <span data-ttu-id="b2b64-137">Выберите тип ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b2b64-137">Select a resource type.</span></span>

    ![анализ запросов](./media/sql-database-performance-tutorial/select_resource_type.png)

3. <span data-ttu-id="b2b64-139">Выберите первый запрос hello в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="b2b64-139">Select hello first query in hello table.</span></span>

    ![анализ запросов](./media/sql-database-performance-tutorial/select_query.png)

4. <span data-ttu-id="b2b64-141">Просмотрите сведения о запросе hello.</span><span class="sxs-lookup"><span data-stu-id="b2b64-141">Review hello query details.</span></span>

    ![анализ запросов](./media/sql-database-performance-tutorial/query_details.png)

## <a name="find-hello-longest-running-query"></a><span data-ttu-id="b2b64-143">Найти наиболее долго выполняющегося запроса hello</span><span class="sxs-lookup"><span data-stu-id="b2b64-143">Find hello longest running query</span></span>

1. <span data-ttu-id="b2b64-144">Откройте tooQuery анализ производительности и выберите hello **длительных запросов** вкладки.</span><span class="sxs-lookup"><span data-stu-id="b2b64-144">Go tooQuery Performance Insight and select hello **Long running queries** tab.</span></span>

    ![анализ запросов](./media/sql-database-performance-tutorial/long_running.png)

3. <span data-ttu-id="b2b64-146">Выберите первый запрос hello в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="b2b64-146">Select hello first query in hello table.</span></span>

    ![анализ запросов](./media/sql-database-performance-tutorial/select_first_query.png)

4. <span data-ttu-id="b2b64-148">Просмотрите сведения о запросе hello.</span><span class="sxs-lookup"><span data-stu-id="b2b64-148">Review hello query details.</span></span>

    ![анализ запросов](./media/sql-database-performance-tutorial/review_query_details.png)



## <a name="next-steps"></a><span data-ttu-id="b2b64-150">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b2b64-150">Next steps</span></span> 
<span data-ttu-id="b2b64-151">Отсутствующие индексы и плохо оптимизированные запросы — распространенные причины низкой производительности баз данных.</span><span class="sxs-lookup"><span data-stu-id="b2b64-151">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="b2b64-152">Из этого руководства вы узнали, как выполнять следующие операции:</span><span class="sxs-lookup"><span data-stu-id="b2b64-152">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="b2b64-153">Просмотр и применение рекомендаций по улучшению производительности и их отмена.</span><span class="sxs-lookup"><span data-stu-id="b2b64-153">Review, apply and revert performance improvement recommendations</span></span>
> * <span data-ttu-id="b2b64-154">Поиск ресурсоемких запросов.</span><span class="sxs-lookup"><span data-stu-id="b2b64-154">Find queries with high resource utilization</span></span>
> * <span data-ttu-id="b2b64-155">Поиск долго выполняющихся запросов.</span><span class="sxs-lookup"><span data-stu-id="b2b64-155">Find long running queries</span></span>

[<span data-ttu-id="b2b64-156">Советы по настройке производительности базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="b2b64-156">SQL Database performance tuning tips</span></span>](https://docs.microsoft.com/azure/sql-database/sql-database-troubleshoot-performance)
