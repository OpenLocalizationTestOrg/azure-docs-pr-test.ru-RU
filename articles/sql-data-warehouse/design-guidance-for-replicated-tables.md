---
title: "Руководство по проектированию реплицированных таблиц — хранилище данных SQL Azure | Документы Майкрософт"
description: "Рекомендации по проектированию реплицированных таблиц в схеме хранилища данных SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: ronortloff
manager: jhubbard
editor: 
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/14/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 437a4f628a343312984d1fa2981df7fa01459e26
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="design-guidance-for-using-replicated-tables-in-azure-sql-data-warehouse"></a><span data-ttu-id="999b6-103">Руководство по проектированию для использования реплицированных таблиц в хранилище данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="999b6-103">Design guidance for using replicated tables in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="999b6-104">В данной статье представлены рекомендации по проектированию реплицированных таблиц в схеме хранилища данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="999b6-104">This article gives recommendations for designing replicated tables in your SQL Data Warehouse schema.</span></span> <span data-ttu-id="999b6-105">Данные рекомендации позволяют повысить производительность запросов за счет уменьшения перемещения данных и упрощения запросов.</span><span class="sxs-lookup"><span data-stu-id="999b6-105">Use these recommendations to improve query performance by reducing data movement and query complexity.</span></span>

> [!NOTE]
> <span data-ttu-id="999b6-106">Функция реплицированной таблицы в настоящее время находится в общедоступной предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="999b6-106">The replicated table feature is currently in public preview.</span></span> <span data-ttu-id="999b6-107">Некоторое поведение может быть изменено.</span><span class="sxs-lookup"><span data-stu-id="999b6-107">Some behaviors are subject to change.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="999b6-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="999b6-108">Prerequisites</span></span>
<span data-ttu-id="999b6-109">В этой статье предполагается, что вы знакомы с распределением данных и основными понятиями перемещения данных в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="999b6-109">This article assumes you are familiar with data distribution and data movement concepts in SQL Data Warehouse.</span></span>  <span data-ttu-id="999b6-110">Дополнительные сведения см. в статье [Распределенные данные](sql-data-warehouse-distributed-data.md).</span><span class="sxs-lookup"><span data-stu-id="999b6-110">For more information, see [Distributed data](sql-data-warehouse-distributed-data.md).</span></span> 

<span data-ttu-id="999b6-111">При проектировании таблиц необходимо максимально четко понять, как устроены данные и как выполняются запросы к данным.</span><span class="sxs-lookup"><span data-stu-id="999b6-111">As part of table design, understand as much as possible about your data and how the data is queried.</span></span>  <span data-ttu-id="999b6-112">Например, для этого можно использовать следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="999b6-112">For example, consider these questions:</span></span>

- <span data-ttu-id="999b6-113">Каков размер таблицы?</span><span class="sxs-lookup"><span data-stu-id="999b6-113">How large is the table?</span></span>   
- <span data-ttu-id="999b6-114">Как часто она обновляется?</span><span class="sxs-lookup"><span data-stu-id="999b6-114">How often is the table refreshed?</span></span>   
- <span data-ttu-id="999b6-115">Имеются ли в хранилище данных таблицы фактов и таблицы измерений?</span><span class="sxs-lookup"><span data-stu-id="999b6-115">Do I have fact and dimension tables in a data warehouse?</span></span>   

## <a name="what-is-a-replicated-table"></a><span data-ttu-id="999b6-116">Что такое реплицированная таблица?</span><span class="sxs-lookup"><span data-stu-id="999b6-116">What is a replicated table?</span></span>
<span data-ttu-id="999b6-117">Реплицированная таблица содержит полную копию таблицы, которая доступна на каждом вычислительном узле.</span><span class="sxs-lookup"><span data-stu-id="999b6-117">A replicated table has a full copy of the table accessible on each Compute node.</span></span> <span data-ttu-id="999b6-118">Репликация таблицы устраняет необходимость передавать данные между вычислительными узлами перед операциями соединения или агрегирования.</span><span class="sxs-lookup"><span data-stu-id="999b6-118">Replicating a table removes the need to transfer data among Compute nodes before a join or aggregation.</span></span> <span data-ttu-id="999b6-119">Поскольку в таблице имеется несколько копий, реплицированные таблицы наиболее эффективны, когда размер таблицы в сжатом состоянии менее 2 ГБ.</span><span class="sxs-lookup"><span data-stu-id="999b6-119">Since the table has multiple copies, replicated tables work best when the table size is less than 2 GB compressed.</span></span>

