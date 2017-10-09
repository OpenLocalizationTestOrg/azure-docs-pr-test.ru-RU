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
# <a name="optimizing-transactions-for-sql-data-warehouse"></a><span data-ttu-id="bbd4e-103">Оптимизация транзакций для хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="bbd4e-103">Optimizing transactions for SQL Data Warehouse</span></span>
<span data-ttu-id="bbd4e-104">В этой статье объясняется, как toooptimize hello производительность свести к минимуму риск long откатов транзакций кода.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-104">This article explains how toooptimize hello performance of your transactional code while minimizing risk for long rollbacks.</span></span>

## <a name="transactions-and-logging"></a><span data-ttu-id="bbd4e-105">Транзакции и ведение журнала</span><span class="sxs-lookup"><span data-stu-id="bbd4e-105">Transactions and logging</span></span>
<span data-ttu-id="bbd4e-106">Транзакции представляют собой важную часть ядра реляционной СУБД.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-106">Transactions are an important component of a relational database engine.</span></span> <span data-ttu-id="bbd4e-107">Хранилище данных SQL использует транзакции во время изменения данных.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-107">SQL Data Warehouse uses transactions during data modification.</span></span> <span data-ttu-id="bbd4e-108">Эти транзакции могут быть явными или неявными.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-108">These transactions can be explicit or implicit.</span></span> <span data-ttu-id="bbd4e-109">Одиночные инструкции `INSERT`, `UPDATE` и `DELETE` являются примерами неявных транзакций.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-109">Single `INSERT`, `UPDATE` and `DELETE` statements are all examples of implicit transactions.</span></span> <span data-ttu-id="bbd4e-110">Явные транзакции написанных вручную разработчиком с помощью `BEGIN TRAN`, `COMMIT TRAN` или `ROLLBACK TRAN` и обычно используются, когда несколько инструкций модификации необходимость toobe связаны друг с другом в одну атомарную операцию.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-110">Explicit transactions are written explicitly by a developer using `BEGIN TRAN`, `COMMIT TRAN` or `ROLLBACK TRAN` and are typically used when multiple modification statements need toobe tied together in a single atomic unit.</span></span> 

<span data-ttu-id="bbd4e-111">Хранилище данных SQL Azure фиксирует изменения базы данных toohello с помощью журналов транзакций.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-111">Azure SQL Data Warehouse commits changes toohello database using transaction logs.</span></span> <span data-ttu-id="bbd4e-112">У каждого распределения есть свой журнал транзакций.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-112">Each distribution has its own transaction log.</span></span> <span data-ttu-id="bbd4e-113">Запись в журналы транзакций выполняется автоматически.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-113">Transaction log writes are automatic.</span></span> <span data-ttu-id="bbd4e-114">Настраивать что-либо не требуется.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-114">There is no configuration required.</span></span> <span data-ttu-id="bbd4e-115">Тем не менее хотя этот процесс гарантирует hello записи его в системе hello вводится дополнительная нагрузка.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-115">However, whilst this process guarantees hello write it does introduce an overhead in hello system.</span></span> <span data-ttu-id="bbd4e-116">Чтобы минимизировать этот эффект, нужно написать эффективный код транзакции.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-116">You can minimize this impact by writing transactionally efficient code.</span></span> <span data-ttu-id="bbd4e-117">Такой код можно условно разделить на две категории.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-117">Transactionally efficient code broadly falls into two categories.</span></span>

* <span data-ttu-id="bbd4e-118">Используйте конструкции минимального ведения журналов, когда это возможно.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-118">Leverage minimal logging constructs where possible</span></span>
* <span data-ttu-id="bbd4e-119">Обработка данных с использованием заданной области пакетов единственного числа tooavoid долго выполняющихся транзакций</span><span class="sxs-lookup"><span data-stu-id="bbd4e-119">Process data using scoped batches tooavoid singular long running transactions</span></span>
* <span data-ttu-id="bbd4e-120">Использовать шаблон для заданного раздела tooa больших изменений переключение секции</span><span class="sxs-lookup"><span data-stu-id="bbd4e-120">Adopt a partition switching pattern for large modifications tooa given partition</span></span>

