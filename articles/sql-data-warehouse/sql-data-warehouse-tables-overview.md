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
# <a name="overview-of-tables-in-sql-data-warehouse"></a><span data-ttu-id="47420-103">Общие сведения о таблицах в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="47420-103">Overview of tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="47420-104">[Обзор][Overview]</span><span class="sxs-lookup"><span data-stu-id="47420-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="47420-105">[Типы данных][Data Types]</span><span class="sxs-lookup"><span data-stu-id="47420-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="47420-106">[Распределение][Distribute]</span><span class="sxs-lookup"><span data-stu-id="47420-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="47420-107">[Индекс][Index]</span><span class="sxs-lookup"><span data-stu-id="47420-107">[Index][Index]</span></span>
> * <span data-ttu-id="47420-108">[Секция][Partition]</span><span class="sxs-lookup"><span data-stu-id="47420-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="47420-109">[Статистика][Statistics]</span><span class="sxs-lookup"><span data-stu-id="47420-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="47420-110">[Временные таблицы][Temporary]</span><span class="sxs-lookup"><span data-stu-id="47420-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="47420-111">Приступить к созданию таблиц в хранилище данных SQL совсем нетрудно.</span><span class="sxs-lookup"><span data-stu-id="47420-111">Getting started with creating tables in SQL Data Warehouse is simple.</span></span>  <span data-ttu-id="47420-112">Hello basic [CREATE TABLE] [ CREATE TABLE] следующий синтаксис hello общий синтаксис, вы, скорее всего уже имеющиеся в работе с другими базами данных.</span><span class="sxs-lookup"><span data-stu-id="47420-112">hello basic [CREATE TABLE][CREATE TABLE] syntax follows hello common syntax you are most likely already familiar with from working with other databases.</span></span>  <span data-ttu-id="47420-113">toocreate таблицы, необходимо просто tooname таблицы, имен столбцов и определения типов данных для каждого столбца.</span><span class="sxs-lookup"><span data-stu-id="47420-113">toocreate a table, you simply need tooname your table, name your columns and define data types for each column.</span></span>  <span data-ttu-id="47420-114">При создании таблицы в других базах данных это выглядит знакомо tooyou.</span><span class="sxs-lookup"><span data-stu-id="47420-114">If you've create tables in other databases, this should look very familiar tooyou.</span></span>

```sql  
CREATE TABLE Customers (FirstName VARCHAR(25), LastName VARCHAR(25))
 ``` 

<span data-ttu-id="47420-115">Привет, приведенном выше примере создается таблица с именем Customers с двумя столбцами, FirstName и LastName.</span><span class="sxs-lookup"><span data-stu-id="47420-115">hello above example creates a table named Customers with two columns, FirstName and LastName.</span></span>  <span data-ttu-id="47420-116">Каждый столбец определен с типом данных VARCHAR(25), ограничивающей hello данных too25 символов.</span><span class="sxs-lookup"><span data-stu-id="47420-116">Each column is defined with a data type of VARCHAR(25), which limits hello data too25 characters.</span></span>  <span data-ttu-id="47420-117">Эти атрибуты базовые таблицы, а также другие, являются hello практически такой же, как другие базы данных.</span><span class="sxs-lookup"><span data-stu-id="47420-117">These fundamental attributes of a table, as well as others, are mostly hello same as other databases.</span></span>  <span data-ttu-id="47420-118">Типы данных определяются для каждого столбца и обеспечения hello целостности данных.</span><span class="sxs-lookup"><span data-stu-id="47420-118">Data types are defined for each column and ensure hello integrity of your data.</span></span>  <span data-ttu-id="47420-119">Индексы могут добавляться tooimprove производительность за счет сокращения операций ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="47420-119">Indexes can be added tooimprove performance by reducing I/O.</span></span>  <span data-ttu-id="47420-120">Секционирование можно добавить tooimprove производительности при необходимости toomodify данных.</span><span class="sxs-lookup"><span data-stu-id="47420-120">Partitioning can be added tooimprove performance when you need toomodify data.</span></span>

<span data-ttu-id="47420-121">Команда для [переименования][RENAME] таблицы хранилища данных SQL выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="47420-121">[Renaming][RENAME] a SQL Data Warehouse table looks like this:</span></span>

```sql  
RENAME OBJECT Customer tooCustomerOrig; 
 ```

