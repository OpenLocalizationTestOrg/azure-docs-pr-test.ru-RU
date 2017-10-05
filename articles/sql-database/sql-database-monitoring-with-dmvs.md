---
title: "Мониторинг базы данных SQL Azure с помощью динамических административных представлений | Документация Майкрософт"
description: "Узнайте, как выявлять и диагностировать распространенные проблемы производительности с помощью динамических представлений управления для мониторинга Базы данных SQL Microsoft Azure."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: d08f505f-3c62-47d4-bab7-35c9a834b79b
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: d9b007d29e06e672db71b4a8415673f258c3fd89
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="monitoring-azure-sql-database-using-dynamic-management-views"></a><span data-ttu-id="63301-103">Мониторинг базы данных SQL Azure с помощью динамических представлений управления</span><span class="sxs-lookup"><span data-stu-id="63301-103">Monitoring Azure SQL Database using dynamic management views</span></span>
<span data-ttu-id="63301-104">База данных SQL Microsoft Azure предлагает ряд динамических представлений управления для диагностирования проблем производительности, которые могут быть вызваны заблокированными или долго выполняющимися запросами, узкими местами ресурсов, непродуманным планом запросов и т. д.</span><span class="sxs-lookup"><span data-stu-id="63301-104">Microsoft Azure SQL Database enables a subset of dynamic management views to diagnose performance problems, which might be caused by blocked or long-running queries, resource bottlenecks, poor query plans, and so on.</span></span> <span data-ttu-id="63301-105">Этот раздел содержит информацию о том, как выявлять распространенные проблемы производительности с помощью динамических административных представлений.</span><span class="sxs-lookup"><span data-stu-id="63301-105">This topic provides information on how to detect common performance problems by using dynamic management views.</span></span>

<span data-ttu-id="63301-106">База данных SQL частично поддерживает три категории динамических представлений управления:</span><span class="sxs-lookup"><span data-stu-id="63301-106">SQL Database partially supports three categories of dynamic management views:</span></span>

* <span data-ttu-id="63301-107">динамические представления управления, относящиеся к базам данных;</span><span class="sxs-lookup"><span data-stu-id="63301-107">Database-related dynamic management views.</span></span>
* <span data-ttu-id="63301-108">динамические представления управления, относящиеся к выполнению;</span><span class="sxs-lookup"><span data-stu-id="63301-108">Execution-related dynamic management views.</span></span>
* <span data-ttu-id="63301-109">динамические представления управления, относящиеся к транзакциям.</span><span class="sxs-lookup"><span data-stu-id="63301-109">Transaction-related dynamic management views.</span></span>

