---
title: "aaaMonitor рабочей нагрузки с помощью динамических административных представлений | Документы Microsoft"
description: "Узнайте, как toomonitor рабочей нагрузки с помощью динамических административных представлений."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 69ecd479-0941-48df-b3d0-cf54c79e6549
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: acccf952d165ccec3de3b4b1c633b18bbbf78077
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-workload-using-dmvs"></a><span data-ttu-id="a3796-103">Мониторинг рабочей нагрузки с помощью динамических административных представлений</span><span class="sxs-lookup"><span data-stu-id="a3796-103">Monitor your workload using DMVs</span></span>
<span data-ttu-id="a3796-104">В этой статье описывается как динамические административные представления (DMV) toomonitor toouse рабочей нагрузки и изучить выполнение запросов в хранилище данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a3796-104">This article describes how toouse Dynamic Management Views (DMVs) toomonitor your workload and investigate query execution in Azure SQL Data Warehouse.</span></span>

## <a name="permissions"></a><span data-ttu-id="a3796-105">Разрешения</span><span class="sxs-lookup"><span data-stu-id="a3796-105">Permissions</span></span>
<span data-ttu-id="a3796-106">hello tooquery динамических административных представлений в этой статье, необходимо разрешение VIEW DATABASE STATE или элемента УПРАВЛЕНИЯ.</span><span class="sxs-lookup"><span data-stu-id="a3796-106">tooquery hello DMVs in this article, you need either VIEW DATABASE STATE or CONTROL permission.</span></span> <span data-ttu-id="a3796-107">Обычно предоставляется право VIEW DATABASE STATE не hello предпочитаемый разрешение, поскольку она является значительно более ограниченным.</span><span class="sxs-lookup"><span data-stu-id="a3796-107">Usually granting VIEW DATABASE STATE is hello preferred permission as it is much more restrictive.</span></span>

```sql
GRANT VIEW DATABASE STATE toomyuser;
```

## <a name="monitor-connections"></a><span data-ttu-id="a3796-108">Мониторинг подключений</span><span class="sxs-lookup"><span data-stu-id="a3796-108">Monitor connections</span></span>
<span data-ttu-id="a3796-109">Все имена входа tooSQL хранилище данных регистрируются слишком[sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].</span><span class="sxs-lookup"><span data-stu-id="a3796-109">All logins tooSQL Data Warehouse are logged too[sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].</span></span>  <span data-ttu-id="a3796-110">Это динамическое административное Представление содержит hello последние 10 000 имена входа.</span><span class="sxs-lookup"><span data-stu-id="a3796-110">This DMV contains hello last 10,000 logins.</span></span>  <span data-ttu-id="a3796-111">Hello session_id — первичный ключ hello, назначенное последовательно для каждого нового сеанса входа.</span><span class="sxs-lookup"><span data-stu-id="a3796-111">hello session_id is hello primary key and is assigned sequentially for each new logon.</span></span>

```sql
-- Other Active Connections
SELECT * FROM sys.dm_pdw_exec_sessions where status <> 'Closed' and session_id <> session_id();
```

## <a name="monitor-query-execution"></a><span data-ttu-id="a3796-112">Наблюдение за выполнением запросов</span><span class="sxs-lookup"><span data-stu-id="a3796-112">Monitor query execution</span></span>
<span data-ttu-id="a3796-113">Все запросы, выполняемые в хранилище данных SQL регистрируются слишком[sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].</span><span class="sxs-lookup"><span data-stu-id="a3796-113">All queries executed on SQL Data Warehouse are logged too[sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].</span></span>  <span data-ttu-id="a3796-114">Это динамическое административное Представление содержит hello последние 10 000 запросов, которые выполняются.</span><span class="sxs-lookup"><span data-stu-id="a3796-114">This DMV contains hello last 10,000 queries executed.</span></span>  <span data-ttu-id="a3796-115">идентификатор_запроса Hello уникальным образом идентифицирует каждый запрос и hello первичный ключ для данного динамического административного Представления.</span><span class="sxs-lookup"><span data-stu-id="a3796-115">hello request_id uniquely identifies each query and is hello primary key for this DMV.</span></span>  <span data-ttu-id="a3796-116">идентификатор_запроса Hello назначается последовательно для каждой новой и префиксом QID, предназначенную для ИД запроса.</span><span class="sxs-lookup"><span data-stu-id="a3796-116">hello request_id is assigned sequentially for each new query and is prefixed with QID, which stands for query ID.</span></span>  <span data-ttu-id="a3796-117">При запросе конкретного session_id из этого динамического административного представления будут показаны все запросы для данной операции входа.</span><span class="sxs-lookup"><span data-stu-id="a3796-117">Querying this DMV for a given session_id shows all queries for a given logon.</span></span>

