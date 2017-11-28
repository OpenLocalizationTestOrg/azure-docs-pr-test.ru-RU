---
title: "aaaTemporary таблиц в хранилище данных SQL | Документы Microsoft"
description: "Начало работы с временными таблицами в хранилище данных SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 9b1119eb-7f54-46d0-ad74-19c85a2a555a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 2e8b122eb6d71d5bc0a99ce8a2ecab5dbe2d1b49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="temporary-tables-in-sql-data-warehouse"></a><span data-ttu-id="1f927-103">Временные таблицы в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="1f927-103">Temporary tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="1f927-104">[Обзор][Overview]</span><span class="sxs-lookup"><span data-stu-id="1f927-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="1f927-105">[Типы данных][Data Types]</span><span class="sxs-lookup"><span data-stu-id="1f927-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="1f927-106">[Распределение][Distribute]</span><span class="sxs-lookup"><span data-stu-id="1f927-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="1f927-107">[Индекс][Index]</span><span class="sxs-lookup"><span data-stu-id="1f927-107">[Index][Index]</span></span>
> * <span data-ttu-id="1f927-108">[Секция][Partition]</span><span class="sxs-lookup"><span data-stu-id="1f927-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="1f927-109">[Статистика][Statistics]</span><span class="sxs-lookup"><span data-stu-id="1f927-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="1f927-110">[Временные таблицы][Temporary]</span><span class="sxs-lookup"><span data-stu-id="1f927-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="1f927-111">Временные таблицы очень полезны при обработке данных — особенно во время преобразования, где hello промежуточные результаты являются временными.</span><span class="sxs-lookup"><span data-stu-id="1f927-111">Temporary tables are very useful when processing data - especially during transformation where hello intermediate results are transient.</span></span> <span data-ttu-id="1f927-112">В хранилище данных SQL временная таблица существует на уровне сеанса hello.</span><span class="sxs-lookup"><span data-stu-id="1f927-112">In SQL Data Warehouse temporary tables exist at hello session level.</span></span>  <span data-ttu-id="1f927-113">Они являются только видимым toohello сеанс в котором они были созданы и автоматически удаляются при выходе этого сеанса.</span><span class="sxs-lookup"><span data-stu-id="1f927-113">They are only visible toohello session in which they were created and are automatically dropped when that session logs off.</span></span>  <span data-ttu-id="1f927-114">Временные таблицы обеспечивают выигрыш в производительности, так как их результаты записываются toolocal, а не внешнего хранилища.</span><span class="sxs-lookup"><span data-stu-id="1f927-114">Temporary tables offer a performance benefit because their results are written toolocal rather than remote storage.</span></span>  <span data-ttu-id="1f927-115">Временные таблицы являются немного отличается от базы данных SQL Azure, в хранилище данных SQL Azure, как они могут осуществляться из любого места внутри hello сеанса, включая как внутри, так и вне хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="1f927-115">Temporary tables are slightly different in Azure SQL Data Warehouse than Azure SQL Database as they can be accessed from anywhere inside hello session, including both inside and outside of a stored procedure.</span></span>

<span data-ttu-id="1f927-116">В этой статье содержит основные рекомендации по использованию временных таблиц и выделяет hello принципы уровня временных таблиц сеансов.</span><span class="sxs-lookup"><span data-stu-id="1f927-116">This article contains essential guidance for using temporary tables and highlights hello principles of session level temporary tables.</span></span> <span data-ttu-id="1f927-117">С помощью hello сведения в этой статье помогут вам структуры модулей кода, повышения повторного использования и простоту обслуживания кода.</span><span class="sxs-lookup"><span data-stu-id="1f927-117">Using hello information in this article can help you modularize your code, improving both reusability and ease of maintenance of your code.</span></span>

## <a name="create-a-temporary-table"></a><span data-ttu-id="1f927-118">Создание временной таблицы</span><span class="sxs-lookup"><span data-stu-id="1f927-118">Create a temporary table</span></span>
<span data-ttu-id="1f927-119">Временные таблицы создаются простым добавлением к имени таблицы префикса `#`.</span><span class="sxs-lookup"><span data-stu-id="1f927-119">Temporary tables are created by simply prefixing your table name with a `#`.</span></span>  <span data-ttu-id="1f927-120">Например:</span><span class="sxs-lookup"><span data-stu-id="1f927-120">For example:</span></span>

