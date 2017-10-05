---
title: "Распределение таблиц в хранилище данных SQL | Документация Майкрософт"
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
ms.openlocfilehash: d0e12bf821a81826a20b8db84e76c48fa60ad9b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="distributing-tables-in-sql-data-warehouse"></a><span data-ttu-id="45ddf-103">Распределение таблиц в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="45ddf-103">Distributing tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="45ddf-104">[Обзор][Overview]</span><span class="sxs-lookup"><span data-stu-id="45ddf-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="45ddf-105">[Типы данных][Data Types]</span><span class="sxs-lookup"><span data-stu-id="45ddf-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="45ddf-106">[Распределение][Distribute]</span><span class="sxs-lookup"><span data-stu-id="45ddf-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="45ddf-107">[Индекс][Index]</span><span class="sxs-lookup"><span data-stu-id="45ddf-107">[Index][Index]</span></span>
> * <span data-ttu-id="45ddf-108">[Секция][Partition]</span><span class="sxs-lookup"><span data-stu-id="45ddf-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="45ddf-109">[Статистика][Statistics]</span><span class="sxs-lookup"><span data-stu-id="45ddf-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="45ddf-110">[Временные таблицы][Temporary]</span><span class="sxs-lookup"><span data-stu-id="45ddf-110">[Temporary][Temporary]</span></span>
>
>

<span data-ttu-id="45ddf-111">Хранилище данных SQL является распределенной системой баз данных с массовой параллельной обработкой (MPP).</span><span class="sxs-lookup"><span data-stu-id="45ddf-111">SQL Data Warehouse is a massively parallel processing (MPP) distributed database system.</span></span>  <span data-ttu-id="45ddf-112">Распределяя данные и возможности обработки между несколькими узлами, хранилище данных SQL может предложить огромную масштабируемость — намного больше любой единой системы.</span><span class="sxs-lookup"><span data-stu-id="45ddf-112">By dividing data and processing capability across multiple nodes, SQL Data Warehouse can offer huge scalability - far beyond any single system.</span></span>  <span data-ttu-id="45ddf-113">Выбор метода распределения данных в хранилище данных SQL — один из наиболее важных факторов достижения оптимальной производительности.</span><span class="sxs-lookup"><span data-stu-id="45ddf-113">Deciding how to distribute your data within your SQL Data Warehouse is one of the most important factors to achieving optimal performance.</span></span>   <span data-ttu-id="45ddf-114">Для достижения оптимальной производительности требуется минимизировать перемещение данных. В свою очередь, для последнего необходимо выбрать подходящий метод распределения.</span><span class="sxs-lookup"><span data-stu-id="45ddf-114">The key to optimal performance is minimizing data movement and in turn the key to minimizing data movement is selecting the right distribution strategy.</span></span>

## <a name="understanding-data-movement"></a><span data-ttu-id="45ddf-115">Основные сведения о перемещении данных</span><span class="sxs-lookup"><span data-stu-id="45ddf-115">Understanding data movement</span></span>
<span data-ttu-id="45ddf-116">В системе MPP данные из каждой таблицы разделяются между несколькими основными базами данных.</span><span class="sxs-lookup"><span data-stu-id="45ddf-116">In an MPP system, the data from each table is divided across several underlying databases.</span></span>  <span data-ttu-id="45ddf-117">Наиболее эффективно запросы в системе MPP выполняются в отдельных распределенных базах данных, которые не взаимодействуют с другими базами данных.</span><span class="sxs-lookup"><span data-stu-id="45ddf-117">The most optimized queries on an MPP system can simply be passed through to execute on the individual distributed databases with no interaction between the other databases.</span></span>  <span data-ttu-id="45ddf-118">Например, предположим, что у вас есть база данных с данными о продажах, содержащая две таблицы: "Продажи" и "Клиенты".</span><span class="sxs-lookup"><span data-stu-id="45ddf-118">For example, let's say you have a database with sales data which contains two tables, sales and customers.</span></span>  <span data-ttu-id="45ddf-119">Если необходимо выполнить запрос на соединение таблиц "Продажи" и "Клиенты", одновременно разделив их по номеру клиента и поместив каждого в отдельную базу данных, этот запрос будет выполняться отдельно в каждой базе данных. При этом в них не будет сведений о других базах данных.</span><span class="sxs-lookup"><span data-stu-id="45ddf-119">If you have a query that needs to join your sales table to your customer table and you divide both your sales and customer tables up by customer number, putting each customer in a separate database, any queries which join sales and customer can be solved within each database with no knowledge of the other databases.</span></span>  <span data-ttu-id="45ddf-120">В то же время, если разделить данные о продажах по номеру заказа, а данные о клиентах по номеру клиента, то любая база данных не будет содержать соответствующие данные о клиенте. Следовательно, чтобы объединить данные о продажах и данные о клиентах, необходимо получить данные о каждом клиенте из других баз данных.</span><span class="sxs-lookup"><span data-stu-id="45ddf-120">In contrast, if you divided your sales data by order number and your customer data by customer number, then any given database will not have the corresponding data for each customer and thus if you wanted to join your sales data to your customer data, you would need to get the data for each customer from the other databases.</span></span>  <span data-ttu-id="45ddf-121">Во втором примере для объединения данных о продажах и данных о клиентах, а в результате и самих таблиц, в которых они находятся, требуется выполнить перемещение данных.</span><span class="sxs-lookup"><span data-stu-id="45ddf-121">In this second example, data movement would need to occur to move the customer data to the sales data, so that the two tables can be joined.</span></span>  

