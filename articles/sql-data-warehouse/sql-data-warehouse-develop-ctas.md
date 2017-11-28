---
title: "Таблица aaaCreate выбора (CTAS) в хранилище данных SQL | Документы Microsoft"
description: "Советы для создания кода с hello создание таблицы как select, инструкция (CTAS) в хранилище данных SQL Azure для разработки решений."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 68ac9a94-09f9-424b-b536-06a125a653bd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 01/30/2017
ms.author: shigu;barbkess
ms.openlocfilehash: e381601a0a4d94e189d8f9115bf2e7593025410b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-table-as-select-ctas-in-sql-data-warehouse"></a><span data-ttu-id="1107c-103">Функция Create Table As Select (CTAS) в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="1107c-103">Create Table As Select (CTAS) in SQL Data Warehouse</span></span>
<span data-ttu-id="1107c-104">Создание таблицы как select или `CTAS` является одним из hello наиболее важные функции T-SQL.</span><span class="sxs-lookup"><span data-stu-id="1107c-104">Create table as select or `CTAS` is one of hello most important T-SQL features available.</span></span> <span data-ttu-id="1107c-105">Это полностью Параллелизованный операцию, которая создает новые таблицы, основанной на hello выходные данные инструкции SELECT.</span><span class="sxs-lookup"><span data-stu-id="1107c-105">It is a fully parallelized operation that creates a new table based on hello output of a SELECT statement.</span></span> <span data-ttu-id="1107c-106">`CTAS`является простым и быстрым способом toocreate hello копии таблицы.</span><span class="sxs-lookup"><span data-stu-id="1107c-106">`CTAS` is hello simplest and fastest way toocreate a copy of a table.</span></span> <span data-ttu-id="1107c-107">Этот документ содержит примеры и рекомендации для `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="1107c-107">This document provides both examples and best practices for `CTAS`.</span></span>

## <a name="selectinto-vs-ctas"></a><span data-ttu-id="1107c-108">Сравнение SELECT..INTO и CTAS;</span><span class="sxs-lookup"><span data-stu-id="1107c-108">SELECT..INTO vs. CTAS</span></span>
<span data-ttu-id="1107c-109">`CTAS` можно рассматривать как сильно расширенную версию `SELECT..INTO`.</span><span class="sxs-lookup"><span data-stu-id="1107c-109">You can consider `CTAS` as a super-charged version of `SELECT..INTO`.</span></span>

<span data-ttu-id="1107c-110">Ниже показан пример простой инструкции `SELECT..INTO`.</span><span class="sxs-lookup"><span data-stu-id="1107c-110">Below is an example of a simple `SELECT..INTO` statement:</span></span>

```sql
SELECT *
INTO    [dbo].[FactInternetSales_new]
FROM    [dbo].[FactInternetSales]
```

<span data-ttu-id="1107c-111">В приведенном выше примере hello `[dbo].[FactInternetSales_new]` будут создаваться как ROUND_ROBIN распределенные таблицы с КЛАСТЕРИЗОВАННЫМ ИНДЕКСОМ COLUMNSTORE в его как hello значения таблиц по умолчанию в хранилище данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="1107c-111">In hello example above `[dbo].[FactInternetSales_new]` would be created as ROUND_ROBIN distributed table with a CLUSTERED COLUMNSTORE INDEX on it as these are hello table defaults in Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="1107c-112">`SELECT..INTO`Однако не позволяет toochange индекс распространения либо hello метода или hello тип как часть операции hello.</span><span class="sxs-lookup"><span data-stu-id="1107c-112">`SELECT..INTO` however does not allow you toochange either hello distribution method or hello index type as part of hello operation.</span></span> <span data-ttu-id="1107c-113">Вот где может пригодиться `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="1107c-113">This is where `CTAS` comes in.</span></span>