## <a name="minimal-vs-full-logging"></a><span data-ttu-id="bbd4e-121">Минимальное ведение журнала и полное ведение журнала</span><span class="sxs-lookup"><span data-stu-id="bbd4e-121">Minimal vs. full logging</span></span>
<span data-ttu-id="bbd4e-122">В отличие от полной регистрацией в журнале операций, использующих hello журнала транзакций tookeep отслеживать все изменения строк, отслеживать связи операции с минимальным протоколированием размещением экстента и только изменения метаданных.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-122">Unlike fully logged operations, which use hello transaction log tookeep track of every row change, minimally logged operations keep track of extent allocations and meta-data changes only.</span></span> <span data-ttu-id="bbd4e-123">Таким образом, минимальное протоколирование — это протоколирование только информации hello, требуется toorollback hello в транзакции hello события сбоя или явный запрос (`ROLLBACK TRAN`).</span><span class="sxs-lookup"><span data-stu-id="bbd4e-123">Therefore, minimal logging involves logging only hello information that is required toorollback hello transaction in hello event of a failure or an explicit request (`ROLLBACK TRAN`).</span></span> <span data-ttu-id="bbd4e-124">Как гораздо меньше сведения отслеживаются в журнале транзакций hello, операции с минимальной регистрацией выполняет лучше, чем операции работают с полным протоколированием одинакового размера.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-124">As much less information is tracked in hello transaction log, a minimally logged operation performs better than a similarly sized fully logged operation.</span></span> <span data-ttu-id="bbd4e-125">Кроме того так как меньшее количество операций записи журнала транзакций hello, создается много меньший объем данных журнала и поэтому дополнительные операции ввода-вывода эффективен.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-125">Furthermore, because fewer writes go hello transaction log, a much smaller amount of log data is generated and so is more I/O efficient.</span></span>

<span data-ttu-id="bbd4e-126">ограничения безопасности транзакций Hello применяются только toofully в журнал операций.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-126">hello transaction safety limits only apply toofully logged operations.</span></span>

> [!NOTE]
> <span data-ttu-id="bbd4e-127">Минимально регистрируемые операции могут быть частью явных транзакций.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-127">Minimally logged operations can participate in explicit transactions.</span></span> <span data-ttu-id="bbd4e-128">Как отслеживаются все изменения структуры распределения, возможные tooroll назад это как минимум в журнал операций.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-128">As all changes in allocation structures are tracked, it is possible tooroll back minimally logged operations.</span></span> <span data-ttu-id="bbd4e-129">Очень важно toounderstand, изменение hello «как минимум» войти, он не не регистрируется.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-129">It is important toounderstand that hello change is "minimally" logged it is not un-logged.</span></span>
> 
> 

## <a name="minimally-logged-operations"></a><span data-ttu-id="bbd4e-130">Минимально регистрируемые операции</span><span class="sxs-lookup"><span data-stu-id="bbd4e-130">Minimally logged operations</span></span>
<span data-ttu-id="bbd4e-131">Hello следующие операции способны выполняется с минимальным протоколированием:</span><span class="sxs-lookup"><span data-stu-id="bbd4e-131">hello following operations are capable of being minimally logged:</span></span>

