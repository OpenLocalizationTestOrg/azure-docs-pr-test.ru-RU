---
title: "Azure SQL базы данных с помощью динамических административных представлений aaaMonitoring | Документы Microsoft"
description: "Узнайте, как toodetect и диагностика общих проблем производительности с помощью динамического административного представления toomonitor базы данных SQL Microsoft Azure."
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
ms.openlocfilehash: 43d5fe2dd9a38d031e9334f6ad49fce5866e3bec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-azure-sql-database-using-dynamic-management-views"></a><span data-ttu-id="c8d16-103">Мониторинг базы данных SQL Azure с использованием динамических административных представлений</span><span class="sxs-lookup"><span data-stu-id="c8d16-103">Monitoring Azure SQL Database using dynamic management views</span></span>
<span data-ttu-id="c8d16-104">Базы данных SQL Microsoft Azure включает подмножество динамических административных представлениях, проблем производительности toodiagnose, которые могут вызываться заблокированных или долго выполняющихся запросов, узкие места ресурсов, непродуманного плана запроса и т. д.</span><span class="sxs-lookup"><span data-stu-id="c8d16-104">Microsoft Azure SQL Database enables a subset of dynamic management views toodiagnose performance problems, which might be caused by blocked or long-running queries, resource bottlenecks, poor query plans, and so on.</span></span> <span data-ttu-id="c8d16-105">Этот раздел содержит сведения о том, как toodetect общих проблем производительности с помощью динамических административных представлений.</span><span class="sxs-lookup"><span data-stu-id="c8d16-105">This topic provides information on how toodetect common performance problems by using dynamic management views.</span></span>

<span data-ttu-id="c8d16-106">База данных SQL частично поддерживает три категории динамических представлений управления:</span><span class="sxs-lookup"><span data-stu-id="c8d16-106">SQL Database partially supports three categories of dynamic management views:</span></span>

* <span data-ttu-id="c8d16-107">динамические представления управления, относящиеся к базам данных;</span><span class="sxs-lookup"><span data-stu-id="c8d16-107">Database-related dynamic management views.</span></span>
* <span data-ttu-id="c8d16-108">динамические представления управления, относящиеся к выполнению;</span><span class="sxs-lookup"><span data-stu-id="c8d16-108">Execution-related dynamic management views.</span></span>
* <span data-ttu-id="c8d16-109">динамические представления управления, относящиеся к транзакциям.</span><span class="sxs-lookup"><span data-stu-id="c8d16-109">Transaction-related dynamic management views.</span></span>