<span data-ttu-id="1107c-114">tooconvert hello выше слишком`CTAS` является довольно прост:</span><span class="sxs-lookup"><span data-stu-id="1107c-114">tooconvert hello above too`CTAS` is quite straight-forward:</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_new]
WITH
(
    DISTRIBUTION = ROUND_ROBIN
,   CLUSTERED COLUMNSTORE INDEX
)
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
;
```

<span data-ttu-id="1107c-115">С `CTAS` , может toochange оба hello распространения hello таблицу данных, а также hello табличного типа.</span><span class="sxs-lookup"><span data-stu-id="1107c-115">With `CTAS` you are able toochange both hello distribution of hello table data as well as hello table type.</span></span> 

> [!NOTE]
> <span data-ttu-id="1107c-116">Если только вы пытаетесь toochange hello индекса в вашей `CTAS` операции и hello исходная таблица является хэш распределенных то ваше устройство `CTAS` выполнит операцию лучше, если вы сохраняете hello же распределение столбца и тип данных.</span><span class="sxs-lookup"><span data-stu-id="1107c-116">If you are only trying toochange hello index in your `CTAS` operation and hello source table is hash distributed then your `CTAS` operation will perform best if you maintain hello same distribution column and data type.</span></span> <span data-ttu-id="1107c-117">Это позволит избежать кросс-распространения перемещения данных во время операции hello, что является более эффективным.</span><span class="sxs-lookup"><span data-stu-id="1107c-117">This will avoid cross distribution data movement during hello operation which is more efficient.</span></span>
> 
> 

## <a name="using-ctas-toocopy-a-table"></a><span data-ttu-id="1107c-118">С помощью CTAS toocopy таблицы</span><span class="sxs-lookup"><span data-stu-id="1107c-118">Using CTAS toocopy a table</span></span>
<span data-ttu-id="1107c-119">Может быть одним из наиболее распространенных hello использует `CTAS` является создание копии таблицы, можно изменить hello DDL.</span><span class="sxs-lookup"><span data-stu-id="1107c-119">Perhaps one of hello most common uses of `CTAS` is creating a copy of a table so that you can change hello DDL.</span></span> <span data-ttu-id="1107c-120">Например которые использовались при создании таблицы как `ROUND_ROBIN` и распределенных теперь хотите изменить его tooa таблицы со столбцами, `CTAS` является изменение столбец распределения hello.</span><span class="sxs-lookup"><span data-stu-id="1107c-120">If for example you originally created your table as `ROUND_ROBIN` and now want change it tooa table distributed on a column, `CTAS` is how you would change hello distribution column.</span></span> <span data-ttu-id="1107c-121">`CTAS`также можно использовать toochange секционирование, индексирование или столбец типов.</span><span class="sxs-lookup"><span data-stu-id="1107c-121">`CTAS` can also be used toochange partitioning, indexing, or column types.</span></span>

<span data-ttu-id="1107c-122">Предположим, что вы создали в этой таблице, используя тип распределения по умолчанию hello для `ROUND_ROBIN` распределенных, так как столбец распределения не была указана в hello `CREATE TABLE`.</span><span class="sxs-lookup"><span data-stu-id="1107c-122">Let's say you created this table using hello default distribution type of `ROUND_ROBIN` distributed since no distribution column was specified in hello `CREATE TABLE`.</span></span>

```sql
CREATE TABLE FactInternetSales
(
    ProductKey int NOT NULL,
    OrderDateKey int NOT NULL,
    DueDateKey int NOT NULL,
    ShipDateKey int NOT NULL,
    CustomerKey int NOT NULL,
    PromotionKey int NOT NULL,
    CurrencyKey int NOT NULL,
    SalesTerritoryKey int NOT NULL,
    SalesOrderNumber nvarchar(20) NOT NULL,
    SalesOrderLineNumber tinyint NOT NULL,
    RevisionNumber tinyint NOT NULL,
    OrderQuantity smallint NOT NULL,
    UnitPrice money NOT NULL,
    ExtendedAmount money NOT NULL,
    UnitPriceDiscountPct float NOT NULL,
    DiscountAmount float NOT NULL,
    ProductStandardCost money NOT NULL,
    TotalProductCost money NOT NULL,
    SalesAmount money NOT NULL,
    TaxAmt money NOT NULL,
    Freight money NOT NULL,
    CarrierTrackingNumber nvarchar(25),
    CustomerPONumber nvarchar(25)
);
```

<span data-ttu-id="1107c-123">Теперь требуется toocreate новую копию этой таблицы с кластеризованным индексом Columnstore, чтобы воспользоваться преимуществами hello производительность таблиц Clustered Columnstore.</span><span class="sxs-lookup"><span data-stu-id="1107c-123">Now you want toocreate a new copy of this table with a Clustered Columnstore Index so that you can take advantage of hello performance of Clustered Columnstore tables.</span></span> <span data-ttu-id="1107c-124">Также можно toodistribute этой таблицы по ProductKey с момента планирование соединения по этому столбцу и требуется перемещение данных tooavoid во время соединения, в отношении ProductKey.</span><span class="sxs-lookup"><span data-stu-id="1107c-124">You also want toodistribute this table on ProductKey since you are anticipating joins on this column and want tooavoid data movement during joins on ProductKey.</span></span> <span data-ttu-id="1107c-125">Наконец также требуется tooadd секционирование по OrderDateKey, чтобы быстро старые данные можно удалить, удалив старые секции.</span><span class="sxs-lookup"><span data-stu-id="1107c-125">Lastly you also want tooadd partitioning on OrderDateKey so that you can quickly delete old data by dropping old partitions.</span></span> <span data-ttu-id="1107c-126">Вот hello CTAS инструкцию, которая будет копировать вашей старой таблицы в новую таблицу.</span><span class="sxs-lookup"><span data-stu-id="1107c-126">Here is hello CTAS statement which would copy your old table into a new table.</span></span>

```sql
CREATE TABLE FactInternetSales_new
WITH
(
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = HASH(ProductKey),
    PARTITION
    (
        OrderDateKey RANGE RIGHT FOR VALUES
        (
        20000101,20010101,20020101,20030101,20040101,20050101,20060101,20070101,20080101,20090101,
        20100101,20110101,20120101,20130101,20140101,20150101,20160101,20170101,20180101,20190101,
        20200101,20210101,20220101,20230101,20240101,20250101,20260101,20270101,20280101,20290101
        )
    )
)
AS SELECT * FROM FactInternetSales;
```

<span data-ttu-id="1107c-127">Наконец можно переименовать вашей tooswap таблицы в новую таблицу и затем удалите старый таблицы.</span><span class="sxs-lookup"><span data-stu-id="1107c-127">Finally you can rename your tables tooswap in your new table and then drop your old table.</span></span>

```sql
RENAME OBJECT FactInternetSales tooFactInternetSales_old;
RENAME OBJECT FactInternetSales_new tooFactInternetSales;

