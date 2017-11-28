---
title: "Оптимизация транзакций для хранилища данных SQL | Документация Майкрософт"
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
ms.openlocfilehash: f9f19d75a37351b3562ce8c2f3629df14c5437c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="optimizing-transactions-for-sql-data-warehouse"></a><span data-ttu-id="cfd5b-103">Оптимизация транзакций для хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="cfd5b-103">Optimizing transactions for SQL Data Warehouse</span></span>
<span data-ttu-id="cfd5b-104">В этой статье объясняется, как оптимизировать производительность кода обработки транзакций, чтобы свести к минимуму риск длительных откатов.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-104">This article explains how to optimize the performance of your transactional code while minimizing risk for long rollbacks.</span></span>

## <a name="transactions-and-logging"></a><span data-ttu-id="cfd5b-105">Транзакции и ведение журнала</span><span class="sxs-lookup"><span data-stu-id="cfd5b-105">Transactions and logging</span></span>
<span data-ttu-id="cfd5b-106">Транзакции представляют собой важную часть ядра реляционной СУБД.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-106">Transactions are an important component of a relational database engine.</span></span> <span data-ttu-id="cfd5b-107">Хранилище данных SQL использует транзакции во время изменения данных.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-107">SQL Data Warehouse uses transactions during data modification.</span></span> <span data-ttu-id="cfd5b-108">Эти транзакции могут быть явными или неявными.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-108">These transactions can be explicit or implicit.</span></span> <span data-ttu-id="cfd5b-109">Одиночные инструкции `INSERT`, `UPDATE` и `DELETE` являются примерами неявных транзакций.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-109">Single `INSERT`, `UPDATE` and `DELETE` statements are all examples of implicit transactions.</span></span> <span data-ttu-id="cfd5b-110">Явные транзакции открыто создает разработчик с помощью инструкций `BEGIN TRAN`, `COMMIT TRAN` или `ROLLBACK TRAN`. Эти транзакции обычно используются, когда несколько инструкций изменения нужно связать в одну неделимую единицу.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-110">Explicit transactions are written explicitly by a developer using `BEGIN TRAN`, `COMMIT TRAN` or `ROLLBACK TRAN` and are typically used when multiple modification statements need to be tied together in a single atomic unit.</span></span> 

<span data-ttu-id="cfd5b-111">Хранилище данных SQL Azure вносит изменения в базу данных с помощью журналов транзакций.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-111">Azure SQL Data Warehouse commits changes to the database using transaction logs.</span></span> <span data-ttu-id="cfd5b-112">У каждого распределения есть свой журнал транзакций.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-112">Each distribution has its own transaction log.</span></span> <span data-ttu-id="cfd5b-113">Запись в журналы транзакций выполняется автоматически.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-113">Transaction log writes are automatic.</span></span> <span data-ttu-id="cfd5b-114">Настраивать что-либо не требуется.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-114">There is no configuration required.</span></span> <span data-ttu-id="cfd5b-115">Этот процесс гарантирует запись, но в то же время увеличивает нагрузку на систему.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-115">However, whilst this process guarantees the write it does introduce an overhead in the system.</span></span> <span data-ttu-id="cfd5b-116">Чтобы минимизировать этот эффект, нужно написать эффективный код транзакции.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-116">You can minimize this impact by writing transactionally efficient code.</span></span> <span data-ttu-id="cfd5b-117">Такой код можно условно разделить на две категории.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-117">Transactionally efficient code broadly falls into two categories.</span></span>

* <span data-ttu-id="cfd5b-118">Используйте конструкции минимального ведения журналов, когда это возможно.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-118">Leverage minimal logging constructs where possible</span></span>
* <span data-ttu-id="cfd5b-119">Обрабатывайте данные в пакетах, чтобы избежать одиночных длительных транзакций.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-119">Process data using scoped batches to avoid singular long running transactions</span></span>
* <span data-ttu-id="cfd5b-120">Пользуйтесь шаблоном переключения разделов при внесении значительных изменений в тот или иной раздел.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-120">Adopt a partition switching pattern for large modifications to a given partition</span></span>

