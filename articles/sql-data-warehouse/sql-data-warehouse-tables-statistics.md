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
# <a name="managing-statistics-on-tables-in-sql-data-warehouse"></a><span data-ttu-id="dc03d-103">Управление статистикой таблиц в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="dc03d-103">Managing statistics on tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="dc03d-104">[Обзор][Overview]</span><span class="sxs-lookup"><span data-stu-id="dc03d-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="dc03d-105">[Типы данных][Data Types]</span><span class="sxs-lookup"><span data-stu-id="dc03d-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="dc03d-106">[Распределение][Distribute]</span><span class="sxs-lookup"><span data-stu-id="dc03d-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="dc03d-107">[Индекс][Index]</span><span class="sxs-lookup"><span data-stu-id="dc03d-107">[Index][Index]</span></span>
> * <span data-ttu-id="dc03d-108">[Секция][Partition]</span><span class="sxs-lookup"><span data-stu-id="dc03d-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="dc03d-109">[Статистика][Statistics]</span><span class="sxs-lookup"><span data-stu-id="dc03d-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="dc03d-110">[Временные таблицы][Temporary]</span><span class="sxs-lookup"><span data-stu-id="dc03d-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="dc03d-111">Hello дополнительные хранилище данных SQL знает о данных, hello быстрее, его можно выполнять запросы к данным.</span><span class="sxs-lookup"><span data-stu-id="dc03d-111">hello more SQL Data Warehouse knows about your data, hello faster it can execute queries against your data.</span></span>  <span data-ttu-id="dc03d-112">Hello осуществляется так, хранилище данных SQL Расскажите о данных, путем сбора статистики о данных.</span><span class="sxs-lookup"><span data-stu-id="dc03d-112">hello way that you tell SQL Data Warehouse about your data, is by collecting statistics about your data.</span></span>  <span data-ttu-id="dc03d-113">Наличие статистики данных является одним hello наиболее важных элементов можно сделать запросы toooptimize.</span><span class="sxs-lookup"><span data-stu-id="dc03d-113">Having statistics on your data is one of hello most important things you can do toooptimize your queries.</span></span>  <span data-ttu-id="dc03d-114">Статистика помогает создать hello наиболее оптимальный план для запросов хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="dc03d-114">Statistics help SQL Data Warehouse create hello most optimal plan for your queries.</span></span>  <span data-ttu-id="dc03d-115">Это происходит потому hello хранилище данных SQL, что оптимизатор имеет место определенная потеря основано на запросе оптимизатора.</span><span class="sxs-lookup"><span data-stu-id="dc03d-115">This is because hello SQL Data Warehouse query optimizer is a cost based optimizer.</span></span>  <span data-ttu-id="dc03d-116">То есть сравнивает hello стоимость разных планов запросов и выбирает план hello с наименьшую стоимость hello, которое также является hello план, который будет выполняться быстрый hello.</span><span class="sxs-lookup"><span data-stu-id="dc03d-116">That is, it compares hello cost of various query plans and then chooses hello plan with hello lowest cost, which should also be hello plan that will execute hello fastest.</span></span>

<span data-ttu-id="dc03d-117">Статистику можно создать по одному или нескольким столбцам, а также на основе индекса таблицы.</span><span class="sxs-lookup"><span data-stu-id="dc03d-117">Statistics can be created on a single column, multiple columns or on an index of a table.</span></span>  <span data-ttu-id="dc03d-118">Статистические данные хранятся в гистограмме, в которой собираются диапазон hello и селективность значений.</span><span class="sxs-lookup"><span data-stu-id="dc03d-118">Statistics are stored in a histogram which captures hello range and selectivity of values.</span></span>  <span data-ttu-id="dc03d-119">Это особый интерес, когда оптимизатор hello должен tooevaluate соединения, GROUP BY, HAVING и WHERE в запросе.</span><span class="sxs-lookup"><span data-stu-id="dc03d-119">This is of particular interest when hello optimizer needs tooevaluate JOINs, GROUP BY, HAVING and WHERE clauses in a query.</span></span>  <span data-ttu-id="dc03d-120">Например, если hello оптимизатор определяет, что возвращает 1 строку hello даты фильтрации в запросе, он может выбрать сильно планировать, чем если он оценивает, что они даты, которые был выбран будет возвращать 1 миллион строк.</span><span class="sxs-lookup"><span data-stu-id="dc03d-120">For example, if hello optimizer estimates that hello date you are filtering in your query will return 1 row, it may choose a very different plan than if it estimates that they date you have selected will return 1 million rows.</span></span>  <span data-ttu-id="dc03d-121">При создании статистики крайне важно, так же важно, что статистика *точно* отражают текущее состояние таблицы hello hello.</span><span class="sxs-lookup"><span data-stu-id="dc03d-121">While creating statistics is extremely important, it is equally important that statistics *accurately* reflect hello current state of hello table.</span></span>  <span data-ttu-id="dc03d-122">Наличие актуальной статистики гарантирует, что хороший план выбранный оптимизатором hello.</span><span class="sxs-lookup"><span data-stu-id="dc03d-122">Having up-to-date statistics ensures that a good plan is selected by hello optimizer.</span></span>  <span data-ttu-id="dc03d-123">Hello планов, созданных оптимизатором hello доступны только в показанной hello статистики на данные.</span><span class="sxs-lookup"><span data-stu-id="dc03d-123">hello plans created by hello optimizer are only as good as hello statistics on your data.</span></span>

<span data-ttu-id="dc03d-124">Hello процесс создания и обновление статистики выполняется в настоящее время вручную, однако является очень простым toodo.</span><span class="sxs-lookup"><span data-stu-id="dc03d-124">hello process of creating and updating statistics is currently a manual process, but is very simple toodo.</span></span>  <span data-ttu-id="dc03d-125">В SQL Server эта процедура выполняется иначе — статистика автоматически создается и обновляется по отдельным столбцам и индексам.</span><span class="sxs-lookup"><span data-stu-id="dc03d-125">This is unlike SQL Server which automatically creates and updates statistics on single columns and indexes.</span></span>  <span data-ttu-id="dc03d-126">Используя приведенные ниже сведения hello, могут значительно автоматизировать управление hello hello статистики на данные.</span><span class="sxs-lookup"><span data-stu-id="dc03d-126">By using hello information below, you can greatly automate hello management of hello statistics on your data.</span></span> 

