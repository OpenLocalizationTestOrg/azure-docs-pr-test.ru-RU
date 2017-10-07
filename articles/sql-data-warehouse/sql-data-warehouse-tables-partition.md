---
title: "aaaPartitioning таблиц в хранилище данных SQL | Документы Microsoft"
description: "Начало работы с секционированием таблиц в хранилище данных SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 6cef870c-114f-470c-af10-02300c58885d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: aa63c51562f3e6f83063320860b195e135a721e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="partitioning-tables-in-sql-data-warehouse"></a><span data-ttu-id="eeda0-103">Секционирование таблиц в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="eeda0-103">Partitioning tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="eeda0-104">[Обзор][Overview]</span><span class="sxs-lookup"><span data-stu-id="eeda0-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="eeda0-105">[Типы данных][Data Types]</span><span class="sxs-lookup"><span data-stu-id="eeda0-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="eeda0-106">[Распределение][Distribute]</span><span class="sxs-lookup"><span data-stu-id="eeda0-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="eeda0-107">[Индекс][Index]</span><span class="sxs-lookup"><span data-stu-id="eeda0-107">[Index][Index]</span></span>
> * <span data-ttu-id="eeda0-108">[Секция][Partition]</span><span class="sxs-lookup"><span data-stu-id="eeda0-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="eeda0-109">[Статистика][Statistics]</span><span class="sxs-lookup"><span data-stu-id="eeda0-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="eeda0-110">[Временные таблицы][Temporary]</span><span class="sxs-lookup"><span data-stu-id="eeda0-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="eeda0-111">Секционирование поддерживается для всех типов таблиц хранилища данных SQL, включая таблицы с кластеризованным индексом Columnstore, кластеризованным индексом и кучу.</span><span class="sxs-lookup"><span data-stu-id="eeda0-111">Partitioning is supported on all SQL Data Warehouse table types; including clustered columnstore, clustered index, and heap.</span></span>  <span data-ttu-id="eeda0-112">Секционирование также поддерживается для всех типов распределения, включая распределение с помощью хэша или методом циклического перебора.</span><span class="sxs-lookup"><span data-stu-id="eeda0-112">Partitioning is also supported on all distribution types, including both hash or round robin distributed.</span></span>  <span data-ttu-id="eeda0-113">Секционирование позволяет toodivide копирования данных на более мелкие группы данных и в большинстве случаев секционирования для столбца дат.</span><span class="sxs-lookup"><span data-stu-id="eeda0-113">Partitioning enables you toodivide your data into smaller groups of data and in most cases, partitioning is done on a date column.</span></span>

## <a name="benefits-of-partitioning"></a><span data-ttu-id="eeda0-114">Преимущества секционирования</span><span class="sxs-lookup"><span data-stu-id="eeda0-114">Benefits of partitioning</span></span>
<span data-ttu-id="eeda0-115">Секционирование позволяет упростить операции обслуживания данных и повысить производительность запросов.</span><span class="sxs-lookup"><span data-stu-id="eeda0-115">Partitioning can benefit data maintenance and query performance.</span></span>  <span data-ttu-id="eeda0-116">Он использует оба или только один зависит способ загрузки данных и ли hello же столбец может использоваться для обоих назначений, поскольку секционирование можно выполнить только по одному столбцу.</span><span class="sxs-lookup"><span data-stu-id="eeda0-116">Whether it benefits both or just one is dependent on how data is loaded and whether hello same column can be used for both purposes, since partitioning can only be done on one column.</span></span>

### <a name="benefits-tooloads"></a><span data-ttu-id="eeda0-117">Преимущества tooloads</span><span class="sxs-lookup"><span data-stu-id="eeda0-117">Benefits tooloads</span></span>
<span data-ttu-id="eeda0-118">Hello основным преимуществом секционирования в хранилище данных SQL улучшить hello эффективность и производительность загрузка данных с помощью удаления секции, переключения и объединение.</span><span class="sxs-lookup"><span data-stu-id="eeda0-118">hello primary benefit of partitioning in SQL Data Warehouse is improve hello efficiency and performance of loading data by use of partition deletion, switching and merging.</span></span>  <span data-ttu-id="eeda0-119">В большинстве случаев секционирования данных на дату столбца, который является тесно связаны toohello последовательности, какие данные hello — загрузить toohello база данных.</span><span class="sxs-lookup"><span data-stu-id="eeda0-119">In most cases data is partitioned on a date column that is closely tied toohello sequence which hello data is loaded toohello database.</span></span>  <span data-ttu-id="eeda0-120">Одним из преимуществ Наибольшее hello с использованием секций toomaintain данных он hello Необязательность использования ведение журнала транзакций.</span><span class="sxs-lookup"><span data-stu-id="eeda0-120">One of hello greatest benefits of using partitions toomaintain data it hello avoidance of transaction logging.</span></span>  <span data-ttu-id="eeda0-121">Хотя просто Вставка, обновление или удаление данных могут быть наиболее простой подход hello с небольшой размышления и трудозатрат, используя секционирование во время процесса загрузки может значительно повысить производительность.</span><span class="sxs-lookup"><span data-stu-id="eeda0-121">While simply inserting, updating or deleting data can be hello most straightforward approach, with a little thought and effort, using partitioning during your load process can substantially improve performance.</span></span>