<span data-ttu-id="45ddf-122">Перемещение данных — не всегда отрицательный момент. Иногда этот процесс требуется для выполнения запроса.</span><span class="sxs-lookup"><span data-stu-id="45ddf-122">Data movement isn't always a bad thing, sometimes it's necessary to solve a query.</span></span>  <span data-ttu-id="45ddf-123">Но избежав его, запрос будет выполняться быстрее.</span><span class="sxs-lookup"><span data-stu-id="45ddf-123">But when this extra step can be avoided, naturally your query will run faster.</span></span>  <span data-ttu-id="45ddf-124">Перемещение данных в основном происходит при объединении или группировании таблиц.</span><span class="sxs-lookup"><span data-stu-id="45ddf-124">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="45ddf-125">Очень часто требуется выполнить и то, и другое. Вы можете избежать перемещения данных для оптимизации одного сценария (например, соединения), но оно может понадобиться для выполнения другого действия (например, группирования).</span><span class="sxs-lookup"><span data-stu-id="45ddf-125">Often you need to do both, so while you may be able to optimize for one scenario, like a join, you still need data movement to help you solve for the other scenario, like an aggregation.</span></span>  <span data-ttu-id="45ddf-126">Нужно понять, какой процесс требует меньше ресурсов и времени.</span><span class="sxs-lookup"><span data-stu-id="45ddf-126">The trick is figuring out which is less work.</span></span>  <span data-ttu-id="45ddf-127">В большинстве случаев один из самых эффективных методов минимизации перемещения данных заключается в распределении больших таблиц фактов по столбцу соединения.</span><span class="sxs-lookup"><span data-stu-id="45ddf-127">In most cases, distributing large fact tables on a commonly joined column is the most effective method for reducing the most data movement.</span></span>  <span data-ttu-id="45ddf-128">Чаще всего распределение данных по столбцам соединения является более эффективным методом минимизации перемещения данных, чем распределение их по столбцам, задействованным в группировании.</span><span class="sxs-lookup"><span data-stu-id="45ddf-128">Distributing data on join columns is a much more common method to reduce data movement than distributing data on columns involved in an aggregation.</span></span>

## <a name="select-distribution-method"></a><span data-ttu-id="45ddf-129">Выбор метода распределения</span><span class="sxs-lookup"><span data-stu-id="45ddf-129">Select distribution method</span></span>
<span data-ttu-id="45ddf-130">Хранилище данных SQL по умолчанию разделяет данные по 60 базам данных.</span><span class="sxs-lookup"><span data-stu-id="45ddf-130">Behind the scenes, SQL Data Warehouse divides your data into 60 databases.</span></span>  <span data-ttu-id="45ddf-131">Каждая отдельная база данных называется **распределением**.</span><span class="sxs-lookup"><span data-stu-id="45ddf-131">Each individual database is referred to as a **distribution**.</span></span>  <span data-ttu-id="45ddf-132">После загрузки данных в каждую таблицу в хранилище данных SQL необходимо определить метод разделения данных по этим 60 распределениям.</span><span class="sxs-lookup"><span data-stu-id="45ddf-132">When data is loaded into each table, SQL Data Warehouse has to know how to divide your data across these 60 distributions.</span></span>  

<span data-ttu-id="45ddf-133">Метод распределения определяется на уровне таблицы. В настоящее время таких методов два:</span><span class="sxs-lookup"><span data-stu-id="45ddf-133">The distribution method is defined at the table level and currently there are two choices:</span></span>

1. <span data-ttu-id="45ddf-134">**Метод циклического перебора** — данные распределяются равномерно, но случайным образом.</span><span class="sxs-lookup"><span data-stu-id="45ddf-134">**Round robin** which distribute data evenly but randomly.</span></span>
2. <span data-ttu-id="45ddf-135">**Хэш-распределение** — данные распределяются на основе хэширования значений одного столбца.</span><span class="sxs-lookup"><span data-stu-id="45ddf-135">**Hash Distributed** which distributes data based on hashing values from a single column</span></span>

<span data-ttu-id="45ddf-136">Если метод распределения данных не выбран, по умолчанию для таблицы используется метод **циклического перебора** .</span><span class="sxs-lookup"><span data-stu-id="45ddf-136">By default, when you do not define a data distribution method, your table will be distributed using the **round robin** distribution method.</span></span>  <span data-ttu-id="45ddf-137">Однако когда вы усовершенствуете навыки работы с хранилищем данных, вы сможете минимизировать перемещение данных для оптимизации производительности запросов, используя **хэш-распределение** таблиц.</span><span class="sxs-lookup"><span data-stu-id="45ddf-137">However, as you become more sophisticated in your implementation, you will want to consider using **hash distributed** tables to minimize data movement which will in turn optimize query performance.</span></span>