> [!NOTE]
> <span data-ttu-id="a3796-118">Хранимые процедуры используют несколько идентификаторов request_id.</span><span class="sxs-lookup"><span data-stu-id="a3796-118">Stored procedures use multiple Request IDs.</span></span>  <span data-ttu-id="a3796-119">Идентификатора запросов назначаются последовательно.</span><span class="sxs-lookup"><span data-stu-id="a3796-119">Request IDs are assigned in sequential order.</span></span> 
> 
> 

<span data-ttu-id="a3796-120">Ниже приведены планы выполнения запросов tooinvestigate toofollow действия и время для конкретного запроса.</span><span class="sxs-lookup"><span data-stu-id="a3796-120">Here are steps toofollow tooinvestigate query execution plans and times for a particular query.</span></span>

### <a name="step-1-identify-hello-query-you-wish-tooinvestigate"></a><span data-ttu-id="a3796-121">Шаг 1: Определение hello запросов, которые вы будете tooinvestigate</span><span class="sxs-lookup"><span data-stu-id="a3796-121">STEP 1: Identify hello query you wish tooinvestigate</span></span>
```sql
-- Monitor active queries
SELECT * 
FROM sys.dm_pdw_exec_requests 
WHERE status not in ('Completed','Failed','Cancelled')
  AND session_id <> session_id()
ORDER BY submit_time DESC;

-- Find top 10 queries longest running queries
SELECT TOP 10 * 
FROM sys.dm_pdw_exec_requests 
ORDER BY total_elapsed_time DESC;

-- Find a query with hello Label 'My Query'
-- Use brackets when querying hello label column, as it it a key word
SELECT  *
FROM    sys.dm_pdw_exec_requests
WHERE   [label] = 'My Query';
```

<span data-ttu-id="a3796-122">Из hello предыдущих результатов запроса **Примечание hello ИД запроса** запроса hello, желательно tooinvestigate.</span><span class="sxs-lookup"><span data-stu-id="a3796-122">From hello preceding query results, **note hello Request ID** of hello query that you would like tooinvestigate.</span></span>

<span data-ttu-id="a3796-123">Запросы в hello **Suspended** состояние ставятся из-за пределов tooconcurrency.</span><span class="sxs-lookup"><span data-stu-id="a3796-123">Queries in hello **Suspended** state are being queued due tooconcurrency limits.</span></span> <span data-ttu-id="a3796-124">Эти запросы появляются также в hello sys.dm_pdw_waits ожиданий запросов с типом UserConcurrencyResourceType.</span><span class="sxs-lookup"><span data-stu-id="a3796-124">These queries also appear in hello sys.dm_pdw_waits waits query with a type of UserConcurrencyResourceType.</span></span> <span data-ttu-id="a3796-125">Дополнительные сведения об ограничениях параллелизма см. в разделе [Управление параллелизмом и рабочей нагрузкой в хранилище данных SQL][Concurrency and workload management].</span><span class="sxs-lookup"><span data-stu-id="a3796-125">See [Concurrency and workload management][Concurrency and workload management] for more details on concurrency limits.</span></span> <span data-ttu-id="a3796-126">Запросы также могут быть отложены по другим причинам, в том числе из-за блокировки объектов.</span><span class="sxs-lookup"><span data-stu-id="a3796-126">Queries can also wait for other reasons such as for object locks.</span></span>  <span data-ttu-id="a3796-127">Если запрос ожидает ресурс, ознакомьтесь с разделом [Исследование запросов, ожидающих ресурсы][Investigating queries waiting for resources] далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="a3796-127">If your query is waiting for a resource, see [Investigating queries waiting for resources][Investigating queries waiting for resources] further down in this article.</span></span>

