---
title: "aaaOverview таблиц в хранилище данных SQL | Документы Microsoft"
description: "Начало работы с таблицами хранилища данных SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 2114d9ad-c113-43da-859f-419d72604bdf
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 06/29/2016
ms.author: shigu;jrj
ms.openlocfilehash: 4edabcb4b0754bf6c99c2b6b3f0c077749051d9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-tables-in-sql-data-warehouse"></a>Общие сведения о таблицах в хранилище данных SQL
> [!div class="op_single_selector"]
> * [Обзор][Overview]
> * [Типы данных][Data Types]
> * [Распределение][Distribute]
> * [Индекс][Index]
> * [Секция][Partition]
> * [Статистика][Statistics]
> * [Временные таблицы][Temporary]
> 
> 

Приступить к созданию таблиц в хранилище данных SQL совсем нетрудно.  Hello basic [CREATE TABLE] [ CREATE TABLE] следующий синтаксис hello общий синтаксис, вы, скорее всего уже имеющиеся в работе с другими базами данных.  toocreate таблицы, необходимо просто tooname таблицы, имен столбцов и определения типов данных для каждого столбца.  При создании таблицы в других базах данных это выглядит знакомо tooyou.

```sql  
CREATE TABLE Customers (FirstName VARCHAR(25), LastName VARCHAR(25))
 ``` 

Привет, приведенном выше примере создается таблица с именем Customers с двумя столбцами, FirstName и LastName.  Каждый столбец определен с типом данных VARCHAR(25), ограничивающей hello данных too25 символов.  Эти атрибуты базовые таблицы, а также другие, являются hello практически такой же, как другие базы данных.  Типы данных определяются для каждого столбца и обеспечения hello целостности данных.  Индексы могут добавляться tooimprove производительность за счет сокращения операций ввода-вывода.  Секционирование можно добавить tooimprove производительности при необходимости toomodify данных.

Команда для [переименования][RENAME] таблицы хранилища данных SQL выглядит следующим образом.

```sql  
RENAME OBJECT Customer tooCustomerOrig; 
 ```

## <a name="distributed-tables"></a>Распределенные таблицы
Новый атрибут фундаментальные представленных распределенных систем, как хранилище данных SQL — hello **столбец распределения**.  столбец распределения Hello — сильно само за себя.  Он является столбцом hello, определяющее, как toodistribute, или деление данных на фоне hello.  При создании таблицы без указания столбец распределения hello hello таблицы автоматически распространяется с помощью **циклический перебор**.  Хотя в некоторых сценариях таблиц, распределенных с использованием метода циклического перебора, может быть достаточно, определение столбцов распределения может значительно уменьшить перемещение данных во время выполнения запросов. Это позволяет оптимизировать производительность.  В ситуациях, когда небольшой объем данных в таблице, выбрав таблицу hello toocreate с hello **реплицировать** тип распределения копирует данные tooeach вычислительный узел и сохраняет движение данных во время выполнения запроса. В разделе [распространение таблицы] [ Distribute] toolearn Дополнительные сведения о том, как tooselect столбец распределения.

## <a name="indexing-and-partitioning-tables"></a>Индексирование и секционирование таблиц
Как вы становятся более сложных в хранилище данных SQL с помощью и производительности toooptimize, будет необходимо toolearn Дополнительные сведения о конструктора таблиц.  toolearn более, статьях hello на [типы данных таблицы][Data Types], [распространение таблицы][Distribute], [индексирования таблицы] [ Index] и [секционировать таблицу][Partition].

## <a name="table-statistics"></a>Статистика таблицы
Статистика, крайне важно toogetting hello повышения производительности хранилища данных SQL.  Поскольку хранилище данных SQL автоматически еще не создавать и обновлять статистику для вас, как может быть tooexpect в базе данных SQL Azure, чтении наши статьи на [статистики] [ Statistics] может быть одним из hello наиболее важные статьи чтения tooensure, вы получаете hello наилучшей производительности из запросов.