<span data-ttu-id="63301-110">Подробные сведения о динамических административных представлениях см. в статье [Динамические административные представления и функции (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) электронной документации по SQL Server.</span><span class="sxs-lookup"><span data-stu-id="63301-110">For detailed information on dynamic management views, see [Dynamic Management Views and Functions (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) in SQL Server Books Online.</span></span>

## <a name="permissions"></a><span data-ttu-id="63301-111">Разрешения</span><span class="sxs-lookup"><span data-stu-id="63301-111">Permissions</span></span>
<span data-ttu-id="63301-112">В Базе данных SQL для запроса динамического представления управления требуется наличие разрешений **VIEW DATABASE STATE** .</span><span class="sxs-lookup"><span data-stu-id="63301-112">In SQL Database, querying a dynamic management view requires **VIEW DATABASE STATE** permissions.</span></span> <span data-ttu-id="63301-113">Разрешение **VIEW DATABASE STATE** возвращает сведения обо всех объектах в текущей базе данных.</span><span class="sxs-lookup"><span data-stu-id="63301-113">The **VIEW DATABASE STATE** permission returns information about all objects within the current database.</span></span>
<span data-ttu-id="63301-114">Чтобы предоставить разрешение **VIEW DATABASE STATE** определенному пользователю базы данных, выполните следующий запрос:</span><span class="sxs-lookup"><span data-stu-id="63301-114">To grant the **VIEW DATABASE STATE** permission to a specific database user, run the following query:</span></span>

```GRANT VIEW DATABASE STATE TO database_user; ```

<span data-ttu-id="63301-115">В экземпляре локального сервера SQL Server динамические административные представления возвращают сведения о состоянии сервера.</span><span class="sxs-lookup"><span data-stu-id="63301-115">In an instance of on-premises SQL Server, dynamic management views return server state information.</span></span> <span data-ttu-id="63301-116">В базе данных SQL они возвращают сведения только о текущей логической базе данных.</span><span class="sxs-lookup"><span data-stu-id="63301-116">In SQL Database, they return information regarding your current logical database only.</span></span>

## <a name="calculating-database-size"></a><span data-ttu-id="63301-117">Вычисление размера базы данных</span><span class="sxs-lookup"><span data-stu-id="63301-117">Calculating database size</span></span>
<span data-ttu-id="63301-118">Следующий запрос возвращает размер базы данных в мегабайтах:</span><span class="sxs-lookup"><span data-stu-id="63301-118">The following query returns the size of your database (in megabytes):</span></span>

```
-- Calculates the size of the database.
SELECT SUM(reserved_page_count)*8.0/1024
FROM sys.dm_db_partition_stats;
GO
```

<span data-ttu-id="63301-119">Следующий запрос возвращает размер отдельных объектов базы данных в мегабайтах:</span><span class="sxs-lookup"><span data-stu-id="63301-119">The following query returns the size of individual objects (in megabytes) in your database:</span></span>

```
-- Calculates the size of individual database objects.
SELECT sys.objects.name, SUM(reserved_page_count) * 8.0 / 1024
FROM sys.dm_db_partition_stats, sys.objects
WHERE sys.dm_db_partition_stats.object_id = sys.objects.object_id
GROUP BY sys.objects.name;
GO
```

## <a name="monitoring-connections"></a><span data-ttu-id="63301-120">Мониторинг подключений</span><span class="sxs-lookup"><span data-stu-id="63301-120">Monitoring connections</span></span>
<span data-ttu-id="63301-121">Чтобы получить сведения о подключениях, установленных к определенному серверу базы данных SQL Azure, можно использовать представление [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx).</span><span class="sxs-lookup"><span data-stu-id="63301-121">You can use the [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) view to retrieve information about the connections established to a specific Azure SQL Database server and the details of each connection.</span></span> <span data-ttu-id="63301-122">Кроме того, представление [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) позволяет получить сведения обо всех активных подключениях пользователя и внутренних задачах.</span><span class="sxs-lookup"><span data-stu-id="63301-122">In addition, the [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) view is helpful when retrieving information about all active user connections and internal tasks.</span></span>
<span data-ttu-id="63301-123">Следующий запрос получает информацию о текущем подключении:</span><span class="sxs-lookup"><span data-stu-id="63301-123">The following query retrieves information on the current connection:</span></span>

```
SELECT
    c.session_id, c.net_transport, c.encrypt_option,
    c.auth_scheme, s.host_name, s.program_name,
    s.client_interface_name, s.login_name, s.nt_domain,
    s.nt_user_name, s.original_login_name, c.connect_time,
    s.login_time
FROM sys.dm_exec_connections AS c
JOIN sys.dm_exec_sessions AS s
    ON c.session_id = s.session_id
WHERE c.session_id = @@SPID;
```

> [!NOTE]
> <span data-ttu-id="63301-124">При выполнении представлений **sys.dm_exec_requests** и **sys.dm_exec_sessions views** с разрешением **VIEW DATABASE STATE** для базы данных вы увидите все выполняющиеся сеансы в базе данных. В противном случае вы увидите только текущий сеанс.</span><span class="sxs-lookup"><span data-stu-id="63301-124">When executing the **sys.dm_exec_requests** and **sys.dm_exec_sessions views**, if you have **VIEW DATABASE STATE** permission on the database, you see all executing sessions on the database; otherwise, you see only the current session.</span></span>
> 
> 

## <a name="monitoring-query-performance"></a><span data-ttu-id="63301-125">Мониторинг производительности запросов</span><span class="sxs-lookup"><span data-stu-id="63301-125">Monitoring query performance</span></span>
<span data-ttu-id="63301-126">Медленные или длительные запросы могут потреблять значительные системные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="63301-126">Slow or long running queries can consume significant system resources.</span></span> <span data-ttu-id="63301-127">В этом разделе показано, как использовать динамические представления управления для выявления нескольких распространенных проблем производительности запросов.</span><span class="sxs-lookup"><span data-stu-id="63301-127">This section demonstrates how to use dynamic management views to detect a few common query performance problems.</span></span> <span data-ttu-id="63301-128">Статья [Устранение неполадок производительности в SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) на веб-сайте Microsoft TechNet — не новый, но по-прежнему полезный справочник по устранению неполадок.</span><span class="sxs-lookup"><span data-stu-id="63301-128">An older but still helpful reference for troubleshooting, is the [Troubleshooting Performance Problems in SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) article on Microsoft TechNet.</span></span>

### <a name="finding-top-n-queries"></a><span data-ttu-id="63301-129">Поиск верхних N запросов</span><span class="sxs-lookup"><span data-stu-id="63301-129">Finding top N queries</span></span>
<span data-ttu-id="63301-130">В следующем примере возвращаются сведения о пяти первых запросах, отсортированных по среднему времени ЦП.</span><span class="sxs-lookup"><span data-stu-id="63301-130">The following example returns information about the top five queries ranked by average CPU time.</span></span> <span data-ttu-id="63301-131">В этом примере выполняется сбор запросов по хэшу запроса, то есть логически схожие запросы группируются по общему потреблению ресурсов.</span><span class="sxs-lookup"><span data-stu-id="63301-131">This example aggregates the queries according to their query hash, so that logically equivalent queries are grouped by their cumulative resource consumption.</span></span>

```
SELECT TOP 5 query_stats.query_hash AS "Query Hash",
    SUM(query_stats.total_worker_time) / SUM(query_stats.execution_count) AS "Avg CPU Time",
    MIN(query_stats.statement_text) AS "Statement Text"
FROM
    (SELECT QS.*,
    SUBSTRING(ST.text, (QS.statement_start_offset/2) + 1,
    ((CASE statement_end_offset
        WHEN -1 THEN DATALENGTH(ST.text)
        ELSE QS.statement_end_offset END
            - QS.statement_start_offset)/2) + 1) AS statement_text
     FROM sys.dm_exec_query_stats AS QS
     CROSS APPLY sys.dm_exec_sql_text(QS.sql_handle) as ST) as query_stats
GROUP BY query_stats.query_hash
ORDER BY 2 DESC;
```

### <a name="monitoring-blocked-queries"></a><span data-ttu-id="63301-132">Мониторинг заблокированных запросов</span><span class="sxs-lookup"><span data-stu-id="63301-132">Monitoring blocked queries</span></span>
<span data-ttu-id="63301-133">Медленные или длительные запросы могут вызывать избыточное потребление ресурсов, что приводит к блокировке запросов.</span><span class="sxs-lookup"><span data-stu-id="63301-133">Slow or long-running queries can contribute to excessive resource consumption and be the consequence of blocked queries.</span></span> <span data-ttu-id="63301-134">Причиной блокировки может быть неэффективная структура приложений, неудачные планы запросов, отсутствие полезных индексов и т. д.</span><span class="sxs-lookup"><span data-stu-id="63301-134">The cause of the blocking can be poor application design, bad query plans, the lack of useful indexes, and so on.</span></span> <span data-ttu-id="63301-135">Представление sys.dm_tran_locks можно использовать для получения сведений о текущих блокировках в Базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="63301-135">You can use the sys.dm_tran_locks view to get information about the current locking activity in your Azure SQL Database.</span></span> <span data-ttu-id="63301-136">Пример кода см. в статье [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) в электронной документации по SQL Server.</span><span class="sxs-lookup"><span data-stu-id="63301-136">For example code, see [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) in SQL Server Books Online.</span></span>

### <a name="monitoring-query-plans"></a><span data-ttu-id="63301-137">Мониторинг планов запросов</span><span class="sxs-lookup"><span data-stu-id="63301-137">Monitoring query plans</span></span>
<span data-ttu-id="63301-138">Неэффективный план запросов может повысить потребление ресурсов ЦП.</span><span class="sxs-lookup"><span data-stu-id="63301-138">An inefficient query plan also may increase CPU consumption.</span></span> <span data-ttu-id="63301-139">В следующем примере представление [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) используется, чтобы определить, какой запрос использует наибольшее количество ресурсов ЦП.</span><span class="sxs-lookup"><span data-stu-id="63301-139">The following example uses the [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) view to determine which query uses the most cumulative CPU.</span></span>

```
SELECT
    highest_cpu_queries.plan_handle,
    highest_cpu_queries.total_worker_time,
    q.dbid,
    q.objectid,
    q.number,
    q.encrypted,
    q.[text]
FROM
    (SELECT TOP 50
        qs.plan_handle,
        qs.total_worker_time
    FROM
        sys.dm_exec_query_stats qs
    ORDER BY qs.total_worker_time desc) AS highest_cpu_queries
    CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS q
ORDER BY highest_cpu_queries.total_worker_time DESC;
```

## <a name="see-also"></a><span data-ttu-id="63301-140">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="63301-140">See also</span></span>
[<span data-ttu-id="63301-141">Введение в базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="63301-141">Introduction to SQL Database</span></span>](sql-database-technical-overview.md)