### <a name="round-robin-tables"></a><span data-ttu-id="45ddf-138">Таблицы, распределенные по методу циклического перебора</span><span class="sxs-lookup"><span data-stu-id="45ddf-138">Round Robin Tables</span></span>
<span data-ttu-id="45ddf-139">Таблицы, распределенные по методу циклического перебора, соответствуют своему названию.</span><span class="sxs-lookup"><span data-stu-id="45ddf-139">Using the Round Robin method of distributing data is very much how it sounds.</span></span>  <span data-ttu-id="45ddf-140">После загрузки данных каждая строка отправляется в следующее распределение.</span><span class="sxs-lookup"><span data-stu-id="45ddf-140">As your data is loaded, each row is simply sent to the next distribution.</span></span>  <span data-ttu-id="45ddf-141">При применении циклического перебора данные всегда равномерно распределяются между всеми распределениями случайным образом.</span><span class="sxs-lookup"><span data-stu-id="45ddf-141">This method of distributing the data will always randomly distribute the data very evenly across all of the distributions.</span></span>  <span data-ttu-id="45ddf-142">Это значит, что данные, распределенные по этому методу, не сортируются.</span><span class="sxs-lookup"><span data-stu-id="45ddf-142">That is, there is no sorting done during the round robin process which places your data.</span></span>  <span data-ttu-id="45ddf-143">По этой причине циклическое распределение иногда называют случайным хэшем.</span><span class="sxs-lookup"><span data-stu-id="45ddf-143">A round robin distribution is sometimes called a random hash for this reason.</span></span>  <span data-ttu-id="45ddf-144">При использовании таблицы с распределением по методу циклического перебора не нужно анализировать используемые данные.</span><span class="sxs-lookup"><span data-stu-id="45ddf-144">With a round-robin distributed table there is no need to understand the data.</span></span>  <span data-ttu-id="45ddf-145">По этой причине такие таблицы часто удобно использовать для загрузки.</span><span class="sxs-lookup"><span data-stu-id="45ddf-145">For this reason, Round-Robin tables often make good loading targets.</span></span>

<span data-ttu-id="45ddf-146">Если метод распределения данных не выбран, по умолчанию используется метод циклического перебора.</span><span class="sxs-lookup"><span data-stu-id="45ddf-146">By default, if no distribution method is chosen, the round robin distribution method will be used.</span></span>  <span data-ttu-id="45ddf-147">Таблицы с распределением по методу циклического перебора удобно использовать, так как данные распределяются по системе случайным образом. Однако система не может гарантировать, в каком распределении будет находиться каждая строка.</span><span class="sxs-lookup"><span data-stu-id="45ddf-147">However, while round robin tables are easy to use, because data is randomly distributed across the system it means that the system can't guarantee which distribution each row is on.</span></span>  <span data-ttu-id="45ddf-148">Таким образом, чтобы упорядочить данные перед разрешением запроса, системе иногда требуется вызывать операции перемещения данных.</span><span class="sxs-lookup"><span data-stu-id="45ddf-148">As a result, the system sometimes needs to invoke a data movement operation to better organize your data before it can resolve a query.</span></span>  <span data-ttu-id="45ddf-149">Это дополнительное действие может повлиять на производительность запросов.</span><span class="sxs-lookup"><span data-stu-id="45ddf-149">This extra step can slow down your queries.</span></span>

<span data-ttu-id="45ddf-150">Рассмотрите возможность использования циклического распределения для таблицы в следующих сценариях:</span><span class="sxs-lookup"><span data-stu-id="45ddf-150">Consider using Round Robin distribution for your table in the following scenarios:</span></span>

* <span data-ttu-id="45ddf-151">если это простая отправная точка для начала работы;</span><span class="sxs-lookup"><span data-stu-id="45ddf-151">When getting started as a simple starting point</span></span>
* <span data-ttu-id="45ddf-152">если отсутствует очевидный ключ соединения;</span><span class="sxs-lookup"><span data-stu-id="45ddf-152">If there is no obvious joining key</span></span>
* <span data-ttu-id="45ddf-153">если отсутствует подходящий для хэш-распределения таблицы столбец;</span><span class="sxs-lookup"><span data-stu-id="45ddf-153">If there is not good candidate column for hash distributing the table</span></span>
* <span data-ttu-id="45ddf-154">если таблица не использует общий ключ соединения с другими таблицами;</span><span class="sxs-lookup"><span data-stu-id="45ddf-154">If the table does not share a common join key with other tables</span></span>
* <span data-ttu-id="45ddf-155">Если соединение менее важно, чем других соединения в запросе.</span><span class="sxs-lookup"><span data-stu-id="45ddf-155">If the join is less significant than other joins in the query</span></span>
* <span data-ttu-id="45ddf-156">если таблица является временной.</span><span class="sxs-lookup"><span data-stu-id="45ddf-156">When the table is a temporary staging table</span></span>

<span data-ttu-id="45ddf-157">Ниже приведены два примера, которые позволяют создать таблицу с распределением по методу циклического перебора.</span><span class="sxs-lookup"><span data-stu-id="45ddf-157">Both of these examples will create a Round Robin Table:</span></span>

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
> <span data-ttu-id="45ddf-158">Хотя циклический перебор используется по умолчанию, предпочтительно, чтобы тип таблицы был явно указан в DDL. Таким образом, все будут видеть предназначение макета таблицы.</span><span class="sxs-lookup"><span data-stu-id="45ddf-158">While round robin is the default table type being explicit in your DDL is considered a best practice so that the intentions of your table layout are clear to others.</span></span>
>
>