## <a name="minimal-vs-full-logging"></a><span data-ttu-id="cfd5b-121">Минимальное ведение журнала и полное ведение журнала</span><span class="sxs-lookup"><span data-stu-id="cfd5b-121">Minimal vs. full logging</span></span>
<span data-ttu-id="cfd5b-122">В отличие от полностью регистрируемых операций, которые с помощью журнала транзакций отслеживают каждое изменение строки, минимально регистрируемые операции отслеживают только выделения экстента и изменения метаданных.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-122">Unlike fully logged operations, which use the transaction log to keep track of every row change, minimally logged operations keep track of extent allocations and meta-data changes only.</span></span> <span data-ttu-id="cfd5b-123">Иными словами, в рамках минимального ведения журнала протоколируется только та информация, которая нужна, чтобы откатить транзакцию в случае сбоя или явного запроса (`ROLLBACK TRAN`).</span><span class="sxs-lookup"><span data-stu-id="cfd5b-123">Therefore, minimal logging involves logging only the information that is required to rollback the transaction in the event of a failure or an explicit request (`ROLLBACK TRAN`).</span></span> <span data-ttu-id="cfd5b-124">Так как в журнал транзакций вносится гораздо меньше информации, минимально регистрируемая операция отличается от полностью регистрируемой операции аналогичного размера более высокой производительностью.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-124">As much less information is tracked in the transaction log, a minimally logged operation performs better than a similarly sized fully logged operation.</span></span> <span data-ttu-id="cfd5b-125">Кроме того, так как в журнал транзакций вносится меньше записей, создается меньше данных журнала и процесс ввода-вывода становится эффективнее.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-125">Furthermore, because fewer writes go the transaction log, a much smaller amount of log data is generated and so is more I/O efficient.</span></span>

<span data-ttu-id="cfd5b-126">Ограничения безопасности транзакций применяются только к полностью регистрируемым операциям.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-126">The transaction safety limits only apply to fully logged operations.</span></span>

> [!NOTE]
> <span data-ttu-id="cfd5b-127">Минимально регистрируемые операции могут быть частью явных транзакций.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-127">Minimally logged operations can participate in explicit transactions.</span></span> <span data-ttu-id="cfd5b-128">Так как все изменения в структурах выделения отслеживаются, такие операции можно откатывать.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-128">As all changes in allocation structures are tracked, it is possible to roll back minimally logged operations.</span></span> <span data-ttu-id="cfd5b-129">Важно понимать, что минимальная регистрация изменений — это не отсутствие регистрации.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-129">It is important to understand that the change is "minimally" logged it is not un-logged.</span></span>
> 
> 

## <a name="minimally-logged-operations"></a><span data-ttu-id="cfd5b-130">Минимально регистрируемые операции</span><span class="sxs-lookup"><span data-stu-id="cfd5b-130">Minimally logged operations</span></span>
<span data-ttu-id="cfd5b-131">Минимально регистрируемыми могут быть такие операции:</span><span class="sxs-lookup"><span data-stu-id="cfd5b-131">The following operations are capable of being minimally logged:</span></span>

* <span data-ttu-id="cfd5b-132">Инструкция CREATE TABLE AS SELECT ([CTAS][CTAS])</span><span class="sxs-lookup"><span data-stu-id="cfd5b-132">CREATE TABLE AS SELECT ([CTAS][CTAS])</span></span>
* <span data-ttu-id="cfd5b-133">INSERT..SELECT</span><span class="sxs-lookup"><span data-stu-id="cfd5b-133">INSERT..SELECT</span></span>
* <span data-ttu-id="cfd5b-134">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="cfd5b-134">CREATE INDEX</span></span>
* <span data-ttu-id="cfd5b-135">ALTER INDEX REBUILD</span><span class="sxs-lookup"><span data-stu-id="cfd5b-135">ALTER INDEX REBUILD</span></span>
* <span data-ttu-id="cfd5b-136">DROP INDEX</span><span class="sxs-lookup"><span data-stu-id="cfd5b-136">DROP INDEX</span></span>
* <span data-ttu-id="cfd5b-137">TRUNCATE TABLE</span><span class="sxs-lookup"><span data-stu-id="cfd5b-137">TRUNCATE TABLE</span></span>
* <span data-ttu-id="cfd5b-138">DROP TABLE</span><span class="sxs-lookup"><span data-stu-id="cfd5b-138">DROP TABLE</span></span>
* <span data-ttu-id="cfd5b-139">ALTER TABLE SWITCH PARTITION</span><span class="sxs-lookup"><span data-stu-id="cfd5b-139">ALTER TABLE SWITCH PARTITION</span></span>

