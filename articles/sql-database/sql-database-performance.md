---
title: "aaaMonitor и повысить производительность - базы данных SQL Azure | Документы Microsoft"
description: "База данных SQL Azure обеспечивает производительность приветствия средств toohelp, определяющие области, которые может повысить производительность текущего запроса."
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
ms.openlocfilehash: 84b8a1bc62698a29deb49e765f208bd7e14d0870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-improve-performance"></a><span data-ttu-id="523aa-103">Мониторинг и повышение производительности</span><span class="sxs-lookup"><span data-stu-id="523aa-103">Monitor and improve performance</span></span>
<span data-ttu-id="523aa-104">База данных SQL Azure выявляет потенциальные проблемы в базе данных и рекомендует действия, которые могут увеличить производительность рабочей нагрузки, предлагая интеллектуальные действия по настройке и рекомендации.</span><span class="sxs-lookup"><span data-stu-id="523aa-104">Azure SQL Database identifies potential problems in your database and recommends actions that can improve performance of your workload by providing intelligent tuning actions and recommendations.</span></span>

<span data-ttu-id="523aa-105">tooreview на производительность базы данных, используйте hello **производительности** плитки на страницу обзора hello, или перейдите вниз слишком «Поддержка + Устранение неполадок» раздела:</span><span class="sxs-lookup"><span data-stu-id="523aa-105">tooreview your database performance, use hello **Performance** tile on hello Overview page, or navigate down too"Support + troubleshooting" section:</span></span>

   ![Производительность просмотра](./media/sql-database-performance/entries.png)

<span data-ttu-id="523aa-107">В разделе hello «Поддержка + Устранение неполадок» можно использовать следующие страницы приветствия:</span><span class="sxs-lookup"><span data-stu-id="523aa-107">In hello "Support + troubleshooting" section, you can use hello following pages:</span></span>