<span data-ttu-id="eeda0-122">Переключение секций может быть используется tooquickly удалить или заменить раздела таблицы.</span><span class="sxs-lookup"><span data-stu-id="eeda0-122">Partition switching can be used tooquickly remove or replace a section of a table.</span></span>  <span data-ttu-id="eeda0-123">Например таблица фактов может содержать только данные для hello последние 36 месяцев.</span><span class="sxs-lookup"><span data-stu-id="eeda0-123">For example, a sales fact table might contain just data for hello past 36 months.</span></span>  <span data-ttu-id="eeda0-124">В конце каждого месяца hello hello старые месяца с данными продаж удаляется из таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="eeda0-124">At hello end of every month, hello oldest month of sales data is deleted from hello table.</span></span>  <span data-ttu-id="eeda0-125">Эти данные может быть удалена с помощью данных hello toodelete инструкции delete для hello старые месяца.</span><span class="sxs-lookup"><span data-stu-id="eeda0-125">This data could be deleted by using a delete statement toodelete hello data for hello oldest month.</span></span>  <span data-ttu-id="eeda0-126">Однако удаление большого объема данных по строкам с инструкцией delete может занять очень много времени, а также создать риск hello большие транзакции, это может занять длительное время toorollback, если что-то пойдет не так.</span><span class="sxs-lookup"><span data-stu-id="eeda0-126">However, deleting a large amount of data row-by-row with a delete statement can take a very long time, as well as create hello risk of large transactions which could take a long time toorollback if something goes wrong.</span></span>  <span data-ttu-id="eeda0-127">Более Оптимальный подход — toosimply drop hello старой секции данных.</span><span class="sxs-lookup"><span data-stu-id="eeda0-127">A more optimal approach is toosimply drop hello oldest partition of data.</span></span>  <span data-ttu-id="eeda0-128">Когда удаление отдельных строк hello может занять часов, удалив весь раздел может потребоваться секунд.</span><span class="sxs-lookup"><span data-stu-id="eeda0-128">Where deleting hello individual rows could take hours, deleting an entire partition could take seconds.</span></span>

### <a name="benefits-tooqueries"></a><span data-ttu-id="eeda0-129">Преимущества tooqueries</span><span class="sxs-lookup"><span data-stu-id="eeda0-129">Benefits tooqueries</span></span>
<span data-ttu-id="eeda0-130">Секционирование также можно использовать tooimprove производительность запросов.</span><span class="sxs-lookup"><span data-stu-id="eeda0-130">Partitioning can also be used tooimprove query performance.</span></span>  <span data-ttu-id="eeda0-131">Если запрос применяет фильтр на столбец секционирования, это может ограничить hello сканирования tooonly hello уточнения разделов, которые могут быть намного меньше, подмножества данных hello, как избежать полное сканирование таблицы.</span><span class="sxs-lookup"><span data-stu-id="eeda0-131">If a query applies a filter on a partitioned column, this can limit hello scan tooonly hello qualifying partitions which may be a much smaller subset of hello data, avoiding a full table scan.</span></span>  <span data-ttu-id="eeda0-132">С появлением hello кластеризованные индексы columnstore выигрыш в производительности предиката исключения hello менее полезной, но в некоторых случаях может быть tooqueries преимущество.</span><span class="sxs-lookup"><span data-stu-id="eeda0-132">With hello introduction of clustered columnstore indexes, hello predicate elimination performance benefits are less beneficial, but in some cases there can be a benefit tooqueries.</span></span>  <span data-ttu-id="eeda0-133">Например если таблица фактов hello секционируется на 36 месяцев, с помощью поля Дата продажи hello, затем запросов, которые фильтруют на Дата продажи hello можно пропустить поиска в секциях, которые не соответствуют значению фильтра hello.</span><span class="sxs-lookup"><span data-stu-id="eeda0-133">For example, if hello sales fact table is partitioned into 36 months using hello sales date field, then queries that filter on hello sale date can skip searching in partitions that don’t match hello filter.</span></span>

