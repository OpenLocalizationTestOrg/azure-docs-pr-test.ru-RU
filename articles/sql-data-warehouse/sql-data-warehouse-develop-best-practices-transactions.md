---
title: "транзакции aaaOptimizing для хранилища данных SQL | Документы Microsoft"
description: "В этой статье вы найдете рекомендации по написанию эффективного кода для обновлений транзакций в хранилище данных SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 6f326f26-8a54-49df-a482-9c96a58db371
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 1a821161711db9460b7e10d3cf7ba498d711448b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="optimizing-transactions-for-sql-data-warehouse"></a>Оптимизация транзакций для хранилища данных SQL
В этой статье объясняется, как toooptimize hello производительность свести к минимуму риск long откатов транзакций кода.

## <a name="transactions-and-logging"></a>Транзакции и ведение журнала
Транзакции представляют собой важную часть ядра реляционной СУБД. Хранилище данных SQL использует транзакции во время изменения данных. Эти транзакции могут быть явными или неявными. Одиночные инструкции `INSERT`, `UPDATE` и `DELETE` являются примерами неявных транзакций. Явные транзакции написанных вручную разработчиком с помощью `BEGIN TRAN`, `COMMIT TRAN` или `ROLLBACK TRAN` и обычно используются, когда несколько инструкций модификации необходимость toobe связаны друг с другом в одну атомарную операцию. 

Хранилище данных SQL Azure фиксирует изменения базы данных toohello с помощью журналов транзакций. У каждого распределения есть свой журнал транзакций. Запись в журналы транзакций выполняется автоматически. Настраивать что-либо не требуется. Тем не менее хотя этот процесс гарантирует hello записи его в системе hello вводится дополнительная нагрузка. Чтобы минимизировать этот эффект, нужно написать эффективный код транзакции. Такой код можно условно разделить на две категории.

* Используйте конструкции минимального ведения журналов, когда это возможно.
* Обработка данных с использованием заданной области пакетов единственного числа tooavoid долго выполняющихся транзакций
* Использовать шаблон для заданного раздела tooa больших изменений переключение секции

## <a name="minimal-vs-full-logging"></a>Минимальное ведение журнала и полное ведение журнала
В отличие от полной регистрацией в журнале операций, использующих hello журнала транзакций tookeep отслеживать все изменения строк, отслеживать связи операции с минимальным протоколированием размещением экстента и только изменения метаданных. Таким образом, минимальное протоколирование — это протоколирование только информации hello, требуется toorollback hello в транзакции hello события сбоя или явный запрос (`ROLLBACK TRAN`). Как гораздо меньше сведения отслеживаются в журнале транзакций hello, операции с минимальной регистрацией выполняет лучше, чем операции работают с полным протоколированием одинакового размера. Кроме того так как меньшее количество операций записи журнала транзакций hello, создается много меньший объем данных журнала и поэтому дополнительные операции ввода-вывода эффективен.

ограничения безопасности транзакций Hello применяются только toofully в журнал операций.

> [!NOTE]
> Минимально регистрируемые операции могут быть частью явных транзакций. Как отслеживаются все изменения структуры распределения, возможные tooroll назад это как минимум в журнал операций. Очень важно toounderstand, изменение hello «как минимум» войти, он не не регистрируется.
> 
> 

## <a name="minimally-logged-operations"></a>Минимально регистрируемые операции
Hello следующие операции способны выполняется с минимальным протоколированием:

* Инструкция CREATE TABLE AS SELECT ([CTAS][CTAS])
* INSERT..SELECT
* CREATE INDEX
* ALTER INDEX REBUILD
* DROP INDEX
* TRUNCATE TABLE
* DROP TABLE
* ALTER TABLE SWITCH PARTITION

<!--
- MERGE
- UPDATE on LOB Types .WRITE
- SELECT..INTO
-->

> [!NOTE]
> Операции перемещения внутренние данные (такие как `BROADCAST` и `SHUFFLE`) не подвержены лимита безопасности транзакций hello.
> 
> 

## <a name="minimal-logging-with-bulk-load"></a>Минимальное ведение журнала и массовая загрузка
`CTAS` и `INSERT...SELECT` — это операции массовой загрузки. Тем не менее оба влияют определение таблицы целевой hello и зависят от сценария нагрузки hello. В таблице, приведенной ниже, перечислены условия, в зависимости от которых ваша массовая операция будет регистрироваться полностью или минимально.  

