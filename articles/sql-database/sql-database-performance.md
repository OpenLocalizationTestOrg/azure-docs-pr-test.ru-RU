---
title: "Мониторинг и повышение производительности базы данных SQL Azure | Документация Майкрософт"
description: "База данных SQL Azure предоставляет средства оценки производительности для выявления областей, которые могут улучшить производительность текущих запросов."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: a60b75ac-cf27-4d73-8322-ee4d4c448aa2
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/19/2016
ms.author: sstein
ms.openlocfilehash: 522b932ab055978c52f085dbaa36095bb6b77962
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-improve-performance"></a><span data-ttu-id="9fa91-103">Мониторинг и повышение производительности</span><span class="sxs-lookup"><span data-stu-id="9fa91-103">Monitor and improve performance</span></span>
<span data-ttu-id="9fa91-104">База данных SQL Azure выявляет потенциальные проблемы в базе данных и рекомендует действия, которые могут увеличить производительность рабочей нагрузки, предлагая интеллектуальные действия по настройке и рекомендации.</span><span class="sxs-lookup"><span data-stu-id="9fa91-104">Azure SQL Database identifies potential problems in your database and recommends actions that can improve performance of your workload by providing intelligent tuning actions and recommendations.</span></span>

<span data-ttu-id="9fa91-105">Чтобы проверить производительность базы данных, воспользуйтесь элементом **Производительность** на странице "Обзор" или перейдите к разделу "Поддержка и устранение неполадок".</span><span class="sxs-lookup"><span data-stu-id="9fa91-105">To review your database performance, use the **Performance** tile on the Overview page, or navigate down to "Support + troubleshooting" section:</span></span>

   ![Производительность просмотра](./media/sql-database-performance/entries.png)

<span data-ttu-id="9fa91-107">В разделе "Поддержка и устранение неполадок" можно воспользоваться следующими страницами:</span><span class="sxs-lookup"><span data-stu-id="9fa91-107">In the "Support + troubleshooting" section, you can use the following pages:</span></span>