DROP TABLE FactInternetSales_old;
```

> [!NOTE]
> <span data-ttu-id="1107c-128">Хранилище данных SQL Azure пока не поддерживает автоматическое создание или автоматическое обновление статистики.</span><span class="sxs-lookup"><span data-stu-id="1107c-128">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="1107c-129">В порядке tooget hello наилучшей производительности запросов очень важно создать статистику для всех столбцов всех таблиц после первой загрузки hello или любые существенные изменения происходят в данных hello.</span><span class="sxs-lookup"><span data-stu-id="1107c-129">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span>  <span data-ttu-id="1107c-130">Подробное описание статистики см. в разделе hello [статистики] [ Statistics] раздела hello разработка группы разделов.</span><span class="sxs-lookup"><span data-stu-id="1107c-130">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span>
> 
> 

## <a name="using-ctas-toowork-around-unsupported-features"></a><span data-ttu-id="1107c-131">С помощью toowork CTAS вокруг неподдерживаемых функций</span><span class="sxs-lookup"><span data-stu-id="1107c-131">Using CTAS toowork around unsupported features</span></span>
<span data-ttu-id="1107c-132">`CTAS`также можно использовать toowork вокруг число перечисленных ниже функций hello не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="1107c-132">`CTAS` can also be used toowork around a number of hello unsupported features listed below.</span></span> <span data-ttu-id="1107c-133">Это может часто доказать toobe ситуации win-win не только код будет соответствующим требованиям, но он будет часто выполняются быстрее в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="1107c-133">This can often prove toobe a win/win situation as not only will your code be compliant but it will often execute faster on SQL Data Warehouse.</span></span> <span data-ttu-id="1107c-134">Это связано с распараллеленной структурой системы.</span><span class="sxs-lookup"><span data-stu-id="1107c-134">This is as a result of its fully parallelized design.</span></span> <span data-ttu-id="1107c-135">Сценарии, которые можно обойти с помощью CTAS:</span><span class="sxs-lookup"><span data-stu-id="1107c-135">Scenarios that can be worked around with CTAS include:</span></span>

* <span data-ttu-id="1107c-136">Синтаксис соединения ANSI с операторами обновления</span><span class="sxs-lookup"><span data-stu-id="1107c-136">ANSI JOINS on UPDATEs</span></span>
* <span data-ttu-id="1107c-137">Синтаксис соединения ANSI с операторами удаления</span><span class="sxs-lookup"><span data-stu-id="1107c-137">ANSI JOINs on DELETEs</span></span>
* <span data-ttu-id="1107c-138">Оператор MERGE</span><span class="sxs-lookup"><span data-stu-id="1107c-138">MERGE statement</span></span>

> [!NOTE]
> <span data-ttu-id="1107c-139">Повторите toothink» CTAS первый».</span><span class="sxs-lookup"><span data-stu-id="1107c-139">Try toothink "CTAS first".</span></span> <span data-ttu-id="1107c-140">Если вы считаете, что может решить проблему с помощью `CTAS` это значение обычно является лучшим способом tooapproach hello его - даже если в результате записи дополнительных данных.</span><span class="sxs-lookup"><span data-stu-id="1107c-140">If you think you can solve a problem using `CTAS` then that is generally hello best way tooapproach it - even if you are writing more data as a result.</span></span>
> 
> 

## <a name="ansi-join-replacement-for-update-statements"></a><span data-ttu-id="1107c-141">Замена синтаксиса соединения ANSI для операторов обновления</span><span class="sxs-lookup"><span data-stu-id="1107c-141">ANSI join replacement for update statements</span></span>
<span data-ttu-id="1107c-142">Вы можете обнаружить, что у вас есть сложные обновление, которое соединяет более двух таблиц, объединенных с помощью присоединения hello tooperform синтаксис ANSI UPDATE или DELETE.</span><span class="sxs-lookup"><span data-stu-id="1107c-142">You may find you have a complex update that joins more than two tables together using ANSI joining syntax tooperform hello UPDATE or DELETE.</span></span>

<span data-ttu-id="1107c-143">Представьте, что вы tooupdate в этой таблице:</span><span class="sxs-lookup"><span data-stu-id="1107c-143">Imagine you had tooupdate this table:</span></span>

```sql
CREATE TABLE [dbo].[AnnualCategorySales]
(    [EnglishProductCategoryName]    NVARCHAR(50)    NOT NULL
,    [CalendarYear]                    SMALLINT        NOT NULL
,    [TotalSalesAmount]                MONEY            NOT NULL
)
WITH
(
    DISTRIBUTION = ROUND_ROBIN
)
;
```

<span data-ttu-id="1107c-144">исходный запрос Hello может выглядел примерно так:</span><span class="sxs-lookup"><span data-stu-id="1107c-144">hello original query might have looked something like this:</span></span>

```sql
UPDATE    acs
SET        [TotalSalesAmount] = [fis].[TotalSalesAmount]
FROM    [dbo].[AnnualCategorySales]     AS acs
JOIN    (
        SELECT    [EnglishProductCategoryName]
        ,        [CalendarYear]
        ,        SUM([SalesAmount])                AS [TotalSalesAmount]
        FROM    [dbo].[FactInternetSales]        AS s
        JOIN    [dbo].[DimDate]                    AS d    ON s.[OrderDateKey]                = d.[DateKey]
        JOIN    [dbo].[DimProduct]                AS p    ON s.[ProductKey]                = p.[ProductKey]
        JOIN    [dbo].[DimProductSubCategory]    AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
        JOIN    [dbo].[DimProductCategory]        AS c    ON u.[ProductCategoryKey]        = c.[ProductCategoryKey]
        WHERE     [CalendarYear] = 2004
        GROUP BY
                [EnglishProductCategoryName]
        ,        [CalendarYear]
        ) AS fis
