---
title: "aaaDistributing таблиц в хранилище данных SQL | Документы Microsoft"
description: "Начало работы с распределением таблиц в хранилище данных SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: 5ed4337f-7262-4ef6-8fd6-1809ce9634fc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 65093eeaeb00fef85aaa6070da2c976fed3f4bbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="distributing-tables-in-sql-data-warehouse"></a>Распределение таблиц в хранилище данных SQL
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

Хранилище данных SQL является распределенной системой баз данных с массовой параллельной обработкой (MPP).  Распределяя данные и возможности обработки между несколькими узлами, хранилище данных SQL может предложить огромную масштабируемость — намного больше любой единой системы.  Выбор способа toodistribute ваши данные в хранилище данных SQL является одним из наиболее важных hello факторы tooachieving оптимальной производительности.   Hello ключа toooptimal производительности минимизация перемещение данных и в свою очередь перемещения данных ключа toominimizing hello при выборе стратегии распространения правой hello.

## <a name="understanding-data-movement"></a>Основные сведения о перемещении данных
В системе MPP hello данные из каждой таблицы разделяются между несколькими базами данных базовой.  Hello наиболее оптимизированные запросы в системе MPP можно просто передать через tooexecute на hello отдельных распределенных баз данных без участия между hello других баз данных.  Например, предположим, что у вас есть база данных с данными о продажах, содержащая две таблицы: "Продажи" и "Клиенты".  Если имеется запрос, который должен toojoin таблицы customer tooyour таблицу продаж и разделения таблицы клиентов вверх и продаж по номеру клиента размещение каждого клиента в отдельной базе данных, любые запросы, которые соединяют продаж и клиента, могут быть устранены в каждой базы данных, не имея сведений о hello других баз данных.  Напротив, если разделить данные о продажах по номеру заказа и данных клиента по номеру клиента, затем любая заданная база данных не будет hello соответствующих данных для каждого клиента и, следовательно, если требуется toojoin данных клиента tooyour данные о продажах, потребовалось бы tooget hello данных для каждого заказчика из hello других баз данных.  Во втором примере перемещения данных, должны toooccur toomove hello клиентские данные toohello данные о продажах, так что hello двух таблиц можно объединить.  

Перемещение данных не всегда плохо, иногда бывает необходимо toosolve запроса.  Но избежав его, запрос будет выполняться быстрее.  Перемещение данных в основном происходит при объединении или группировании таблиц.  Часто toodo оба, необходимо, чтобы во время могут потребоваться toooptimize один из сценариев, таких как соединения, вы по-прежнему требуется toohelp перемещения данных, решения для hello другие сценарии, как статистическая обработка.  выяснить, что прием Hello которого требует меньше усилий.  В большинстве случаев распространение большими таблицами фактов обычно соединяемыми столбца является hello наиболее эффективный способ уменьшения hello большинство перемещения данных.  Распределение данных в столбцах соединения происходит намного более распространенным перемещения данных метод tooreduce от распределения данных для столбцов, участвующих в статистическое выражение.

## <a name="select-distribution-method"></a>Выбор метода распределения
В фоновом hello хранилище данных SQL делит данные на 60 баз данных.  Каждая отдельная база данных является связанной tooas **распространения**.  При загрузке данных в каждой таблице хранилища данных SQL имеет tooknow как toodivide через эти 60 распределения данных.  

метод распределения Hello определяется на уровне таблицы hello и в настоящее время существует два варианта:

1. **Метод циклического перебора** — данные распределяются равномерно, но случайным образом.
2. **Хэш-распределение** — данные распределяются на основе хэширования значений одного столбца.

По умолчанию, если не определить способ распространения данных таблицы будут распределяться с помощью hello **циклический перебор** метода распространения.  Тем не менее, как становятся более сложными, в реализации, будет необходимо с помощью tooconsider **хэш распределенных** таблиц toominimize перемещения данных, который в свою очередь оптимизирует производительность запросов.

### <a name="round-robin-tables"></a>Таблицы, распределенные по методу циклического перебора
Существенно как кажется является использование hello циклического способа передачи данных.  После загрузки данных в каждой строки просто отправляется toohello Далее распространения.  Этот метод распространения hello данных будет всегда случайным образом hello данных очень равномерно распределять по всем hello распределений.  То есть нет сортировки выполняются во время hello циклический перебор процесс, который помещает данные.  По этой причине циклическое распределение иногда называют случайным хэшем.  С таблицей распределенных циклического нет данных необходимость toounderstand hello.  По этой причине такие таблицы часто удобно использовать для загрузки.