1. <span data-ttu-id="9fa91-108">Страница [Обзор производительности](#performance-overview) позволяет отслеживать производительность базы данных.</span><span class="sxs-lookup"><span data-stu-id="9fa91-108">[Performance overview](#performance-overview) to monitor performance of your database.</span></span> 
2. <span data-ttu-id="9fa91-109">На странице [Рекомендации по производительности](#performance-recommendations) можно найти рекомендации по производительности, которые могут увеличить производительность рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="9fa91-109">[Performance recommendations](#performance-recommendations) to find performance recommendations that can improve performance of your workload.</span></span>
3. <span data-ttu-id="9fa91-110">На странице [Анализ производительности запросов](#query-performance-insight) можно найти список основных запросов, использующих больше всего ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9fa91-110">[Query Performance Insight](#query-performance-insight) to find top resource consuming queries.</span></span>
4. <span data-ttu-id="9fa91-111">На странице [Автонастройка](#automatic-tuning) можно настроить Базу данных SQL Azure для автоматической оптимизации вашей базы данных.</span><span class="sxs-lookup"><span data-stu-id="9fa91-111">[Automatic tuning](#automatic-tuning) to let Azure SQL Database automatically optimize your database.</span></span>

## <a name="performance-overview"></a><span data-ttu-id="9fa91-112">Общие сведения о производительности</span><span class="sxs-lookup"><span data-stu-id="9fa91-112">Performance Overview</span></span>
<span data-ttu-id="9fa91-113">Это представление содержит сводку данных по производительности базы данных и помогает в настройке производительности и устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="9fa91-113">This view provides a summary of your database performance, and helps you with performance tuning and troubleshooting.</span></span> 

![Производительность](./media/sql-database-performance/performance.png)

* <span data-ttu-id="9fa91-115">Элемент **Рекомендации** содержит разбор рекомендаций по настройке базы данных (если рекомендаций много, отображаются только первые три).</span><span class="sxs-lookup"><span data-stu-id="9fa91-115">The **Recommendations** tile provides a breakdown of tuning recommendations for your database (top three recommendations are shown if there are more).</span></span> <span data-ttu-id="9fa91-116">Если щелкнуть этот элемент, отобразится страница **[Рекомендации по производительности](#performance-recommendations)**.</span><span class="sxs-lookup"><span data-stu-id="9fa91-116">Clicking this tile takes you to **[Performance recommendations](#performance-recommendations)**.</span></span> 
* <span data-ttu-id="9fa91-117">Элемент **Действие настройки** содержит сводные данные о текущих и выполненных действиях настройки базы данных и позволяет быстро получить представление об истории действий настройки.</span><span class="sxs-lookup"><span data-stu-id="9fa91-117">The **Tuning activity** tile provides a summary of the ongoing and completed tuning actions for your database, giving you a quick view into the history of tuning activity.</span></span> <span data-ttu-id="9fa91-118">Щелчок по этой плитке открывает полную историю настройки вашей базы данных.</span><span class="sxs-lookup"><span data-stu-id="9fa91-118">Clicking this tile takes you to the full tuning history view for your database.</span></span>
* <span data-ttu-id="9fa91-119">В элементе **Автонастройка** отображается [конфигурация автоматической настройки](sql-database-automatic-tuning-enable.md) вашей базы данных (какие действия по настройке применяются к базе данных автоматически).</span><span class="sxs-lookup"><span data-stu-id="9fa91-119">The **Auto-tuning** tile shows the [auto-tuning configuration](sql-database-automatic-tuning-enable.md) for your database (tuning options that are automatically applied to your database).</span></span> <span data-ttu-id="9fa91-120">Щелкнув по этой плитке, вы откроете диалоговое окно настройки автоматизации.</span><span class="sxs-lookup"><span data-stu-id="9fa91-120">Clicking this tile opens the automation configuration dialog.</span></span>
* <span data-ttu-id="9fa91-121">На элементе **Запросы к базе данных** отображаются сводные данные о производительности запросов к вашей базе данных (общий объем использования DTU и наиболее ресурсоемкие запросы).</span><span class="sxs-lookup"><span data-stu-id="9fa91-121">The **Database queries** tile shows the summary of the query performance for your database (overall DTU usage and top resource consuming queries).</span></span> <span data-ttu-id="9fa91-122">Если щелкнуть этот элемент, отобразится страница **[Анализ производительности запросов](#query-performance-insight)**.</span><span class="sxs-lookup"><span data-stu-id="9fa91-122">Clicking this tile takes you to **[Query Performance Insight](#query-performance-insight)**.</span></span>

## <a name="performance-recommendations"></a><span data-ttu-id="9fa91-123">Рекомендации по производительности</span><span class="sxs-lookup"><span data-stu-id="9fa91-123">Performance recommendations</span></span>
<span data-ttu-id="9fa91-124">На этой странице отображаются интеллектуальные [рекомендации по настройке](sql-database-advisor.md), способные повысить производительность базы данных.</span><span class="sxs-lookup"><span data-stu-id="9fa91-124">This page provides intelligent [tuning recommendations](sql-database-advisor.md) that can improve your database's performance.</span></span> <span data-ttu-id="9fa91-125">На этой странице отображаются рекомендации следующих типов.</span><span class="sxs-lookup"><span data-stu-id="9fa91-125">The following types of recommendations are shown on this page:</span></span>

* <span data-ttu-id="9fa91-126">Рекомендации по созданию или удалению индексов.</span><span class="sxs-lookup"><span data-stu-id="9fa91-126">Recommendations on which indexes to create or drop.</span></span>
* <span data-ttu-id="9fa91-127">Рекомендации по действиям при обнаружении ошибок схемы в базе данных.</span><span class="sxs-lookup"><span data-stu-id="9fa91-127">Recommendations when schema issues are identified in the database.</span></span>
* <span data-ttu-id="9fa91-128">Рекомендации по использованию параметризованных запросов для повышения производительности запросов.</span><span class="sxs-lookup"><span data-stu-id="9fa91-128">Recommendations when queries can benefit from parameterized queries.</span></span>

![Производительность](./media/sql-database-performance/recommendations.png)

<span data-ttu-id="9fa91-130">Кроме того, вам доступен полный журнал действий по настройке, которые были применены ранее.</span><span class="sxs-lookup"><span data-stu-id="9fa91-130">You can also find complete history of tuning actions that were applied in the past.</span></span>

<span data-ttu-id="9fa91-131">Узнать, как найти и применить рекомендации по производительности, можно в статье [Поиск и применение рекомендаций по производительности](sql-database-advisor-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9fa91-131">Learn how to find an apply performance recommendations in [Find and apply performance recommendations](sql-database-advisor-portal.md) article.</span></span>

## <a name="automatic-tuning"></a><span data-ttu-id="9fa91-132">Автоматическая настройка</span><span class="sxs-lookup"><span data-stu-id="9fa91-132">Automatic tuning</span></span>
<span data-ttu-id="9fa91-133">База данных SQL Azure может автоматически настраивать производительность базы данных, применяя [рекомендации по производительности](sql-database-advisor.md).</span><span class="sxs-lookup"><span data-stu-id="9fa91-133">Azure SQL Databases can automatically tune database performance by applying [performance recommendations](sql-database-advisor.md).</span></span> <span data-ttu-id="9fa91-134">Чтобы узнать больше, прочитайте статью [Автоматическая настройка](sql-database-automatic-tuning.md).</span><span class="sxs-lookup"><span data-stu-id="9fa91-134">To learn more, read [Automatic tuning article](sql-database-automatic-tuning.md).</span></span> <span data-ttu-id="9fa91-135">Кроме того, вы можете узнать, [как включить автоматическую настройку](sql-database-automatic-tuning-enable.md).</span><span class="sxs-lookup"><span data-stu-id="9fa91-135">To enable it, read [how to enable automatic tuning](sql-database-automatic-tuning-enable.md).</span></span>

## <a name="query-performance-insight"></a><span data-ttu-id="9fa91-136">анализ производительности запросов</span><span class="sxs-lookup"><span data-stu-id="9fa91-136">Query Performance Insight</span></span>
<span data-ttu-id="9fa91-137">[Анализ производительности запросов](sql-database-query-performance.md) позволяет тратить меньше времени на устранение неполадок с производительностью базы данных, предоставляя следующие возможности.</span><span class="sxs-lookup"><span data-stu-id="9fa91-137">[Query Performance Insight](sql-database-query-performance.md) allows you to spend less time troubleshooting database performance by providing:</span></span>

* <span data-ttu-id="9fa91-138">Более глубокое понимание потребления ресурсов базы данных (DTU).</span><span class="sxs-lookup"><span data-stu-id="9fa91-138">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="9fa91-139">Определение запросов, максимально использующих ресурсы процессора. Этот показатель можно настроить и улучшить производительность.</span><span class="sxs-lookup"><span data-stu-id="9fa91-139">The top CPU consuming queries, which can potentially be tuned for improved performance.</span></span> 
* <span data-ttu-id="9fa91-140">Возможность получить подробные сведения о запросе.</span><span class="sxs-lookup"><span data-stu-id="9fa91-140">The ability to drill down into the details of a query.</span></span> 

  ![панель мониторинга производительности](./media/sql-database-query-performance/performance.png)

<span data-ttu-id="9fa91-142">Дополнительные сведения об этой странице можно найти в статье **[Анализ производительности запросов базы данных Azure SQL](sql-database-query-performance.md)**.</span><span class="sxs-lookup"><span data-stu-id="9fa91-142">Find more information about this page in the article **[How to use Query Performance Insight](sql-database-query-performance.md)**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9fa91-143">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9fa91-143">Additional resources</span></span>
* [<span data-ttu-id="9fa91-144">Руководство по производительности базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="9fa91-144">Azure SQL Database performance guidance for single databases</span></span>](sql-database-performance-guidance.md)
* [<span data-ttu-id="9fa91-145">Когда следует использовать эластичный пул?</span><span class="sxs-lookup"><span data-stu-id="9fa91-145">When should an elastic pool be used?</span></span>](sql-database-elastic-pool-guidance.md)