ON    [acs].[EnglishProductCategoryName]    = [fis].[EnglishProductCategoryName]
AND    [acs].[CalendarYear]                = [fis].[CalendarYear]
;
```

<span data-ttu-id="1107c-145">Поскольку хранилище данных SQL не поддерживает ANSI соединения в hello `FROM` предложения `UPDATE` инструкции, без изменения ее слегка не удается скопировать этот код по.</span><span class="sxs-lookup"><span data-stu-id="1107c-145">Since SQL Data Warehouse does not support ANSI joins in hello `FROM` clause of an `UPDATE` statement, you cannot copy this code over without changing it slightly.</span></span>

<span data-ttu-id="1107c-146">Можно использовать сочетание `CTAS` и неявного соединения tooreplace этот код:</span><span class="sxs-lookup"><span data-stu-id="1107c-146">You can use a combination of a `CTAS` and an implicit join tooreplace this code:</span></span>

```sql
-- Create an interim table
CREATE TABLE CTAS_acs
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT    ISNULL(CAST([EnglishProductCategoryName] AS NVARCHAR(50)),0)    AS [EnglishProductCategoryName]
,        ISNULL(CAST([CalendarYear] AS SMALLINT),0)                         AS [CalendarYear]
,        ISNULL(CAST(SUM([SalesAmount]) AS MONEY),0)                        AS [TotalSalesAmount]
FROM    [dbo].[FactInternetSales]        AS s
JOIN    [dbo].[DimDate]                    AS d    ON s.[OrderDateKey]                = d.[DateKey]
JOIN    [dbo].[DimProduct]                AS p    ON s.[ProductKey]                = p.[ProductKey]
JOIN    [dbo].[DimProductSubCategory]    AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
JOIN    [dbo].[DimProductCategory]        AS c    ON u.[ProductCategoryKey]        = c.[ProductCategoryKey]
WHERE     [CalendarYear] = 2004
GROUP BY
        [EnglishProductCategoryName]