* <span data-ttu-id="bbd4e-132">Инструкция CREATE TABLE AS SELECT ([CTAS][CTAS])</span><span class="sxs-lookup"><span data-stu-id="bbd4e-132">CREATE TABLE AS SELECT ([CTAS][CTAS])</span></span>
* <span data-ttu-id="bbd4e-133">INSERT..SELECT</span><span class="sxs-lookup"><span data-stu-id="bbd4e-133">INSERT..SELECT</span></span>
* <span data-ttu-id="bbd4e-134">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="bbd4e-134">CREATE INDEX</span></span>
* <span data-ttu-id="bbd4e-135">ALTER INDEX REBUILD</span><span class="sxs-lookup"><span data-stu-id="bbd4e-135">ALTER INDEX REBUILD</span></span>
* <span data-ttu-id="bbd4e-136">DROP INDEX</span><span class="sxs-lookup"><span data-stu-id="bbd4e-136">DROP INDEX</span></span>
* <span data-ttu-id="bbd4e-137">TRUNCATE TABLE</span><span class="sxs-lookup"><span data-stu-id="bbd4e-137">TRUNCATE TABLE</span></span>
* <span data-ttu-id="bbd4e-138">DROP TABLE</span><span class="sxs-lookup"><span data-stu-id="bbd4e-138">DROP TABLE</span></span>
* <span data-ttu-id="bbd4e-139">ALTER TABLE SWITCH PARTITION</span><span class="sxs-lookup"><span data-stu-id="bbd4e-139">ALTER TABLE SWITCH PARTITION</span></span>

<!--
- MERGE
- UPDATE on LOB Types .WRITE
- SELECT..INTO
-->

> [!NOTE]
> <span data-ttu-id="bbd4e-140">Операции перемещения внутренние данные (такие как `BROADCAST` и `SHUFFLE`) не подвержены лимита безопасности транзакций hello.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-140">Internal data movement operations (such as `BROADCAST` and `SHUFFLE`) are not affected by hello transaction safety limit.</span></span>
> 
> 

## <a name="minimal-logging-with-bulk-load"></a><span data-ttu-id="bbd4e-141">Минимальное ведение журнала и массовая загрузка</span><span class="sxs-lookup"><span data-stu-id="bbd4e-141">Minimal logging with bulk load</span></span>
<span data-ttu-id="bbd4e-142">`CTAS` и `INSERT...SELECT` — это операции массовой загрузки.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-142">`CTAS` and `INSERT...SELECT` are both bulk load operations.</span></span> <span data-ttu-id="bbd4e-143">Тем не менее оба влияют определение таблицы целевой hello и зависят от сценария нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-143">However, both are influenced by hello target table definition and depend on hello load scenario.</span></span> <span data-ttu-id="bbd4e-144">В таблице, приведенной ниже, перечислены условия, в зависимости от которых ваша массовая операция будет регистрироваться полностью или минимально.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-144">Below is a table that explains if your bulk operation will be fully or minimally logged:</span></span>  