| Первичный индекс | Сценарий загрузки | Режим ведения журнала |
| --- | --- | --- |
| Куча |Любой |**Минимальный** |
| Кластеризованный индекс |Пустая целевая таблица |**Минимальный** |
| Кластеризованный индекс |Загруженные строки не перекрывают существующие страницы в целевом объекте |**Минимальный** |
| Кластеризованный индекс |Загруженные строки перекрывают существующие страницы в целевом объекте |Полное |
| Кластеризованный индекс columnstore |Размер пакета >= 102 400 для распределения с выравниванием по разделам |**Минимальный** |
| Кластеризованный индекс columnstore |Размер пакета < 102 400 для распределения с выравниванием по разделам |Полное |

Стоит отметить, что запись tooupdate получателей или некластеризованных индексов будет всегда полностью зарегистрированных операций.

> [!IMPORTANT]
> В хранилище данных SQL есть 60 распределений. Таким образом при условии, что все строки равномерно распределяются целевой в одной секции, пакет должен toocontain 6,144,000 строк или больше toobe как минимум записанных в журнал при записи tooa кластеризованный индекс Columnstore. Если hello таблица секционирована и hello строк, вставляемых span границы секций, потребуется 6,144,000 строк на границу секции, при условии, что равномерное распределение данных. Каждая секция в каждом распространения независимо друг от друга должно превышать hello 102 400 строк пороговое значение с минимальным протоколированием в распространения hello toobe вставки hello.
> 
> 

При загрузке данных в непустую таблицу с кластеризованным индексом некоторые строки могут быть полностью регистрируемыми, а некоторые — минимально. Кластеризованный индекс — это сбалансированное дерево страниц. Если страница hello записываемых tooalready содержит строки из другой транзакции, затем эти записи полностью заносятся. Тем не менее если пустая страница hello затем hello записи toothat страницы будет возможно минимальное протоколирование.

## <a name="optimizing-deletes"></a>Оптимизация операций удаления
`DELETE` является полностью регистрируемой.  Если вам требуется toodelete большой объем данных в таблице или секции, часто смысл слишком`SELECT` hello данных нужно tookeep, которая может выполняться как операция с минимальной регистрацией.  tooaccomplish это, создайте новую таблицу с [CTAS][CTAS].  После создания с помощью [ПЕРЕИМЕНОВАНИЕ] [ RENAME] tooswap out вашей старой таблицы с таблицей вновь созданные hello.

```sql
-- Delete all sales transactions for Promotions except PromotionKey 2.

--Step 01. Create a new table select only hello records we want tookep (PromotionKey 2)
CREATE TABLE [dbo].[FactInternetSales_d]
WITH
(    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([ProductKey])
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20000101, 20010101, 20020101, 20030101, 20040101, 20050101
                                                ,    20060101, 20070101, 20080101, 20090101, 20100101, 20110101
                                                ,    20120101, 20130101, 20140101, 20150101, 20160101, 20170101
                                                ,    20180101, 20190101, 20200101, 20210101, 20220101, 20230101
                                                ,    20240101, 20250101, 20260101, 20270101, 20280101, 20290101
                                                )
)
AS
SELECT     *
FROM     [dbo].[FactInternetSales]
WHERE    [PromotionKey] = 2
OPTION (LABEL = 'CTAS : Delete')
;

--Step 02. Rename hello Tables tooreplace hello 
RENAME OBJECT [dbo].[FactInternetSales]   too[FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_d] too[FactInternetSales];
```

## <a name="optimizing-updates"></a>Оптимизация операций обновления
`UPDATE` является полностью регистрируемой.  Если необходимо, чтобы tooupdate большое количество строк в таблице или секции часто может оказаться гораздо более эффективно toouse операция с минимальной регистрацией, например [CTAS] [ CTAS] toodo так.

В hello в примере выполняется обновление всей таблицы был преобразованный tooa `CTAS` таким образом, возможно минимальное протоколирование.

В этом случае мы retrospectively добавляем продажи toohello сумма скидки в таблице hello:

```sql
--Step 01. Create a new table containing hello "Update". 
CREATE TABLE [dbo].[FactInternetSales_u]
WITH
(    CLUSTERED INDEX
,    DISTRIBUTION = HASH([ProductKey])
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20000101, 20010101, 20020101, 20030101, 20040101, 20050101
                                                ,    20060101, 20070101, 20080101, 20090101, 20100101, 20110101
                                                ,    20120101, 20130101, 20140101, 20150101, 20160101, 20170101
                                                ,    20180101, 20190101, 20200101, 20210101, 20220101, 20230101
                                                ,    20240101, 20250101, 20260101, 20270101, 20280101, 20290101
                                                )
                )
)
AS 
SELECT
    [ProductKey]  
,    [OrderDateKey] 
,    [DueDateKey]  
,    [ShipDateKey] 
,    [CustomerKey] 
,    [PromotionKey] 
,    [CurrencyKey] 
,    [SalesTerritoryKey]
,    [SalesOrderNumber]
,    [SalesOrderLineNumber]
,    [RevisionNumber]
,    [OrderQuantity]
,    [UnitPrice]
,    [ExtendedAmount]
,    [UnitPriceDiscountPct]
,    ISNULL(CAST(5 as float),0) AS [DiscountAmount]
,    [ProductStandardCost]
,    [TotalProductCost]
,    ISNULL(CAST(CASE WHEN [SalesAmount] <=5 THEN 0
         ELSE [SalesAmount] - 5
         END AS MONEY),0) AS [SalesAmount]
,    [TaxAmt]
,    [Freight]
,    [CarrierTrackingNumber] 
,    [CustomerPONumber]
FROM    [dbo].[FactInternetSales]
OPTION (LABEL = 'CTAS : Update')
;

--Step 02. Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales]   too[FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_u] too[FactInternetSales];

--Step 03. Drop hello old table
DROP TABLE [dbo].[FactInternetSales_old]
```

> [!NOTE]
> Повторное создание больших таблиц может быть удобнее, если использовать функции управления рабочими нагрузками хранилища данных SQL. Для сведения см. в раздел управления toohello рабочей нагрузки в hello [параллелизма] [ concurrency] статьи.
> 
> 

## <a name="optimizing-with-partition-switching"></a>Оптимизация с помощью переключения секций
Если вы столкнулись с крупномасштабными изменениями в [секции таблицы][table partition], то имеет смысл воспользоваться схемой переключения секций. Если hello значительные изменения данных и обеспечивает несколько секций, а затем просто перебора hello секций диапазоны hello того же результата.

Ниже приведены действия Hello tooperform переключения секций.

1. Создайте пустой выходной раздел.
2. Выполнить обновление «hello» как CTAS
3. Исходящего hello существующих данных toohello таблица исходящего переключения
4. Переключитесь в новых данных hello
5. Очистка данных hello

Однако toohelp идентификации tooswitch секций hello, будет необходимо сначала toobuild вспомогательную процедуру, например hello один ниже. 

```sql
CREATE PROCEDURE dbo.partition_data_get
    @schema_name           NVARCHAR(128)
,    @table_name               NVARCHAR(128)
,    @boundary_value           INT
AS
IF OBJECT_ID('tempdb..#ptn_data') IS NOT NULL
BEGIN
    DROP TABLE #ptn_data
END
CREATE TABLE #ptn_data
WITH    (    DISTRIBUTION = ROUND_ROBIN
        ,    HEAP
        )
AS
WITH CTE
AS
(
SELECT     s.name                            AS [schema_name]
,        t.name                            AS [table_name]
,         p.partition_number                AS [ptn_nmbr]
,        p.[rows]                        AS [ptn_rows]
,        CAST(r.[value] AS INT)            AS [boundary_value]
FROM        sys.schemas                    AS s
JOIN        sys.tables                    AS t    ON  s.[schema_id]        = t.[schema_id]
JOIN        sys.indexes                    AS i    ON     t.[object_id]        = i.[object_id]
JOIN        sys.partitions                AS p    ON     i.[object_id]        = p.[object_id] 
                                                AND i.[index_id]        = p.[index_id] 
JOIN        sys.partition_schemes        AS h    ON     i.[data_space_id]    = h.[data_space_id]
JOIN        sys.partition_functions        AS f    ON     h.[function_id]        = f.[function_id]
LEFT JOIN    sys.partition_range_values    AS r     ON     f.[function_id]        = r.[function_id] 
                                                AND r.[boundary_id]        = p.[partition_number]
WHERE i.[index_id] <= 1
)
SELECT    *
FROM    CTE
WHERE    [schema_name]        = @schema_name
AND        [table_name]        = @table_name
AND        [boundary_value]    = @boundary_value
OPTION (LABEL = 'dbo.partition_data_get : CTAS : #ptn_data')
;
GO
```

