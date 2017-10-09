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
# <a name="distributing-tables-in-sql-data-warehouse"></a><span data-ttu-id="7192c-103">Распределение таблиц в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="7192c-103">Distributing tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="7192c-104">[Обзор][Overview]</span><span class="sxs-lookup"><span data-stu-id="7192c-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="7192c-105">[Типы данных][Data Types]</span><span class="sxs-lookup"><span data-stu-id="7192c-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="7192c-106">[Распределение][Distribute]</span><span class="sxs-lookup"><span data-stu-id="7192c-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="7192c-107">[Индекс][Index]</span><span class="sxs-lookup"><span data-stu-id="7192c-107">[Index][Index]</span></span>
> * <span data-ttu-id="7192c-108">[Секция][Partition]</span><span class="sxs-lookup"><span data-stu-id="7192c-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="7192c-109">[Статистика][Statistics]</span><span class="sxs-lookup"><span data-stu-id="7192c-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="7192c-110">[Временные таблицы][Temporary]</span><span class="sxs-lookup"><span data-stu-id="7192c-110">[Temporary][Temporary]</span></span>
>
>

<span data-ttu-id="7192c-111">Хранилище данных SQL является распределенной системой баз данных с массовой параллельной обработкой (MPP).</span><span class="sxs-lookup"><span data-stu-id="7192c-111">SQL Data Warehouse is a massively parallel processing (MPP) distributed database system.</span></span>  <span data-ttu-id="7192c-112">Распределяя данные и возможности обработки между несколькими узлами, хранилище данных SQL может предложить огромную масштабируемость — намного больше любой единой системы.</span><span class="sxs-lookup"><span data-stu-id="7192c-112">By dividing data and processing capability across multiple nodes, SQL Data Warehouse can offer huge scalability - far beyond any single system.</span></span>  <span data-ttu-id="7192c-113">Выбор способа toodistribute ваши данные в хранилище данных SQL является одним из наиболее важных hello факторы tooachieving оптимальной производительности.</span><span class="sxs-lookup"><span data-stu-id="7192c-113">Deciding how toodistribute your data within your SQL Data Warehouse is one of hello most important factors tooachieving optimal performance.</span></span>   <span data-ttu-id="7192c-114">Hello ключа toooptimal производительности минимизация перемещение данных и в свою очередь перемещения данных ключа toominimizing hello при выборе стратегии распространения правой hello.</span><span class="sxs-lookup"><span data-stu-id="7192c-114">hello key toooptimal performance is minimizing data movement and in turn hello key toominimizing data movement is selecting hello right distribution strategy.</span></span>

## <a name="understanding-data-movement"></a><span data-ttu-id="7192c-115">Основные сведения о перемещении данных</span><span class="sxs-lookup"><span data-stu-id="7192c-115">Understanding data movement</span></span>
<span data-ttu-id="7192c-116">В системе MPP hello данные из каждой таблицы разделяются между несколькими базами данных базовой.</span><span class="sxs-lookup"><span data-stu-id="7192c-116">In an MPP system, hello data from each table is divided across several underlying databases.</span></span>  <span data-ttu-id="7192c-117">Hello наиболее оптимизированные запросы в системе MPP можно просто передать через tooexecute на hello отдельных распределенных баз данных без участия между hello других баз данных.</span><span class="sxs-lookup"><span data-stu-id="7192c-117">hello most optimized queries on an MPP system can simply be passed through tooexecute on hello individual distributed databases with no interaction between hello other databases.</span></span>  <span data-ttu-id="7192c-118">Например, предположим, что у вас есть база данных с данными о продажах, содержащая две таблицы: "Продажи" и "Клиенты".</span><span class="sxs-lookup"><span data-stu-id="7192c-118">For example, let's say you have a database with sales data which contains two tables, sales and customers.</span></span>  <span data-ttu-id="7192c-119">Если имеется запрос, который должен toojoin таблицы customer tooyour таблицу продаж и разделения таблицы клиентов вверх и продаж по номеру клиента размещение каждого клиента в отдельной базе данных, любые запросы, которые соединяют продаж и клиента, могут быть устранены в каждой базы данных, не имея сведений о hello других баз данных.</span><span class="sxs-lookup"><span data-stu-id="7192c-119">If you have a query that needs toojoin your sales table tooyour customer table and you divide both your sales and customer tables up by customer number, putting each customer in a separate database, any queries which join sales and customer can be solved within each database with no knowledge of hello other databases.</span></span>  <span data-ttu-id="7192c-120">Напротив, если разделить данные о продажах по номеру заказа и данных клиента по номеру клиента, затем любая заданная база данных не будет hello соответствующих данных для каждого клиента и, следовательно, если требуется toojoin данных клиента tooyour данные о продажах, потребовалось бы tooget hello данных для каждого заказчика из hello других баз данных.</span><span class="sxs-lookup"><span data-stu-id="7192c-120">In contrast, if you divided your sales data by order number and your customer data by customer number, then any given database will not have hello corresponding data for each customer and thus if you wanted toojoin your sales data tooyour customer data, you would need tooget hello data for each customer from hello other databases.</span></span>  <span data-ttu-id="7192c-121">Во втором примере перемещения данных, должны toooccur toomove hello клиентские данные toohello данные о продажах, так что hello двух таблиц можно объединить.</span><span class="sxs-lookup"><span data-stu-id="7192c-121">In this second example, data movement would need toooccur toomove hello customer data toohello sales data, so that hello two tables can be joined.</span></span>  