<!--
- MERGE
- UPDATE on LOB Types .WRITE
- SELECT..INTO
-->

> [!NOTE]
> <span data-ttu-id="cfd5b-140">Ограничение безопасности транзакций не влияет на внутренние операции перемещения данных (например, `BROADCAST` и `SHUFFLE`).</span><span class="sxs-lookup"><span data-stu-id="cfd5b-140">Internal data movement operations (such as `BROADCAST` and `SHUFFLE`) are not affected by the transaction safety limit.</span></span>
> 
> 

## <a name="minimal-logging-with-bulk-load"></a><span data-ttu-id="cfd5b-141">Минимальное ведение журнала и массовая загрузка</span><span class="sxs-lookup"><span data-stu-id="cfd5b-141">Minimal logging with bulk load</span></span>
<span data-ttu-id="cfd5b-142">`CTAS` и `INSERT...SELECT` — это операции массовой загрузки.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-142">`CTAS` and `INSERT...SELECT` are both bulk load operations.</span></span> <span data-ttu-id="cfd5b-143">Тем не менее обе они зависят от определения целевой таблицы и сценария загрузки.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-143">However, both are influenced by the target table definition and depend on the load scenario.</span></span> <span data-ttu-id="cfd5b-144">В таблице, приведенной ниже, перечислены условия, в зависимости от которых ваша массовая операция будет регистрироваться полностью или минимально.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-144">Below is a table that explains if your bulk operation will be fully or minimally logged:</span></span>  

| <span data-ttu-id="cfd5b-145">Первичный индекс</span><span class="sxs-lookup"><span data-stu-id="cfd5b-145">Primary Index</span></span> | <span data-ttu-id="cfd5b-146">Сценарий загрузки</span><span class="sxs-lookup"><span data-stu-id="cfd5b-146">Load Scenario</span></span> | <span data-ttu-id="cfd5b-147">Режим ведения журнала</span><span class="sxs-lookup"><span data-stu-id="cfd5b-147">Logging Mode</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cfd5b-148">Куча</span><span class="sxs-lookup"><span data-stu-id="cfd5b-148">Heap</span></span> |<span data-ttu-id="cfd5b-149">Любой</span><span class="sxs-lookup"><span data-stu-id="cfd5b-149">Any</span></span> |<span data-ttu-id="cfd5b-150">**Минимальный**</span><span class="sxs-lookup"><span data-stu-id="cfd5b-150">**Minimal**</span></span> |
| <span data-ttu-id="cfd5b-151">Кластеризованный индекс</span><span class="sxs-lookup"><span data-stu-id="cfd5b-151">Clustered Index</span></span> |<span data-ttu-id="cfd5b-152">Пустая целевая таблица</span><span class="sxs-lookup"><span data-stu-id="cfd5b-152">Empty target table</span></span> |<span data-ttu-id="cfd5b-153">**Минимальный**</span><span class="sxs-lookup"><span data-stu-id="cfd5b-153">**Minimal**</span></span> |
| <span data-ttu-id="cfd5b-154">Кластеризованный индекс</span><span class="sxs-lookup"><span data-stu-id="cfd5b-154">Clustered Index</span></span> |<span data-ttu-id="cfd5b-155">Загруженные строки не перекрывают существующие страницы в целевом объекте</span><span class="sxs-lookup"><span data-stu-id="cfd5b-155">Loaded rows do not overlap with existing pages in target</span></span> |<span data-ttu-id="cfd5b-156">**Минимальный**</span><span class="sxs-lookup"><span data-stu-id="cfd5b-156">**Minimal**</span></span> |
| <span data-ttu-id="cfd5b-157">Кластеризованный индекс</span><span class="sxs-lookup"><span data-stu-id="cfd5b-157">Clustered Index</span></span> |<span data-ttu-id="cfd5b-158">Загруженные строки перекрывают существующие страницы в целевом объекте</span><span class="sxs-lookup"><span data-stu-id="cfd5b-158">Loaded rows overlap with existing pages in target</span></span> |<span data-ttu-id="cfd5b-159">Полное</span><span class="sxs-lookup"><span data-stu-id="cfd5b-159">Full</span></span> |
| <span data-ttu-id="cfd5b-160">Кластеризованный индекс columnstore</span><span class="sxs-lookup"><span data-stu-id="cfd5b-160">Clustered Columnstore Index</span></span> |<span data-ttu-id="cfd5b-161">Размер пакета >= 102 400 для распределения с выравниванием по разделам</span><span class="sxs-lookup"><span data-stu-id="cfd5b-161">Batch size >= 102,400 per partition aligned distribution</span></span> |<span data-ttu-id="cfd5b-162">**Минимальный**</span><span class="sxs-lookup"><span data-stu-id="cfd5b-162">**Minimal**</span></span> |
| <span data-ttu-id="cfd5b-163">Кластеризованный индекс columnstore</span><span class="sxs-lookup"><span data-stu-id="cfd5b-163">Clustered Columnstore Index</span></span> |<span data-ttu-id="cfd5b-164">Размер пакета < 102 400 для распределения с выравниванием по разделам</span><span class="sxs-lookup"><span data-stu-id="cfd5b-164">Batch size < 102,400 per partition aligned distribution</span></span> |<span data-ttu-id="cfd5b-165">Полное</span><span class="sxs-lookup"><span data-stu-id="cfd5b-165">Full</span></span> |

