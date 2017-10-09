---
title: "aaaGroup с параметрами в хранилище данных SQL | Документы Microsoft"
description: "Советы по реализации параметров предложения Group By в хранилище данных SQL Azure для разработки решений."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: f95a1e43-768f-4b7b-8a10-8a0509d0c871
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: cc443c2af4e3ef2babd74d78aa6fb57bb3c1c7ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="group-by-options-in-sql-data-warehouse"></a><span data-ttu-id="42e23-103">Группировка по параметрам в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="42e23-103">Group by options in SQL Data Warehouse</span></span>
<span data-ttu-id="42e23-104">Hello [GROUP BY] [ GROUP BY] используется предложение tooaggregate данных tooa сводки набора строк.</span><span class="sxs-lookup"><span data-stu-id="42e23-104">hello [GROUP BY][GROUP BY] clause is used tooaggregate data tooa summary set of rows.</span></span> <span data-ttu-id="42e23-105">Он также имеет ряд возможностей, расширения его функциональных возможностей, toobe необходимость альтернативное решение, поскольку они не поддерживаются напрямую в хранилище данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="42e23-105">It also has a few options that extend it's functionality that need toobe worked around as they are not directly supported by Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="42e23-106">Доступны следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="42e23-106">These options are</span></span>

* <span data-ttu-id="42e23-107">GROUP BY с ROLLUP;</span><span class="sxs-lookup"><span data-stu-id="42e23-107">GROUP BY with ROLLUP</span></span>
* <span data-ttu-id="42e23-108">GROUPING SETS;</span><span class="sxs-lookup"><span data-stu-id="42e23-108">GROUPING SETS</span></span>
* <span data-ttu-id="42e23-109">GROUP BY с CUBE.</span><span class="sxs-lookup"><span data-stu-id="42e23-109">GROUP BY with CUBE</span></span>

## <a name="rollup-and-grouping-sets-options"></a><span data-ttu-id="42e23-110">Параметры Rollup и Grouping Sets</span><span class="sxs-lookup"><span data-stu-id="42e23-110">Rollup and grouping sets options</span></span>
<span data-ttu-id="42e23-111">Hello здесь простой вариант — toouse `UNION ALL` вместо tooperform hello свертки, а не полагаться на hello явный синтаксис.</span><span class="sxs-lookup"><span data-stu-id="42e23-111">hello simplest option here is toouse `UNION ALL` instead tooperform hello rollup rather than relying on hello explicit syntax.</span></span> <span data-ttu-id="42e23-112">результат Hello точно hello же</span><span class="sxs-lookup"><span data-stu-id="42e23-112">hello result is exactly hello same</span></span>

<span data-ttu-id="42e23-113">Ниже приведен пример group by инструкции с помощью hello `ROLLUP` параметр:</span><span class="sxs-lookup"><span data-stu-id="42e23-113">Below is an example of a group by statement using hello `ROLLUP` option:</span></span>

```sql
SELECT [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
,      SUM(SalesAmount)             AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t       ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY ROLLUP (
                        [SalesTerritoryCountry]
                ,       [SalesTerritoryRegion]
                )
;
```

<span data-ttu-id="42e23-114">С помощью СВЕРТКИ запросили hello следующие статистические выражения:</span><span class="sxs-lookup"><span data-stu-id="42e23-114">By using ROLLUP we have requested hello following aggregations:</span></span>

* <span data-ttu-id="42e23-115">Страна и регион</span><span class="sxs-lookup"><span data-stu-id="42e23-115">Country and Region</span></span>
* <span data-ttu-id="42e23-116">Страна</span><span class="sxs-lookup"><span data-stu-id="42e23-116">Country</span></span>
* <span data-ttu-id="42e23-117">Общий итог</span><span class="sxs-lookup"><span data-stu-id="42e23-117">Grand Total</span></span>