<span data-ttu-id="7192c-122">Перемещение данных не всегда плохо, иногда бывает необходимо toosolve запроса.</span><span class="sxs-lookup"><span data-stu-id="7192c-122">Data movement isn't always a bad thing, sometimes it's necessary toosolve a query.</span></span>  <span data-ttu-id="7192c-123">Но избежав его, запрос будет выполняться быстрее.</span><span class="sxs-lookup"><span data-stu-id="7192c-123">But when this extra step can be avoided, naturally your query will run faster.</span></span>  <span data-ttu-id="7192c-124">Перемещение данных в основном происходит при объединении или группировании таблиц.</span><span class="sxs-lookup"><span data-stu-id="7192c-124">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="7192c-125">Часто toodo оба, необходимо, чтобы во время могут потребоваться toooptimize один из сценариев, таких как соединения, вы по-прежнему требуется toohelp перемещения данных, решения для hello другие сценарии, как статистическая обработка.</span><span class="sxs-lookup"><span data-stu-id="7192c-125">Often you need toodo both, so while you may be able toooptimize for one scenario, like a join, you still need data movement toohelp you solve for hello other scenario, like an aggregation.</span></span>  <span data-ttu-id="7192c-126">выяснить, что прием Hello которого требует меньше усилий.</span><span class="sxs-lookup"><span data-stu-id="7192c-126">hello trick is figuring out which is less work.</span></span>  <span data-ttu-id="7192c-127">В большинстве случаев распространение большими таблицами фактов обычно соединяемыми столбца является hello наиболее эффективный способ уменьшения hello большинство перемещения данных.</span><span class="sxs-lookup"><span data-stu-id="7192c-127">In most cases, distributing large fact tables on a commonly joined column is hello most effective method for reducing hello most data movement.</span></span>  <span data-ttu-id="7192c-128">Распределение данных в столбцах соединения происходит намного более распространенным перемещения данных метод tooreduce от распределения данных для столбцов, участвующих в статистическое выражение.</span><span class="sxs-lookup"><span data-stu-id="7192c-128">Distributing data on join columns is a much more common method tooreduce data movement than distributing data on columns involved in an aggregation.</span></span>

## <a name="select-distribution-method"></a><span data-ttu-id="7192c-129">Выбор метода распределения</span><span class="sxs-lookup"><span data-stu-id="7192c-129">Select distribution method</span></span>
<span data-ttu-id="7192c-130">В фоновом hello хранилище данных SQL делит данные на 60 баз данных.</span><span class="sxs-lookup"><span data-stu-id="7192c-130">Behind hello scenes, SQL Data Warehouse divides your data into 60 databases.</span></span>  <span data-ttu-id="7192c-131">Каждая отдельная база данных является связанной tooas **распространения**.</span><span class="sxs-lookup"><span data-stu-id="7192c-131">Each individual database is referred tooas a **distribution**.</span></span>  <span data-ttu-id="7192c-132">При загрузке данных в каждой таблице хранилища данных SQL имеет tooknow как toodivide через эти 60 распределения данных.</span><span class="sxs-lookup"><span data-stu-id="7192c-132">When data is loaded into each table, SQL Data Warehouse has tooknow how toodivide your data across these 60 distributions.</span></span>  

<span data-ttu-id="7192c-133">метод распределения Hello определяется на уровне таблицы hello и в настоящее время существует два варианта:</span><span class="sxs-lookup"><span data-stu-id="7192c-133">hello distribution method is defined at hello table level and currently there are two choices:</span></span>

1. <span data-ttu-id="7192c-134">**Метод циклического перебора** — данные распределяются равномерно, но случайным образом.</span><span class="sxs-lookup"><span data-stu-id="7192c-134">**Round robin** which distribute data evenly but randomly.</span></span>
2. <span data-ttu-id="7192c-135">**Хэш-распределение** — данные распределяются на основе хэширования значений одного столбца.</span><span class="sxs-lookup"><span data-stu-id="7192c-135">**Hash Distributed** which distributes data based on hashing values from a single column</span></span>

<span data-ttu-id="7192c-136">По умолчанию, если не определить способ распространения данных таблицы будут распределяться с помощью hello **циклический перебор** метода распространения.</span><span class="sxs-lookup"><span data-stu-id="7192c-136">By default, when you do not define a data distribution method, your table will be distributed using hello **round robin** distribution method.</span></span>  <span data-ttu-id="7192c-137">Тем не менее, как становятся более сложными, в реализации, будет необходимо с помощью tooconsider **хэш распределенных** таблиц toominimize перемещения данных, который в свою очередь оптимизирует производительность запросов.</span><span class="sxs-lookup"><span data-stu-id="7192c-137">However, as you become more sophisticated in your implementation, you will want tooconsider using **hash distributed** tables toominimize data movement which will in turn optimize query performance.</span></span>