### <a name="hash-distributed-tables"></a><span data-ttu-id="45ddf-159">Распределяемые по хэшу таблицы</span><span class="sxs-lookup"><span data-stu-id="45ddf-159">Hash Distributed Tables</span></span>
<span data-ttu-id="45ddf-160">Использование **хэш-алгоритма** для распределения данных в таблицах позволяет повысить производительность во многих сценариях благодаря снижению перемещения данных во время выполнения запроса.</span><span class="sxs-lookup"><span data-stu-id="45ddf-160">Using a **Hash distributed** algorithm to distribute your tables can improve performance for many scenarios by reducing data movement at query time.</span></span>  <span data-ttu-id="45ddf-161">Распределяемые по хэшу таблицы разделяются между распределенными базами данных с помощью хэш-алгоритма по одному выбранному столбцу.</span><span class="sxs-lookup"><span data-stu-id="45ddf-161">Hash distributed tables are tables which are divided between the distributed databases using a hashing algorithm on a single column which you select.</span></span>  <span data-ttu-id="45ddf-162">Столбец распределения определят метод разделения данных по распределенным базам данных.</span><span class="sxs-lookup"><span data-stu-id="45ddf-162">The distribution column is what determines how the data is divided across your distributed databases.</span></span>  <span data-ttu-id="45ddf-163">Этот столбец используется в хэш-функции для назначения строк распределениям.</span><span class="sxs-lookup"><span data-stu-id="45ddf-163">The hash function uses the distribution column to assign rows to distributions.</span></span>  <span data-ttu-id="45ddf-164">Алгоритм хэширования и итоговое распределение являются детерминированными.</span><span class="sxs-lookup"><span data-stu-id="45ddf-164">The hashing algorithm and resulting distribution is deterministic.</span></span>  <span data-ttu-id="45ddf-165">Это значит, что одинаковое значение с тем же типом данных всегда определяется в одно распределение.</span><span class="sxs-lookup"><span data-stu-id="45ddf-165">That is the same value with the same data type will always has to the same distribution.</span></span>    

<span data-ttu-id="45ddf-166">Ниже приведен пример создания таблицы, распределенной по идентификаторам.</span><span class="sxs-lookup"><span data-stu-id="45ddf-166">This example will create a table distributed on id:</span></span>

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

## <a name="select-distribution-column"></a><span data-ttu-id="45ddf-167">Выбор столбца распределения</span><span class="sxs-lookup"><span data-stu-id="45ddf-167">Select distribution column</span></span>
<span data-ttu-id="45ddf-168">При выборе **хэш-распределения** таблицы также необходимо выбрать один столбец распределения.</span><span class="sxs-lookup"><span data-stu-id="45ddf-168">When you choose to **hash distribute** a table, you will need to select a single distribution column.</span></span>  <span data-ttu-id="45ddf-169">При этом необходимо учитывать три основных фактора.</span><span class="sxs-lookup"><span data-stu-id="45ddf-169">When selecting a distribution column, there are three major factors to consider.</span></span>  

<span data-ttu-id="45ddf-170">Столбец должен соответствовать следующим критериям.</span><span class="sxs-lookup"><span data-stu-id="45ddf-170">Select a single column which will:</span></span>

1. <span data-ttu-id="45ddf-171">Он должен быть необновляемым.</span><span class="sxs-lookup"><span data-stu-id="45ddf-171">Not be updated</span></span>
2. <span data-ttu-id="45ddf-172">Он должен распределять данные равномерно, предотвращая их смещение.</span><span class="sxs-lookup"><span data-stu-id="45ddf-172">Distribute data evenly, avoiding data skew</span></span>
3. <span data-ttu-id="45ddf-173">Минимизация перемещения данных</span><span class="sxs-lookup"><span data-stu-id="45ddf-173">Minimize data movement</span></span>

### <a name="select-distribution-column-which-will-not-be-updated"></a><span data-ttu-id="45ddf-174">Выбор необновляемого столбца распределения</span><span class="sxs-lookup"><span data-stu-id="45ddf-174">Select distribution column which will not be updated</span></span>
<span data-ttu-id="45ddf-175">Столбцы распределения являются необновляемыми. Поэтому для этой роли необходимо выбрать столбец со статическими значениями.</span><span class="sxs-lookup"><span data-stu-id="45ddf-175">Distribution columns are not updatable, therefore, select a column with static values.</span></span>  <span data-ttu-id="45ddf-176">Если столбец требует обновления, он не подходит для этой роли.</span><span class="sxs-lookup"><span data-stu-id="45ddf-176">If a column will need to be updated, it is generally not a good distribution candidate.</span></span>  <span data-ttu-id="45ddf-177">Чтобы обновить столбец распределения, сначала необходимо удалить строку, а затем добавить новую.</span><span class="sxs-lookup"><span data-stu-id="45ddf-177">If there is a case where you must update a distribution column, this can be done by first deleting the row and then inserting a new row.</span></span>