## <a name="partition-sizing-guidance"></a><span data-ttu-id="eeda0-134">Руководство по определению размеров секции</span><span class="sxs-lookup"><span data-stu-id="eeda0-134">Partition sizing guidance</span></span>
<span data-ttu-id="eeda0-135">Во время секционирования может быть производительности используется tooimprove некоторые сценарии, создание таблицы с **слишком много** секций может вызвать снижение производительности при некоторых обстоятельствах.</span><span class="sxs-lookup"><span data-stu-id="eeda0-135">While partitioning can be used tooimprove performance some scenarios, creating a table with **too many** partitions can hurt performance under some circumstances.</span></span>  <span data-ttu-id="eeda0-136">В частности, это свойственно для таблиц с кластеризированными индексами Columnstore.</span><span class="sxs-lookup"><span data-stu-id="eeda0-136">These concerns are especially true for clustered columnstore tables.</span></span>  <span data-ttu-id="eeda0-137">Для секционирования toobe полезно, это важно toounderstand при toouse секционирования и hello количество секций toocreate.</span><span class="sxs-lookup"><span data-stu-id="eeda0-137">For partitioning toobe helpful, it is important toounderstand when toouse partitioning and hello number of partitions toocreate.</span></span>  <span data-ttu-id="eeda0-138">Существует правило не жестких быстрого как toohow большого числа секций слишком много, зависит от данных и сколько секций загрузке toosimultaneously.</span><span class="sxs-lookup"><span data-stu-id="eeda0-138">There is no hard fast rule as toohow many partitions are too many, it depends on your data and how many partitions you are loading toosimultaneously.</span></span>  <span data-ttu-id="eeda0-139">Но, как правило, представить Добавление десятках too100s секций не тысячах.</span><span class="sxs-lookup"><span data-stu-id="eeda0-139">But as a general rule of thumb, think of adding 10s too100s of partitions, not 1000s.</span></span>

<span data-ttu-id="eeda0-140">При создании разделов на **кластеризованном** таблиц, является важным tooconsider, сколько строк будут перемещаться в каждой секции.</span><span class="sxs-lookup"><span data-stu-id="eeda0-140">When creating partitioning on **clustered columnstore** tables, it is important tooconsider how many rows will land in each partition.</span></span>  <span data-ttu-id="eeda0-141">Для оптимального сжатия и производительности таких таблиц требуется как минимум 1 миллион строк на одно распределение и одну секцию.</span><span class="sxs-lookup"><span data-stu-id="eeda0-141">For optimal compression and performance of clustered columnstore tables, a minimum of 1 million rows per distribution and partition is needed.</span></span>  <span data-ttu-id="eeda0-142">Еще до создания секций хранилище данных SQL делит каждую таблицу на 60 распределенных баз данных.</span><span class="sxs-lookup"><span data-stu-id="eeda0-142">Before partitions are created, SQL Data Warehouse already divides each table into 60 distributed databases.</span></span>  <span data-ttu-id="eeda0-143">Любой секционирования таблицы добавлены tooa — Кроме toohello распределения, созданные в фоновом hello.</span><span class="sxs-lookup"><span data-stu-id="eeda0-143">Any partitioning added tooa table is in addition toohello distributions created behind hello scenes.</span></span>  <span data-ttu-id="eeda0-144">В этом примере, если таблица фактов hello содержится 36 ежемесячными секциями и учитывая, что хранилище данных SQL имеет 60 распределения hello фактов продаж, что таблица должна содержать 60 миллионов строк в месяц или 2.1 миллиарда строк после заполнения всех месяцев.</span><span class="sxs-lookup"><span data-stu-id="eeda0-144">Using this example, if hello sales fact table contained 36 monthly partitions, and given that SQL Data Warehouse has 60 distributions, then hello sales fact table should contain 60 million rows per month, or 2.1 billion rows when all months are populated.</span></span>  <span data-ttu-id="eeda0-145">Если таблица содержит значительно меньше строк, чем hello Рекомендуемое минимальное число строк на каждую секцию, рассмотрите возможность использования меньше секций в порядке toomake увеличение hello количество строк в секции.</span><span class="sxs-lookup"><span data-stu-id="eeda0-145">If a table contains significantly less rows than hello recommended minimum number of rows per partition, consider using fewer partitions in order toomake increase hello number of rows per partition.</span></span>  <span data-ttu-id="eeda0-146">См. также hello [индексирования] [ Index] статьи, включая запросы, которые могут быть запущены на хранилище данных SQL tooassess hello качество индексов columnstore кластера.</span><span class="sxs-lookup"><span data-stu-id="eeda0-146">Also see hello [Indexing][Index] article which includes queries that can be run on SQL Data Warehouse tooassess hello quality of cluster columnstore indexes.</span></span>

