---
title: "aaaManaging статистика для таблиц в хранилище данных SQL | Документы Microsoft"
description: "Начало работы со статистикой таблиц в хранилище данных SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: c9521dc47891f68d124e77a53e2e15d03275caaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="managing-statistics-on-tables-in-sql-data-warehouse"></a>Управление статистикой таблиц в хранилище данных SQL
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

Hello дополнительные хранилище данных SQL знает о данных, hello быстрее, его можно выполнять запросы к данным.  Hello осуществляется так, хранилище данных SQL Расскажите о данных, путем сбора статистики о данных.  Наличие статистики данных является одним hello наиболее важных элементов можно сделать запросы toooptimize.  Статистика помогает создать hello наиболее оптимальный план для запросов хранилища данных SQL.  Это происходит потому hello хранилище данных SQL, что оптимизатор имеет место определенная потеря основано на запросе оптимизатора.  То есть сравнивает hello стоимость разных планов запросов и выбирает план hello с наименьшую стоимость hello, которое также является hello план, который будет выполняться быстрый hello.

Статистику можно создать по одному или нескольким столбцам, а также на основе индекса таблицы.  Статистические данные хранятся в гистограмме, в которой собираются диапазон hello и селективность значений.  Это особый интерес, когда оптимизатор hello должен tooevaluate соединения, GROUP BY, HAVING и WHERE в запросе.  Например, если hello оптимизатор определяет, что возвращает 1 строку hello даты фильтрации в запросе, он может выбрать сильно планировать, чем если он оценивает, что они даты, которые был выбран будет возвращать 1 миллион строк.  При создании статистики крайне важно, так же важно, что статистика *точно* отражают текущее состояние таблицы hello hello.  Наличие актуальной статистики гарантирует, что хороший план выбранный оптимизатором hello.  Hello планов, созданных оптимизатором hello доступны только в показанной hello статистики на данные.

Hello процесс создания и обновление статистики выполняется в настоящее время вручную, однако является очень простым toodo.  В SQL Server эта процедура выполняется иначе — статистика автоматически создается и обновляется по отдельным столбцам и индексам.  Используя приведенные ниже сведения hello, могут значительно автоматизировать управление hello hello статистики на данные. 

## <a name="getting-started-with-statistics"></a>Начало работы со статистикой
 Создание выборочную статистику для каждого столбца tooget легко запускается со статистикой.  Так как это столь же важно tookeep статистики актуальные, высокий уровень безопасности может быть tooupdate статистике ежедневно или после каждого нагрузки. Всегда есть компромиссы между производительностью и стоимость hello toocreate и обновите статистику.  Если обнаружится, что это занимает слишком много времени toomaintain все статистики, может понадобиться tootry toobe более селективным о есть статистика, какие столбцы или столбцы, которые необходимо частое обновление.  Например может потребоваться столбцов даты tooupdate ежедневно, как могут быть добавлены новые значения, а не после каждой загрузки. Опять же, вы приобретете hello максимальную выгоду, что статистика для столбцов, участвующих в соединениях, GROUP BY, HAVING и WHERE.  Если у вас есть таблица с большим количеством столбцов, используемых только в hello предложение SELECT, статистику для этих столбцов может затруднить и тратит немного больше усилий tooidentify только столбцы hello, где поможет статистические данные, можно уменьшить время toomaintain hello статистике .

## <a name="multi-column-statistics"></a>Многостолбцовая статистика
В дополнение к этому toocreating статистику по отдельным столбцам, вы обнаружите что запросы, смогут воспользоваться преимуществами нескольких столбцов статистики.  Многостолбцовая статистика — это статистика, созданная по списку столбцов.  Они включают один столбец статистики в первом столбце hello в списке hello, а также некоторые сведения о корреляции между столбцами вызывается плотности.  Например если имеется таблица, соединяющее tooanother два столбца, возможно, хранилище данных SQL может быть лучше оптимизирован hello план, если он поддерживает hello связь между двумя столбцами.   Многостолбцовая статистика может повысить производительность запросов для некоторых операций, например составных соединений и группировки.