### <a name="select-distribution-column-which-will-distribute-data-evenly"></a><span data-ttu-id="45ddf-178">Выбор столбца распределения, который распределяет данные равномерно</span><span class="sxs-lookup"><span data-stu-id="45ddf-178">Select distribution column which will distribute data evenly</span></span>
<span data-ttu-id="45ddf-179">Распределенная система выполняет запросы так же быстро, как и самое медленное распределение, поэтому важно разделить работу между распределениями равномерно. Так вы сможете обеспечить сбалансированное выполнение запросов в системе.</span><span class="sxs-lookup"><span data-stu-id="45ddf-179">Since a distributed system performs only as fast as its slowest distribution, it is important to divide the work evenly across the distributions in order to achieve balanced execution across the system.</span></span>  <span data-ttu-id="45ddf-180">Метод разделения работы в распределенной системе зависит от расположения данных каждого распределения.</span><span class="sxs-lookup"><span data-stu-id="45ddf-180">The way the work is divided on a distributed system is based on where the data for each distribution lives.</span></span>  <span data-ttu-id="45ddf-181">Поэтому для распределения данных очень важно выбрать подходящий столбец распределения. Так работа будет равномерно разделяться между распределениями и выполняться за одинаковый промежуток времени.</span><span class="sxs-lookup"><span data-stu-id="45ddf-181">This makes it very important to select the right distribution column for distributing the data so that each distribution has equal work and will take the same time to complete its portion of the work.</span></span>  <span data-ttu-id="45ddf-182">Когда работа эффективно разделена по всей системе, то данные равномерно размещены в распределениях.</span><span class="sxs-lookup"><span data-stu-id="45ddf-182">When work is well divided across the system, the data is balanced across the distributions.</span></span>  <span data-ttu-id="45ddf-183">Если данные распределены неравномерно, это называется **неравномерным распределением данных**.</span><span class="sxs-lookup"><span data-stu-id="45ddf-183">When data is not evenly balanced, we call this **data skew**.</span></span>  

<span data-ttu-id="45ddf-184">Чтобы равномерно разделить данные и избежать их смещения, при выборе столбца распределения учтите следующие моменты.</span><span class="sxs-lookup"><span data-stu-id="45ddf-184">To divide data evenly and avoid data skew, consider the following when selecting your distribution column:</span></span>

1. <span data-ttu-id="45ddf-185">Выберите столбец, содержащий значительное количество различных значений.</span><span class="sxs-lookup"><span data-stu-id="45ddf-185">Select a column which contains a significant number of distinct values.</span></span>
2. <span data-ttu-id="45ddf-186">Избегайте распределения данных по столбцам, содержащим несколько различных значений.</span><span class="sxs-lookup"><span data-stu-id="45ddf-186">Avoid distributing data on columns with a few distinct values.</span></span>
3. <span data-ttu-id="45ddf-187">Избегайте распределения данных по столбцам с высоким коэффициентом содержания значений NULL.</span><span class="sxs-lookup"><span data-stu-id="45ddf-187">Avoid distributing data on columns with a high frequency of nulls.</span></span>
4. <span data-ttu-id="45ddf-188">Не распределяйте данные по столбцам с датами.</span><span class="sxs-lookup"><span data-stu-id="45ddf-188">Avoid distributing data on date columns.</span></span>

<span data-ttu-id="45ddf-189">Так как каждое значение хэшируется в 1 из 60 распределений, для равномерного распределения необходимо выбрать исключительно уникальный столбец, содержащий больше 60 уникальных значений.</span><span class="sxs-lookup"><span data-stu-id="45ddf-189">Since each value is hashed to 1 of 60 distributions, to achieve even distribution you will want to select a column that is highly unique and contains more than 60 unique values.</span></span>  <span data-ttu-id="45ddf-190">В качестве примера рассмотрим случай, когда столбец содержит только 40 уникальных значений.</span><span class="sxs-lookup"><span data-stu-id="45ddf-190">To illustrate, consider a case where a column only has 40 unique values.</span></span>  <span data-ttu-id="45ddf-191">Если этот столбец выбран в качестве ключа распределения, то данные этой таблицы будут распределяться только по 40 распределениям. 20 распределений останутся без данных, а значит, не будут выполнять обработку.</span><span class="sxs-lookup"><span data-stu-id="45ddf-191">If this column was selected as the distribution key, the data for that table would land on 40 distributions at most, leaving 20 distributions with no data and no processing to do.</span></span>  <span data-ttu-id="45ddf-192">И наоборот, 40 распределений будут обрабатывать большее количество данных, чем если бы данные были равномерно распределены по 60 распределениям.</span><span class="sxs-lookup"><span data-stu-id="45ddf-192">Conversely, the other 40 distributions would have more work to do that if the data was evenly spread over 60 distributions.</span></span>  <span data-ttu-id="45ddf-193">Этот сценарий является примером неравномерного распределения данных.</span><span class="sxs-lookup"><span data-stu-id="45ddf-193">This scenario is an example of data skew.</span></span>

<span data-ttu-id="45ddf-194">В системе MPP каждый этап запроса ожидает, пока все распределения не выполнят свою часть работы.</span><span class="sxs-lookup"><span data-stu-id="45ddf-194">In MPP system, each query step waits for all distributions to complete their share of the work.</span></span>  <span data-ttu-id="45ddf-195">Если одно распределение выполняет больше работы, чем остальные, то ресурсы остальных распределений фактически простаивают впустую, ожидая, пока занятое распределение завершит обработку.</span><span class="sxs-lookup"><span data-stu-id="45ddf-195">If one distribution is doing more work than the others, then the resource of the other distributions are essentially wasted just waiting on the busy distribution.</span></span>  <span data-ttu-id="45ddf-196">Если работа неравномерно разделена между всеми распределениями, это называется **неравномерным распределением обработки**.</span><span class="sxs-lookup"><span data-stu-id="45ddf-196">When work is not evenly spread across all distributions, we call this **processing skew**.</span></span>  <span data-ttu-id="45ddf-197">При неравномерном распределении обработки запросы выполняются медленнее, чем при равномерном разделении рабочей нагрузки между распределениями.</span><span class="sxs-lookup"><span data-stu-id="45ddf-197">Processing skew will cause queries to run slower than if the workload can be evenly spread across the distributions.</span></span>  <span data-ttu-id="45ddf-198">Неравномерное распределение данных приведет к неравномерному распределению обработки.</span><span class="sxs-lookup"><span data-stu-id="45ddf-198">Data skew will lead to processing skew.</span></span>