,        [CalendarYear]
;

-- Use an implicit join tooperform hello update
UPDATE  AnnualCategorySales
SET     AnnualCategorySales.TotalSalesAmount = CTAS_ACS.TotalSalesAmount
FROM    CTAS_acs
WHERE   CTAS_acs.[EnglishProductCategoryName] = AnnualCategorySales.[EnglishProductCategoryName]
AND     CTAS_acs.[CalendarYear]               = AnnualCategorySales.[CalendarYear]
;

--Drop hello interim table
DROP TABLE CTAS_acs
;
```

## <a name="ansi-join-replacement-for-delete-statements"></a><span data-ttu-id="1107c-147">Замена синтаксиса соединения ANSI для операторов удаления</span><span class="sxs-lookup"><span data-stu-id="1107c-147">ANSI join replacement for delete statements</span></span>
<span data-ttu-id="1107c-148">Иногда hello для удаления данных лучше toouse `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="1107c-148">Sometimes hello best approach for deleting data is toouse `CTAS`.</span></span> <span data-ttu-id="1107c-149">Вместо удаления данных hello, просто выберите hello данные tookeep.</span><span class="sxs-lookup"><span data-stu-id="1107c-149">Rather than deleting hello data simply select hello data you want tookeep.</span></span> <span data-ttu-id="1107c-150">Это особенно верно для `DELETE` инструкции, использующие объединение синтаксиса, так как хранилище данных SQL не поддерживает соединения ANSI в hello ansi `FROM` предложения `DELETE` инструкции.</span><span class="sxs-lookup"><span data-stu-id="1107c-150">This especially true for `DELETE` statements that use ansi joining syntax since SQL Data Warehouse does not support ANSI joins in hello `FROM` clause of a `DELETE` statement.</span></span>

<span data-ttu-id="1107c-151">Пример преобразованного оператора DELETE:</span><span class="sxs-lookup"><span data-stu-id="1107c-151">An example of a converted DELETE statement is available below:</span></span>

```sql
CREATE TABLE dbo.DimProduct_upsert
WITH
(   Distribution=HASH(ProductKey)
,   CLUSTERED INDEX (ProductKey)
)
AS -- Select Data you wish tookeep
SELECT     p.ProductKey
,          p.EnglishProductName
,          p.Color
FROM       dbo.DimProduct p
RIGHT JOIN dbo.stg_DimProduct s
ON         p.ProductKey = s.ProductKey
;

RENAME OBJECT dbo.DimProduct        tooDimProduct_old;
RENAME OBJECT dbo.DimProduct_upsert tooDimProduct;
```

## <a name="replace-merge-statements"></a><span data-ttu-id="1107c-152">Замена операторов объединения</span><span class="sxs-lookup"><span data-stu-id="1107c-152">Replace merge statements</span></span>
<span data-ttu-id="1107c-153">Функция `CTAS`может (по крайней мере частично) заменить операторы объединения.</span><span class="sxs-lookup"><span data-stu-id="1107c-153">Merge statements can be replaced, at least in part, by using `CTAS`.</span></span> <span data-ttu-id="1107c-154">Можно объединять hello `INSERT` и hello `UPDATE` в один оператор.</span><span class="sxs-lookup"><span data-stu-id="1107c-154">You can consolidate hello `INSERT` and hello `UPDATE` into a single statement.</span></span> <span data-ttu-id="1107c-155">Удаленные записи, должны toobe закрытие в еще одну инструкцию.</span><span class="sxs-lookup"><span data-stu-id="1107c-155">Any deleted records would need toobe closed off in a second statement.</span></span>

<span data-ttu-id="1107c-156">Пример оператора `UPSERT` :</span><span class="sxs-lookup"><span data-stu-id="1107c-156">An example of an `UPSERT` is available below:</span></span>

```sql
CREATE TABLE dbo.[DimProduct_upsert]
WITH
(   DISTRIBUTION = HASH([ProductKey])
,   CLUSTERED INDEX ([ProductKey])
)
AS
-- New rows and new versions of rows
SELECT      s.[ProductKey]
,           s.[EnglishProductName]
,           s.[Color]
FROM      dbo.[stg_DimProduct] AS s
UNION ALL  
-- Keep rows that are not being touched
SELECT      p.[ProductKey]
,           p.[EnglishProductName]
,           p.[Color]
FROM      dbo.[DimProduct] AS p
WHERE NOT EXISTS
(   SELECT  *
    FROM    [dbo].[stg_DimProduct] s
    WHERE   s.[ProductKey] = p.[ProductKey]
)
;

RENAME OBJECT dbo.[DimProduct]          too[DimProduct_old];
RENAME OBJECT dbo.[DimpProduct_upsert]  too[DimProduct];

```