<span data-ttu-id="a3796-128">Уточняющий запрос hello toosimplify запроса в таблице sys.dm_pdw_exec_requests hello, используйте [МЕТКА] [ LABEL] tooassign tooyour запрос комментарий, который можно найти в представлении sys.dm_pdw_exec_requests hello.</span><span class="sxs-lookup"><span data-stu-id="a3796-128">toosimplify hello lookup of a query in hello sys.dm_pdw_exec_requests table, use [LABEL][LABEL] tooassign a comment tooyour query that can be looked up in hello sys.dm_pdw_exec_requests view.</span></span>

```sql
-- Query with Label
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query')
;
```

### <a name="step-2-investigate-hello-query-plan"></a><span data-ttu-id="a3796-129">Шаг 2: Проверьте план запроса hello</span><span class="sxs-lookup"><span data-stu-id="a3796-129">STEP 2: Investigate hello query plan</span></span>
<span data-ttu-id="a3796-130">Использовать план распределенных SQL (DSQL) tooretrieve hello hello ИД запроса запроса из [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].</span><span class="sxs-lookup"><span data-stu-id="a3796-130">Use hello Request ID tooretrieve hello query's distributed SQL (DSQL) plan from [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].</span></span>

```sql
-- Find hello distributed query plan steps for a specific query.
-- Replace request_id with value from Step 1.

SELECT * FROM sys.dm_pdw_request_steps
WHERE request_id = 'QID####'
ORDER BY step_index;
```

<span data-ttu-id="a3796-131">Если план DSQL занимает больше времени, чем ожидалось, hello может быть вызвано сложным план с многих DSQL действия или только один этап, слишком долго.</span><span class="sxs-lookup"><span data-stu-id="a3796-131">When a DSQL plan is taking longer than expected, hello cause can be a complex plan with many DSQL steps or just one step taking a long time.</span></span>  <span data-ttu-id="a3796-132">Если план hello множество действий с несколькими операциями перемещения, рассмотрите возможность оптимизации вашей перемещение данных tooreduce распределения таблицы.</span><span class="sxs-lookup"><span data-stu-id="a3796-132">If hello plan is many steps with several move operations, consider optimizing your table distributions tooreduce data movement.</span></span> <span data-ttu-id="a3796-133">Hello [распределение таблиц] [ Table distribution] статье объясняется, почему данные должны быть перемещены toosolve запроса и описание некоторых перемещения данных toominimize стратегии распространения.</span><span class="sxs-lookup"><span data-stu-id="a3796-133">hello [Table distribution][Table distribution] article explains why data must be moved toosolve a query and explains some distribution strategies toominimize data movement.</span></span>

<span data-ttu-id="a3796-134">tooinvestigate Дополнительные сведения об одном шаге hello *operation_type* столбец hello продолжительный запрос шаг и Примечание hello **индекс**:</span><span class="sxs-lookup"><span data-stu-id="a3796-134">tooinvestigate further details about a single step, hello *operation_type* column of hello long-running query step and note hello **Step Index**:</span></span>

* <span data-ttu-id="a3796-135">Перейдите к шагу 3а для **операций SQL**: OnOperation, RemoteOperation, ReturnOperation.</span><span class="sxs-lookup"><span data-stu-id="a3796-135">Proceed with Step 3a for **SQL operations**: OnOperation, RemoteOperation, ReturnOperation.</span></span>
* <span data-ttu-id="a3796-136">Перейдите к шагу 3б для **операций перемещения данных**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.</span><span class="sxs-lookup"><span data-stu-id="a3796-136">Proceed with Step 3b for **Data Movement operations**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.</span></span>

### <a name="step-3a-investigate-sql-on-hello-distributed-databases"></a><span data-ttu-id="a3796-137">ШАГ 3a: исследовать hello распределенных баз данных SQL</span><span class="sxs-lookup"><span data-stu-id="a3796-137">STEP 3a: Investigate SQL on hello distributed databases</span></span>
<span data-ttu-id="a3796-138">Используйте hello ИД запроса и hello индекс tooretrieve сведений из [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], который содержит сведения о выполнении шага hello запроса на всех hello распределенных баз данных.</span><span class="sxs-lookup"><span data-stu-id="a3796-138">Use hello Request ID and hello Step Index tooretrieve details from [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], which contains execution information of hello query step on all of hello distributed databases.</span></span>