## <a name="syntax-difference-from-sql-server"></a><span data-ttu-id="eeda0-147">Отличие синтаксиса от SQL Server</span><span class="sxs-lookup"><span data-stu-id="eeda0-147">Syntax difference from SQL Server</span></span>
<span data-ttu-id="eeda0-148">В хранилище данных SQL применяется упрощенное определение секций, которое несколько отличается от аналогичного определения в SQL Server.</span><span class="sxs-lookup"><span data-stu-id="eeda0-148">SQL Data Warehouse introduces a simplified definition of partitions which is slightly different from SQL Server.</span></span>  <span data-ttu-id="eeda0-149">В хранилище данных SQL функции и схемы секционирования используются не так, как в SQL Server.</span><span class="sxs-lookup"><span data-stu-id="eeda0-149">Partitioning functions and schemes are not used in SQL Data Warehouse as they are in SQL Server.</span></span>  <span data-ttu-id="eeda0-150">Вместо этого все что нужно toodo — определения секционированного точек границ столбец и hello.</span><span class="sxs-lookup"><span data-stu-id="eeda0-150">Instead, all you need toodo is identify partitioned column and hello boundary points.</span></span>  <span data-ttu-id="eeda0-151">Хотя синтаксис hello секционирования может быть немного отличается от SQL Server, являются hello же основные понятия hello.</span><span class="sxs-lookup"><span data-stu-id="eeda0-151">While hello syntax of partitioning may be slightly different from SQL Server, hello basic concepts are hello same.</span></span>  <span data-ttu-id="eeda0-152">В SQL Server и хранилище данных SQL поддерживается по одному секционированному столбцу на таблицу, которую можно секционировать по диапазонам.</span><span class="sxs-lookup"><span data-stu-id="eeda0-152">SQL Server and SQL Data Warehouse support one partition column per table, which can be ranged partition.</span></span>  <span data-ttu-id="eeda0-153">toolearn Дополнительные сведения о секционировании, в разделе [секционированных таблиц и индексов][Partitioned Tables and Indexes].</span><span class="sxs-lookup"><span data-stu-id="eeda0-153">toolearn more about partitioning, see [Partitioned Tables and Indexes][Partitioned Tables and Indexes].</span></span>

<span data-ttu-id="eeda0-154">Hello ниже примером секционированы хранилища данных SQL [CREATE TABLE] [ CREATE TABLE] инструкции, секции таблицы FactInternetSales hello по столбцу OrderDateKey hello:</span><span class="sxs-lookup"><span data-stu-id="eeda0-154">hello below example of a SQL Data Warehouse partitioned [CREATE TABLE][CREATE TABLE] statement, partitions hello FactInternetSales table on hello OrderDateKey column:</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
    [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    (20000101,20010101,20020101
                    ,20030101,20040101,20050101
                    )
                )
)
;
```

## <a name="migrating-partitioning-from-sql-server"></a><span data-ttu-id="eeda0-155">Перенос секционирования из SQL Server</span><span class="sxs-lookup"><span data-stu-id="eeda0-155">Migrating partitioning from SQL Server</span></span>
<span data-ttu-id="eeda0-156">SQL Server toomigrate просто секционировать tooSQL определения хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="eeda0-156">toomigrate SQL Server partition definitions tooSQL Data Warehouse simply:</span></span>

* <span data-ttu-id="eeda0-157">Исключить hello SQL Server [схемы секционирования][partition scheme].</span><span class="sxs-lookup"><span data-stu-id="eeda0-157">Eliminate hello SQL Server [partition scheme][partition scheme].</span></span>
* <span data-ttu-id="eeda0-158">Добавить hello [функция секционирования] [ partition function] tooyour определение создать ТАБЛИЦУ.</span><span class="sxs-lookup"><span data-stu-id="eeda0-158">Add hello [partition function][partition function] definition tooyour CREATE TABLE.</span></span>

<span data-ttu-id="eeda0-159">При переносе секционированной таблицы из типа hello экземпляр SQL Server под SQL, чтобы toointerrogate hello количество строк в каждой секции.</span><span class="sxs-lookup"><span data-stu-id="eeda0-159">If you are migrating a partitioned table from a SQL Server instance hello below SQL can help you toointerrogate hello number of rows that are in each partition.</span></span>  <span data-ttu-id="eeda0-160">Имейте в виду, что hello одинаковую гранулярность секционирования при использовании в хранилище данных SQL, hello количество строк в секции приведет к уменьшению вдвое 60.</span><span class="sxs-lookup"><span data-stu-id="eeda0-160">Keep in mind that if hello same partitioning granularity is used on SQL Data Warehouse, hello number of rows per partition will decrease by a factor of 60.</span></span>  

```sql
-- Partition information for a SQL Server Database
SELECT      s.[name]                        AS      [schema_name]
,           t.[name]                        AS      [table_name]
,           i.[name]                        AS      [index_name]
,           p.[partition_number]            AS      [partition_number]
,           SUM(a.[used_pages]*8.0)         AS      [partition_size_kb]
,           SUM(a.[used_pages]*8.0)/1024    AS      [partition_size_mb]
,           SUM(a.[used_pages]*8.0)/1048576 AS      [partition_size_gb]
,           p.[rows]                        AS      [partition_row_count]
,           rv.[value]                      AS      [partition_boundary_value]
,           p.[data_compression_desc]       AS      [partition_compression_desc]
FROM        sys.schemas s
JOIN        sys.tables t                    ON      t.[schema_id]         = s.[schema_id]
JOIN        sys.partitions p                ON      p.[object_id]         = t.[object_id]
JOIN        sys.allocation_units a          ON      a.[container_id]      = p.[partition_id]
JOIN        sys.indexes i                   ON      i.[object_id]         = p.[object_id]
                                            AND     i.[index_id]          = p.[index_id]
