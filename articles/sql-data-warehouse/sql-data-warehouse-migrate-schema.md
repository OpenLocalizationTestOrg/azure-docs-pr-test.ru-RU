---
title: "aaaMigrate tooSQL к схеме хранилища данных | Документы Microsoft"
description: "Советы по переносу tooAzure вашей схемы хранилища данных SQL для разработки решений."
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
ms.openlocfilehash: 1309b743b78564575695038a4856d9d25a2b18d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-schemas-toosql-data-warehouse"></a><span data-ttu-id="8bf74-103">Перенос вашей tooSQL схемы хранилища данных</span><span class="sxs-lookup"><span data-stu-id="8bf74-103">Migrate your schemas tooSQL Data Warehouse</span></span>
<span data-ttu-id="8bf74-104">Рекомендации по переносу вашей tooSQL схем SQL хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="8bf74-104">Guidance for migrating your SQL schemas tooSQL Data Warehouse.</span></span> 

## <a name="plan-your-schema-migration"></a><span data-ttu-id="8bf74-105">Планирование переноса схемы</span><span class="sxs-lookup"><span data-stu-id="8bf74-105">Plan your schema migration</span></span>

<span data-ttu-id="8bf74-106">При планировании миграции в разделе hello [Общие сведения о таблицах] [ table overview] toobecome знакомы таблицы вопросы проектирования, таких как статистика распределения, секционирования и индексирование.</span><span class="sxs-lookup"><span data-stu-id="8bf74-106">As you plan a migration, see hello [table overview][table overview] toobecome familiar with table design considerations such as statistics, distribution, partitioning, and indexing.</span></span>  <span data-ttu-id="8bf74-107">В нем также рассматриваются некоторые [неподдерживаемые функции таблиц][unsupported table features] и способы их обойти.</span><span class="sxs-lookup"><span data-stu-id="8bf74-107">It also lists some [unsupported table features][unsupported table features] and their workarounds.</span></span>

## <a name="use-user-defined-schemas-tooconsolidate-databases"></a><span data-ttu-id="8bf74-108">Использовать базы данных tooconsolidate пользовательских схем</span><span class="sxs-lookup"><span data-stu-id="8bf74-108">Use user-defined schemas tooconsolidate databases</span></span>

<span data-ttu-id="8bf74-109">Ваша текущая рабочая нагрузка, вероятно, использует более одной базы данных.</span><span class="sxs-lookup"><span data-stu-id="8bf74-109">Your existing workload probably has more than one database.</span></span> <span data-ttu-id="8bf74-110">Например, хранилище данных SQL Server может включать в себя промежуточную базу данных, базу данных хранилища данных и базы данных киоска данных.</span><span class="sxs-lookup"><span data-stu-id="8bf74-110">For example, a SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="8bf74-111">В этой топологии на каждой базе данных выполняется отдельная рабочая нагрузка с собственными политиками безопасности.</span><span class="sxs-lookup"><span data-stu-id="8bf74-111">In this topology, each database runs as a separate workload with separate security policies.</span></span>

<span data-ttu-id="8bf74-112">В отличие от этого хранилище данных SQL выполняется hello нагрузку хранилища данных в одной базе данных.</span><span class="sxs-lookup"><span data-stu-id="8bf74-112">By contrast, SQL Data Warehouse runs hello entire data warehouse workload within one database.</span></span> <span data-ttu-id="8bf74-113">Кроссплатформенные соединения баз данных не допускаются.</span><span class="sxs-lookup"><span data-stu-id="8bf74-113">Cross database joins are not permitted.</span></span> <span data-ttu-id="8bf74-114">Таким образом хранилище данных SQL ожидает, что все таблицы, используемые toobe хранилища данных hello, хранятся в одной базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="8bf74-114">Therefore, SQL Data Warehouse expects all tables used by hello data warehouse toobe stored within hello one database.</span></span>

<span data-ttu-id="8bf74-115">Мы рекомендуем использовать пользовательских схем tooconsolidate вашей текущей рабочей нагрузки в одну базу данных.</span><span class="sxs-lookup"><span data-stu-id="8bf74-115">We recommend using user-defined schemas tooconsolidate your existing workload into one database.</span></span> <span data-ttu-id="8bf74-116">Примеры см. в разделе [Пользовательские схемы](sql-data-warehouse-develop-user-defined-schemas.md).</span><span class="sxs-lookup"><span data-stu-id="8bf74-116">For examples, see [User-defined schemas](sql-data-warehouse-develop-user-defined-schemas.md)</span></span>