## <a name="updating-statistics"></a>Обновление статистики
Обновление статистики — это важная часть процедуры управления базой данных.  При изменении hello распределение данных в базе данных hello, статистики должны toobe обновлены.  Устаревшие статистические данные могут стать причиной toosub оптимальной производительности запросов.

Один рекомендуется tooupdate Статистика по столбцам даты в день по мере добавления новые даты.  Каждый время новые строки будут загружены в хранилище данных hello, новые нагрузки даты или даты операций добавляются. Они изменяют распределение данных hello и сделать устаревшей статистики hello. И наоборот статистические данные по столбцу страны в таблице customer редко требуется toobe обновлен, обычно не изменяют hello распределение значений. Предположим, что hello распространения является константой между клиентами, Добавление нового варианта таблицы toohello строк не будет toochange hello данных распространения. Тем не менее если хранилище данных содержит только одной стране и отобразить данные из новых страны, в результате получаются данные из нескольких стран хранения, определенно необходимо tooupdate статистики для столбца страны hello.

Одно из hello первый вопросы tooask при диагностике запроса, «актуальны hello статистики?»

Этот вопрос не может получать ответ hello срок хранения данных hello. Объект статистики вверх toodate может быть очень старым, если нет toohello существенные изменения базовым данным. Когда существенно измениться hello количество строк или существенных изменений в hello распределение значений для данного столбца *затем* это tooupdate Статистика по времени.  

Для справки **SQL Server** (не хранилище данных SQL) автоматически обновляет статистику в следующих случаях:

* Если ни одной строки в таблице hello, при добавлении строк, вы получите автоматическое обновление статистики
* При добавлении более 500 tooa таблицы строк, начиная с менее 500 строк (например в начале имеется 499 и затем добавьте 500 строк tooa объем 999 строк), вы сможете получить автоматического обновления 
* После того, как более 500 строк имеется 500 дополнительных строк tooadd + 20% от размера hello hello таблицы перед вы увидите автоматическое обновление на hello stats

Так как не toodetermine динамического административного Представления данных в таблице hello изменился с момента обновления статистики последнего hello, зная возраст hello статистики можно предоставить с часть изображения hello.  Можно использовать hello в следующем запросе toodetermine hello время последней статистике где обновления для каждой таблицы.  

> [!NOTE]
> Помните, если есть существенные изменения в hello распределение значений для данного столбца, необходимо обновлять статистику независимо от hello время последнего обновления.  
> 
> 

```sql
SELECT
    sm.[name] AS [schema_name],
    tb.[name] AS [table_name],
    co.[name] AS [stats_column_name],
    st.[name] AS [stats_name],
    STATS_DATE(st.[object_id],st.[stats_id]) AS [stats_last_updated_date]
FROM
    sys.objects ob
    JOIN sys.stats st
        ON  ob.[object_id] = st.[object_id]
    JOIN sys.stats_columns sc    
        ON  st.[stats_id] = sc.[stats_id]
        AND st.[object_id] = sc.[object_id]
    JOIN sys.columns co    
        ON  sc.[column_id] = co.[column_id]
        AND sc.[object_id] = co.[object_id]
    JOIN sys.types  ty    
        ON  co.[user_type_id] = ty.[user_type_id]
    JOIN sys.tables tb    
        ON  co.[object_id] = tb.[object_id]
    JOIN sys.schemas sm    
        ON  tb.[schema_id] = sm.[schema_id]
WHERE
    st.[user_created] = 1;
```