## <a name="distributed-tables"></a><span data-ttu-id="47420-122">Распределенные таблицы</span><span class="sxs-lookup"><span data-stu-id="47420-122">Distributed tables</span></span>
<span data-ttu-id="47420-123">Новый атрибут фундаментальные представленных распределенных систем, как хранилище данных SQL — hello **столбец распределения**.</span><span class="sxs-lookup"><span data-stu-id="47420-123">A new fundamental attribute introduced by distributed systems like SQL Data Warehouse is hello **distribution column**.</span></span>  <span data-ttu-id="47420-124">столбец распределения Hello — сильно само за себя.</span><span class="sxs-lookup"><span data-stu-id="47420-124">hello distribution column is very much what it sounds like.</span></span>  <span data-ttu-id="47420-125">Он является столбцом hello, определяющее, как toodistribute, или деление данных на фоне hello.</span><span class="sxs-lookup"><span data-stu-id="47420-125">It is hello column that determines how toodistribute, or divide, your data behind hello scenes.</span></span>  <span data-ttu-id="47420-126">При создании таблицы без указания столбец распределения hello hello таблицы автоматически распространяется с помощью **циклический перебор**.</span><span class="sxs-lookup"><span data-stu-id="47420-126">When you create a table without specifying hello distribution column, hello table is automatically distributed using **round robin**.</span></span>  <span data-ttu-id="47420-127">Хотя в некоторых сценариях таблиц, распределенных с использованием метода циклического перебора, может быть достаточно, определение столбцов распределения может значительно уменьшить перемещение данных во время выполнения запросов. Это позволяет оптимизировать производительность.</span><span class="sxs-lookup"><span data-stu-id="47420-127">While round robin tables can be sufficient in some scenarios, defining distribution columns can greatly reduce data movement during queries, thus optimizing performance.</span></span>  <span data-ttu-id="47420-128">В ситуациях, когда небольшой объем данных в таблице, выбрав таблицу hello toocreate с hello **реплицировать** тип распределения копирует данные tooeach вычислительный узел и сохраняет движение данных во время выполнения запроса.</span><span class="sxs-lookup"><span data-stu-id="47420-128">In situations where there is a small amount of data in a table, choosing toocreate hello table with hello **replicate** distribution type copies data tooeach compute node and saves data movement at query execution time.</span></span> <span data-ttu-id="47420-129">В разделе [распространение таблицы] [ Distribute] toolearn Дополнительные сведения о том, как tooselect столбец распределения.</span><span class="sxs-lookup"><span data-stu-id="47420-129">See [Distributing a Table][Distribute] toolearn more about how tooselect a distribution column.</span></span>

## <a name="indexing-and-partitioning-tables"></a><span data-ttu-id="47420-130">Индексирование и секционирование таблиц</span><span class="sxs-lookup"><span data-stu-id="47420-130">Indexing and partitioning tables</span></span>
<span data-ttu-id="47420-131">Как вы становятся более сложных в хранилище данных SQL с помощью и производительности toooptimize, будет необходимо toolearn Дополнительные сведения о конструктора таблиц.</span><span class="sxs-lookup"><span data-stu-id="47420-131">As you become more advanced in using SQL Data Warehouse and want toooptimize performance, you'll want toolearn more about Table Design.</span></span>  <span data-ttu-id="47420-132">toolearn более, статьях hello на [типы данных таблицы][Data Types], [распространение таблицы][Distribute], [индексирования таблицы] [ Index] и [секционировать таблицу][Partition].</span><span class="sxs-lookup"><span data-stu-id="47420-132">toolearn more, see hello articles on [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index] and  [Partitioning a Table][Partition].</span></span>

## <a name="table-statistics"></a><span data-ttu-id="47420-133">Статистика таблицы</span><span class="sxs-lookup"><span data-stu-id="47420-133">Table statistics</span></span>
<span data-ttu-id="47420-134">Статистика, крайне важно toogetting hello повышения производительности хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="47420-134">Statistics are an extremely important toogetting hello best performance out of your SQL Data Warehouse.</span></span>  <span data-ttu-id="47420-135">Поскольку хранилище данных SQL автоматически еще не создавать и обновлять статистику для вас, как может быть tooexpect в базе данных SQL Azure, чтении наши статьи на [статистики] [ Statistics] может быть одним из hello наиболее важные статьи чтения tooensure, вы получаете hello наилучшей производительности из запросов.</span><span class="sxs-lookup"><span data-stu-id="47420-135">Since SQL Data Warehouse does not yet automatically create and update statistics for you, like you may have come tooexpect in Azure SQL Database, reading our article on [Statistics][Statistics] might be one of hello most important articles you read tooensure that you get hello best performance from your queries.</span></span>