## <a name="getting-started-with-statistics"></a><span data-ttu-id="dc03d-127">Начало работы со статистикой</span><span class="sxs-lookup"><span data-stu-id="dc03d-127">Getting started with statistics</span></span>
 <span data-ttu-id="dc03d-128">Создание выборочную статистику для каждого столбца tooget легко запускается со статистикой.</span><span class="sxs-lookup"><span data-stu-id="dc03d-128">Creating sampled statistics on every column is an easy way tooget started with statistics.</span></span>  <span data-ttu-id="dc03d-129">Так как это столь же важно tookeep статистики актуальные, высокий уровень безопасности может быть tooupdate статистике ежедневно или после каждого нагрузки.</span><span class="sxs-lookup"><span data-stu-id="dc03d-129">Since it is equally important tookeep statistics up-to-date, a conservative approach may be tooupdate your statistics daily or after each load.</span></span> <span data-ttu-id="dc03d-130">Всегда есть компромиссы между производительностью и стоимость hello toocreate и обновите статистику.</span><span class="sxs-lookup"><span data-stu-id="dc03d-130">There are always trade-offs between performance and hello cost toocreate and update statistics.</span></span>  <span data-ttu-id="dc03d-131">Если обнаружится, что это занимает слишком много времени toomaintain все статистики, может понадобиться tootry toobe более селективным о есть статистика, какие столбцы или столбцы, которые необходимо частое обновление.</span><span class="sxs-lookup"><span data-stu-id="dc03d-131">If you find it is taking too long toomaintain all of your statistics, you may want tootry toobe more selective about which columns have statistics or which columns need frequent updating.</span></span>  <span data-ttu-id="dc03d-132">Например может потребоваться столбцов даты tooupdate ежедневно, как могут быть добавлены новые значения, а не после каждой загрузки.</span><span class="sxs-lookup"><span data-stu-id="dc03d-132">For example, you might want tooupdate date columns daily, as new values may be added rather than after every load.</span></span> <span data-ttu-id="dc03d-133">Опять же, вы приобретете hello максимальную выгоду, что статистика для столбцов, участвующих в соединениях, GROUP BY, HAVING и WHERE.</span><span class="sxs-lookup"><span data-stu-id="dc03d-133">Again, you will gain hello most benefit by having statistics on columns involved in JOINs, GROUP BY, HAVING and WHERE clauses.</span></span>  <span data-ttu-id="dc03d-134">Если у вас есть таблица с большим количеством столбцов, используемых только в hello предложение SELECT, статистику для этих столбцов может затруднить и тратит немного больше усилий tooidentify только столбцы hello, где поможет статистические данные, можно уменьшить время toomaintain hello статистике .</span><span class="sxs-lookup"><span data-stu-id="dc03d-134">If you have a table with a lot of columns which are only used in hello SELECT clause, statistics on these columns may not help, and spending a little more effort tooidentify only hello columns where statistics will help, can reduce hello time toomaintain your statistics.</span></span>

## <a name="multi-column-statistics"></a><span data-ttu-id="dc03d-135">Многостолбцовая статистика</span><span class="sxs-lookup"><span data-stu-id="dc03d-135">Multi-column statistics</span></span>
<span data-ttu-id="dc03d-136">В дополнение к этому toocreating статистику по отдельным столбцам, вы обнаружите что запросы, смогут воспользоваться преимуществами нескольких столбцов статистики.</span><span class="sxs-lookup"><span data-stu-id="dc03d-136">In addition toocreating statistics on single columns, you may find that your queries will benefit from multi-column statistics.</span></span>  <span data-ttu-id="dc03d-137">Многостолбцовая статистика — это статистика, созданная по списку столбцов.</span><span class="sxs-lookup"><span data-stu-id="dc03d-137">Multi-column statistics are statistics created on a list of columns.</span></span>  <span data-ttu-id="dc03d-138">Они включают один столбец статистики в первом столбце hello в списке hello, а также некоторые сведения о корреляции между столбцами вызывается плотности.</span><span class="sxs-lookup"><span data-stu-id="dc03d-138">They include single column statistics on hello first column in hello list, plus some cross-column correlation information called densities.</span></span>  <span data-ttu-id="dc03d-139">Например если имеется таблица, соединяющее tooanother два столбца, возможно, хранилище данных SQL может быть лучше оптимизирован hello план, если он поддерживает hello связь между двумя столбцами.</span><span class="sxs-lookup"><span data-stu-id="dc03d-139">For example, if you have a table that joins tooanother on two columns, you may find that SQL Data Warehouse can better optimize hello plan if it understands hello relationship between two columns.</span></span>   <span data-ttu-id="dc03d-140">Многостолбцовая статистика может повысить производительность запросов для некоторых операций, например составных соединений и группировки.</span><span class="sxs-lookup"><span data-stu-id="dc03d-140">Multi-column statistics can improve query performance for some operations such as composite joins and group by.</span></span>

## <a name="updating-statistics"></a><span data-ttu-id="dc03d-141">Обновление статистики</span><span class="sxs-lookup"><span data-stu-id="dc03d-141">Updating statistics</span></span>
<span data-ttu-id="dc03d-142">Обновление статистики — это важная часть процедуры управления базой данных.</span><span class="sxs-lookup"><span data-stu-id="dc03d-142">Updating statistics is an important part of your database management routine.</span></span>  <span data-ttu-id="dc03d-143">При изменении hello распределение данных в базе данных hello, статистики должны toobe обновлены.</span><span class="sxs-lookup"><span data-stu-id="dc03d-143">When hello distribution of data in hello database changes, statistics need toobe updated.</span></span>  <span data-ttu-id="dc03d-144">Устаревшие статистические данные могут стать причиной toosub оптимальной производительности запросов.</span><span class="sxs-lookup"><span data-stu-id="dc03d-144">Out-of-date statistics will lead toosub-optimal query performance.</span></span>

<span data-ttu-id="dc03d-145">Один рекомендуется tooupdate Статистика по столбцам даты в день по мере добавления новые даты.</span><span class="sxs-lookup"><span data-stu-id="dc03d-145">One best practice is tooupdate statistics on date columns each day as new dates are added.</span></span>  <span data-ttu-id="dc03d-146">Каждый время новые строки будут загружены в хранилище данных hello, новые нагрузки даты или даты операций добавляются.</span><span class="sxs-lookup"><span data-stu-id="dc03d-146">Each time new rows are loaded into hello data warehouse, new load dates or transaction dates are added.</span></span> <span data-ttu-id="dc03d-147">Они изменяют распределение данных hello и сделать устаревшей статистики hello.</span><span class="sxs-lookup"><span data-stu-id="dc03d-147">These change hello data distribution and make hello statistics out-of-date.</span></span> <span data-ttu-id="dc03d-148">И наоборот статистические данные по столбцу страны в таблице customer редко требуется toobe обновлен, обычно не изменяют hello распределение значений.</span><span class="sxs-lookup"><span data-stu-id="dc03d-148">Conversely, statistics on a country column in a customer table might never need toobe updated, as hello distribution of values doesn’t generally change.</span></span> <span data-ttu-id="dc03d-149">Предположим, что hello распространения является константой между клиентами, Добавление нового варианта таблицы toohello строк не будет toochange hello данных распространения.</span><span class="sxs-lookup"><span data-stu-id="dc03d-149">Assuming hello distribution is constant between customers, adding new rows toohello table variation isn't going toochange hello data distribution.</span></span> <span data-ttu-id="dc03d-150">Тем не менее если хранилище данных содержит только одной стране и отобразить данные из новых страны, в результате получаются данные из нескольких стран хранения, определенно необходимо tooupdate статистики для столбца страны hello.</span><span class="sxs-lookup"><span data-stu-id="dc03d-150">However, if your data warehouse only contains one country and you bring in data from a new country, resulting in data from multiple countries being stored, then you definitely need tooupdate statistics on hello country column.</span></span>

<span data-ttu-id="dc03d-151">Одно из hello первый вопросы tooask при диагностике запроса, «актуальны hello статистики?»</span><span class="sxs-lookup"><span data-stu-id="dc03d-151">One of hello first questions tooask when troubleshooting a query is, "Are hello statistics up-to-date?"</span></span>

