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
# <a name="partitioning-tables-in-sql-data-warehouse"></a>Секционирование таблиц в хранилище данных SQL
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

Секционирование поддерживается для всех типов таблиц хранилища данных SQL, включая таблицы с кластеризованным индексом Columnstore, кластеризованным индексом и кучу.  Секционирование также поддерживается для всех типов распределения, включая распределение с помощью хэша или методом циклического перебора.  Секционирование позволяет toodivide копирования данных на более мелкие группы данных и в большинстве случаев секционирования для столбца дат.

## <a name="benefits-of-partitioning"></a>Преимущества секционирования
Секционирование позволяет упростить операции обслуживания данных и повысить производительность запросов.  Он использует оба или только один зависит способ загрузки данных и ли hello же столбец может использоваться для обоих назначений, поскольку секционирование можно выполнить только по одному столбцу.

### <a name="benefits-tooloads"></a>Преимущества tooloads
Hello основным преимуществом секционирования в хранилище данных SQL улучшить hello эффективность и производительность загрузка данных с помощью удаления секции, переключения и объединение.  В большинстве случаев секционирования данных на дату столбца, который является тесно связаны toohello последовательности, какие данные hello — загрузить toohello база данных.  Одним из преимуществ Наибольшее hello с использованием секций toomaintain данных он hello Необязательность использования ведение журнала транзакций.  Хотя просто Вставка, обновление или удаление данных могут быть наиболее простой подход hello с небольшой размышления и трудозатрат, используя секционирование во время процесса загрузки может значительно повысить производительность.

Переключение секций может быть используется tooquickly удалить или заменить раздела таблицы.  Например таблица фактов может содержать только данные для hello последние 36 месяцев.  В конце каждого месяца hello hello старые месяца с данными продаж удаляется из таблицы hello.  Эти данные может быть удалена с помощью данных hello toodelete инструкции delete для hello старые месяца.  Однако удаление большого объема данных по строкам с инструкцией delete может занять очень много времени, а также создать риск hello большие транзакции, это может занять длительное время toorollback, если что-то пойдет не так.  Более Оптимальный подход — toosimply drop hello старой секции данных.  Когда удаление отдельных строк hello может занять часов, удалив весь раздел может потребоваться секунд.

### <a name="benefits-tooqueries"></a>Преимущества tooqueries
Секционирование также можно использовать tooimprove производительность запросов.  Если запрос применяет фильтр на столбец секционирования, это может ограничить hello сканирования tooonly hello уточнения разделов, которые могут быть намного меньше, подмножества данных hello, как избежать полное сканирование таблицы.  С появлением hello кластеризованные индексы columnstore выигрыш в производительности предиката исключения hello менее полезной, но в некоторых случаях может быть tooqueries преимущество.  Например если таблица фактов hello секционируется на 36 месяцев, с помощью поля Дата продажи hello, затем запросов, которые фильтруют на Дата продажи hello можно пропустить поиска в секциях, которые не соответствуют значению фильтра hello.

## <a name="partition-sizing-guidance"></a>Руководство по определению размеров секции
Во время секционирования может быть производительности используется tooimprove некоторые сценарии, создание таблицы с **слишком много** секций может вызвать снижение производительности при некоторых обстоятельствах.  В частности, это свойственно для таблиц с кластеризированными индексами Columnstore.  Для секционирования toobe полезно, это важно toounderstand при toouse секционирования и hello количество секций toocreate.  Существует правило не жестких быстрого как toohow большого числа секций слишком много, зависит от данных и сколько секций загрузке toosimultaneously.  Но, как правило, представить Добавление десятках too100s секций не тысячах.