## <a name="temporary-tables"></a><span data-ttu-id="47420-136">Временные таблицы</span><span class="sxs-lookup"><span data-stu-id="47420-136">Temporary tables</span></span>
<span data-ttu-id="47420-137">Временные таблицы — это таблицы, которые только существует hello время входа, недоступных для просмотра другими пользователями.</span><span class="sxs-lookup"><span data-stu-id="47420-137">Temporary tables are tables which only exist for hello duration of your logon and cannot be seen by other users.</span></span>  <span data-ttu-id="47420-138">Временные таблицы можно tooprevent хорошим способом другим пользователям просматривать временных результатов и уменьшить потребность hello очистки.</span><span class="sxs-lookup"><span data-stu-id="47420-138">Temporary tables can be a good way tooprevent others from seeing temporary results and also reduce hello need for cleanup.</span></span>  <span data-ttu-id="47420-139">Так как временные таблицы используют локальное хранилище, некоторые операции выполняются быстрее.</span><span class="sxs-lookup"><span data-stu-id="47420-139">Since temporary tables also utilize local storage, they can offer faster performance for some operations.</span></span>  <span data-ttu-id="47420-140">В разделе hello [временной таблицы] [ Temporary] статьи Дополнительные сведения о временных таблицах.</span><span class="sxs-lookup"><span data-stu-id="47420-140">See hello [Temporary Table][Temporary] articles for more details about temporary tables.</span></span>

## <a name="external-tables"></a><span data-ttu-id="47420-141">Внешние таблицы</span><span class="sxs-lookup"><span data-stu-id="47420-141">External tables</span></span>
<span data-ttu-id="47420-142">Внешние таблицы, также известный как Polybase таблицы, являются таблицы, которые могут запрашиваться из хранилища данных SQL, но внешние toodata точки из хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="47420-142">External tables, also known as Polybase tables, are tables which can be queried from SQL Data Warehouse, but point toodata external from SQL Data Warehouse.</span></span>  <span data-ttu-id="47420-143">Например созданием внешнюю таблицу какие toofiles точек в хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="47420-143">For example, you can create an external table which points toofiles on Azure Blob Storage.</span></span>  <span data-ttu-id="47420-144">Дополнительные сведения о статье toocreate и запроса внешней таблицы, [загрузки данных с помощью Polybase][Load data with Polybase].</span><span class="sxs-lookup"><span data-stu-id="47420-144">For more details on how toocreate and query an external table, see [Load data with Polybase][Load data with Polybase].</span></span>  

## <a name="unsupported-table-features"></a><span data-ttu-id="47420-145">Неподдерживаемые функции таблиц</span><span class="sxs-lookup"><span data-stu-id="47420-145">Unsupported table features</span></span>
<span data-ttu-id="47420-146">Хранилище данных SQL содержит множество hello и те же возможности таблицы, предоставляемые другими базами данных, существуют некоторые возможности, которые не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="47420-146">While SQL Data Warehouse contains many of hello same table features offered by other databases, there are some features which are not yet supported.</span></span>  <span data-ttu-id="47420-147">Ниже приведен список некоторых hello возможности таблиц, которые не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="47420-147">Below is a list of some of hello table features which are not yet supported.</span></span>

| <span data-ttu-id="47420-148">Неподдерживаемые функции</span><span class="sxs-lookup"><span data-stu-id="47420-148">Unsupported features</span></span> |
| --- |
| <span data-ttu-id="47420-149">Первичный ключ, внешние ключи, [ограничения таблицы][Table Constraints]</span><span class="sxs-lookup"><span data-stu-id="47420-149">Primary key, Foreign keys, Unique and Check [Table Constraints][Table Constraints]</span></span> |
| <span data-ttu-id="47420-150">[Уникальные индексы][Unique Indexes]</span><span class="sxs-lookup"><span data-stu-id="47420-150">[Unique Indexes][Unique Indexes]</span></span> |
| <span data-ttu-id="47420-151">[Вычисляемые столбцы][Computed Columns]</span><span class="sxs-lookup"><span data-stu-id="47420-151">[Computed Columns][Computed Columns]</span></span> |
| <span data-ttu-id="47420-152">[Разреженные столбцы][Sparse Columns]</span><span class="sxs-lookup"><span data-stu-id="47420-152">[Sparse Columns][Sparse Columns]</span></span> |
| <span data-ttu-id="47420-153">[Пользовательские типы][User-Defined Types]</span><span class="sxs-lookup"><span data-stu-id="47420-153">[User-Defined Types][User-Defined Types]</span></span> |
| <span data-ttu-id="47420-154">[Последовательность][Sequence]</span><span class="sxs-lookup"><span data-stu-id="47420-154">[Sequence][Sequence]</span></span> |
| <span data-ttu-id="47420-155">[Триггеры][Triggers]</span><span class="sxs-lookup"><span data-stu-id="47420-155">[Triggers][Triggers]</span></span> |
| <span data-ttu-id="47420-156">[Индексированные представления][Indexed Views]</span><span class="sxs-lookup"><span data-stu-id="47420-156">[Indexed Views][Indexed Views]</span></span> |
| <span data-ttu-id="47420-157">[Синонимы][Synonyms]</span><span class="sxs-lookup"><span data-stu-id="47420-157">[Synonyms][Synonyms]</span></span> |