| <span data-ttu-id="bbd4e-145">Первичный индекс</span><span class="sxs-lookup"><span data-stu-id="bbd4e-145">Primary Index</span></span> | <span data-ttu-id="bbd4e-146">Сценарий загрузки</span><span class="sxs-lookup"><span data-stu-id="bbd4e-146">Load Scenario</span></span> | <span data-ttu-id="bbd4e-147">Режим ведения журнала</span><span class="sxs-lookup"><span data-stu-id="bbd4e-147">Logging Mode</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bbd4e-148">Куча</span><span class="sxs-lookup"><span data-stu-id="bbd4e-148">Heap</span></span> |<span data-ttu-id="bbd4e-149">Любой</span><span class="sxs-lookup"><span data-stu-id="bbd4e-149">Any</span></span> |<span data-ttu-id="bbd4e-150">**Минимальный**</span><span class="sxs-lookup"><span data-stu-id="bbd4e-150">**Minimal**</span></span> |
| <span data-ttu-id="bbd4e-151">Кластеризованный индекс</span><span class="sxs-lookup"><span data-stu-id="bbd4e-151">Clustered Index</span></span> |<span data-ttu-id="bbd4e-152">Пустая целевая таблица</span><span class="sxs-lookup"><span data-stu-id="bbd4e-152">Empty target table</span></span> |<span data-ttu-id="bbd4e-153">**Минимальный**</span><span class="sxs-lookup"><span data-stu-id="bbd4e-153">**Minimal**</span></span> |
| <span data-ttu-id="bbd4e-154">Кластеризованный индекс</span><span class="sxs-lookup"><span data-stu-id="bbd4e-154">Clustered Index</span></span> |<span data-ttu-id="bbd4e-155">Загруженные строки не перекрывают существующие страницы в целевом объекте</span><span class="sxs-lookup"><span data-stu-id="bbd4e-155">Loaded rows do not overlap with existing pages in target</span></span> |<span data-ttu-id="bbd4e-156">**Минимальный**</span><span class="sxs-lookup"><span data-stu-id="bbd4e-156">**Minimal**</span></span> |
| <span data-ttu-id="bbd4e-157">Кластеризованный индекс</span><span class="sxs-lookup"><span data-stu-id="bbd4e-157">Clustered Index</span></span> |<span data-ttu-id="bbd4e-158">Загруженные строки перекрывают существующие страницы в целевом объекте</span><span class="sxs-lookup"><span data-stu-id="bbd4e-158">Loaded rows overlap with existing pages in target</span></span> |<span data-ttu-id="bbd4e-159">Полное</span><span class="sxs-lookup"><span data-stu-id="bbd4e-159">Full</span></span> |
| <span data-ttu-id="bbd4e-160">Кластеризованный индекс columnstore</span><span class="sxs-lookup"><span data-stu-id="bbd4e-160">Clustered Columnstore Index</span></span> |<span data-ttu-id="bbd4e-161">Размер пакета >= 102 400 для распределения с выравниванием по разделам</span><span class="sxs-lookup"><span data-stu-id="bbd4e-161">Batch size >= 102,400 per partition aligned distribution</span></span> |<span data-ttu-id="bbd4e-162">**Минимальный**</span><span class="sxs-lookup"><span data-stu-id="bbd4e-162">**Minimal**</span></span> |
| <span data-ttu-id="bbd4e-163">Кластеризованный индекс columnstore</span><span class="sxs-lookup"><span data-stu-id="bbd4e-163">Clustered Columnstore Index</span></span> |<span data-ttu-id="bbd4e-164">Размер пакета < 102 400 для распределения с выравниванием по разделам</span><span class="sxs-lookup"><span data-stu-id="bbd4e-164">Batch size < 102,400 per partition aligned distribution</span></span> |<span data-ttu-id="bbd4e-165">Полное</span><span class="sxs-lookup"><span data-stu-id="bbd4e-165">Full</span></span> |

<span data-ttu-id="bbd4e-166">Стоит отметить, что запись tooupdate получателей или некластеризованных индексов будет всегда полностью зарегистрированных операций.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-166">It is worth noting that any writes tooupdate secondary or non-clustered indexes will always be fully logged operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bbd4e-167">В хранилище данных SQL есть 60 распределений.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-167">SQL Data Warehouse has 60 distributions.</span></span> <span data-ttu-id="bbd4e-168">Таким образом при условии, что все строки равномерно распределяются целевой в одной секции, пакет должен toocontain 6,144,000 строк или больше toobe как минимум записанных в журнал при записи tooa кластеризованный индекс Columnstore.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-168">Therefore, assuming all rows are evenly distributed and landing in a single partition, your batch will need toocontain 6,144,000 rows or larger toobe minimally logged when writing tooa Clustered Columnstore Index.</span></span> <span data-ttu-id="bbd4e-169">Если hello таблица секционирована и hello строк, вставляемых span границы секций, потребуется 6,144,000 строк на границу секции, при условии, что равномерное распределение данных.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-169">If hello table is partitioned and hello rows being inserted span partition boundaries, then you will need 6,144,000 rows per partition boundary assuming even data distribution.</span></span> <span data-ttu-id="bbd4e-170">Каждая секция в каждом распространения независимо друг от друга должно превышать hello 102 400 строк пороговое значение с минимальным протоколированием в распространения hello toobe вставки hello.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-170">Each partition in each distribution must independently exceed hello 102,400 row threshold for hello insert toobe minimally logged into hello distribution.</span></span>
> 
> 

