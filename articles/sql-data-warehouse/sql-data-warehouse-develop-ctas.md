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
# <a name="create-table-as-select-ctas-in-sql-data-warehouse"></a>Функция Create Table As Select (CTAS) в хранилище данных SQL
Создание таблицы как select или `CTAS` является одним из hello наиболее важные функции T-SQL. Это полностью Параллелизованный операцию, которая создает новые таблицы, основанной на hello выходные данные инструкции SELECT. `CTAS`является простым и быстрым способом toocreate hello копии таблицы. Этот документ содержит примеры и рекомендации для `CTAS`.

## <a name="selectinto-vs-ctas"></a>Сравнение SELECT..INTO и CTAS;
`CTAS` можно рассматривать как сильно расширенную версию `SELECT..INTO`.

Ниже показан пример простой инструкции `SELECT..INTO`.

```sql
SELECT *
INTO    [dbo].[FactInternetSales_new]
FROM    [dbo].[FactInternetSales]
```

В приведенном выше примере hello `[dbo].[FactInternetSales_new]` будут создаваться как ROUND_ROBIN распределенные таблицы с КЛАСТЕРИЗОВАННЫМ ИНДЕКСОМ COLUMNSTORE в его как hello значения таблиц по умолчанию в хранилище данных SQL Azure.

`SELECT..INTO`Однако не позволяет toochange индекс распространения либо hello метода или hello тип как часть операции hello. Вот где может пригодиться `CTAS`.

tooconvert hello выше слишком`CTAS` является довольно прост:

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

С `CTAS` , может toochange оба hello распространения hello таблицу данных, а также hello табличного типа. 

> [!NOTE]
> Если только вы пытаетесь toochange hello индекса в вашей `CTAS` операции и hello исходная таблица является хэш распределенных то ваше устройство `CTAS` выполнит операцию лучше, если вы сохраняете hello же распределение столбца и тип данных. Это позволит избежать кросс-распространения перемещения данных во время операции hello, что является более эффективным.
> 
> 

## <a name="using-ctas-toocopy-a-table"></a>С помощью CTAS toocopy таблицы
Может быть одним из наиболее распространенных hello использует `CTAS` является создание копии таблицы, можно изменить hello DDL. Например которые использовались при создании таблицы как `ROUND_ROBIN` и распределенных теперь хотите изменить его tooa таблицы со столбцами, `CTAS` является изменение столбец распределения hello. `CTAS`также можно использовать toochange секционирование, индексирование или столбец типов.

Предположим, что вы создали в этой таблице, используя тип распределения по умолчанию hello для `ROUND_ROBIN` распределенных, так как столбец распределения не была указана в hello `CREATE TABLE`.

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

Теперь требуется toocreate новую копию этой таблицы с кластеризованным индексом Columnstore, чтобы воспользоваться преимуществами hello производительность таблиц Clustered Columnstore. Также можно toodistribute этой таблицы по ProductKey с момента планирование соединения по этому столбцу и требуется перемещение данных tooavoid во время соединения, в отношении ProductKey. Наконец также требуется tooadd секционирование по OrderDateKey, чтобы быстро старые данные можно удалить, удалив старые секции. Вот hello CTAS инструкцию, которая будет копировать вашей старой таблицы в новую таблицу.

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

Наконец можно переименовать вашей tooswap таблицы в новую таблицу и затем удалите старый таблицы.

```sql
RENAME OBJECT FactInternetSales tooFactInternetSales_old;
RENAME OBJECT FactInternetSales_new tooFactInternetSales;

DROP TABLE FactInternetSales_old;
```

> [!NOTE]
> Хранилище данных SQL Azure пока не поддерживает автоматическое создание или автоматическое обновление статистики.  В порядке tooget hello наилучшей производительности запросов очень важно создать статистику для всех столбцов всех таблиц после первой загрузки hello или любые существенные изменения происходят в данных hello.  Подробное описание статистики см. в разделе hello [статистики] [ Statistics] раздела hello разработка группы разделов.
> 
> 

## <a name="using-ctas-toowork-around-unsupported-features"></a>С помощью toowork CTAS вокруг неподдерживаемых функций
`CTAS`также можно использовать toowork вокруг число перечисленных ниже функций hello не поддерживается. Это может часто доказать toobe ситуации win-win не только код будет соответствующим требованиям, но он будет часто выполняются быстрее в хранилище данных SQL. Это связано с распараллеленной структурой системы. Сценарии, которые можно обойти с помощью CTAS:

* Синтаксис соединения ANSI с операторами обновления
* Синтаксис соединения ANSI с операторами удаления
* Оператор MERGE

> [!NOTE]
> Повторите toothink» CTAS первый». Если вы считаете, что может решить проблему с помощью `CTAS` это значение обычно является лучшим способом tooapproach hello его - даже если в результате записи дополнительных данных.
> 
> 

## <a name="ansi-join-replacement-for-update-statements"></a>Замена синтаксиса соединения ANSI для операторов обновления
Вы можете обнаружить, что у вас есть сложные обновление, которое соединяет более двух таблиц, объединенных с помощью присоединения hello tooperform синтаксис ANSI UPDATE или DELETE.

Представьте, что вы tooupdate в этой таблице:

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