```sql
CREATE TABLE #stats_ddl
(
    [schema_name]        NVARCHAR(128) NOT NULL
,    [table_name]            NVARCHAR(128) NOT NULL
,    [stats_name]            NVARCHAR(128) NOT NULL
,    [stats_is_filtered]     BIT           NOT NULL
,    [seq_nmbr]              BIGINT        NOT NULL
,    [two_part_name]         NVARCHAR(260) NOT NULL
,    [three_part_name]       NVARCHAR(400) NOT NULL
)
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
,    HEAP
)
```

<span data-ttu-id="1f927-121">Временные таблицы можно также создать с помощью `CTAS` точно с помощью hello же подход:</span><span class="sxs-lookup"><span data-stu-id="1f927-121">Temporary tables can also be created with a `CTAS` using exactly hello same approach:</span></span>

```sql
CREATE TABLE #stats_ddl
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
,    HEAP
)
AS
(
SELECT
        sm.[name]                                                                AS [schema_name]
,        tb.[name]                                                                AS [table_name]
,        st.[name]                                                                AS [stats_name]
,        st.[has_filter]                                                            AS [stats_is_filtered]
,       ROW_NUMBER()
        OVER(ORDER BY (SELECT NULL))                                            AS [seq_nmbr]
,                                 QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [two_part_name]
,        QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [three_part_name]
FROM    sys.objects            AS ob
JOIN    sys.stats            AS st    ON    ob.[object_id]        = st.[object_id]
JOIN    sys.stats_columns    AS sc    ON    st.[stats_id]        = sc.[stats_id]
                                    AND st.[object_id]        = sc.[object_id]
JOIN    sys.columns            AS co    ON    sc.[column_id]        = co.[column_id]
                                    AND    sc.[object_id]        = co.[object_id]
JOIN    sys.tables            AS tb    ON    co.[object_id]        = tb.[object_id]
JOIN    sys.schemas            AS sm    ON    tb.[schema_id]        = sm.[schema_id]
WHERE    1=1
AND        st.[user_created]   = 1
GROUP BY
        sm.[name]
,        tb.[name]
,        st.[name]
,        st.[filter_definition]
,        st.[has_filter]
)
SELECT
    CASE @update_type
    WHEN 1
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+');'
    WHEN 2
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH FULLSCAN;'
    WHEN 3
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH SAMPLE '+CAST(@sample_pct AS VARCHAR(20))+' PERCENT;'
    WHEN 4
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH RESAMPLE;'
    END AS [update_stats_ddl]
,   [seq_nmbr]
FROM    t1
;
``` 

> [!NOTE]
> <span data-ttu-id="1f927-122">`CTAS`Это очень мощный команда и hello добавил преимуществом является очень эффективен при ее использовании места в журнале транзакций.</span><span class="sxs-lookup"><span data-stu-id="1f927-122">`CTAS` is a very powerful command and has hello added advantage of being very efficient in its use of transaction log space.</span></span> 
> 
> 

## <a name="dropping-temporary-tables"></a><span data-ttu-id="1f927-123">Удаление временных таблиц</span><span class="sxs-lookup"><span data-stu-id="1f927-123">Dropping temporary tables</span></span>
<span data-ttu-id="1f927-124">При создании сеанса не должно быть ни одной временной таблицы.</span><span class="sxs-lookup"><span data-stu-id="1f927-124">When a new session is created, no temporary tables should exist.</span></span>  <span data-ttu-id="1f927-125">Тем не менее, при вызове hello же хранимой процедуры, которая создает временную с hello таким же именем, tooensure, ваш `CREATE TABLE` инструкции выполняются успешно простую проверку существования предварительной с `DROP` может использоваться как hello в примере ниже:</span><span class="sxs-lookup"><span data-stu-id="1f927-125">However, if you are calling hello same stored procedure, which creates a temporary with hello same name, tooensure that your `CREATE TABLE` statements are successful a simple pre-existence check with a `DROP` can be used as in hello below example:</span></span>

```sql
IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END
```