## <a name="temporary-tables"></a>Временные таблицы
Временные таблицы — это таблицы, которые только существует hello время входа, недоступных для просмотра другими пользователями.  Временные таблицы можно tooprevent хорошим способом другим пользователям просматривать временных результатов и уменьшить потребность hello очистки.  Так как временные таблицы используют локальное хранилище, некоторые операции выполняются быстрее.  В разделе hello [временной таблицы] [ Temporary] статьи Дополнительные сведения о временных таблицах.

## <a name="external-tables"></a>Внешние таблицы
Внешние таблицы, также известный как Polybase таблицы, являются таблицы, которые могут запрашиваться из хранилища данных SQL, но внешние toodata точки из хранилища данных SQL.  Например созданием внешнюю таблицу какие toofiles точек в хранилище больших двоичных объектов Azure.  Дополнительные сведения о статье toocreate и запроса внешней таблицы, [загрузки данных с помощью Polybase][Load data with Polybase].  

## <a name="unsupported-table-features"></a>Неподдерживаемые функции таблиц
Хранилище данных SQL содержит множество hello и те же возможности таблицы, предоставляемые другими базами данных, существуют некоторые возможности, которые не поддерживаются.  Ниже приведен список некоторых hello возможности таблиц, которые не поддерживаются.

| Неподдерживаемые функции |
| --- |
| Первичный ключ, внешние ключи, [ограничения таблицы][Table Constraints] |
| [Уникальные индексы][Unique Indexes] |
| [Вычисляемые столбцы][Computed Columns] |
| [Разреженные столбцы][Sparse Columns] |
| [Пользовательские типы][User-Defined Types] |
| [Последовательность][Sequence] |
| [Триггеры][Triggers] |
| [Индексированные представления][Indexed Views] |
| [Синонимы][Synonyms] |

## <a name="table-size-queries"></a>Запросы размера таблицы
Один простой способ tooidentify пространства и строки, используемые таблицы в каждом распределений hello 60 — toouse [DBCC PDW_SHOWSPACEUSED][DBCC PDW_SHOWSPACEUSED].