Например, для столбцов дат в хранилище данных обычно требуется часто обновлять статистику. Каждый время новые строки будут загружены в хранилище данных hello, новые нагрузки даты или даты операций добавляются. Они изменяют распределение данных hello и сделать устаревшей статистики hello.  И наоборот статистические данные по столбцу "Пол" на таблице заказчика никогда не может потребоваться обновить toobe. Предположим, что hello распространения является константой между клиентами, Добавление нового варианта таблицы toohello строк не будет toochange hello данных распространения. Тем не менее если хранилище данных содержит только один пол и новые требования результаты в нескольких мужчин и женщин определенно необходимо tooupdate статистику на столбце gender hello.

Подробные пояснения см. в статье, посвященной [управлению статистикой][Statistics], на сайте MSDN.

## <a name="implementing-statistics-management"></a>Реализация управления статистикой
Часто бывает tooextend смысл tooensure процесса, статистические данные обновляются при загрузке данных hello конце hello загрузки. Загрузка данных Hello при таблицы наиболее часто изменяются, их размера и их распределение значений. Следовательно, это tooimplement логично некоторые процессы управления.

Некоторые основные принципы приведены ниже для обновления статистики во время процесса загрузки hello:

* Убедитесь, что для каждой загружаемой таблицы обновляется по крайней мере один объект статистики. Это hello обновления таблицы сведения о размере (количество строк и количество страниц) как часть обновления статистики hello.
* Сосредоточьтесь на столбцах, участвующие в предложениях JOIN, GROUP BY, ORDER BY и DISTINCT.
* Рекомендуется обновлять столбцы «по возрастанию ключ», например транзакции более часто, как эти значения не будет включен в гистограммы статистики hello дат.
* Рекомендуется реже обновлять столбцы со статическим распределением.
* Помните, что каждый объект статистики обновляется последовательно. Просто реализовать `UPDATE STATISTICS <TABLE_NAME>` может быть не идеальным решением, особенно для обширных таблиц с большим количеством объектов статистики.

> [!NOTE]
> Дополнительные сведения о [возрастания ключа] см. SQL Server 2014 toohello Технический оценки количества элементов.
> 
> 

Подробные пояснения см. в статье [Оценка количества элементов (SQL Server)][Cardinality Estimation] на сайте MSDN.

## <a name="examples-create-statistics"></a>Примеры: создание статистики
В следующих примерах как toouse различные параметры для создания статистики. Параметры Hello, используемых для каждого столбца зависят от hello характеристик данных и как hello столбец будет использоваться в запросах.

### <a name="a-create-single-column-statistics-with-default-options"></a>О. Создание одностолбцовой статистики с параметрами по умолчанию
toocreate статистики по столбцу, достаточно просто указать имя объекта статистики hello и hello hello столбца.

Следующий синтаксис использует все параметры по умолчанию hello. По умолчанию хранилище данных SQL выборку 20 процентов hello таблицы при создании статистики.

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]);
```

Например:

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1);
```

### <a name="b-create-single-column-statistics-by-examining-every-row"></a>B. Создание одностолбцовой статистики путем проверки всех строк
в большинстве случаев достаточно Hello частота выборки по умолчанию — 20 процентов. Однако можно изменить частоту выборки hello.

hello toosample полной таблицы, используйте следующий синтаксис:

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]) WITH FULLSCAN;
```

Например:

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH FULLSCAN;
```

