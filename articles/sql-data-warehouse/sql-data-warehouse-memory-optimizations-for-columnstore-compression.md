---
title: "aaaImprove производительности индекса columnstore в Azure SQL | Документы Microsoft"
description: "Уменьшить требования к памяти или увеличьте hello доступной памяти toomaximize hello количество строк индекса columnstore сжимает в каждой группы строк."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 6/2/2017
ms.author: shigu;barbkess
ms.openlocfilehash: 2c5a68435aa200236a2dc8538aa4638b52a59093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="maximizing-rowgroup-quality-for-columnstore"></a><span data-ttu-id="07cda-103">Максимальное повышение качества группы строк для индекса columnstore</span><span class="sxs-lookup"><span data-stu-id="07cda-103">Maximizing rowgroup quality for columnstore</span></span>

<span data-ttu-id="07cda-104">Качество группы строк определяется hello количество строк в группе строк.</span><span class="sxs-lookup"><span data-stu-id="07cda-104">Rowgroup quality is determined by hello number of rows in a rowgroup.</span></span> <span data-ttu-id="07cda-105">Уменьшить требования к памяти или увеличьте hello доступной памяти toomaximize hello количество строк индекса columnstore сжимает в каждой группы строк.</span><span class="sxs-lookup"><span data-stu-id="07cda-105">Reduce memory requirements or increase hello available memory toomaximize hello number of rows a columnstore index compresses into each rowgroup.</span></span>  <span data-ttu-id="07cda-106">Используйте эти методы tooimprove сжатия и производительности запросов для индексов columnstore.</span><span class="sxs-lookup"><span data-stu-id="07cda-106">Use these methods tooimprove compression rates and query performance for columnstore indexes.</span></span>

## <a name="why-hello-rowgroup-size-matters"></a><span data-ttu-id="07cda-107">Важная роль hello размер группы строк</span><span class="sxs-lookup"><span data-stu-id="07cda-107">Why hello rowgroup size matters</span></span>
<span data-ttu-id="07cda-108">Поскольку индекс columnstore просматривает таблицу путем сканирования сегменты столбцов отдельные группы строк, максимальное увеличение hello количество строк в каждой группе строк повышает производительность запросов.</span><span class="sxs-lookup"><span data-stu-id="07cda-108">Since a columnstore index scans a table by scanning column segments of individual rowgroups, maximizing hello number of rows in each rowgroup enhances query performance.</span></span> <span data-ttu-id="07cda-109">Когда группы строк имеют большое количество строк, сжатие данных повышает, что означает, что имеется меньше tooread данных с диска.</span><span class="sxs-lookup"><span data-stu-id="07cda-109">When rowgroups have a high number of rows, data compression improves which means there is less data tooread from disk.</span></span>