По умолчанию Если вы выбрали метод распространения hello циклического метода распространения будет использоваться.  Тем не менее пока циклический перебор таблицы являются легко toouse, поскольку данные распределяются случайным образом на системе hello, это значит, что система hello не могут гарантировать какой распространения каждой строки составляет на.  Как результат, система hello иногда требуется tooinvoke toobetter операции перемещения данных организации данных, прежде чем его можно разрешить запрос.  Это дополнительное действие может повлиять на производительность запросов.

Рассмотрите возможность использования циклическое распределение для таблицы в hello следующие сценарии:

* если это простая отправная точка для начала работы;
* если отсутствует очевидный ключ соединения;
* Если не столбец хорошим кандидатом для распространения hello таблицы хэша
* Если hello таблицы не использует общий ключ соединения с другими таблицами
* Если соединение hello менее важна, чем другие соединения в запросе hello
* Когда таблица hello является временной промежуточной таблицы

Ниже приведены два примера, которые позволяют создать таблицу с распределением по методу циклического перебора.

```SQL
-- Round Robin created by default
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
;

-- Explicitly Created Round Robin Table
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
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
,   DISTRIBUTION = ROUND_ROBIN
)
;
```

> [!NOTE]
> Пока что hello по умолчанию табличного типа, в явном виде в DDL считается рекомендуется, чтобы намерения hello таблице макета, снимите флажок tooothers циклического перебора.
>
>

### <a name="hash-distributed-tables"></a>Распределяемые по хэшу таблицы
С помощью **хэш распределенных** toodistribute алгоритм таблицы может повысить производительность во многих сценариях за счет уменьшения перемещения данных во время выполнения запроса.  Распределенные таблицы — это таблицы, которые разделены между hello хеширования распределенных баз данных с помощью хэш-алгоритма для одного столбца, который нужно установить.  столбец распределения Hello является то, что определяет, как hello данные распределяются между распределенных баз данных.  хэш-функции Hello использует hello распространения столбца tooassign строки toodistributions.  Здравствуйте, алгоритма хэширования и детерминированным полученный распространения.  То есть hello совпадают с hello того же типа данных будет всегда имеет toohello одинаковое распределение.    

Ниже приведен пример создания таблицы, распределенной по идентификаторам.

```SQL
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
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
,  DISTRIBUTION = HASH([ProductKey])
)
;
```

## <a name="select-distribution-column"></a>Выбор столбца распределения
При выборе слишком**распространять хэш** таблицу, вам потребуется tooselect распространения один столбец.  При выборе столбца распределения, существует три основных факторов tooconsider.  

Столбец должен соответствовать следующим критериям.

1. Он должен быть необновляемым.
2. Он должен распределять данные равномерно, предотвращая их смещение.
3. Минимизация перемещения данных

### <a name="select-distribution-column-which-will-not-be-updated"></a>Выбор необновляемого столбца распределения
Столбцы распределения являются необновляемыми. Поэтому для этой роли необходимо выбрать столбец со статическими значениями.  Если столбец, потребуется обновить toobe, это обычно не распространения хорошим кандидатом.  Если есть случай, когда необходимо обновлять столбец распределения, это можно сделать, сначала удалив строку hello и последующей вставке новой строки.

### <a name="select-distribution-column-which-will-distribute-data-evenly"></a>Выбор столбца распределения, который распределяет данные равномерно
Так как только быстро, как его медленных распространения выполняет распределенной системе, он может важные toodivide hello рабочих равномерно распределения hello в порядке выполнения tooachieve балансировки во всей системе hello.  Работа hello разделена на распределенных систем, как Hello основан на где находятся данные hello для каждого распределения.  Это делает столбец вправо распределения hello tooselect очень важны для распространения данных hello, чтобы каждого распределения есть равно работы и будет взять hello же toocomplete времени его часть работы hello.  Когда рабочие также и распределены по системе hello, hello данных распределяется среди hello распределения.  Если данные распределены неравномерно, это называется **неравномерным распределением данных**.  

toodivide данные равномерно и избежать наклона данных, необходимо учитывать следующие hello, при выборе столбца распространения:

1. Выберите столбец, содержащий значительное количество различных значений.
2. Избегайте распределения данных по столбцам, содержащим несколько различных значений.
3. Избегайте распределения данных по столбцам с высоким коэффициентом содержания значений NULL.
4. Не распределяйте данные по столбцам с датами.