```sql
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

Однако возможности команд DBCC достаточно ограничены.  Динамические административные представления (DMV) позволит вам toosee гораздо более подробно, а также гораздо больший контроль над hello результаты запроса.  Начните с создания это представление, в котором будет находиться ссылка tooby многих примерах в этом и других статьях.

```sql
CREATE VIEW dbo.vTableSizes
AS
WITH base
AS
(
SELECT 
 GETDATE()                                                             AS  [execution_time]
, DB_NAME()                                                            AS  [database_name]
, s.name                                                               AS  [schema_name]
, t.name                                                               AS  [table_name]
, QUOTENAME(s.name)+'.'+QUOTENAME(t.name)                              AS  [two_part_name]
, nt.[name]                                                            AS  [node_table_name]
, ROW_NUMBER() OVER(PARTITION BY nt.[name] ORDER BY (SELECT NULL))     AS  [node_table_name_seq]
, tp.[distribution_policy_desc]                                        AS  [distribution_policy_name]
, c.[name]                                                             AS  [distribution_column]
, nt.[distribution_id]                                                 AS  [distribution_id]
, i.[type]                                                             AS  [index_type]
, i.[type_desc]                                                        AS  [index_type_desc]
, nt.[pdw_node_id]                                                     AS  [pdw_node_id]
, pn.[type]                                                            AS  [pdw_node_type]
, pn.[name]                                                            AS  [pdw_node_name]
, di.name                                                              AS  [dist_name]
, di.position                                                          AS  [dist_position]
, nps.[partition_number]                                               AS  [partition_nmbr]
, nps.[reserved_page_count]                                            AS  [reserved_space_page_count]
, nps.[reserved_page_count] - nps.[used_page_count]                    AS  [unused_space_page_count]
, nps.[in_row_data_page_count] 
    + nps.[row_overflow_used_page_count] 
    + nps.[lob_used_page_count]                                        AS  [data_space_page_count]
, nps.[reserved_page_count] 
 - (nps.[reserved_page_count] - nps.[used_page_count]) 
 - ([in_row_data_page_count] 
         + [row_overflow_used_page_count]+[lob_used_page_count])       AS  [index_space_page_count]
, nps.[row_count]                                                      AS  [row_count]
from 
    sys.schemas s
INNER JOIN sys.tables t
    ON s.[schema_id] = t.[schema_id]
INNER JOIN sys.indexes i
    ON  t.[object_id] = i.[object_id]
    AND i.[index_id] <= 1
INNER JOIN sys.pdw_table_distribution_properties tp
    ON t.[object_id] = tp.[object_id]
INNER JOIN sys.pdw_table_mappings tm
    ON t.[object_id] = tm.[object_id]
INNER JOIN sys.pdw_nodes_tables nt
    ON tm.[physical_name] = nt.[name]
INNER JOIN sys.dm_pdw_nodes pn
    ON  nt.[pdw_node_id] = pn.[pdw_node_id]
INNER JOIN sys.pdw_distributions di
    ON  nt.[distribution_id] = di.[distribution_id]
INNER JOIN sys.dm_pdw_nodes_db_partition_stats nps
    ON nt.[object_id] = nps.[object_id]
    AND nt.[pdw_node_id] = nps.[pdw_node_id]
    AND nt.[distribution_id] = nps.[distribution_id]
LEFT OUTER JOIN (select * from sys.pdw_column_distribution_properties where distribution_ordinal = 1) cdp
    ON t.[object_id] = cdp.[object_id]
LEFT OUTER JOIN sys.columns c
    ON cdp.[object_id] = c.[object_id]
    AND cdp.[column_id] = c.[column_id]
)
, size
AS
(
SELECT
   [execution_time]
,  [database_name]
,  [schema_name]
,  [table_name]
,  [two_part_name]
,  [node_table_name]
,  [node_table_name_seq]
,  [distribution_policy_name]
,  [distribution_column]
,  [distribution_id]
,  [index_type]
,  [index_type_desc]
,  [pdw_node_id]
,  [pdw_node_type]
,  [pdw_node_name]
,  [dist_name]
,  [dist_position]
,  [partition_nmbr]
,  [reserved_space_page_count]
,  [unused_space_page_count]
,  [data_space_page_count]
,  [index_space_page_count]
,  [row_count]
,  ([reserved_space_page_count] * 8.0)                                 AS [reserved_space_KB]
,  ([reserved_space_page_count] * 8.0)/1000                            AS [reserved_space_MB]
,  ([reserved_space_page_count] * 8.0)/1000000                         AS [reserved_space_GB]
,  ([reserved_space_page_count] * 8.0)/1000000000                      AS [reserved_space_TB]
,  ([unused_space_page_count]   * 8.0)                                 AS [unused_space_KB]
,  ([unused_space_page_count]   * 8.0)/1000                            AS [unused_space_MB]
,  ([unused_space_page_count]   * 8.0)/1000000                         AS [unused_space_GB]
,  ([unused_space_page_count]   * 8.0)/1000000000                      AS [unused_space_TB]
,  ([data_space_page_count]     * 8.0)                                 AS [data_space_KB]
,  ([data_space_page_count]     * 8.0)/1000                            AS [data_space_MB]
,  ([data_space_page_count]     * 8.0)/1000000                         AS [data_space_GB]
,  ([data_space_page_count]     * 8.0)/1000000000                      AS [data_space_TB]
,  ([index_space_page_count]  * 8.0)                                   AS [index_space_KB]
,  ([index_space_page_count]  * 8.0)/1000                              AS [index_space_MB]
,  ([index_space_page_count]  * 8.0)/1000000                           AS [index_space_GB]
,  ([index_space_page_count]  * 8.0)/1000000000                        AS [index_space_TB]
FROM base
)
SELECT * 
FROM size
;
```

### <a name="table-space-summary"></a>Сводка табличного пространства
Этот запрос возвращает строки hello и места по таблице.  Это отличный запроса toosee, какие таблицы — наибольшее таблиц и являются ли они циклического перебора, реплицированных или распределенных хэш.  Для распределенных хэш-таблицы также показаны столбец распределения hello.  В большинстве случаев наибольшая таблица должна иметь хэш-распределение и кластеризованный индекс columnstore.

```sql
SELECT 
     database_name