### <a name="c-create-single-column-statistics-by-specifying-hello-sample-size"></a>C. Создать статистику по отдельным столбцам, задав размер образца hello
Кроме того можно указать размер образца hello в процентах:

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH SAMPLE = 50 PERCENT;
```

### <a name="d-create-single-column-statistics-on-only-some-of-hello-rows"></a>D. Создание статистики по отдельным столбцам на всех строк hello
Другой вариант, можно создать статистику на части hello строк в таблице. Это называется отфильтрованной статистикой.

Например отфильтрованную статистику можно использовать при планировании tooquery определенную секцию большой секционированной таблице. Создав статистики hello только значениями параметров секций, hello точность статистики hello будет улучшить и таким образом повысить производительность запросов.

Этот пример создает статистику по диапазону значений. значения Hello легко может быть определен toomatch hello диапазон значений в секции.

```sql
CREATE STATISTICS stats_col1 ON table1(col1) WHERE col1 > '2000101' AND col1 < '20001231';
```

> [!NOTE]
> Для оптимизатора запросов hello tooconsider с помощью отфильтрованную статистику, при выборе плана hello распределенного запроса запрос hello должен лежать в пределах определения hello объекта статистики hello. Используя предыдущий пример hello, hello запроса целей значения col1 toospecify между 2000101 и 20001231 предложения.
> 
> 

### <a name="e-create-single-column-statistics-with-all-hello-options"></a>E. Создание статистики по отдельным столбцам со всеми параметрами hello
Можно Конечно, объединять параметры hello вместе. пример Hello создает объект отфильтрованной статистики с размером пользовательский образец:

```sql
CREATE STATISTICS stats_col1 ON table1 (col1) WHERE col1 > '2000101' AND col1 < '20001231' WITH SAMPLE = 50 PERCENT;
```

Hello полную справочную информацию см. в разделе [CREATE STATISTICS] [ CREATE STATISTICS] в библиотеке MSDN.

### <a name="f-create-multi-column-statistics"></a>F. Создание многостолбцовой статистики
toocreate статистики нескольких столбцов, просто используйте hello предыдущих примерах, но указать дополнительные столбцы.

> [!NOTE]
> Гистограмма Hello, который используется tooestimate количество строк в результатах запроса hello, доступно только для первого столбца hello указаны в определении объекта статистики hello.
> 
> 

В этом примере hello гистограммы находится на *продукта\_категории*. Статистика между столбцами вычисляется по *product\_category* и *product\_sub_c\ategory*.

```sql
CREATE STATISTICS stats_2cols ON table1 (product_category, product_sub_category) WHERE product_category > '2000101' AND product_category < '20001231' WITH SAMPLE = 50 PERCENT;
```

Так как нет корреляцию между *продукта\_категории* и *продукта\_sub\_категории*, stat нескольких столбцов может быть полезно, если эти столбцы доступны в hello то же время.

### <a name="g-create-statistics-on-all-hello-columns-in-a-table"></a>Ж. Создание статистики для всех столбцов таблицы hello
Одним из способов toocreate статистики — tooissues команды CREATE STATISTICS после создания таблицы hello.

```sql
CREATE TABLE dbo.table1
(
   col1 int
,  col2 int
,  col3 int
)
WITH
  (
    CLUSTERED COLUMNSTORE INDEX
  )
;

CREATE STATISTICS stats_col1 on dbo.table1 (col1);
CREATE STATISTICS stats_col2 on dbo.table2 (col2);
CREATE STATISTICS stats_col3 on dbo.table3 (col3);
```

### <a name="h-use-a-stored-procedure-toocreate-statistics-on-all-columns-in-a-database"></a>З. Используйте хранимую процедуру toocreate статистики для всех столбцов в базе данных
Хранилище данных SQL не имеет эквивалентного хранимая процедура системы слишком [] [sp_create_stats] в SQL Server. Эта хранимая процедура создает объект статистики один столбец для каждого столбца hello базы данных, в котором еще нет статистики.

Это поможет приступить к проектированию базы данных. Чувствовать себя свободного tooadapt он должен tooyour.

```sql
CREATE PROCEDURE    [dbo].[prc_sqldw_create_stats]
(   @create_type    tinyint -- 1 default 2 Fullscan 3 Sample
,   @sample_pct     tinyint
)
AS

IF @create_type NOT IN (1,2,3)
BEGIN
    THROW 151000,'Invalid value for @stats_type parameter. Valid range 1 (default), 2 (fullscan) or 3 (sample).',1;
END;

IF @sample_pct IS NULL
BEGIN;
    SET @sample_pct = 20;
END;

IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN;
    DROP TABLE #stats_ddl;
END;