<span data-ttu-id="bbd4e-171">При загрузке данных в непустую таблицу с кластеризованным индексом некоторые строки могут быть полностью регистрируемыми, а некоторые — минимально.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-171">Loading data into a non-empty table with a clustered index can often contain a mixture of fully logged and minimally logged rows.</span></span> <span data-ttu-id="bbd4e-172">Кластеризованный индекс — это сбалансированное дерево страниц.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-172">A clustered index is a balanced tree (b-tree) of pages.</span></span> <span data-ttu-id="bbd4e-173">Если страница hello записываемых tooalready содержит строки из другой транзакции, затем эти записи полностью заносятся.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-173">If hello page being written tooalready contains rows from another transaction, then these writes will be fully logged.</span></span> <span data-ttu-id="bbd4e-174">Тем не менее если пустая страница hello затем hello записи toothat страницы будет возможно минимальное протоколирование.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-174">However, if hello page is empty then hello write toothat page will be minimally logged.</span></span>

## <a name="optimizing-deletes"></a><span data-ttu-id="bbd4e-175">Оптимизация операций удаления</span><span class="sxs-lookup"><span data-stu-id="bbd4e-175">Optimizing deletes</span></span>
<span data-ttu-id="bbd4e-176">`DELETE` является полностью регистрируемой.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-176">`DELETE` is a fully logged operation.</span></span>  <span data-ttu-id="bbd4e-177">Если вам требуется toodelete большой объем данных в таблице или секции, часто смысл слишком`SELECT` hello данных нужно tookeep, которая может выполняться как операция с минимальной регистрацией.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-177">If you need toodelete a large amount of data in a table or a partition, it often makes more sense too`SELECT` hello data you wish tookeep, which can be run as a minimally logged operation.</span></span>  <span data-ttu-id="bbd4e-178">tooaccomplish это, создайте новую таблицу с [CTAS][CTAS].</span><span class="sxs-lookup"><span data-stu-id="bbd4e-178">tooaccomplish this, create a new table with [CTAS][CTAS].</span></span>  <span data-ttu-id="bbd4e-179">После создания с помощью [ПЕРЕИМЕНОВАНИЕ] [ RENAME] tooswap out вашей старой таблицы с таблицей вновь созданные hello.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-179">Once created, use [RENAME][RENAME] tooswap out your old table with hello newly created table.</span></span>

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

## <a name="optimizing-updates"></a><span data-ttu-id="bbd4e-180">Оптимизация операций обновления</span><span class="sxs-lookup"><span data-stu-id="bbd4e-180">Optimizing updates</span></span>
<span data-ttu-id="bbd4e-181">`UPDATE` является полностью регистрируемой.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-181">`UPDATE` is a fully logged operation.</span></span>  <span data-ttu-id="bbd4e-182">Если необходимо, чтобы tooupdate большое количество строк в таблице или секции часто может оказаться гораздо более эффективно toouse операция с минимальной регистрацией, например [CTAS] [ CTAS] toodo так.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-182">If you need tooupdate a large number of rows in a table or a partition it can often be far more efficient toouse a minimally logged operation such as [CTAS][CTAS] toodo so.</span></span>

<span data-ttu-id="bbd4e-183">В hello в примере выполняется обновление всей таблицы был преобразованный tooa `CTAS` таким образом, возможно минимальное протоколирование.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-183">In hello example below a full table update has been converted tooa `CTAS` so that minimal logging is possible.</span></span>

<span data-ttu-id="bbd4e-184">В этом случае мы retrospectively добавляем продажи toohello сумма скидки в таблице hello:</span><span class="sxs-lookup"><span data-stu-id="bbd4e-184">In this case we are retrospectively adding a discount amount toohello sales in hello table:</span></span>

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
> <span data-ttu-id="bbd4e-185">Повторное создание больших таблиц может быть удобнее, если использовать функции управления рабочими нагрузками хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-185">Re-creating large tables can benefit from using SQL Data Warehouse workload management features.</span></span> <span data-ttu-id="bbd4e-186">Для сведения см. в раздел управления toohello рабочей нагрузки в hello [параллелизма] [ concurrency] статьи.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-186">For more details please refer toohello workload management section in hello [concurrency][concurrency] article.</span></span>
> 
> 