<span data-ttu-id="42e23-118">tooreplace это потребуется toouse `UNION ALL`; указание hello агрегатов требуется явно tooreturn hello такие же результаты:</span><span class="sxs-lookup"><span data-stu-id="42e23-118">tooreplace this you will need toouse `UNION ALL`; specifying hello aggregations required explicitly tooreturn hello same results:</span></span>

```sql
SELECT [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY
       [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
UNION ALL
SELECT [SalesTerritoryCountry]
,      NULL
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY
       [SalesTerritoryCountry]
UNION ALL
SELECT NULL
,      NULL
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey;
```

<span data-ttu-id="42e23-119">Для hello же основной GROUPING SETS, нам нужно toodo всего применять, но создать ОБЪЕДИНЕНИЕ всех разделов для hello только уровни статистической обработки, мы хотим toosee</span><span class="sxs-lookup"><span data-stu-id="42e23-119">For GROUPING SETS all we need toodo is adopt hello same principal but only create UNION ALL sections for hello aggregation levels we want toosee</span></span>

## <a name="cube-options"></a><span data-ttu-id="42e23-120">Параметры Cube</span><span class="sxs-lookup"><span data-stu-id="42e23-120">Cube options</span></span>
<span data-ttu-id="42e23-121">Это возможно toocreate GROUP BY WITH CUBE с помощью UNION ALL подход hello.</span><span class="sxs-lookup"><span data-stu-id="42e23-121">It is possible toocreate a GROUP BY WITH CUBE using hello UNION ALL approach.</span></span> <span data-ttu-id="42e23-122">Hello проблема заключается в том, что код hello может быстро стать сложной и неудобной и.</span><span class="sxs-lookup"><span data-stu-id="42e23-122">hello problem is that hello code can quickly become cumbersome and unwieldy.</span></span> <span data-ttu-id="42e23-123">toomitigate это эту функцию можно использовать несколько дополнительных подход.</span><span class="sxs-lookup"><span data-stu-id="42e23-123">toomitigate this you can use this more advanced approach.</span></span>

<span data-ttu-id="42e23-124">Воспользуемся приведенном выше примере hello.</span><span class="sxs-lookup"><span data-stu-id="42e23-124">Let's use hello example above.</span></span>

<span data-ttu-id="42e23-125">Первым шагом Hello — toodefine hello «куба», который определяет все уровни статистической обработки, что мы хотим toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="42e23-125">hello first step is toodefine hello 'cube' that defines all hello levels of aggregation that we want toocreate.</span></span> <span data-ttu-id="42e23-126">Это важные tootake внимание hello CROSS JOIN hello два производных таблиц.</span><span class="sxs-lookup"><span data-stu-id="42e23-126">It is important tootake note of hello CROSS JOIN of hello two derived tables.</span></span> <span data-ttu-id="42e23-127">Это приводит к возникновению ошибки все уровни hello нам.</span><span class="sxs-lookup"><span data-stu-id="42e23-127">This generates all hello levels for us.</span></span> <span data-ttu-id="42e23-128">Hello остальной части кода hello есть действительно для форматирования.</span><span class="sxs-lookup"><span data-stu-id="42e23-128">hello rest of hello code is really there for formatting.</span></span>

```sql
CREATE TABLE #Cube
WITH
(   DISTRIBUTION = ROUND_ROBIN
,   LOCATION = USER_DB
)
AS
WITH GrpCube AS
(SELECT    CAST(ISNULL(Country,'NULL')+','+ISNULL(Region,'NULL') AS NVARCHAR(50)) as 'Cols'
,          CAST(ISNULL(Country+',','')+ISNULL(Region,'') AS NVARCHAR(50))  as 'GroupBy'
,          ROW_NUMBER() OVER (ORDER BY Country) as 'Seq'
FROM       ( SELECT 'SalesTerritoryCountry' as Country
             UNION ALL
             SELECT NULL
           ) c
CROSS JOIN ( SELECT 'SalesTerritoryRegion' as Region
             UNION ALL
             SELECT NULL
           ) r
)
SELECT Cols
,      CASE WHEN SUBSTRING(GroupBy,LEN(GroupBy),1) = ','
            THEN SUBSTRING(GroupBy,1,LEN(GroupBy)-1)
            ELSE GroupBy
       END AS GroupBy  --Remove Trailing Comma
,Seq
FROM GrpCube;
```