,    schema_name
,    table_name
,    distribution_policy_name
,      distribution_column
,    index_type_desc
,    COUNT(distinct partition_nmbr) as nbr_partitions
,    SUM(row_count)                 as table_row_count
,    SUM(reserved_space_GB)         as table_reserved_space_GB
,    SUM(data_space_GB)             as table_data_space_GB
,    SUM(index_space_GB)            as table_index_space_GB
,    SUM(unused_space_GB)           as table_unused_space_GB
FROM 
    dbo.vTableSizes
GROUP BY 
     database_name
,    schema_name
,    table_name
,    distribution_policy_name
,      distribution_column
,    index_type_desc
ORDER BY
    table_reserved_space_GB desc
;
```

### <a name="table-space-by-distribution-type"></a>Табличное пространство по типу распределения
```sql
SELECT 
     distribution_policy_name
,    SUM(row_count)                as table_type_row_count
,    SUM(reserved_space_GB)        as table_type_reserved_space_GB
,    SUM(data_space_GB)            as table_type_data_space_GB
,    SUM(index_space_GB)           as table_type_index_space_GB
,    SUM(unused_space_GB)          as table_type_unused_space_GB
FROM dbo.vTableSizes
GROUP BY distribution_policy_name
;
```

### <a name="table-space-by-index-type"></a>Табличное пространство по типу индекса
```sql
SELECT 
     index_type_desc
,    SUM(row_count)                as table_type_row_count
,    SUM(reserved_space_GB)        as table_type_reserved_space_GB
,    SUM(data_space_GB)            as table_type_data_space_GB
,    SUM(index_space_GB)           as table_type_index_space_GB
,    SUM(unused_space_GB)          as table_type_unused_space_GB
FROM dbo.vTableSizes
GROUP BY index_type_desc
;
```

### <a name="distribution-space-summary"></a>Сводка пространства распределения
```sql
SELECT 
    distribution_id
,    SUM(row_count)                as total_node_distribution_row_count
,    SUM(reserved_space_MB)        as total_node_distribution_reserved_space_MB
,    SUM(data_space_MB)            as total_node_distribution_data_space_MB
,    SUM(index_space_MB)           as total_node_distribution_index_space_MB
,    SUM(unused_space_MB)          as total_node_distribution_unused_space_MB
FROM dbo.vTableSizes
GROUP BY     distribution_id
ORDER BY    distribution_id
;
```

## <a name="next-steps"></a>Дальнейшие действия
toolearn более, статьях hello на [типы данных таблицы][Data Types], [распространение таблицы][Distribute], [индексирования таблицы] [ Index], [Секционировать таблицу][Partition], [статистики таблицы] [ Statistics] и [ Временные таблицы][Temporary].  Дополнительные рекомендации см. в статье [Рекомендации по использованию хранилища данных SQL Azure][SQL Data Warehouse Best Practices].

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md
[Load data with Polybase]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md

<!--MSDN references-->
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[RENAME]: https://msdn.microsoft.com/library/mt631611.aspx
[DBCC PDW_SHOWSPACEUSED]: https://msdn.microsoft.com/library/mt204028.aspx
[Table Constraints]: https://msdn.microsoft.com/library/ms188066.aspx
[Computed Columns]: https://msdn.microsoft.com/library/ms186241.aspx
[Sparse Columns]: https://msdn.microsoft.com/library/cc280604.aspx
[User-Defined Types]: https://msdn.microsoft.com/library/ms131694.aspx
[Sequence]: https://msdn.microsoft.com/library/ff878091.aspx
[Triggers]: https://msdn.microsoft.com/library/ms189799.aspx
[Indexed Views]: https://msdn.microsoft.com/library/ms191432.aspx
[Synonyms]: https://msdn.microsoft.com/library/ms177544.aspx
[Unique Indexes]: https://msdn.microsoft.com/library/ms188783.aspx

<!--Other Web references-->