```sql
-- Find hello distribution run times for a SQL step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_sql_requests
WHERE request_id = 'QID####' AND step_index = 2;
```

<span data-ttu-id="a3796-139">При выполнении действия запроса hello, [: DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN] может быть используется tooretrieve hello SQL Server предполагаемый план из кэша планов SQL Server для выполнения на определенной шага hello hello распределение.</span><span class="sxs-lookup"><span data-stu-id="a3796-139">When hello query step is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used tooretrieve hello SQL Server estimated plan from hello SQL Server plan cache for hello step running on a particular distribution.</span></span>

```sql
-- Find hello SQL Server execution plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(1, 78);
```

### <a name="step-3b-investigate-data-movement-on-hello-distributed-databases"></a><span data-ttu-id="a3796-140">ШАГ 3b: исследовать перемещения данных hello распределенных баз данных</span><span class="sxs-lookup"><span data-stu-id="a3796-140">STEP 3b: Investigate data movement on hello distributed databases</span></span>
<span data-ttu-id="a3796-141">Используйте hello ИД запроса и hello индекс tooretrieve сведения о шаг перемещения данных, работающих на каждого распределения из [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].</span><span class="sxs-lookup"><span data-stu-id="a3796-141">Use hello Request ID and hello Step Index tooretrieve information about a data movement step running on each distribution from [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].</span></span>

```sql
-- Find hello information about all hello workers completing a Data Movement Step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_dms_workers
WHERE request_id = 'QID####' AND step_index = 2;
```

* <span data-ttu-id="a3796-142">Проверьте hello *total_elapsed_time* toosee столбца, если частичным распределением занимает больше времени, чем другие для перемещения данных.</span><span class="sxs-lookup"><span data-stu-id="a3796-142">Check hello *total_elapsed_time* column toosee if a particular distribution is taking significantly longer than others for data movement.</span></span>
* <span data-ttu-id="a3796-143">Для распространения hello длительное время, проверьте hello *rows_processed* toosee столбца, если число строк, перемещается из этого распространения hello значительно больше, чем другие.</span><span class="sxs-lookup"><span data-stu-id="a3796-143">For hello long-running distribution, check hello *rows_processed* column toosee if hello number of rows being moved from that distribution is significantly larger than others.</span></span> <span data-ttu-id="a3796-144">Если это так, то это может означать отклонение базовых данных.</span><span class="sxs-lookup"><span data-stu-id="a3796-144">If so, this may indicate skew of your underlying data.</span></span>

<span data-ttu-id="a3796-145">Если выполняется запрос hello, [: DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN] может быть используется tooretrieve hello SQL Server предполагаемый план из кэша планов SQL Server для hello, запущенных в течение определенного шага SQL hello распределение.</span><span class="sxs-lookup"><span data-stu-id="a3796-145">If hello query is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used tooretrieve hello SQL Server estimated plan from hello SQL Server plan cache for hello currently running SQL Step within a particular distribution.</span></span>

```sql
-- Find hello SQL Server estimated plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(55, 238);
```

<a name="waiting"></a>

## <a name="monitor-waiting-queries"></a><span data-ttu-id="a3796-146">Наблюдение за ожидающими запросами</span><span class="sxs-lookup"><span data-stu-id="a3796-146">Monitor waiting queries</span></span>
<span data-ttu-id="a3796-147">Если вы обнаружили, что запрос не выполняется, так как он ожидает ресурс, вот запрос, отображающий все ресурсы hello Ожидание запроса.</span><span class="sxs-lookup"><span data-stu-id="a3796-147">If you discover that your query is not making progress because it is waiting for a resource, here is a query that shows all hello resources a query is waiting for.</span></span>

```sql
-- Find queries 
-- Replace request_id with value from Step 1.

SELECT waits.session_id,
      waits.request_id,  
      requests.command,
      requests.status,
      requests.start_time,  
      waits.type,
      waits.state,
      waits.object_type,
      waits.object_name
FROM   sys.dm_pdw_waits waits
   JOIN  sys.dm_pdw_exec_requests requests
   ON waits.request_id=requests.request_id
WHERE waits.request_id = 'QID####'
ORDER BY waits.object_name, waits.object_type, waits.state;
```

