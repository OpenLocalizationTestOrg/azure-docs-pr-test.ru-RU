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
# <a name="group-by-options-in-sql-data-warehouse"></a>Группировка по параметрам в хранилище данных SQL
Hello [GROUP BY] [ GROUP BY] используется предложение tooaggregate данных tooa сводки набора строк. Он также имеет ряд возможностей, расширения его функциональных возможностей, toobe необходимость альтернативное решение, поскольку они не поддерживаются напрямую в хранилище данных SQL Azure.

Доступны следующие параметры:

* GROUP BY с ROLLUP;
* GROUPING SETS;
* GROUP BY с CUBE.

## <a name="rollup-and-grouping-sets-options"></a>Параметры Rollup и Grouping Sets
Hello здесь простой вариант — toouse `UNION ALL` вместо tooperform hello свертки, а не полагаться на hello явный синтаксис. результат Hello точно hello же

Ниже приведен пример group by инструкции с помощью hello `ROLLUP` параметр:

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

С помощью СВЕРТКИ запросили hello следующие статистические выражения:

* Страна и регион
* Страна
* Общий итог

tooreplace это потребуется toouse `UNION ALL`; указание hello агрегатов требуется явно tooreturn hello такие же результаты:

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

Для hello же основной GROUPING SETS, нам нужно toodo всего применять, но создать ОБЪЕДИНЕНИЕ всех разделов для hello только уровни статистической обработки, мы хотим toosee

## <a name="cube-options"></a>Параметры Cube
Это возможно toocreate GROUP BY WITH CUBE с помощью UNION ALL подход hello. Hello проблема заключается в том, что код hello может быстро стать сложной и неудобной и. toomitigate это эту функцию можно использовать несколько дополнительных подход.

Воспользуемся приведенном выше примере hello.

Первым шагом Hello — toodefine hello «куба», который определяет все уровни статистической обработки, что мы хотим toocreate hello. Это важные tootake внимание hello CROSS JOIN hello два производных таблиц. Это приводит к возникновению ошибки все уровни hello нам. Hello остальной части кода hello есть действительно для форматирования.

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

результаты Hello hello CTAS приводятся ниже:

![][1]

второй шаг Hello — toospecify, промежуточная toostore целевой таблицы результатов:

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

Третий шаг Hello — tooloop на нашем кубе столбцов при выполнении статистической функции hello. Hello запроса будет запустить один раз для каждой строки в hello #Cube временной таблицы и хранения результатов hello во временной таблице hello #Results

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

Наконец может возвращать результаты hello, просто считывая из временной таблицы hello #Results

```sql
SELECT *
FROM #Results
ORDER BY 1,2,3
;
```

Разбиении на разделы кода hello и создания цикла hello конструкция кода становится управляемость и простым в обслуживании.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][development overview].

<!--Image references-->
[1]: media/sql-data-warehouse-develop-group-by-options/sql-data-warehouse-develop-group-by-cube.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[GROUP BY]: https://msdn.microsoft.com/library/ms177673.aspx


<!--Other Web references-->