<span data-ttu-id="dc03d-152">Этот вопрос не может получать ответ hello срок хранения данных hello.</span><span class="sxs-lookup"><span data-stu-id="dc03d-152">This question is not one that can be answered by hello age of hello data.</span></span> <span data-ttu-id="dc03d-153">Объект статистики вверх toodate может быть очень старым, если нет toohello существенные изменения базовым данным.</span><span class="sxs-lookup"><span data-stu-id="dc03d-153">An up toodate statistics object could be very old if there's been no material change toohello underlying data.</span></span> <span data-ttu-id="dc03d-154">Когда существенно измениться hello количество строк или существенных изменений в hello распределение значений для данного столбца *затем* это tooupdate Статистика по времени.</span><span class="sxs-lookup"><span data-stu-id="dc03d-154">When hello number of rows has changed substantially or there is a material change in hello distribution of values for a given column *then* it's time tooupdate statistics.</span></span>  

<span data-ttu-id="dc03d-155">Для справки **SQL Server** (не хранилище данных SQL) автоматически обновляет статистику в следующих случаях:</span><span class="sxs-lookup"><span data-stu-id="dc03d-155">For reference, **SQL Server** (not SQL Data Warehouse) automatically updates statistics for these situations:</span></span>

* <span data-ttu-id="dc03d-156">Если ни одной строки в таблице hello, при добавлении строк, вы получите автоматическое обновление статистики</span><span class="sxs-lookup"><span data-stu-id="dc03d-156">If you have zero rows in hello table, when you add rows, you’ll get an automatic update of statistics</span></span>
* <span data-ttu-id="dc03d-157">При добавлении более 500 tooa таблицы строк, начиная с менее 500 строк (например в начале имеется 499 и затем добавьте 500 строк tooa объем 999 строк), вы сможете получить автоматического обновления</span><span class="sxs-lookup"><span data-stu-id="dc03d-157">When you add more than 500 rows tooa table starting with less than 500 rows (e.g. at start you have 499 and then add 500 rows tooa total of 999 rows), you’ll get an automatic update</span></span> 
* <span data-ttu-id="dc03d-158">После того, как более 500 строк имеется 500 дополнительных строк tooadd + 20% от размера hello hello таблицы перед вы увидите автоматическое обновление на hello stats</span><span class="sxs-lookup"><span data-stu-id="dc03d-158">Once you’re over 500 rows you will have tooadd 500 additional rows + 20% of hello size of hello table before you’ll see an automatic update on hello stats</span></span>

<span data-ttu-id="dc03d-159">Так как не toodetermine динамического административного Представления данных в таблице hello изменился с момента обновления статистики последнего hello, зная возраст hello статистики можно предоставить с часть изображения hello.</span><span class="sxs-lookup"><span data-stu-id="dc03d-159">Since there is no DMV toodetermine if data within hello table has changed since hello last time statistics were updated, knowing hello age of your statistics can provide you with part of hello picture.</span></span>  <span data-ttu-id="dc03d-160">Можно использовать hello в следующем запросе toodetermine hello время последней статистике где обновления для каждой таблицы.</span><span class="sxs-lookup"><span data-stu-id="dc03d-160">You can use hello following query toodetermine hello last time your statistics where updated on each table.</span></span>  

> [!NOTE]
> <span data-ttu-id="dc03d-161">Помните, если есть существенные изменения в hello распределение значений для данного столбца, необходимо обновлять статистику независимо от hello время последнего обновления.</span><span class="sxs-lookup"><span data-stu-id="dc03d-161">Remember if there is a material change in hello distribution of values for a given column, you should update statistics regardless of hello last time they were updated.</span></span>  
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

<span data-ttu-id="dc03d-162">Например, для столбцов дат в хранилище данных обычно требуется часто обновлять статистику.</span><span class="sxs-lookup"><span data-stu-id="dc03d-162">Date columns in a data warehouse, for example, usually need frequent statistics updates.</span></span> <span data-ttu-id="dc03d-163">Каждый время новые строки будут загружены в хранилище данных hello, новые нагрузки даты или даты операций добавляются.</span><span class="sxs-lookup"><span data-stu-id="dc03d-163">Each time new rows are loaded into hello data warehouse, new load dates or transaction dates are added.</span></span> <span data-ttu-id="dc03d-164">Они изменяют распределение данных hello и сделать устаревшей статистики hello.</span><span class="sxs-lookup"><span data-stu-id="dc03d-164">These change hello data distribution and make hello statistics out-of-date.</span></span>  <span data-ttu-id="dc03d-165">И наоборот статистические данные по столбцу "Пол" на таблице заказчика никогда не может потребоваться обновить toobe.</span><span class="sxs-lookup"><span data-stu-id="dc03d-165">Conversely, statistics on a gender column on a customer table might never need toobe updated.</span></span> <span data-ttu-id="dc03d-166">Предположим, что hello распространения является константой между клиентами, Добавление нового варианта таблицы toohello строк не будет toochange hello данных распространения.</span><span class="sxs-lookup"><span data-stu-id="dc03d-166">Assuming hello distribution is constant between customers, adding new rows toohello table variation isn't going toochange hello data distribution.</span></span> <span data-ttu-id="dc03d-167">Тем не менее если хранилище данных содержит только один пол и новые требования результаты в нескольких мужчин и женщин определенно необходимо tooupdate статистику на столбце gender hello.</span><span class="sxs-lookup"><span data-stu-id="dc03d-167">However, if your data warehouse only contains one gender and a new requirement results in multiple genders then you definitely need tooupdate statistics on hello gender column.</span></span>

<span data-ttu-id="dc03d-168">Подробные пояснения см. в статье, посвященной [управлению статистикой][Statistics], на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="dc03d-168">For further explanation, see [Statistics][Statistics] on MSDN.</span></span>

## <a name="implementing-statistics-management"></a><span data-ttu-id="dc03d-169">Реализация управления статистикой</span><span class="sxs-lookup"><span data-stu-id="dc03d-169">Implementing statistics management</span></span>
<span data-ttu-id="dc03d-170">Часто бывает tooextend смысл tooensure процесса, статистические данные обновляются при загрузке данных hello конце hello загрузки.</span><span class="sxs-lookup"><span data-stu-id="dc03d-170">It is often a good idea tooextend your data loading process tooensure that statistics are updated at hello end of hello load.</span></span> <span data-ttu-id="dc03d-171">Загрузка данных Hello при таблицы наиболее часто изменяются, их размера и их распределение значений.</span><span class="sxs-lookup"><span data-stu-id="dc03d-171">hello data load is when tables most frequently change their size and/or their distribution of values.</span></span> <span data-ttu-id="dc03d-172">Следовательно, это tooimplement логично некоторые процессы управления.</span><span class="sxs-lookup"><span data-stu-id="dc03d-172">Therefore, this is a logical place tooimplement some management processes.</span></span>

<span data-ttu-id="dc03d-173">Некоторые основные принципы приведены ниже для обновления статистики во время процесса загрузки hello:</span><span class="sxs-lookup"><span data-stu-id="dc03d-173">Some guiding principles are provided below for updating your statistics during hello load process:</span></span>

