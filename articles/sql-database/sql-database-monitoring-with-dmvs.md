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
# <a name="monitoring-azure-sql-database-using-dynamic-management-views"></a>Мониторинг базы данных SQL Azure с использованием динамических административных представлений
Базы данных SQL Microsoft Azure включает подмножество динамических административных представлениях, проблем производительности toodiagnose, которые могут вызываться заблокированных или долго выполняющихся запросов, узкие места ресурсов, непродуманного плана запроса и т. д. Этот раздел содержит сведения о том, как toodetect общих проблем производительности с помощью динамических административных представлений.

База данных SQL частично поддерживает три категории динамических представлений управления:

* динамические представления управления, относящиеся к базам данных;
* динамические представления управления, относящиеся к выполнению;
* динамические представления управления, относящиеся к транзакциям.

Подробные сведения о динамических административных представлениях см. в статье [Динамические административные представления и функции (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) электронной документации по SQL Server.

## <a name="permissions"></a>Разрешения
В Базе данных SQL для запроса динамического представления управления требуется наличие разрешений **VIEW DATABASE STATE** . Hello **VIEW DATABASE STATE** разрешение возвращает сведения обо всех объектах в текущей базе данных hello.
toogrant hello **VIEW DATABASE STATE** разрешение tooa конкретного пользователя базы данных, запустите приветствия при следующем запросе:

```GRANT VIEW DATABASE STATE toodatabase_user; ```

В экземпляре локального сервера SQL Server динамические административные представления возвращают сведения о состоянии сервера. В базе данных SQL они возвращают сведения только о текущей логической базе данных.

## <a name="calculating-database-size"></a>Вычисление размера базы данных
Hello следующий запрос возвращает hello размер базы данных (в мегабайтах).

```
-- Calculates hello size of hello database.
SELECT SUM(reserved_page_count)*8.0/1024
FROM sys.dm_db_partition_stats;
GO
```

Hello следующий запрос возвращает размер hello отдельные объекты (в мегабайтах) в базе данных.

```
-- Calculates hello size of individual database objects.
SELECT sys.objects.name, SUM(reserved_page_count) * 8.0 / 1024
FROM sys.dm_db_partition_stats, sys.objects
WHERE sys.dm_db_partition_stats.object_id = sys.objects.object_id
GROUP BY sys.objects.name;
GO
```

## <a name="monitoring-connections"></a>Мониторинг подключений
Можно использовать hello [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) просмотра tooretrieve сведений о hello подключений tooa конкретного сервера, базы данных SQL Azure и hello сведений о каждом соединении. Кроме того, hello [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) это полезно, если получение сведений обо всех активных соединениях пользователей и внутренних задачах.
Hello следующий запрос возвращает сведения о текущем соединении hello.

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
> При выполнении hello **sys.dm_exec_requests** и **представления sys.dm_exec_sessions**, если у вас есть **VIEW DATABASE STATE** разрешений в базе данных hello, вы видите всех выполняющихся сеансы на hello базы данных. в противном случае видеть hello только текущий сеанс.
> 
> 

## <a name="monitoring-query-performance"></a>Мониторинг производительности запросов
Медленные или длительные запросы могут потреблять значительные системные ресурсы. В этом разделе показано, как toouse динамические представления toodetect несколько общих проблем производительности запросов. Ссылки на более старые, но по-прежнему полезны для устранения неполадок — hello [Устранение неполадок производительности в SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) статьи в библиотеке Microsoft TechNet.

### <a name="finding-top-n-queries"></a>Поиск верхних N запросов
Hello следующий пример возвращает сведения о hello первых пяти запросах по среднему времени ЦП. В этом примере объединяются запросы hello в соответствии с tootheir хэш запроса таким образом, чтобы группировку логически эквивалентных запросов по их совокупному потреблению ресурсов.

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

### <a name="monitoring-blocked-queries"></a>Мониторинг заблокированных запросов
Медленное или долго выполняющихся запросов мог добавлять запросы tooexcessive потребления ресурсов и быть следствием hello заблокированных запросов. Причина Hello hello блокировки может быть недостаточно продуманной конструкцией приложения, плохо планы запросов hello не хватает полезных индексов и т. д. Можно использовать tooget hello sys.dm_tran_locks Просмотр сведений об активности текущей блокировки hello в базе данных SQL Azure. Пример кода см. в статье [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) в электронной документации по SQL Server.

### <a name="monitoring-query-plans"></a>Мониторинг планов запросов
Неэффективный план запросов может повысить потребление ресурсов ЦП. Hello следующий пример использует hello [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) просмотра toodetermine, какой запрос использует наибольшее количество ресурсов ЦП hello.

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

## <a name="see-also"></a>См. также
[Введение tooSQL базы данных](sql-database-technical-overview.md)