<span data-ttu-id="a3796-148">Если активно hello запрос ожидает ресурсы из другой запрос, то будет иметь состояние hello **AcquireResources**.</span><span class="sxs-lookup"><span data-stu-id="a3796-148">If hello query is actively waiting on resources from another query, then hello state will be **AcquireResources**.</span></span>  <span data-ttu-id="a3796-149">Если запрос hello имеет все необходимые hello ресурсы, то будет иметь состояние hello **Granted**.</span><span class="sxs-lookup"><span data-stu-id="a3796-149">If hello query has all hello required resources, then hello state will be **Granted**.</span></span>

## <a name="monitor-tempdb"></a><span data-ttu-id="a3796-150">Мониторинг tempdb</span><span class="sxs-lookup"><span data-stu-id="a3796-150">Monitor tempdb</span></span>
<span data-ttu-id="a3796-151">Использование высокого уровня базы данных tempdb может быть hello основную причину проблем с нехваткой памяти и снижению производительности.</span><span class="sxs-lookup"><span data-stu-id="a3796-151">High tempdb utilization can be hello root cause for slow performance and out of memory issues.</span></span> <span data-ttu-id="a3796-152">Проверьте Если rowgroups наклона или снижению качества данных и предпринять соответствующие действия hello сначала.</span><span class="sxs-lookup"><span data-stu-id="a3796-152">Please first check if you have data skew or poor quality rowgroups and take hello appropriate actions.</span></span> <span data-ttu-id="a3796-153">Вы можете рассмотреть масштабирование хранилища данных, если во время выполнения запроса наблюдается приближение к пределам базы данных tempdb.</span><span class="sxs-lookup"><span data-stu-id="a3796-153">Consider scaling your data warehouse if you find tempdb reaching its limits during query execution.</span></span> <span data-ttu-id="a3796-154">Hello ниже приводится способ использования базы данных tempdb tooidentify каждого запроса на каждом узле.</span><span class="sxs-lookup"><span data-stu-id="a3796-154">hello following describes how tooidentify tempdb usage per query on each node.</span></span> 

<span data-ttu-id="a3796-155">Создайте код представления tooassociate hello соответствующий узел подписки для sys.dm_pdw_sql_requests hello.</span><span class="sxs-lookup"><span data-stu-id="a3796-155">Create hello following view tooassociate hello appropriate node id for sys.dm_pdw_sql_requests.</span></span> <span data-ttu-id="a3796-156">Это включает вы tooleverage других к серверу динамических административных представлений и объедините эти таблицы с sys.dm_pdw_sql_requests.</span><span class="sxs-lookup"><span data-stu-id="a3796-156">This will enable you tooleverage other pass-through DMVs and join those tables with sys.dm_pdw_sql_requests.</span></span>

```sql
-- sys.dm_pdw_sql_requests with hello correct node id
CREATE VIEW sql_requests AS
(SELECT
       sr.request_id,
       sr.step_index,
       (CASE 
              WHEN (sr.distribution_id = -1 ) THEN 
              (SELECT pdw_node_id FROM sys.dm_pdw_nodes WHERE type = 'CONTROL') 
              ELSE d.pdw_node_id END) AS pdw_node_id,
       sr.distribution_id,
       sr.status,
       sr.error_id,
       sr.start_time,
       sr.end_time,
       sr.total_elapsed_time,
       sr.row_count,
       sr.spid,
       sr.command
FROM sys.pdw_distributions AS d
RIGHT JOIN sys.dm_pdw_sql_requests AS sr ON d.distribution_id = sr.distribution_id)
```
<span data-ttu-id="a3796-157">Выполните следующий запрос toomonitor tempdb hello.</span><span class="sxs-lookup"><span data-stu-id="a3796-157">Run hello following query toomonitor tempdb:</span></span>