* <span data-ttu-id="dc03d-174">Убедитесь, что для каждой загружаемой таблицы обновляется по крайней мере один объект статистики.</span><span class="sxs-lookup"><span data-stu-id="dc03d-174">Ensure that each loaded table has at least one statistics object updated.</span></span> <span data-ttu-id="dc03d-175">Это hello обновления таблицы сведения о размере (количество строк и количество страниц) как часть обновления статистики hello.</span><span class="sxs-lookup"><span data-stu-id="dc03d-175">This updates hello tables size (row count and page count) information as part of hello stats update.</span></span>
* <span data-ttu-id="dc03d-176">Сосредоточьтесь на столбцах, участвующие в предложениях JOIN, GROUP BY, ORDER BY и DISTINCT.</span><span class="sxs-lookup"><span data-stu-id="dc03d-176">Focus on columns participating in JOIN, GROUP BY, ORDER BY and DISTINCT clauses</span></span>
* <span data-ttu-id="dc03d-177">Рекомендуется обновлять столбцы «по возрастанию ключ», например транзакции более часто, как эти значения не будет включен в гистограммы статистики hello дат.</span><span class="sxs-lookup"><span data-stu-id="dc03d-177">Consider updating "ascending key" columns such as transaction dates more frequently as these values will not be included in hello statistics histogram.</span></span>
* <span data-ttu-id="dc03d-178">Рекомендуется реже обновлять столбцы со статическим распределением.</span><span class="sxs-lookup"><span data-stu-id="dc03d-178">Consider updating static distribution columns less frequently.</span></span>
* <span data-ttu-id="dc03d-179">Помните, что каждый объект статистики обновляется последовательно.</span><span class="sxs-lookup"><span data-stu-id="dc03d-179">Remember each statistic object is updated in series.</span></span> <span data-ttu-id="dc03d-180">Просто реализовать `UPDATE STATISTICS <TABLE_NAME>` может быть не идеальным решением, особенно для обширных таблиц с большим количеством объектов статистики.</span><span class="sxs-lookup"><span data-stu-id="dc03d-180">Simply implementing `UPDATE STATISTICS <TABLE_NAME>` may not be ideal - especially for wide tables with lots of statistics objects.</span></span>

> [!NOTE]
> <span data-ttu-id="dc03d-181">Дополнительные сведения о [возрастания ключа] см. SQL Server 2014 toohello Технический оценки количества элементов.</span><span class="sxs-lookup"><span data-stu-id="dc03d-181">For more details on [ascending key] please refer toohello SQL Server 2014 cardinality estimation model whitepaper.</span></span>
> 
> 

<span data-ttu-id="dc03d-182">Подробные пояснения см. в статье [Оценка количества элементов (SQL Server)][Cardinality Estimation] на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="dc03d-182">For further explanation, see  [Cardinality Estimation][Cardinality Estimation] on MSDN.</span></span>

## <a name="examples-create-statistics"></a><span data-ttu-id="dc03d-183">Примеры: создание статистики</span><span class="sxs-lookup"><span data-stu-id="dc03d-183">Examples: Create statistics</span></span>
<span data-ttu-id="dc03d-184">В следующих примерах как toouse различные параметры для создания статистики.</span><span class="sxs-lookup"><span data-stu-id="dc03d-184">These examples show how toouse various options for creating statistics.</span></span> <span data-ttu-id="dc03d-185">Параметры Hello, используемых для каждого столбца зависят от hello характеристик данных и как hello столбец будет использоваться в запросах.</span><span class="sxs-lookup"><span data-stu-id="dc03d-185">hello options that you use for each column depend on hello characteristics of your data and how hello column will be used in queries.</span></span>

### <a name="a-create-single-column-statistics-with-default-options"></a><span data-ttu-id="dc03d-186">О.</span><span class="sxs-lookup"><span data-stu-id="dc03d-186">A.</span></span> <span data-ttu-id="dc03d-187">Создание одностолбцовой статистики с параметрами по умолчанию</span><span class="sxs-lookup"><span data-stu-id="dc03d-187">Create single-column statistics with default options</span></span>
<span data-ttu-id="dc03d-188">toocreate статистики по столбцу, достаточно просто указать имя объекта статистики hello и hello hello столбца.</span><span class="sxs-lookup"><span data-stu-id="dc03d-188">toocreate statistics on a column, simply provide a name for hello statistics object and hello name of hello column.</span></span>

<span data-ttu-id="dc03d-189">Следующий синтаксис использует все параметры по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="dc03d-189">This syntax uses all of hello default options.</span></span> <span data-ttu-id="dc03d-190">По умолчанию хранилище данных SQL выборку 20 процентов hello таблицы при создании статистики.</span><span class="sxs-lookup"><span data-stu-id="dc03d-190">By default, SQL Data Warehouse samples 20 percent of hello table when it creates statistics.</span></span>

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]);
```

<span data-ttu-id="dc03d-191">Например:</span><span class="sxs-lookup"><span data-stu-id="dc03d-191">For example:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1);
```

### <a name="b-create-single-column-statistics-by-examining-every-row"></a><span data-ttu-id="dc03d-192">B.</span><span class="sxs-lookup"><span data-stu-id="dc03d-192">B.</span></span> <span data-ttu-id="dc03d-193">Создание одностолбцовой статистики путем проверки всех строк</span><span class="sxs-lookup"><span data-stu-id="dc03d-193">Create single-column statistics by examining every row</span></span>
<span data-ttu-id="dc03d-194">в большинстве случаев достаточно Hello частота выборки по умолчанию — 20 процентов.</span><span class="sxs-lookup"><span data-stu-id="dc03d-194">hello default sampling rate of 20 percent is sufficient for most situations.</span></span> <span data-ttu-id="dc03d-195">Однако можно изменить частоту выборки hello.</span><span class="sxs-lookup"><span data-stu-id="dc03d-195">However, you can adjust hello sampling rate.</span></span>

<span data-ttu-id="dc03d-196">hello toosample полной таблицы, используйте следующий синтаксис:</span><span class="sxs-lookup"><span data-stu-id="dc03d-196">toosample hello full table, use this syntax:</span></span>

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]) WITH FULLSCAN;
```

<span data-ttu-id="dc03d-197">Например:</span><span class="sxs-lookup"><span data-stu-id="dc03d-197">For example:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH FULLSCAN;
```

