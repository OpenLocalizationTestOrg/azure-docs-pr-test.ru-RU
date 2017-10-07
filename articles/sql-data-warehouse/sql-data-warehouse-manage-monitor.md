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
# <a name="monitor-your-workload-using-dmvs"></a>Мониторинг рабочей нагрузки с помощью динамических административных представлений
В этой статье описывается как динамические административные представления (DMV) toomonitor toouse рабочей нагрузки и изучить выполнение запросов в хранилище данных SQL Azure.

## <a name="permissions"></a>Разрешения
hello tooquery динамических административных представлений в этой статье, необходимо разрешение VIEW DATABASE STATE или элемента УПРАВЛЕНИЯ. Обычно предоставляется право VIEW DATABASE STATE не hello предпочитаемый разрешение, поскольку она является значительно более ограниченным.

```sql
GRANT VIEW DATABASE STATE toomyuser;
```

## <a name="monitor-connections"></a>Мониторинг подключений
Все имена входа tooSQL хранилище данных регистрируются слишком[sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].  Это динамическое административное Представление содержит hello последние 10 000 имена входа.  Hello session_id — первичный ключ hello, назначенное последовательно для каждого нового сеанса входа.

```sql
-- Other Active Connections
SELECT * FROM sys.dm_pdw_exec_sessions where status <> 'Closed' and session_id <> session_id();
```

## <a name="monitor-query-execution"></a>Наблюдение за выполнением запросов
Все запросы, выполняемые в хранилище данных SQL регистрируются слишком[sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].  Это динамическое административное Представление содержит hello последние 10 000 запросов, которые выполняются.  идентификатор_запроса Hello уникальным образом идентифицирует каждый запрос и hello первичный ключ для данного динамического административного Представления.  идентификатор_запроса Hello назначается последовательно для каждой новой и префиксом QID, предназначенную для ИД запроса.  При запросе конкретного session_id из этого динамического административного представления будут показаны все запросы для данной операции входа.

> [!NOTE]
> Хранимые процедуры используют несколько идентификаторов request_id.  Идентификатора запросов назначаются последовательно. 
> 
> 

Ниже приведены планы выполнения запросов tooinvestigate toofollow действия и время для конкретного запроса.

### <a name="step-1-identify-hello-query-you-wish-tooinvestigate"></a>Шаг 1: Определение hello запросов, которые вы будете tooinvestigate
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

Из hello предыдущих результатов запроса **Примечание hello ИД запроса** запроса hello, желательно tooinvestigate.

Запросы в hello **Suspended** состояние ставятся из-за пределов tooconcurrency. Эти запросы появляются также в hello sys.dm_pdw_waits ожиданий запросов с типом UserConcurrencyResourceType. Дополнительные сведения об ограничениях параллелизма см. в разделе [Управление параллелизмом и рабочей нагрузкой в хранилище данных SQL][Concurrency and workload management]. Запросы также могут быть отложены по другим причинам, в том числе из-за блокировки объектов.  Если запрос ожидает ресурс, ознакомьтесь с разделом [Исследование запросов, ожидающих ресурсы][Investigating queries waiting for resources] далее в этой статье.

Уточняющий запрос hello toosimplify запроса в таблице sys.dm_pdw_exec_requests hello, используйте [МЕТКА] [ LABEL] tooassign tooyour запрос комментарий, который можно найти в представлении sys.dm_pdw_exec_requests hello.

```sql
-- Query with Label
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query')
;
```

### <a name="step-2-investigate-hello-query-plan"></a>Шаг 2: Проверьте план запроса hello
Использовать план распределенных SQL (DSQL) tooretrieve hello hello ИД запроса запроса из [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].

```sql
-- Find hello distributed query plan steps for a specific query.
-- Replace request_id with value from Step 1.

SELECT * FROM sys.dm_pdw_request_steps
WHERE request_id = 'QID####'
ORDER BY step_index;
```

Если план DSQL занимает больше времени, чем ожидалось, hello может быть вызвано сложным план с многих DSQL действия или только один этап, слишком долго.  Если план hello множество действий с несколькими операциями перемещения, рассмотрите возможность оптимизации вашей перемещение данных tooreduce распределения таблицы. Hello [распределение таблиц] [ Table distribution] статье объясняется, почему данные должны быть перемещены toosolve запроса и описание некоторых перемещения данных toominimize стратегии распространения.

tooinvestigate Дополнительные сведения об одном шаге hello *operation_type* столбец hello продолжительный запрос шаг и Примечание hello **индекс**:

* Перейдите к шагу 3а для **операций SQL**: OnOperation, RemoteOperation, ReturnOperation.
* Перейдите к шагу 3б для **операций перемещения данных**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.

### <a name="step-3a-investigate-sql-on-hello-distributed-databases"></a>ШАГ 3a: исследовать hello распределенных баз данных SQL
Используйте hello ИД запроса и hello индекс tooretrieve сведений из [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], который содержит сведения о выполнении шага hello запроса на всех hello распределенных баз данных.

```sql
-- Find hello distribution run times for a SQL step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_sql_requests
WHERE request_id = 'QID####' AND step_index = 2;
```

При выполнении действия запроса hello, [: DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN] может быть используется tooretrieve hello SQL Server предполагаемый план из кэша планов SQL Server для выполнения на определенной шага hello hello распределение.

```sql
-- Find hello SQL Server execution plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(1, 78);
```

### <a name="step-3b-investigate-data-movement-on-hello-distributed-databases"></a>ШАГ 3b: исследовать перемещения данных hello распределенных баз данных
Используйте hello ИД запроса и hello индекс tooretrieve сведения о шаг перемещения данных, работающих на каждого распределения из [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].

```sql
-- Find hello information about all hello workers completing a Data Movement Step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_dms_workers
WHERE request_id = 'QID####' AND step_index = 2;
```

* Проверьте hello *total_elapsed_time* toosee столбца, если частичным распределением занимает больше времени, чем другие для перемещения данных.
* Для распространения hello длительное время, проверьте hello *rows_processed* toosee столбца, если число строк, перемещается из этого распространения hello значительно больше, чем другие. Если это так, то это может означать отклонение базовых данных.

Если выполняется запрос hello, [: DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN] может быть используется tooretrieve hello SQL Server предполагаемый план из кэша планов SQL Server для hello, запущенных в течение определенного шага SQL hello распределение.

```sql
-- Find hello SQL Server estimated plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(55, 238);
```

<a name="waiting"></a>

## <a name="monitor-waiting-queries"></a>Наблюдение за ожидающими запросами
Если вы обнаружили, что запрос не выполняется, так как он ожидает ресурс, вот запрос, отображающий все ресурсы hello Ожидание запроса.

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

Если активно hello запрос ожидает ресурсы из другой запрос, то будет иметь состояние hello **AcquireResources**.  Если запрос hello имеет все необходимые hello ресурсы, то будет иметь состояние hello **Granted**.

## <a name="monitor-tempdb"></a>Мониторинг tempdb
Использование высокого уровня базы данных tempdb может быть hello основную причину проблем с нехваткой памяти и снижению производительности. Проверьте Если rowgroups наклона или снижению качества данных и предпринять соответствующие действия hello сначала. Вы можете рассмотреть масштабирование хранилища данных, если во время выполнения запроса наблюдается приближение к пределам базы данных tempdb. Hello ниже приводится способ использования базы данных tempdb tooidentify каждого запроса на каждом узле. 

Создайте код представления tooassociate hello соответствующий узел подписки для sys.dm_pdw_sql_requests hello. Это включает вы tooleverage других к серверу динамических административных представлений и объедините эти таблицы с sys.dm_pdw_sql_requests.

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
Выполните следующий запрос toomonitor tempdb hello.

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
## <a name="monitor-memory"></a>Мониторинг памяти

Память может быть hello основную причину проблем с нехваткой памяти и снижению производительности. Проверьте Если rowgroups наклона или снижению качества данных и предпринять соответствующие действия hello сначала. Вы можете рассмотреть масштабирование хранилища данных, если во время выполнения запроса наблюдается активное использование памяти SQL Server (приближение к пределам).

Привет, в следующем запросе возвращает нехватка памяти SQL Server использование и памяти на каждом узле: 
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
## <a name="monitor-transaction-log-size"></a>Мониторинг размера журнала транзакций
Hello следующий запрос возвращает размер журнала транзакций hello на каждого распределения. Проверьте, если rowgroups наклона или снижению качества данных и предпринять соответствующие действия hello. Если один из файлов журнала hello почти 160 ГБ, следует рассмотреть вертикальное масштабирование экземпляра или ограничение на размер транзакции. 
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
## <a name="monitor-transaction-log-rollback"></a>Мониторинг отката журнала транзакций
Если не удается установить запросы или подсчета tooproceed много времени, можно проверить и мониторинга, если у вас есть все транзакции, откат.
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

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о динамических административных представлениях см. в разделе [Системные представления][System views].
Дополнительные рекомендации см. в статье [Рекомендации по использованию хранилища данных SQL][SQL Data Warehouse best practices].

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