```sql
-- Monitor tempdb
SELECT
    sr.request_id,
    ssu.session_id,
    ssu.pdw_node_id,
    sr.command,
    sr.total_elapsed_time,
    es.login_name AS 'LoginName',
    DB_NAME(ssu.database_id) AS 'DatabaseName',
    (es.memory_usage * 8) AS 'MemoryUsage (in KB)',
    (ssu.user_objects_alloc_page_count * 8) AS 'Space Allocated For User Objects (in KB)',
    (ssu.user_objects_dealloc_page_count * 8) AS 'Space Deallocated For User Objects (in KB)',
    (ssu.internal_objects_alloc_page_count * 8) AS 'Space Allocated For Internal Objects (in KB)',
    (ssu.internal_objects_dealloc_page_count * 8) AS 'Space Deallocated For Internal Objects (in KB)',
    CASE es.is_user_process
    WHEN 1 THEN 'User Session'
    WHEN 0 THEN 'System Session'
    END AS 'SessionType',
    es.row_count AS 'RowCount'
FROM sys.dm_pdw_nodes_db_session_space_usage AS ssu
    INNER JOIN sys.dm_pdw_nodes_exec_sessions AS es ON ssu.session_id = es.session_id AND ssu.pdw_node_id = es.pdw_node_id
    INNER JOIN sys.dm_pdw_nodes_exec_connections AS er ON ssu.session_id = er.session_id AND ssu.pdw_node_id = er.pdw_node_id
    INNER JOIN sql_requests AS sr ON ssu.session_id = sr.spid AND ssu.pdw_node_id = sr.pdw_node_id
WHERE DB_NAME(ssu.database_id) = 'tempdb'
    AND es.session_id <> @@SPID
    AND es.login_name <> 'sa' 
ORDER BY sr.request_id;
```
## <a name="monitor-memory"></a><span data-ttu-id="a3796-158">Мониторинг памяти</span><span class="sxs-lookup"><span data-stu-id="a3796-158">Monitor memory</span></span>

<span data-ttu-id="a3796-159">Память может быть hello основную причину проблем с нехваткой памяти и снижению производительности.</span><span class="sxs-lookup"><span data-stu-id="a3796-159">Memory can be hello root cause for slow performance and out of memory issues.</span></span> <span data-ttu-id="a3796-160">Проверьте Если rowgroups наклона или снижению качества данных и предпринять соответствующие действия hello сначала.</span><span class="sxs-lookup"><span data-stu-id="a3796-160">Please first check if you have data skew or poor quality rowgroups and take hello appropriate actions.</span></span> <span data-ttu-id="a3796-161">Вы можете рассмотреть масштабирование хранилища данных, если во время выполнения запроса наблюдается активное использование памяти SQL Server (приближение к пределам).</span><span class="sxs-lookup"><span data-stu-id="a3796-161">Consider scaling your data warehouse if you find SQL Server memory usage reaching its limits during query execution.</span></span>