### <a name="c-create-single-column-statistics-by-specifying-hello-sample-size"></a><span data-ttu-id="dc03d-198">C.</span><span class="sxs-lookup"><span data-stu-id="dc03d-198">C.</span></span> <span data-ttu-id="dc03d-199">Создать статистику по отдельным столбцам, задав размер образца hello</span><span class="sxs-lookup"><span data-stu-id="dc03d-199">Create single-column statistics by specifying hello sample size</span></span>
<span data-ttu-id="dc03d-200">Кроме того можно указать размер образца hello в процентах:</span><span class="sxs-lookup"><span data-stu-id="dc03d-200">Alternatively, you can specify hello sample size as a percent:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH SAMPLE = 50 PERCENT;
```

### <a name="d-create-single-column-statistics-on-only-some-of-hello-rows"></a><span data-ttu-id="dc03d-201">D.</span><span class="sxs-lookup"><span data-stu-id="dc03d-201">D.</span></span> <span data-ttu-id="dc03d-202">Создание статистики по отдельным столбцам на всех строк hello</span><span class="sxs-lookup"><span data-stu-id="dc03d-202">Create single-column statistics on only some of hello rows</span></span>
<span data-ttu-id="dc03d-203">Другой вариант, можно создать статистику на части hello строк в таблице.</span><span class="sxs-lookup"><span data-stu-id="dc03d-203">Another option, you can create statistics on a portion of hello rows in your table.</span></span> <span data-ttu-id="dc03d-204">Это называется отфильтрованной статистикой.</span><span class="sxs-lookup"><span data-stu-id="dc03d-204">This is called a filtered statistic.</span></span>

<span data-ttu-id="dc03d-205">Например отфильтрованную статистику можно использовать при планировании tooquery определенную секцию большой секционированной таблице.</span><span class="sxs-lookup"><span data-stu-id="dc03d-205">For example, you could use filtered statistics when you plan tooquery a specific partition of a large partitioned table.</span></span> <span data-ttu-id="dc03d-206">Создав статистики hello только значениями параметров секций, hello точность статистики hello будет улучшить и таким образом повысить производительность запросов.</span><span class="sxs-lookup"><span data-stu-id="dc03d-206">By creating statistics on only hello partition values, hello accuracy of hello statistics will improve, and therefore improve query performance.</span></span>

<span data-ttu-id="dc03d-207">Этот пример создает статистику по диапазону значений.</span><span class="sxs-lookup"><span data-stu-id="dc03d-207">This example creates statistics on a range of values.</span></span> <span data-ttu-id="dc03d-208">значения Hello легко может быть определен toomatch hello диапазон значений в секции.</span><span class="sxs-lookup"><span data-stu-id="dc03d-208">hello values could easily be defined toomatch hello range of values in a partition.</span></span>

```sql
CREATE STATISTICS stats_col1 ON table1(col1) WHERE col1 > '2000101' AND col1 < '20001231';
```

> [!NOTE]
> <span data-ttu-id="dc03d-209">Для оптимизатора запросов hello tooconsider с помощью отфильтрованную статистику, при выборе плана hello распределенного запроса запрос hello должен лежать в пределах определения hello объекта статистики hello.</span><span class="sxs-lookup"><span data-stu-id="dc03d-209">For hello query optimizer tooconsider using filtered statistics when it chooses hello distributed query plan, hello query must fit inside hello definition of hello statistics object.</span></span> <span data-ttu-id="dc03d-210">Используя предыдущий пример hello, hello запроса целей значения col1 toospecify между 2000101 и 20001231 предложения.</span><span class="sxs-lookup"><span data-stu-id="dc03d-210">Using hello previous example, hello query's where clause needs toospecify col1 values between 2000101 and 20001231.</span></span>
> 
> 

### <a name="e-create-single-column-statistics-with-all-hello-options"></a><span data-ttu-id="dc03d-211">E.</span><span class="sxs-lookup"><span data-stu-id="dc03d-211">E.</span></span> <span data-ttu-id="dc03d-212">Создание статистики по отдельным столбцам со всеми параметрами hello</span><span class="sxs-lookup"><span data-stu-id="dc03d-212">Create single-column statistics with all hello options</span></span>
<span data-ttu-id="dc03d-213">Можно Конечно, объединять параметры hello вместе.</span><span class="sxs-lookup"><span data-stu-id="dc03d-213">You can, of course, combine hello options together.</span></span> <span data-ttu-id="dc03d-214">пример Hello создает объект отфильтрованной статистики с размером пользовательский образец:</span><span class="sxs-lookup"><span data-stu-id="dc03d-214">hello example below creates a filtered statistics object with a custom sample size:</span></span>

```sql
CREATE STATISTICS stats_col1 ON table1 (col1) WHERE col1 > '2000101' AND col1 < '20001231' WITH SAMPLE = 50 PERCENT;
```

<span data-ttu-id="dc03d-215">Hello полную справочную информацию см. в разделе [CREATE STATISTICS] [ CREATE STATISTICS] в библиотеке MSDN.</span><span class="sxs-lookup"><span data-stu-id="dc03d-215">For hello full reference, see [CREATE STATISTICS][CREATE STATISTICS] on MSDN.</span></span>

### <a name="f-create-multi-column-statistics"></a><span data-ttu-id="dc03d-216">F.</span><span class="sxs-lookup"><span data-stu-id="dc03d-216">F.</span></span> <span data-ttu-id="dc03d-217">Создание многостолбцовой статистики</span><span class="sxs-lookup"><span data-stu-id="dc03d-217">Create multi-column statistics</span></span>
<span data-ttu-id="dc03d-218">toocreate статистики нескольких столбцов, просто используйте hello предыдущих примерах, но указать дополнительные столбцы.</span><span class="sxs-lookup"><span data-stu-id="dc03d-218">toocreate a multi-column statistics, simply use hello previous examples, but specify more columns.</span></span>

> [!NOTE]
> <span data-ttu-id="dc03d-219">Гистограмма Hello, который используется tooestimate количество строк в результатах запроса hello, доступно только для первого столбца hello указаны в определении объекта статистики hello.</span><span class="sxs-lookup"><span data-stu-id="dc03d-219">hello histogram, which is used tooestimate number of rows in hello query result, is only available for hello first column listed in hello statistics object definition.</span></span>
> 
> 

<span data-ttu-id="dc03d-220">В этом примере hello гистограммы находится на *продукта\_категории*.</span><span class="sxs-lookup"><span data-stu-id="dc03d-220">In this example, hello histogram is on *product\_category*.</span></span> <span data-ttu-id="dc03d-221">Статистика между столбцами вычисляется по *product\_category* и *product\_sub_c\ategory*.</span><span class="sxs-lookup"><span data-stu-id="dc03d-221">Cross-column statistics are calculated on *product\_category* and *product\_sub_c\ategory*:</span></span>

```sql
CREATE STATISTICS stats_2cols ON table1 (product_category, product_sub_category) WHERE product_category > '2000101' AND product_category < '20001231' WITH SAMPLE = 50 PERCENT;
```

<span data-ttu-id="dc03d-222">Так как нет корреляцию между *продукта\_категории* и *продукта\_sub\_категории*, stat нескольких столбцов может быть полезно, если эти столбцы доступны в hello то же время.</span><span class="sxs-lookup"><span data-stu-id="dc03d-222">Since there is a correlation between *product\_category* and *product\_sub\_category*, a multi-column stat can be useful if these columns are accessed at hello same time.</span></span>

### <a name="g-create-statistics-on-all-hello-columns-in-a-table"></a><span data-ttu-id="dc03d-223">Ж.</span><span class="sxs-lookup"><span data-stu-id="dc03d-223">G.</span></span> <span data-ttu-id="dc03d-224">Создание статистики для всех столбцов таблицы hello</span><span class="sxs-lookup"><span data-stu-id="dc03d-224">Create statistics on all hello columns in a table</span></span>
<span data-ttu-id="dc03d-225">Одним из способов toocreate статистики — tooissues команды CREATE STATISTICS после создания таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="dc03d-225">One way toocreate statistics is tooissues CREATE STATISTICS commands after creating hello table.</span></span>

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

### <a name="h-use-a-stored-procedure-toocreate-statistics-on-all-columns-in-a-database"></a><span data-ttu-id="dc03d-226">З.</span><span class="sxs-lookup"><span data-stu-id="dc03d-226">H.</span></span> <span data-ttu-id="dc03d-227">Используйте хранимую процедуру toocreate статистики для всех столбцов в базе данных</span><span class="sxs-lookup"><span data-stu-id="dc03d-227">Use a stored procedure toocreate statistics on all columns in a database</span></span>
<span data-ttu-id="dc03d-228">Хранилище данных SQL не имеет эквивалентного хранимая процедура системы слишком [] [sp_create_stats] в SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dc03d-228">SQL Data Warehouse does not have a system stored procedure equivalent too[sp_create_stats][] in SQL Server.</span></span> <span data-ttu-id="dc03d-229">Эта хранимая процедура создает объект статистики один столбец для каждого столбца hello базы данных, в котором еще нет статистики.</span><span class="sxs-lookup"><span data-stu-id="dc03d-229">This stored procedure creates a single column statistics object on every column of hello database that doesn't already have statistics.</span></span>

<span data-ttu-id="dc03d-230">Это поможет приступить к проектированию базы данных.</span><span class="sxs-lookup"><span data-stu-id="dc03d-230">This will help you get started with your database design.</span></span> <span data-ttu-id="dc03d-231">Чувствовать себя свободного tooadapt он должен tooyour.</span><span class="sxs-lookup"><span data-stu-id="dc03d-231">Feel free tooadapt it tooyour needs.</span></span>

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

<span data-ttu-id="dc03d-232">toocreate статистики для всех столбцов в таблице hello в этой процедуре просто вызовите процедуру hello.</span><span class="sxs-lookup"><span data-stu-id="dc03d-232">toocreate statistics on all columns in hello table with this procedure, simply call hello procedure.</span></span>

```sql
prc_sqldw_create_stats;
```

## <a name="examples-update-statistics"></a><span data-ttu-id="dc03d-233">Примеры: обновление статистики</span><span class="sxs-lookup"><span data-stu-id="dc03d-233">Examples: update statistics</span></span>
<span data-ttu-id="dc03d-234">Статистика tooupdate, можно сделать следующее.</span><span class="sxs-lookup"><span data-stu-id="dc03d-234">tooupdate statistics, you can:</span></span>

1. <span data-ttu-id="dc03d-235">Обновить один объект статистики.</span><span class="sxs-lookup"><span data-stu-id="dc03d-235">Update one statistics object.</span></span> <span data-ttu-id="dc03d-236">Укажите имя объекта статистики, которые вы будете tooupdate hello hello.</span><span class="sxs-lookup"><span data-stu-id="dc03d-236">Specify hello name of hello statistics object you wish tooupdate.</span></span>
2. <span data-ttu-id="dc03d-237">Обновить все объекты статистики для таблицы.</span><span class="sxs-lookup"><span data-stu-id="dc03d-237">Update all statistics objects on a table.</span></span> <span data-ttu-id="dc03d-238">Укажите имя hello hello таблицы вместо одного указанного объекта статистики.</span><span class="sxs-lookup"><span data-stu-id="dc03d-238">Specify hello name of hello table instead of one specific statistics object.</span></span>

### <a name="a-update-one-specific-statistics-object"></a><span data-ttu-id="dc03d-239">О.</span><span class="sxs-lookup"><span data-stu-id="dc03d-239">A.</span></span> <span data-ttu-id="dc03d-240">Обновление одного указанного объекта статистики</span><span class="sxs-lookup"><span data-stu-id="dc03d-240">Update one specific statistics object</span></span>
<span data-ttu-id="dc03d-241">Используйте следующий синтаксис tooupdate указанного объекта статистики hello.</span><span class="sxs-lookup"><span data-stu-id="dc03d-241">Use hello following syntax tooupdate a specific statistics object:</span></span>

```sql
UPDATE STATISTICS [schema_name].[table_name]([stat_name]);
```

<span data-ttu-id="dc03d-242">Например:</span><span class="sxs-lookup"><span data-stu-id="dc03d-242">For example:</span></span>

```sql
UPDATE STATISTICS [dbo].[table1] ([stats_col1]);
```

<span data-ttu-id="dc03d-243">Обновляя конкретной статистике объектов, можно свести к минимуму hello статистики toomanage требуется время и ресурсы.</span><span class="sxs-lookup"><span data-stu-id="dc03d-243">By updating specific statistics objects, you can minimize hello time and resources required toomanage statistics.</span></span> <span data-ttu-id="dc03d-244">Требуется некоторые считали, однако объекты tooupdate toochoose hello наиболее статистики.</span><span class="sxs-lookup"><span data-stu-id="dc03d-244">This requires some thought, though, toochoose hello best statistics objects tooupdate.</span></span>

### <a name="b-update-all-statistics-on-a-table"></a><span data-ttu-id="dc03d-245">B.</span><span class="sxs-lookup"><span data-stu-id="dc03d-245">B.</span></span> <span data-ttu-id="dc03d-246">Обновление всей статистики для таблицы</span><span class="sxs-lookup"><span data-stu-id="dc03d-246">Update all statistics on a table</span></span>
<span data-ttu-id="dc03d-247">Это показан простой метод для обновления всех объектов hello статистики для таблицы.</span><span class="sxs-lookup"><span data-stu-id="dc03d-247">This shows a simple method for updating all hello statistics objects on a table.</span></span>

```sql
UPDATE STATISTICS [schema_name].[table_name];
```

<span data-ttu-id="dc03d-248">Например:</span><span class="sxs-lookup"><span data-stu-id="dc03d-248">For example:</span></span>

```sql
UPDATE STATISTICS dbo.table1;
```

<span data-ttu-id="dc03d-249">Эта инструкция является просто toouse.</span><span class="sxs-lookup"><span data-stu-id="dc03d-249">This statement is easy toouse.</span></span> <span data-ttu-id="dc03d-250">Необходимо помните это обновляет всю статистику для таблицы hello и, следовательно, может выполнять больше работы, чем необходимо.</span><span class="sxs-lookup"><span data-stu-id="dc03d-250">Just remember this updates all statistics on hello table, and therefore might perform more work than is necessary.</span></span> <span data-ttu-id="dc03d-251">Если производительность hello не является проблемой, это определенно hello простой и эффективный способ tooguarantee статистические данные актуальны.</span><span class="sxs-lookup"><span data-stu-id="dc03d-251">If hello performance is not an issue, this is definitely hello easiest and most complete way tooguarantee statistics are up-to-date.</span></span>

> [!NOTE]
> <span data-ttu-id="dc03d-252">Если обновление всей статистики для таблицы, хранилище данных SQL не просмотра toosample hello таблицу для каждой статистики.</span><span class="sxs-lookup"><span data-stu-id="dc03d-252">When updating all statistics on a table, SQL Data Warehouse does a scan toosample hello table for each statistics.</span></span> <span data-ttu-id="dc03d-253">Если hello таблица имеет большой размер, имеет много столбцов и статистику, может быть более эффективным tooupdate отдельных статистические данные на основе необходимого.</span><span class="sxs-lookup"><span data-stu-id="dc03d-253">If hello table is large, has many columns, and many statistics, it might be more efficient tooupdate individual statistics based on need.</span></span>
> 
> 

<span data-ttu-id="dc03d-254">Для реализации `UPDATE STATISTICS` процедуры см. в разделе hello [временные таблицы] [ Temporary] статьи.</span><span class="sxs-lookup"><span data-stu-id="dc03d-254">For an implementation of an `UPDATE STATISTICS` procedure please see hello [Temporary Tables][Temporary] article.</span></span> <span data-ttu-id="dc03d-255">метод реализации Hello является немного отличается toohello `CREATE STATISTICS` описанную выше процедуру, кроме hello конечным результатом является таким же hello.</span><span class="sxs-lookup"><span data-stu-id="dc03d-255">hello implementation method is slightly different toohello `CREATE STATISTICS` procedure above but hello end result is hello same.</span></span>

<span data-ttu-id="dc03d-256">Hello полный синтаксис см. в разделе [обновление статистики] [ Update Statistics] в библиотеке MSDN.</span><span class="sxs-lookup"><span data-stu-id="dc03d-256">For hello full syntax, see [Update Statistics][Update Statistics] on MSDN.</span></span>

## <a name="statistics-metadata"></a><span data-ttu-id="dc03d-257">Метаданные статистики</span><span class="sxs-lookup"><span data-stu-id="dc03d-257">Statistics metadata</span></span>
<span data-ttu-id="dc03d-258">Существует несколько функций, которые можно использовать toofind сведения о статистике и Системное представление.</span><span class="sxs-lookup"><span data-stu-id="dc03d-258">There are several system view and functions that you can use toofind information about statistics.</span></span> <span data-ttu-id="dc03d-259">Например можно увидеть, если объект статистики может оказаться устаревшей, используя toosee функции hello stats даты при последней Статистика создана или обновлена.</span><span class="sxs-lookup"><span data-stu-id="dc03d-259">For example, you can see if a statistics object might be out-of-date by using hello stats-date function toosee when statistics were last created or updated.</span></span>

### <a name="catalog-views-for-statistics"></a><span data-ttu-id="dc03d-260">Представления каталога для статистики</span><span class="sxs-lookup"><span data-stu-id="dc03d-260">Catalog views for statistics</span></span>
<span data-ttu-id="dc03d-261">Вот какие системные представления показывают информацию о статистике:</span><span class="sxs-lookup"><span data-stu-id="dc03d-261">These system views provide information about statistics:</span></span>

| <span data-ttu-id="dc03d-262">Представление каталога</span><span class="sxs-lookup"><span data-stu-id="dc03d-262">Catalog View</span></span> | <span data-ttu-id="dc03d-263">Описание</span><span class="sxs-lookup"><span data-stu-id="dc03d-263">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="dc03d-264">[sys.columns][sys.columns]</span><span class="sxs-lookup"><span data-stu-id="dc03d-264">[sys.columns][sys.columns]</span></span> |<span data-ttu-id="dc03d-265">Одна строка для каждого столбца.</span><span class="sxs-lookup"><span data-stu-id="dc03d-265">One row for each column.</span></span> |
| <span data-ttu-id="dc03d-266">[sys.objects][sys.objects]</span><span class="sxs-lookup"><span data-stu-id="dc03d-266">[sys.objects][sys.objects]</span></span> |<span data-ttu-id="dc03d-267">Одну строку для каждого объекта в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="dc03d-267">One row for each object in hello database.</span></span> |
| <span data-ttu-id="dc03d-268">[sys.schemas][sys.schemas]</span><span class="sxs-lookup"><span data-stu-id="dc03d-268">[sys.schemas][sys.schemas]</span></span> |<span data-ttu-id="dc03d-269">Одну строку для каждой схемы в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="dc03d-269">One row for each schema in hello database.</span></span> |
| <span data-ttu-id="dc03d-270">[sys.stats][sys.stats]</span><span class="sxs-lookup"><span data-stu-id="dc03d-270">[sys.stats][sys.stats]</span></span> |<span data-ttu-id="dc03d-271">Одна строка для каждого объекта статистики.</span><span class="sxs-lookup"><span data-stu-id="dc03d-271">One row for each statistics object.</span></span> |
| <span data-ttu-id="dc03d-272">[sys.stats_columns][sys.stats_columns]</span><span class="sxs-lookup"><span data-stu-id="dc03d-272">[sys.stats_columns][sys.stats_columns]</span></span> |<span data-ttu-id="dc03d-273">Одну строку для каждого столбца в объекте статистики hello.</span><span class="sxs-lookup"><span data-stu-id="dc03d-273">One row for each column in hello statistics object.</span></span> <span data-ttu-id="dc03d-274">Ссылающемся toosys.columns.</span><span class="sxs-lookup"><span data-stu-id="dc03d-274">Links back toosys.columns.</span></span> |
| <span data-ttu-id="dc03d-275">[sys.tables][sys.tables]</span><span class="sxs-lookup"><span data-stu-id="dc03d-275">[sys.tables][sys.tables]</span></span> |<span data-ttu-id="dc03d-276">Одна строка для каждой таблицы (включая внешние таблицы).</span><span class="sxs-lookup"><span data-stu-id="dc03d-276">One row for each table (includes external tables).</span></span> |
| <span data-ttu-id="dc03d-277">[sys.table_types][sys.table_types]</span><span class="sxs-lookup"><span data-stu-id="dc03d-277">[sys.table_types][sys.table_types]</span></span> |<span data-ttu-id="dc03d-278">Одна строка для каждого типа данных.</span><span class="sxs-lookup"><span data-stu-id="dc03d-278">One row for each data type.</span></span> |

### <a name="system-functions-for-statistics"></a><span data-ttu-id="dc03d-279">Системные функции для статистики</span><span class="sxs-lookup"><span data-stu-id="dc03d-279">System functions for statistics</span></span>
<span data-ttu-id="dc03d-280">Эти системные функции полезны для работы со статистикой:</span><span class="sxs-lookup"><span data-stu-id="dc03d-280">These system functions are useful for working with statistics:</span></span>

| <span data-ttu-id="dc03d-281">Системная функция</span><span class="sxs-lookup"><span data-stu-id="dc03d-281">System Function</span></span> | <span data-ttu-id="dc03d-282">Описание</span><span class="sxs-lookup"><span data-stu-id="dc03d-282">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="dc03d-283">[STATS_DATE][STATS_DATE]</span><span class="sxs-lookup"><span data-stu-id="dc03d-283">[STATS_DATE][STATS_DATE]</span></span> |<span data-ttu-id="dc03d-284">Объект статистики hello Дата последнего обновления.</span><span class="sxs-lookup"><span data-stu-id="dc03d-284">Date hello statistics object was last updated.</span></span> |
| <span data-ttu-id="dc03d-285">[DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]</span><span class="sxs-lookup"><span data-stu-id="dc03d-285">[DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]</span></span> |<span data-ttu-id="dc03d-286">Предоставляет сводные уровня и подробных сведений о hello распределение значений, подразумевается hello объекта статистики.</span><span class="sxs-lookup"><span data-stu-id="dc03d-286">Provides summary level and detailed information about hello distribution of values as understood by hello statistics object.</span></span> |

### <a name="combine-statistics-columns-and-functions-into-one-view"></a><span data-ttu-id="dc03d-287">Сочетание столбцов и функций статистики в одном представлении</span><span class="sxs-lookup"><span data-stu-id="dc03d-287">Combine statistics columns and functions into one view</span></span>
<span data-ttu-id="dc03d-288">В этом представлении объединяет столбцы, связывающие toostatistics и результаты из функции hello [STATS_DATE()] [] друг с другом.</span><span class="sxs-lookup"><span data-stu-id="dc03d-288">This view brings columns that relate toostatistics, and results from hello [STATS_DATE()][]function together.</span></span>

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

## <a name="dbcc-showstatistics-examples"></a><span data-ttu-id="dc03d-289">Примеры DBCC SHOW_STATISTICS()</span><span class="sxs-lookup"><span data-stu-id="dc03d-289">DBCC SHOW_STATISTICS() examples</span></span>
<span data-ttu-id="dc03d-290">DBCC SHOW_STATISTICS() показывает hello данные, хранящиеся в объекте статистики.</span><span class="sxs-lookup"><span data-stu-id="dc03d-290">DBCC SHOW_STATISTICS() shows hello data held within a statistics object.</span></span> <span data-ttu-id="dc03d-291">Эти данные состоят из трех частей:</span><span class="sxs-lookup"><span data-stu-id="dc03d-291">This data comes in three parts.</span></span>

1. <span data-ttu-id="dc03d-292">Заголовок</span><span class="sxs-lookup"><span data-stu-id="dc03d-292">Header</span></span>
2. <span data-ttu-id="dc03d-293">вектор плотности;</span><span class="sxs-lookup"><span data-stu-id="dc03d-293">Density Vector</span></span>
3. <span data-ttu-id="dc03d-294">Гистограмма</span><span class="sxs-lookup"><span data-stu-id="dc03d-294">Histogram</span></span>

<span data-ttu-id="dc03d-295">Здравствуйте, заголовок метаданных о статистике hello.</span><span class="sxs-lookup"><span data-stu-id="dc03d-295">hello header metadata about hello statistics.</span></span> <span data-ttu-id="dc03d-296">Hello гистограмма отображает hello распределение значений в первом ключевом столбце hello объекта статистики hello.</span><span class="sxs-lookup"><span data-stu-id="dc03d-296">hello histogram displays hello distribution of values in hello first key column of hello statistics object.</span></span> <span data-ttu-id="dc03d-297">вектор плотностей Hello измеряет корреляции между столбцами.</span><span class="sxs-lookup"><span data-stu-id="dc03d-297">hello density vector measures cross-column correlation.</span></span> <span data-ttu-id="dc03d-298">SQLDW вычисляет оценки количества элементов с помощью любого из данных hello в объекте статистики hello.</span><span class="sxs-lookup"><span data-stu-id="dc03d-298">SQLDW computes cardinality estimates with any of hello data in hello statistics object.</span></span>

### <a name="show-header-density-and-histogram"></a><span data-ttu-id="dc03d-299">Отображение заголовка, плотности и гистограммы</span><span class="sxs-lookup"><span data-stu-id="dc03d-299">Show header, density, and histogram</span></span>
<span data-ttu-id="dc03d-300">Это простой пример показывает все три части объекта статистики.</span><span class="sxs-lookup"><span data-stu-id="dc03d-300">This simple example shows all three parts of a statistics object.</span></span>

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>)
```