## <a name="optimizing-with-partition-switching"></a><span data-ttu-id="bbd4e-187">Оптимизация с помощью переключения секций</span><span class="sxs-lookup"><span data-stu-id="bbd4e-187">Optimizing with partition switching</span></span>
<span data-ttu-id="bbd4e-188">Если вы столкнулись с крупномасштабными изменениями в [секции таблицы][table partition], то имеет смысл воспользоваться схемой переключения секций.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-188">When faced with large scale modifications inside a [table partition][table partition], then a partition switching pattern makes a lot of sense.</span></span> <span data-ttu-id="bbd4e-189">Если hello значительные изменения данных и обеспечивает несколько секций, а затем просто перебора hello секций диапазоны hello того же результата.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-189">If hello data modification is significant and spans multiple partitions, then simply iterating over hello partitions achieves hello same result.</span></span>

<span data-ttu-id="bbd4e-190">Ниже приведены действия Hello tooperform переключения секций.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-190">hello steps tooperform a partition switch are as follows:</span></span>

1. <span data-ttu-id="bbd4e-191">Создайте пустой выходной раздел.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-191">Create an empty out partition</span></span>
2. <span data-ttu-id="bbd4e-192">Выполнить обновление «hello» как CTAS</span><span class="sxs-lookup"><span data-stu-id="bbd4e-192">Perform hello 'update' as a CTAS</span></span>
3. <span data-ttu-id="bbd4e-193">Исходящего hello существующих данных toohello таблица исходящего переключения</span><span class="sxs-lookup"><span data-stu-id="bbd4e-193">Switch out hello existing data toohello out table</span></span>
4. <span data-ttu-id="bbd4e-194">Переключитесь в новых данных hello</span><span class="sxs-lookup"><span data-stu-id="bbd4e-194">Switch in hello new data</span></span>
5. <span data-ttu-id="bbd4e-195">Очистка данных hello</span><span class="sxs-lookup"><span data-stu-id="bbd4e-195">Clean up hello data</span></span>

<span data-ttu-id="bbd4e-196">Однако toohelp идентификации tooswitch секций hello, будет необходимо сначала toobuild вспомогательную процедуру, например hello один ниже.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-196">However, toohelp identify hello partitions tooswitch we will first need toobuild a helper procedure such as hello one below.</span></span> 

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

<span data-ttu-id="bbd4e-197">Эта процедура позволяет максимально увеличить повторное использование кода и отслеживает переключения более компактным пример hello секций.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-197">This procedure maximizes code re-use and keeps hello partition switching example more compact.</span></span>

<span data-ttu-id="bbd4e-198">Приведенный ниже код Hello демонстрируется пять шагов hello вышеупомянутых tooachieve полной секции переключение подпрограмму.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-198">hello code below demonstrates hello five steps mentioned above tooachieve a full partition switching routine.</span></span>

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

## <a name="minimize-logging-with-small-batches"></a><span data-ttu-id="bbd4e-199">Сведение к минимуму ведения журнала с помощью небольших пакетов</span><span class="sxs-lookup"><span data-stu-id="bbd4e-199">Minimize logging with small batches</span></span>
<span data-ttu-id="bbd4e-200">Для операций модификации данных большого объема может быть смысле toodivide hello операция в блок hello tooscope блоков или пакетов.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-200">For large data modification operations, it may make sense toodivide hello operation into chunks or batches tooscope hello unit of work.</span></span>

<span data-ttu-id="bbd4e-201">Ниже приведен рабочий пример.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-201">A working example is provided below.</span></span> <span data-ttu-id="bbd4e-202">размер пакета Hello задал tooa тривиальные номеров toohighlight hello прием.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-202">hello batch size has been set tooa trivial number toohighlight hello technique.</span></span> <span data-ttu-id="bbd4e-203">В реальности размер пакета hello бы значительно больше.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-203">In reality hello batch size would be significantly larger.</span></span> 

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

