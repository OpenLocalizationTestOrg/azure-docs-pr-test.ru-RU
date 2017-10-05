---
title: "Устранение проблем с производительностью и оптимизация базы данных | Документация Майкрософт"
description: "Применяйте рекомендации по повышению производительности базы данных SQL, а также узнайте, как получить ценные сведения о производительности запросов базы данных"
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
ms.openlocfilehash: f9ae96cdc80c347593f229cb2fce3f2d4d8e7caf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-performance-issues-and-optimize-your-database"></a><span data-ttu-id="d701a-103">Устранение проблем с производительностью и оптимизация базы данных</span><span class="sxs-lookup"><span data-stu-id="d701a-103">Troubleshoot performance issues and optimize your database</span></span>

<span data-ttu-id="d701a-104">Отсутствующие индексы и плохо оптимизированные запросы — распространенные причины низкой производительности баз данных.</span><span class="sxs-lookup"><span data-stu-id="d701a-104">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="d701a-105">Из этого руководства вы узнаете, как выполнять такие задачи.</span><span class="sxs-lookup"><span data-stu-id="d701a-105">In this tutorial you learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="d701a-106">Просмотр и применение рекомендаций по улучшению производительности и их отмена.</span><span class="sxs-lookup"><span data-stu-id="d701a-106">Review, apply and revert performance improvement recommendations</span></span>
> * <span data-ttu-id="d701a-107">Поиск ресурсоемких запросов.</span><span class="sxs-lookup"><span data-stu-id="d701a-107">Find queries with high resource utilization</span></span>
> * <span data-ttu-id="d701a-108">Поиск долго выполняющихся запросов.</span><span class="sxs-lookup"><span data-stu-id="d701a-108">Find long running queries</span></span>

> <span data-ttu-id="d701a-109">Чтобы получить рекомендации, вам нужна непрерывная рабочая нагрузка в базе данных с проблемами с производительностью, такими как отсутствующий индекс.</span><span class="sxs-lookup"><span data-stu-id="d701a-109">You need a continuous workload on a database with performance issues – missing an index for example to receive a recommendation.</span></span>
>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="d701a-110">Войдите на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d701a-110">Log in to the Azure portal</span></span>

<span data-ttu-id="d701a-111">Войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d701a-111">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="review-and-apply-a-recommendation"></a><span data-ttu-id="d701a-112">Просмотр и применение рекомендации</span><span class="sxs-lookup"><span data-stu-id="d701a-112">Review and apply a recommendation</span></span>

<span data-ttu-id="d701a-113">Чтобы применить рекомендацию из системы для базы данных, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="d701a-113">Follow these steps to apply a recommendation from the system for your database:</span></span>

1. <span data-ttu-id="d701a-114">В колонке базы данных щелкните меню **Рекомендации по производительности**.</span><span class="sxs-lookup"><span data-stu-id="d701a-114">Click the **Performance recommendations** menu in the database blade.</span></span>

    ![рекомендации по производительности](./media/sql-database-performance-tutorial/perf_recommendations.png)

2. <span data-ttu-id="d701a-116">Выберите активную рекомендацию из списка рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="d701a-116">From the list of recommendations, select an active recommendation.</span></span> <span data-ttu-id="d701a-117">В нашем примере это "Создание индекса".</span><span class="sxs-lookup"><span data-stu-id="d701a-117">In this example, Create Index.</span></span>

    ![выбор рекомендации](./media/sql-database-performance-tutorial/create_index.png)

3. <span data-ttu-id="d701a-119">Примените рекомендацию, нажав кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="d701a-119">Apply the recommendation by clicking the **Apply** button.</span></span> <span data-ttu-id="d701a-120">При необходимости просмотрите сведения о рекомендации и выполняемый скрипт T-SQL, нажав кнопку **Показать скрипт**.</span><span class="sxs-lookup"><span data-stu-id="d701a-120">Optionally, review the recommendation details and see the T-SQL script to  be executed by clicking on **View Script** button.</span></span>

    ![применение рекомендации](./media/sql-database-performance-tutorial/apply.png)

4. <span data-ttu-id="d701a-122">[Необязательно.] Включите автоматическую настройку для автоматического применения рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="d701a-122">[Optional] Enable automatic tuning for recommendations to be applied automatically.</span></span>

    ![автоматическая настройка](./media/sql-database-performance-tutorial/auto_tuning.png)

## <a name="revert-a-recommendation"></a><span data-ttu-id="d701a-124">Отмена рекомендации</span><span class="sxs-lookup"><span data-stu-id="d701a-124">Revert a recommendation</span></span>

<span data-ttu-id="d701a-125">Помощник по работе с базами данных отслеживает каждую внедренную рекомендацию.</span><span class="sxs-lookup"><span data-stu-id="d701a-125">The Database Advisor monitors every recommendation implemented.</span></span> <span data-ttu-id="d701a-126">Если после внедрения рекомендации производительность рабочей нагрузки не увеличилась, она будет автоматически отменена.</span><span class="sxs-lookup"><span data-stu-id="d701a-126">If a recommendation doesn't improve the workload it will be automatically reverted.</span></span> <span data-ttu-id="d701a-127">Рекомендацию также можно отменить вручную, но в большинстве случаев это не требуется.</span><span class="sxs-lookup"><span data-stu-id="d701a-127">Manually reverting a recommendation is possible, but not necessary in most cases.</span></span> <span data-ttu-id="d701a-128">Отмена рекомендации</span><span class="sxs-lookup"><span data-stu-id="d701a-128">To revert a recommendation:</span></span>