<span data-ttu-id="999b6-120">На схеме ниже показана реплицированная таблица, которая доступна на каждом вычислительном узле.</span><span class="sxs-lookup"><span data-stu-id="999b6-120">The following diagram shows a replicated table that is accessible on each Compute node.</span></span> <span data-ttu-id="999b6-121">Для хранилища данных SQL реплицируемая таблица полностью копируется в базу данных распространителя на каждом вычислительном узле.</span><span class="sxs-lookup"><span data-stu-id="999b6-121">In SQL Data Warehouse, the replicated table is fully copied to a distribution database on each Compute node.</span></span> 

<span data-ttu-id="999b6-122">![Реплицируемая таблица](media/guidance-for-using-replicated-tables/replicated-table.png "Реплицируемая таблица")</span><span class="sxs-lookup"><span data-stu-id="999b6-122">![Replicated table](media/guidance-for-using-replicated-tables/replicated-table.png "Replicated table")</span></span>  

<span data-ttu-id="999b6-123">Реплицированные таблицы отлично подходят для небольших таблиц измерения в схеме типа "звезда".</span><span class="sxs-lookup"><span data-stu-id="999b6-123">Replicated tables work well for small dimension tables in a star schema.</span></span> <span data-ttu-id="999b6-124">Размер таблицы измерений обычно таков, что позволяет хранить и поддерживать несколько копий.</span><span class="sxs-lookup"><span data-stu-id="999b6-124">Dimension tables are usually of a size that makes it feasible to store and maintain multiple copies.</span></span> <span data-ttu-id="999b6-125">В измерениях хранятся описательные данные, которые изменяются редко, например имя и адрес клиента, а также сведения о продукте.</span><span class="sxs-lookup"><span data-stu-id="999b6-125">Dimensions store descriptive data that changes slowly, such as customer name and address, and product details.</span></span> <span data-ttu-id="999b6-126">Такое свойство данных способствует тому, что перестроение реплицированной таблицы также происходит реже.</span><span class="sxs-lookup"><span data-stu-id="999b6-126">The slowly changing nature of the data leads to fewer rebuilds of the replicated table.</span></span> 

<span data-ttu-id="999b6-127">Реплицированные таблицы подходят в ситуациях, когда:</span><span class="sxs-lookup"><span data-stu-id="999b6-127">Consider using a replicated table when:</span></span>