исходный запрос Hello может выглядел примерно так:

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

Поскольку хранилище данных SQL не поддерживает ANSI соединения в hello `FROM` предложения `UPDATE` инструкции, без изменения ее слегка не удается скопировать этот код по.

Можно использовать сочетание `CTAS` и неявного соединения tooreplace этот код:

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

## <a name="ansi-join-replacement-for-delete-statements"></a>Замена синтаксиса соединения ANSI для операторов удаления
Иногда hello для удаления данных лучше toouse `CTAS`. Вместо удаления данных hello, просто выберите hello данные tookeep. Это особенно верно для `DELETE` инструкции, использующие объединение синтаксиса, так как хранилище данных SQL не поддерживает соединения ANSI в hello ansi `FROM` предложения `DELETE` инструкции.

Пример преобразованного оператора DELETE:

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

## <a name="replace-merge-statements"></a>Замена операторов объединения
Функция `CTAS`может (по крайней мере частично) заменить операторы объединения. Можно объединять hello `INSERT` и hello `UPDATE` в один оператор. Удаленные записи, должны toobe закрытие в еще одну инструкцию.

Пример оператора `UPSERT` :

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

## <a name="ctas-recommendation-explicitly-state-data-type-and-nullability-of-output"></a>Рекомендация по использованию функции CTAS: прямо указывайте тип данных и допустимость нулевого результата
При переносе кода вы можете встретить следующую схему кодовой комбинации:

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

Instinctively вы думаете, необходимо перенести этот код tooa CTAS, и они будут правильно. При этом нужно помнить о подводных камнях.

Hello следующий код не дает hello одинаковый результат:

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

Обратите внимание, hello столбец «результат» вперед выполняет hello тип и допустимость значений NULL значения данных hello выражения. Это может привести toosubtle дисперсии значений следует соблюдать осторожность.

Попробуйте выполните следующие hello в качестве примера.

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

Hello значение для результата — другой. Hello сохраненное значение в столбце hello результат используется в других выражениях hello ошибки становится еще более значительные.

![][1]

Это особенно важно при переносе данных. Несмотря на то, что второй запрос hello пожалуй точнее имеется проблема. Hello данные будут содержать разные сравниваемых toohello исходной системы, и это ведет tooquestions целостности hello миграции. Это один из тех редких случаях, где фактически hello вправо на один ответ «неправильный» hello!

Hello причине, мы увидим это несоответствие между двумя hello результаты не работает tooimplicit приведение типов. Первый пример hello таблицы hello определяет hello определения столбца. При вставке строки hello происходит неявное преобразование типов. В втором примере hello нет не неявное преобразование типов как hello выражение определяет тип данных столбца hello. Обратите внимание также этим столбцом hello в hello во втором примере был определен как столбец допускает значения NULL, тогда как в первом примере hello не установлена. При создании таблицы hello в hello первый пример столбца возможности содержать значения NULL явно определен. В втором примере hello он был оставить toohello выражение и по умолчанию в результате определением NULL.  

tooresolve этих проблем, необходимо явно задать преобразование типа hello и допустимость значений NULL в hello `SELECT` часть hello `CTAS` инструкции. Невозможно задать свойства в hello создают таблицы частей.

Приведенный ниже пример Hello показывает, как toofix hello кода:

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

Обратите внимание hello следующие:

* Можно было использовать CAST или CONVERT.
* ISNULL — используется tooforce допустимость значений NULL не COALESCE
* Функция ISNULL является внешней функции hello
* во второй части Hello hello ISNULL является константой т. е. 0

> [!NOTE]
> Для его правильно установить toobe hello допустимость значений NULL является жизненно важных toouse `ISNULL` и не `COALESCE`. `COALESCE`не является детерминированной функции и поэтому hello результат выражения hello всегда будет иметь значения NULL. `ISNULL` действует иначе. Он детерминирован, Поэтому при hello во второй части hello `ISNULL` функции является константой или литералом, то будет hello результирующее значение NOT NULL.
> 
> 

Этот совет не просто нужно, чтобы гарантировать целостность hello вычисления. но и играет важную роль в переключении между разделами таблицы. Предположим, эта таблица определена как факт:

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

Поле значения hello то, вычисляемое выражение не является частью hello исходных данных.

toocreate секционированных набор данных может потребоваться toodo это:

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

Hello запрос будет выполняться в полном порядке. Hello проблема возникает при попытке переключения секций tooperform hello. определения таблиц Hello не совпадают. определения таблиц hello toomake соответствует CTAS требуется изменить toobe hello.

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

Таким образом, можно сказать, что соблюдать единство типов данных и контролировать свойства допустимости нулевых значений в CTAS всегда полезно. Это поможет toomaintain целостности в вычислениях и также гарантирует, что переключение секций невозможно.

См. Дополнительные сведения об использовании tooMSDN [CTAS][CTAS]. Он является одним из наиболее важных инструкций hello в хранилище данных SQL Azure. Научитесь его применять.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][development overview].

<!--Image references-->
[1]: media/sql-data-warehouse-develop-ctas/ctas-results.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[CTAS]: https://msdn.microsoft.com/library/mt204041.aspx

<!--Other Web references-->