### <a name="round-robin-tables"></a><span data-ttu-id="7192c-138">Таблицы, распределенные по методу циклического перебора</span><span class="sxs-lookup"><span data-stu-id="7192c-138">Round Robin Tables</span></span>
<span data-ttu-id="7192c-139">Существенно как кажется является использование hello циклического способа передачи данных.</span><span class="sxs-lookup"><span data-stu-id="7192c-139">Using hello Round Robin method of distributing data is very much how it sounds.</span></span>  <span data-ttu-id="7192c-140">После загрузки данных в каждой строки просто отправляется toohello Далее распространения.</span><span class="sxs-lookup"><span data-stu-id="7192c-140">As your data is loaded, each row is simply sent toohello next distribution.</span></span>  <span data-ttu-id="7192c-141">Этот метод распространения hello данных будет всегда случайным образом hello данных очень равномерно распределять по всем hello распределений.</span><span class="sxs-lookup"><span data-stu-id="7192c-141">This method of distributing hello data will always randomly distribute hello data very evenly across all of hello distributions.</span></span>  <span data-ttu-id="7192c-142">То есть нет сортировки выполняются во время hello циклический перебор процесс, который помещает данные.</span><span class="sxs-lookup"><span data-stu-id="7192c-142">That is, there is no sorting done during hello round robin process which places your data.</span></span>  <span data-ttu-id="7192c-143">По этой причине циклическое распределение иногда называют случайным хэшем.</span><span class="sxs-lookup"><span data-stu-id="7192c-143">A round robin distribution is sometimes called a random hash for this reason.</span></span>  <span data-ttu-id="7192c-144">С таблицей распределенных циклического нет данных необходимость toounderstand hello.</span><span class="sxs-lookup"><span data-stu-id="7192c-144">With a round-robin distributed table there is no need toounderstand hello data.</span></span>  <span data-ttu-id="7192c-145">По этой причине такие таблицы часто удобно использовать для загрузки.</span><span class="sxs-lookup"><span data-stu-id="7192c-145">For this reason, Round-Robin tables often make good loading targets.</span></span>

<span data-ttu-id="7192c-146">По умолчанию Если вы выбрали метод распространения hello циклического метода распространения будет использоваться.</span><span class="sxs-lookup"><span data-stu-id="7192c-146">By default, if no distribution method is chosen, hello round robin distribution method will be used.</span></span>  <span data-ttu-id="7192c-147">Тем не менее пока циклический перебор таблицы являются легко toouse, поскольку данные распределяются случайным образом на системе hello, это значит, что система hello не могут гарантировать какой распространения каждой строки составляет на.</span><span class="sxs-lookup"><span data-stu-id="7192c-147">However, while round robin tables are easy toouse, because data is randomly distributed across hello system it means that hello system can't guarantee which distribution each row is on.</span></span>  <span data-ttu-id="7192c-148">Как результат, система hello иногда требуется tooinvoke toobetter операции перемещения данных организации данных, прежде чем его можно разрешить запрос.</span><span class="sxs-lookup"><span data-stu-id="7192c-148">As a result, hello system sometimes needs tooinvoke a data movement operation toobetter organize your data before it can resolve a query.</span></span>  <span data-ttu-id="7192c-149">Это дополнительное действие может повлиять на производительность запросов.</span><span class="sxs-lookup"><span data-stu-id="7192c-149">This extra step can slow down your queries.</span></span>

<span data-ttu-id="7192c-150">Рассмотрите возможность использования циклическое распределение для таблицы в hello следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="7192c-150">Consider using Round Robin distribution for your table in hello following scenarios:</span></span>

* <span data-ttu-id="7192c-151">если это простая отправная точка для начала работы;</span><span class="sxs-lookup"><span data-stu-id="7192c-151">When getting started as a simple starting point</span></span>
* <span data-ttu-id="7192c-152">если отсутствует очевидный ключ соединения;</span><span class="sxs-lookup"><span data-stu-id="7192c-152">If there is no obvious joining key</span></span>
* <span data-ttu-id="7192c-153">Если не столбец хорошим кандидатом для распространения hello таблицы хэша</span><span class="sxs-lookup"><span data-stu-id="7192c-153">If there is not good candidate column for hash distributing hello table</span></span>
* <span data-ttu-id="7192c-154">Если hello таблицы не использует общий ключ соединения с другими таблицами</span><span class="sxs-lookup"><span data-stu-id="7192c-154">If hello table does not share a common join key with other tables</span></span>
* <span data-ttu-id="7192c-155">Если соединение hello менее важна, чем другие соединения в запросе hello</span><span class="sxs-lookup"><span data-stu-id="7192c-155">If hello join is less significant than other joins in hello query</span></span>
* <span data-ttu-id="7192c-156">Когда таблица hello является временной промежуточной таблицы</span><span class="sxs-lookup"><span data-stu-id="7192c-156">When hello table is a temporary staging table</span></span>

<span data-ttu-id="7192c-157">Ниже приведены два примера, которые позволяют создать таблицу с распределением по методу циклического перебора.</span><span class="sxs-lookup"><span data-stu-id="7192c-157">Both of these examples will create a Round Robin Table:</span></span>

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
> <span data-ttu-id="7192c-158">Пока что hello по умолчанию табличного типа, в явном виде в DDL считается рекомендуется, чтобы намерения hello таблице макета, снимите флажок tooothers циклического перебора.</span><span class="sxs-lookup"><span data-stu-id="7192c-158">While round robin is hello default table type being explicit in your DDL is considered a best practice so that hello intentions of your table layout are clear tooothers.</span></span>
>
>