JOIN        sys.data_spaces ds              ON      ds.[data_space_id]    = i.[data_space_id]
LEFT JOIN   sys.partition_schemes ps        ON      ps.[data_space_id]    = ds.[data_space_id]
LEFT JOIN   sys.partition_functions pf      ON      pf.[function_id]      = ps.[function_id]
LEFT JOIN   sys.partition_range_values rv   ON      rv.[function_id]      = pf.[function_id]
                                            AND     rv.[boundary_id]      = p.[partition_number]
WHERE       p.[index_id] <=1
GROUP BY    s.[name]
,           t.[name]
,           i.[name]
,           p.[partition_number]
,           p.[rows]
,           rv.[value]
,           p.[data_compression_desc]
;
```

## <a name="workload-management"></a><span data-ttu-id="eeda0-161">Управление рабочей нагрузкой</span><span class="sxs-lookup"><span data-stu-id="eeda0-161">Workload management</span></span>
<span data-ttu-id="eeda0-162">— Один toofactor рассмотрения завершающего элемента в решение секции таблицы toohello [управления рабочей нагрузкой][workload management].</span><span class="sxs-lookup"><span data-stu-id="eeda0-162">One final piece consideration toofactor in toohello table partition decision is [workload management][workload management].</span></span>  <span data-ttu-id="eeda0-163">Управление рабочими нагрузками в хранилище данных SQL — в первую очередь hello управление памяти и параллелизма.</span><span class="sxs-lookup"><span data-stu-id="eeda0-163">Workload management in SQL Data Warehouse is primarily hello management of memory and concurrency.</span></span>  <span data-ttu-id="eeda0-164">В хранилище данных SQL hello максимальный объем памяти, выделенной tooeach распространения во время выполнения запроса является классов управляемых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="eeda0-164">In SQL Data Warehouse hello maximum memory allocated tooeach distribution during query execution is governed resource classes.</span></span>  <span data-ttu-id="eeda0-165">В идеале секций будет изменяться размер буферная таких факторов, как hello памяти, необходимой построение кластеризованных индексов.</span><span class="sxs-lookup"><span data-stu-id="eeda0-165">Ideally your partitions will be sized in consideration of other factors like hello memory needs of building clustered columnstore indexes.</span></span>  <span data-ttu-id="eeda0-166">Кластеризованные индексы Columnstore наиболее эффективны, когда для них выделяется больший объем памяти.</span><span class="sxs-lookup"><span data-stu-id="eeda0-166">Clustered columnstore indexes benefit greatly when they are allocated more memory.</span></span>  <span data-ttu-id="eeda0-167">Таким образом необходимо вернуть tooensure, перестройте индекс секции не испытывает существенной нехватки памяти.</span><span class="sxs-lookup"><span data-stu-id="eeda0-167">Therefore, you will want tooensure that a partition index rebuild is not starved of memory.</span></span> <span data-ttu-id="eeda0-168">Увеличение hello объем памяти, доступной tooyour запроса достигается путем переключения из роли по умолчанию hello, smallrc, tooone из других ролей, таких как largerc "hello".</span><span class="sxs-lookup"><span data-stu-id="eeda0-168">Increasing hello amount of memory available tooyour query can be achieved by switching from hello default role, smallrc, tooone of hello other roles such as largerc.</span></span>

<span data-ttu-id="eeda0-169">Сведения на hello выделения памяти для каждого распространителя можно найти с помощью запроса представления динамического управления регулятора ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="eeda0-169">Information on hello allocation of memory per distribution is available by querying hello resource governor dynamic management views.</span></span> <span data-ttu-id="eeda0-170">На самом деле на предоставление памяти будет меньше hello рисунках.</span><span class="sxs-lookup"><span data-stu-id="eeda0-170">In reality your memory grant will be less than hello figures below.</span></span> <span data-ttu-id="eeda0-171">Информация приведена на уровне рекомендации, ее можно использовать при планировании размера секций для операций управления данными.</span><span class="sxs-lookup"><span data-stu-id="eeda0-171">However, this provides a level of guidance that you can use when sizing your partitions for data management operations.</span></span>  <span data-ttu-id="eeda0-172">Попробуйте tooavoid изменение размера секций после предоставления памяти hello, предоставляемый классом долгосрочного ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="eeda0-172">Try tooavoid sizing your partitions beyond hello memory grant provided by hello extra large resource class.</span></span> <span data-ttu-id="eeda0-173">Если увеличение секций на рисунке запуском риск hello свободной памяти, что в свою очередь ведет оптимальное сжатие сборки.</span><span class="sxs-lookup"><span data-stu-id="eeda0-173">If your partitions grow beyond this figure you run hello risk of memory pressure which in turn leads tooless optimal compression.</span></span>

```sql
SELECT  rp.[name]                                AS [pool_name]
,       rp.[max_memory_kb]                        AS [max_memory_kb]
,       rp.[max_memory_kb]/1024                    AS [max_memory_mb]
,       rp.[max_memory_kb]/1048576                AS [mex_memory_gb]
,       rp.[max_memory_percent]                    AS [max_memory_percent]
,       wg.[name]                                AS [group_name]
,       wg.[importance]                            AS [group_importance]
,       wg.[request_max_memory_grant_percent]    AS [request_max_memory_grant_percent]
FROM    sys.dm_pdw_nodes_resource_governor_workload_groups    wg
JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools    rp ON wg.[pool_id] = rp.[pool_id]
WHERE   wg.[name] like 'SloDWGroup%'
AND     rp.[name]    = 'SloDWPool'
;
```

## <a name="partition-switching"></a><span data-ttu-id="eeda0-174">Переключение секций</span><span class="sxs-lookup"><span data-stu-id="eeda0-174">Partition switching</span></span>
<span data-ttu-id="eeda0-175">Хранилище данных SQL поддерживает разбиение, слияние и переключение секций.</span><span class="sxs-lookup"><span data-stu-id="eeda0-175">SQL Data Warehouse supports partition splitting, merging, and switching.</span></span> <span data-ttu-id="eeda0-176">Каждая из этих функций — с помощью hello excuted [ALTER TABLE] [ ALTER TABLE] инструкции.</span><span class="sxs-lookup"><span data-stu-id="eeda0-176">Each of these functions is excuted using hello [ALTER TABLE][ALTER TABLE] statement.</span></span>

<span data-ttu-id="eeda0-177">tooswitch секций между двумя таблицами, необходимо убедиться, что секции hello выровнены по их соответствующих границ и соответствуют hello определения таблиц.</span><span class="sxs-lookup"><span data-stu-id="eeda0-177">tooswitch partitions between two tables you must ensure that hello partitions align on their respective boundaries and that hello table definitions match.</span></span> <span data-ttu-id="eeda0-178">Проверочные ограничения не являются доступными tooenforce hello диапазона значений в таблице hello исходной таблицы должен содержать hello же секции границы как hello целевой таблицы.</span><span class="sxs-lookup"><span data-stu-id="eeda0-178">As check constraints are not available tooenforce hello range of values in a table hello source table must contain hello same partition boundaries as hello target table.</span></span> <span data-ttu-id="eeda0-179">Если это не так hello, hello переключение секции завершится ошибкой, hello метаданных секции не будут синхронизированы.</span><span class="sxs-lookup"><span data-stu-id="eeda0-179">If this is not hello case, then hello partition switch will fail as hello partition metadata will not be synchronized.</span></span>

### <a name="how-toosplit-a-partition-that-contains-data"></a><span data-ttu-id="eeda0-180">Как toosplit секцию, которая содержит данные</span><span class="sxs-lookup"><span data-stu-id="eeda0-180">How toosplit a partition that contains data</span></span>
<span data-ttu-id="eeda0-181">Hello наиболее эффективный метод toosplit секцию, которая уже содержит данные — toouse `CTAS` инструкции.</span><span class="sxs-lookup"><span data-stu-id="eeda0-181">hello most efficient method toosplit a partition that already contains data is toouse a `CTAS` statement.</span></span> <span data-ttu-id="eeda0-182">Если кластеризованный индекс columnstore секционированной таблицы hello затем hello таблицы секция должна быть пустой, прежде чем она может быть разбита.</span><span class="sxs-lookup"><span data-stu-id="eeda0-182">If hello partitioned table is a clustered columnstore then hello table partition must be empty before it can be split.</span></span>

<span data-ttu-id="eeda0-183">Ниже приведен пример секционированной таблицы columnstore, содержащей по одной строке в каждой секции:</span><span class="sxs-lookup"><span data-stu-id="eeda0-183">Below is a sample partitioned columnstore table containing one row in each partition:</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
        [ProductKey]            int          NOT NULL
    ,   [OrderDateKey]          int          NOT NULL
    ,   [CustomerKey]           int          NOT NULL
    ,   [PromotionKey]          int          NOT NULL
    ,   [SalesOrderNumber]      nvarchar(20) NOT NULL
    ,   [OrderQuantity]         smallint     NOT NULL
    ,   [UnitPrice]             money        NOT NULL
    ,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    (20000101
                    )
                )
)
;

INSERT INTO dbo.FactInternetSales
VALUES (1,19990101,1,1,1,1,1,1);
INSERT INTO dbo.FactInternetSales
VALUES (1,20000101,1,1,1,1,1,1);


CREATE STATISTICS Stat_dbo_FactInternetSales_OrderDateKey ON dbo.FactInternetSales(OrderDateKey);
```