CREATE TABLE #stats_ddl
WITH    (   DISTRIBUTION    = HASH([seq_nmbr])
        ,   LOCATION        = USER_DB
        )
AS
WITH T
AS
(
SELECT      t.[name]                        AS [table_name]
,           s.[name]                        AS [table_schema_name]
,           c.[name]                        AS [column_name]
,           c.[column_id]                   AS [column_id]
,           t.[object_id]                   AS [object_id]
,           ROW_NUMBER()
            OVER(ORDER BY (SELECT NULL))    AS [seq_nmbr]
FROM        sys.[tables] t
JOIN        sys.[schemas] s         ON  t.[schema_id]       = s.[schema_id]
JOIN        sys.[columns] c         ON  t.[object_id]       = c.[object_id]
LEFT JOIN   sys.[stats_columns] l   ON  l.[object_id]       = c.[object_id]
                                    AND l.[column_id]       = c.[column_id]
                                    AND l.[stats_column_id] = 1
LEFT JOIN    sys.[external_tables] e    ON    e.[object_id]        = t.[object_id]
WHERE       l.[object_id] IS NULL
AND            e.[object_id] IS NULL -- not an external table
)
SELECT  [table_schema_name]
,       [table_name]
,       [column_name]
,       [column_id]
,       [object_id]
,       [seq_nmbr]
,       CASE @create_type
        WHEN 1
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+')' AS VARCHAR(8000))
        WHEN 2
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+') WITH FULLSCAN' AS VARCHAR(8000))
        WHEN 3
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+') WITH SAMPLE '+@sample_pct+'PERCENT' AS VARCHAR(8000))
        END AS create_stat_ddl
FROM T
;