<span data-ttu-id="45ddf-199">Избегайте распределения по столбцам с высоким коэффициентом содержания значений NULL, так как значения NULL попадут в одно и то же распределение.</span><span class="sxs-lookup"><span data-stu-id="45ddf-199">Avoid distributing on highly nullable column as the null values will all land on the same distribution.</span></span> <span data-ttu-id="45ddf-200">Распределение по столбцу даты также может привести к неравномерному распределению обработки, так как все данные для конкретной даты попадут в одно распределение.</span><span class="sxs-lookup"><span data-stu-id="45ddf-200">Distributing on a date column can also cause processing skew because all data for a given date will land on the same distribution.</span></span> <span data-ttu-id="45ddf-201">Если несколько пользователей будут выполнять запросы с фильтром по одной и той же дате, то всю работу будет выполнять только 1 распределение из 60, так как для этой даты будет доступно только одно распределение.</span><span class="sxs-lookup"><span data-stu-id="45ddf-201">If several users are executing queries all filtering on the same date, then only 1 of the 60 distributions will be doing all of the work since a given date will only be on one distribution.</span></span> <span data-ttu-id="45ddf-202">Скорее всего, в этом случае запросы будут выполняться в 60 раз медленнее, чем если бы данные были равномерно разделены между всеми распределениями.</span><span class="sxs-lookup"><span data-stu-id="45ddf-202">In this scenario, the queries will likely run 60 times slower than if the data were equally spread over all of the distributions.</span></span>

<span data-ttu-id="45ddf-203">Если ни один столбец не подходит, рекомендуется использовать метод циклического перебора.</span><span class="sxs-lookup"><span data-stu-id="45ddf-203">When no good candidate columns exist, then consider using round robin as the distribution method.</span></span>

### <a name="select-distribution-column-which-will-minimize-data-movement"></a><span data-ttu-id="45ddf-204">Выбор столбца распределения, который минимизирует перемещение данных</span><span class="sxs-lookup"><span data-stu-id="45ddf-204">Select distribution column which will minimize data movement</span></span>
<span data-ttu-id="45ddf-205">Минимизация перемещения данных за счет выбора подходящего столбца распределения — одна из самых важных стратегий оптимизации производительности хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="45ddf-205">Minimizing data movement by selecting the right distribution column is one of the most important strategies for optimizing performance of your SQL Data Warehouse.</span></span>  <span data-ttu-id="45ddf-206">Перемещение данных в основном происходит при объединении или группировании таблиц.</span><span class="sxs-lookup"><span data-stu-id="45ddf-206">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="45ddf-207">Все столбцы, используемые в предложениях `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` и `HAVING`, **могут** становиться столбцами хэш-распределения.</span><span class="sxs-lookup"><span data-stu-id="45ddf-207">Columns used in `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` and `HAVING` clauses all make for **good** hash distribution candidates.</span></span>

<span data-ttu-id="45ddf-208">С другой стороны, в качестве столбца хэш-распределения мы **не** рекомендуем применять столбцы, используемые в предложении `WHERE`, так как они ограничивают распределения, участвующие в запросе, что приводит к неравномерному распределению обработки.</span><span class="sxs-lookup"><span data-stu-id="45ddf-208">On the other hand, columns in the `WHERE` clause do **not** make for good hash column candidates because they limit which distributions participate in the query, causing processing skew.</span></span>  <span data-ttu-id="45ddf-209">Хорошим примером столбца, который может казаться удачным выбором для распределения, но часто может приводить к неравномерному распределению обработки, является столбец даты.</span><span class="sxs-lookup"><span data-stu-id="45ddf-209">A good example of a column which might be tempting to distribute on, but often can cause this processing skew is a date column.</span></span>

<span data-ttu-id="45ddf-210">В общем, при наличии двух больших таблиц фактов, часто используемых в соединениях, оптимальная производительность достигается путем распределения обеих таблиц по одному из столбцов соединения.</span><span class="sxs-lookup"><span data-stu-id="45ddf-210">Generally speaking, if you have two large fact tables frequently involved in a join, you will gain the most performance by distributing both tables on one of the join columns.</span></span>  <span data-ttu-id="45ddf-211">При наличии таблицы, которая никогда не присоединялась к другой большой таблице фактов, рекомендуется использовать столбцы из предложения `GROUP BY` .</span><span class="sxs-lookup"><span data-stu-id="45ddf-211">If you have a table that is never joined to another large fact table, then look to columns that are frequently in the `GROUP BY` clause.</span></span>

<span data-ttu-id="45ddf-212">Существует несколько моментов, на которые следует обратить внимание, чтобы избежать перемещения данных во время операции соединения.</span><span class="sxs-lookup"><span data-stu-id="45ddf-212">There are a few key criteria which must be met to avoid data movement during a join:</span></span>