При создании разделов на **кластеризованном** таблиц, является важным tooconsider, сколько строк будут перемещаться в каждой секции.  Для оптимального сжатия и производительности таких таблиц требуется как минимум 1 миллион строк на одно распределение и одну секцию.  Еще до создания секций хранилище данных SQL делит каждую таблицу на 60 распределенных баз данных.  Любой секционирования таблицы добавлены tooa — Кроме toohello распределения, созданные в фоновом hello.  В этом примере, если таблица фактов hello содержится 36 ежемесячными секциями и учитывая, что хранилище данных SQL имеет 60 распределения hello фактов продаж, что таблица должна содержать 60 миллионов строк в месяц или 2.1 миллиарда строк после заполнения всех месяцев.  Если таблица содержит значительно меньше строк, чем hello Рекомендуемое минимальное число строк на каждую секцию, рассмотрите возможность использования меньше секций в порядке toomake увеличение hello количество строк в секции.  См. также hello [индексирования] [ Index] статьи, включая запросы, которые могут быть запущены на хранилище данных SQL tooassess hello качество индексов columnstore кластера.

## <a name="syntax-difference-from-sql-server"></a>Отличие синтаксиса от SQL Server
В хранилище данных SQL применяется упрощенное определение секций, которое несколько отличается от аналогичного определения в SQL Server.  В хранилище данных SQL функции и схемы секционирования используются не так, как в SQL Server.  Вместо этого все что нужно toodo — определения секционированного точек границ столбец и hello.  Хотя синтаксис hello секционирования может быть немного отличается от SQL Server, являются hello же основные понятия hello.  В SQL Server и хранилище данных SQL поддерживается по одному секционированному столбцу на таблицу, которую можно секционировать по диапазонам.  toolearn Дополнительные сведения о секционировании, в разделе [секционированных таблиц и индексов][Partitioned Tables and Indexes].

Hello ниже примером секционированы хранилища данных SQL [CREATE TABLE] [ CREATE TABLE] инструкции, секции таблицы FactInternetSales hello по столбцу OrderDateKey hello:

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

## <a name="migrating-partitioning-from-sql-server"></a>Перенос секционирования из SQL Server
SQL Server toomigrate просто секционировать tooSQL определения хранилища данных.

* Исключить hello SQL Server [схемы секционирования][partition scheme].
* Добавить hello [функция секционирования] [ partition function] tooyour определение создать ТАБЛИЦУ.

При переносе секционированной таблицы из типа hello экземпляр SQL Server под SQL, чтобы toointerrogate hello количество строк в каждой секции.  Имейте в виду, что hello одинаковую гранулярность секционирования при использовании в хранилище данных SQL, hello количество строк в секции приведет к уменьшению вдвое 60.  

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

## <a name="workload-management"></a>Управление рабочей нагрузкой
— Один toofactor рассмотрения завершающего элемента в решение секции таблицы toohello [управления рабочей нагрузкой][workload management].  Управление рабочими нагрузками в хранилище данных SQL — в первую очередь hello управление памяти и параллелизма.  В хранилище данных SQL hello максимальный объем памяти, выделенной tooeach распространения во время выполнения запроса является классов управляемых ресурсов.  В идеале секций будет изменяться размер буферная таких факторов, как hello памяти, необходимой построение кластеризованных индексов.  Кластеризованные индексы Columnstore наиболее эффективны, когда для них выделяется больший объем памяти.  Таким образом необходимо вернуть tooensure, перестройте индекс секции не испытывает существенной нехватки памяти. Увеличение hello объем памяти, доступной tooyour запроса достигается путем переключения из роли по умолчанию hello, smallrc, tooone из других ролей, таких как largerc "hello".

Сведения на hello выделения памяти для каждого распространителя можно найти с помощью запроса представления динамического управления регулятора ресурсов hello. На самом деле на предоставление памяти будет меньше hello рисунках. Информация приведена на уровне рекомендации, ее можно использовать при планировании размера секций для операций управления данными.  Попробуйте tooavoid изменение размера секций после предоставления памяти hello, предоставляемый классом долгосрочного ресурсов hello. Если увеличение секций на рисунке запуском риск hello свободной памяти, что в свою очередь ведет оптимальное сжатие сборки.

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

