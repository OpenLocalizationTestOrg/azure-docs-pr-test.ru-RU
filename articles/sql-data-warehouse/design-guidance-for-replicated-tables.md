---
title: "руководство по aaaDesign для реплицированных таблиц - хранилище данных SQL Azure | Документы Microsoft"
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
ms.openlocfilehash: 5d405b8c404c65177b387ba959126839c1cf8799
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="design-guidance-for-using-replicated-tables-in-azure-sql-data-warehouse"></a><span data-ttu-id="9ca83-103">Руководство по проектированию для использования реплицированных таблиц в хранилище данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="9ca83-103">Design guidance for using replicated tables in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="9ca83-104">В данной статье представлены рекомендации по проектированию реплицированных таблиц в схеме хранилища данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="9ca83-104">This article gives recommendations for designing replicated tables in your SQL Data Warehouse schema.</span></span> <span data-ttu-id="9ca83-105">Используйте эти рекомендации tooimprove производительность за счет уменьшения сложности перемещения и запроса данных.</span><span class="sxs-lookup"><span data-stu-id="9ca83-105">Use these recommendations tooimprove query performance by reducing data movement and query complexity.</span></span>

> [!NOTE]
> <span data-ttu-id="9ca83-106">компонент Hello реплицируемой таблицы в настоящее время находится в общедоступной предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="9ca83-106">hello replicated table feature is currently in public preview.</span></span> <span data-ttu-id="9ca83-107">Некоторые поведения — это toochange субъекта.</span><span class="sxs-lookup"><span data-stu-id="9ca83-107">Some behaviors are subject toochange.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="9ca83-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9ca83-108">Prerequisites</span></span>
<span data-ttu-id="9ca83-109">В этой статье предполагается, что вы знакомы с распределением данных и основными понятиями перемещения данных в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="9ca83-109">This article assumes you are familiar with data distribution and data movement concepts in SQL Data Warehouse.</span></span>  <span data-ttu-id="9ca83-110">Дополнительные сведения см. в статье [Распределенные данные](sql-data-warehouse-distributed-data.md).</span><span class="sxs-lookup"><span data-stu-id="9ca83-110">For more information, see [Distributed data](sql-data-warehouse-distributed-data.md).</span></span> 

<span data-ttu-id="9ca83-111">Как часть структуры таблиц понять, насколько возможно, связанные с данными и как выполнять запросы к данным hello.</span><span class="sxs-lookup"><span data-stu-id="9ca83-111">As part of table design, understand as much as possible about your data and how hello data is queried.</span></span>  <span data-ttu-id="9ca83-112">Например, для этого можно использовать следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="9ca83-112">For example, consider these questions:</span></span>

- <span data-ttu-id="9ca83-113">Размер таблицы hello?</span><span class="sxs-lookup"><span data-stu-id="9ca83-113">How large is hello table?</span></span>   
- <span data-ttu-id="9ca83-114">Как часто обновлять таблицы hello</span><span class="sxs-lookup"><span data-stu-id="9ca83-114">How often is hello table refreshed?</span></span>   
- <span data-ttu-id="9ca83-115">Имеются ли в хранилище данных таблицы фактов и таблицы измерений?</span><span class="sxs-lookup"><span data-stu-id="9ca83-115">Do I have fact and dimension tables in a data warehouse?</span></span>   

## <a name="what-is-a-replicated-table"></a><span data-ttu-id="9ca83-116">Что такое реплицированная таблица?</span><span class="sxs-lookup"><span data-stu-id="9ca83-116">What is a replicated table?</span></span>
<span data-ttu-id="9ca83-117">Реплицированные таблицы имеет полную копию таблицы hello доступны на каждом вычислительном узле.</span><span class="sxs-lookup"><span data-stu-id="9ca83-117">A replicated table has a full copy of hello table accessible on each Compute node.</span></span> <span data-ttu-id="9ca83-118">Таблицы репликации удаляет данные tootransfer необходимость hello среди вычислительных узлов перед соединения или статистической обработки.</span><span class="sxs-lookup"><span data-stu-id="9ca83-118">Replicating a table removes hello need tootransfer data among Compute nodes before a join or aggregation.</span></span> <span data-ttu-id="9ca83-119">Поскольку таблица hello имеет несколько копий, реплицированные таблицы лучше всего при размере таблицы hello сжатые меньше, чем 2 ГБ.</span><span class="sxs-lookup"><span data-stu-id="9ca83-119">Since hello table has multiple copies, replicated tables work best when hello table size is less than 2 GB compressed.</span></span>

