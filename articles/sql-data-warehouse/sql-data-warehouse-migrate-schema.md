---
title: "Перенос схемы в хранилище данных SQL | Документация Майкрософт"
description: "Советы по переносу схемы в хранилище данных SQL Azure для разработки решений."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 538b60c9-a07f-49bf-9ea3-1082ed6699fb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: 07ca2321852e276502187e768177e7e82bdfd080
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-your-schemas-to-sql-data-warehouse"></a><span data-ttu-id="3bfc5-103">Перенос схем в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="3bfc5-103">Migrate your schemas to SQL Data Warehouse</span></span>
<span data-ttu-id="3bfc5-104">Рекомендации по переносу схем SQL в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="3bfc5-104">Guidance for migrating your SQL schemas to SQL Data Warehouse.</span></span> 

## <a name="plan-your-schema-migration"></a><span data-ttu-id="3bfc5-105">Планирование переноса схемы</span><span class="sxs-lookup"><span data-stu-id="3bfc5-105">Plan your schema migration</span></span>

<span data-ttu-id="3bfc5-106">При планировании переноса прочитайте [обзор таблиц][table overview], чтобы ознакомиться с вопросами проектирования таблиц, такими как статистика, распределение, секционирование и индексирование.</span><span class="sxs-lookup"><span data-stu-id="3bfc5-106">As you plan a migration, see the [table overview][table overview] to become familiar with table design considerations such as statistics, distribution, partitioning, and indexing.</span></span>  <span data-ttu-id="3bfc5-107">В нем также рассматриваются некоторые [неподдерживаемые функции таблиц][unsupported table features] и способы их обойти.</span><span class="sxs-lookup"><span data-stu-id="3bfc5-107">It also lists some [unsupported table features][unsupported table features] and their workarounds.</span></span>

## <a name="use-user-defined-schemas-to-consolidate-databases"></a><span data-ttu-id="3bfc5-108">Применение пользовательских схем для консолидации баз данных</span><span class="sxs-lookup"><span data-stu-id="3bfc5-108">Use user-defined schemas to consolidate databases</span></span>

<span data-ttu-id="3bfc5-109">Ваша текущая рабочая нагрузка, вероятно, использует более одной базы данных.</span><span class="sxs-lookup"><span data-stu-id="3bfc5-109">Your existing workload probably has more than one database.</span></span> <span data-ttu-id="3bfc5-110">Например, хранилище данных SQL Server может включать в себя промежуточную базу данных, базу данных хранилища данных и базы данных киоска данных.</span><span class="sxs-lookup"><span data-stu-id="3bfc5-110">For example, a SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="3bfc5-111">В этой топологии на каждой базе данных выполняется отдельная рабочая нагрузка с собственными политиками безопасности.</span><span class="sxs-lookup"><span data-stu-id="3bfc5-111">In this topology, each database runs as a separate workload with separate security policies.</span></span>

<span data-ttu-id="3bfc5-112">Напротив, хранилище данных SQL выполняет всю рабочую нагрузку хранилища данных в одной базе данных.</span><span class="sxs-lookup"><span data-stu-id="3bfc5-112">By contrast, SQL Data Warehouse runs the entire data warehouse workload within one database.</span></span> <span data-ttu-id="3bfc5-113">Кроссплатформенные соединения баз данных не допускаются.</span><span class="sxs-lookup"><span data-stu-id="3bfc5-113">Cross database joins are not permitted.</span></span> <span data-ttu-id="3bfc5-114">Поэтому хранилище данных SQL ожидает, что все таблицы, используемые в хранилище данных, хранятся в одной базе данных.</span><span class="sxs-lookup"><span data-stu-id="3bfc5-114">Therefore, SQL Data Warehouse expects all tables used by the data warehouse to be stored within the one database.</span></span>

<span data-ttu-id="3bfc5-115">Мы рекомендуем применять пользовательские схемы для консолидации имеющейся рабочей нагрузки в одной базе данных.</span><span class="sxs-lookup"><span data-stu-id="3bfc5-115">We recommend using user-defined schemas to consolidate your existing workload into one database.</span></span> <span data-ttu-id="3bfc5-116">Примеры см. в разделе [Пользовательские схемы](sql-data-warehouse-develop-user-defined-schemas.md).</span><span class="sxs-lookup"><span data-stu-id="3bfc5-116">For examples, see [User-defined schemas](sql-data-warehouse-develop-user-defined-schemas.md)</span></span>

