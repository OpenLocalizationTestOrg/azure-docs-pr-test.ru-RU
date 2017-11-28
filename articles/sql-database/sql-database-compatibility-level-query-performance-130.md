---
title: "уровень совместимости aaaDatabase 130 - базы данных SQL Azure | Документы Microsoft"
description: "В этой статье мы исследовать преимущества hello, используя преимущества hello hello новый оптимизатор запросов и запуска базы данных SQL Azure на уровне совместимости 130 и запросить набор функций процессора. Мы обсудим вопросы hello побочные эффекты на производительность запросов hello hello существующих приложений SQL."
services: sql-database
documentationcenter: 
author: alainlissoir
manager: jhubbard
editor: 
ms.assetid: 8619f90b-7516-46dc-9885-98429add0053
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.devlang: NA
ms.tgt_pltfrm: NA
ms.topic: article
ms.date: 08/08/2016
ms.author: alainl
ms.openlocfilehash: 25693c5f7b01405b7073fa7d4cc2833fbe125e2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="improved-query-performance-with-compatibility-level-130-in-azure-sql-database"></a><span data-ttu-id="4ab51-104">Повышение производительности запросов с использованием уровня совместимости 130 в базе данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="4ab51-104">Improved query performance with compatibility Level 130 in Azure SQL Database</span></span>
<span data-ttu-id="4ab51-105">База данных SQL Azure выполняется прозрачно сотни тысяч баз данных на многих различных совместимости уровнях, сохранение и обеспечивая hello обратной совместимости toohello соответствующую версию Microsoft SQL Server для всех клиентов!</span><span class="sxs-lookup"><span data-stu-id="4ab51-105">Azure SQL Database is running transparently hundreds of thousands of databases at many different compatibility levels, preserving and guaranteeing hello backward compatibility toohello corresponding version of Microsoft SQL Server for all its customers!</span></span>

<span data-ttu-id="4ab51-106">В этой статье мы исследовать преимущества hello под управлением вашей базе данных SQL Azure на уровне совместимости 130 и использование преимуществ hello hello новый оптимизатор запросов и запросов функций процессора.</span><span class="sxs-lookup"><span data-stu-id="4ab51-106">In this article, we explore hello benefits of running your Azure SQL Databse at compatibility level 130, and leveraging hello benefits of hello new query optimizer and query processor features.</span></span> <span data-ttu-id="4ab51-107">Мы обсудим вопросы hello побочные эффекты на производительность запросов hello hello существующих приложений SQL.</span><span class="sxs-lookup"><span data-stu-id="4ab51-107">We also address hello possible side-effects on hello query performance for hello existing SQL applications.</span></span>

<span data-ttu-id="4ab51-108">Напоминаем журнала выравнивание hello уровни совместимости toodefault версии SQL выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4ab51-108">As a reminder of history, hello alignment of SQL versions toodefault compatibility levels are as follows:</span></span>

* <span data-ttu-id="4ab51-109">100 — в SQL Server 2008 и Базе данных SQL Azure версии 11;</span><span class="sxs-lookup"><span data-stu-id="4ab51-109">100: in SQL Server 2008 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="4ab51-110">110 — в SQL Server 2012 и Базе данных SQL Azure версии 11;</span><span class="sxs-lookup"><span data-stu-id="4ab51-110">110: in SQL Server 2012 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="4ab51-111">120 — в SQL Server 2014 и Базе данных SQL Azure версии 12;</span><span class="sxs-lookup"><span data-stu-id="4ab51-111">120: in SQL Server 2014 and Azure SQL Database V12.</span></span>
* <span data-ttu-id="4ab51-112">130 — в SQL Server 2016 и <азе данных SQL Azure версии 12.</span><span class="sxs-lookup"><span data-stu-id="4ab51-112">130: in SQL Server 2016 and Azure SQL Database V12.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4ab51-113">Начиная с версии **mid июня 2016 г.**, в базе данных SQL Azure, уровень совместимости по умолчанию hello будет 130 вместо 120 для **только что созданный** баз данных.</span><span class="sxs-lookup"><span data-stu-id="4ab51-113">Starting in **mid-June 2016**, in Azure SQL Database, hello default compatibility level will be 130 instead of 120 for **newly created** databases.</span></span>
> 
> <span data-ttu-id="4ab51-114">Это *не* касается баз данных, созданных до середины июня 2016 года. Они сохранят текущий уровень совместимости (100, 110 и 120).</span><span class="sxs-lookup"><span data-stu-id="4ab51-114">Databases created before mid-June 2016 will *not* be affected, and will maintain their current compatibility level (100, 110, or 120).</span></span> <span data-ttu-id="4ab51-115">Базы данных, перенесенные из базы данных SQL Azure версии V11 tooV12 будет иметь уровень совместимости 100 и 110.</span><span class="sxs-lookup"><span data-stu-id="4ab51-115">Databases that migrated from Azure SQL Database version V11 tooV12 will have a compatibility level of either 100 or 110.</span></span> 
> 

## <a name="about-compatibility-level-130"></a><span data-ttu-id="4ab51-116">Об уровне совместимости 130</span><span class="sxs-lookup"><span data-stu-id="4ab51-116">About compatibility level 130</span></span>
<span data-ttu-id="4ab51-117">Во-первых Если вы хотите tooknow hello текущий уровень совместимости базы данных, выполните hello, следующем за инструкцией Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="4ab51-117">First, if you want tooknow hello current compatibility level of your database, execute hello following Transact-SQL statement.</span></span>

```
SELECT compatibility_level
    FROM sys.databases
    WHERE name = '<YOUR DATABASE_NAME>’;
```


<span data-ttu-id="4ab51-118">До этого изменения toolevel 130 происходит для **вновь** создаваемых баз данных, давайте просмотрите все о — это изменение некоторых примеров очень простой запрос и посмотрим, как любой пользователь, могут помочь от него.</span><span class="sxs-lookup"><span data-stu-id="4ab51-118">Before this change toolevel 130 happens for **newly** created databases, let’s review what this change is all about through some very basic query examples, and see how anyone can benefit from it.</span></span>

<span data-ttu-id="4ab51-119">Обработка запросов в реляционных базах данных могут быть очень сложными и может привести toolots компьютера научных вычислений и математические toounderstand hello связаны конкретные варианты и поведений.</span><span class="sxs-lookup"><span data-stu-id="4ab51-119">Query processing in relational databases can be very complex and can lead toolots of computer science and mathematics toounderstand hello inherent design choices and behaviors.</span></span> <span data-ttu-id="4ab51-120">В этом документе hello содержимого был намеренно упрощенная tooensure, что любой пользователь с минимальным технические сведения понять влияние hello изменение уровня совместимости hello и определить его преимущества приложений.</span><span class="sxs-lookup"><span data-stu-id="4ab51-120">In this document, hello content has been intentionally simplified tooensure that anyone with some minimum technical background can understand hello impact of hello compatibility level change and determine how it can benefit applications.</span></span>