## <a name="partition-switching"></a>Переключение секций
Хранилище данных SQL поддерживает разбиение, слияние и переключение секций. Каждая из этих функций — с помощью hello excuted [ALTER TABLE] [ ALTER TABLE] инструкции.

tooswitch секций между двумя таблицами, необходимо убедиться, что секции hello выровнены по их соответствующих границ и соответствуют hello определения таблиц. Проверочные ограничения не являются доступными tooenforce hello диапазона значений в таблице hello исходной таблицы должен содержать hello же секции границы как hello целевой таблицы. Если это не так hello, hello переключение секции завершится ошибкой, hello метаданных секции не будут синхронизированы.

### <a name="how-toosplit-a-partition-that-contains-data"></a>Как toosplit секцию, которая содержит данные
Hello наиболее эффективный метод toosplit секцию, которая уже содержит данные — toouse `CTAS` инструкции. Если кластеризованный индекс columnstore секционированной таблицы hello затем hello таблицы секция должна быть пустой, прежде чем она может быть разбита.

Ниже приведен пример секционированной таблицы columnstore, содержащей по одной строке в каждой секции:

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
> По объекту статистики Создание hello мы убедитесь, что является более точной метаданные этой таблицы. Если пропустить создание объекта статистики, хранилище данных SQL будет использовать значения по умолчанию. Сведения об управлении статистикой таблиц в хранилище данных SQL см. в [этой статье][statistics].
> 
> 

Затем мы можете запрашивать hello количество строк, с помощью hello `sys.partitions` представления каталога:

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

Если мы попытаемся toosplit этой таблицы, возникает ошибка:

```sql
ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

Msg 35346 уровень 15, состояние 1, строку 44 РАЗДЕЛИТЬ предложением инструкции ALTER PARTITION сбой hello секция не пуста.  Только пустые секции могут быть разбиты в, если существует индекс columnstore в таблице hello. Рекомендуется отключить индекс columnstore hello перед выполнения инструкции ALTER PARTITION hello, а перестроение индекса columnstore hello после завершения инструкции ALTER PARTITION.

Тем не менее, мы используем `CTAS` toocreate новый toohold таблицы данных.

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

Выровненный границы секций hello разрешается переключателя. Пустая секция, мы впоследствии можно разделить, оставлять hello исходной таблицы.

```sql
ALTER TABLE FactInternetSales SWITCH PARTITION 2 too FactInternetSales_20000101 PARTITION 2;

ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

Все, что остается toodo — tooalign toohello наши данные секции новые границы, используя `CTAS` и переключитесь обратно в основной таблице toohello наши данные

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

После завершения перемещения hello hello данных является хорошей идеей toorefresh hello статистики на hello целевой таблицы tooensure они точно отражают hello новый распределение данных hello в их соответствующие разделы:

```sql
UPDATE STATISTICS [dbo].[FactInternetSales];
```

### <a name="table-partitioning-source-control"></a>Система управления версиями секционирования таблиц
tooavoid определение таблицы из **ржавчина** в системе управления версиями можно tooconsider hello следующий подход:

1. Создать hello таблицы как секционированной таблицы, но без значений секционирования

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

1. `SPLIT`Таблица Hello в рамках процесса развертывания hello:

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

С этого подхода hello кода в системе управления версиями остается статические и hello секционирования граничных значений допускаются toobe динамического; развиваться с хранилищем hello со временем.

## <a name="next-steps"></a>Дальнейшие действия
toolearn более, статьях hello на [Общие сведения о таблицах][Overview], [типы данных таблицы][Data Types], [распространение таблицы] [ Distribute], [Индексирования таблицы][Index], [статистики таблицы] [ Statistics] и [ Временные таблицы][Temporary].  Дополнительные рекомендации см. в статье [Рекомендации по использованию хранилища данных SQL Azure][SQL Data Warehouse Best Practices].

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