<span data-ttu-id="dc03d-301">Например:</span><span class="sxs-lookup"><span data-stu-id="dc03d-301">For example:</span></span>

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1);
```

### <a name="show-one-or-more-parts-of-dbcc-showstatistics"></a><span data-ttu-id="dc03d-302">Отображение одной или нескольких частей DBCC SHOW_STATISTICS()</span><span class="sxs-lookup"><span data-stu-id="dc03d-302">Show one or more parts of DBCC SHOW_STATISTICS();</span></span>
<span data-ttu-id="dc03d-303">Если только вы заинтересованы в просмотре определенных компонентов, используйте hello `WITH` предложения и укажите, какие части требуется toosee:</span><span class="sxs-lookup"><span data-stu-id="dc03d-303">If you are only interested in viewing specific parts, use hello `WITH` clause and specify which parts you want toosee:</span></span>

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>) WITH stat_header, histogram, density_vector
```

<span data-ttu-id="dc03d-304">Например:</span><span class="sxs-lookup"><span data-stu-id="dc03d-304">For example:</span></span>

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1) WITH histogram, density_vector
```

## <a name="dbcc-showstatistics-differences"></a><span data-ttu-id="dc03d-305">Отличия DBCC SHOW_STATISTICS()</span><span class="sxs-lookup"><span data-stu-id="dc03d-305">DBCC SHOW_STATISTICS() differences</span></span>
<span data-ttu-id="dc03d-306">DBCC SHOW_STATISTICS() более строго, реализованы в tooSQL сравнивается хранилище данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dc03d-306">DBCC SHOW_STATISTICS() is more strictly implemented in SQL Data Warehouse compared tooSQL Server.</span></span>

1. <span data-ttu-id="dc03d-307">Недокументированные возможности не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="dc03d-307">Undocumented features are not supported</span></span>
2. <span data-ttu-id="dc03d-308">Нельзя использовать Stats_stream.</span><span class="sxs-lookup"><span data-stu-id="dc03d-308">Cannot use Stats_stream</span></span>
3. <span data-ttu-id="dc03d-309">Нельзя соединить результаты для определенных подмножеств данных статистики, например (STAT_HEADER JOIN DENSITY_VECTOR).</span><span class="sxs-lookup"><span data-stu-id="dc03d-309">Cannot join results for specific subsets of statistics data e.g. (STAT_HEADER JOIN DENSITY_VECTOR)</span></span>
4. <span data-ttu-id="dc03d-310">Невозможно задать NO_INFOMSGS для подавления сообщений.</span><span class="sxs-lookup"><span data-stu-id="dc03d-310">NO_INFOMSGS cannot be set for message suppression</span></span>
5. <span data-ttu-id="dc03d-311">Нельзя использовать квадратные скобки вокруг имен статистики.</span><span class="sxs-lookup"><span data-stu-id="dc03d-311">Square brackets around statistics names cannot be used</span></span>
6. <span data-ttu-id="dc03d-312">Невозможно использовать объекты статистики tooidentify имена столбцов</span><span class="sxs-lookup"><span data-stu-id="dc03d-312">Cannot use column names tooidentify statistics objects</span></span>
7. <span data-ttu-id="dc03d-313">Пользовательская ошибка 2767 не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="dc03d-313">Custom error 2767 is not supported</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc03d-314">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dc03d-314">Next steps</span></span>
<span data-ttu-id="dc03d-315">Дополнительные сведения см. в статье [Инструкция DBCC SHOW_STATISTICS (Transact-SQL)][DBCC SHOW_STATISTICS] на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="dc03d-315">For more details, see [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] on MSDN.</span></span>  <span data-ttu-id="dc03d-316">toolearn более, статьях hello на [Общие сведения о таблицах][Overview], [типы данных таблицы][Data Types], [распространение таблицы] [ Distribute], [Индексирования таблицы][Index], [секционировать таблицу] [ Partition] и [ Временные таблицы][Temporary].</span><span class="sxs-lookup"><span data-stu-id="dc03d-316">toolearn more, see hello articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="dc03d-317">Дополнительные рекомендации см. в статье [Рекомендации по использованию хранилища данных SQL Azure][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="dc03d-317">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>  

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