<span data-ttu-id="07cda-110">Дополнительные сведения о группах строк см. в [руководстве по индексам сolumnstore](https://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="07cda-110">For more information about rowgroups, see [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

## <a name="target-size-for-rowgroups"></a><span data-ttu-id="07cda-111">Целевой размер для групп строк</span><span class="sxs-lookup"><span data-stu-id="07cda-111">Target size for rowgroups</span></span>
<span data-ttu-id="07cda-112">Для наилучшей производительности запросов hello целью является toomaximize hello число строк для группы строк в индексе columnstore.</span><span class="sxs-lookup"><span data-stu-id="07cda-112">For best query performance, hello goal is toomaximize hello number of rows per rowgroup in a columnstore index.</span></span> <span data-ttu-id="07cda-113">Группа строк может включать до 1 048 576 строк.</span><span class="sxs-lookup"><span data-stu-id="07cda-113">A rowgroup can have a maximum of 1,048,576 rows.</span></span> <span data-ttu-id="07cda-114">Хорошо toonot имеют hello максимальное число строк для группы строк.</span><span class="sxs-lookup"><span data-stu-id="07cda-114">It's okay toonot have hello maximum number of rows per rowgroup.</span></span> <span data-ttu-id="07cda-115">Индексы columnstore обеспечивают высокую производительность, если группы строк включают хотя бы 100 000 строк.</span><span class="sxs-lookup"><span data-stu-id="07cda-115">Columnstore indexes achieve good performance when rowgroups have at least 100,000 rows.</span></span>

## <a name="rowgroups-can-get-trimmed-during-compression"></a><span data-ttu-id="07cda-116">Группы строк при сжатии можно обрезать</span><span class="sxs-lookup"><span data-stu-id="07cda-116">Rowgroups can get trimmed during compression</span></span>

<span data-ttu-id="07cda-117">Во время массовой загрузки или columnstore перестроения индекса иногда нет доступных toocompress достаточно памяти, всех hello строки, предназначенные для каждой группы строк.</span><span class="sxs-lookup"><span data-stu-id="07cda-117">During a bulk load or columnstore index rebuild, sometimes there isn't enough memory available toocompress all hello rows designated for each rowgroup.</span></span> <span data-ttu-id="07cda-118">При нехватке памяти, индексы columnstore trim hello размер группы строк, поэтому может быть успешным, сжатия в hello columnstore.</span><span class="sxs-lookup"><span data-stu-id="07cda-118">When there is memory pressure, columnstore indexes trim hello rowgroup sizes so compression into hello columnstore can succeed.</span></span> 

<span data-ttu-id="07cda-119">Если недостаточно памяти toocompress по крайней мере 10 000 строк в каждой группы строк, хранилище данных SQL приведет к ошибке.</span><span class="sxs-lookup"><span data-stu-id="07cda-119">When there is insufficient memory toocompress at least 10,000 rows into each rowgroup, SQL Data Warehouse generates an error.</span></span>

<span data-ttu-id="07cda-120">Дополнительные сведения о выполнении массовой загрузки см. в статье [Загрузка данных индексов ColumnStore](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span><span class="sxs-lookup"><span data-stu-id="07cda-120">For more information on bulk loading, see [Bulk load into a clustered columnstore index](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span></span>

## <a name="how-toomonitor-rowgroup-quality"></a><span data-ttu-id="07cda-121">Как качество toomonitor группы строк</span><span class="sxs-lookup"><span data-stu-id="07cda-121">How toomonitor rowgroup quality</span></span>

<span data-ttu-id="07cda-122">Динамическое административное Представление (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats), предоставляет полезные сведения, такие как количество строк в группы строк и hello причина усечения, если был обрезки не существует.</span><span class="sxs-lookup"><span data-stu-id="07cda-122">There is a DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) that exposes useful information such as number of rows in rowgroups and hello reason for trimming if there was trimming.</span></span> <span data-ttu-id="07cda-123">Можно создать эти сведения tooget динамического административного Представления hello следующие представления в виде tooquery удобным способом для усечения группы строк.</span><span class="sxs-lookup"><span data-stu-id="07cda-123">You can create hello following view as a handy way tooquery this DMV tooget information on rowgroup trimming.</span></span>

```sql
create view dbo.vCS_rg_physical_stats
as 
with cte
as
(
select   tb.[name]                    AS [logical_table_name]
,        rg.[row_group_id]            AS [row_group_id]
,        rg.[state]                   AS [state]
,        rg.[state_desc]              AS [state_desc]
,        rg.[total_rows]              AS [total_rows]
,        rg.[trim_reason_desc]        AS trim_reason_desc
,        mp.[physical_name]           AS physical_name
FROM    sys.[schemas] sm
JOIN    sys.[tables] tb               ON  sm.[schema_id]          = tb.[schema_id]                             
JOIN    sys.[pdw_table_mappings] mp   ON  tb.[object_id]          = mp.[object_id]
JOIN    sys.[pdw_nodes_tables] nt     ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[dm_pdw_nodes_db_column_store_row_group_physical_stats] rg      ON  rg.[object_id]     = nt.[object_id]
                                                                            AND rg.[pdw_node_id]   = nt.[pdw_node_id]
                                        AND rg.[distribution_id]    = nt.[distribution_id]                                          
)
select *
from cte;
```

<span data-ttu-id="07cda-124">Hello trim_reason_desc сообщает ли hello группы строк был усечен (trim_reason_desc = NO_TRIM подразумевает без обрезания, и группа строк имеет оптимального качества).</span><span class="sxs-lookup"><span data-stu-id="07cda-124">hello trim_reason_desc tells whether hello rowgroup was trimmed(trim_reason_desc = NO_TRIM implies there was no trimming and row group is of optimal quality).</span></span> <span data-ttu-id="07cda-125">Hello причин trim указывают преждевременное усечения hello группы строк:</span><span class="sxs-lookup"><span data-stu-id="07cda-125">hello following trim reasons indicate premature trimming of hello rowgroup:</span></span>
- <span data-ttu-id="07cda-126">BULKLOAD: В связи с этим trim используется при hello входящего пакета строк для hello нагрузки было меньше, чем 1 миллион строк.</span><span class="sxs-lookup"><span data-stu-id="07cda-126">BULKLOAD: This trim reason is used when hello incoming batch of rows for hello load had less than 1 million rows.</span></span> <span data-ttu-id="07cda-127">Если существует более 100 000 строк, вставляемых (как противоположность tooinserting в hello разностного хранилища), но наборы hello tooBULKLOAD причина усечения Hello engine создаст группы строк в сжатых.</span><span class="sxs-lookup"><span data-stu-id="07cda-127">hello engine will create compressed row groups if there are greater than 100,000 rows being inserted (as opposed tooinserting into hello delta store) but sets hello trim reason tooBULKLOAD.</span></span> <span data-ttu-id="07cda-128">В этом случае можно попробуйте увеличить tooaccumulate окна нагрузки вашего пакета больше строк.</span><span class="sxs-lookup"><span data-stu-id="07cda-128">In this scenario, consider increasing your batch load window tooaccumulate more rows.</span></span> <span data-ttu-id="07cda-129">Кроме того пересчитать вашей секционирования tooensure схему, не слишком детальные группы строк не может охватывать границы секций.</span><span class="sxs-lookup"><span data-stu-id="07cda-129">Also, reevaluate your partitioning scheme tooensure it is not too granular as row groups cannot span partition boundaries.</span></span>
- <span data-ttu-id="07cda-130">MEMORY_LIMITATION: hello engine требуется toocreate групп строк с 1 миллиона строк, определенный объем рабочей памяти.</span><span class="sxs-lookup"><span data-stu-id="07cda-130">MEMORY_LIMITATION: toocreate row groups with 1 million rows, a certain amount of working memory is required by hello engine.</span></span> <span data-ttu-id="07cda-131">Когда hello загрузки сеанса доступной памяти меньше необходимого hello Работа памяти, группы строк получить преждевременно усекаются.</span><span class="sxs-lookup"><span data-stu-id="07cda-131">When available memory of hello loading session is less than hello required working memory, row groups get prematurely trimmed.</span></span> <span data-ttu-id="07cda-132">Привет, в следующих разделах объясняется, как tooestimate памяти необходимо выделить больше памяти.</span><span class="sxs-lookup"><span data-stu-id="07cda-132">hello following sections explain how tooestimate memory required and allocate more memory.</span></span>
- <span data-ttu-id="07cda-133">DICTIONARY_SIZE. Эта причина усечения указывает на то, что усечение групп строк вызвано наличием по крайней мере одного столбца строки с широкими строками и (или) со строками, имеющими большое количество элементов.</span><span class="sxs-lookup"><span data-stu-id="07cda-133">DICTIONARY_SIZE: This trim reason indicates that rowgroup trimming occurred because there was at least one string column with wide and/or high cardinality strings.</span></span> <span data-ttu-id="07cda-134">размер словаря Hello является ограниченной too16, МБ в памяти, и когда этот предел будет достигнут hello группа строк сжимается.</span><span class="sxs-lookup"><span data-stu-id="07cda-134">hello dictionary size is limited too16 MB in memory and once this limit is reached hello row group is compressed.</span></span> <span data-ttu-id="07cda-135">При запуске в этом случае рекомендуется отключить hello проблемный столбца в отдельную таблицу.</span><span class="sxs-lookup"><span data-stu-id="07cda-135">If you do run into this situation, consider isolating hello problematic column into a separate table.</span></span>

## <a name="how-tooestimate-memory-requirements"></a><span data-ttu-id="07cda-136">Как tooestimate требования к памяти</span><span class="sxs-lookup"><span data-stu-id="07cda-136">How tooestimate memory requirements</span></span>

<!--
tooview an estimate of hello memory requirements toocompress a rowgroup of maximum size into a columnstore index, download and run hello view [dbo.vCS_mon_mem_grant](). This view shows hello size of hello memory grant that a rowgroup requires for compression in toohello columnstore.
-->

<span data-ttu-id="07cda-137">Максимальный объем памяти требуется Hello toocompress одну группу строк — приблизительно</span><span class="sxs-lookup"><span data-stu-id="07cda-137">hello maximum required memory toocompress one rowgroup is approximately</span></span>

- <span data-ttu-id="07cda-138">72 МБ +</span><span class="sxs-lookup"><span data-stu-id="07cda-138">72 MB +</span></span>
- <span data-ttu-id="07cda-139">\#строки \* \#столбцы \* 8 байт +</span><span class="sxs-lookup"><span data-stu-id="07cda-139">\#rows \* \#columns \* 8 bytes +</span></span>
- <span data-ttu-id="07cda-140">\#строки \* \#столбцы коротких строк \* 32 байта +</span><span class="sxs-lookup"><span data-stu-id="07cda-140">\#rows \* \#short-string-columns \* 32 bytes +</span></span>
- <span data-ttu-id="07cda-141">\#столбцы длинных строк \* 16 МБ для словаря сжатия</span><span class="sxs-lookup"><span data-stu-id="07cda-141">\#long-string-columns \* 16 MB for compression dictionary</span></span>

<span data-ttu-id="07cda-142">где столбцы коротких строк используют типы строковых данных размером <= 32 байта, а столбцы длинных строк используют типы строковых данных размером > 32 байта.</span><span class="sxs-lookup"><span data-stu-id="07cda-142">where short-string-columns use string data types of <= 32 bytes and long-string-columns use string data types of > 32 bytes.</span></span>

<span data-ttu-id="07cda-143">Используемый метод сжатия длинных строк предназначен для сжатия текста.</span><span class="sxs-lookup"><span data-stu-id="07cda-143">Long strings are compressed with a compression method designed for compressing text.</span></span> <span data-ttu-id="07cda-144">Этот метод сжатия использует *словарь* toostore текстовых шаблонов.</span><span class="sxs-lookup"><span data-stu-id="07cda-144">This compression method uses a *dictionary* toostore text patterns.</span></span> <span data-ttu-id="07cda-145">Максимальный размер словаря Hello составляет 16 МБ.</span><span class="sxs-lookup"><span data-stu-id="07cda-145">hello maximum size of a dictionary is 16 MB.</span></span> <span data-ttu-id="07cda-146">Имеется только один словарь для каждого столбца длинной строки в группе строк hello.</span><span class="sxs-lookup"><span data-stu-id="07cda-146">There is only one dictionary for each long string column in hello rowgroup.</span></span>

<span data-ttu-id="07cda-147">Подробные сведения о требованиях к памяти columnstore см. в [видео-руководстве по настройке масштабирования хранилища данных SQL Azure](https://myignite.microsoft.com/videos/14822).</span><span class="sxs-lookup"><span data-stu-id="07cda-147">For an in-depth discussion of columnstore memory requirements, see the video [Azure SQL Data Warehouse scaling: configuration and guidance](https://myignite.microsoft.com/videos/14822).</span></span>

## <a name="ways-tooreduce-memory-requirements"></a><span data-ttu-id="07cda-148">Требования к памяти tooreduce способами</span><span class="sxs-lookup"><span data-stu-id="07cda-148">Ways tooreduce memory requirements</span></span>

<span data-ttu-id="07cda-149">Используйте следующие методики требования к памяти tooreduce hello сжатия группы строк в индексах columnstore hello.</span><span class="sxs-lookup"><span data-stu-id="07cda-149">Use hello following techniques tooreduce hello memory requirements for compressing rowgroups into columnstore indexes.</span></span>

### <a name="use-fewer-columns"></a><span data-ttu-id="07cda-150">Используйте меньшее число столбцов</span><span class="sxs-lookup"><span data-stu-id="07cda-150">Use fewer columns</span></span>
<span data-ttu-id="07cda-151">Если это возможно Разрабатывайте hello таблицы с меньшим количеством столбцов.</span><span class="sxs-lookup"><span data-stu-id="07cda-151">If possible, design hello table with fewer columns.</span></span> <span data-ttu-id="07cda-152">Когда группа строк сжимается в hello columnstore, индекс columnstore hello сжимает каждый сегмент столбца отдельно.</span><span class="sxs-lookup"><span data-stu-id="07cda-152">When a rowgroup is compressed into hello columnstore, hello columnstore index compresses each column segment separately.</span></span> <span data-ttu-id="07cda-153">Здравствуйте, поэтому требования к памяти toocompress группы строк увеличивается как столбцы увеличения количества hello.</span><span class="sxs-lookup"><span data-stu-id="07cda-153">Therefore hello memory requirements toocompress a rowgroup increase as hello number of columns increases.</span></span>


### <a name="use-fewer-string-columns"></a><span data-ttu-id="07cda-154">Используйте меньшее число строковых столбцов</span><span class="sxs-lookup"><span data-stu-id="07cda-154">Use fewer string columns</span></span>
<span data-ttu-id="07cda-155">Столбцы строковых типов данных требуют больше памяти, чем числовые типы и типы даты.</span><span class="sxs-lookup"><span data-stu-id="07cda-155">Columns of string data types require more memory than numeric and date data types.</span></span> <span data-ttu-id="07cda-156">требования к памяти tooreduce, рассмотрите возможность удаления строковых столбцов из таблицы фактов и разместив их в небольших таблиц измерений.</span><span class="sxs-lookup"><span data-stu-id="07cda-156">tooreduce memory requirements, consider removing string columns from fact tables and putting them in smaller dimension tables.</span></span>

<span data-ttu-id="07cda-157">Дополнительные требования к памяти при сжатии строк:</span><span class="sxs-lookup"><span data-stu-id="07cda-157">Additional memory requirements for string compression:</span></span>

- <span data-ttu-id="07cda-158">Копирование символов too32 строковых данных может потребовать 32 байта дополнительные каждого значения.</span><span class="sxs-lookup"><span data-stu-id="07cda-158">String data types up too32 characters can require 32 additional bytes per value.</span></span>
- <span data-ttu-id="07cda-159">строковые типы данных свыше 32 символов сжимаются с помощью методов словаря,</span><span class="sxs-lookup"><span data-stu-id="07cda-159">String data types with more than 32 characters are compressed using dictionary methods.</span></span>  <span data-ttu-id="07cda-160">Каждый столбец в группе строк hello, может потребоваться копирование tooan дополнительных 16 МБ toobuild hello словарей.</span><span class="sxs-lookup"><span data-stu-id="07cda-160">Each column in hello rowgroup can require up tooan additional 16 MB toobuild hello dictionary.</span></span>

### <a name="avoid-over-partitioning"></a><span data-ttu-id="07cda-161">Избегайте избыточного секционирования</span><span class="sxs-lookup"><span data-stu-id="07cda-161">Avoid over-partitioning</span></span>

<span data-ttu-id="07cda-162">Индексы columnstore создают одну или несколько групп строк в каждой секции.</span><span class="sxs-lookup"><span data-stu-id="07cda-162">Columnstore indexes create one or more rowgroups per partition.</span></span> <span data-ttu-id="07cda-163">В хранилище данных SQL hello количество секций быстро увеличивается из-за распределения данных hello и каждого распределения секционирована.</span><span class="sxs-lookup"><span data-stu-id="07cda-163">In SQL Data Warehouse, hello number of partitions grows quickly because hello data is distributed and each distribution is partitioned.</span></span> <span data-ttu-id="07cda-164">Если таблица hello содержит слишком много секций, могут не существовать rowgroups hello toofill достаточное количество строк.</span><span class="sxs-lookup"><span data-stu-id="07cda-164">If hello table has too many partitions, there might not be enough rows toofill hello rowgroups.</span></span> <span data-ttu-id="07cda-165">отсутствие Hello строк, вызывают нехватку памяти во время сжатия, но приводит toorowgroups, не произойдет hello наилучшую производительность запросов columnstore.</span><span class="sxs-lookup"><span data-stu-id="07cda-165">hello lack of rows does not create memory pressure during compression, but it leads toorowgroups that do not achieve hello best columnstore query performance.</span></span>

<span data-ttu-id="07cda-166">Другой причине tooavoid чрезмерно секционирования является памяти затраты для загрузки строк в индекс columnstore на секционированной таблице.</span><span class="sxs-lookup"><span data-stu-id="07cda-166">Another reason tooavoid over-partitioning is there is a memory overhead for loading rows into a columnstore index on a partitioned table.</span></span> <span data-ttu-id="07cda-167">При загрузке большого числа секций может получать hello входящих строк, которые хранятся в памяти, пока каждая секция имеет достаточно toobe строк сжаты.</span><span class="sxs-lookup"><span data-stu-id="07cda-167">During a load, many partitions could receive hello incoming rows, which are held in memory until each partition has enough rows toobe compressed.</span></span> <span data-ttu-id="07cda-168">Слишком большое число секций приводит к избыточному потреблению памяти.</span><span class="sxs-lookup"><span data-stu-id="07cda-168">Having too many partitions creates additional memory pressure.</span></span>

### <a name="simplify-hello-load-query"></a><span data-ttu-id="07cda-169">Упростите запрос загрузки hello</span><span class="sxs-lookup"><span data-stu-id="07cda-169">Simplify hello load query</span></span>

<span data-ttu-id="07cda-170">Hello базы данных общих папок hello предоставления памяти для запроса среди всех операторов hello в запросе hello.</span><span class="sxs-lookup"><span data-stu-id="07cda-170">hello database shares hello memory grant for a query among all hello operators in hello query.</span></span> <span data-ttu-id="07cda-171">Если загрузить запрос имеет сложную сортировку и соединения, уменьшается hello памяти, доступный для сжатия.</span><span class="sxs-lookup"><span data-stu-id="07cda-171">When a load query has complex sorts and joins, hello memory available for compression is reduced.</span></span>

<span data-ttu-id="07cda-172">Проектирование hello toofocus запросов нагрузки только на загрузке запроса hello.</span><span class="sxs-lookup"><span data-stu-id="07cda-172">Design hello load query toofocus only on loading hello query.</span></span> <span data-ttu-id="07cda-173">Если вам требуется toorun преобразований данных hello, запускайте их отдельно от hello нагрузки запроса.</span><span class="sxs-lookup"><span data-stu-id="07cda-173">If you need toorun transformations on hello data, run them separate from hello load query.</span></span> <span data-ttu-id="07cda-174">Например данные hello этап таблицы кучи, запуска преобразований hello и затем загружать hello промежуточной таблицы в индекс columnstore hello.</span><span class="sxs-lookup"><span data-stu-id="07cda-174">For example, stage hello data in a heap table, run hello transformations, and then load hello staging table into hello columnstore index.</span></span> <span data-ttu-id="07cda-175">Можно также сначала загрузить данные hello и затем использовать hello MPP системы tootransform hello данные.</span><span class="sxs-lookup"><span data-stu-id="07cda-175">You can also load hello data first and then use hello MPP system tootransform hello data.</span></span>

### <a name="adjust-maxdop"></a><span data-ttu-id="07cda-176">Настройка MAXDOP</span><span class="sxs-lookup"><span data-stu-id="07cda-176">Adjust MAXDOP</span></span>

<span data-ttu-id="07cda-177">Каждого распределения сжимает группы строк в columnstore hello в параллельном режиме, при наличии более чем одного ядра ЦП, доступных для распространения.</span><span class="sxs-lookup"><span data-stu-id="07cda-177">Each distribution compresses rowgroups into hello columnstore in parallel when there is more than one CPU core available per distribution.</span></span> <span data-ttu-id="07cda-178">параллелизм Hello требует дополнительных ресурсов памяти, что может привести нехватка toomemory и усечения строк.</span><span class="sxs-lookup"><span data-stu-id="07cda-178">hello parallelism requires additional memory resources, which can lead toomemory pressure and rowgroup trimming.</span></span>

<span data-ttu-id="07cda-179">hello MAXDOP запроса указание tooforce hello нагрузки операции toorun tooreduce нехватки памяти, можно использовать в последовательном режиме внутри каждого распределения.</span><span class="sxs-lookup"><span data-stu-id="07cda-179">tooreduce memory pressure, you can use hello MAXDOP query hint tooforce hello load operation toorun in serial mode within each distribution.</span></span>

```
CREATE TABLE MyFactSalesQuota
WITH (DISTRIBUTION = ROUND_ROBIN)
AS SELECT * FROM FactSalesQUota
OPTION (MAXDOP 1);
```

## <a name="ways-tooallocate-more-memory"></a><span data-ttu-id="07cda-180">Способы tooallocate больший объем памяти</span><span class="sxs-lookup"><span data-stu-id="07cda-180">Ways tooallocate more memory</span></span>

<span data-ttu-id="07cda-181">DWU размер и hello класс пользовательских ресурсов вместе определяют, какой объем памяти доступен для запроса пользователя.</span><span class="sxs-lookup"><span data-stu-id="07cda-181">DWU size and hello user resource class together determine how much memory is available for a user query.</span></span> <span data-ttu-id="07cda-182">tooincrease hello памяти предоставить для загрузки запроса, можно увеличить число hello Dwu или увеличить hello класс ресурсов.</span><span class="sxs-lookup"><span data-stu-id="07cda-182">tooincrease hello memory grant for a load query, you can either increase hello number of DWUs or increase hello resource class.</span></span>

- <span data-ttu-id="07cda-183">. в разделе hello tooincrease Dwu, [как масштабировать производительность?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span><span class="sxs-lookup"><span data-stu-id="07cda-183">tooincrease hello DWUs, see [How do I scale performance?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span></span>
- <span data-ttu-id="07cda-184">Класс ресурсов hello toochange для запроса, в разделе [измените пример класса ресурса для пользователя](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="07cda-184">toochange hello resource class for a query, see [Change a user resource class example](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

<span data-ttu-id="07cda-185">Например на DWU 100 пользователь в классе ресурса smallrc hello может использовать 100 МБ памяти для каждого распределения.</span><span class="sxs-lookup"><span data-stu-id="07cda-185">For example, on DWU 100 a user in hello smallrc resource class can use 100 MB of memory for each distribution.</span></span> <span data-ttu-id="07cda-186">Hello Подробнее [параллелизма в хранилище данных SQL](sql-data-warehouse-develop-concurrency.md).</span><span class="sxs-lookup"><span data-stu-id="07cda-186">For hello details, see [Concurrency in SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).</span></span>

<span data-ttu-id="07cda-187">Предположим, что определить необходимость 700 МБ размер группы строк высокого качества tooget памяти.</span><span class="sxs-lookup"><span data-stu-id="07cda-187">Suppose you determine that you need 700 MB of memory tooget high-quality rowgroup sizes.</span></span> <span data-ttu-id="07cda-188">Эти примеры показывают, как можно выполнить запрос hello нагрузки с достаточным объемом памяти.</span><span class="sxs-lookup"><span data-stu-id="07cda-188">These examples show how you can run hello load query with enough memory.</span></span>

- <span data-ttu-id="07cda-189">При наличии DWU 1000 и mediumrc выделение памяти составит 800 МБ.</span><span class="sxs-lookup"><span data-stu-id="07cda-189">Using DWU 1000 and mediumrc, your memory grant is 800 MB</span></span>
- <span data-ttu-id="07cda-190">При наличии DWU 600 и largerc выделение памяти составит 800 МБ.</span><span class="sxs-lookup"><span data-stu-id="07cda-190">Using DWU 600 and largerc, your memory grant is 800 MB.</span></span>


## <a name="next-steps"></a><span data-ttu-id="07cda-191">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="07cda-191">Next steps</span></span>

<span data-ttu-id="07cda-192">toofind большую производительность tooimprove способами, в хранилище данных SQL, в разделе hello [Обзор производительности](sql-data-warehouse-overview-manage-user-queries.md).</span><span class="sxs-lookup"><span data-stu-id="07cda-192">toofind more ways tooimprove performance in SQL Data Warehouse, see hello [Performance overview](sql-data-warehouse-overview-manage-user-queries.md).</span></span>

<!--Image references-->

<!--Article references-->


<!--MSDN references-->

<!--Other Web references-->