### <a name="hash-distributed-tables"></a><span data-ttu-id="7192c-159">Распределяемые по хэшу таблицы</span><span class="sxs-lookup"><span data-stu-id="7192c-159">Hash Distributed Tables</span></span>
<span data-ttu-id="7192c-160">С помощью **хэш распределенных** toodistribute алгоритм таблицы может повысить производительность во многих сценариях за счет уменьшения перемещения данных во время выполнения запроса.</span><span class="sxs-lookup"><span data-stu-id="7192c-160">Using a **Hash distributed** algorithm toodistribute your tables can improve performance for many scenarios by reducing data movement at query time.</span></span>  <span data-ttu-id="7192c-161">Распределенные таблицы — это таблицы, которые разделены между hello хеширования распределенных баз данных с помощью хэш-алгоритма для одного столбца, который нужно установить.</span><span class="sxs-lookup"><span data-stu-id="7192c-161">Hash distributed tables are tables which are divided between hello distributed databases using a hashing algorithm on a single column which you select.</span></span>  <span data-ttu-id="7192c-162">столбец распределения Hello является то, что определяет, как hello данные распределяются между распределенных баз данных.</span><span class="sxs-lookup"><span data-stu-id="7192c-162">hello distribution column is what determines how hello data is divided across your distributed databases.</span></span>  <span data-ttu-id="7192c-163">хэш-функции Hello использует hello распространения столбца tooassign строки toodistributions.</span><span class="sxs-lookup"><span data-stu-id="7192c-163">hello hash function uses hello distribution column tooassign rows toodistributions.</span></span>  <span data-ttu-id="7192c-164">Здравствуйте, алгоритма хэширования и детерминированным полученный распространения.</span><span class="sxs-lookup"><span data-stu-id="7192c-164">hello hashing algorithm and resulting distribution is deterministic.</span></span>  <span data-ttu-id="7192c-165">То есть hello совпадают с hello того же типа данных будет всегда имеет toohello одинаковое распределение.</span><span class="sxs-lookup"><span data-stu-id="7192c-165">That is hello same value with hello same data type will always has toohello same distribution.</span></span>    

<span data-ttu-id="7192c-166">Ниже приведен пример создания таблицы, распределенной по идентификаторам.</span><span class="sxs-lookup"><span data-stu-id="7192c-166">This example will create a table distributed on id:</span></span>

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

## <a name="select-distribution-column"></a><span data-ttu-id="7192c-167">Выбор столбца распределения</span><span class="sxs-lookup"><span data-stu-id="7192c-167">Select distribution column</span></span>
<span data-ttu-id="7192c-168">При выборе слишком**распространять хэш** таблицу, вам потребуется tooselect распространения один столбец.</span><span class="sxs-lookup"><span data-stu-id="7192c-168">When you choose too**hash distribute** a table, you will need tooselect a single distribution column.</span></span>  <span data-ttu-id="7192c-169">При выборе столбца распределения, существует три основных факторов tooconsider.</span><span class="sxs-lookup"><span data-stu-id="7192c-169">When selecting a distribution column, there are three major factors tooconsider.</span></span>  

<span data-ttu-id="7192c-170">Столбец должен соответствовать следующим критериям.</span><span class="sxs-lookup"><span data-stu-id="7192c-170">Select a single column which will:</span></span>

1. <span data-ttu-id="7192c-171">Он должен быть необновляемым.</span><span class="sxs-lookup"><span data-stu-id="7192c-171">Not be updated</span></span>
2. <span data-ttu-id="7192c-172">Он должен распределять данные равномерно, предотвращая их смещение.</span><span class="sxs-lookup"><span data-stu-id="7192c-172">Distribute data evenly, avoiding data skew</span></span>
3. <span data-ttu-id="7192c-173">Минимизация перемещения данных</span><span class="sxs-lookup"><span data-stu-id="7192c-173">Minimize data movement</span></span>

### <a name="select-distribution-column-which-will-not-be-updated"></a><span data-ttu-id="7192c-174">Выбор необновляемого столбца распределения</span><span class="sxs-lookup"><span data-stu-id="7192c-174">Select distribution column which will not be updated</span></span>
<span data-ttu-id="7192c-175">Столбцы распределения являются необновляемыми. Поэтому для этой роли необходимо выбрать столбец со статическими значениями.</span><span class="sxs-lookup"><span data-stu-id="7192c-175">Distribution columns are not updatable, therefore, select a column with static values.</span></span>  <span data-ttu-id="7192c-176">Если столбец, потребуется обновить toobe, это обычно не распространения хорошим кандидатом.</span><span class="sxs-lookup"><span data-stu-id="7192c-176">If a column will need toobe updated, it is generally not a good distribution candidate.</span></span>  <span data-ttu-id="7192c-177">Если есть случай, когда необходимо обновлять столбец распределения, это можно сделать, сначала удалив строку hello и последующей вставке новой строки.</span><span class="sxs-lookup"><span data-stu-id="7192c-177">If there is a case where you must update a distribution column, this can be done by first deleting hello row and then inserting a new row.</span></span>