<span data-ttu-id="1f927-126">Для кодирования согласованности, это хорошо практики toouse этот шаблон для таблиц и временных таблиц.</span><span class="sxs-lookup"><span data-stu-id="1f927-126">For coding consistency, it is a good practice toouse this pattern for both tables and temporary tables.</span></span>  <span data-ttu-id="1f927-127">Это также toouse смысл `DROP TABLE` tooremove временные таблицы после завершения с ними в коде.</span><span class="sxs-lookup"><span data-stu-id="1f927-127">It is also a good idea toouse `DROP TABLE` tooremove temporary tables when you have finished with them in your code.</span></span>  <span data-ttu-id="1f927-128">В хранимой процедуре разработки это довольно часто toosee hello команд drop объединяются в конце hello tooensure процедуры, эти объекты очищаются.</span><span class="sxs-lookup"><span data-stu-id="1f927-128">In stored procedure development it is quite common toosee hello drop commands bundled together at hello end of a procedure tooensure these objects are cleaned up.</span></span>

```sql
DROP TABLE #stats_ddl
```

## <a name="modularizing-code"></a><span data-ttu-id="1f927-129">Разделение кода на модули</span><span class="sxs-lookup"><span data-stu-id="1f927-129">Modularizing code</span></span>
<span data-ttu-id="1f927-130">Так как временные таблицы можно увидеть в любом месте в сеансе пользователя, это может быть Устранение toohelp можно разбить на модули кода приложения.</span><span class="sxs-lookup"><span data-stu-id="1f927-130">Since temporary tables can be seen anywhere in a user session, this can be exploited toohelp you modularize your application code.</span></span>  <span data-ttu-id="1f927-131">Например hello ниже хранимая процедура объединяет в себе hello, рекомендации по работе из верхнего toogenerate DDL, в которой будет обновление всей статистики в базе данных hello, имя статистики.</span><span class="sxs-lookup"><span data-stu-id="1f927-131">For example, hello stored procedure below brings together hello recommended practices from above toogenerate DDL which will update all statistics in hello database by statistic name.</span></span>

```sql
CREATE PROCEDURE    [dbo].[prc_sqldw_update_stats]
(   @update_type    tinyint -- 1 default 2 fullscan 3 sample 4 resample
    ,@sample_pct     tinyint
)
AS

IF @update_type NOT IN (1,2,3,4)
BEGIN;
    THROW 151000,'Invalid value for @update_type parameter. Valid range 1 (default), 2 (fullscan), 3 (sample) or 4 (resample).',1;
END;

IF @sample_pct IS NULL
BEGIN;
    SET @sample_pct = 20;
END;

IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END

CREATE TABLE #stats_ddl
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
)
AS
(
SELECT
        sm.[name]                                                                AS [schema_name]
,        tb.[name]                                                                AS [table_name]
,        st.[name]                                                                AS [stats_name]
,        st.[has_filter]                                                            AS [stats_is_filtered]
,       ROW_NUMBER()
        OVER(ORDER BY (SELECT NULL))                                            AS [seq_nmbr]
,                                 QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [two_part_name]
,        QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [three_part_name]
FROM    sys.objects            AS ob
JOIN    sys.stats            AS st    ON    ob.[object_id]        = st.[object_id]
JOIN    sys.stats_columns    AS sc    ON    st.[stats_id]        = sc.[stats_id]
                                    AND st.[object_id]        = sc.[object_id]
JOIN    sys.columns            AS co    ON    sc.[column_id]        = co.[column_id]
                                    AND    sc.[object_id]        = co.[object_id]
JOIN    sys.tables            AS tb    ON    co.[object_id]        = tb.[object_id]
JOIN    sys.schemas            AS sm    ON    tb.[schema_id]        = sm.[schema_id]
WHERE    1=1
AND        st.[user_created]   = 1
GROUP BY
        sm.[name]
,        tb.[name]
,        st.[name]
,        st.[filter_definition]
,        st.[has_filter]
)
SELECT
    CASE @update_type
    WHEN 1
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+');'
    WHEN 2
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH FULLSCAN;'
    WHEN 3
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH SAMPLE '+CAST(@sample_pct AS VARCHAR(20))+' PERCENT;'
    WHEN 4
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH RESAMPLE;'
    END AS [update_stats_ddl]
,   [seq_nmbr]
FROM    t1
;
GO
```