## <a name="use-compatible-data-types"></a><span data-ttu-id="8bf74-117">Использование совместимых типов данных</span><span class="sxs-lookup"><span data-stu-id="8bf74-117">Use compatible data types</span></span>
<span data-ttu-id="8bf74-118">Измените ваш toobe типы данных, совместимый с хранилищем данных SQL.</span><span class="sxs-lookup"><span data-stu-id="8bf74-118">Modify your data types toobe compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="8bf74-119">Список поддерживаемых и неподдерживаемых типов данных см. в разделе [о типах данных][data types].</span><span class="sxs-lookup"><span data-stu-id="8bf74-119">For a list of supported and unsupported data types, see [data types][data types].</span></span> <span data-ttu-id="8bf74-120">Этот раздел предоставляет обходные пути для типов hello не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="8bf74-120">That topic gives workarounds for hello unsupported types.</span></span> <span data-ttu-id="8bf74-121">Он также предоставляет запрос tooidentify существующие типы, которые не поддерживаются в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="8bf74-121">It also provides a query tooidentify existing types that are not supported in SQL Data Warehouse.</span></span>

## <a name="minimize-row-size"></a><span data-ttu-id="8bf74-122">Сведение к минимуму длины строки</span><span class="sxs-lookup"><span data-stu-id="8bf74-122">Minimize row size</span></span>
<span data-ttu-id="8bf74-123">Для повышения производительности рекомендуется свести к минимуму hello длина строки таблицы.</span><span class="sxs-lookup"><span data-stu-id="8bf74-123">For best performance, minimize hello row length of your tables.</span></span> <span data-ttu-id="8bf74-124">Так как более короткие длины строк привести toobetter производительности, используете типы данных наименьшее hello, которые работают для данных.</span><span class="sxs-lookup"><span data-stu-id="8bf74-124">Since shorter row lengths lead toobetter performance, use hello smallest data types that work for your data.</span></span> 

<span data-ttu-id="8bf74-125">Для ширины строки таблицы в PolyBase действует ограничение в 1 МБ.</span><span class="sxs-lookup"><span data-stu-id="8bf74-125">For table row width, PolyBase has a 1 MB limit.</span></span>  <span data-ttu-id="8bf74-126">Если планируется tooload данных в хранилище данных SQL с помощью PolyBase, обновите ширина максимальной строка таблицы toohave меньше 1 МБ.</span><span class="sxs-lookup"><span data-stu-id="8bf74-126">If you plan tooload data into SQL Data Warehouse with PolyBase, update your tables toohave maximum row widths of less than 1 MB.</span></span> 

<!--
- For example, this table uses variable length data but hello largest possible size of hello row is still less than 1 MB. PolyBase will load data into this table.

- This table uses variable length data and hello defined row width is less than one MB. When loading rows, PolyBase allocates hello full length of hello variable-length data. hello full length of this row is greater than one MB.  PolyBase will not load data into this table.  

-->

## <a name="specify-hello-distribution-option"></a><span data-ttu-id="8bf74-127">Укажите параметр распространения hello</span><span class="sxs-lookup"><span data-stu-id="8bf74-127">Specify hello distribution option</span></span>
<span data-ttu-id="8bf74-128">Хранилище данных SQL — это система управления распределенными базами данных.</span><span class="sxs-lookup"><span data-stu-id="8bf74-128">SQL Data Warehouse is a distributed database system.</span></span> <span data-ttu-id="8bf74-129">Каждая таблица распределения или реплицировать по hello вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="8bf74-129">Each table is distributed or replicated across hello Compute nodes.</span></span> <span data-ttu-id="8bf74-130">Отсутствует параметр, позволяющий указать, каким образом toodistribute hello данных.</span><span class="sxs-lookup"><span data-stu-id="8bf74-130">There's a table option that lets you specify how toodistribute hello data.</span></span> <span data-ttu-id="8bf74-131">варианты Hello реплицируются циклический перебор, или распределенные хэш.</span><span class="sxs-lookup"><span data-stu-id="8bf74-131">hello choices are  round-robin, replicated, or hash distributed.</span></span> <span data-ttu-id="8bf74-132">У каждого варианта есть преимущества и недостатки.</span><span class="sxs-lookup"><span data-stu-id="8bf74-132">Each has pros and cons.</span></span> <span data-ttu-id="8bf74-133">Если не указать параметр распространения hello, хранилище данных SQL будет использовать циклический перебор по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="8bf74-133">If you don't specify hello distribution option, SQL Data Warehouse will use round-robin as hello default.</span></span>