Поскольку каждое значение хэшированное too1 60 распределений, равномерное распределение tooachieve требуется tooselect столбцом с высокой степенью уникален и содержит более 60 уникальные значения.  tooillustrate, рассмотрим случай, когда столбец содержит только 40 уникальные значения.  Если этот столбец был выбран в качестве ключа распределения hello, hello данных для этой таблицы окажется на 40 распределения максимум, оставляя 20 распределения не данными и toodo без обработки.  И наоборот hello других 40 распределениях бы дополнительные toodo работы, что hello данных был равномерно распределять более 60 распределения.  Этот сценарий является примером неравномерного распределения данных.

В системе MPP каждого действия запроса ожидает всех распределений toocomplete их доля рабочих hello.  Если одна распространения не выполняет дополнительную работу, чем другие hello, а затем hello ресурс hello других дистрибутивах, которых фактически напрасно как ожидание в занят распространения hello.  Если работа неравномерно разделена между всеми распределениями, это называется **неравномерным распределением обработки**.  Наклон обработки вызовет toorun запросов медленнее, чем если hello рабочей нагрузки могут быть равномерно распределены по hello распределения.  Наклон данных вызовет tooprocessing наклона.

Избегайте распространение на высокой допускает значения NULL столбца в соответствии с hello значения null все попадете на hello же распространителя. Распространение по столбцу даты также могут вызвать наклона обработки, так как все данные для данной даты будут перемещаться на hello же распространителя. Если несколько пользователей выполняются все фильтрации запросов на hello же даты, а затем только 1 60 распределений hello могут быть представлены все действия hello после указанной даты будет только одна распространения. В этом случае запросы hello скорее всего будут выполняться медленнее, чем hello данных были равномерно распределять по всем распределений hello 60 раз.

Если столбцы не подходит, рассмотрите возможность использования циклического метода распространения hello.

### <a name="select-distribution-column-which-will-minimize-data-movement"></a>Выбор столбца распределения, который минимизирует перемещение данных
Минимизация перемещения данных, выбрав столбец вправо распределения hello является одним из наиболее важных стратегий hello для оптимизации производительности в хранилище данных SQL.  Перемещение данных в основном происходит при объединении или группировании таблиц.  Все столбцы, используемые в предложениях `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` и `HAVING`, **могут** становиться столбцами хэш-распределения.

Здравствуйте, с другой стороны, столбцы в hello `WHERE` предложение **не** сделать столбец кандидатов хорошей хэш из-за ограничения котором распределения участвовать в запросе hello, вызывая обработки наклона.  Хорошим примером для столбца, который может быть заманчивой toodistribute на, но часто может вызвать такая обработка наклона — столбец даты.

Вообще говоря при наличии двух большими таблицами фактов часто встречающиеся в соединении вы приобретете hello максимальной производительности путем распределения обе таблицы в одном из столбцов соединения hello.  Если у вас есть таблицы, не присоединены к домену tooanother большой таблицы фактов, найдите toocolumns, которые часто находятся в hello `GROUP BY` предложения.

Существует несколько ключевых критерии, которые должны быть выполнены tooavoid перемещение данных во время соединения.

1. Hello таблицам, участвующим в соединении hello должен быть распределен по хэш **один** hello столбцов, участвующих в соединении hello.
2. типы данных Hello hello столбцы соединения должны совпадать между обеих таблиц.
3. Hello столбцы должны быть присоединены с помощью оператора равенства.
4. Hello соединения тип не может быть `CROSS JOIN`.

## <a name="troubleshooting-data-skew"></a>Устранение смещения данных
При распространении данных таблицы с помощью метода распространения хэш hello, существует возможность того, что некоторые дистрибутивы будет синхронизована toohave непропорционально больше данных, чем другие. Наклон излишнего данных может повлиять на производительность запроса, так как конечный результат hello распределенный запрос должен ожидать hello наиболее долго выполняющегося распространения toofinish. В зависимости от степени hello наклона, может потребоваться tooaddress данных hello его.

### <a name="identifying-skew"></a>Определение смещения данных
Простой способ tooidentify таблицы как неравномерным — toouse `DBCC PDW_SHOWSPACEUSED`.  Это очень быстрый и простой способ toosee hello число строк таблицы, которые хранятся в каждом распределений hello 60 базы данных.  Помните, что для производительности наиболее балансировки hello hello строк в таблице распределенных должны вводиться равномерно в все распределения hello.