### <a name="select-distribution-column-which-will-distribute-data-evenly"></a><span data-ttu-id="7192c-178">Выбор столбца распределения, который распределяет данные равномерно</span><span class="sxs-lookup"><span data-stu-id="7192c-178">Select distribution column which will distribute data evenly</span></span>
<span data-ttu-id="7192c-179">Так как только быстро, как его медленных распространения выполняет распределенной системе, он может важные toodivide hello рабочих равномерно распределения hello в порядке выполнения tooachieve балансировки во всей системе hello.</span><span class="sxs-lookup"><span data-stu-id="7192c-179">Since a distributed system performs only as fast as its slowest distribution, it is important toodivide hello work evenly across hello distributions in order tooachieve balanced execution across hello system.</span></span>  <span data-ttu-id="7192c-180">Работа hello разделена на распределенных систем, как Hello основан на где находятся данные hello для каждого распределения.</span><span class="sxs-lookup"><span data-stu-id="7192c-180">hello way hello work is divided on a distributed system is based on where hello data for each distribution lives.</span></span>  <span data-ttu-id="7192c-181">Это делает столбец вправо распределения hello tooselect очень важны для распространения данных hello, чтобы каждого распределения есть равно работы и будет взять hello же toocomplete времени его часть работы hello.</span><span class="sxs-lookup"><span data-stu-id="7192c-181">This makes it very important tooselect hello right distribution column for distributing hello data so that each distribution has equal work and will take hello same time toocomplete its portion of hello work.</span></span>  <span data-ttu-id="7192c-182">Когда рабочие также и распределены по системе hello, hello данных распределяется среди hello распределения.</span><span class="sxs-lookup"><span data-stu-id="7192c-182">When work is well divided across hello system, hello data is balanced across hello distributions.</span></span>  <span data-ttu-id="7192c-183">Если данные распределены неравномерно, это называется **неравномерным распределением данных**.</span><span class="sxs-lookup"><span data-stu-id="7192c-183">When data is not evenly balanced, we call this **data skew**.</span></span>  

<span data-ttu-id="7192c-184">toodivide данные равномерно и избежать наклона данных, необходимо учитывать следующие hello, при выборе столбца распространения:</span><span class="sxs-lookup"><span data-stu-id="7192c-184">toodivide data evenly and avoid data skew, consider hello following when selecting your distribution column:</span></span>

1. <span data-ttu-id="7192c-185">Выберите столбец, содержащий значительное количество различных значений.</span><span class="sxs-lookup"><span data-stu-id="7192c-185">Select a column which contains a significant number of distinct values.</span></span>
2. <span data-ttu-id="7192c-186">Избегайте распределения данных по столбцам, содержащим несколько различных значений.</span><span class="sxs-lookup"><span data-stu-id="7192c-186">Avoid distributing data on columns with a few distinct values.</span></span>
3. <span data-ttu-id="7192c-187">Избегайте распределения данных по столбцам с высоким коэффициентом содержания значений NULL.</span><span class="sxs-lookup"><span data-stu-id="7192c-187">Avoid distributing data on columns with a high frequency of nulls.</span></span>
4. <span data-ttu-id="7192c-188">Не распределяйте данные по столбцам с датами.</span><span class="sxs-lookup"><span data-stu-id="7192c-188">Avoid distributing data on date columns.</span></span>

<span data-ttu-id="7192c-189">Поскольку каждое значение хэшированное too1 60 распределений, равномерное распределение tooachieve требуется tooselect столбцом с высокой степенью уникален и содержит более 60 уникальные значения.</span><span class="sxs-lookup"><span data-stu-id="7192c-189">Since each value is hashed too1 of 60 distributions, tooachieve even distribution you will want tooselect a column that is highly unique and contains more than 60 unique values.</span></span>  <span data-ttu-id="7192c-190">tooillustrate, рассмотрим случай, когда столбец содержит только 40 уникальные значения.</span><span class="sxs-lookup"><span data-stu-id="7192c-190">tooillustrate, consider a case where a column only has 40 unique values.</span></span>  <span data-ttu-id="7192c-191">Если этот столбец был выбран в качестве ключа распределения hello, hello данных для этой таблицы окажется на 40 распределения максимум, оставляя 20 распределения не данными и toodo без обработки.</span><span class="sxs-lookup"><span data-stu-id="7192c-191">If this column was selected as hello distribution key, hello data for that table would land on 40 distributions at most, leaving 20 distributions with no data and no processing toodo.</span></span>  <span data-ttu-id="7192c-192">И наоборот hello других 40 распределениях бы дополнительные toodo работы, что hello данных был равномерно распределять более 60 распределения.</span><span class="sxs-lookup"><span data-stu-id="7192c-192">Conversely, hello other 40 distributions would have more work toodo that if hello data was evenly spread over 60 distributions.</span></span>  <span data-ttu-id="7192c-193">Этот сценарий является примером неравномерного распределения данных.</span><span class="sxs-lookup"><span data-stu-id="7192c-193">This scenario is an example of data skew.</span></span>

<span data-ttu-id="7192c-194">В системе MPP каждого действия запроса ожидает всех распределений toocomplete их доля рабочих hello.</span><span class="sxs-lookup"><span data-stu-id="7192c-194">In MPP system, each query step waits for all distributions toocomplete their share of hello work.</span></span>  <span data-ttu-id="7192c-195">Если одна распространения не выполняет дополнительную работу, чем другие hello, а затем hello ресурс hello других дистрибутивах, которых фактически напрасно как ожидание в занят распространения hello.</span><span class="sxs-lookup"><span data-stu-id="7192c-195">If one distribution is doing more work than hello others, then hello resource of hello other distributions are essentially wasted just waiting on hello busy distribution.</span></span>  <span data-ttu-id="7192c-196">Если работа неравномерно разделена между всеми распределениями, это называется **неравномерным распределением обработки**.</span><span class="sxs-lookup"><span data-stu-id="7192c-196">When work is not evenly spread across all distributions, we call this **processing skew**.</span></span>  <span data-ttu-id="7192c-197">Наклон обработки вызовет toorun запросов медленнее, чем если hello рабочей нагрузки могут быть равномерно распределены по hello распределения.</span><span class="sxs-lookup"><span data-stu-id="7192c-197">Processing skew will cause queries toorun slower than if hello workload can be evenly spread across hello distributions.</span></span>  <span data-ttu-id="7192c-198">Наклон данных вызовет tooprocessing наклона.</span><span class="sxs-lookup"><span data-stu-id="7192c-198">Data skew will lead tooprocessing skew.</span></span>