1. <span data-ttu-id="d701a-129">Перейдите в меню рекомендаций по производительности и выберите одну из примененных рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="d701a-129">Go to the performance recommendations menu and select one of the applied recommendations.</span></span>

    ![выбор рекомендации](./media/sql-database-performance-tutorial/select.png)

2. <span data-ttu-id="d701a-131">В представлении сведений щелкните **Отменить изменения**.</span><span class="sxs-lookup"><span data-stu-id="d701a-131">In the details view, click **Revert**.</span></span>

    ![отмена рекомендации](./media/sql-database-performance-tutorial/revert.png)

## <a name="find-the-query-that-consumes-the-most-resources"></a><span data-ttu-id="d701a-133">Поиск самого ресурсоемкого запроса</span><span class="sxs-lookup"><span data-stu-id="d701a-133">Find the query that consumes the most resources</span></span>

<span data-ttu-id="d701a-134">Чтобы найти запрос, использующий больше всего ресурсов, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="d701a-134">Follow these steps to find the query consuming the most resources:</span></span>

1. <span data-ttu-id="d701a-135">В колонке базы данных щелкните меню **Анализ производительности запросов**.</span><span class="sxs-lookup"><span data-stu-id="d701a-135">Click on the **Query Performance Insight** menu in the database blade.</span></span>

    ![анализ запросов](./media/sql-database-performance-tutorial/query_perf_insights.png)

2. <span data-ttu-id="d701a-137">Выберите тип ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d701a-137">Select a resource type.</span></span>

    ![анализ запросов](./media/sql-database-performance-tutorial/select_resource_type.png)

3. <span data-ttu-id="d701a-139">Выберите первый запрос в таблице.</span><span class="sxs-lookup"><span data-stu-id="d701a-139">Select the first query in the table.</span></span>

    ![анализ запросов](./media/sql-database-performance-tutorial/select_query.png)

4. <span data-ttu-id="d701a-141">Просмотрите сведения о запросе.</span><span class="sxs-lookup"><span data-stu-id="d701a-141">Review the query details.</span></span>

    ![анализ запросов](./media/sql-database-performance-tutorial/query_details.png)

## <a name="find-the-longest-running-query"></a><span data-ttu-id="d701a-143">Поиск самого длительного запроса</span><span class="sxs-lookup"><span data-stu-id="d701a-143">Find the longest running query</span></span>

1. <span data-ttu-id="d701a-144">Перейдите в меню "Анализ производительности запросов" и выберите вкладку **Длительные запросы**.</span><span class="sxs-lookup"><span data-stu-id="d701a-144">Go to Query Performance Insight and select the **Long running queries** tab.</span></span>

    ![анализ запросов](./media/sql-database-performance-tutorial/long_running.png)

3. <span data-ttu-id="d701a-146">Выберите первый запрос в таблице.</span><span class="sxs-lookup"><span data-stu-id="d701a-146">Select the first query in the table.</span></span>

    ![анализ запросов](./media/sql-database-performance-tutorial/select_first_query.png)

4. <span data-ttu-id="d701a-148">Просмотрите сведения о запросе.</span><span class="sxs-lookup"><span data-stu-id="d701a-148">Review the query details.</span></span>

    ![анализ запросов](./media/sql-database-performance-tutorial/review_query_details.png)



## <a name="next-steps"></a><span data-ttu-id="d701a-150">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d701a-150">Next steps</span></span> 
<span data-ttu-id="d701a-151">Отсутствующие индексы и плохо оптимизированные запросы — распространенные причины низкой производительности баз данных.</span><span class="sxs-lookup"><span data-stu-id="d701a-151">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="d701a-152">Из этого руководства вы узнали, как выполнять следующие операции:</span><span class="sxs-lookup"><span data-stu-id="d701a-152">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="d701a-153">Просмотр и применение рекомендаций по улучшению производительности и их отмена.</span><span class="sxs-lookup"><span data-stu-id="d701a-153">Review, apply and revert performance improvement recommendations</span></span>
> * <span data-ttu-id="d701a-154">Поиск ресурсоемких запросов.</span><span class="sxs-lookup"><span data-stu-id="d701a-154">Find queries with high resource utilization</span></span>
> * <span data-ttu-id="d701a-155">Поиск долго выполняющихся запросов.</span><span class="sxs-lookup"><span data-stu-id="d701a-155">Find long running queries</span></span>

[<span data-ttu-id="d701a-156">Советы по настройке производительности базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="d701a-156">SQL Database performance tuning tips</span></span>](https://docs.microsoft.com/azure/sql-database/sql-database-troubleshoot-performance)