> [!NOTE]
> <span data-ttu-id="eeda0-184">По объекту статистики Создание hello мы убедитесь, что является более точной метаданные этой таблицы.</span><span class="sxs-lookup"><span data-stu-id="eeda0-184">By Creating hello statistic object, we ensure that table metadata is more accurate.</span></span> <span data-ttu-id="eeda0-185">Если пропустить создание объекта статистики, хранилище данных SQL будет использовать значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="eeda0-185">If we omit creating statistics, then SQL Data Warehouse will use default values.</span></span> <span data-ttu-id="eeda0-186">Сведения об управлении статистикой таблиц в хранилище данных SQL см. в [этой статье][statistics].</span><span class="sxs-lookup"><span data-stu-id="eeda0-186">For details on statistics please review [statistics][statistics].</span></span>
> 
> 

<span data-ttu-id="eeda0-187">Затем мы можете запрашивать hello количество строк, с помощью hello `sys.partitions` представления каталога:</span><span class="sxs-lookup"><span data-stu-id="eeda0-187">We can then query for hello row count using hello `sys.partitions` catalog view:</span></span>

```sql
SELECT  QUOTENAME(s.[name])+'.'+QUOTENAME(t.[name]) as Table_name
,       i.[name] as Index_name
,       p.partition_number as Partition_nmbr
,       p.[rows] as Row_count
,       p.[data_compression_desc] as Data_Compression_desc
FROM    sys.partitions p
JOIN    sys.tables     t    ON    p.[object_id]   = t.[object_id]
JOIN    sys.schemas    s    ON    t.[schema_id]   = s.[schema_id]
JOIN    sys.indexes    i    ON    p.[object_id]   = i.[object_Id]
                            AND   p.[index_Id]    = i.[index_Id]
WHERE t.[name] = 'FactInternetSales'
;
```