## <a name="ctas-recommendation-explicitly-state-data-type-and-nullability-of-output"></a><span data-ttu-id="1107c-157">Рекомендация по использованию функции CTAS: прямо указывайте тип данных и допустимость нулевого результата</span><span class="sxs-lookup"><span data-stu-id="1107c-157">CTAS recommendation: Explicitly state data type and nullability of output</span></span>
<span data-ttu-id="1107c-158">При переносе кода вы можете встретить следующую схему кодовой комбинации:</span><span class="sxs-lookup"><span data-stu-id="1107c-158">When migrating code you might find you run across this type of coding pattern:</span></span>

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE result
(result DECIMAL(7,2) NOT NULL
)
WITH (DISTRIBUTION = ROUND_ROBIN)

INSERT INTO result
SELECT @d*@f
;
```

<span data-ttu-id="1107c-159">Instinctively вы думаете, необходимо перенести этот код tooa CTAS, и они будут правильно.</span><span class="sxs-lookup"><span data-stu-id="1107c-159">Instinctively you might think you should migrate this code tooa CTAS and you would be correct.</span></span> <span data-ttu-id="1107c-160">При этом нужно помнить о подводных камнях.</span><span class="sxs-lookup"><span data-stu-id="1107c-160">However, there is a hidden issue here.</span></span>

<span data-ttu-id="1107c-161">Hello следующий код не дает hello одинаковый результат:</span><span class="sxs-lookup"><span data-stu-id="1107c-161">hello following code does NOT yield hello same result:</span></span>

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455
;

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT @d*@f as result
;
```

<span data-ttu-id="1107c-162">Обратите внимание, hello столбец «результат» вперед выполняет hello тип и допустимость значений NULL значения данных hello выражения.</span><span class="sxs-lookup"><span data-stu-id="1107c-162">Notice that hello column "result" carries forward hello data type and nullability values of hello expression.</span></span> <span data-ttu-id="1107c-163">Это может привести toosubtle дисперсии значений следует соблюдать осторожность.</span><span class="sxs-lookup"><span data-stu-id="1107c-163">This can lead toosubtle variances in values if you aren't careful.</span></span>

<span data-ttu-id="1107c-164">Попробуйте выполните следующие hello в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="1107c-164">Try hello following as an example:</span></span>

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

<span data-ttu-id="1107c-165">Hello значение для результата — другой.</span><span class="sxs-lookup"><span data-stu-id="1107c-165">hello value stored for result is different.</span></span> <span data-ttu-id="1107c-166">Hello сохраненное значение в столбце hello результат используется в других выражениях hello ошибки становится еще более значительные.</span><span class="sxs-lookup"><span data-stu-id="1107c-166">As hello persisted value in hello result column is used in other expressions hello error becomes even more significant.</span></span>

![][1]

<span data-ttu-id="1107c-167">Это особенно важно при переносе данных.</span><span class="sxs-lookup"><span data-stu-id="1107c-167">This is particularly important for data migrations.</span></span> <span data-ttu-id="1107c-168">Несмотря на то, что второй запрос hello пожалуй точнее имеется проблема.</span><span class="sxs-lookup"><span data-stu-id="1107c-168">Even though hello second query is arguably more accurate there is a problem.</span></span> <span data-ttu-id="1107c-169">Hello данные будут содержать разные сравниваемых toohello исходной системы, и это ведет tooquestions целостности hello миграции.</span><span class="sxs-lookup"><span data-stu-id="1107c-169">hello data would be different compared toohello source system and that leads tooquestions of integrity in hello migration.</span></span> <span data-ttu-id="1107c-170">Это один из тех редких случаях, где фактически hello вправо на один ответ «неправильный» hello!</span><span class="sxs-lookup"><span data-stu-id="1107c-170">This is one of those rare cases where hello "wrong" answer is actually hello right one!</span></span>