<span data-ttu-id="9ca83-120">Hello следующей диаграмме показан реплицируемой таблицы, доступной на каждом вычислительном узле.</span><span class="sxs-lookup"><span data-stu-id="9ca83-120">hello following diagram shows a replicated table that is accessible on each Compute node.</span></span> <span data-ttu-id="9ca83-121">В хранилище данных SQL hello реплицируемой таблицы является полностью копируются tooa базы данных распространителя на каждом вычислительном узле.</span><span class="sxs-lookup"><span data-stu-id="9ca83-121">In SQL Data Warehouse, hello replicated table is fully copied tooa distribution database on each Compute node.</span></span> 

<span data-ttu-id="9ca83-122">![Реплицируемая таблица](media/guidance-for-using-replicated-tables/replicated-table.png "Реплицируемая таблица")</span><span class="sxs-lookup"><span data-stu-id="9ca83-122">![Replicated table](media/guidance-for-using-replicated-tables/replicated-table.png "Replicated table")</span></span>  

<span data-ttu-id="9ca83-123">Реплицированные таблицы отлично подходят для небольших таблиц измерения в схеме типа "звезда".</span><span class="sxs-lookup"><span data-stu-id="9ca83-123">Replicated tables work well for small dimension tables in a star schema.</span></span> <span data-ttu-id="9ca83-124">Таблицы измерений обычно имеют размер, который делает возможным toostore и поддерживать несколько экземпляров.</span><span class="sxs-lookup"><span data-stu-id="9ca83-124">Dimension tables are usually of a size that makes it feasible toostore and maintain multiple copies.</span></span> <span data-ttu-id="9ca83-125">В измерениях хранятся описательные данные, которые изменяются редко, например имя и адрес клиента, а также сведения о продукте.</span><span class="sxs-lookup"><span data-stu-id="9ca83-125">Dimensions store descriptive data that changes slowly, such as customer name and address, and product details.</span></span> <span data-ttu-id="9ca83-126">Hello медленно изменяющихся характер данных hello приводит перестроение toofewer hello реплицируемой таблицы.</span><span class="sxs-lookup"><span data-stu-id="9ca83-126">hello slowly changing nature of hello data leads toofewer rebuilds of hello replicated table.</span></span> 

<span data-ttu-id="9ca83-127">Реплицированные таблицы подходят в ситуациях, когда:</span><span class="sxs-lookup"><span data-stu-id="9ca83-127">Consider using a replicated table when:</span></span>

- <span data-ttu-id="9ca83-128">размер таблицы Hello на диске — меньше, чем 2 ГБ, вне зависимости от hello количество строк.</span><span class="sxs-lookup"><span data-stu-id="9ca83-128">hello table size on disk is less than 2 GB, regardless of hello number of rows.</span></span> <span data-ttu-id="9ca83-129">размер hello toofind таблицы, можно использовать hello [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) команды: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`.</span><span class="sxs-lookup"><span data-stu-id="9ca83-129">toofind hello size of a table, you can use hello [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) command: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`.</span></span> 
- <span data-ttu-id="9ca83-130">Таблица Hello используется в соединениях, которые в противном случае потребуется перемещение данных.</span><span class="sxs-lookup"><span data-stu-id="9ca83-130">hello table is used in joins that would otherwise require data movement.</span></span> <span data-ttu-id="9ca83-131">Например соединение в таблицах, распределенных хэш требует перемещения данных hello присоединяемый столбцы не являются hello же столбец распределения.</span><span class="sxs-lookup"><span data-stu-id="9ca83-131">For example, a join on hash-distributed tables requires data movement when hello joining columns are not hello same distribution column.</span></span> <span data-ttu-id="9ca83-132">Если одна из таблиц распределенного хэш hello мал, рассмотрите возможность реплицируемой таблицы.</span><span class="sxs-lookup"><span data-stu-id="9ca83-132">If one of hello hash-distributed tables is small, consider a replicated table.</span></span> <span data-ttu-id="9ca83-133">Для соединения в таблице с распределением методом циклического перебора требуется перемещение данных.</span><span class="sxs-lookup"><span data-stu-id="9ca83-133">A join on a round-robin table requires data movement.</span></span> <span data-ttu-id="9ca83-134">В большинстве случаев вместо таких таблиц рекомендуется использовать реплицированные таблицы.</span><span class="sxs-lookup"><span data-stu-id="9ca83-134">We recommend using replicated tables instead of round-robin tables in most cases.</span></span> 