<span data-ttu-id="eeda0-188">Если мы попытаемся toosplit этой таблицы, возникает ошибка:</span><span class="sxs-lookup"><span data-stu-id="eeda0-188">If we try toosplit this table, we will get an error:</span></span>

```sql
ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

<span data-ttu-id="eeda0-189">Msg 35346 уровень 15, состояние 1, строку 44 РАЗДЕЛИТЬ предложением инструкции ALTER PARTITION сбой hello секция не пуста.</span><span class="sxs-lookup"><span data-stu-id="eeda0-189">Msg 35346, Level 15, State 1, Line 44 SPLIT clause of ALTER PARTITION statement failed because hello partition is not empty.</span></span>  <span data-ttu-id="eeda0-190">Только пустые секции могут быть разбиты в, если существует индекс columnstore в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="eeda0-190">Only empty partitions can be split in when a columnstore index exists on hello table.</span></span> <span data-ttu-id="eeda0-191">Рекомендуется отключить индекс columnstore hello перед выполнения инструкции ALTER PARTITION hello, а перестроение индекса columnstore hello после завершения инструкции ALTER PARTITION.</span><span class="sxs-lookup"><span data-stu-id="eeda0-191">Consider disabling hello columnstore index before issuing hello ALTER PARTITION statement, then rebuilding hello columnstore index after ALTER PARTITION is complete.</span></span>

<span data-ttu-id="eeda0-192">Тем не менее, мы используем `CTAS` toocreate новый toohold таблицы данных.</span><span class="sxs-lookup"><span data-stu-id="eeda0-192">However, we can use `CTAS` toocreate a new table toohold our data.</span></span>

```sql
CREATE TABLE dbo.FactInternetSales_20000101
    WITH    (   DISTRIBUTION = HASH(ProductKey)
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101
                                )
                            )
            )
AS
SELECT *
FROM    FactInternetSales
WHERE   1=2
;
```

<span data-ttu-id="eeda0-193">Выровненный границы секций hello разрешается переключателя.</span><span class="sxs-lookup"><span data-stu-id="eeda0-193">As hello partition boundaries are aligned a switch is permitted.</span></span> <span data-ttu-id="eeda0-194">Пустая секция, мы впоследствии можно разделить, оставлять hello исходной таблицы.</span><span class="sxs-lookup"><span data-stu-id="eeda0-194">This will leave hello source table with an empty partition that we can subsequently split.</span></span>

```sql
ALTER TABLE FactInternetSales SWITCH PARTITION 2 too FactInternetSales_20000101 PARTITION 2;

ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

<span data-ttu-id="eeda0-195">Все, что остается toodo — tooalign toohello наши данные секции новые границы, используя `CTAS` и переключитесь обратно в основной таблице toohello наши данные</span><span class="sxs-lookup"><span data-stu-id="eeda0-195">All that is left toodo is tooalign our data toohello new partition boundaries using `CTAS` and switch our data back in toohello main table</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_20000101_20010101]
    WITH    (   DISTRIBUTION = HASH([ProductKey])
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101,20010101
                                )
                            )
            )
AS
SELECT  *
FROM    [dbo].[FactInternetSales_20000101]
WHERE   [OrderDateKey] >= 20000101
AND     [OrderDateKey] <  20010101
;