## <a name="use-compatible-data-types"></a><span data-ttu-id="3bfc5-117">Использование совместимых типов данных</span><span class="sxs-lookup"><span data-stu-id="3bfc5-117">Use compatible data types</span></span>
<span data-ttu-id="3bfc5-118">Измените типы данных, чтобы обеспечить совместимость с хранилищем данных SQL.</span><span class="sxs-lookup"><span data-stu-id="3bfc5-118">Modify your data types to be compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="3bfc5-119">Список поддерживаемых и неподдерживаемых типов данных см. в разделе [о типах данных][data types].</span><span class="sxs-lookup"><span data-stu-id="3bfc5-119">For a list of supported and unsupported data types, see [data types][data types].</span></span> <span data-ttu-id="3bfc5-120">В нем представлены обходные пути для неподдерживаемых типов.</span><span class="sxs-lookup"><span data-stu-id="3bfc5-120">That topic gives workarounds for the unsupported types.</span></span> <span data-ttu-id="3bfc5-121">Кроме того, в нем приводится запрос для определения имеющихся типов, которые не поддерживаются в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="3bfc5-121">It also provides a query to identify existing types that are not supported in SQL Data Warehouse.</span></span>

## <a name="minimize-row-size"></a><span data-ttu-id="3bfc5-122">Сведение к минимуму длины строки</span><span class="sxs-lookup"><span data-stu-id="3bfc5-122">Minimize row size</span></span>
<span data-ttu-id="3bfc5-123">Для повышения производительности рекомендуется свести к минимуму длину строк таблицы.</span><span class="sxs-lookup"><span data-stu-id="3bfc5-123">For best performance, minimize the row length of your tables.</span></span> <span data-ttu-id="3bfc5-124">Чем короче строки, тем выше производительность. Поэтому используйте наименьшие типы данных, которые вам подходят.</span><span class="sxs-lookup"><span data-stu-id="3bfc5-124">Since shorter row lengths lead to better performance, use the smallest data types that work for your data.</span></span> 

<span data-ttu-id="3bfc5-125">Для ширины строки таблицы в PolyBase действует ограничение в 1 МБ.</span><span class="sxs-lookup"><span data-stu-id="3bfc5-125">For table row width, PolyBase has a 1 MB limit.</span></span>  <span data-ttu-id="3bfc5-126">Если планируется загружать данные в хранилище данных SQL с помощью PolyBase, обновите таблицы, обеспечив максимальную ширину строки меньше 1 МБ.</span><span class="sxs-lookup"><span data-stu-id="3bfc5-126">If you plan to load data into SQL Data Warehouse with PolyBase, update your tables to have maximum row widths of less than 1 MB.</span></span> 

<!--
- For example, this table uses variable length data but the largest possible size of the row is still less than 1 MB. PolyBase will load data into this table.

- This table uses variable length data and the defined row width is less than one MB. When loading rows, PolyBase allocates the full length of the variable-length data. The full length of this row is greater than one MB.  PolyBase will not load data into this table.  

-->

## <a name="specify-the-distribution-option"></a><span data-ttu-id="3bfc5-127">Указание параметра распределения</span><span class="sxs-lookup"><span data-stu-id="3bfc5-127">Specify the distribution option</span></span>
<span data-ttu-id="3bfc5-128">Хранилище данных SQL — это система управления распределенными базами данных.</span><span class="sxs-lookup"><span data-stu-id="3bfc5-128">SQL Data Warehouse is a distributed database system.</span></span> <span data-ttu-id="3bfc5-129">Каждая таблица распределяется или реплицируется на вычислительные узлы.</span><span class="sxs-lookup"><span data-stu-id="3bfc5-129">Each table is distributed or replicated across the Compute nodes.</span></span> <span data-ttu-id="3bfc5-130">Доступен параметр таблицы, позволяющий указать способ распределения данных.</span><span class="sxs-lookup"><span data-stu-id="3bfc5-130">There's a table option that lets you specify how to distribute the data.</span></span> <span data-ttu-id="3bfc5-131">Можно выбрать циклический перебор, репликацию или хэш-распределение.</span><span class="sxs-lookup"><span data-stu-id="3bfc5-131">The choices are  round-robin, replicated, or hash distributed.</span></span> <span data-ttu-id="3bfc5-132">У каждого варианта есть преимущества и недостатки.</span><span class="sxs-lookup"><span data-stu-id="3bfc5-132">Each has pros and cons.</span></span> <span data-ttu-id="3bfc5-133">Если не указать параметр распределения, по умолчанию хранилищем данных SQL будет использоваться циклический перебор.</span><span class="sxs-lookup"><span data-stu-id="3bfc5-133">If you don't specify the distribution option, SQL Data Warehouse will use round-robin as the default.</span></span>