<span data-ttu-id="42e23-129">результаты Hello hello CTAS приводятся ниже:</span><span class="sxs-lookup"><span data-stu-id="42e23-129">hello results of hello CTAS can be seen below:</span></span>

![][1]

<span data-ttu-id="42e23-130">второй шаг Hello — toospecify, промежуточная toostore целевой таблицы результатов:</span><span class="sxs-lookup"><span data-stu-id="42e23-130">hello second step is toospecify a target table toostore interim results:</span></span>

```sql
DECLARE
 @SQL NVARCHAR(4000)
,@Columns NVARCHAR(4000)
,@GroupBy NVARCHAR(4000)
,@i INT = 1
,@nbr INT = 0
;
CREATE TABLE #Results
(
 [SalesTerritoryCountry] NVARCHAR(50)
,[SalesTerritoryRegion]  NVARCHAR(50)
,[TotalSalesAmount]      MONEY
)
WITH
(   DISTRIBUTION = ROUND_ROBIN
,   LOCATION = USER_DB
)
;
```

<span data-ttu-id="42e23-131">Третий шаг Hello — tooloop на нашем кубе столбцов при выполнении статистической функции hello.</span><span class="sxs-lookup"><span data-stu-id="42e23-131">hello third step is tooloop over our cube of columns performing hello aggregation.</span></span> <span data-ttu-id="42e23-132">Hello запроса будет запустить один раз для каждой строки в hello #Cube временной таблицы и хранения результатов hello во временной таблице hello #Results</span><span class="sxs-lookup"><span data-stu-id="42e23-132">hello query will run once for every row in hello #Cube temporary table and store hello results in hello #Results temp table</span></span>

```sql
SET @nbr =(SELECT MAX(Seq) FROM #Cube);

WHILE @i<=@nbr
BEGIN
    SET @Columns = (SELECT Cols    FROM #Cube where seq = @i);
    SET @GroupBy = (SELECT GroupBy FROM #Cube where seq = @i);

    SET @SQL ='INSERT INTO #Results
              SELECT '+@Columns+'
              ,      SUM(SalesAmount) AS TotalSalesAmount
              FROM  dbo.factInternetSales s
              JOIN  dbo.DimSalesTerritory t  
              ON s.SalesTerritoryKey = t.SalesTerritoryKey
              '+CASE WHEN @GroupBy <>''
                     THEN 'GROUP BY '+@GroupBy ELSE '' END

    EXEC sp_executesql @SQL;
    SET @i +=1;
END
```

<span data-ttu-id="42e23-133">Наконец может возвращать результаты hello, просто считывая из временной таблицы hello #Results</span><span class="sxs-lookup"><span data-stu-id="42e23-133">Lastly we can return hello results by simply reading from hello #Results temporary table</span></span>

```sql
SELECT *
FROM #Results
ORDER BY 1,2,3
;
```

<span data-ttu-id="42e23-134">Разбиении на разделы кода hello и создания цикла hello конструкция кода становится управляемость и простым в обслуживании.</span><span class="sxs-lookup"><span data-stu-id="42e23-134">By breaking hello code up into sections and generating a looping construct hello code becomes more manageable and maintainable.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42e23-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="42e23-135">Next steps</span></span>
<span data-ttu-id="42e23-136">Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][development overview].</span><span class="sxs-lookup"><span data-stu-id="42e23-136">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-group-by-options/sql-data-warehouse-develop-group-by-cube.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[GROUP BY]: https://msdn.microsoft.com/library/ms177673.aspx


<!--Other Web references-->