ALTER TABLE dbo.FactInternetSales_20000101_20010101 SWITCH PARTITION 2 toodbo.FactInternetSales PARTITION 2;
```

<span data-ttu-id="eeda0-196">После завершения перемещения hello hello данных является хорошей идеей toorefresh hello статистики на hello целевой таблицы tooensure они точно отражают hello новый распределение данных hello в их соответствующие разделы:</span><span class="sxs-lookup"><span data-stu-id="eeda0-196">Once you have completed hello movement of hello data it is a good idea toorefresh hello statistics on hello target table tooensure they accurately reflect hello new distribution of hello data in their respective partitions:</span></span>

```sql
UPDATE STATISTICS [dbo].[FactInternetSales];
```

### <a name="table-partitioning-source-control"></a><span data-ttu-id="eeda0-197">Система управления версиями секционирования таблиц</span><span class="sxs-lookup"><span data-stu-id="eeda0-197">Table partitioning source control</span></span>
<span data-ttu-id="eeda0-198">tooavoid определение таблицы из **ржавчина** в системе управления версиями можно tooconsider hello следующий подход:</span><span class="sxs-lookup"><span data-stu-id="eeda0-198">tooavoid your table definition from **rusting** in your source control system you may want tooconsider hello following approach:</span></span>

1. <span data-ttu-id="eeda0-199">Создать hello таблицы как секционированной таблицы, но без значений секционирования</span><span class="sxs-lookup"><span data-stu-id="eeda0-199">Create hello table as a partitioned table but with no partition values</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
    [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    ()
                )
)
;
```

1. <span data-ttu-id="eeda0-200">`SPLIT`Таблица Hello в рамках процесса развертывания hello:</span><span class="sxs-lookup"><span data-stu-id="eeda0-200">`SPLIT` hello table as part of hello deployment process:</span></span>

```sql
-- Create a table containing hello partition boundaries

CREATE TABLE #partitions
WITH
(
    LOCATION = USER_DB
,   DISTRIBUTION = HASH(ptn_no)
)
AS
SELECT  ptn_no
,       ROW_NUMBER() OVER (ORDER BY (ptn_no)) as seq_no
FROM    (
        SELECT CAST(20000101 AS INT) ptn_no
        UNION ALL
        SELECT CAST(20010101 AS INT)
        UNION ALL
        SELECT CAST(20020101 AS INT)
        UNION ALL
        SELECT CAST(20030101 AS INT)
        UNION ALL
        SELECT CAST(20040101 AS INT)
        ) a
;

-- Iterate over hello partition boundaries and split hello table

DECLARE @c INT = (SELECT COUNT(*) FROM #partitions)
,       @i INT = 1                                 --iterator for while loop
,       @q NVARCHAR(4000)                          --query
,       @p NVARCHAR(20)     = N''                  --partition_number
,       @s NVARCHAR(128)    = N'dbo'               --schema
,       @t NVARCHAR(128)    = N'FactInternetSales' --table
;

WHILE @i <= @c
BEGIN
    SET @p = (SELECT ptn_no FROM #partitions WHERE seq_no = @i);
    SET @q = (SELECT N'ALTER TABLE '+@s+N'.'+@t+N' SPLIT RANGE ('+@p+N');');

    -- PRINT @q;
    EXECUTE sp_executesql @q;

    SET @i+=1;
END

-- Code clean-up

DROP TABLE #partitions;
```

<span data-ttu-id="eeda0-201">С этого подхода hello кода в системе управления версиями остается статические и hello секционирования граничных значений допускаются toobe динамического; развиваться с хранилищем hello со временем.</span><span class="sxs-lookup"><span data-stu-id="eeda0-201">With this approach hello code in source control remains static and hello partitioning boundary values are allowed toobe dynamic; evolving with hello warehouse over time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eeda0-202">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="eeda0-202">Next steps</span></span>
<span data-ttu-id="eeda0-203">toolearn более, статьях hello на [Общие сведения о таблицах][Overview], [типы данных таблицы][Data Types], [распространение таблицы] [ Distribute], [Индексирования таблицы][Index], [статистики таблицы] [ Statistics] и [ Временные таблицы][Temporary].</span><span class="sxs-lookup"><span data-stu-id="eeda0-203">toolearn more, see hello articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index], [Maintaining Table Statistics][Statistics] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="eeda0-204">Дополнительные рекомендации см. в статье [Рекомендации по использованию хранилища данных SQL Azure][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="eeda0-204">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[workload management]: ./sql-data-warehouse-develop-concurrency.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!-- MSDN Articles -->
[Partitioned Tables and Indexes]: https://msdn.microsoft.com/library/ms190787.aspx
[ALTER TABLE]: https://msdn.microsoft.com/en-us/library/ms190273.aspx
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[partition function]: https://msdn.microsoft.com/library/ms187802.aspx
[partition scheme]: https://msdn.microsoft.com/library/ms179854.aspx


<!-- Other web references -->