<span data-ttu-id="1f927-132">На этом этапе hello единственным действием, которое произошло является создание hello хранимая процедура, которая будет просто ошибке временная таблица stats_ddl #, с помощью инструкций DDL.</span><span class="sxs-lookup"><span data-stu-id="1f927-132">At this stage hello only action that has occurred is hello creation of a stored procedure which will simply generated a temporary table, #stats_ddl, with DDL statements.</span></span>  <span data-ttu-id="1f927-133">Эта хранимая процедура будет удалена #stats_ddl, если он уже существует tooensure, он не завершаться ошибкой, если выполнить более одного раза в пределах одного сеанса.</span><span class="sxs-lookup"><span data-stu-id="1f927-133">This stored procedure will drop #stats_ddl if it already exists tooensure it does not fail if run more than once within a session.</span></span>  <span data-ttu-id="1f927-134">Тем не менее так как она не `DROP TABLE` конце hello hello хранимой процедуры, после hello хранимой процедуры, она будет закрыто hello создания таблицы, чтобы она могла считывать вне hello хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="1f927-134">However, since there is no `DROP TABLE` at hello end of hello stored procedure, when hello stored procedure completes, it will leave hello created table so that it can be read outside of hello stored procedure.</span></span>  <span data-ttu-id="1f927-135">В хранилище данных SQL в отличие от других баз данных SQL Server, это временная таблица возможных toouse hello вне процедуры hello, в которой он был создан.</span><span class="sxs-lookup"><span data-stu-id="1f927-135">In SQL Data Warehouse, unlike other SQL Server databases, it is possible toouse hello temporary table outside of hello procedure that created it.</span></span>  <span data-ttu-id="1f927-136">Временные таблицы хранилища данных SQL можно использовать **в любом** внутри сеанса hello.</span><span class="sxs-lookup"><span data-stu-id="1f927-136">SQL Data Warehouse temporary tables can be used **anywhere** inside hello session.</span></span> <span data-ttu-id="1f927-137">Это может привести к toomore модульных и управляемость кода как hello в примере ниже:</span><span class="sxs-lookup"><span data-stu-id="1f927-137">This can lead toomore modular and manageable code as in hello below example:</span></span>

```sql
EXEC [dbo].[prc_sqldw_update_stats] @update_type = 1, @sample_pct = NULL;

DECLARE @i INT              = 1
,       @t INT              = (SELECT COUNT(*) FROM #stats_ddl)
,       @s NVARCHAR(4000)   = N''

WHILE @i <= @t
BEGIN
    SET @s=(SELECT update_stats_ddl FROM #stats_ddl WHERE seq_nmbr = @i);

    PRINT @s
    EXEC sp_executesql @s
    SET @i+=1;
END

DROP TABLE #stats_ddl;
```

## <a name="temporary-table-limitations"></a><span data-ttu-id="1f927-138">Ограничения временной таблицы</span><span class="sxs-lookup"><span data-stu-id="1f927-138">Temporary table limitations</span></span>
<span data-ttu-id="1f927-139">В хранилище данных SQL есть несколько ограничений, касающихся реализации временных таблиц.</span><span class="sxs-lookup"><span data-stu-id="1f927-139">SQL Data Warehouse does impose a couple of limitations when implementing temporary tables.</span></span>  <span data-ttu-id="1f927-140">В настоящее время поддерживаются временные таблицы, которые можно просмотреть только в сеансе.</span><span class="sxs-lookup"><span data-stu-id="1f927-140">Currently, only session scoped temporary tables are supported.</span></span>  <span data-ttu-id="1f927-141">Глобальные временные таблицы не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="1f927-141">Global Temporary Tables are not supported.</span></span>  <span data-ttu-id="1f927-142">Кроме того, для временных таблиц нельзя создавать представления.</span><span class="sxs-lookup"><span data-stu-id="1f927-142">In addition, views cannot be created on temporary tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f927-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1f927-143">Next steps</span></span>
<span data-ttu-id="1f927-144">toolearn более, статьях hello на [Общие сведения о таблицах][Overview], [типы данных таблицы][Data Types], [распространение таблицы] [ Distribute], [Индексирования таблицы][Index], [секционировать таблицу] [ Partition] и [ Таблица статистики][Statistics].</span><span class="sxs-lookup"><span data-stu-id="1f927-144">toolearn more, see hello articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Maintaining Table Statistics][Statistics].</span></span>  <span data-ttu-id="1f927-145">Дополнительные рекомендации см. в статье [Рекомендации по использованию хранилища данных SQL Azure][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="1f927-145">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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

<!--MSDN references-->

<!--Other Web references-->