Эта процедура позволяет максимально увеличить повторное использование кода и отслеживает переключения более компактным пример hello секций.

Приведенный ниже код Hello демонстрируется пять шагов hello вышеупомянутых tooachieve полной секции переключение подпрограмму.

```sql
--Create a partitioned aligned empty table tooswitch out hello data 
IF OBJECT_ID('[dbo].[FactInternetSales_out]') IS NOT NULL
BEGIN
    DROP TABLE [dbo].[FactInternetSales_out]
END

CREATE TABLE [dbo].[FactInternetSales_out]
WITH
(    DISTRIBUTION = HASH([ProductKey])
,    CLUSTERED COLUMNSTORE INDEX
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20020101, 20030101
                                                )
                )
)
AS
SELECT *
FROM    [dbo].[FactInternetSales]
WHERE 1=2
OPTION (LABEL = 'CTAS : Partition Switch IN : UPDATE')
;

--Create a partitioned aligned table and update hello data in hello select portion of hello CTAS
IF OBJECT_ID('[dbo].[FactInternetSales_in]') IS NOT NULL
BEGIN
    DROP TABLE [dbo].[FactInternetSales_in]
END

CREATE TABLE [dbo].[FactInternetSales_in]
WITH
(    DISTRIBUTION = HASH([ProductKey])
,    CLUSTERED COLUMNSTORE INDEX
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20020101, 20030101
                                                )
                )
)
AS 
SELECT
    [ProductKey]  
,    [OrderDateKey] 
,    [DueDateKey]  
,    [ShipDateKey] 
,    [CustomerKey] 
,    [PromotionKey] 
,    [CurrencyKey] 
,    [SalesTerritoryKey]
,    [SalesOrderNumber]
,    [SalesOrderLineNumber]
,    [RevisionNumber]
,    [OrderQuantity]
,    [UnitPrice]
,    [ExtendedAmount]
,    [UnitPriceDiscountPct]
,    ISNULL(CAST(5 as float),0) AS [DiscountAmount]
,    [ProductStandardCost]
,    [TotalProductCost]
,    ISNULL(CAST(CASE WHEN [SalesAmount] <=5 THEN 0
         ELSE [SalesAmount] - 5
         END AS MONEY),0) AS [SalesAmount]
,    [TaxAmt]
,    [Freight]
,    [CarrierTrackingNumber] 
,    [CustomerPONumber]
FROM    [dbo].[FactInternetSales]
WHERE    OrderDateKey BETWEEN 20020101 AND 20021231
OPTION (LABEL = 'CTAS : Partition Switch IN : UPDATE')
;

--Use hello helper procedure tooidentify hello partitions
--hello source table
EXEC dbo.partition_data_get 'dbo','FactInternetSales',20030101
DECLARE @ptn_nmbr_src INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_src

--hello "in" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_in',20030101
DECLARE @ptn_nmbr_in INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_in

--hello "out" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_out',20030101
DECLARE @ptn_nmbr_out INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_out

--Switch hello partitions over
DECLARE @SQL NVARCHAR(4000) = '
ALTER TABLE [dbo].[FactInternetSales]    SWITCH PARTITION '+CAST(@ptn_nmbr_src AS VARCHAR(20))    +' too[dbo].[FactInternetSales_out] PARTITION '    +CAST(@ptn_nmbr_out AS VARCHAR(20))+';
ALTER TABLE [dbo].[FactInternetSales_in] SWITCH PARTITION '+CAST(@ptn_nmbr_in AS VARCHAR(20))    +' too[dbo].[FactInternetSales] PARTITION '        +CAST(@ptn_nmbr_src AS VARCHAR(20))+';'
EXEC sp_executesql @SQL

--Perform hello clean-up
TRUNCATE TABLE dbo.FactInternetSales_out;
TRUNCATE TABLE dbo.FactInternetSales_in;

DROP TABLE dbo.FactInternetSales_out
DROP TABLE dbo.FactInternetSales_in
DROP TABLE #ptn_data
```

## <a name="minimize-logging-with-small-batches"></a>Сведение к минимуму ведения журнала с помощью небольших пакетов
Для операций модификации данных большого объема может быть смысле toodivide hello операция в блок hello tooscope блоков или пакетов.