<span data-ttu-id="7192c-199">Избегайте распространение на высокой допускает значения NULL столбца в соответствии с hello значения null все попадете на hello же распространителя.</span><span class="sxs-lookup"><span data-stu-id="7192c-199">Avoid distributing on highly nullable column as hello null values will all land on hello same distribution.</span></span> <span data-ttu-id="7192c-200">Распространение по столбцу даты также могут вызвать наклона обработки, так как все данные для данной даты будут перемещаться на hello же распространителя.</span><span class="sxs-lookup"><span data-stu-id="7192c-200">Distributing on a date column can also cause processing skew because all data for a given date will land on hello same distribution.</span></span> <span data-ttu-id="7192c-201">Если несколько пользователей выполняются все фильтрации запросов на hello же даты, а затем только 1 60 распределений hello могут быть представлены все действия hello после указанной даты будет только одна распространения.</span><span class="sxs-lookup"><span data-stu-id="7192c-201">If several users are executing queries all filtering on hello same date, then only 1 of hello 60 distributions will be doing all of hello work since a given date will only be on one distribution.</span></span> <span data-ttu-id="7192c-202">В этом случае запросы hello скорее всего будут выполняться медленнее, чем hello данных были равномерно распределять по всем распределений hello 60 раз.</span><span class="sxs-lookup"><span data-stu-id="7192c-202">In this scenario, hello queries will likely run 60 times slower than if hello data were equally spread over all of hello distributions.</span></span>

<span data-ttu-id="7192c-203">Если столбцы не подходит, рассмотрите возможность использования циклического метода распространения hello.</span><span class="sxs-lookup"><span data-stu-id="7192c-203">When no good candidate columns exist, then consider using round robin as hello distribution method.</span></span>

### <a name="select-distribution-column-which-will-minimize-data-movement"></a><span data-ttu-id="7192c-204">Выбор столбца распределения, который минимизирует перемещение данных</span><span class="sxs-lookup"><span data-stu-id="7192c-204">Select distribution column which will minimize data movement</span></span>
<span data-ttu-id="7192c-205">Минимизация перемещения данных, выбрав столбец вправо распределения hello является одним из наиболее важных стратегий hello для оптимизации производительности в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="7192c-205">Minimizing data movement by selecting hello right distribution column is one of hello most important strategies for optimizing performance of your SQL Data Warehouse.</span></span>  <span data-ttu-id="7192c-206">Перемещение данных в основном происходит при объединении или группировании таблиц.</span><span class="sxs-lookup"><span data-stu-id="7192c-206">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="7192c-207">Все столбцы, используемые в предложениях `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` и `HAVING`, **могут** становиться столбцами хэш-распределения.</span><span class="sxs-lookup"><span data-stu-id="7192c-207">Columns used in `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` and `HAVING` clauses all make for **good** hash distribution candidates.</span></span>

<span data-ttu-id="7192c-208">Здравствуйте, с другой стороны, столбцы в hello `WHERE` предложение **не** сделать столбец кандидатов хорошей хэш из-за ограничения котором распределения участвовать в запросе hello, вызывая обработки наклона.</span><span class="sxs-lookup"><span data-stu-id="7192c-208">On hello other hand, columns in hello `WHERE` clause do **not** make for good hash column candidates because they limit which distributions participate in hello query, causing processing skew.</span></span>  <span data-ttu-id="7192c-209">Хорошим примером для столбца, который может быть заманчивой toodistribute на, но часто может вызвать такая обработка наклона — столбец даты.</span><span class="sxs-lookup"><span data-stu-id="7192c-209">A good example of a column which might be tempting toodistribute on, but often can cause this processing skew is a date column.</span></span>

<span data-ttu-id="7192c-210">Вообще говоря при наличии двух большими таблицами фактов часто встречающиеся в соединении вы приобретете hello максимальной производительности путем распределения обе таблицы в одном из столбцов соединения hello.</span><span class="sxs-lookup"><span data-stu-id="7192c-210">Generally speaking, if you have two large fact tables frequently involved in a join, you will gain hello most performance by distributing both tables on one of hello join columns.</span></span>  <span data-ttu-id="7192c-211">Если у вас есть таблицы, не присоединены к домену tooanother большой таблицы фактов, найдите toocolumns, которые часто находятся в hello `GROUP BY` предложения.</span><span class="sxs-lookup"><span data-stu-id="7192c-211">If you have a table that is never joined tooanother large fact table, then look toocolumns that are frequently in hello `GROUP BY` clause.</span></span>

<span data-ttu-id="7192c-212">Существует несколько ключевых критерии, которые должны быть выполнены tooavoid перемещение данных во время соединения.</span><span class="sxs-lookup"><span data-stu-id="7192c-212">There are a few key criteria which must be met tooavoid data movement during a join:</span></span>