- <span data-ttu-id="3bfc5-134">Циклический перебор используется по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3bfc5-134">Round-robin is the default.</span></span> <span data-ttu-id="3bfc5-135">Он проще всего в использовании и загружает данные быстрее остальных методов, однако для операций соединения потребуется перемещение данных, что снизит производительность запросов.</span><span class="sxs-lookup"><span data-stu-id="3bfc5-135">It is the simplest to use, and loads the data as fast as possible, but joins will require data movement which slows query performance.</span></span>
- <span data-ttu-id="3bfc5-136">Копия реплицированной таблицы хранится на каждом вычислительном узле.</span><span class="sxs-lookup"><span data-stu-id="3bfc5-136">Replicated stores a copy of the table on each Compute node.</span></span> <span data-ttu-id="3bfc5-137">Реплицированные таблицы являются высокопроизводительных, так как они не требуют перемещения данных для операций соединения и агрегирования.</span><span class="sxs-lookup"><span data-stu-id="3bfc5-137">Replicated tables are performant because they do not require data movement for joins and aggregations.</span></span> <span data-ttu-id="3bfc5-138">Для них требуется дополнительное место в хранилище, поэтому этот тип распределения лучше всего подходит для небольших таблиц.</span><span class="sxs-lookup"><span data-stu-id="3bfc5-138">They do require extra storage, and therefore work best for smaller tables.</span></span>
- <span data-ttu-id="3bfc5-139">При хэш-распределении строки распределяются по всем узлам с помощью хэш-функции.</span><span class="sxs-lookup"><span data-stu-id="3bfc5-139">Hash distributed distributes the rows across all the nodes via a hash function.</span></span> <span data-ttu-id="3bfc5-140">Хэш-распределенные таблицы являются основой хранилища данных SQL, так как они предназначены обеспечить высокую производительность запросов в больших таблицах.</span><span class="sxs-lookup"><span data-stu-id="3bfc5-140">Hash distributed tables are the heart of SQL Data Warehouse since they are designed to provide high query performance on large tables.</span></span> <span data-ttu-id="3bfc5-141">Для данного типа распределения требуется выполнить планирование, чтобы выбрать наиболее подходящий столбец для распределения данных.</span><span class="sxs-lookup"><span data-stu-id="3bfc5-141">This option requires some planning to select the best column on which to distribute the data.</span></span> <span data-ttu-id="3bfc5-142">Тем не менее, если вы не выбрали наиболее подходящий столбец с первого раза, то сможете легко повторно распределить данные по другому столбцу.</span><span class="sxs-lookup"><span data-stu-id="3bfc5-142">However, if you don't choose the best column the first time, you can easily re-distribute the data on a different column.</span></span> 

<span data-ttu-id="3bfc5-143">Чтобы выбрать оптимальный вариант распределения для каждой таблицы, ознакомьтесь с разделом [Распределение таблиц в хранилище данных SQL](sql-data-warehouse-tables-distribute.md).</span><span class="sxs-lookup"><span data-stu-id="3bfc5-143">To choose the best distribution option for each table, see [Distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="3bfc5-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3bfc5-144">Next steps</span></span>
<span data-ttu-id="3bfc5-145">После успешного переноса схемы базы данных в хранилище данных SQL вы можете перейти к одной из приведенных ниже статей.</span><span class="sxs-lookup"><span data-stu-id="3bfc5-145">Once you have successfully migrated your database schema to SQL Data Warehouse, proceed to one of the following articles:</span></span>

* <span data-ttu-id="3bfc5-146">[Перенос данных][Migrate your data]</span><span class="sxs-lookup"><span data-stu-id="3bfc5-146">[Migrate your data][Migrate your data]</span></span>
* <span data-ttu-id="3bfc5-147">[Перенос кода][Migrate your code]</span><span class="sxs-lookup"><span data-stu-id="3bfc5-147">[Migrate your code][Migrate your code]</span></span>

<span data-ttu-id="3bfc5-148">Дополнительные рекомендации по работе с хранилищем данных SQL см. в статье [Рекомендации по использованию хранилища данных SQL Azure][best practices].</span><span class="sxs-lookup"><span data-stu-id="3bfc5-148">For more about SQL Data Warehouse best practices, see the [best practices][best practices] article.</span></span>

<!--Image references-->

<!--Article references-->
[Migrate your code]: ./sql-data-warehouse-migrate-code.md
[Migrate your data]: ./sql-data-warehouse-migrate-data.md
[best practices]: ./sql-data-warehouse-best-practices.md
[table overview]: ./sql-data-warehouse-tables-overview.md
[unsupported table features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[data types]: ./sql-data-warehouse-tables-data-types.md
[unsupported data types]: ./sql-data-warehouse-tables-data-types.md#unsupported-data-types

<!--MSDN references-->


<!--Other Web references-->