<span data-ttu-id="cfd5b-166">Следует отметить, что любые записи, выполняемые для обновления вторичных или некластеризованных индексов, считаются полностью регистрируемыми операциями.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-166">It is worth noting that any writes to update secondary or non-clustered indexes will always be fully logged operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cfd5b-167">В хранилище данных SQL есть 60 распределений.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-167">SQL Data Warehouse has 60 distributions.</span></span> <span data-ttu-id="cfd5b-168">Поэтому, если исходить из того, что все строки распределены равномерно и их целью является один раздел, пакет должен содержать 6 144 000 строк (или больше), чтобы быть минимально регистрируемым, когда запись выполняется в кластеризованный индекс columnstore.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-168">Therefore, assuming all rows are evenly distributed and landing in a single partition, your batch will need to contain 6,144,000 rows or larger to be minimally logged when writing to a Clustered Columnstore Index.</span></span> <span data-ttu-id="cfd5b-169">Если таблица секционирована и вставляемые строки охватывают границы секции, потребуется 6 144 000 строк на границу секции (при условии, что данные распределяются равномерно).</span><span class="sxs-lookup"><span data-stu-id="cfd5b-169">If the table is partitioned and the rows being inserted span partition boundaries, then you will need 6,144,000 rows per partition boundary assuming even data distribution.</span></span> <span data-ttu-id="cfd5b-170">Чтобы вставка данных в распределении была минимально регистрируемой, размер каждого раздела в каждом распределении должен превышать пороговое значение (102 400 строк).</span><span class="sxs-lookup"><span data-stu-id="cfd5b-170">Each partition in each distribution must independently exceed the 102,400 row threshold for the insert to be minimally logged into the distribution.</span></span>
> 
> 

<span data-ttu-id="cfd5b-171">При загрузке данных в непустую таблицу с кластеризованным индексом некоторые строки могут быть полностью регистрируемыми, а некоторые — минимально.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-171">Loading data into a non-empty table with a clustered index can often contain a mixture of fully logged and minimally logged rows.</span></span> <span data-ttu-id="cfd5b-172">Кластеризованный индекс — это сбалансированное дерево страниц.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-172">A clustered index is a balanced tree (b-tree) of pages.</span></span> <span data-ttu-id="cfd5b-173">Если страница, на которой выполняется запись, уже содержит строки другой транзакции, эти операции записи будут полностью регистрируемыми в журнале.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-173">If the page being written to already contains rows from another transaction, then these writes will be fully logged.</span></span> <span data-ttu-id="cfd5b-174">Однако если страница пустая, то операция записи на ней будет минимально регистрируемой.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-174">However, if the page is empty then the write to that page will be minimally logged.</span></span>