1. <span data-ttu-id="7192c-213">Hello таблицам, участвующим в соединении hello должен быть распределен по хэш **один** hello столбцов, участвующих в соединении hello.</span><span class="sxs-lookup"><span data-stu-id="7192c-213">hello tables involved in hello join must be hash distributed on **one** of hello columns participating in hello join.</span></span>
2. <span data-ttu-id="7192c-214">типы данных Hello hello столбцы соединения должны совпадать между обеих таблиц.</span><span class="sxs-lookup"><span data-stu-id="7192c-214">hello data types of hello join columns must match between both tables.</span></span>
3. <span data-ttu-id="7192c-215">Hello столбцы должны быть присоединены с помощью оператора равенства.</span><span class="sxs-lookup"><span data-stu-id="7192c-215">hello columns must be joined with an equals operator.</span></span>
4. <span data-ttu-id="7192c-216">Hello соединения тип не может быть `CROSS JOIN`.</span><span class="sxs-lookup"><span data-stu-id="7192c-216">hello join type may not be a `CROSS JOIN`.</span></span>

## <a name="troubleshooting-data-skew"></a><span data-ttu-id="7192c-217">Устранение смещения данных</span><span class="sxs-lookup"><span data-stu-id="7192c-217">Troubleshooting data skew</span></span>
<span data-ttu-id="7192c-218">При распространении данных таблицы с помощью метода распространения хэш hello, существует возможность того, что некоторые дистрибутивы будет синхронизована toohave непропорционально больше данных, чем другие.</span><span class="sxs-lookup"><span data-stu-id="7192c-218">When table data is distributed using hello hash distribution method there is a chance that some distributions will be skewed toohave disproportionately more data than others.</span></span> <span data-ttu-id="7192c-219">Наклон излишнего данных может повлиять на производительность запроса, так как конечный результат hello распределенный запрос должен ожидать hello наиболее долго выполняющегося распространения toofinish.</span><span class="sxs-lookup"><span data-stu-id="7192c-219">Excessive data skew can impact query performance because hello final result of a distributed query must wait for hello longest running distribution toofinish.</span></span> <span data-ttu-id="7192c-220">В зависимости от степени hello наклона, может потребоваться tooaddress данных hello его.</span><span class="sxs-lookup"><span data-stu-id="7192c-220">Depending on hello degree of hello data skew you might need tooaddress it.</span></span>

### <a name="identifying-skew"></a><span data-ttu-id="7192c-221">Определение смещения данных</span><span class="sxs-lookup"><span data-stu-id="7192c-221">Identifying skew</span></span>
<span data-ttu-id="7192c-222">Простой способ tooidentify таблицы как неравномерным — toouse `DBCC PDW_SHOWSPACEUSED`.</span><span class="sxs-lookup"><span data-stu-id="7192c-222">A simple way tooidentify a table as skewed is toouse `DBCC PDW_SHOWSPACEUSED`.</span></span>  <span data-ttu-id="7192c-223">Это очень быстрый и простой способ toosee hello число строк таблицы, которые хранятся в каждом распределений hello 60 базы данных.</span><span class="sxs-lookup"><span data-stu-id="7192c-223">This is a very quick and simple way toosee hello number of table rows that are stored in each of hello 60 distributions of your database.</span></span>  <span data-ttu-id="7192c-224">Помните, что для производительности наиболее балансировки hello hello строк в таблице распределенных должны вводиться равномерно в все распределения hello.</span><span class="sxs-lookup"><span data-stu-id="7192c-224">Remember that for hello most balanced performance, hello rows in your distributed table should be spread evenly across all hello distributions.</span></span>