1. <span data-ttu-id="45ddf-213">Таблицы, входящие в соединение, должны быть распределены по методу хэш-распределения по **одному** из столбцов соединения.</span><span class="sxs-lookup"><span data-stu-id="45ddf-213">The tables involved in the join must be hash distributed on **one** of the columns participating in the join.</span></span>
2. <span data-ttu-id="45ddf-214">Типы данных столбцов соединения в обеих таблицах должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="45ddf-214">The data types of the join columns must match between both tables.</span></span>
3. <span data-ttu-id="45ddf-215">Объединение столбцов необходимо выполнять с помощью оператора equals.</span><span class="sxs-lookup"><span data-stu-id="45ddf-215">The columns must be joined with an equals operator.</span></span>
4. <span data-ttu-id="45ddf-216">Типом соединения не может быть `CROSS JOIN`.</span><span class="sxs-lookup"><span data-stu-id="45ddf-216">The join type may not be a `CROSS JOIN`.</span></span>

## <a name="troubleshooting-data-skew"></a><span data-ttu-id="45ddf-217">Устранение смещения данных</span><span class="sxs-lookup"><span data-stu-id="45ddf-217">Troubleshooting data skew</span></span>
<span data-ttu-id="45ddf-218">Если данные таблицы распределяются путем хэш-распределения, существует вероятность, что распределение будет неравномерным, т. е. в некоторых местах будет непропорционально больше данных.</span><span class="sxs-lookup"><span data-stu-id="45ddf-218">When table data is distributed using the hash distribution method there is a chance that some distributions will be skewed to have disproportionately more data than others.</span></span> <span data-ttu-id="45ddf-219">Чрезмерное смещение данных может повлиять на производительность запроса, так как выполнение распределенного запроса завершится только после длительного процесса распределения.</span><span class="sxs-lookup"><span data-stu-id="45ddf-219">Excessive data skew can impact query performance because the final result of a distributed query must wait for the longest running distribution to finish.</span></span> <span data-ttu-id="45ddf-220">В таком случае необходимо предпринять меры по устранению проблемы.</span><span class="sxs-lookup"><span data-stu-id="45ddf-220">Depending on the degree of the data skew you might need to address it.</span></span>

### <a name="identifying-skew"></a><span data-ttu-id="45ddf-221">Определение смещения данных</span><span class="sxs-lookup"><span data-stu-id="45ddf-221">Identifying skew</span></span>
<span data-ttu-id="45ddf-222">Для выявления неравномерного распределения в таблице можно воспользоваться `DBCC PDW_SHOWSPACEUSED`.</span><span class="sxs-lookup"><span data-stu-id="45ddf-222">A simple way to identify a table as skewed is to use `DBCC PDW_SHOWSPACEUSED`.</span></span>  <span data-ttu-id="45ddf-223">Это позволяет легко и быстро увидеть, сколько строк таблицы хранится в каждом из 60 распределений базы данных.</span><span class="sxs-lookup"><span data-stu-id="45ddf-223">This is a very quick and simple way to see the number of table rows that are stored in each of the 60 distributions of your database.</span></span>  <span data-ttu-id="45ddf-224">Помните, что для максимально сбалансированной производительности строки в распределенной таблице должны размещаться равномерно по всем распределениям.</span><span class="sxs-lookup"><span data-stu-id="45ddf-224">Remember that for the most balanced performance, the rows in your distributed table should be spread evenly across all the distributions.</span></span>