<span data-ttu-id="4ab51-121">Давайте рассмотрим быстрого hello уровень совместимости 130 переводит в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="4ab51-121">Let’s have a quick look at what hello compatibility level 130 brings at hello table.</span></span>  <span data-ttu-id="4ab51-122">Дополнительные сведения см. в статье [Уровень совместимости инструкции ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx). Ниже представлены краткие сведения.</span><span class="sxs-lookup"><span data-stu-id="4ab51-122">You can find more details at [ALTER DATABASE Compatibility Level (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), but here is a short summary:</span></span>

* <span data-ttu-id="4ab51-123">Hello операции вставки в инструкции Insert select может быть многопоточных или параллельный план, а перед эта операция была однопотоковой.</span><span class="sxs-lookup"><span data-stu-id="4ab51-123">hello Insert operation of an Insert-select statement can be multi-threaded or can have a parallel plan, while before this operation was single-threaded.</span></span>
* <span data-ttu-id="4ab51-124">У запроса оптимизированной для памяти таблицы и табличных переменных теперь могут быть параллельные планы. Раньше у этой операции также был один поток.</span><span class="sxs-lookup"><span data-stu-id="4ab51-124">Memory Optimized table and table variables queries can now have parallel plans, while before this operation was also single-threaded .</span></span>
* <span data-ttu-id="4ab51-125">Теперь можно выполнять выборку статистики для оптимизированных для памяти таблиц, а также автоматически обновлять ее.</span><span class="sxs-lookup"><span data-stu-id="4ab51-125">Statistics for Memory Optimized table can now be sampled and are auto-updated.</span></span> <span data-ttu-id="4ab51-126">Дополнительные сведения см. в подразделе о [выполняющейся в памяти OLTP раздела "Новые возможности в ядре СУБД"](https://msdn.microsoft.com/library/bb510411.aspx#InMemory).</span><span class="sxs-lookup"><span data-stu-id="4ab51-126">See [What's New in Database Engine: In-Memory OLTP](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) for more details.</span></span>
* <span data-ttu-id="4ab51-127">Изменения в пакетном режиме и в режиме строки, связанные с индексами хранилища столбцов</span><span class="sxs-lookup"><span data-stu-id="4ab51-127">Batch mode v/s Row Mode changes with Column Store indexes</span></span>
  * <span data-ttu-id="4ab51-128">Сортировка в таблице с индексом хранилища столбцов теперь выполняется в пакетном режиме.</span><span class="sxs-lookup"><span data-stu-id="4ab51-128">Sorts on a table with a Column Store index are now in batch mode.</span></span>
  * <span data-ttu-id="4ab51-129">Оконные статистические выражения, например инструкции TSQL LAG или LEAD, теперь работают в пакетном режиме.</span><span class="sxs-lookup"><span data-stu-id="4ab51-129">Windowing aggregates now operate in batch mode such as TSQL LAG/LEAD statements.</span></span>
  * <span data-ttu-id="4ab51-130">Запросы к таблицам хранилища столбцов с несколькими отдельными предложениями работают в пакетном режиме.</span><span class="sxs-lookup"><span data-stu-id="4ab51-130">Queries on Column Store tables with Multiple distinct clauses operate in Batch mode.</span></span>
  * <span data-ttu-id="4ab51-131">Запросы со степенью параллелизма DOP=1 или с последовательным планом также выполняются в пакетном режиме.</span><span class="sxs-lookup"><span data-stu-id="4ab51-131">Queries running under DOP=1 or with a serial plan also execute in Batch Mode.</span></span>
* <span data-ttu-id="4ab51-132">И, наконец усовершенствования кратности фактически соединяющиеся с уровнем совместимости 120, но для тех, запущенные в совместимости ниже уровня (т. е. 100 или 110), hello уровня toocompatibility перемещения 130 будет также восстановить эти усовершенствования и их можно также повышения производительности запросов hello приложений.</span><span class="sxs-lookup"><span data-stu-id="4ab51-132">Last, Cardinality Estimation improvements are actually coming with compatibility level 120, but for those of you running at a lower Compatibility level (i.e. 100, or 110), hello move toocompatibility level 130 will also bring these improvements, and these can also benefit hello query performance of your applications.</span></span>

## <a name="practicing-compatibility-level-130"></a><span data-ttu-id="4ab51-133">Использование уровня совместимости 130</span><span class="sxs-lookup"><span data-stu-id="4ab51-133">Practicing compatibility level 130</span></span>
<span data-ttu-id="4ab51-134">Первый давайте некоторых таблиц, индексов и случайные данные, созданные toopractice некоторые из этих новых возможностей.</span><span class="sxs-lookup"><span data-stu-id="4ab51-134">First let’s get some tables, indexes and random data created toopractice some of these new capabilities.</span></span> <span data-ttu-id="4ab51-135">Примеры сценариев TSQL Hello может выполняться в SQL Server 2016 или в базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4ab51-135">hello TSQL script examples can be executed under SQL Server 2016, or under Azure SQL Database.</span></span> <span data-ttu-id="4ab51-136">Тем не менее при создании базы данных Azure SQL, убедитесь, что выберите не hello минимальное P2 базы данных, поскольку требуется по крайней мере несколько ядер tooallow многопоточность и поэтому преимущества этих функций.</span><span class="sxs-lookup"><span data-stu-id="4ab51-136">However, when creating an Azure SQL database, make sure you choose at hello minimum a P2 database because you need at least a couple of cores tooallow multi-threading and therefore benefit from these features.</span></span>

```
-- Create a Premium P2 Database in Azure SQL Database

CREATE DATABASE MyTestDB
    (EDITION=’Premium’, SERVICE_OBJECTIVE=’P2′);
GO

-- Create 2 tables with a column store index on
-- hello second one (only available on Premium databases)

CREATE TABLE T_source
    (Color varchar(10), c1 bigint, c2 bigint);

CREATE TABLE T_target
    (c1 bigint, c2 bigint);

CREATE CLUSTERED COLUMNSTORE INDEX CCI ON T_target;
GO

-- Insert few rows.

INSERT T_source VALUES
    (‘Blue’, RAND() * 100000, RAND() * 100000),
    (‘Yellow’, RAND() * 100000, RAND() * 100000),
    (‘Red’, RAND() * 100000, RAND() * 100000),
    (‘Green’, RAND() * 100000, RAND() * 100000),
    (‘Black’, RAND() * 100000, RAND() * 100000);

GO 200

INSERT T_source SELECT * FROM T_source;

GO 10
```


<span data-ttu-id="4ab51-137">Теперь давайте имеют вид toosome функций обработки запроса hello, поступающих с уровнем совместимости 130.</span><span class="sxs-lookup"><span data-stu-id="4ab51-137">Now, let’s have a look toosome of hello Query Processing features coming with compatibility level 130.</span></span>

## <a name="parallel-insert"></a><span data-ttu-id="4ab51-138">Параллельное выполнение операции INSERT</span><span class="sxs-lookup"><span data-stu-id="4ab51-138">Parallel INSERT</span></span>
<span data-ttu-id="4ab51-139">Выполнение инструкций TSQL hello ниже выполняется hello операции вставки при уровне совместимости 120 и 130, выполняющего соответственно hello операции вставки в одной модели потоков (120), а также в многопоточной модели (130).</span><span class="sxs-lookup"><span data-stu-id="4ab51-139">Executing hello TSQL statements below executes hello INSERT operation under compatibility level 120 and 130, which respectively executes hello INSERT operation in a single threaded model (120), and in a multi-threaded model (130).</span></span>

```
-- Parallel INSERT … SELECT … in heap or CCI
-- is available under 130 only

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO 

-- hello INSERT part is in serial

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130
GO

-- hello INSERT part is in parallel

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

SET STATISTICS XML OFF;
```


<span data-ttu-id="4ab51-140">Запросив план запроса фактический hello hello, просмотрев его графическое представление или его содержимое XML, можно определить, какие функции является играют оценки количества элементов.</span><span class="sxs-lookup"><span data-stu-id="4ab51-140">By requesting hello actual hello query plan, looking at its graphical representation or its XML content, you can determine which Cardinality Estimation function is at play.</span></span> <span data-ttu-id="4ab51-141">Глядя hello планы side-by-side на рисунке 1, четко видно, что hello выполнения вставки хранилища столбца выходит из последовательного в 120 tooparallel в 130.</span><span class="sxs-lookup"><span data-stu-id="4ab51-141">Looking at hello plans side-by-side on figure 1, we can clearly see that hello Column Store INSERT execution goes from serial in 120 tooparallel in 130.</span></span> <span data-ttu-id="4ab51-142">Кроме того Обратите внимание hello изменения значка итератора hello в 130 плана hello отображение параллельных со стрелками, демонстрирующая hello факт, что теперь hello итератора выполнение на самом деле параллельных.</span><span class="sxs-lookup"><span data-stu-id="4ab51-142">Also, note that hello change of hello iterator icon in hello 130 plan showing two parallel arrows, illustrating hello fact that now hello iterator execution is indeed parallel.</span></span> <span data-ttu-id="4ab51-143">При наличии больших toocomplete операций INSERT, параллельное выполнение hello, количество связанных toohello core вами в вашем распоряжении для hello базы данных, увеличивается производительность; копирование tooa 100 раз быстрее, в зависимости от ситуации!</span><span class="sxs-lookup"><span data-stu-id="4ab51-143">If you have large INSERT operations toocomplete, hello parallel execution, linked toohello number of core you have at your disposal for hello database, will perform better; up tooa 100 times faster depending your situation!</span></span>

<span data-ttu-id="4ab51-144">*Рисунок 1: Вставка операции изменения из последовательного tooparallel с уровнем совместимости 130.*</span><span class="sxs-lookup"><span data-stu-id="4ab51-144">*Figure 1: INSERT operation changes from serial tooparallel with compatibility level 130.*</span></span>

![На рисунке 1](./media/sql-database-compatibility-level-query-performance-130/figure-1.jpg)

## <a name="serial-batch-mode"></a><span data-ttu-id="4ab51-146">Последовательный пакетный режим</span><span class="sxs-lookup"><span data-stu-id="4ab51-146">SERIAL Batch Mode</span></span>
<span data-ttu-id="4ab51-147">Аналогичным образом перемещение уровня toocompatibility 130 при обработке строки данных включает пакетную обработку.</span><span class="sxs-lookup"><span data-stu-id="4ab51-147">Similarly, moving toocompatibility level 130 when processing rows of data enables batch mode processing.</span></span> <span data-ttu-id="4ab51-148">Во-первых, выполнение операций в пакетном режиме доступно только при наличии индекса хранилища столбцов.</span><span class="sxs-lookup"><span data-stu-id="4ab51-148">First, batch mode operations  are only available when you have a column store index in place.</span></span> <span data-ttu-id="4ab51-149">Во-вторых пакет обычно представляет ~ 900 строк и использует логику кода, оптимизированный для несколькими ядрами ЦП, пропускную способность памяти, и непосредственно использует hello сжатых данных hello хранилища столбцов, когда это возможно.</span><span class="sxs-lookup"><span data-stu-id="4ab51-149">Second, a batch typically represents ~900 rows, and uses a code logic optimized for multicore CPU, higher memory throughput and directly leverages hello compressed data of hello Column Store whenever possible.</span></span> <span data-ttu-id="4ab51-150">В этих условиях SQL Server 2016 может обрабатывать ~ 900 строк за один раз вместо 1 строку во время hello и как следствие, hello в целом накладные расходы hello операции теперь совместно используется весь пакет hello, уменьшая hello Общая стоимость по строкам.</span><span class="sxs-lookup"><span data-stu-id="4ab51-150">Under these conditions, SQL Server 2016 can process ~900 rows at once, instead of 1 row at hello time, and as a consequence, hello overall overhead cost of hello operation is now shared by hello entire batch, reducing hello overall cost by row.</span></span> <span data-ttu-id="4ab51-151">Этот общий объем вкупе с hello сжатие хранилища столбцов, по сути снижает задержку hello в режиме ВЫБЕРИТЕ пакетной операции.</span><span class="sxs-lookup"><span data-stu-id="4ab51-151">This shared amount of operations combined with hello column store compression basically reduces hello latency involved in a SELECT batch mode operation.</span></span> <span data-ttu-id="4ab51-152">Можно получить дополнительные сведения о хранилище столбцов hello и пакета режиме на [руководство по индексам Columnstore](https://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="4ab51-152">You can find more details about hello column store and batch mode at [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

```
-- Serial batch mode execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT (C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO 

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="4ab51-153">Как видимый ниже просматривая hello запроса планы side-by-side на рис. 2, мы видим, режим обработки hello изменилось с уровнем совместимости hello и вследствие этого, при выполнении запросов hello в обоих уровень совместимости полностью, можно видеть, что большую часть времени обработки hello, затраченное на строки режима (86%) по сравнению toohello пакетный режим (14%), где были обработаны 2 пакетов.</span><span class="sxs-lookup"><span data-stu-id="4ab51-153">As visible below, by observing hello query plans side-by-side on figure 2, we can see that hello processing mode has changed with hello compatibility level, and as a consequence, when executing hello queries in both compatibility level altogether, we can see that most of hello processing time is spent in row mode (86%) compared toohello batch mode (14%), where 2 batches have been processed.</span></span> <span data-ttu-id="4ab51-154">Увеличить hello набора данных, hello преимущество увеличится.</span><span class="sxs-lookup"><span data-stu-id="4ab51-154">Increase hello dataset, hello benefit will increase.</span></span>

<span data-ttu-id="4ab51-155">*Рисунок 2: ВЫБЕРИТЕ режим последовательного toobatch с уровнем совместимости 130 операции изменения.*</span><span class="sxs-lookup"><span data-stu-id="4ab51-155">*Figure 2: SELECT operation changes from serial toobatch mode with compatibility level 130.*</span></span>

![На рис. 2](./media/sql-database-compatibility-level-query-performance-130/figure-2.jpg)

## <a name="batch-mode-on-sort-execution"></a><span data-ttu-id="4ab51-157">Пакетный режим при выполнении сортировки</span><span class="sxs-lookup"><span data-stu-id="4ab51-157">Batch mode on Sort Execution</span></span>
<span data-ttu-id="4ab51-158">Аналогичные toohello выше, но применяется tooa операцию сортировки, hello переход из режима toobatch режиме (при уровне совместимости 120) строки (при уровне совместимости 130) повышает производительность hello hello операция СОРТИРОВКИ для hello те же причины.</span><span class="sxs-lookup"><span data-stu-id="4ab51-158">Similar toohello above, but applied tooa sort operation, hello transition from row mode (compatibility level 120) toobatch mode (compatibility level 130) improves hello performance of hello SORT operation for hello same reasons.</span></span>

```
-- Batch mode on sort execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="4ab51-159">Отображается side-by-side на рис. 3, можно увидеть, операция сортировки hello в режиме "строка" представляет 81% hello затрат, пока hello пакетный режим только представляет % 19 hello затрат (соответственно 81% и % 56 сортировать hello сам).</span><span class="sxs-lookup"><span data-stu-id="4ab51-159">Visible side-by-side on figure 3, we can see that hello sort operation in row mode represents 81% of hello cost, while hello batch mode only represents 19% of hello cost (respectively 81% and 56% on hello sort itself).</span></span>

<span data-ttu-id="4ab51-160">*Рисунок 3: Операция СОРТИРОВКИ изменяет режим toobatch строк с уровнем совместимости 130.*</span><span class="sxs-lookup"><span data-stu-id="4ab51-160">*Figure 3: SORT operation changes from row toobatch mode with compatibility level 130.*</span></span>

![Рис. 3](./media/sql-database-compatibility-level-query-performance-130/figure-3.png)

<span data-ttu-id="4ab51-162">Очевидно, что в этих примерах только содержат десятки тысяч строк, никаких действий при просмотре в наши дни hello данные, доступные в большинство серверов SQL.</span><span class="sxs-lookup"><span data-stu-id="4ab51-162">Obviously, these samples only contain tens of thousands of rows, which is nothing when looking at hello data available in most SQL Servers these days.</span></span> <span data-ttu-id="4ab51-163">Только их к нескольким миллионам строк вместо этого проекта, и это можно легко преобразовать в несколько минут выполнения перенести каждый день, ожидающих hello характер рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="4ab51-163">Just project these against millions of rows instead, and this can translate in several minutes of execution spared every day pending hello nature of your workload.</span></span>

## <a name="cardinality-estimation-ce-improvements"></a><span data-ttu-id="4ab51-164">Улучшение оценки количества элементов</span><span class="sxs-lookup"><span data-stu-id="4ab51-164">Cardinality Estimation (CE) improvements</span></span>
<span data-ttu-id="4ab51-165">Появилась в SQL Server 2014, сделает все базы данных уровня совместимости 120 или выше используйте hello новые возможности для оценки количества элементов.</span><span class="sxs-lookup"><span data-stu-id="4ab51-165">Introduced with SQL Server 2014, any database running at a compatibility level 120 or above will make use of hello new Cardinality Estimation functionality.</span></span> <span data-ttu-id="4ab51-166">По существу оценки количества элементов — использовать логику hello toodetermine, как SQL server выполняет запрос на расчетные затраты на его основе.</span><span class="sxs-lookup"><span data-stu-id="4ab51-166">Essentially, cardinality estimation is hello logic used toodetermine how SQL server will execute a query based on its estimated cost.</span></span> <span data-ttu-id="4ab51-167">Оценка Hello вычисляется с помощью входных данных из статистические данные, связанные с объектами, участвующих в этом запросе.</span><span class="sxs-lookup"><span data-stu-id="4ab51-167">hello estimation is calculated using input from statistics associated with objects involved in that query.</span></span> <span data-ttu-id="4ab51-168">На практике на высоком уровне, функции оценки количества элементов являются оценочными счетчик строк наряду с информацией о распределении hello hello значений счетчиков уникальное значение, и повторяющиеся количество содержащихся в hello таблиц и объектов, указанных в запросе hello.</span><span class="sxs-lookup"><span data-stu-id="4ab51-168">Practically, at a high-level, Cardinality Estimation functions are row count estimates along with information about hello distribution of hello values, distinct value counts, and duplicate counts contained in hello tables and objects referenced in hello query.</span></span> <span data-ttu-id="4ab51-169">Получение этих оценок так, может привести к toounnecessary дискового ввода-вывода из-за выделения памяти tooinsufficient (т. е. сбросы TempDB) или выбор tooa за параллельного выполнения последовательного плана план выполнения, tooname несколько.</span><span class="sxs-lookup"><span data-stu-id="4ab51-169">Getting these estimates wrong, can lead toounnecessary disk I/O due tooinsufficient memory grants (i.e. TempDB spills), or tooa selection of a serial plan execution over a parallel plan execution, tooname a few.</span></span> <span data-ttu-id="4ab51-170">Заключение, неправильное оценки может привести tooan общего снижения производительности выполнения запросов hello.</span><span class="sxs-lookup"><span data-stu-id="4ab51-170">Conclusion, incorrect estimates can lead tooan overall performance degradation of hello query execution.</span></span> <span data-ttu-id="4ab51-171">На hello другой стороне лучше оценивает, более точным оценкам, выполнения запросов интересы toobetter!</span><span class="sxs-lookup"><span data-stu-id="4ab51-171">On hello other side, better estimates, more accurate estimates, leads toobetter query executions!</span></span>

<span data-ttu-id="4ab51-172">Как упоминалось ранее, оптимизации запросов и оценки являются просто, но если вы хотите toolearn Дополнительные сведения о планы запросов и механизм оценки количества элементов, можно ссылаться toohello документ в [оптимизация свои планы запросов с hello SQL Server 2014 Механизм оценки количества элементов](https://msdn.microsoft.com/library/dn673537.aspx) для более подробного изучения.</span><span class="sxs-lookup"><span data-stu-id="4ab51-172">As mentioned before, query optimizations and estimates are a complex matter, but if you want toolearn more about query plans and cardinality estimator, you can refer toohello document at [Optimizing Your Query Plans with hello SQL Server 2014 Cardinality Estimator](https://msdn.microsoft.com/library/dn673537.aspx) for a deeper dive.</span></span>

## <a name="which-cardinality-estimation-do-you-currently-use"></a><span data-ttu-id="4ab51-173">Определение используемой оценки количества элементов</span><span class="sxs-lookup"><span data-stu-id="4ab51-173">Which Cardinality Estimation do you currently use?</span></span>
<span data-ttu-id="4ab51-174">toodetermine, под которой выполняются запросы оценки количества элементов, давайте просто использовать запрос hello примеры ниже.</span><span class="sxs-lookup"><span data-stu-id="4ab51-174">toodetermine under which Cardinality Estimation your queries are running, let’s just use hello query samples below.</span></span> <span data-ttu-id="4ab51-175">Обратите внимание, что в первом примере будет запускаться при уровне совместимости 110, подразумевает использование hello hello старые функции оценки количества элементов.</span><span class="sxs-lookup"><span data-stu-id="4ab51-175">Note that this first example will run under compatibility level 110, implying hello use of hello old Cardinality Estimation functions.</span></span>

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 110;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="4ab51-176">После завершения выполнения, щелкните ссылку XML hello и просмотрите свойства hello hello первый итератора, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="4ab51-176">Once execution is complete, click on hello XML link, and look at hello properties of hello first iterator as shown below.</span></span> <span data-ttu-id="4ab51-177">Имя свойства hello вызывается CardinalityEstimationModelVersion, заданных в настоящее время на 70.</span><span class="sxs-lookup"><span data-stu-id="4ab51-177">Note hello property name called CardinalityEstimationModelVersion currently set on 70.</span></span> <span data-ttu-id="4ab51-178">Это не значит, что hello базы данных имеет уровень совместимости версии SQL Server 7.0 toohello (устанавливается на 110 как видимый в инструкциях TSQL hello выше), но hello значение 70 просто представляет hello кратности функциональные возможности прошлых доступно с версии SQL Сервер 7.0, которых нет основной номер версии до SQL Server 2014 (который поставляется с уровнем совместимости 120).</span><span class="sxs-lookup"><span data-stu-id="4ab51-178">It does not mean that hello database compatibility level is set toohello SQL Server 7.0 version (it is set on 110 as visible in hello TSQL statements above), but hello value 70 simply represents hello legacy Cardinality Estimation functionality available since SQL Server 7.0, which had no major revisions until SQL Server 2014 (which comes with a compatibility level of 120).</span></span>

<span data-ttu-id="4ab51-179">*Рис. 4: hello CardinalityEstimationModelVersion установлено too70, при использовании уровнем совместимости 110 и ниже.*</span><span class="sxs-lookup"><span data-stu-id="4ab51-179">*Figure 4: hello CardinalityEstimationModelVersion is set too70 when using a compatibility level of 110 or below.*</span></span>

![Рис. 4](./media/sql-database-compatibility-level-query-performance-130/figure-4.png)

<span data-ttu-id="4ab51-181">Кроме того, можно изменить too130 уровня совместимости hello и отключить использование hello hello новая функция оценки количества элементов с помощью hello LEGACY_CARDINALITY_ESTIMATION задать tooON с [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx).</span><span class="sxs-lookup"><span data-stu-id="4ab51-181">Alternatively, you can change hello compatibility level too130, and disable hello use of hello new Cardinality Estimation function by using hello LEGACY_CARDINALITY_ESTIMATION set tooON with [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx).</span></span> <span data-ttu-id="4ab51-182">Это будет иметь ровно hello такой же, как с помощью 110 с кратности функция точки зрения, при использовании hello последнего запроса, уровень совместимости обработки.</span><span class="sxs-lookup"><span data-stu-id="4ab51-182">This will be exactly hello same as using 110 from a Cardinality Estimation function point of view, while using hello latest query processing compatibility level.</span></span> <span data-ttu-id="4ab51-183">Таким образом, можно использовать преимущества hello новый запрос, функциях, поступающих с hello последний уровень совместимости (т. е. пакетный режим), но по-прежнему использует Здравствуй, старый функциональные возможности оценки количества элементов при необходимости.</span><span class="sxs-lookup"><span data-stu-id="4ab51-183">Doing so, you can benefit from hello new query processing features coming with hello latest compatibility level (i.e. batch mode), but still rely on hello old Cardinality Estimation functionality if necessary.</span></span>

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="4ab51-184">Просто перемещаются toohello уровня совместимости 120 или 130 позволяет hello новые функциональные возможности оценки количества элементов.</span><span class="sxs-lookup"><span data-stu-id="4ab51-184">Simply moving toohello compatibility level 120 or 130 enables hello new Cardinality Estimation functionality.</span></span> <span data-ttu-id="4ab51-185">В этом случае по умолчанию hello CardinalityEstimationModelVersion задается соответствующим образом too120 или 130 как видимый ниже.</span><span class="sxs-lookup"><span data-stu-id="4ab51-185">In such a case, hello default CardinalityEstimationModelVersion will be set accordingly too120 or 130 as visible below.</span></span>

```
-- New CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="4ab51-186">*Рисунок 5: hello CardinalityEstimationModelVersion установлено too130, при использовании уровень совместимости 130.*</span><span class="sxs-lookup"><span data-stu-id="4ab51-186">*Figure 5: hello CardinalityEstimationModelVersion is set too130 when using a compatibility level of 130.*</span></span>

![Рис. 5](./media/sql-database-compatibility-level-query-performance-130/figure-5.jpg)

## <a name="witnessing-hello-cardinality-estimation-differences"></a><span data-ttu-id="4ab51-188">Witnessing различия hello оценки количества элементов</span><span class="sxs-lookup"><span data-stu-id="4ab51-188">Witnessing hello Cardinality Estimation differences</span></span>
<span data-ttu-id="4ab51-189">Теперь запустим немного более сложная запросов, включающих INNER JOIN с предложением WHERE, и некоторые предикатов и рассмотрим hello предполагаемое число строк из старой кратности функции hello сначала.</span><span class="sxs-lookup"><span data-stu-id="4ab51-189">Now, let’s run a slightly more complex query involving an INNER JOIN with a WHERE clause with some predicates, and let’s look at hello row count estimate from hello old Cardinality Estimation function first.</span></span>

```
-- Old CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="4ab51-190">Для эффективного выполнения этого запроса возвращает 200,704 строки, во время оценки строку hello hello старого функциональность для оценки количества элементов утверждений 194,284 строк.</span><span class="sxs-lookup"><span data-stu-id="4ab51-190">Executing this query effectively returns 200,704 rows, while hello row estimate with hello old Cardinality Estimation functionality claims 194,284 rows.</span></span> <span data-ttu-id="4ab51-191">Очевидно, что как отмечалось ранее, результаты вычислений эти строки также зависят от как часто вы выполняли hello предыдущих примерах, который заполняет таблиц образец hello снова и снова при каждом запуске.</span><span class="sxs-lookup"><span data-stu-id="4ab51-191">Obviously, as said before, these row count results will also depend how often you ran hello previous samples, which populates hello sample tables over and over again at each run.</span></span> <span data-ttu-id="4ab51-192">Очевидно, что предикаты hello в запросе также будет иметь влияет на фактическое оценки hello помимо hello таблицы форму, содержимое данных и как эти данные фактически сопоставлять друг с другом.</span><span class="sxs-lookup"><span data-stu-id="4ab51-192">Obviously, hello predicates in your query will also have an influence on hello actual estimation aside from hello table shape, data content, and how this data actually correlate with each other.</span></span>

<span data-ttu-id="4ab51-193">*Рисунок 6: предполагаемое число строк hello отключено 194,284 или 6 000 строк из ожидаемых 200,704 строк hello.*</span><span class="sxs-lookup"><span data-stu-id="4ab51-193">*Figure 6: hello row count estimate is 194,284 or 6,000 rows off from hello 200,704 rows expected.*</span></span>

![Рис. 6](./media/sql-database-compatibility-level-query-performance-130/figure-6.jpg)

<span data-ttu-id="4ab51-195">В hello аналогичным образом, давайте теперь можно выполнить hello же запрос с новыми возможностями кратности hello.</span><span class="sxs-lookup"><span data-stu-id="4ab51-195">In hello same way, let’s now execute hello same query with hello new Cardinality Estimation functionality.</span></span>

```
-- New CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="4ab51-196">Просматривая ниже hello, теперь видно, что эту оценку строку hello 202,877, или гораздо более подробно и выше, чем hello старого оценки количества элементов.</span><span class="sxs-lookup"><span data-stu-id="4ab51-196">Looking at hello below, we now see that hello row estimate is 202,877, or much closer and higher than hello old Cardinality Estimation.</span></span>

<span data-ttu-id="4ab51-197">*Рисунок 7: предполагаемое число строк hello сейчас 202,877 вместо 194,284.*</span><span class="sxs-lookup"><span data-stu-id="4ab51-197">*Figure 7: hello row count estimate is now 202,877, instead of 194,284.*</span></span>

![Рис. 7](./media/sql-database-compatibility-level-query-performance-130/figure-7.jpg)

<span data-ttu-id="4ab51-199">На самом деле hello результирующий набор будет 200,704 строк (все они зависит, как часто вы запускали hello запросы hello предыдущих примерах, но что более важно, так как hello TSQL использует инструкцию RAND() hello, hello фактические значения, возвращаемые может меняться от одного выполнения toohello далее).</span><span class="sxs-lookup"><span data-stu-id="4ab51-199">In reality, hello result set is 200,704 rows (but all of it depends how often you did run hello queries of hello previous samples, but more importantly, because hello TSQL uses hello RAND() statement, hello actual values returned can vary from one run toohello next).</span></span> <span data-ttu-id="4ab51-200">Таким образом в данном конкретном примере hello Новая оценка кратности возникновения в оценка hello количество строк, так как 202,877 гораздо ближе too200, 704, чем 194,284 задание лучше!</span><span class="sxs-lookup"><span data-stu-id="4ab51-200">Therefore, in this particular example, hello new Cardinality Estimation does a better job at estimating hello number of rows because 202,877 is much closer too200,704, than 194,284!</span></span> <span data-ttu-id="4ab51-201">Наконец, если изменить предложение WHERE предикаты tooequality hello (вместо «>» для экземпляра), это может сделать оценки hello между hello старые и новые функции количества элементов еще более другой, в зависимости от того, сколько результатов можно получить.</span><span class="sxs-lookup"><span data-stu-id="4ab51-201">Last, if you change hello WHERE clause predicates tooequality (rather than “>” for instance), this could make hello estimates between hello old and new Cardinality function even more different, depending on how many matches you can get.</span></span>

<span data-ttu-id="4ab51-202">Очевидно, что в этом случае погрешность в 6000 строк от действительного количества — сравнительно небольшой объем данных в некоторых ситуациях.</span><span class="sxs-lookup"><span data-stu-id="4ab51-202">Obviously, in this case, being ~6000 rows off from actual count does not represent a lot of data in some situations.</span></span> <span data-ttu-id="4ab51-203">Теперь Транспонирование этой toomillions строк на несколько таблиц и более сложные запросы, и во время оценки hello предположительно расходится с миллионами строк и таким образом, hello риск неверный план выполнения, или запрос нехватки памяти предоставляет начальные hello комплектации вверх достигнута максимальная планка tooTempDB и поэтому дополнительные операции ввода-вывода, являются гораздо более высокий.</span><span class="sxs-lookup"><span data-stu-id="4ab51-203">Now, transpose this toomillions of rows across several tables and more complex queries, and at times hello estimate can be off by millions of rows , and therefore, hello risk of picking-up hello wrong execution plan, or requesting insufficient memory grants leading tooTempDB spills, and so more I/O, are much higher.</span></span>

<span data-ttu-id="4ab51-204">Если у вас есть возможность hello, практики это сравнение с наиболее типичных запросов и наборов данных и узнайте, сколько некоторых старых и новых оценок hello повреждены, хотя некоторые просто станут более off условиях hello или некоторые другие просто Подсчет ближе действительного числа toohello строк, фактически извлеченных в hello результирующих наборов.</span><span class="sxs-lookup"><span data-stu-id="4ab51-204">If you have hello opportunity, practice this comparison with your most typical queries and datasets, and see for yourself by how much some of hello old and new estimates are affected, while some could just become more off from hello reality, or some others just simply closer toohello actual row counts actually returned in hello result sets.</span></span> <span data-ttu-id="4ab51-205">Все они будут зависеть от фигуры hello запросов, характеристики базы данных Azure SQL hello, hello характер и размер hello наборов данных и hello статистики о них.</span><span class="sxs-lookup"><span data-stu-id="4ab51-205">All of it will depend of hello shape of your queries, hello Azure SQL database characteristics, hello nature and hello size of your datasets, and hello statistics available about them.</span></span> <span data-ttu-id="4ab51-206">Если вы только что создали вы экземпляр базы данных SQL Azure, hello запроса оптимизатор будет иметь toobuild выполняется знаний с нуля вместо повторное использование статистики, состоящие из предыдущего запроса hello.</span><span class="sxs-lookup"><span data-stu-id="4ab51-206">If you just created your Azure SQL Database instance, hello query optimizer will have toobuild its knowledge from scratch instead of reusing statistics made of hello previous query runs.</span></span> <span data-ttu-id="4ab51-207">Таким образом hello оценки являются очень контекстные и почти конкретные tooevery ситуации сервера и приложения.</span><span class="sxs-lookup"><span data-stu-id="4ab51-207">So, hello estimates are very contextual and almost specific tooevery server and application situation.</span></span> <span data-ttu-id="4ab51-208">Это важный аспект tookeep помнить!</span><span class="sxs-lookup"><span data-stu-id="4ab51-208">It is an important aspect tookeep in mind!</span></span>

## <a name="some-considerations-tootake-into-account"></a><span data-ttu-id="4ab51-209">Некоторые особенности tootake в учетную запись</span><span class="sxs-lookup"><span data-stu-id="4ab51-209">Some considerations tootake into account</span></span>
<span data-ttu-id="4ab51-210">Несмотря на то, что большинство рабочих нагрузок будет полезным hello уровень совместимости 130, прежде чем переходить на уровень совместимости hello для рабочей среды, по сути доступны 3.</span><span class="sxs-lookup"><span data-stu-id="4ab51-210">Although most workloads would benefit from hello compatibility level 130, before you adopting hello compatibility level for your production environment, you basically have 3 options:</span></span>

1. <span data-ttu-id="4ab51-211">Перемещение toocompatibility 130 и увидеть, как работают вещей.</span><span class="sxs-lookup"><span data-stu-id="4ab51-211">You move toocompatibility level 130, and see how things perform.</span></span> <span data-ttu-id="4ab51-212">В случае, если вы заметили регрессий, просто задайте tooits уровень обратной совместимости hello исходный уровень или сохранить 130 и только обратного hello кратности задней toohello устаревший режим (как описано выше, это отдельно решить проблему hello).</span><span class="sxs-lookup"><span data-stu-id="4ab51-212">In case you notice some regressions, you just simply set hello compatibility level back tooits original level, or keep 130, and only reverse hello Cardinality Estimation back toohello legacy mode (As explained above, this alone could address hello issue).</span></span>
2. <span data-ttu-id="4ab51-213">Тщательно проверьте существующие приложения в аналогичные рабочей нагрузки, тонкой настройки и проверка производительности hello перед выходом tooproduction.</span><span class="sxs-lookup"><span data-stu-id="4ab51-213">You thoroughly test your existing applications under similar production load, fine tune, and validate hello performance before going tooproduction.</span></span> <span data-ttu-id="4ab51-214">В случае проблемы такой же, как показано выше, можно всегда вернуться toohello исходный уровень совместимости, или просто отменить hello кратности задней toohello устаревший режим.</span><span class="sxs-lookup"><span data-stu-id="4ab51-214">In case of issues, same as above, you can always go back toohello original compatibility level, or simply reverse hello Cardinality Estimation back toohello legacy mode.</span></span>
3. <span data-ttu-id="4ab51-215">Последний вариант и hello последней tooaddress способом эти вопросы, — хранилище запросов tooleverage hello.</span><span class="sxs-lookup"><span data-stu-id="4ab51-215">As a final option, and hello most recent way tooaddress these questions, is tooleverage hello Query Store.</span></span> <span data-ttu-id="4ab51-216">Это рекомендуемый вариант для современной среды.</span><span class="sxs-lookup"><span data-stu-id="4ab51-216">That’s today’s recommended option!</span></span> <span data-ttu-id="4ab51-217">Анализ hello tooassist запросов в режиме совместимости на уровне 120 или ниже и 130, не рекомендуем вам достаточно toouse хранилище запросов.</span><span class="sxs-lookup"><span data-stu-id="4ab51-217">tooassist hello analysis of your queries under compatibility level 120 or below versus 130, we cannot encourage you enough toouse Query Store.</span></span> <span data-ttu-id="4ab51-218">Хранилище запросов доступен в последнюю версию базы данных SQL Azure V12 hello, и она предназначена toohelp вам в устранении неполадок производительности запроса.</span><span class="sxs-lookup"><span data-stu-id="4ab51-218">Query Store is available with hello latest version of Azure SQL Database V12, and it’s designed toohelp you with query performance troubleshooting.</span></span> <span data-ttu-id="4ab51-219">Hello хранилище запросов можно рассматривать как "черный ящик" данных для базы данных, собирая и предоставляя подробные исторические сведения обо всех запросах.</span><span class="sxs-lookup"><span data-stu-id="4ab51-219">Think of hello Query Store as a flight data recorder for your database collecting and presenting detailed historic information about all queries.</span></span> <span data-ttu-id="4ab51-220">Это значительно упрощает расследований производительности за счет уменьшения времени toodiagnose hello и устранения проблем.</span><span class="sxs-lookup"><span data-stu-id="4ab51-220">This greatly simplifies performance forensics by reducing hello time toodiagnose and resolve issues.</span></span> <span data-ttu-id="4ab51-221">Дополнительные сведения см. в записи блога [Query Store: A flight data recorder for your database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/) (Хранилище данных: черный ящик для базы данных).</span><span class="sxs-lookup"><span data-stu-id="4ab51-221">You can find more information at [Query Store: A flight data recorder for your database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).</span></span>

<span data-ttu-id="4ab51-222">В hello высокого уровня, если уже имеется набор баз данных с уровнем совместимости 120 или ниже и планирование toomove некоторые из них too130, или так как рабочая нагрузка Автоматическая подготовка новых баз данных, которая будет в скором времени станет значение по умолчанию too130, попробуйте Hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="4ab51-222">At hello high-level, if you already have a set of databases running at compatibility level 120 or below, and plan toomove some of them too130, or because your workload automatically provision new databases that will be soon be set by default too130, please consider hello followings:</span></span>

* <span data-ttu-id="4ab51-223">Прежде чем изменять toohello новый уровень совместимости в рабочей среде, включите хранилище запросов.</span><span class="sxs-lookup"><span data-stu-id="4ab51-223">Before changing toohello new compatibility level in production, enable Query Store.</span></span> <span data-ttu-id="4ab51-224">Можно ссылаться слишком[изменить hello режима совместимости базы данных и использование hello хранилище запросов](https://msdn.microsoft.com/library/bb895281.aspx) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="4ab51-224">You can refer too[Change hello Database Compatibility Mode and Use hello Query Store](https://msdn.microsoft.com/library/bb895281.aspx) for more information.</span></span>
* <span data-ttu-id="4ab51-225">Теперь необходимо протестируйте всех критических рабочих нагрузок, использующих репрезентативные данные и запросы рабочей среды и сравните производительность hello произошел, а указанная хранилищем запросов.</span><span class="sxs-lookup"><span data-stu-id="4ab51-225">Next, test all critical workloads using representative data and queries of a production-like environment, and compare hello performance experienced and as reported by Query Store.</span></span> <span data-ttu-id="4ab51-226">При возникновении некоторых регрессии можно определить hello регрессионных запросов с hello хранилище запросов и использовать форсирования планов hello параметр из хранилища запросов (также называемого планирование закрепление).</span><span class="sxs-lookup"><span data-stu-id="4ab51-226">If you experience some regressions, you can identify hello regressed queries with hello Query Store and use hello plan forcing option from Query Store (aka plan pinning).</span></span> <span data-ttu-id="4ab51-227">В этом случае вы точно оставался у hello уровень совместимости 130 и использовать hello бывшая запросов плана предполагается по hello хранилища запросов.</span><span class="sxs-lookup"><span data-stu-id="4ab51-227">In such a case, you definitively stay with hello compatibility level 130, and use hello former query plan as suggested by hello Query Store.</span></span>
* <span data-ttu-id="4ab51-228">Если tooleverage новые функции и возможности базы данных SQL Azure (который работает под управлением SQL Server 2016), но являются конфиденциальных toochanges переведена в режим hello уровень совместимости 130, в качестве последнего средства может можно воспользоваться режимом вынужденного hello обратно уровень совместимости уровень toohello, который подходит для рабочей нагрузки с помощью инструкции ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="4ab51-228">If you want tooleverage new features and capabilities of Azure SQL Database (which is running SQL Server 2016), but are sensitive toochanges brought by hello compatibility level 130, as a last resort, you could consider forcing hello compatibility level back toohello level that suits your workload by using an ALTER DATABASE statement.</span></span> <span data-ttu-id="4ab51-229">Но во-первых, помните, что хранилище запросов плана hello закрепление параметр является наилучшим вариантом, так как не используется 130 по сути остаются на уровне функций hello более раннюю версию SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4ab51-229">But first, be aware that hello Query Store plan pinning option is your best option because not using 130 is basically staying at hello functionality level of an older SQL Server version.</span></span>
* <span data-ttu-id="4ab51-230">При наличии многопользовательских приложений, объединение нескольких баз данных, возможно, она hello необходимые tooupdate подготовки логику tooensure вашей базы данных уровень совместимости согласованность всех баз данных; старые и новые подготовленные признаков.</span><span class="sxs-lookup"><span data-stu-id="4ab51-230">If you have multitenant applications spanning multiple databases, it may be necessary tooupdate hello provisioning logic of your databases tooensure a consistent compatibility level across all databases; old and newly provisioned ones.</span></span> <span data-ttu-id="4ab51-231">Производительность рабочей нагрузки приложения может быть конфиденциальных toohello факт, что некоторые базы данных выполняются на уровнях совместимости разных и таким образом, может потребоваться согласованность на уровне совместимости между любой базы данных в порядке tooprovide hello же интерфейс для работы клиентов tooyour все доски hello.</span><span class="sxs-lookup"><span data-stu-id="4ab51-231">Your application workload performance could be sensitive toohello fact that some databases are running at different compatibility levels, and therefore, compatibility level consistency across any database could be required in order tooprovide hello same experience tooyour customers all across hello board.</span></span> <span data-ttu-id="4ab51-232">Обратите внимание, что это не требование это зависит влияние уровня совместимости hello приложения.</span><span class="sxs-lookup"><span data-stu-id="4ab51-232">Note that it is not a mandate, it really depends on how your application is affected by hello compatibility level.</span></span>
* <span data-ttu-id="4ab51-233">И, наконец, касающиеся hello оценки количества элементов, а так же, как изменение уровня совместимости hello, прежде чем продолжить, в рабочей среде, это рекомендуется tootest рабочей нагрузкой в новые условия toodetermine hello, если приложение использует преимущества Улучшение оценки количества элементов Hello.</span><span class="sxs-lookup"><span data-stu-id="4ab51-233">Last, regarding hello Cardinality Estimation, and just like changing hello compatibility level, before proceeding in production, it is recommended tootest your production workload under hello new conditions toodetermine if your application benefits from hello Cardinality Estimation improvements.</span></span>

## <a name="conclusion"></a><span data-ttu-id="4ab51-234">Заключение</span><span class="sxs-lookup"><span data-stu-id="4ab51-234">Conclusion</span></span>
<span data-ttu-id="4ab51-235">Использование базы данных SQL Azure toobenefit всех возможностей SQL Server 2016 четко повышает вашей выполнения запросов.</span><span class="sxs-lookup"><span data-stu-id="4ab51-235">Using Azure SQL Database toobenefit from all SQL Server 2016 enhancements can clearly improve your query executions.</span></span> <span data-ttu-id="4ab51-236">Все очень просто.</span><span class="sxs-lookup"><span data-stu-id="4ab51-236">Just as-is!</span></span> <span data-ttu-id="4ab51-237">Конечно так же, как любые новые, правильного определения должно производиться toodetermine hello точные условия при которых рабочей нагрузки базы данных работает hello, наилучшим образом.</span><span class="sxs-lookup"><span data-stu-id="4ab51-237">Of course, like any new feature, a proper evaluation must be done toodetermine hello exact conditions under which your database workload operates hello best.</span></span> <span data-ttu-id="4ab51-238">Опыт показывает, что большая часть рабочей нагрузки, ожидаемое tooat бы незаметно при уровне совместимости 130, используя новый запрос, обработка функций и новые оценки количества элементов при этом.</span><span class="sxs-lookup"><span data-stu-id="4ab51-238">Experience shows that most workload are expected tooat least run transparently under compatibility level 130, while leveraging new query processing functions, and new Cardinality Estimation.</span></span> <span data-ttu-id="4ab51-239">Говорят, что, в действительности всегда существуют некоторые исключения и выполнив соответствующие заказа экспертизы является важным оценки toodetermine, насколько вы можете выиграть от этих улучшений.</span><span class="sxs-lookup"><span data-stu-id="4ab51-239">That said, realistically, there are always some exceptions and doing proper due diligence is an important assessment toodetermine how much you can benefit from these enhancements.</span></span> <span data-ttu-id="4ab51-240">И опять же, hello хранилище запросов может быть очень поможет в выполнении!</span><span class="sxs-lookup"><span data-stu-id="4ab51-240">And again, hello Query Store can be of a great help in doing this work!</span></span>

<span data-ttu-id="4ab51-241">По мере развития SQL Azure, можно ожидать уровнем совместимости 140 hello будущих.</span><span class="sxs-lookup"><span data-stu-id="4ab51-241">As SQL Azure evolves, you can expect a compatibility level 140 in hello future.</span></span> <span data-ttu-id="4ab51-242">Тогда мы расскажем о возможностях уровня совместимости 140 так же, как сделали это для уровня совместимости 130.</span><span class="sxs-lookup"><span data-stu-id="4ab51-242">When time is appropriate, we will start talking about what this future compatibility level 140 will bring, just as we briefly discussed here what compatibility level 130 is bringing today.</span></span>

<span data-ttu-id="4ab51-243">На данном этапе не стоит забывать, начиная с июня 2016 года базы данных SQL Azure будет заменен уровень совместимости по умолчанию hello 120 too130 для новых баз данных.</span><span class="sxs-lookup"><span data-stu-id="4ab51-243">For now, let’s not forget, starting June 2016, Azure SQL Database will change hello default compatibility level from 120 too130 for newly created databases.</span></span> <span data-ttu-id="4ab51-244">Помните об этом.</span><span class="sxs-lookup"><span data-stu-id="4ab51-244">Be aware!</span></span>

## <a name="references"></a><span data-ttu-id="4ab51-245">Ссылки</span><span class="sxs-lookup"><span data-stu-id="4ab51-245">References</span></span>
* [<span data-ttu-id="4ab51-246">Новые возможности (компонент Database Engine)</span><span class="sxs-lookup"><span data-stu-id="4ab51-246">What’s New in Database Engine</span></span>](https://msdn.microsoft.com/library/bb510411.aspx#InMemory)
* [<span data-ttu-id="4ab51-247">Запись блога. Query Store: A flight data recorder for your database (Хранилище данных: черный ящик для базы данных). Автор: Борко Новакович (Borko Novakovic). 8 июня 2016 года</span><span class="sxs-lookup"><span data-stu-id="4ab51-247">Blog: Query Store: A flight data recorder for your database, by Borko Novakovic, June 8 2016</span></span>](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)
* [<span data-ttu-id="4ab51-248">Уровень совместимости инструкции ALTER DATABASE (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="4ab51-248">ALTER DATABASE Compatibility Level (Transact-SQL)</span></span>](https://msdn.microsoft.com/library/bb510680.aspx)
* [<span data-ttu-id="4ab51-249">ALTER DATABASE SCOPED CONFIGURATION</span><span class="sxs-lookup"><span data-stu-id="4ab51-249">ALTER DATABASE SCOPED CONFIGURATION</span></span>](https://msdn.microsoft.com/library/mt629158.aspx)
* [<span data-ttu-id="4ab51-250">Compatibility Level 130 for Azure SQL Database V12</span><span class="sxs-lookup"><span data-stu-id="4ab51-250">Compatibility Level 130 for Azure SQL Database V12</span></span>](https://azure.microsoft.com/updates/compatibility-level-130-for-azure-sql-database-v12/)
* [<span data-ttu-id="4ab51-251">Оптимизация свои планы запросов с hello механизм оценки количества элементов SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="4ab51-251">Optimizing Your Query Plans with hello SQL Server 2014 Cardinality Estimator</span></span>](https://msdn.microsoft.com/library/dn673537.aspx)
* [<span data-ttu-id="4ab51-252">Описание индексов columnstore</span><span class="sxs-lookup"><span data-stu-id="4ab51-252">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
* [<span data-ttu-id="4ab51-253">Запись блога. Повышение производительности запросов с использованием уровня совместимости 130 в базе данных SQL Azure. Автор: Ален Лиссуар (Alain Lissoir). 6 мая 2016 года</span><span class="sxs-lookup"><span data-stu-id="4ab51-253">Blog: Improved Query Performance with Compatibility Level 130 in Azure SQL Database, by Alain Lissoir, May 6 2016</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/)

<!--
Improved Query Performance with Compatibility Level 130 in Azure SQL Database

May 6, 2016 by Alain Lissoir (AlainL), on GitHub 'alainlissoir'.

https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/

..... Now, above.
....................
..... Soon, below?

CAPS / MSDN ideally, but instead on ACom:
.. # Assess effects of latest compatibility level on query performance, how to

sql-database-compatibility-level-query-performance-130.md

genemi = MightyPen , 2016-05-20  Friday  17:00pm
-->