<span data-ttu-id="a3796-162">Привет, в следующем запросе возвращает нехватка памяти SQL Server использование и памяти на каждом узле:</span><span class="sxs-lookup"><span data-stu-id="a3796-162">hello following query returns SQL Server memory usage and memory pressure per node:</span></span> 
```sql
-- Memory consumption
SELECT
  pc1.cntr_value as Curr_Mem_KB, 
  pc1.cntr_value/1024.0 as Curr_Mem_MB,
  (pc1.cntr_value/1048576.0) as Curr_Mem_GB,
  pc2.cntr_value as Max_Mem_KB,
  pc2.cntr_value/1024.0 as Max_Mem_MB,
  (pc2.cntr_value/1048576.0) as Max_Mem_GB,
  pc1.cntr_value * 100.0/pc2.cntr_value AS Memory_Utilization_Percentage,
  pc1.pdw_node_id
FROM
-- pc1: current memory
sys.dm_pdw_nodes_os_performance_counters AS pc1
-- pc2: total memory allowed for this SQL instance
JOIN sys.dm_pdw_nodes_os_performance_counters AS pc2 
ON pc1.object_name = pc2.object_name AND pc1.pdw_node_id = pc2.pdw_node_id
WHERE
pc1.counter_name = 'Total Server Memory (KB)'
AND pc2.counter_name = 'Target Server Memory (KB)'
```
## <a name="monitor-transaction-log-size"></a><span data-ttu-id="a3796-163">Мониторинг размера журнала транзакций</span><span class="sxs-lookup"><span data-stu-id="a3796-163">Monitor transaction log size</span></span>
<span data-ttu-id="a3796-164">Hello следующий запрос возвращает размер журнала транзакций hello на каждого распределения.</span><span class="sxs-lookup"><span data-stu-id="a3796-164">hello following query returns hello transaction log size on each distribution.</span></span> <span data-ttu-id="a3796-165">Проверьте, если rowgroups наклона или снижению качества данных и предпринять соответствующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="a3796-165">Please check if you have data skew or poor quality rowgroups and take hello appropriate actions.</span></span> <span data-ttu-id="a3796-166">Если один из файлов журнала hello почти 160 ГБ, следует рассмотреть вертикальное масштабирование экземпляра или ограничение на размер транзакции.</span><span class="sxs-lookup"><span data-stu-id="a3796-166">If one of hello log files is reaching 160GB, you should consider scaling up your instance or limiting your transaction size.</span></span> 
```sql
-- Transaction log size
SELECT
  instance_name as distribution_db,
  cntr_value*1.0/1048576 as log_file_size_used_GB,
  pdw_node_id 
FROM sys.dm_pdw_nodes_os_performance_counters 
WHERE 
instance_name like 'Distribution_%' 
AND counter_name = 'Log File(s) Used Size (KB)'
AND counter_name = 'Target Server Memory (KB)'
```
## <a name="monitor-transaction-log-rollback"></a><span data-ttu-id="a3796-167">Мониторинг отката журнала транзакций</span><span class="sxs-lookup"><span data-stu-id="a3796-167">Monitor transaction log rollback</span></span>
<span data-ttu-id="a3796-168">Если не удается установить запросы или подсчета tooproceed много времени, можно проверить и мониторинга, если у вас есть все транзакции, откат.</span><span class="sxs-lookup"><span data-stu-id="a3796-168">If your queries are failing or taking a long time tooproceed, you can check and monitor if you have any transactions rolling back.</span></span>
```sql
-- Monitor rollback
SELECT 
    SUM(CASE WHEN t.database_transaction_next_undo_lsn IS NOT NULL THEN 1 ELSE 0 END),
    t.pdw_node_id,
    nod.[type]
FROM sys.dm_pdw_nodes_tran_database_transactions t
JOIN sys.dm_pdw_nodes nod ON t.pdw_node_id = nod.pdw_node_id
GROUP BY t.pdw_node_id, nod.[type]
```

## <a name="next-steps"></a><span data-ttu-id="a3796-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a3796-169">Next steps</span></span>
<span data-ttu-id="a3796-170">Дополнительные сведения о динамических административных представлениях см. в разделе [Системные представления][System views].</span><span class="sxs-lookup"><span data-stu-id="a3796-170">See [System views][System views] for more information on DMVs.</span></span>
<span data-ttu-id="a3796-171">Дополнительные рекомендации см. в статье [Рекомендации по использованию хранилища данных SQL][SQL Data Warehouse best practices].</span><span class="sxs-lookup"><span data-stu-id="a3796-171">See [SQL Data Warehouse best practices][SQL Data Warehouse best practices] for more information about best practices</span></span>

<!--Image references-->

<!--Article references-->
[Manage overview]: ./sql-data-warehouse-overview-manage.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[System views]: ./sql-data-warehouse-reference-tsql-system-views.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Concurrency and workload management]: ./sql-data-warehouse-develop-concurrency.md
[Investigating queries waiting for resources]: ./sql-data-warehouse-manage-monitor.md#waiting

<!--MSDN references-->
[sys.dm_pdw_dms_workers]: http://msdn.microsoft.com/library/mt203878.aspx
[sys.dm_pdw_exec_requests]: http://msdn.microsoft.com/library/mt203887.aspx
[sys.dm_pdw_exec_sessions]: http://msdn.microsoft.com/library/mt203883.aspx
[sys.dm_pdw_request_steps]: http://msdn.microsoft.com/library/mt203913.aspx
[sys.dm_pdw_sql_requests]: http://msdn.microsoft.com/library/mt203889.aspx
[DBCC PDW_SHOWEXECUTIONPLAN]: http://msdn.microsoft.com/library/mt204017.aspx
[DBCC PDW_SHOWSPACEUSED]: http://msdn.microsoft.com/library/mt204028.aspx
[LABEL]: https://msdn.microsoft.com/library/ms190322.aspx