```sql
-- Find data skew for a distributed table
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

<span data-ttu-id="7192c-225">Тем не менее если запрос hello хранилище данных SQL Azure динамические административные представления (DMV) можно выполнить более глубокий анализ.</span><span class="sxs-lookup"><span data-stu-id="7192c-225">However, if you query hello Azure SQL Data Warehouse dynamic management views (DMV) you can perform a more detailed analysis.</span></span>  <span data-ttu-id="7192c-226">toostart, создание представления "hello" [dbo.vTableSizes] [ dbo.vTableSizes] просмотреть с помощью hello SQL из [Общие сведения о таблицах] [ Overview] статьи.</span><span class="sxs-lookup"><span data-stu-id="7192c-226">toostart, create hello view [dbo.vTableSizes][dbo.vTableSizes] view using hello SQL from [Table Overview][Overview] article.</span></span>  <span data-ttu-id="7192c-227">После создания представления hello выполните этот запрос tooidentify, таблицы, для которых не более 10% данных наклон.</span><span class="sxs-lookup"><span data-stu-id="7192c-227">Once hello view is created, run this query tooidentify which tables have more than 10% data skew.</span></span>

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

### <a name="resolving-data-skew"></a><span data-ttu-id="7192c-228">Устранение неравномерности данных</span><span class="sxs-lookup"><span data-stu-id="7192c-228">Resolving data skew</span></span>
<span data-ttu-id="7192c-229">Не все наклона было достаточно toowarrant.</span><span class="sxs-lookup"><span data-stu-id="7192c-229">Not all skew is enough toowarrant a fix.</span></span>  <span data-ttu-id="7192c-230">В некоторых случаях hello производительности таблицы в некоторые запросы могут перевесить hello повреждений данных наклона.</span><span class="sxs-lookup"><span data-stu-id="7192c-230">In some cases, hello performance of a table in some queries can outweigh hello harm of data skew.</span></span>  <span data-ttu-id="7192c-231">toodecide, если необходимо разрешить данные наклон в таблице, необходимо понимать как можно больше об объемах данных hello и запросы в рабочей нагрузке.</span><span class="sxs-lookup"><span data-stu-id="7192c-231">toodecide if you should resolve data skew in a table, you should understand as much as possible about hello data volumes and queries in your workload.</span></span>   <span data-ttu-id="7192c-232">Одним из способов toolook на hello влияние наклон — toouse hello инструкциям hello [мониторинг запросов] [ Query Monitoring] статью влияние hello toomonitor наклона на производительность запросов и специально hello влияние toohow длительных запросов. Отключите toocomplete на отдельные распределения hello.</span><span class="sxs-lookup"><span data-stu-id="7192c-232">One way toolook at hello impact of skew is toouse hello steps in hello [Query Monitoring][Query Monitoring] article toomonitor hello impact of skew on query performance and specifically hello impact toohow long queries take toocomplete on hello individual distributions.</span></span>

<span data-ttu-id="7192c-233">Распределение данных зависит от поиск hello баланс между минимизация Рассогласование данных и минимизации перемещения данных.</span><span class="sxs-lookup"><span data-stu-id="7192c-233">Distributing data is a matter of finding hello right balance between minimizing data skew and minimizing data movement.</span></span> <span data-ttu-id="7192c-234">Они могут противоположных целей и иногда необходимо tookeep данных наклона при перемещении данных tooreduce заказа.</span><span class="sxs-lookup"><span data-stu-id="7192c-234">These can be opposing goals, and sometimes you will want tookeep data skew in order tooreduce data movement.</span></span> <span data-ttu-id="7192c-235">Например если столбец распределения hello часто hello общего столбца соединения и агрегаты, вы будет минимизацию перемещения данных.</span><span class="sxs-lookup"><span data-stu-id="7192c-235">For example, when hello distribution column is frequently hello shared column in joins and aggregations, you will be minimizing data movement.</span></span> <span data-ttu-id="7192c-236">Hello преимущество наличия перемещения минимальными данными hello способны перевесить издержки расхода последствия hello к искажению данных.</span><span class="sxs-lookup"><span data-stu-id="7192c-236">hello benefit of having hello minimal data movement might outweigh hello impact of having data skew.</span></span>

<span data-ttu-id="7192c-237">типичный способ Hello разница в показаниях данных tooresolve: toore-создать hello таблицу со столбцом иное распределение.</span><span class="sxs-lookup"><span data-stu-id="7192c-237">hello typical way tooresolve data skew is toore-create hello table with a different distribution column.</span></span> <span data-ttu-id="7192c-238">Поскольку нет способа столбец распределения hello toochange на существующем, hello способом toochange hello распределение таблиц таблицы его toorecreate его с [CTAS] [].</span><span class="sxs-lookup"><span data-stu-id="7192c-238">Since there is no way toochange hello distribution column on an existing table, hello way toochange hello distribution of a table it toorecreate it with a [CTAS][].</span></span>  <span data-ttu-id="7192c-239">Смещение данных можно устранить двумя способами.</span><span class="sxs-lookup"><span data-stu-id="7192c-239">Here are two examples of how resolve data skew:</span></span>

### <a name="example-1-re-create-hello-table-with-a-new-distribution-column"></a><span data-ttu-id="7192c-240">Пример 1: Создать повторно таблицу hello с новый столбец распределения</span><span class="sxs-lookup"><span data-stu-id="7192c-240">Example 1: Re-create hello table with a new distribution column</span></span>
<span data-ttu-id="7192c-241">В этом примере используется toore [CTAS] []-создать таблицу со столбцом распространения другой хэш.</span><span class="sxs-lookup"><span data-stu-id="7192c-241">This example uses [CTAS][] toore-create a table with a different hash distribution column.</span></span>

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

### <a name="example-2-re-create-hello-table-using-round-robin-distribution"></a><span data-ttu-id="7192c-242">Пример 2: Создать повторно таблицу hello, с использованием циклического распределения</span><span class="sxs-lookup"><span data-stu-id="7192c-242">Example 2: Re-create hello table using round robin distribution</span></span>
<span data-ttu-id="7192c-243">В этом примере используется toore [CTAS] []-создать таблицу с циклическим перебором вместо хэш-распределения.</span><span class="sxs-lookup"><span data-stu-id="7192c-243">This example uses [CTAS][] toore-create a table with round robin instead of a hash distribution.</span></span> <span data-ttu-id="7192c-244">Это изменение вызовет распространения даже данные по цене hello перемещения данных.</span><span class="sxs-lookup"><span data-stu-id="7192c-244">This change will produce even data distribution at hello cost of increased data movement.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="7192c-245">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7192c-245">Next steps</span></span>
<span data-ttu-id="7192c-246">toolearn более о таблице, в разделе hello [распределить][Distribute], [индекс][Index], [секции] [ Partition], [Типы данных][Data Types], [статистики] [ Statistics] и [временных таблиц] [ Temporary] статей.</span><span class="sxs-lookup"><span data-stu-id="7192c-246">toolearn more about table design, see hello [Distribute][Distribute], [Index][Index], [Partition][Partition], [Data Types][Data Types], [Statistics][Statistics] and [Temporary Tables][Temporary] articles.</span></span>

<span data-ttu-id="7192c-247">Обзор рекомендаций по использованию приведен в статье [Рекомендации по использованию хранилища данных SQL Azure][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="7192c-247">For an overview of best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