- <span data-ttu-id="999b6-128">Размер таблицы на диске менее 2 ГБ, независимо от количества строк.</span><span class="sxs-lookup"><span data-stu-id="999b6-128">The table size on disk is less than 2 GB, regardless of the number of rows.</span></span> <span data-ttu-id="999b6-129">Чтобы определить размер таблицы, можно использовать команду [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql): `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`.</span><span class="sxs-lookup"><span data-stu-id="999b6-129">To find the size of a table, you can use the [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) command: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`.</span></span> 
- <span data-ttu-id="999b6-130">Таблица используется в соединениях, для которых в противном случае требуется перемещение данных.</span><span class="sxs-lookup"><span data-stu-id="999b6-130">The table is used in joins that would otherwise require data movement.</span></span> <span data-ttu-id="999b6-131">Например, соединение таблиц распределенного хэша требует перемещения данных, когда присоединяемые столбцы не являются одним и тем же столбцом распределения.</span><span class="sxs-lookup"><span data-stu-id="999b6-131">For example, a join on hash-distributed tables requires data movement when the joining columns are not the same distribution column.</span></span> <span data-ttu-id="999b6-132">Если одна из таблиц распределенного хэша достаточно мала, рассмотрите возможность использования реплицированной таблицы.</span><span class="sxs-lookup"><span data-stu-id="999b6-132">If one of the hash-distributed tables is small, consider a replicated table.</span></span> <span data-ttu-id="999b6-133">Для соединения в таблице с распределением методом циклического перебора требуется перемещение данных.</span><span class="sxs-lookup"><span data-stu-id="999b6-133">A join on a round-robin table requires data movement.</span></span> <span data-ttu-id="999b6-134">В большинстве случаев вместо таких таблиц рекомендуется использовать реплицированные таблицы.</span><span class="sxs-lookup"><span data-stu-id="999b6-134">We recommend using replicated tables instead of round-robin tables in most cases.</span></span> 


<span data-ttu-id="999b6-135">Преобразовать существующие распределенные таблицы в реплицированные рекомендуется в случаях, когда:</span><span class="sxs-lookup"><span data-stu-id="999b6-135">Consider converting an existing distributed table to a replicated table when:</span></span>

- <span data-ttu-id="999b6-136">В планах запросов используются операции перемещения данных для их распространения на все вычислительные узлы.</span><span class="sxs-lookup"><span data-stu-id="999b6-136">Query plans use data movement operations that broadcast the data to all the Compute nodes.</span></span> <span data-ttu-id="999b6-137">Операция BroadcastMoveOperation является ресурсоемкой и снижает производительность запросов.</span><span class="sxs-lookup"><span data-stu-id="999b6-137">The BroadcastMoveOperation is expensive and slows query performance.</span></span> <span data-ttu-id="999b6-138">Чтобы просмотреть операции перемещения данных в планах запросов, используйте [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="999b6-138">To view data movement operations in query plans, use [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).</span></span>
 
<span data-ttu-id="999b6-139">Реплицированные таблицы не гарантируют лучшую производительность, когда:</span><span class="sxs-lookup"><span data-stu-id="999b6-139">Replicated tables may not yield the best query performance when:</span></span>

- <span data-ttu-id="999b6-140">Таблица содержит частые операции вставки, обновления и удаления.</span><span class="sxs-lookup"><span data-stu-id="999b6-140">The table has frequent insert, update, and delete operations.</span></span> <span data-ttu-id="999b6-141">Эти операции языка обработки данных (DML) требуют перестроения реплицированной таблицы.</span><span class="sxs-lookup"><span data-stu-id="999b6-141">These data manipulation language (DML) operations require a rebuild of the replicated table.</span></span> <span data-ttu-id="999b6-142">Зачастую перестроение приводит к снижению производительности.</span><span class="sxs-lookup"><span data-stu-id="999b6-142">Rebuilding frequently can cause slower performance.</span></span>
- <span data-ttu-id="999b6-143">Хранилище данных масштабируется достаточно часто.</span><span class="sxs-lookup"><span data-stu-id="999b6-143">The data warehouse is scaled frequently.</span></span> <span data-ttu-id="999b6-144">В ходе масштабирования хранилища данных изменяется количество вычислительных узлов, что влечет за собой повторное построение.</span><span class="sxs-lookup"><span data-stu-id="999b6-144">Scaling a data warehouse changes the number of Compute nodes, which incurs a rebuild.</span></span>
- <span data-ttu-id="999b6-145">Таблица содержит много столбцов, однако операции с данными обычно обращаются только к небольшому числу столбцов.</span><span class="sxs-lookup"><span data-stu-id="999b6-145">The table has a large number of columns, but data operations typically access only a small number of columns.</span></span> <span data-ttu-id="999b6-146">В этом случае вместо репликации всей таблицы лучше всего использовать хэш-распределение таблицы, а затем создать индекс для часто используемых столбцов.</span><span class="sxs-lookup"><span data-stu-id="999b6-146">In this scenario, instead of replicating the entire table, it might be more effective to hash distribute the table, and then create an index on the frequently accessed columns.</span></span> <span data-ttu-id="999b6-147">Если запрос требует перемещения данных, хранилище данных SQL перемещает только данные в требуемых столбцах.</span><span class="sxs-lookup"><span data-stu-id="999b6-147">When a query requires data movement, SQL Data Warehouse only moves data in the requested columns.</span></span> 



## <a name="use-replicated-tables-with-simple-query-predicates"></a><span data-ttu-id="999b6-148">Использование реплицированных таблиц с предикатами простого запроса</span><span class="sxs-lookup"><span data-stu-id="999b6-148">Use replicated tables with simple query predicates</span></span>
<span data-ttu-id="999b6-149">Прежде чем выбрать распространение или репликацию таблицы, выберите типы запросов, которые планируется выполнять к таблице.</span><span class="sxs-lookup"><span data-stu-id="999b6-149">Before you choose to distribute or replicate a table, think about the types of queries you plan to run against the table.</span></span> <span data-ttu-id="999b6-150">Когда это возможно:</span><span class="sxs-lookup"><span data-stu-id="999b6-150">Whenever possible,</span></span>

- <span data-ttu-id="999b6-151">Используйте реплицированные таблицы для запросов с предикатами простого запроса, например равенства или неравенства.</span><span class="sxs-lookup"><span data-stu-id="999b6-151">Use replicated tables for queries with simple query predicates, such as equality or inequality.</span></span>
- <span data-ttu-id="999b6-152">Используйте распределенные таблицы для запросов с предикатами сложного запроса, например LIKE или NOT LIKE.</span><span class="sxs-lookup"><span data-stu-id="999b6-152">Use distributed tables for queries with complex query predicates, such as LIKE or NOT LIKE.</span></span>

<span data-ttu-id="999b6-153">Ресурсоемкие запросы лучше всего использовать в случаях, когда работа распределяется по всем вычислительным узлам.</span><span class="sxs-lookup"><span data-stu-id="999b6-153">CPU-intensive queries perform best when the work is distributed across all of the Compute nodes.</span></span> <span data-ttu-id="999b6-154">Например, запросы, которые запускают вычисления для каждой строки таблицы, выполняются более эффективно в распределенных таблицах, чем реплицированных.</span><span class="sxs-lookup"><span data-stu-id="999b6-154">For example, queries that run computations on each row of a table perform better on distributed tables than replicated tables.</span></span> <span data-ttu-id="999b6-155">Поскольку реплицированные таблицы хранятся в полном объеме на каждом вычислительном узле, ресурсоемкие запросы к реплицированной таблице применяются ко всей таблице на каждом вычислительном узле.</span><span class="sxs-lookup"><span data-stu-id="999b6-155">Since a replicated table is stored in full on each Compute node, a CPU-intensive query against a replicated table runs against the entire table on every Compute node.</span></span> <span data-ttu-id="999b6-156">Лишние вычисления могут снизить производительность запроса.</span><span class="sxs-lookup"><span data-stu-id="999b6-156">The extra computation can slow query performance.</span></span>

<span data-ttu-id="999b6-157">Например, в этом запросе содержится сложный предикат.</span><span class="sxs-lookup"><span data-stu-id="999b6-157">For example, this query has a complex predicate.</span></span>  <span data-ttu-id="999b6-158">Он выполняется быстрее, когда в качестве поставщика выступает распределенная таблица вместо реплицированной таблицы.</span><span class="sxs-lookup"><span data-stu-id="999b6-158">It runs faster when supplier is a distributed table instead of a replicated table.</span></span> <span data-ttu-id="999b6-159">В этом примере для поставщика можно выполнить хэш-распределение или распределение методом циклического перебора.</span><span class="sxs-lookup"><span data-stu-id="999b6-159">In this example, supplier can be hash-distributed or round-robin distributed.</span></span>

```sql