## <a name="optimizing-deletes"></a><span data-ttu-id="cfd5b-175">Оптимизация операций удаления</span><span class="sxs-lookup"><span data-stu-id="cfd5b-175">Optimizing deletes</span></span>
<span data-ttu-id="cfd5b-176">`DELETE` является полностью регистрируемой.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-176">`DELETE` is a fully logged operation.</span></span>  <span data-ttu-id="cfd5b-177">Если необходимо удалить большой объем данных в таблице или секции, часто разумнее применить к данным, которые вы хотите оставить, минимально регистрируемую операцию `SELECT` .</span><span class="sxs-lookup"><span data-stu-id="cfd5b-177">If you need to delete a large amount of data in a table or a partition, it often makes more sense to `SELECT` the data you wish to keep, which can be run as a minimally logged operation.</span></span>  <span data-ttu-id="cfd5b-178">Для этого необходимо создать новую таблицу с помощью [CTAS][CTAS].</span><span class="sxs-lookup"><span data-stu-id="cfd5b-178">To accomplish this, create a new table with [CTAS][CTAS].</span></span>  <span data-ttu-id="cfd5b-179">После этого с помощью [RENAME][RENAME] замените старую таблицу только что созданной таблицей.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-179">Once created, use [RENAME][RENAME] to swap out your old table with the newly created table.</span></span>

```sql
-- Delete all sales transactions for Promotions except PromotionKey 2.

--Step 01. Create a new table select only the records we want to kep (PromotionKey 2)
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

--Step 02. Rename the Tables to replace the 
RENAME OBJECT [dbo].[FactInternetSales]   TO [FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_d] TO [FactInternetSales];
```

## <a name="optimizing-updates"></a><span data-ttu-id="cfd5b-180">Оптимизация операций обновления</span><span class="sxs-lookup"><span data-stu-id="cfd5b-180">Optimizing updates</span></span>
<span data-ttu-id="cfd5b-181">`UPDATE` является полностью регистрируемой.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-181">`UPDATE` is a fully logged operation.</span></span>  <span data-ttu-id="cfd5b-182">Если нужно обновить много строк в таблице или секции, для этого, как правило, намного эффективнее использовать минимально регистрируемую операцию, например [CTAS][CTAS].</span><span class="sxs-lookup"><span data-stu-id="cfd5b-182">If you need to update a large number of rows in a table or a partition it can often be far more efficient to use a minimally logged operation such as [CTAS][CTAS] to do so.</span></span>

<span data-ttu-id="cfd5b-183">В примере ниже полное обновление таблицы преобразовано в операцию `CTAS` , что делает возможным минимальное ведение журнала.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-183">In the example below a full table update has been converted to a `CTAS` so that minimal logging is possible.</span></span>

<span data-ttu-id="cfd5b-184">В этом случае мы задним числом добавляем сумму скидки к сумме продаж в таблице.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-184">In this case we are retrospectively adding a discount amount to the sales in the table:</span></span>

```sql
--Step 01. Create a new table containing the "Update". 
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

--Step 02. Rename the tables
RENAME OBJECT [dbo].[FactInternetSales]   TO [FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_u] TO [FactInternetSales];

--Step 03. Drop the old table
DROP TABLE [dbo].[FactInternetSales_old]
```

> [!NOTE]
> <span data-ttu-id="cfd5b-185">Повторное создание больших таблиц может быть удобнее, если использовать функции управления рабочими нагрузками хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-185">Re-creating large tables can benefit from using SQL Data Warehouse workload management features.</span></span> <span data-ttu-id="cfd5b-186">Для получения дополнительных сведений см. раздел, посвященный управлению рабочими нагрузками, в статье о [параллелизме][concurrency].</span><span class="sxs-lookup"><span data-stu-id="cfd5b-186">For more details please refer to the workload management section in the [concurrency][concurrency] article.</span></span>
> 
> 