- <span data-ttu-id="8bf74-134">Циклический перебор — по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="8bf74-134">Round-robin is hello default.</span></span> <span data-ttu-id="8bf74-135">Это простейший toouse hello и загружает данные hello максимально возможной скоростью, но соединения потребуется перемещение данных, что снижает производительность запросов.</span><span class="sxs-lookup"><span data-stu-id="8bf74-135">It is hello simplest toouse, and loads hello data as fast as possible, but joins will require data movement which slows query performance.</span></span>
- <span data-ttu-id="8bf74-136">Хранит реплицированные копии таблицы hello на каждом вычислительном узле.</span><span class="sxs-lookup"><span data-stu-id="8bf74-136">Replicated stores a copy of hello table on each Compute node.</span></span> <span data-ttu-id="8bf74-137">Реплицированные таблицы являются высокопроизводительных, так как они не требуют перемещения данных для операций соединения и агрегирования.</span><span class="sxs-lookup"><span data-stu-id="8bf74-137">Replicated tables are performant because they do not require data movement for joins and aggregations.</span></span> <span data-ttu-id="8bf74-138">Для них требуется дополнительное место в хранилище, поэтому этот тип распределения лучше всего подходит для небольших таблиц.</span><span class="sxs-lookup"><span data-stu-id="8bf74-138">They do require extra storage, and therefore work best for smaller tables.</span></span>
- <span data-ttu-id="8bf74-139">Хэш распределенных распределяет hello строк по всем узлам hello через хэш-функции.</span><span class="sxs-lookup"><span data-stu-id="8bf74-139">Hash distributed distributes hello rows across all hello nodes via a hash function.</span></span> <span data-ttu-id="8bf74-140">Распределенных хэш-таблицы являются основой hello хранилище данных SQL, поскольку они являются спроектированный tooprovide высокую производительность запросов в больших таблицах.</span><span class="sxs-lookup"><span data-stu-id="8bf74-140">Hash distributed tables are hello heart of SQL Data Warehouse since they are designed tooprovide high query performance on large tables.</span></span> <span data-ttu-id="8bf74-141">Этот параметр требует некоторых планирования tooselect hello столбец лучше всего на какие данные toodistribute hello.</span><span class="sxs-lookup"><span data-stu-id="8bf74-141">This option requires some planning tooselect hello best column on which toodistribute hello data.</span></span> <span data-ttu-id="8bf74-142">Тем не менее если не выбрать лучший столбца hello hello первый раз, можно легко повторно распространять hello данные на другой столбец.</span><span class="sxs-lookup"><span data-stu-id="8bf74-142">However, if you don't choose hello best column hello first time, you can easily re-distribute hello data on a different column.</span></span> 

<span data-ttu-id="8bf74-143">toochoose hello распространения оптимальным для каждой таблицы в статье [распределенных таблиц](sql-data-warehouse-tables-distribute.md).</span><span class="sxs-lookup"><span data-stu-id="8bf74-143">toochoose hello best distribution option for each table, see [Distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="8bf74-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8bf74-144">Next steps</span></span>
<span data-ttu-id="8bf74-145">Вы успешно перенесли вашей tooSQL схемы базы данных хранилища данных, откройте tooone из hello в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="8bf74-145">Once you have successfully migrated your database schema tooSQL Data Warehouse, proceed tooone of hello following articles:</span></span>

* <span data-ttu-id="8bf74-146">[Перенос данных][Migrate your data]</span><span class="sxs-lookup"><span data-stu-id="8bf74-146">[Migrate your data][Migrate your data]</span></span>
* <span data-ttu-id="8bf74-147">[Перенос кода][Migrate your code]</span><span class="sxs-lookup"><span data-stu-id="8bf74-147">[Migrate your code][Migrate your code]</span></span>

<span data-ttu-id="8bf74-148">Дополнительные сведения о хранилище данных SQL советы и рекомендации см. в разделе hello [рекомендации] [ best practices] статьи.</span><span class="sxs-lookup"><span data-stu-id="8bf74-148">For more about SQL Data Warehouse best practices, see hello [best practices][best practices] article.</span></span>

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