DECLARE @i INT              = 1
,       @t INT              = (SELECT COUNT(*) FROM #stats_ddl)
,       @s NVARCHAR(4000)   = N''
;

WHILE @i <= @t
BEGIN
    SET @s=(SELECT create_stat_ddl FROM #stats_ddl WHERE seq_nmbr = @i);

    PRINT @s
    EXEC sp_executesql @s
    SET @i+=1;
END

DROP TABLE #stats_ddl;
```

toocreate статистики для всех столбцов в таблице hello в этой процедуре просто вызовите процедуру hello.

```sql
prc_sqldw_create_stats;
```

## <a name="examples-update-statistics"></a>Примеры: обновление статистики
Статистика tooupdate, можно сделать следующее.

1. Обновить один объект статистики. Укажите имя объекта статистики, которые вы будете tooupdate hello hello.
2. Обновить все объекты статистики для таблицы. Укажите имя hello hello таблицы вместо одного указанного объекта статистики.

### <a name="a-update-one-specific-statistics-object"></a>О. Обновление одного указанного объекта статистики
Используйте следующий синтаксис tooupdate указанного объекта статистики hello.

```sql
UPDATE STATISTICS [schema_name].[table_name]([stat_name]);
```

Например:

```sql
UPDATE STATISTICS [dbo].[table1] ([stats_col1]);
```

Обновляя конкретной статистике объектов, можно свести к минимуму hello статистики toomanage требуется время и ресурсы. Требуется некоторые считали, однако объекты tooupdate toochoose hello наиболее статистики.

### <a name="b-update-all-statistics-on-a-table"></a>B. Обновление всей статистики для таблицы
Это показан простой метод для обновления всех объектов hello статистики для таблицы.

```sql
UPDATE STATISTICS [schema_name].[table_name];
```

Например:

```sql
UPDATE STATISTICS dbo.table1;
```

Эта инструкция является просто toouse. Необходимо помните это обновляет всю статистику для таблицы hello и, следовательно, может выполнять больше работы, чем необходимо. Если производительность hello не является проблемой, это определенно hello простой и эффективный способ tooguarantee статистические данные актуальны.

> [!NOTE]
> Если обновление всей статистики для таблицы, хранилище данных SQL не просмотра toosample hello таблицу для каждой статистики. Если hello таблица имеет большой размер, имеет много столбцов и статистику, может быть более эффективным tooupdate отдельных статистические данные на основе необходимого.
> 
> 

Для реализации `UPDATE STATISTICS` процедуры см. в разделе hello [временные таблицы] [ Temporary] статьи. метод реализации Hello является немного отличается toohello `CREATE STATISTICS` описанную выше процедуру, кроме hello конечным результатом является таким же hello.

Hello полный синтаксис см. в разделе [обновление статистики] [ Update Statistics] в библиотеке MSDN.

## <a name="statistics-metadata"></a>Метаданные статистики
Существует несколько функций, которые можно использовать toofind сведения о статистике и Системное представление. Например можно увидеть, если объект статистики может оказаться устаревшей, используя toosee функции hello stats даты при последней Статистика создана или обновлена.

### <a name="catalog-views-for-statistics"></a>Представления каталога для статистики
Вот какие системные представления показывают информацию о статистике:

| Представление каталога | Описание |
|:--- |:--- |
| [sys.columns][sys.columns] |Одна строка для каждого столбца. |
| [sys.objects][sys.objects] |Одну строку для каждого объекта в базе данных hello. |
| [sys.schemas][sys.schemas] |Одну строку для каждой схемы в базе данных hello. |
| [sys.stats][sys.stats] |Одна строка для каждого объекта статистики. |
| [sys.stats_columns][sys.stats_columns] |Одну строку для каждого столбца в объекте статистики hello. Ссылающемся toosys.columns. |
| [sys.tables][sys.tables] |Одна строка для каждой таблицы (включая внешние таблицы). |
| [sys.table_types][sys.table_types] |Одна строка для каждого типа данных. |

### <a name="system-functions-for-statistics"></a>Системные функции для статистики
Эти системные функции полезны для работы со статистикой:

| Системная функция | Описание |
|:--- |:--- |
| [STATS_DATE][STATS_DATE] |Объект статистики hello Дата последнего обновления. |
| [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] |Предоставляет сводные уровня и подробных сведений о hello распределение значений, подразумевается hello объекта статистики. |

### <a name="combine-statistics-columns-and-functions-into-one-view"></a>Сочетание столбцов и функций статистики в одном представлении
В этом представлении объединяет столбцы, связывающие toostatistics и результаты из функции hello [STATS_DATE()] [] друг с другом.

```sql
CREATE VIEW dbo.vstats_columns
AS
SELECT
        sm.[name]                           AS [schema_name]
,       tb.[name]                           AS [table_name]
,       st.[name]                           AS [stats_name]
,       st.[filter_definition]              AS [stats_filter_defiinition]
,       st.[has_filter]                     AS [stats_is_filtered]
,       STATS_DATE(st.[object_id],st.[stats_id])
                                            AS [stats_last_updated_date]
,       co.[name]                           AS [stats_column_name]
,       ty.[name]                           AS [column_type]
,       co.[max_length]                     AS [column_max_length]
,       co.[precision]                      AS [column_precision]
,       co.[scale]                          AS [column_scale]
,       co.[is_nullable]                    AS [column_is_nullable]
,       co.[collation_name]                 AS [column_collation_name]
,       QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])
                                            AS two_part_name
,       QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])
                                            AS three_part_name
FROM    sys.objects                         AS ob
JOIN    sys.stats           AS st ON    ob.[object_id]      = st.[object_id]
JOIN    sys.stats_columns   AS sc ON    st.[stats_id]       = sc.[stats_id]
                            AND         st.[object_id]      = sc.[object_id]
JOIN    sys.columns         AS co ON    sc.[column_id]      = co.[column_id]
                            AND         sc.[object_id]      = co.[object_id]