<span data-ttu-id="1107c-171">Hello причине, мы увидим это несоответствие между двумя hello результаты не работает tooimplicit приведение типов.</span><span class="sxs-lookup"><span data-stu-id="1107c-171">hello reason we see this disparity between hello two results is down tooimplicit type casting.</span></span> <span data-ttu-id="1107c-172">Первый пример hello таблицы hello определяет hello определения столбца.</span><span class="sxs-lookup"><span data-stu-id="1107c-172">In hello first example hello table defines hello column definition.</span></span> <span data-ttu-id="1107c-173">При вставке строки hello происходит неявное преобразование типов.</span><span class="sxs-lookup"><span data-stu-id="1107c-173">When hello row is inserted an implicit type conversion occurs.</span></span> <span data-ttu-id="1107c-174">В втором примере hello нет не неявное преобразование типов как hello выражение определяет тип данных столбца hello.</span><span class="sxs-lookup"><span data-stu-id="1107c-174">In hello second example there is no implicit type conversion as hello expression defines data type of hello column.</span></span> <span data-ttu-id="1107c-175">Обратите внимание также этим столбцом hello в hello во втором примере был определен как столбец допускает значения NULL, тогда как в первом примере hello не установлена.</span><span class="sxs-lookup"><span data-stu-id="1107c-175">Notice also that hello column in hello second example has been defined as a NULLable column whereas in hello first example it has not.</span></span> <span data-ttu-id="1107c-176">При создании таблицы hello в hello первый пример столбца возможности содержать значения NULL явно определен.</span><span class="sxs-lookup"><span data-stu-id="1107c-176">When hello table was created in hello first example column nullability was explicitly defined.</span></span> <span data-ttu-id="1107c-177">В втором примере hello он был оставить toohello выражение и по умолчанию в результате определением NULL.</span><span class="sxs-lookup"><span data-stu-id="1107c-177">In hello second example it was just left toohello expression and by default this would result in a NULL definition.</span></span>  

<span data-ttu-id="1107c-178">tooresolve этих проблем, необходимо явно задать преобразование типа hello и допустимость значений NULL в hello `SELECT` часть hello `CTAS` инструкции.</span><span class="sxs-lookup"><span data-stu-id="1107c-178">tooresolve these issues you must explicitly set hello type conversion and nullability in hello `SELECT` portion of hello `CTAS` statement.</span></span> <span data-ttu-id="1107c-179">Невозможно задать свойства в hello создают таблицы частей.</span><span class="sxs-lookup"><span data-stu-id="1107c-179">You cannot set these properties in hello create table part.</span></span>

<span data-ttu-id="1107c-180">Приведенный ниже пример Hello показывает, как toofix hello кода:</span><span class="sxs-lookup"><span data-stu-id="1107c-180">hello example below demonstrates how toofix hello code:</span></span>

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

<span data-ttu-id="1107c-181">Обратите внимание hello следующие:</span><span class="sxs-lookup"><span data-stu-id="1107c-181">Note hello following:</span></span>

* <span data-ttu-id="1107c-182">Можно было использовать CAST или CONVERT.</span><span class="sxs-lookup"><span data-stu-id="1107c-182">CAST or CONVERT could have been used</span></span>
* <span data-ttu-id="1107c-183">ISNULL — используется tooforce допустимость значений NULL не COALESCE</span><span class="sxs-lookup"><span data-stu-id="1107c-183">ISNULL is used tooforce NULLability not COALESCE</span></span>
* <span data-ttu-id="1107c-184">Функция ISNULL является внешней функции hello</span><span class="sxs-lookup"><span data-stu-id="1107c-184">ISNULL is hello outermost function</span></span>
* <span data-ttu-id="1107c-185">во второй части Hello hello ISNULL является константой т. е. 0</span><span class="sxs-lookup"><span data-stu-id="1107c-185">hello second part of hello ISNULL is a constant i.e. 0</span></span>

> [!NOTE]
> <span data-ttu-id="1107c-186">Для его правильно установить toobe hello допустимость значений NULL является жизненно важных toouse `ISNULL` и не `COALESCE`.</span><span class="sxs-lookup"><span data-stu-id="1107c-186">For hello nullability toobe correctly set it is vital toouse `ISNULL` and not `COALESCE`.</span></span> <span data-ttu-id="1107c-187">`COALESCE`не является детерминированной функции и поэтому hello результат выражения hello всегда будет иметь значения NULL.</span><span class="sxs-lookup"><span data-stu-id="1107c-187">`COALESCE` is not a deterministic function and so hello result of hello expression will always be NULLable.</span></span> <span data-ttu-id="1107c-188">`ISNULL` действует иначе.</span><span class="sxs-lookup"><span data-stu-id="1107c-188">`ISNULL` is different.</span></span> <span data-ttu-id="1107c-189">Он детерминирован,</span><span class="sxs-lookup"><span data-stu-id="1107c-189">It is deterministic.</span></span> <span data-ttu-id="1107c-190">Поэтому при hello во второй части hello `ISNULL` функции является константой или литералом, то будет hello результирующее значение NOT NULL.</span><span class="sxs-lookup"><span data-stu-id="1107c-190">Therefore when hello second part of hello `ISNULL` function is a constant or a literal then hello resulting value will be NOT NULL.</span></span>
> 
> 