## <a name="optimizing-with-partition-switching"></a><span data-ttu-id="cfd5b-187">Оптимизация с помощью переключения секций</span><span class="sxs-lookup"><span data-stu-id="cfd5b-187">Optimizing with partition switching</span></span>
<span data-ttu-id="cfd5b-188">Если вы столкнулись с крупномасштабными изменениями в [секции таблицы][table partition], то имеет смысл воспользоваться схемой переключения секций.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-188">When faced with large scale modifications inside a [table partition][table partition], then a partition switching pattern makes a lot of sense.</span></span> <span data-ttu-id="cfd5b-189">Если изменения данных существенные и охватывают несколько секций, то простая итерация по секциям приводит к тому же результату.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-189">If the data modification is significant and spans multiple partitions, then simply iterating over the partitions achieves the same result.</span></span>

<span data-ttu-id="cfd5b-190">Чтобы переключить разделы, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-190">The steps to perform a partition switch are as follows:</span></span>

1. <span data-ttu-id="cfd5b-191">Создайте пустой выходной раздел.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-191">Create an empty out partition</span></span>
2. <span data-ttu-id="cfd5b-192">Выполните обновление в виде операции CTAS.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-192">Perform the 'update' as a CTAS</span></span>
3. <span data-ttu-id="cfd5b-193">Переключите существующие данные на выходную таблицу.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-193">Switch out the existing data to the out table</span></span>
4. <span data-ttu-id="cfd5b-194">Подключите новые данные.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-194">Switch in the new data</span></span>
5. <span data-ttu-id="cfd5b-195">Очистите данные.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-195">Clean up the data</span></span>

<span data-ttu-id="cfd5b-196">Тем не менее нужно уметь определять разделы, которые следует переключить. Для этого нам понадобится вспомогательная процедура наподобие приведенной ниже.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-196">However, to help identify the partitions to switch we will first need to build a helper procedure such as the one below.</span></span> 

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

<span data-ttu-id="cfd5b-197">Эта процедура позволяет максимально повторно использовать код и делает пример переключения секций более компактным.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-197">This procedure maximizes code re-use and keeps the partition switching example more compact.</span></span>

<span data-ttu-id="cfd5b-198">Приведенный ниже код содержит все пять действий, упомянутых выше. В результате получилась полноценная процедура переключения разделов.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-198">The code below demonstrates the five steps mentioned above to achieve a full partition switching routine.</span></span>

```sql
--Create a partitioned aligned empty table to switch out the data 
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

--Create a partitioned aligned table and update the data in the select portion of the CTAS
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

--Use the helper procedure to identify the partitions
--The source table
EXEC dbo.partition_data_get 'dbo','FactInternetSales',20030101
DECLARE @ptn_nmbr_src INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_src

--The "in" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_in',20030101
DECLARE @ptn_nmbr_in INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_in

--The "out" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_out',20030101
DECLARE @ptn_nmbr_out INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_out

--Switch the partitions over
DECLARE @SQL NVARCHAR(4000) = '
ALTER TABLE [dbo].[FactInternetSales]    SWITCH PARTITION '+CAST(@ptn_nmbr_src AS VARCHAR(20))    +' TO [dbo].[FactInternetSales_out] PARTITION '    +CAST(@ptn_nmbr_out AS VARCHAR(20))+';
ALTER TABLE [dbo].[FactInternetSales_in] SWITCH PARTITION '+CAST(@ptn_nmbr_in AS VARCHAR(20))    +' TO [dbo].[FactInternetSales] PARTITION '        +CAST(@ptn_nmbr_src AS VARCHAR(20))+';'
EXEC sp_executesql @SQL

--Perform the clean-up
TRUNCATE TABLE dbo.FactInternetSales_out;
TRUNCATE TABLE dbo.FactInternetSales_in;

DROP TABLE dbo.FactInternetSales_out
DROP TABLE dbo.FactInternetSales_in
DROP TABLE #ptn_data
```

## <a name="minimize-logging-with-small-batches"></a><span data-ttu-id="cfd5b-199">Сведение к минимуму ведения журнала с помощью небольших пакетов</span><span class="sxs-lookup"><span data-stu-id="cfd5b-199">Minimize logging with small batches</span></span>
<span data-ttu-id="cfd5b-200">Операции по изменению больших объемов данных бывает полезно разбить на блоки или пакеты, чтобы охватить единицу работы.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-200">For large data modification operations, it may make sense to divide the operation into chunks or batches to scope the unit of work.</span></span>