## <a name="pause-and-scaling-guidance"></a><span data-ttu-id="bbd4e-204">Рекомендации по приостановке и масштабированию</span><span class="sxs-lookup"><span data-stu-id="bbd4e-204">Pause and scaling guidance</span></span>
<span data-ttu-id="bbd4e-205">Работу хранилища данных SQL Azure можно по запросу приостановить или возобновить. Также его можно масштабировать.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-205">Azure SQL Data Warehouse lets you pause, resume and scale your data warehouse on demand.</span></span> <span data-ttu-id="bbd4e-206">При приостановке или масштабировать хранилище данных SQL является важным toounderstand, что все транзакции на лету прекращаются немедленно; вызывает любой toobe открытых транзакций выполнен откат.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-206">When you pause or scale your SQL Data Warehouse it is important toounderstand that any in-flight transactions are terminated immediately; causing any open transactions toobe rolled back.</span></span> <span data-ttu-id="bbd4e-207">Если рабочей нагрузки выдан длительные и неполные данные изменения предыдущих toohello приостановить или операции масштабирования, а затем эта работа потребуется toobe отменено.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-207">If your workload had issued a long running and incomplete data modification prior toohello pause or scale operation, then this work will need toobe undone.</span></span> <span data-ttu-id="bbd4e-208">Это может повлиять на время hello toopause или масштабирование базы данных хранилища данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-208">This may impact hello time it takes toopause or scale your Azure SQL Data Warehouse database.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="bbd4e-209">`UPDATE` и `DELETE` — это полностью регистрируемые операции, поэтому упомянутые операции отмены и повтора могут выполняться значительно дольше, чем такие же минимально регистрируемые операции.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-209">Both `UPDATE` and `DELETE` are fully logged operations and so these undo/redo operations can take significantly longer than equivalent minimally logged operations.</span></span> 
> 
> 

<span data-ttu-id="bbd4e-210">Hello наилучшего сценария toolet находится в полете данных изменения транзакций завершения предыдущего toopausing или масштабирования хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-210">hello best scenario is toolet in flight data modification transactions complete prior toopausing or scaling SQL Data Warehouse.</span></span> <span data-ttu-id="bbd4e-211">Однако это не всегда удобно.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-211">However, this may not always be practical.</span></span> <span data-ttu-id="bbd4e-212">риск hello toomitigate long отката, можно воспользоваться hello следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-212">toomitigate hello risk of a long rollback, consider one of hello following options:</span></span>

* <span data-ttu-id="bbd4e-213">Измените долго выполняющиеся операции, используя [CTAS][CTAS].</span><span class="sxs-lookup"><span data-stu-id="bbd4e-213">Re-write long running operations using [CTAS][CTAS]</span></span>
* <span data-ttu-id="bbd4e-214">Операция hello разделяются на блоки. работать с подмножеством строк hello</span><span class="sxs-lookup"><span data-stu-id="bbd4e-214">Break hello operation down into chunks; operating on a subset of hello rows</span></span>

## <a name="next-steps"></a><span data-ttu-id="bbd4e-215">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bbd4e-215">Next steps</span></span>
<span data-ttu-id="bbd4e-216">В разделе [транзакций в хранилище данных SQL] [ Transactions in SQL Data Warehouse] toolearn дополнительные уровни изоляции и лимиты транзакций.</span><span class="sxs-lookup"><span data-stu-id="bbd4e-216">See [Transactions in SQL Data Warehouse][Transactions in SQL Data Warehouse] toolearn more about isolation levels and transactional limits.</span></span>  <span data-ttu-id="bbd4e-217">Рекомендации по использованию хранилища данных SQL Azure см. в статье [Рекомендации по использованию хранилища данных SQL Azure][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="bbd4e-217">For an overview of other Best Practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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