SELECT EnglishProductName 
FROM DimProduct 
WHERE EnglishDescription LIKE '%frame%comfortable%'

```

## <a name="convert-existing-round-robin-tables-to-replicated-tables"></a><span data-ttu-id="999b6-160">Преобразование существующих циклических таблиц в реплицированные таблицы</span><span class="sxs-lookup"><span data-stu-id="999b6-160">Convert existing round-robin tables to replicated tables</span></span>
<span data-ttu-id="999b6-161">Если имеются циклические таблицы, их рекомендуется преобразовать в реплицированные таблицы, если они удовлетворяют критериям, обозначенным в этой статье.</span><span class="sxs-lookup"><span data-stu-id="999b6-161">If you already have round-robin tables, we recommend converting them to replicated tables if they meet with criteria outlined in this article.</span></span> <span data-ttu-id="999b6-162">Реплицированные таблицы эффективнее по сравнению с циклическими таблицами, поскольку они исключают необходимость в перемещении данных.</span><span class="sxs-lookup"><span data-stu-id="999b6-162">Replicated tables improve performance over round-robin tables because they eliminate the need for data movement.</span></span>  <span data-ttu-id="999b6-163">Для соединений в циклической таблице всегда требуется перемещение данных.</span><span class="sxs-lookup"><span data-stu-id="999b6-163">A round-robin table always requires data movement for joins.</span></span> 

<span data-ttu-id="999b6-164">В этом примере используется функция [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) для изменения таблицы DimSalesTerritory в реплицированную таблицу.</span><span class="sxs-lookup"><span data-stu-id="999b6-164">This example uses [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) to change the DimSalesTerritory table to a replicated table.</span></span> <span data-ttu-id="999b6-165">В данном примере неважно, была ли таблица DimSalesTerritory хэш-распределена или распределена методом циклического перебора.</span><span class="sxs-lookup"><span data-stu-id="999b6-165">This example works regardless of whether DimSalesTerritory is hash-distributed or round-robin.</span></span>

```sql
CREATE TABLE [dbo].[DimSalesTerritory_REPLICATE]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = REPLICATE  
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]
OPTION  (LABEL  = 'CTAS : DimSalesTerritory_REPLICATE') 

--Create statistics on new table
CREATE STATISTICS [SalesTerritoryKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryKey]);
CREATE STATISTICS [SalesTerritoryAlternateKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryAlternateKey]);
CREATE STATISTICS [SalesTerritoryRegion] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryRegion]);
CREATE STATISTICS [SalesTerritoryCountry] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryCountry]);
CREATE STATISTICS [SalesTerritoryGroup] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryGroup]);