<span data-ttu-id="cfd5b-201">Ниже приведен рабочий пример.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-201">A working example is provided below.</span></span> <span data-ttu-id="cfd5b-202">В целях демонстрации указан небольшой размер пакета.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-202">The batch size has been set to a trivial number to highlight the technique.</span></span> <span data-ttu-id="cfd5b-203">В реальной среде он был бы гораздо больше.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-203">In reality the batch size would be significantly larger.</span></span> 

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

## <a name="pause-and-scaling-guidance"></a><span data-ttu-id="cfd5b-204">Рекомендации по приостановке и масштабированию</span><span class="sxs-lookup"><span data-stu-id="cfd5b-204">Pause and scaling guidance</span></span>
<span data-ttu-id="cfd5b-205">Работу хранилища данных SQL Azure можно по запросу приостановить или возобновить. Также его можно масштабировать.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-205">Azure SQL Data Warehouse lets you pause, resume and scale your data warehouse on demand.</span></span> <span data-ttu-id="cfd5b-206">Когда вы приостанавливаете работу хранилища данных SQL или масштабируете его, важно понимать, что запущенные транзакции немедленно прекращаются, что, в свою очередь, откатывает открытые транзакции.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-206">When you pause or scale your SQL Data Warehouse it is important to understand that any in-flight transactions are terminated immediately; causing any open transactions to be rolled back.</span></span> <span data-ttu-id="cfd5b-207">Если в рамках рабочей нагрузки выполнено длительное и незавершенное изменение данных перед операцией приостановки или масштабирования, это изменение нужно отменить.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-207">If your workload had issued a long running and incomplete data modification prior to the pause or scale operation, then this work will need to be undone.</span></span> <span data-ttu-id="cfd5b-208">Это может повлиять на время, требующееся для приостановки или масштабирования базы данных хранилища данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-208">This may impact the time it takes to pause or scale your Azure SQL Data Warehouse database.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="cfd5b-209">`UPDATE` и `DELETE` — это полностью регистрируемые операции, поэтому упомянутые операции отмены и повтора могут выполняться значительно дольше, чем такие же минимально регистрируемые операции.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-209">Both `UPDATE` and `DELETE` are fully logged operations and so these undo/redo operations can take significantly longer than equivalent minimally logged operations.</span></span> 
> 
> 

<span data-ttu-id="cfd5b-210">Лучше всего перед приостановкой работы или масштабированием хранилища данных SQL подождать, пока не завершатся текущие транзакции по изменению данных.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-210">The best scenario is to let in flight data modification transactions complete prior to pausing or scaling SQL Data Warehouse.</span></span> <span data-ttu-id="cfd5b-211">Однако это не всегда удобно.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-211">However, this may not always be practical.</span></span> <span data-ttu-id="cfd5b-212">Чтобы снизить риск длительного отката, выполните одно из следующих действий.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-212">To mitigate the risk of a long rollback, consider one of the following options:</span></span>

* <span data-ttu-id="cfd5b-213">Измените долго выполняющиеся операции, используя [CTAS][CTAS].</span><span class="sxs-lookup"><span data-stu-id="cfd5b-213">Re-write long running operations using [CTAS][CTAS]</span></span>
* <span data-ttu-id="cfd5b-214">Разбейте операцию на блоки для работы с подмножествами строк.</span><span class="sxs-lookup"><span data-stu-id="cfd5b-214">Break the operation down into chunks; operating on a subset of the rows</span></span>

## <a name="next-steps"></a><span data-ttu-id="cfd5b-215">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cfd5b-215">Next steps</span></span>
<span data-ttu-id="cfd5b-216">Сведения об уровнях изоляции и ограничениях транзакций см. в статье [Транзакции в хранилище данных SQL][Transactions in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="cfd5b-216">See [Transactions in SQL Data Warehouse][Transactions in SQL Data Warehouse] to learn more about isolation levels and transactional limits.</span></span>  <span data-ttu-id="cfd5b-217">Рекомендации по использованию хранилища данных SQL Azure см. в статье [Рекомендации по использованию хранилища данных SQL Azure][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="cfd5b-217">For an overview of other Best Practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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