```sql
-- Find data skew for a distributed table
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

<span data-ttu-id="45ddf-225">Более глубокий анализ можно выполнить с помощью динамических административных представлений (DMV) хранилища данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="45ddf-225">However, if you query the Azure SQL Data Warehouse dynamic management views (DMV) you can perform a more detailed analysis.</span></span>  <span data-ttu-id="45ddf-226">Для начала создайте представление [dbo.vTableSizes][dbo.vTableSizes], используя хранилище данных SQL, описанное в статье [Общие сведения о таблицах в хранилище данных SQL][Overview].</span><span class="sxs-lookup"><span data-stu-id="45ddf-226">To start, create the view [dbo.vTableSizes][dbo.vTableSizes] view using the SQL from [Table Overview][Overview] article.</span></span>  <span data-ttu-id="45ddf-227">После этого выполните этот запрос, чтобы определить таблицы со смещением данных с показателем более 10 %.</span><span class="sxs-lookup"><span data-stu-id="45ddf-227">Once the view is created, run this query to identify which tables have more than 10% data skew.</span></span>

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

### <a name="resolving-data-skew"></a><span data-ttu-id="45ddf-228">Устранение неравномерности данных</span><span class="sxs-lookup"><span data-stu-id="45ddf-228">Resolving data skew</span></span>
<span data-ttu-id="45ddf-229">Не все смещения нужно исправлять.</span><span class="sxs-lookup"><span data-stu-id="45ddf-229">Not all skew is enough to warrant a fix.</span></span>  <span data-ttu-id="45ddf-230">В некоторых случаях производительность таблицы при выполнении некоторых запросов может компенсировать вред, нанесенный в результате смещения.</span><span class="sxs-lookup"><span data-stu-id="45ddf-230">In some cases, the performance of a table in some queries can outweigh the harm of data skew.</span></span>  <span data-ttu-id="45ddf-231">Чтобы решить, следует ли устранять смещение данных в таблице, нужно узнать как можно больше об объемах данных и запросах в рамках рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="45ddf-231">To decide if you should resolve data skew in a table, you should understand as much as possible about the data volumes and queries in your workload.</span></span>   <span data-ttu-id="45ddf-232">Чтобы определить последствия неравномерного распределения, можно воспользоваться действиями, описанными в статье [Мониторинг рабочей нагрузки с помощью динамических административных представлений][Query Monitoring]. Они позволяют определить влияние неравномерного распределения на производительность запросов, а именно на время выполнения запросов в определенных распределениях.</span><span class="sxs-lookup"><span data-stu-id="45ddf-232">One way to look at the impact of skew is to use the steps in the [Query Monitoring][Query Monitoring] article to monitor the impact of skew on query performance and specifically the impact to how long queries take to complete on the individual distributions.</span></span>

<span data-ttu-id="45ddf-233">В основе распределения данных лежит поиск баланса между уменьшением степени смещения и перемещения данных.</span><span class="sxs-lookup"><span data-stu-id="45ddf-233">Distributing data is a matter of finding the right balance between minimizing data skew and minimizing data movement.</span></span> <span data-ttu-id="45ddf-234">Это могут быть противоположные цели, и иногда нужно сохранить смещение данных, чтобы уменьшить степень их перемещения.</span><span class="sxs-lookup"><span data-stu-id="45ddf-234">These can be opposing goals, and sometimes you will want to keep data skew in order to reduce data movement.</span></span> <span data-ttu-id="45ddf-235">Например, если столбец распределения используется и для соединения, и для объединения, степень перемещения данных уменьшится.</span><span class="sxs-lookup"><span data-stu-id="45ddf-235">For example, when the distribution column is frequently the shared column in joins and aggregations, you will be minimizing data movement.</span></span> <span data-ttu-id="45ddf-236">Преимущество минимального перемещения данных может компенсировать последствия смещения данных.</span><span class="sxs-lookup"><span data-stu-id="45ddf-236">The benefit of having the minimal data movement might outweigh the impact of having data skew.</span></span>

<span data-ttu-id="45ddf-237">Стандартный способ устранения смещения данных — повторно создать таблицу с другим столбцом распределения.</span><span class="sxs-lookup"><span data-stu-id="45ddf-237">The typical way to resolve data skew is to re-create the table with a different distribution column.</span></span> <span data-ttu-id="45ddf-238">Столбец распределения в имеющейся таблице изменить невозможно. Поэтому для изменения распределения таблицы необходимо создать ее повторно с помощью инструкции [CTAS][].</span><span class="sxs-lookup"><span data-stu-id="45ddf-238">Since there is no way to change the distribution column on an existing table, the way to change the distribution of a table it to recreate it with a [CTAS][].</span></span>  <span data-ttu-id="45ddf-239">Смещение данных можно устранить двумя способами.</span><span class="sxs-lookup"><span data-stu-id="45ddf-239">Here are two examples of how resolve data skew:</span></span>

### <a name="example-1-re-create-the-table-with-a-new-distribution-column"></a><span data-ttu-id="45ddf-240">Способ 1. Повторное создание таблицы с новым столбцом распределения</span><span class="sxs-lookup"><span data-stu-id="45ddf-240">Example 1: Re-create the table with a new distribution column</span></span>
<span data-ttu-id="45ddf-241">В примере ниже для повторного создания таблицы с другим столбцом хэш-распределения используется инструкция [CTAS][].</span><span class="sxs-lookup"><span data-stu-id="45ddf-241">This example uses [CTAS][] to re-create a table with a different hash distribution column.</span></span>

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

--Rename the tables
RENAME OBJECT [dbo].[FactInternetSales] TO [FactInternetSales_ProductKey];
RENAME OBJECT [dbo].[FactInternetSales_CustomerKey] TO [FactInternetSales];
```

### <a name="example-2-re-create-the-table-using-round-robin-distribution"></a><span data-ttu-id="45ddf-242">Способ 2. Повторное создание таблицы с распределением по принципу циклического перебора</span><span class="sxs-lookup"><span data-stu-id="45ddf-242">Example 2: Re-create the table using round robin distribution</span></span>
<span data-ttu-id="45ddf-243">В примере ниже для повторного создания таблицы, распределенной по методу циклического перебора, вместо хэш-распределения используется инструкция [CTAS][].</span><span class="sxs-lookup"><span data-stu-id="45ddf-243">This example uses [CTAS][] to re-create a table with round robin instead of a hash distribution.</span></span> <span data-ttu-id="45ddf-244">В результате применения такого сценария вы получите равномерное распределение данных. Однако это приводит к увеличению их перемещения.</span><span class="sxs-lookup"><span data-stu-id="45ddf-244">This change will produce even data distribution at the cost of increased data movement.</span></span>

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

--Rename the tables
RENAME OBJECT [dbo].[FactInternetSales] TO [FactInternetSales_HASH];
RENAME OBJECT [dbo].[FactInternetSales_ROUND_ROBIN] TO [FactInternetSales];
```

## <a name="next-steps"></a><span data-ttu-id="45ddf-245">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="45ddf-245">Next steps</span></span>
<span data-ttu-id="45ddf-246">Дополнительные сведения о проектировании таблиц см. в статьях, посвященных [распределению][Distribute], [индексированию][Index], [секционированию таблиц][Partition], а также [типам данных][Data Types], [управлению статистикой][Statistics] и [временным таблицам][Temporary].</span><span class="sxs-lookup"><span data-stu-id="45ddf-246">To learn more about table design, see the [Distribute][Distribute], [Index][Index], [Partition][Partition], [Data Types][Data Types], [Statistics][Statistics] and [Temporary Tables][Temporary] articles.</span></span>

<span data-ttu-id="45ddf-247">Обзор рекомендаций по использованию приведен в статье [Рекомендации по использованию хранилища данных SQL Azure][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="45ddf-247">For an overview of best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