1. <span data-ttu-id="523aa-108">[Общие сведения о производительности](#performance-overview) toomonitor производительность базы данных.</span><span class="sxs-lookup"><span data-stu-id="523aa-108">[Performance overview](#performance-overview) toomonitor performance of your database.</span></span> 
2. <span data-ttu-id="523aa-109">[Рекомендации по повышению производительности](#performance-recommendations) toofind рекомендации по повышению производительности, которые могут увеличить производительность рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="523aa-109">[Performance recommendations](#performance-recommendations) toofind performance recommendations that can improve performance of your workload.</span></span>
3. <span data-ttu-id="523aa-110">[Анализ производительности запросов](#query-performance-insight) toofind запросов использования ресурсов.</span><span class="sxs-lookup"><span data-stu-id="523aa-110">[Query Performance Insight](#query-performance-insight) toofind top resource consuming queries.</span></span>
4. <span data-ttu-id="523aa-111">[Автоматической настройки](#automatic-tuning) toolet базы данных SQL Azure автоматически оптимизации базы данных.</span><span class="sxs-lookup"><span data-stu-id="523aa-111">[Automatic tuning](#automatic-tuning) toolet Azure SQL Database automatically optimize your database.</span></span>

## <a name="performance-overview"></a><span data-ttu-id="523aa-112">Общие сведения о производительности</span><span class="sxs-lookup"><span data-stu-id="523aa-112">Performance Overview</span></span>
<span data-ttu-id="523aa-113">Это представление содержит сводку данных по производительности базы данных и помогает в настройке производительности и устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="523aa-113">This view provides a summary of your database performance, and helps you with performance tuning and troubleshooting.</span></span> 

![Производительность](./media/sql-database-performance/performance.png)

* <span data-ttu-id="523aa-115">Hello **рекомендации** плитки приводится декомпозиция рекомендаций по настройке для базы данных (первые три рекомендаций показаны Если есть и другие).</span><span class="sxs-lookup"><span data-stu-id="523aa-115">hello **Recommendations** tile provides a breakdown of tuning recommendations for your database (top three recommendations are shown if there are more).</span></span> <span data-ttu-id="523aa-116">Щелкните эту плитку осуществляется слишком**[рекомендации по повышению производительности](#performance-recommendations)**.</span><span class="sxs-lookup"><span data-stu-id="523aa-116">Clicking this tile takes you too**[Performance recommendations](#performance-recommendations)**.</span></span> 
* <span data-ttu-id="523aa-117">Hello **действия по настройке** плитки Сводная информация о hello выполняющихся и завершенных, помощник по настройке действия для базы данных, позволяя быстро получить представление hello журнал действий по настройке.</span><span class="sxs-lookup"><span data-stu-id="523aa-117">hello **Tuning activity** tile provides a summary of hello ongoing and completed tuning actions for your database, giving you a quick view into hello history of tuning activity.</span></span> <span data-ttu-id="523aa-118">Щелкните эту плитку принимает toohello полной настройки представления журнала для базы данных.</span><span class="sxs-lookup"><span data-stu-id="523aa-118">Clicking this tile takes you toohello full tuning history view for your database.</span></span>
* <span data-ttu-id="523aa-119">Hello **автоматической настройки** отражает hello [автоматической настройки конфигурации](sql-database-automatic-tuning-enable.md) для базы данных (параметров настройки, будут автоматически применяться tooyour базы данных).</span><span class="sxs-lookup"><span data-stu-id="523aa-119">hello **Auto-tuning** tile shows hello [auto-tuning configuration](sql-database-automatic-tuning-enable.md) for your database (tuning options that are automatically applied tooyour database).</span></span> <span data-ttu-id="523aa-120">Эта Плитка открывают диалоговое окно конфигурации автоматизации hello.</span><span class="sxs-lookup"><span data-stu-id="523aa-120">Clicking this tile opens hello automation configuration dialog.</span></span>
* <span data-ttu-id="523aa-121">Hello **запросов баз данных** отражает hello Сводка hello производительность запросов для базы данных (Общая DTU использования и top-запросов использования ресурсов).</span><span class="sxs-lookup"><span data-stu-id="523aa-121">hello **Database queries** tile shows hello summary of hello query performance for your database (overall DTU usage and top resource consuming queries).</span></span> <span data-ttu-id="523aa-122">Щелкните эту плитку осуществляется слишком**[анализ производительности запросов](#query-performance-insight)**.</span><span class="sxs-lookup"><span data-stu-id="523aa-122">Clicking this tile takes you too**[Query Performance Insight](#query-performance-insight)**.</span></span>

## <a name="performance-recommendations"></a><span data-ttu-id="523aa-123">Рекомендации по производительности</span><span class="sxs-lookup"><span data-stu-id="523aa-123">Performance recommendations</span></span>
<span data-ttu-id="523aa-124">На этой странице отображаются интеллектуальные [рекомендации по настройке](sql-database-advisor.md), способные повысить производительность базы данных.</span><span class="sxs-lookup"><span data-stu-id="523aa-124">This page provides intelligent [tuning recommendations](sql-database-advisor.md) that can improve your database's performance.</span></span> <span data-ttu-id="523aa-125">на этой странице отображаются следующие типы рекомендаций Hello.</span><span class="sxs-lookup"><span data-stu-id="523aa-125">hello following types of recommendations are shown on this page:</span></span>

* <span data-ttu-id="523aa-126">Рекомендации по какие индексы toocreate или drop.</span><span class="sxs-lookup"><span data-stu-id="523aa-126">Recommendations on which indexes toocreate or drop.</span></span>
* <span data-ttu-id="523aa-127">Рекомендации по проблемы схемы определяются в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="523aa-127">Recommendations when schema issues are identified in hello database.</span></span>
* <span data-ttu-id="523aa-128">Рекомендации по использованию параметризованных запросов для повышения производительности запросов.</span><span class="sxs-lookup"><span data-stu-id="523aa-128">Recommendations when queries can benefit from parameterized queries.</span></span>

![Производительность](./media/sql-database-performance/recommendations.png)

<span data-ttu-id="523aa-130">Также можно найти полный журнал настройки действий, которые были применены в прошлом hello.</span><span class="sxs-lookup"><span data-stu-id="523aa-130">You can also find complete history of tuning actions that were applied in hello past.</span></span>

<span data-ttu-id="523aa-131">Узнайте, как toofind применить рекомендации по повышению производительности в [поиска и применить рекомендации по повышению производительности](sql-database-advisor-portal.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="523aa-131">Learn how toofind an apply performance recommendations in [Find and apply performance recommendations](sql-database-advisor-portal.md) article.</span></span>

## <a name="automatic-tuning"></a><span data-ttu-id="523aa-132">Автоматическая настройка</span><span class="sxs-lookup"><span data-stu-id="523aa-132">Automatic tuning</span></span>
<span data-ttu-id="523aa-133">База данных SQL Azure может автоматически настраивать производительность базы данных, применяя [рекомендации по производительности](sql-database-advisor.md).</span><span class="sxs-lookup"><span data-stu-id="523aa-133">Azure SQL Databases can automatically tune database performance by applying [performance recommendations](sql-database-advisor.md).</span></span> <span data-ttu-id="523aa-134">лучше, ознакомьтесь с toolearn [автоматической настройки статьи](sql-database-automatic-tuning.md).</span><span class="sxs-lookup"><span data-stu-id="523aa-134">toolearn more, read [Automatic tuning article](sql-database-automatic-tuning.md).</span></span> <span data-ttu-id="523aa-135">чтение tooenable, [как автоматической настройки tooenable](sql-database-automatic-tuning-enable.md).</span><span class="sxs-lookup"><span data-stu-id="523aa-135">tooenable it, read [how tooenable automatic tuning](sql-database-automatic-tuning-enable.md).</span></span>

## <a name="query-performance-insight"></a><span data-ttu-id="523aa-136">Анализ производительности запросов</span><span class="sxs-lookup"><span data-stu-id="523aa-136">Query Performance Insight</span></span>
<span data-ttu-id="523aa-137">[Анализ производительности запросов](sql-database-query-performance.md) позволяет toospend меньше времени, устранение неполадок производительности базы данных, указав:</span><span class="sxs-lookup"><span data-stu-id="523aa-137">[Query Performance Insight](sql-database-query-performance.md) allows you toospend less time troubleshooting database performance by providing:</span></span>

* <span data-ttu-id="523aa-138">Более глубокое понимание потребления ресурсов базы данных (DTU).</span><span class="sxs-lookup"><span data-stu-id="523aa-138">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="523aa-139">Hello Процессора, запросы, которые потенциально могут настраиваться для повышения производительности.</span><span class="sxs-lookup"><span data-stu-id="523aa-139">hello top CPU consuming queries, which can potentially be tuned for improved performance.</span></span> 
* <span data-ttu-id="523aa-140">Здравствуйте toodrill возможность работы в детали hello запроса.</span><span class="sxs-lookup"><span data-stu-id="523aa-140">hello ability toodrill down into hello details of a query.</span></span> 

  ![панель мониторинга производительности](./media/sql-database-query-performance/performance.png)

<span data-ttu-id="523aa-142">Дополнительные сведения об этой странице найти в статье hello  **[как toouse анализ производительности запросов](sql-database-query-performance.md)**.</span><span class="sxs-lookup"><span data-stu-id="523aa-142">Find more information about this page in hello article **[How toouse Query Performance Insight](sql-database-query-performance.md)**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="523aa-143">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="523aa-143">Additional resources</span></span>
* [<span data-ttu-id="523aa-144">Руководство по производительности базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="523aa-144">Azure SQL Database performance guidance for single databases</span></span>](sql-database-performance-guidance.md)
* [<span data-ttu-id="523aa-145">Когда следует использовать эластичный пул?</span><span class="sxs-lookup"><span data-stu-id="523aa-145">When should an elastic pool be used?</span></span>](sql-database-elastic-pool-guidance.md)