<span data-ttu-id="1107c-191">Этот совет не просто нужно, чтобы гарантировать целостность hello вычисления.</span><span class="sxs-lookup"><span data-stu-id="1107c-191">This tip is not just useful for ensuring hello integrity of your calculations.</span></span> <span data-ttu-id="1107c-192">но и играет важную роль в переключении между разделами таблицы.</span><span class="sxs-lookup"><span data-stu-id="1107c-192">It is also important for table partition switching.</span></span> <span data-ttu-id="1107c-193">Предположим, эта таблица определена как факт:</span><span class="sxs-lookup"><span data-stu-id="1107c-193">Imagine you have this table defined as your fact:</span></span>

```sql
CREATE TABLE [dbo].[Sales]
(
    [date]      INT     NOT NULL
,   [product]   INT     NOT NULL
,   [store]     INT     NOT NULL
,   [quantity]  INT     NOT NULL
,   [price]     MONEY   NOT NULL
,   [amount]    MONEY   NOT NULL
)
WITH
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101,20020101
                    ,20030101,20040101,20050101
                    )
                )
)
;
```

<span data-ttu-id="1107c-194">Поле значения hello то, вычисляемое выражение не является частью hello исходных данных.</span><span class="sxs-lookup"><span data-stu-id="1107c-194">However, hello value field is a calculated expression it is not part of hello source data.</span></span>

<span data-ttu-id="1107c-195">toocreate секционированных набор данных может потребоваться toodo это:</span><span class="sxs-lookup"><span data-stu-id="1107c-195">toocreate your partitioned dataset you might want toodo this:</span></span>

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   [quantity]*[price]  AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create')
;
```

<span data-ttu-id="1107c-196">Hello запрос будет выполняться в полном порядке.</span><span class="sxs-lookup"><span data-stu-id="1107c-196">hello query would run perfectly fine.</span></span> <span data-ttu-id="1107c-197">Hello проблема возникает при попытке переключения секций tooperform hello.</span><span class="sxs-lookup"><span data-stu-id="1107c-197">hello problem comes when you try tooperform hello partition switch.</span></span> <span data-ttu-id="1107c-198">определения таблиц Hello не совпадают.</span><span class="sxs-lookup"><span data-stu-id="1107c-198">hello table definitions do not match.</span></span> <span data-ttu-id="1107c-199">определения таблиц hello toomake соответствует CTAS требуется изменить toobe hello.</span><span class="sxs-lookup"><span data-stu-id="1107c-199">toomake hello table definitions match hello CTAS needs toobe modified.</span></span>

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   ISNULL(CAST([quantity]*[price] AS MONEY),0) AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create');
```

<span data-ttu-id="1107c-200">Таким образом, можно сказать, что соблюдать единство типов данных и контролировать свойства допустимости нулевых значений в CTAS всегда полезно.</span><span class="sxs-lookup"><span data-stu-id="1107c-200">You can see therefore that type consistency and maintaining nullability properties on a CTAS is a good engineering best practice.</span></span> <span data-ttu-id="1107c-201">Это поможет toomaintain целостности в вычислениях и также гарантирует, что переключение секций невозможно.</span><span class="sxs-lookup"><span data-stu-id="1107c-201">It helps toomaintain integrity in your calculations and also ensures that partition switching is possible.</span></span>

<span data-ttu-id="1107c-202">См. Дополнительные сведения об использовании tooMSDN [CTAS][CTAS].</span><span class="sxs-lookup"><span data-stu-id="1107c-202">Please refer tooMSDN for more information on using [CTAS][CTAS].</span></span> <span data-ttu-id="1107c-203">Он является одним из наиболее важных инструкций hello в хранилище данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="1107c-203">It is one of hello most important statements in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="1107c-204">Научитесь его применять.</span><span class="sxs-lookup"><span data-stu-id="1107c-204">Make sure you thoroughly understand it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1107c-205">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1107c-205">Next steps</span></span>
<span data-ttu-id="1107c-206">Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][development overview].</span><span class="sxs-lookup"><span data-stu-id="1107c-206">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-ctas/ctas-results.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[CTAS]: https://msdn.microsoft.com/library/mt204041.aspx

<!--Other Web references-->