<span data-ttu-id="9ca83-135">Рассмотрите возможность преобразования существующего распределенного tooa таблицы реплицируются таблицу при:</span><span class="sxs-lookup"><span data-stu-id="9ca83-135">Consider converting an existing distributed table tooa replicated table when:</span></span>

- <span data-ttu-id="9ca83-136">Использование операций перемещения данных, передающих hello данных tooall hello вычислительные узлы планы запроса.</span><span class="sxs-lookup"><span data-stu-id="9ca83-136">Query plans use data movement operations that broadcast hello data tooall hello Compute nodes.</span></span> <span data-ttu-id="9ca83-137">Hello BroadcastMoveOperation расходуется и снижает производительность запросов.</span><span class="sxs-lookup"><span data-stu-id="9ca83-137">hello BroadcastMoveOperation is expensive and slows query performance.</span></span> <span data-ttu-id="9ca83-138">использовать tooview операций перемещения данных в планах запросов [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="9ca83-138">tooview data movement operations in query plans, use [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).</span></span>
 
<span data-ttu-id="9ca83-139">Реплицированные таблицы не может привести к hello лучшую производительность при:</span><span class="sxs-lookup"><span data-stu-id="9ca83-139">Replicated tables may not yield hello best query performance when:</span></span>

- <span data-ttu-id="9ca83-140">Таблица Hello имеет часто вставки, обновления и удаления операций.</span><span class="sxs-lookup"><span data-stu-id="9ca83-140">hello table has frequent insert, update, and delete operations.</span></span> <span data-ttu-id="9ca83-141">Эти операций языка обработки данных требуется повторное создание таблицы реплицируются hello.</span><span class="sxs-lookup"><span data-stu-id="9ca83-141">These data manipulation language (DML) operations require a rebuild of hello replicated table.</span></span> <span data-ttu-id="9ca83-142">Зачастую перестроение приводит к снижению производительности.</span><span class="sxs-lookup"><span data-stu-id="9ca83-142">Rebuilding frequently can cause slower performance.</span></span>
- <span data-ttu-id="9ca83-143">часто масштабируется Hello хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="9ca83-143">hello data warehouse is scaled frequently.</span></span> <span data-ttu-id="9ca83-144">Масштабирование хранилище данных изменяется hello количество вычислительных узлов, что влечет за собой повторное построение.</span><span class="sxs-lookup"><span data-stu-id="9ca83-144">Scaling a data warehouse changes hello number of Compute nodes, which incurs a rebuild.</span></span>
- <span data-ttu-id="9ca83-145">Hello таблица содержит много столбцов, но данные обычно доступ только небольшое число столбцов.</span><span class="sxs-lookup"><span data-stu-id="9ca83-145">hello table has a large number of columns, but data operations typically access only a small number of columns.</span></span> <span data-ttu-id="9ca83-146">В этом случае вместо репликации hello всю таблицу, возможно, более эффективные toohash распространения hello таблицу и затем создать индекс для hello часто используемых столбцов.</span><span class="sxs-lookup"><span data-stu-id="9ca83-146">In this scenario, instead of replicating hello entire table, it might be more effective toohash distribute hello table, and then create an index on hello frequently accessed columns.</span></span> <span data-ttu-id="9ca83-147">Когда запрос требует перемещения данных, хранилище данных SQL, перенос данных в hello запросить столбцы всего.</span><span class="sxs-lookup"><span data-stu-id="9ca83-147">When a query requires data movement, SQL Data Warehouse only moves data in hello requested columns.</span></span> 



## <a name="use-replicated-tables-with-simple-query-predicates"></a><span data-ttu-id="9ca83-148">Использование реплицированных таблиц с предикатами простого запроса</span><span class="sxs-lookup"><span data-stu-id="9ca83-148">Use replicated tables with simple query predicates</span></span>
<span data-ttu-id="9ca83-149">Прежде чем выбрать toodistribute или репликации таблицы, подумайте о hello типов запросов плана toorun hello для таблицы.</span><span class="sxs-lookup"><span data-stu-id="9ca83-149">Before you choose toodistribute or replicate a table, think about hello types of queries you plan toorun against hello table.</span></span> <span data-ttu-id="9ca83-150">Когда это возможно:</span><span class="sxs-lookup"><span data-stu-id="9ca83-150">Whenever possible,</span></span>

- <span data-ttu-id="9ca83-151">Используйте реплицированные таблицы для запросов с предикатами простого запроса, например равенства или неравенства.</span><span class="sxs-lookup"><span data-stu-id="9ca83-151">Use replicated tables for queries with simple query predicates, such as equality or inequality.</span></span>
- <span data-ttu-id="9ca83-152">Используйте распределенные таблицы для запросов с предикатами сложного запроса, например LIKE или NOT LIKE.</span><span class="sxs-lookup"><span data-stu-id="9ca83-152">Use distributed tables for queries with complex query predicates, such as LIKE or NOT LIKE.</span></span>

<span data-ttu-id="9ca83-153">Процессор запросов выполните лучше всего при hello работа распределяется по всем hello вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="9ca83-153">CPU-intensive queries perform best when hello work is distributed across all of hello Compute nodes.</span></span> <span data-ttu-id="9ca83-154">Например, запросы, которые запускают вычисления для каждой строки таблицы, выполняются более эффективно в распределенных таблицах, чем реплицированных.</span><span class="sxs-lookup"><span data-stu-id="9ca83-154">For example, queries that run computations on each row of a table perform better on distributed tables than replicated tables.</span></span> <span data-ttu-id="9ca83-155">Поскольку реплицируемой таблицы хранятся в полном объеме на каждом вычислительном узле, процессор запрос к реплицируемой таблицы запускает hello всю таблицу на каждом вычислительном узле.</span><span class="sxs-lookup"><span data-stu-id="9ca83-155">Since a replicated table is stored in full on each Compute node, a CPU-intensive query against a replicated table runs against hello entire table on every Compute node.</span></span> <span data-ttu-id="9ca83-156">Hello лишние вычисления может снизить производительность запроса.</span><span class="sxs-lookup"><span data-stu-id="9ca83-156">hello extra computation can slow query performance.</span></span>

<span data-ttu-id="9ca83-157">Например, в этом запросе содержится сложный предикат.</span><span class="sxs-lookup"><span data-stu-id="9ca83-157">For example, this query has a complex predicate.</span></span>  <span data-ttu-id="9ca83-158">Он выполняется быстрее, когда в качестве поставщика выступает распределенная таблица вместо реплицированной таблицы.</span><span class="sxs-lookup"><span data-stu-id="9ca83-158">It runs faster when supplier is a distributed table instead of a replicated table.</span></span> <span data-ttu-id="9ca83-159">В этом примере для поставщика можно выполнить хэш-распределение или распределение методом циклического перебора.</span><span class="sxs-lookup"><span data-stu-id="9ca83-159">In this example, supplier can be hash-distributed or round-robin distributed.</span></span>

```sql

SELECT EnglishProductName 
FROM DimProduct 
WHERE EnglishDescription LIKE '%frame%comfortable%'

```

## <a name="convert-existing-round-robin-tables-tooreplicated-tables"></a><span data-ttu-id="9ca83-160">Преобразование существующих таблиц tooreplicated таблиц циклический перебор</span><span class="sxs-lookup"><span data-stu-id="9ca83-160">Convert existing round-robin tables tooreplicated tables</span></span>
<span data-ttu-id="9ca83-161">При наличии таблиц циклический перебор, рекомендуется их преобразования tooreplicated таблицы, если они удовлетворяют условиям, приведенным в этой статье.</span><span class="sxs-lookup"><span data-stu-id="9ca83-161">If you already have round-robin tables, we recommend converting them tooreplicated tables if they meet with criteria outlined in this article.</span></span> <span data-ttu-id="9ca83-162">Реплицированные таблицы повышает производительность для циклического таблицы так, как они устраняют необходимость hello для перемещения данных.</span><span class="sxs-lookup"><span data-stu-id="9ca83-162">Replicated tables improve performance over round-robin tables because they eliminate hello need for data movement.</span></span>  <span data-ttu-id="9ca83-163">Для соединений в циклической таблице всегда требуется перемещение данных.</span><span class="sxs-lookup"><span data-stu-id="9ca83-163">A round-robin table always requires data movement for joins.</span></span> 

<span data-ttu-id="9ca83-164">В этом примере используется [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) tooa таблицы DimSalesTerritory hello toochange реплицированная таблица.</span><span class="sxs-lookup"><span data-stu-id="9ca83-164">This example uses [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) toochange hello DimSalesTerritory table tooa replicated table.</span></span> <span data-ttu-id="9ca83-165">В данном примере неважно, была ли таблица DimSalesTerritory хэш-распределена или распределена методом циклического перебора.</span><span class="sxs-lookup"><span data-stu-id="9ca83-165">This example works regardless of whether DimSalesTerritory is hash-distributed or round-robin.</span></span>

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
RENAME OBJECT [dbo].[DimSalesTerritory] too[DimSalesTerritory_old];
RENAME OBJECT [dbo].[DimSalesTerritory_REPLICATE] too[DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```  

### <a name="query-performance-example-for-round-robin-versus-replicated"></a><span data-ttu-id="9ca83-166">Пример производительности запросов для циклической и реплицированной таблиц</span><span class="sxs-lookup"><span data-stu-id="9ca83-166">Query performance example for round-robin versus replicated</span></span> 

<span data-ttu-id="9ca83-167">Поскольку hello вся таблица уже существует на каждом вычислительном узле реплицируемой таблицы не требует перемещения данных для соединения.</span><span class="sxs-lookup"><span data-stu-id="9ca83-167">A replicated table does not require any data movement for joins because hello entire table is already present on each Compute node.</span></span> <span data-ttu-id="9ca83-168">Циклического распределенных таблиц измерений hello, соединение копирует hello таблицу измерения в полной tooeach вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="9ca83-168">If hello dimension tables are round-robin distributed, a join copies hello dimension table in full tooeach Compute node.</span></span> <span data-ttu-id="9ca83-169">данные toomove hello, hello план запроса содержит эта операция называется BroadcastMoveOperation.</span><span class="sxs-lookup"><span data-stu-id="9ca83-169">toomove hello data, hello query plan contains an operation called BroadcastMoveOperation.</span></span> <span data-ttu-id="9ca83-170">Операции перемещения данных данного типа снижают производительность запросов. Устранить это можно с помощью реплицированных таблиц.</span><span class="sxs-lookup"><span data-stu-id="9ca83-170">This type of data movement operation slows query performance and is eliminated by using replicated tables.</span></span> <span data-ttu-id="9ca83-171">действия плана запроса tooview, использовать hello [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) представления системного каталога.</span><span class="sxs-lookup"><span data-stu-id="9ca83-171">tooview query plan steps, use hello [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) system catalog view.</span></span> 

<span data-ttu-id="9ca83-172">Например, в следующем запросе к схема AdventureWorks hello hello ` FactInternetSales` таблицы распределенных хэш.</span><span class="sxs-lookup"><span data-stu-id="9ca83-172">For example, in following query against hello AdventureWorks schema, hello ` FactInternetSales` table is hash-distributed.</span></span> <span data-ttu-id="9ca83-173">Hello `DimDate` и `DimSalesTerritory` меньшего размера таблицы измерения.</span><span class="sxs-lookup"><span data-stu-id="9ca83-173">hello `DimDate` and `DimSalesTerritory` tables are smaller dimension tables.</span></span> <span data-ttu-id="9ca83-174">Этот запрос возвращает hello общий объем продаж в Северной Америке для 2004 финансовом году.</span><span class="sxs-lookup"><span data-stu-id="9ca83-174">This query returns hello total sales in North America for fiscal year 2004:</span></span>
 
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
<span data-ttu-id="9ca83-175">Мы повторно создали таблицы `DimDate` и `DimSalesTerritory` как циклические таблицы.</span><span class="sxs-lookup"><span data-stu-id="9ca83-175">We re-created `DimDate` and `DimSalesTerritory` as round-robin tables.</span></span> <span data-ttu-id="9ca83-176">В результате запроса hello показал hello, следуя плана запроса, который имеет несколько вещания переноса операций:</span><span class="sxs-lookup"><span data-stu-id="9ca83-176">As a result, hello query showed hello following query plan, which has multiple broadcast move operations:</span></span> 
 
![План запроса с циклическим перебором](media/design-guidance-for-replicated-tables/round-robin-tables-query-plan.jpg) 

<span data-ttu-id="9ca83-178">Повторно создан `DimDate` и `DimSalesTerritory` как в реплицированных таблицах и запущена hello запрос повторно.</span><span class="sxs-lookup"><span data-stu-id="9ca83-178">We re-created `DimDate` and `DimSalesTerritory` as replicated tables, and ran hello query again.</span></span> <span data-ttu-id="9ca83-179">Hello результирующий план запроса намного короче, и не иметь любой передает переход.</span><span class="sxs-lookup"><span data-stu-id="9ca83-179">hello resulting query plan is much shorter and does not have any broadcast moves.</span></span>

![План запроса с репликацией](media/design-guidance-for-replicated-tables/replicated-tables-query-plan.jpg) 


## <a name="performance-considerations-for-modifying-replicated-tables"></a><span data-ttu-id="9ca83-181">Рекомендации по повышению производительности для изменения реплицированных таблиц</span><span class="sxs-lookup"><span data-stu-id="9ca83-181">Performance considerations for modifying replicated tables</span></span>
<span data-ttu-id="9ca83-182">Хранилище данных SQL реализует реплицированной таблицы, сохраняя главной версии таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="9ca83-182">SQL Data Warehouse implements a replicated table by maintaining a master version of hello table.</span></span> <span data-ttu-id="9ca83-183">Он копирует hello базы данных распространителя главной версии tooone на каждом вычислительном узле.</span><span class="sxs-lookup"><span data-stu-id="9ca83-183">It copies hello master version tooone distribution database on each Compute node.</span></span> <span data-ttu-id="9ca83-184">При наличии изменений, хранилище данных SQL обновляет сначала hello главную таблицу.</span><span class="sxs-lookup"><span data-stu-id="9ca83-184">When there is a change, SQL Data Warehouse first updates hello master table.</span></span> <span data-ttu-id="9ca83-185">Затем он требуется повторное создание таблиц hello на каждом вычислительном узле.</span><span class="sxs-lookup"><span data-stu-id="9ca83-185">Then it requires a rebuild of hello tables on each Compute node.</span></span> <span data-ttu-id="9ca83-186">Перестроение реплицируемой таблицы включает копирование hello таблицы tooeach вычислительных узлов и последующее перестроение индексов hello.</span><span class="sxs-lookup"><span data-stu-id="9ca83-186">A rebuild of a replicated table includes copying hello table tooeach Compute node and then rebuilding hello indexes.</span></span>

<span data-ttu-id="9ca83-187">Перестроение требуется после следующего:</span><span class="sxs-lookup"><span data-stu-id="9ca83-187">Rebuilds are required after:</span></span>
- <span data-ttu-id="9ca83-188">Загрузка или изменение данных</span><span class="sxs-lookup"><span data-stu-id="9ca83-188">Data is loaded or modified</span></span>
- <span data-ttu-id="9ca83-189">хранилище данных Hello — другой параметр DWU масштабированный tooa</span><span class="sxs-lookup"><span data-stu-id="9ca83-189">hello data warehouse is scaled tooa different DWU setting</span></span>
- <span data-ttu-id="9ca83-190">Обновление определения таблицы</span><span class="sxs-lookup"><span data-stu-id="9ca83-190">Table definition is updated</span></span>

<span data-ttu-id="9ca83-191">Перестроение не требуется после следующего:</span><span class="sxs-lookup"><span data-stu-id="9ca83-191">Rebuilds are not required after:</span></span>
- <span data-ttu-id="9ca83-192">Выполнение операции приостановки</span><span class="sxs-lookup"><span data-stu-id="9ca83-192">Pause operation</span></span>
- <span data-ttu-id="9ca83-193">Выполнение операции возобновления</span><span class="sxs-lookup"><span data-stu-id="9ca83-193">Resume operation</span></span>

<span data-ttu-id="9ca83-194">Перестроение Hello не происходит немедленно после изменения данных.</span><span class="sxs-lookup"><span data-stu-id="9ca83-194">hello rebuild does not happen immediately after data is modified.</span></span> <span data-ttu-id="9ca83-195">Вместо этого hello перестройка инициируется hello первый раз, запрос выбирает данные из таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="9ca83-195">Instead, hello rebuild is triggered hello first time a query selects from hello table.</span></span>  <span data-ttu-id="9ca83-196">В инструкции select начальной hello из таблицы hello находятся действия toorebuild hello реплицируемой таблицы.</span><span class="sxs-lookup"><span data-stu-id="9ca83-196">Within hello initial select statement from hello table are steps toorebuild hello replicated table.</span></span>  <span data-ttu-id="9ca83-197">Так как в запросе hello выполняется перестроение hello, hello влияние toohello начальной инструкции select может быть значительной в зависимости от размера таблицы hello hello.</span><span class="sxs-lookup"><span data-stu-id="9ca83-197">Because hello rebuild is done within hello query, hello impact toohello initial select statement could be significant depending on hello size of hello table.</span></span>  <span data-ttu-id="9ca83-198">Если участвуют несколько реплицируемых таблиц, требующие повторной сборки, каждая копия будет перестроен последовательно как действия в рамках инструкции hello.</span><span class="sxs-lookup"><span data-stu-id="9ca83-198">If multiple replicated tables are involved that need a rebuild, each copy is rebuilt serially as steps within hello statement.</span></span>  <span data-ttu-id="9ca83-199">согласованность данных toomaintain во время перестроения hello hello реплицируются hello таблице применяется монопольная блокировка таблицы.</span><span class="sxs-lookup"><span data-stu-id="9ca83-199">toomaintain data consistency during hello rebuild of hello replicated table an exclusive lock is taken on hello table.</span></span>  <span data-ttu-id="9ca83-200">Hello Блокировка предотвращает все таблицы access toohello hello время перестроения hello.</span><span class="sxs-lookup"><span data-stu-id="9ca83-200">hello lock prevents all access toohello table for hello duration of hello rebuild.</span></span> 

### <a name="use-indexes-conservatively"></a><span data-ttu-id="9ca83-201">Консервативный подход к использованию индексов</span><span class="sxs-lookup"><span data-stu-id="9ca83-201">Use indexes conservatively</span></span>
<span data-ttu-id="9ca83-202">Стандартные рекомендации индексирования относятся tooreplicated таблиц.</span><span class="sxs-lookup"><span data-stu-id="9ca83-202">Standard indexing practices apply tooreplicated tables.</span></span> <span data-ttu-id="9ca83-203">Хранилище данных SQL перестраивает каждый индекс реплицируемой таблицы в процессе перестроения hello.</span><span class="sxs-lookup"><span data-stu-id="9ca83-203">SQL Data Warehouse rebuilds each replicated table index as part of hello rebuild.</span></span> <span data-ttu-id="9ca83-204">Используйте индексы только в том случае, если hello выигрыш в производительности перевешивает стоимость hello перестроение индексов hello.</span><span class="sxs-lookup"><span data-stu-id="9ca83-204">Only use indexes when hello performance gain outweighs hello cost of rebuilding hello indexes.</span></span>  
 
### <a name="batch-data-loads"></a><span data-ttu-id="9ca83-205">Пакетная загрузка данных</span><span class="sxs-lookup"><span data-stu-id="9ca83-205">Batch data loads</span></span>
<span data-ttu-id="9ca83-206">При загрузке данных в реплицированных таблицах, попробуйте toominimize перестроение путем объединения загружает пакет.</span><span class="sxs-lookup"><span data-stu-id="9ca83-206">When loading data into replicated tables, try toominimize rebuilds by batching loads together.</span></span> <span data-ttu-id="9ca83-207">Выполните все загрузки hello в пакетном режиме, перед выполнением инструкции select.</span><span class="sxs-lookup"><span data-stu-id="9ca83-207">Perform all hello batched loads before running select statements.</span></span>

<span data-ttu-id="9ca83-208">Например, ниже представлен шаблон загрузки данных из четырех источников и запуска четырех операций перестроения.</span><span class="sxs-lookup"><span data-stu-id="9ca83-208">For example, this load pattern loads data from four sources and invokes four rebuilds.</span></span> 

- <span data-ttu-id="9ca83-209">Загрузка из источника 1.</span><span class="sxs-lookup"><span data-stu-id="9ca83-209">Load from source 1.</span></span>
- <span data-ttu-id="9ca83-210">Инструкция SELECT вызывает перестроение 1.</span><span class="sxs-lookup"><span data-stu-id="9ca83-210">Select statement triggers rebuild 1.</span></span>
- <span data-ttu-id="9ca83-211">Загрузка из источника 2.</span><span class="sxs-lookup"><span data-stu-id="9ca83-211">Load from source 2.</span></span>
- <span data-ttu-id="9ca83-212">Инструкция SELECT вызывает перестроение 2.</span><span class="sxs-lookup"><span data-stu-id="9ca83-212">Select statement triggers rebuild 2.</span></span>
- <span data-ttu-id="9ca83-213">Загрузка из источника 3.</span><span class="sxs-lookup"><span data-stu-id="9ca83-213">Load from source 3.</span></span>
- <span data-ttu-id="9ca83-214">Инструкция SELECT вызывает перестроение 3.</span><span class="sxs-lookup"><span data-stu-id="9ca83-214">Select statement triggers rebuild 3.</span></span>
- <span data-ttu-id="9ca83-215">Загрузка из источника 4.</span><span class="sxs-lookup"><span data-stu-id="9ca83-215">Load from source 4.</span></span>
- <span data-ttu-id="9ca83-216">Инструкция SELECT вызывает перестроение 4.</span><span class="sxs-lookup"><span data-stu-id="9ca83-216">Select statement triggers rebuild 4.</span></span>

<span data-ttu-id="9ca83-217">Например, ниже представлен шаблон загрузки данных из четырех источников и запуска только одной операции перестроения.</span><span class="sxs-lookup"><span data-stu-id="9ca83-217">For example, this load pattern loads data from four sources, but only invokes one rebuild.</span></span>

- <span data-ttu-id="9ca83-218">Загрузка из источника 1.</span><span class="sxs-lookup"><span data-stu-id="9ca83-218">Load from source 1.</span></span>
- <span data-ttu-id="9ca83-219">Загрузка из источника 2.</span><span class="sxs-lookup"><span data-stu-id="9ca83-219">Load from source 2.</span></span>
- <span data-ttu-id="9ca83-220">Загрузка из источника 3.</span><span class="sxs-lookup"><span data-stu-id="9ca83-220">Load from source 3.</span></span>
- <span data-ttu-id="9ca83-221">Загрузка из источника 4.</span><span class="sxs-lookup"><span data-stu-id="9ca83-221">Load from source 4.</span></span>
- <span data-ttu-id="9ca83-222">Инструкция SELECT вызывает перестроение.</span><span class="sxs-lookup"><span data-stu-id="9ca83-222">Select statement triggers rebuild.</span></span>


### <a name="rebuild-a-replicated-table-after-a-batch-load"></a><span data-ttu-id="9ca83-223">Перестроение реплицированной таблицы после пакетной загрузки</span><span class="sxs-lookup"><span data-stu-id="9ca83-223">Rebuild a replicated table after a batch load</span></span>
<span data-ttu-id="9ca83-224">tooensure согласованного выполнения запросов, рекомендуется принудительное обновление таблиц, реплицированных hello после загрузки пакета.</span><span class="sxs-lookup"><span data-stu-id="9ca83-224">tooensure consistent query execution times, we recommend forcing a refresh of hello replicated tables after a batch load.</span></span> <span data-ttu-id="9ca83-225">В противном случае — первый запрос hello должен ожидать toorefresh hello таблиц, включая перестроение индексов hello.</span><span class="sxs-lookup"><span data-stu-id="9ca83-225">Otherwise, hello first query must wait for hello tables toorefresh, which includes rebuilding hello indexes.</span></span> <span data-ttu-id="9ca83-226">В зависимости от размера hello и количество затронутых реплицированных таблицах влияние на производительность hello может оказаться значительным.</span><span class="sxs-lookup"><span data-stu-id="9ca83-226">Depending on hello size and number of replicated tables affected, hello performance impact can be significant.</span></span>  

<span data-ttu-id="9ca83-227">Этот запрос использует hello [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) hello toolist динамического административного Представления в реплицированных таблицах, которые были изменены, но не может быть перестроен.</span><span class="sxs-lookup"><span data-stu-id="9ca83-227">This query uses hello [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) DMV toolist hello replicated tables that have been modified, but not rebuilt.</span></span>

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
 
<span data-ttu-id="9ca83-228">tooforce перестроения, запустите следующие инструкции для каждой таблицы в предшествующих выходных данных hello hello.</span><span class="sxs-lookup"><span data-stu-id="9ca83-228">tooforce a rebuild, run hello following statement on each table in hello preceding output.</span></span> 

```sql
SELECT TOP 1 * FROM [ReplicatedTable]
``` 
 
## <a name="next-steps"></a><span data-ttu-id="9ca83-229">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9ca83-229">Next steps</span></span> 
<span data-ttu-id="9ca83-230">toocreate реплицированной таблицы, используйте один из следующих инструкций:</span><span class="sxs-lookup"><span data-stu-id="9ca83-230">toocreate a replicated table, use one of these statements:</span></span>

- [<span data-ttu-id="9ca83-231">CREATE TABLE (хранилище данных Azure SQL)</span><span class="sxs-lookup"><span data-stu-id="9ca83-231">CREATE TABLE (Azure SQL Data Warehouse)</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-azure-sql-data-warehouse)
- [<span data-ttu-id="9ca83-232">CREATE TABLE AS SELECT (хранилище данных Azure SQL)</span><span class="sxs-lookup"><span data-stu-id="9ca83-232">CREATE TABLE AS SELECT (Azure SQL Data Warehouse</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse)

<span data-ttu-id="9ca83-233">Обзор распределенных таблиц см. в разделе [Распределенные таблицы](sql-data-warehouse-tables-distribute.md).</span><span class="sxs-lookup"><span data-stu-id="9ca83-233">For an overview of distributed tables, see [distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>