Ниже приведен рабочий пример. размер пакета Hello задал tooa тривиальные номеров toohighlight hello прием. В реальности размер пакета hello бы значительно больше. 

```sql
SET NO_COUNT ON;
IF OBJECT_ID('tempdb..#t') IS NOT NULL
BEGIN
    DROP TABLE #t;
    PRINT '#t dropped';
END

CREATE TABLE #t
WITH    (    DISTRIBUTION = ROUND_ROBIN
        ,    HEAP
        )
AS
SELECT    ROW_NUMBER() OVER(ORDER BY (SELECT NULL)) AS seq_nmbr
,        SalesOrderNumber
,        SalesOrderLineNumber
FROM    dbo.FactInternetSales
WHERE    [OrderDateKey] BETWEEN 20010101 and 20011231
;

DECLARE    @seq_start        INT = 1
,        @batch_iterator    INT = 1
,        @batch_size        INT = 50
,        @max_seq_nmbr    INT = (SELECT MAX(seq_nmbr) FROM dbo.#t)
;

DECLARE    @batch_count    INT = (SELECT CEILING((@max_seq_nmbr*1.0)/@batch_size))
,        @seq_end        INT = @batch_size
;

SELECT COUNT(*)
FROM    dbo.FactInternetSales f

PRINT 'MAX_seq_nmbr '+CAST(@max_seq_nmbr AS VARCHAR(20))
PRINT 'MAX_Batch_count '+CAST(@batch_count AS VARCHAR(20))

WHILE    @batch_iterator <= @batch_count
BEGIN
    DELETE
    FROM    dbo.FactInternetSales
    WHERE EXISTS
    (
            SELECT    1
            FROM    #t t
            WHERE    seq_nmbr BETWEEN  @seq_start AND @seq_end
            AND        FactInternetSales.SalesOrderNumber        = t.SalesOrderNumber
            AND        FactInternetSales.SalesOrderLineNumber    = t.SalesOrderLineNumber
    )
    ;

    SET @seq_start = @seq_end
    SET @seq_end = (@seq_start+@batch_size);
    SET @batch_iterator +=1;
END
```

## <a name="pause-and-scaling-guidance"></a>Рекомендации по приостановке и масштабированию
Работу хранилища данных SQL Azure можно по запросу приостановить или возобновить. Также его можно масштабировать. При приостановке или масштабировать хранилище данных SQL является важным toounderstand, что все транзакции на лету прекращаются немедленно; вызывает любой toobe открытых транзакций выполнен откат. Если рабочей нагрузки выдан длительные и неполные данные изменения предыдущих toohello приостановить или операции масштабирования, а затем эта работа потребуется toobe отменено. Это может повлиять на время hello toopause или масштабирование базы данных хранилища данных SQL Azure. 

> [!IMPORTANT]
> `UPDATE` и `DELETE` — это полностью регистрируемые операции, поэтому упомянутые операции отмены и повтора могут выполняться значительно дольше, чем такие же минимально регистрируемые операции. 
> 
> 

Hello наилучшего сценария toolet находится в полете данных изменения транзакций завершения предыдущего toopausing или масштабирования хранилища данных SQL. Однако это не всегда удобно. риск hello toomitigate long отката, можно воспользоваться hello следующие параметры.

* Измените долго выполняющиеся операции, используя [CTAS][CTAS].
* Операция hello разделяются на блоки. работать с подмножеством строк hello

## <a name="next-steps"></a>Дальнейшие действия
В разделе [транзакций в хранилище данных SQL] [ Transactions in SQL Data Warehouse] toolearn дополнительные уровни изоляции и лимиты транзакций.  Рекомендации по использованию хранилища данных SQL Azure см. в статье [Рекомендации по использованию хранилища данных SQL Azure][SQL Data Warehouse Best Practices].

<!--Image references-->

<!--Article references-->
[Transactions in SQL Data Warehouse]: ./sql-data-warehouse-develop-transactions.md
[table partition]: ./sql-data-warehouse-tables-partition.md
[Concurrency]: ./sql-data-warehouse-develop-concurrency.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->
[alter index]:https://msdn.microsoft.com/library/ms188388.aspx
[RENAME]: https://msdn.microsoft.com/library/mt631611.aspx

<!-- Other web references -->