## <a name="table-size-queries"></a><span data-ttu-id="47420-158">Запросы размера таблицы</span><span class="sxs-lookup"><span data-stu-id="47420-158">Table size queries</span></span>
<span data-ttu-id="47420-159">Один простой способ tooidentify пространства и строки, используемые таблицы в каждом распределений hello 60 — toouse [DBCC PDW_SHOWSPACEUSED][DBCC PDW_SHOWSPACEUSED].</span><span class="sxs-lookup"><span data-stu-id="47420-159">One simple way tooidentify space and rows consumed by a table in each of hello 60 distributions, is toouse [DBCC PDW_SHOWSPACEUSED][DBCC PDW_SHOWSPACEUSED].</span></span>

```sql
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

<span data-ttu-id="47420-160">Однако возможности команд DBCC достаточно ограничены.</span><span class="sxs-lookup"><span data-stu-id="47420-160">However, using DBCC commands can be quite limiting.</span></span>  <span data-ttu-id="47420-161">Динамические административные представления (DMV) позволит вам toosee гораздо более подробно, а также гораздо больший контроль над hello результаты запроса.</span><span class="sxs-lookup"><span data-stu-id="47420-161">Dynamic management views (DMVs) will allow you toosee much more detail as well as give you much greater control over hello query results.</span></span>  <span data-ttu-id="47420-162">Начните с создания это представление, в котором будет находиться ссылка tooby многих примерах в этом и других статьях.</span><span class="sxs-lookup"><span data-stu-id="47420-162">Start by creating this view, which will be referred tooby many of our examples in this and other articles.</span></span>

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

### <a name="table-space-summary"></a><span data-ttu-id="47420-163">Сводка табличного пространства</span><span class="sxs-lookup"><span data-stu-id="47420-163">Table space summary</span></span>
<span data-ttu-id="47420-164">Этот запрос возвращает строки hello и места по таблице.</span><span class="sxs-lookup"><span data-stu-id="47420-164">This query returns hello rows and space by table.</span></span>  <span data-ttu-id="47420-165">Это отличный запроса toosee, какие таблицы — наибольшее таблиц и являются ли они циклического перебора, реплицированных или распределенных хэш.</span><span class="sxs-lookup"><span data-stu-id="47420-165">It is a great query toosee which tables are your largest tables and whether they are round robin, replicated or hash distributed.</span></span>  <span data-ttu-id="47420-166">Для распределенных хэш-таблицы также показаны столбец распределения hello.</span><span class="sxs-lookup"><span data-stu-id="47420-166">For hash distributed tables it also shows hello distribution column.</span></span>  <span data-ttu-id="47420-167">В большинстве случаев наибольшая таблица должна иметь хэш-распределение и кластеризованный индекс columnstore.</span><span class="sxs-lookup"><span data-stu-id="47420-167">In most cases your largest tables should be hash distributed with a clustered columnstore index.</span></span>

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

### <a name="table-space-by-distribution-type"></a><span data-ttu-id="47420-168">Табличное пространство по типу распределения</span><span class="sxs-lookup"><span data-stu-id="47420-168">Table space by distribution type</span></span>
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

### <a name="table-space-by-index-type"></a><span data-ttu-id="47420-169">Табличное пространство по типу индекса</span><span class="sxs-lookup"><span data-stu-id="47420-169">Table space by index type</span></span>
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

### <a name="distribution-space-summary"></a><span data-ttu-id="47420-170">Сводка пространства распределения</span><span class="sxs-lookup"><span data-stu-id="47420-170">Distribution space summary</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="47420-171">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="47420-171">Next steps</span></span>
<span data-ttu-id="47420-172">toolearn более, статьях hello на [типы данных таблицы][Data Types], [распространение таблицы][Distribute], [индексирования таблицы] [ Index], [Секционировать таблицу][Partition], [статистики таблицы] [ Statistics] и [ Временные таблицы][Temporary].</span><span class="sxs-lookup"><span data-stu-id="47420-172">toolearn more, see hello articles on [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition], [Maintaining Table Statistics][Statistics] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="47420-173">Дополнительные рекомендации см. в статье [Рекомендации по использованию хранилища данных SQL Azure][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="47420-173">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