```sql
-- Find data skew for a distributed table
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

Тем не менее если запрос hello хранилище данных SQL Azure динамические административные представления (DMV) можно выполнить более глубокий анализ.  toostart, создание представления "hello" [dbo.vTableSizes] [ dbo.vTableSizes] просмотреть с помощью hello SQL из [Общие сведения о таблицах] [ Overview] статьи.  После создания представления hello выполните этот запрос tooidentify, таблицы, для которых не более 10% данных наклон.

```sql
select *
from dbo.vTableSizes
where two_part_name in
    (
    select two_part_name
    from dbo.vTableSizes
    where row_count > 0
    group by two_part_name
    having min(row_count * 1.000)/max(row_count * 1.000) > .10
    )
order by two_part_name, row_count
;
```

### <a name="resolving-data-skew"></a>Устранение неравномерности данных
Не все наклона было достаточно toowarrant.  В некоторых случаях hello производительности таблицы в некоторые запросы могут перевесить hello повреждений данных наклона.  toodecide, если необходимо разрешить данные наклон в таблице, необходимо понимать как можно больше об объемах данных hello и запросы в рабочей нагрузке.   Одним из способов toolook на hello влияние наклон — toouse hello инструкциям hello [мониторинг запросов] [ Query Monitoring] статью влияние hello toomonitor наклона на производительность запросов и специально hello влияние toohow длительных запросов. Отключите toocomplete на отдельные распределения hello.

Распределение данных зависит от поиск hello баланс между минимизация Рассогласование данных и минимизации перемещения данных. Они могут противоположных целей и иногда необходимо tookeep данных наклона при перемещении данных tooreduce заказа. Например если столбец распределения hello часто hello общего столбца соединения и агрегаты, вы будет минимизацию перемещения данных. Hello преимущество наличия перемещения минимальными данными hello способны перевесить издержки расхода последствия hello к искажению данных.

типичный способ Hello разница в показаниях данных tooresolve: toore-создать hello таблицу со столбцом иное распределение. Поскольку нет способа столбец распределения hello toochange на существующем, hello способом toochange hello распределение таблиц таблицы его toorecreate его с [CTAS] [].  Смещение данных можно устранить двумя способами.

### <a name="example-1-re-create-hello-table-with-a-new-distribution-column"></a>Пример 1: Создать повторно таблицу hello с новый столбец распределения
В этом примере используется toore [CTAS] []-создать таблицу со столбцом распространения другой хэш.

```sql
CREATE TABLE [dbo].[FactInternetSales_CustomerKey]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  HASH([CustomerKey])
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_CustomerKey')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_CustomerKey] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_CustomerKey] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_CustomerKey] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_CustomerKey] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_CustomerKey] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_CustomerKey] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_CustomerKey] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_CustomerKey] ([SalesAmount]);

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_ProductKey];
RENAME OBJECT [dbo].[FactInternetSales_CustomerKey] too[FactInternetSales];
```

### <a name="example-2-re-create-hello-table-using-round-robin-distribution"></a>Пример 2: Создать повторно таблицу hello, с использованием циклического распределения
В этом примере используется toore [CTAS] []-создать таблицу с циклическим перебором вместо хэш-распределения. Это изменение вызовет распространения даже данные по цене hello перемещения данных.

```sql
CREATE TABLE [dbo].[FactInternetSales_ROUND_ROBIN]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  ROUND_ROBIN
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_ROUND_ROBIN')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_ROUND_ROBIN] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_ROUND_ROBIN] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_ROUND_ROBIN] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_ROUND_ROBIN] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_ROUND_ROBIN] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_ROUND_ROBIN] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_ROUND_ROBIN] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_ROUND_ROBIN] ([SalesAmount]);

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_HASH];
RENAME OBJECT [dbo].[FactInternetSales_ROUND_ROBIN] too[FactInternetSales];
```

## <a name="next-steps"></a>Дальнейшие действия
toolearn более о таблице, в разделе hello [распределить][Distribute], [индекс][Index], [секции] [ Partition], [Типы данных][Data Types], [статистики] [ Statistics] и [временных таблиц] [ Temporary] статей.

Обзор рекомендаций по использованию приведен в статье [Рекомендации по использованию хранилища данных SQL Azure][SQL Data Warehouse Best Practices].

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
[Query Monitoring]: ./sql-data-warehouse-manage-monitor.md
[dbo.vTableSizes]: ./sql-data-warehouse-tables-overview.md#table-size-queries

<!--MSDN references-->
[DBCC PDW_SHOWSPACEUSED()]: https://msdn.microsoft.com/library/mt204028.aspx

<!--Other Web references-->