<span data-ttu-id="c8d16-110">Подробные сведения о динамических административных представлениях см. в статье [Динамические административные представления и функции (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) электронной документации по SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c8d16-110">For detailed information on dynamic management views, see [Dynamic Management Views and Functions (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) in SQL Server Books Online.</span></span>

## <a name="permissions"></a><span data-ttu-id="c8d16-111">Разрешения</span><span class="sxs-lookup"><span data-stu-id="c8d16-111">Permissions</span></span>
<span data-ttu-id="c8d16-112">В Базе данных SQL для запроса динамического представления управления требуется наличие разрешений **VIEW DATABASE STATE** .</span><span class="sxs-lookup"><span data-stu-id="c8d16-112">In SQL Database, querying a dynamic management view requires **VIEW DATABASE STATE** permissions.</span></span> <span data-ttu-id="c8d16-113">Hello **VIEW DATABASE STATE** разрешение возвращает сведения обо всех объектах в текущей базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="c8d16-113">hello **VIEW DATABASE STATE** permission returns information about all objects within hello current database.</span></span>
<span data-ttu-id="c8d16-114">toogrant hello **VIEW DATABASE STATE** разрешение tooa конкретного пользователя базы данных, запустите приветствия при следующем запросе:</span><span class="sxs-lookup"><span data-stu-id="c8d16-114">toogrant hello **VIEW DATABASE STATE** permission tooa specific database user, run hello following query:</span></span>

```GRANT VIEW DATABASE STATE toodatabase_user; ```

<span data-ttu-id="c8d16-115">В экземпляре локального сервера SQL Server динамические административные представления возвращают сведения о состоянии сервера.</span><span class="sxs-lookup"><span data-stu-id="c8d16-115">In an instance of on-premises SQL Server, dynamic management views return server state information.</span></span> <span data-ttu-id="c8d16-116">В базе данных SQL они возвращают сведения только о текущей логической базе данных.</span><span class="sxs-lookup"><span data-stu-id="c8d16-116">In SQL Database, they return information regarding your current logical database only.</span></span>

## <a name="calculating-database-size"></a><span data-ttu-id="c8d16-117">Вычисление размера базы данных</span><span class="sxs-lookup"><span data-stu-id="c8d16-117">Calculating database size</span></span>
<span data-ttu-id="c8d16-118">Hello следующий запрос возвращает hello размер базы данных (в мегабайтах).</span><span class="sxs-lookup"><span data-stu-id="c8d16-118">hello following query returns hello size of your database (in megabytes):</span></span>

```
-- Calculates hello size of hello database.
SELECT SUM(reserved_page_count)*8.0/1024
FROM sys.dm_db_partition_stats;
GO
```

<span data-ttu-id="c8d16-119">Hello следующий запрос возвращает размер hello отдельные объекты (в мегабайтах) в базе данных.</span><span class="sxs-lookup"><span data-stu-id="c8d16-119">hello following query returns hello size of individual objects (in megabytes) in your database:</span></span>

```
-- Calculates hello size of individual database objects.
SELECT sys.objects.name, SUM(reserved_page_count) * 8.0 / 1024
FROM sys.dm_db_partition_stats, sys.objects
WHERE sys.dm_db_partition_stats.object_id = sys.objects.object_id
GROUP BY sys.objects.name;
GO
```

## <a name="monitoring-connections"></a><span data-ttu-id="c8d16-120">Мониторинг подключений</span><span class="sxs-lookup"><span data-stu-id="c8d16-120">Monitoring connections</span></span>
<span data-ttu-id="c8d16-121">Можно использовать hello [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) просмотра tooretrieve сведений о hello подключений tooa конкретного сервера, базы данных SQL Azure и hello сведений о каждом соединении.</span><span class="sxs-lookup"><span data-stu-id="c8d16-121">You can use hello [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) view tooretrieve information about hello connections established tooa specific Azure SQL Database server and hello details of each connection.</span></span> <span data-ttu-id="c8d16-122">Кроме того, hello [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) это полезно, если получение сведений обо всех активных соединениях пользователей и внутренних задачах.</span><span class="sxs-lookup"><span data-stu-id="c8d16-122">In addition, hello [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) view is helpful when retrieving information about all active user connections and internal tasks.</span></span>
<span data-ttu-id="c8d16-123">Hello следующий запрос возвращает сведения о текущем соединении hello.</span><span class="sxs-lookup"><span data-stu-id="c8d16-123">hello following query retrieves information on hello current connection:</span></span>

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
> <span data-ttu-id="c8d16-124">При выполнении hello **sys.dm_exec_requests** и **представления sys.dm_exec_sessions**, если у вас есть **VIEW DATABASE STATE** разрешений в базе данных hello, вы видите всех выполняющихся сеансы на hello базы данных. в противном случае видеть hello только текущий сеанс.</span><span class="sxs-lookup"><span data-stu-id="c8d16-124">When executing hello **sys.dm_exec_requests** and **sys.dm_exec_sessions views**, if you have **VIEW DATABASE STATE** permission on hello database, you see all executing sessions on hello database; otherwise, you see only hello current session.</span></span>
> 
> 

## <a name="monitoring-query-performance"></a><span data-ttu-id="c8d16-125">Мониторинг производительности запросов</span><span class="sxs-lookup"><span data-stu-id="c8d16-125">Monitoring query performance</span></span>
<span data-ttu-id="c8d16-126">Медленные или длительные запросы могут потреблять значительные системные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="c8d16-126">Slow or long running queries can consume significant system resources.</span></span> <span data-ttu-id="c8d16-127">В этом разделе показано, как toouse динамические представления toodetect несколько общих проблем производительности запросов.</span><span class="sxs-lookup"><span data-stu-id="c8d16-127">This section demonstrates how toouse dynamic management views toodetect a few common query performance problems.</span></span> <span data-ttu-id="c8d16-128">Ссылки на более старые, но по-прежнему полезны для устранения неполадок — hello [Устранение неполадок производительности в SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) статьи в библиотеке Microsoft TechNet.</span><span class="sxs-lookup"><span data-stu-id="c8d16-128">An older but still helpful reference for troubleshooting, is hello [Troubleshooting Performance Problems in SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) article on Microsoft TechNet.</span></span>

### <a name="finding-top-n-queries"></a><span data-ttu-id="c8d16-129">Поиск верхних N запросов</span><span class="sxs-lookup"><span data-stu-id="c8d16-129">Finding top N queries</span></span>
<span data-ttu-id="c8d16-130">Hello следующий пример возвращает сведения о hello первых пяти запросах по среднему времени ЦП.</span><span class="sxs-lookup"><span data-stu-id="c8d16-130">hello following example returns information about hello top five queries ranked by average CPU time.</span></span> <span data-ttu-id="c8d16-131">В этом примере объединяются запросы hello в соответствии с tootheir хэш запроса таким образом, чтобы группировку логически эквивалентных запросов по их совокупному потреблению ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c8d16-131">This example aggregates hello queries according tootheir query hash, so that logically equivalent queries are grouped by their cumulative resource consumption.</span></span>

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

### <a name="monitoring-blocked-queries"></a><span data-ttu-id="c8d16-132">Мониторинг заблокированных запросов</span><span class="sxs-lookup"><span data-stu-id="c8d16-132">Monitoring blocked queries</span></span>
<span data-ttu-id="c8d16-133">Медленное или долго выполняющихся запросов мог добавлять запросы tooexcessive потребления ресурсов и быть следствием hello заблокированных запросов.</span><span class="sxs-lookup"><span data-stu-id="c8d16-133">Slow or long-running queries can contribute tooexcessive resource consumption and be hello consequence of blocked queries.</span></span> <span data-ttu-id="c8d16-134">Причина Hello hello блокировки может быть недостаточно продуманной конструкцией приложения, плохо планы запросов hello не хватает полезных индексов и т. д.</span><span class="sxs-lookup"><span data-stu-id="c8d16-134">hello cause of hello blocking can be poor application design, bad query plans, hello lack of useful indexes, and so on.</span></span> <span data-ttu-id="c8d16-135">Можно использовать tooget hello sys.dm_tran_locks Просмотр сведений об активности текущей блокировки hello в базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c8d16-135">You can use hello sys.dm_tran_locks view tooget information about hello current locking activity in your Azure SQL Database.</span></span> <span data-ttu-id="c8d16-136">Пример кода см. в статье [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) в электронной документации по SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c8d16-136">For example code, see [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) in SQL Server Books Online.</span></span>

### <a name="monitoring-query-plans"></a><span data-ttu-id="c8d16-137">Мониторинг планов запросов</span><span class="sxs-lookup"><span data-stu-id="c8d16-137">Monitoring query plans</span></span>
<span data-ttu-id="c8d16-138">Неэффективный план запросов может повысить потребление ресурсов ЦП.</span><span class="sxs-lookup"><span data-stu-id="c8d16-138">An inefficient query plan also may increase CPU consumption.</span></span> <span data-ttu-id="c8d16-139">Hello следующий пример использует hello [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) просмотра toodetermine, какой запрос использует наибольшее количество ресурсов ЦП hello.</span><span class="sxs-lookup"><span data-stu-id="c8d16-139">hello following example uses hello [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) view toodetermine which query uses hello most cumulative CPU.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="c8d16-140">См. также</span><span class="sxs-lookup"><span data-stu-id="c8d16-140">See also</span></span>
[<span data-ttu-id="c8d16-141">Введение tooSQL базы данных</span><span class="sxs-lookup"><span data-stu-id="c8d16-141">Introduction tooSQL Database</span></span>](sql-database-technical-overview.md)