JOIN    sys.types           AS ty ON    co.[user_type_id]   = ty.[user_type_id]
JOIN    sys.tables          AS tb ON  co.[object_id]        = tb.[object_id]
JOIN    sys.schemas         AS sm ON  tb.[schema_id]        = sm.[schema_id]
WHERE   1=1
AND     st.[user_created] = 1
;
```

## <a name="dbcc-showstatistics-examples"></a>Примеры DBCC SHOW_STATISTICS()
DBCC SHOW_STATISTICS() показывает hello данные, хранящиеся в объекте статистики. Эти данные состоят из трех частей:

1. Заголовок
2. вектор плотности;
3. Гистограмма

Здравствуйте, заголовок метаданных о статистике hello. Hello гистограмма отображает hello распределение значений в первом ключевом столбце hello объекта статистики hello. вектор плотностей Hello измеряет корреляции между столбцами. SQLDW вычисляет оценки количества элементов с помощью любого из данных hello в объекте статистики hello.

### <a name="show-header-density-and-histogram"></a>Отображение заголовка, плотности и гистограммы
Это простой пример показывает все три части объекта статистики.

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>)
```

Например:

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1);
```

### <a name="show-one-or-more-parts-of-dbcc-showstatistics"></a>Отображение одной или нескольких частей DBCC SHOW_STATISTICS()
Если только вы заинтересованы в просмотре определенных компонентов, используйте hello `WITH` предложения и укажите, какие части требуется toosee:

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>) WITH stat_header, histogram, density_vector
```

Например:

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1) WITH histogram, density_vector
```

## <a name="dbcc-showstatistics-differences"></a>Отличия DBCC SHOW_STATISTICS()
DBCC SHOW_STATISTICS() более строго, реализованы в tooSQL сравнивается хранилище данных SQL Server.

1. Недокументированные возможности не поддерживаются.
2. Нельзя использовать Stats_stream.
3. Нельзя соединить результаты для определенных подмножеств данных статистики, например (STAT_HEADER JOIN DENSITY_VECTOR).
4. Невозможно задать NO_INFOMSGS для подавления сообщений.
5. Нельзя использовать квадратные скобки вокруг имен статистики.
6. Невозможно использовать объекты статистики tooidentify имена столбцов
7. Пользовательская ошибка 2767 не поддерживается.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения см. в статье [Инструкция DBCC SHOW_STATISTICS (Transact-SQL)][DBCC SHOW_STATISTICS] на сайте MSDN.  toolearn более, статьях hello на [Общие сведения о таблицах][Overview], [типы данных таблицы][Data Types], [распространение таблицы] [ Distribute], [Индексирования таблицы][Index], [секционировать таблицу] [ Partition] и [ Временные таблицы][Temporary].  Дополнительные рекомендации см. в статье [Рекомендации по использованию хранилища данных SQL Azure][SQL Data Warehouse Best Practices].  

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
[Cardinality Estimation]: https://msdn.microsoft.com/library/dn600374.aspx
[CREATE STATISTICS]: https://msdn.microsoft.com/library/ms188038.aspx
[DBCC SHOW_STATISTICS]:https://msdn.microsoft.com/library/ms174384.aspx
[Statistics]: https://msdn.microsoft.com/library/ms190397.aspx
[STATS_DATE]: https://msdn.microsoft.com/library/ms190330.aspx
[sys.columns]: https://msdn.microsoft.com/library/ms176106.aspx
[sys.objects]: https://msdn.microsoft.com/library/ms190324.aspx
[sys.schemas]: https://msdn.microsoft.com/library/ms190324.aspx
[sys.stats]: https://msdn.microsoft.com/library/ms177623.aspx
[sys.stats_columns]: https://msdn.microsoft.com/library/ms187340.aspx
[sys.tables]: https://msdn.microsoft.com/library/ms187406.aspx
[sys.table_types]: https://msdn.microsoft.com/library/bb510623.aspx
[UPDATE STATISTICS]: https://msdn.microsoft.com/library/ms187348.aspx

<!--Other Web references-->  