-- Switch table names
RENAME OBJECT [dbo].[DimSalesTerritory] to [DimSalesTerritory_old];
RENAME OBJECT [dbo].[DimSalesTerritory_REPLICATE] TO [DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```  

### <a name="query-performance-example-for-round-robin-versus-replicated"></a><span data-ttu-id="999b6-166">Пример производительности запросов для циклической и реплицированной таблиц</span><span class="sxs-lookup"><span data-stu-id="999b6-166">Query performance example for round-robin versus replicated</span></span> 

<span data-ttu-id="999b6-167">Поскольку вся таблица уже существует на каждом вычислительном узле, для реплицированной таблицы не требуется перемещать данные для соединений.</span><span class="sxs-lookup"><span data-stu-id="999b6-167">A replicated table does not require any data movement for joins because the entire table is already present on each Compute node.</span></span> <span data-ttu-id="999b6-168">Если таблицы измерений распределены методом циклического перебора, соединение копирует таблицу измерения в полном объеме на каждом вычислительном узле.</span><span class="sxs-lookup"><span data-stu-id="999b6-168">If the dimension tables are round-robin distributed, a join copies the dimension table in full to each Compute node.</span></span> <span data-ttu-id="999b6-169">Чтобы переместить данные, план запроса содержит операцию, которая называется BroadcastMoveOperation.</span><span class="sxs-lookup"><span data-stu-id="999b6-169">To move the data, the query plan contains an operation called BroadcastMoveOperation.</span></span> <span data-ttu-id="999b6-170">Операции перемещения данных данного типа снижают производительность запросов. Устранить это можно с помощью реплицированных таблиц.</span><span class="sxs-lookup"><span data-stu-id="999b6-170">This type of data movement operation slows query performance and is eliminated by using replicated tables.</span></span> <span data-ttu-id="999b6-171">Чтобы просмотреть действия плана запроса, используйте представление системного каталога [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="999b6-171">To view query plan steps, use the [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) system catalog view.</span></span> 

<span data-ttu-id="999b6-172">Например, в следующем запросе к схеме AdventureWorks таблица ` FactInternetSales` хэш-распределена.</span><span class="sxs-lookup"><span data-stu-id="999b6-172">For example, in following query against the AdventureWorks schema, the ` FactInternetSales` table is hash-distributed.</span></span> <span data-ttu-id="999b6-173">Таблицы `DimDate` и `DimSalesTerritory` являются таблицами измерений меньшего размера.</span><span class="sxs-lookup"><span data-stu-id="999b6-173">The `DimDate` and `DimSalesTerritory` tables are smaller dimension tables.</span></span> <span data-ttu-id="999b6-174">Этот запрос возвращает общий объем продаж в Северной Америке за 2004 финансовый год:</span><span class="sxs-lookup"><span data-stu-id="999b6-174">This query returns the total sales in North America for fiscal year 2004:</span></span>
 
```sql
SELECT [TotalSalesAmount] = SUM(SalesAmount)
FROM dbo.FactInternetSales s
INNER JOIN dbo.DimDate d
  ON d.DateKey = s.OrderDateKey
INNER JOIN dbo.DimSalesTerritory t
  ON t.SalesTerritoryKey = s.SalesTerritoryKey
WHERE d.FiscalYear = 2004
  AND t.SalesTerritoryGroup = 'North America'
```
<span data-ttu-id="999b6-175">Мы повторно создали таблицы `DimDate` и `DimSalesTerritory` как циклические таблицы.</span><span class="sxs-lookup"><span data-stu-id="999b6-175">We re-created `DimDate` and `DimSalesTerritory` as round-robin tables.</span></span> <span data-ttu-id="999b6-176">В результате запрос показал следующий план запроса, в котором имеется несколько операций широковещательного переноса:</span><span class="sxs-lookup"><span data-stu-id="999b6-176">As a result, the query showed the following query plan, which has multiple broadcast move operations:</span></span> 
 
![План запроса с циклическим перебором](media/design-guidance-for-replicated-tables/round-robin-tables-query-plan.jpg) 

<span data-ttu-id="999b6-178">Мы повторно создали таблицы `DimDate` и `DimSalesTerritory` как в реплицированные таблицы, а затем снова выполнили запрос.</span><span class="sxs-lookup"><span data-stu-id="999b6-178">We re-created `DimDate` and `DimSalesTerritory` as replicated tables, and ran the query again.</span></span> <span data-ttu-id="999b6-179">Результирующий план запроса намного короче, а также в нем нет широковещательного переноса.</span><span class="sxs-lookup"><span data-stu-id="999b6-179">The resulting query plan is much shorter and does not have any broadcast moves.</span></span>

![План запроса с репликацией](media/design-guidance-for-replicated-tables/replicated-tables-query-plan.jpg) 


## <a name="performance-considerations-for-modifying-replicated-tables"></a><span data-ttu-id="999b6-181">Рекомендации по повышению производительности для изменения реплицированных таблиц</span><span class="sxs-lookup"><span data-stu-id="999b6-181">Performance considerations for modifying replicated tables</span></span>
<span data-ttu-id="999b6-182">Хранилище данных SQL реализует реплицированную таблицу путем сохранения главной версии таблицы.</span><span class="sxs-lookup"><span data-stu-id="999b6-182">SQL Data Warehouse implements a replicated table by maintaining a master version of the table.</span></span> <span data-ttu-id="999b6-183">Для этого оно копирует главную версию в одну базу данных распространителя на каждый вычислительный узел.</span><span class="sxs-lookup"><span data-stu-id="999b6-183">It copies the master version to one distribution database on each Compute node.</span></span> <span data-ttu-id="999b6-184">При наличии изменений хранилище данных SQL обновляет сначала главную таблицу.</span><span class="sxs-lookup"><span data-stu-id="999b6-184">When there is a change, SQL Data Warehouse first updates the master table.</span></span> <span data-ttu-id="999b6-185">Затем требуется перестроение таблиц на каждом вычислительном узле.</span><span class="sxs-lookup"><span data-stu-id="999b6-185">Then it requires a rebuild of the tables on each Compute node.</span></span> <span data-ttu-id="999b6-186">Перестроение реплицированной таблицы включает копирование таблицы на каждый вычислительный узел и последующее перестроение индексов.</span><span class="sxs-lookup"><span data-stu-id="999b6-186">A rebuild of a replicated table includes copying the table to each Compute node and then rebuilding the indexes.</span></span>

<span data-ttu-id="999b6-187">Перестроение требуется после следующего:</span><span class="sxs-lookup"><span data-stu-id="999b6-187">Rebuilds are required after:</span></span>
- <span data-ttu-id="999b6-188">Загрузка или изменение данных</span><span class="sxs-lookup"><span data-stu-id="999b6-188">Data is loaded or modified</span></span>
- <span data-ttu-id="999b6-189">Масштабирование хранилища с использованием другого параметра DWU</span><span class="sxs-lookup"><span data-stu-id="999b6-189">The data warehouse is scaled to a different DWU setting</span></span>
- <span data-ttu-id="999b6-190">Обновление определения таблицы</span><span class="sxs-lookup"><span data-stu-id="999b6-190">Table definition is updated</span></span>

<span data-ttu-id="999b6-191">Перестроение не требуется после следующего:</span><span class="sxs-lookup"><span data-stu-id="999b6-191">Rebuilds are not required after:</span></span>
- <span data-ttu-id="999b6-192">Выполнение операции приостановки</span><span class="sxs-lookup"><span data-stu-id="999b6-192">Pause operation</span></span>
- <span data-ttu-id="999b6-193">Выполнение операции возобновления</span><span class="sxs-lookup"><span data-stu-id="999b6-193">Resume operation</span></span>

<span data-ttu-id="999b6-194">Перестроение не происходит сразу после изменения данных.</span><span class="sxs-lookup"><span data-stu-id="999b6-194">The rebuild does not happen immediately after data is modified.</span></span> <span data-ttu-id="999b6-195">Вместо этого оно выполняется при первом выборе запросом данных из таблицы.</span><span class="sxs-lookup"><span data-stu-id="999b6-195">Instead, the rebuild is triggered the first time a query selects from the table.</span></span>  <span data-ttu-id="999b6-196">В первоначальной инструкции SELECT для выбора данных из таблицы содержатся действия для перестроения реплицированной таблицы.</span><span class="sxs-lookup"><span data-stu-id="999b6-196">Within the initial select statement from the table are steps to rebuild the replicated table.</span></span>  <span data-ttu-id="999b6-197">Поскольку перестроение выполняется в запросе, влияние первоначальной инструкции SELECT может быть значительным в зависимости от размера таблицы.</span><span class="sxs-lookup"><span data-stu-id="999b6-197">Because the rebuild is done within the query, the impact to the initial select statement could be significant depending on the size of the table.</span></span>  <span data-ttu-id="999b6-198">Если имеется несколько реплицированных таблиц, требующих перестроения, каждая копия перестраивается последовательно в соответствии с порядком действий в рамках инструкции.</span><span class="sxs-lookup"><span data-stu-id="999b6-198">If multiple replicated tables are involved that need a rebuild, each copy is rebuilt serially as steps within the statement.</span></span>  <span data-ttu-id="999b6-199">Для сохранения целостности данных во время перестроения реплицированной таблицы к ней применяется монопольная блокировка.</span><span class="sxs-lookup"><span data-stu-id="999b6-199">To maintain data consistency during the rebuild of the replicated table an exclusive lock is taken on the table.</span></span>  <span data-ttu-id="999b6-200">Блокировка предотвращает любой доступ к таблице на время ее перестроения.</span><span class="sxs-lookup"><span data-stu-id="999b6-200">The lock prevents all access to the table for the duration of the rebuild.</span></span> 

### <a name="use-indexes-conservatively"></a><span data-ttu-id="999b6-201">Консервативный подход к использованию индексов</span><span class="sxs-lookup"><span data-stu-id="999b6-201">Use indexes conservatively</span></span>
<span data-ttu-id="999b6-202">В отношении реплицированных таблиц применяется стандартный подход к индексированию.</span><span class="sxs-lookup"><span data-stu-id="999b6-202">Standard indexing practices apply to replicated tables.</span></span> <span data-ttu-id="999b6-203">В процессе перестроения хранилище данных SQL перестраивает индекс каждой реплицированной таблицы.</span><span class="sxs-lookup"><span data-stu-id="999b6-203">SQL Data Warehouse rebuilds each replicated table index as part of the rebuild.</span></span> <span data-ttu-id="999b6-204">Индексы следует использовать только в том случае, если для повышения производительности целесообразно перестроить индексы.</span><span class="sxs-lookup"><span data-stu-id="999b6-204">Only use indexes when the performance gain outweighs the cost of rebuilding the indexes.</span></span>  
 
### <a name="batch-data-loads"></a><span data-ttu-id="999b6-205">Пакетная загрузка данных</span><span class="sxs-lookup"><span data-stu-id="999b6-205">Batch data loads</span></span>
<span data-ttu-id="999b6-206">При загрузке данных в реплицированные таблицы попробуйте минимизировать перестроения путем пакетной загрузки.</span><span class="sxs-lookup"><span data-stu-id="999b6-206">When loading data into replicated tables, try to minimize rebuilds by batching loads together.</span></span> <span data-ttu-id="999b6-207">Выполните все пакетные загрузки перед выполнением инструкции SELECT.</span><span class="sxs-lookup"><span data-stu-id="999b6-207">Perform all the batched loads before running select statements.</span></span>

<span data-ttu-id="999b6-208">Например, ниже представлен шаблон загрузки данных из четырех источников и запуска четырех операций перестроения.</span><span class="sxs-lookup"><span data-stu-id="999b6-208">For example, this load pattern loads data from four sources and invokes four rebuilds.</span></span> 

- <span data-ttu-id="999b6-209">Загрузка из источника 1.</span><span class="sxs-lookup"><span data-stu-id="999b6-209">Load from source 1.</span></span>
- <span data-ttu-id="999b6-210">Инструкция SELECT вызывает перестроение 1.</span><span class="sxs-lookup"><span data-stu-id="999b6-210">Select statement triggers rebuild 1.</span></span>
- <span data-ttu-id="999b6-211">Загрузка из источника 2.</span><span class="sxs-lookup"><span data-stu-id="999b6-211">Load from source 2.</span></span>
- <span data-ttu-id="999b6-212">Инструкция SELECT вызывает перестроение 2.</span><span class="sxs-lookup"><span data-stu-id="999b6-212">Select statement triggers rebuild 2.</span></span>
- <span data-ttu-id="999b6-213">Загрузка из источника 3.</span><span class="sxs-lookup"><span data-stu-id="999b6-213">Load from source 3.</span></span>
- <span data-ttu-id="999b6-214">Инструкция SELECT вызывает перестроение 3.</span><span class="sxs-lookup"><span data-stu-id="999b6-214">Select statement triggers rebuild 3.</span></span>
- <span data-ttu-id="999b6-215">Загрузка из источника 4.</span><span class="sxs-lookup"><span data-stu-id="999b6-215">Load from source 4.</span></span>
- <span data-ttu-id="999b6-216">Инструкция SELECT вызывает перестроение 4.</span><span class="sxs-lookup"><span data-stu-id="999b6-216">Select statement triggers rebuild 4.</span></span>

<span data-ttu-id="999b6-217">Например, ниже представлен шаблон загрузки данных из четырех источников и запуска только одной операции перестроения.</span><span class="sxs-lookup"><span data-stu-id="999b6-217">For example, this load pattern loads data from four sources, but only invokes one rebuild.</span></span>

- <span data-ttu-id="999b6-218">Загрузка из источника 1.</span><span class="sxs-lookup"><span data-stu-id="999b6-218">Load from source 1.</span></span>
- <span data-ttu-id="999b6-219">Загрузка из источника 2.</span><span class="sxs-lookup"><span data-stu-id="999b6-219">Load from source 2.</span></span>
- <span data-ttu-id="999b6-220">Загрузка из источника 3.</span><span class="sxs-lookup"><span data-stu-id="999b6-220">Load from source 3.</span></span>
- <span data-ttu-id="999b6-221">Загрузка из источника 4.</span><span class="sxs-lookup"><span data-stu-id="999b6-221">Load from source 4.</span></span>
- <span data-ttu-id="999b6-222">Инструкция SELECT вызывает перестроение.</span><span class="sxs-lookup"><span data-stu-id="999b6-222">Select statement triggers rebuild.</span></span>


### <a name="rebuild-a-replicated-table-after-a-batch-load"></a><span data-ttu-id="999b6-223">Перестроение реплицированной таблицы после пакетной загрузки</span><span class="sxs-lookup"><span data-stu-id="999b6-223">Rebuild a replicated table after a batch load</span></span>
<span data-ttu-id="999b6-224">Чтобы обеспечить согласованное выполнение запросов, рекомендуется принудительно обновить реплицированные таблицы после пакетной загрузки.</span><span class="sxs-lookup"><span data-stu-id="999b6-224">To ensure consistent query execution times, we recommend forcing a refresh of the replicated tables after a batch load.</span></span> <span data-ttu-id="999b6-225">В противном случае при выполнении первого запроса потребуется дождаться обновления таблиц, что включает перестроение индексов.</span><span class="sxs-lookup"><span data-stu-id="999b6-225">Otherwise, the first query must wait for the tables to refresh, which includes rebuilding the indexes.</span></span> <span data-ttu-id="999b6-226">В зависимости от размера и количество затронутых реплицированных таблиц это может оказать значительное влияние на производительность.</span><span class="sxs-lookup"><span data-stu-id="999b6-226">Depending on the size and number of replicated tables affected, the performance impact can be significant.</span></span>  

<span data-ttu-id="999b6-227">В этом запросе используется динамическое административное представление [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) для отображения реплицированных таблиц, которые были изменены, но не перестроены.</span><span class="sxs-lookup"><span data-stu-id="999b6-227">This query uses the [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) DMV to list the replicated tables that have been modified, but not rebuilt.</span></span>

```sql 
SELECT [ReplicatedTable] = t.[name]
  FROM sys.tables t  
  JOIN sys.pdw_replicated_table_cache_state c  
    ON c.object_id = t.object_id 
  JOIN sys.pdw_table_distribution_properties p 
    ON p.object_id = t.object_id 
  WHERE c.[state] = 'NotReady'
    AND p.[distribution_policy_desc] = 'REPLICATE'
```
 
<span data-ttu-id="999b6-228">Чтобы принудительно перестроить таблицы, выполните следующую инструкцию для каждой таблицы в предыдущих выходных данных.</span><span class="sxs-lookup"><span data-stu-id="999b6-228">To force a rebuild, run the following statement on each table in the preceding output.</span></span> 

```sql
SELECT TOP 1 * FROM [ReplicatedTable]
``` 
 
## <a name="next-steps"></a><span data-ttu-id="999b6-229">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="999b6-229">Next steps</span></span> 
<span data-ttu-id="999b6-230">Чтобы создать реплицированную таблицу, воспользуйтесь одной из следующих инструкций:</span><span class="sxs-lookup"><span data-stu-id="999b6-230">To create a replicated table, use one of these statements:</span></span>

- [<span data-ttu-id="999b6-231">CREATE TABLE (хранилище данных Azure SQL)</span><span class="sxs-lookup"><span data-stu-id="999b6-231">CREATE TABLE (Azure SQL Data Warehouse)</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-azure-sql-data-warehouse)
- [<span data-ttu-id="999b6-232">CREATE TABLE AS SELECT (хранилище данных Azure SQL)</span><span class="sxs-lookup"><span data-stu-id="999b6-232">CREATE TABLE AS SELECT (Azure SQL Data Warehouse</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse)

<span data-ttu-id="999b6-233">Обзор распределенных таблиц см. в разделе [Распределенные таблицы](sql-data-warehouse-tables-distribute.md).</span><span class="sxs-lookup"><span data-stu-id="999b6-233">For an overview of distributed tables, see [distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>



