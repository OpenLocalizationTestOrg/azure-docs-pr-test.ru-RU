---
title: "aaaScale ожидания базы данных Azure SQL | Документы Microsoft"
description: "Как toouse hello ShardMapManager клиентской библиотеке эластичной базы данных"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 0e9d647a-9ba9-4875-aa22-662d01283439
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 4cf670d42ad7ded98fb8d6f0830154587dd2c6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scale-out-databases-with-hello-shard-map-manager"></a><span data-ttu-id="2a3fe-103">Горизонтальное масштабирование баз данных с использованием диспетчера карты сегментов hello</span><span class="sxs-lookup"><span data-stu-id="2a3fe-103">Scale out databases with hello shard map manager</span></span>
<span data-ttu-id="2a3fe-104">tooeasily горизонтальное масштабирование баз данных в SQL Azure, используйте диспетчера карты сегментов.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-104">tooeasily scale out databases on SQL Azure, use a shard map manager.</span></span> <span data-ttu-id="2a3fe-105">диспетчера карты сегментов Hello является специальная база данных, которое поддерживает глобального сопоставления информацию о всем сегментам (базы данных) в наборе сегментов.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-105">hello shard map manager is a special database that maintains global mapping information about all shards (databases) in a shard set.</span></span> <span data-ttu-id="2a3fe-106">Hello метаданных позволяет tooconnect toohello правильный базы данных приложения на основе значения hello hello **ключа сегментирования**.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-106">hello metadata allows an application tooconnect toohello correct database based upon hello value of hello **sharding key**.</span></span> <span data-ttu-id="2a3fe-107">Кроме того, каждый сегмент в наборе hello содержит maps, отслеживающие hello локального сегментов данных (известный как **Подсегменты**).</span><span class="sxs-lookup"><span data-stu-id="2a3fe-107">In addition, every shard in hello set contains maps that track hello local shard data (known as **shardlets**).</span></span> 

![Управление размещением сегментов](./media/sql-database-elastic-scale-shard-map-management/glossary.png)

<span data-ttu-id="2a3fe-109">Понимание того, как создавать эти карты, управления essential tooshard карты.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-109">Understanding how these maps are constructed is essential tooshard map management.</span></span> <span data-ttu-id="2a3fe-110">Это делается с помощью hello [класса ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)в hello [клиентской библиотеке эластичной базы данных](sql-database-elastic-database-client-library.md) toomanage сегмент соответствует.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-110">This is done using hello [ShardMapManager class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx), found in hello [Elastic Database client library](sql-database-elastic-database-client-library.md) toomanage shard maps.</span></span>  

## <a name="shard-maps-and-shard-mappings"></a><span data-ttu-id="2a3fe-111">Карты сегментов и сопоставление сегментов</span><span class="sxs-lookup"><span data-stu-id="2a3fe-111">Shard maps and shard mappings</span></span>
<span data-ttu-id="2a3fe-112">Для каждого сегмента необходимо выбрать тип hello toocreate карты сегментов.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-112">For each shard, you must select hello type of shard map toocreate.</span></span> <span data-ttu-id="2a3fe-113">Выбор Hello зависит от архитектуры hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-113">hello choice depends on hello database architecture:</span></span> 

1. <span data-ttu-id="2a3fe-114">По одному клиенту для каждой базы данных.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-114">Single tenant per database</span></span>  
2. <span data-ttu-id="2a3fe-115">Несколько клиентов на одну базу данных (два типа):</span><span class="sxs-lookup"><span data-stu-id="2a3fe-115">Multiple tenants per database (two types):</span></span>
   1. <span data-ttu-id="2a3fe-116">Сопоставление по спискам</span><span class="sxs-lookup"><span data-stu-id="2a3fe-116">List mapping</span></span>
   2. <span data-ttu-id="2a3fe-117">Сопоставление по диапазонам</span><span class="sxs-lookup"><span data-stu-id="2a3fe-117">Range mapping</span></span>

<span data-ttu-id="2a3fe-118">Для модели с одним клиентом создайте карту сегментов с **сопоставлением по списку** .</span><span class="sxs-lookup"><span data-stu-id="2a3fe-118">For a single-tenant model, create a **list mapping** shard map.</span></span> <span data-ttu-id="2a3fe-119">модель одного клиента Hello назначает одной базы данных на клиенте.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-119">hello single-tenant model assigns one database per tenant.</span></span> <span data-ttu-id="2a3fe-120">Эта модель подходит для разработчиков SaaS, так как она упрощает управление.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-120">This is an effective model for SaaS developers as it simplifies management.</span></span>

![Сопоставление по спискам][1]

<span data-ttu-id="2a3fe-122">Hello мультитенантной модели назначает несколько клиентов tooa одной базы данных (и групп клиентов можно распределить по нескольким базам данных).</span><span class="sxs-lookup"><span data-stu-id="2a3fe-122">hello multi-tenant model assigns several tenants tooa single database (and you can distribute groups of tenants across multiple databases).</span></span> <span data-ttu-id="2a3fe-123">Эту модель можно используйте, когда предполагается, что данные, toohave небольшой каждого клиента.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-123">Use this model when you expect each tenant toohave small data needs.</span></span> <span data-ttu-id="2a3fe-124">В этой модели мы назначает диапазон клиентов tooa базы данных с помощью **сопоставления диапазона**.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-124">In this model, we assign a range of tenants tooa database using **range mapping**.</span></span> 

![Сопоставление по диапазонам][2]

<span data-ttu-id="2a3fe-126">Или можно применить модель базы данных нескольких клиентов с помощью *сопоставление списка* tooassign несколько клиентов tooa одной базы данных.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-126">Or you can implement a multi-tenant database model using a *list mapping* tooassign multiple tenants tooa single database.</span></span> <span data-ttu-id="2a3fe-127">Например используется toostore сведения об ИД клиента 1 и 5 — DB1 и DB2 хранит данные для клиента 7 и 10 клиента.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-127">For example, DB1 is used toostore information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span></span> 

![Несколько клиентов для одной базы данных][3] 

### <a name="supported-net-types-for-sharding-keys"></a><span data-ttu-id="2a3fe-129">Поддерживаемые типы .net для ключей сегментирования</span><span class="sxs-lookup"><span data-stu-id="2a3fe-129">Supported .Net types for sharding keys</span></span>
<span data-ttu-id="2a3fe-130">Эластичный hello поддержки масштабирования, следующие .net Framework типы как ключи сегментирования:</span><span class="sxs-lookup"><span data-stu-id="2a3fe-130">Elastic Scale support hello following .Net Framework types as sharding keys:</span></span>

* <span data-ttu-id="2a3fe-131">целое число</span><span class="sxs-lookup"><span data-stu-id="2a3fe-131">integer</span></span>
* <span data-ttu-id="2a3fe-132">длинное целое число</span><span class="sxs-lookup"><span data-stu-id="2a3fe-132">long</span></span>
* <span data-ttu-id="2a3fe-133">guid</span><span class="sxs-lookup"><span data-stu-id="2a3fe-133">guid</span></span>
* <span data-ttu-id="2a3fe-134">byte[]</span><span class="sxs-lookup"><span data-stu-id="2a3fe-134">byte[]</span></span>  
* <span data-ttu-id="2a3fe-135">datetime;</span><span class="sxs-lookup"><span data-stu-id="2a3fe-135">datetime</span></span>
* <span data-ttu-id="2a3fe-136">интервал времени</span><span class="sxs-lookup"><span data-stu-id="2a3fe-136">timespan</span></span>
* <span data-ttu-id="2a3fe-137">datetimeoffset;</span><span class="sxs-lookup"><span data-stu-id="2a3fe-137">datetimeoffset</span></span>

### <a name="list-and-range-shard-maps"></a><span data-ttu-id="2a3fe-138">Списочные и диапазонные карты сегментов</span><span class="sxs-lookup"><span data-stu-id="2a3fe-138">List and range shard maps</span></span>
<span data-ttu-id="2a3fe-139">Карты сегментов могут быть созданы с использованием **списков индивидуальных величин сегментных ключей** или с использованием **диапазонов величин сегментных ключей**.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-139">Shard maps can be constructed using **lists of individual sharding key values**, or they can be constructed using **ranges of sharding key values**.</span></span> 

### <a name="list-shard-maps"></a><span data-ttu-id="2a3fe-140">Списочные карты сегментов</span><span class="sxs-lookup"><span data-stu-id="2a3fe-140">List shard maps</span></span>
<span data-ttu-id="2a3fe-141">**Сегменты** содержат **Подсегменты** и hello сопоставление подсегментов tooshards обеспечивается карты сегментов.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-141">**Shards** contain **shardlets** and hello mapping of shardlets tooshards is maintained by a shard map.</span></span> <span data-ttu-id="2a3fe-142">Объект **карта сегментов список** — это связь между hello отдельные значения ключей, идентифицирующих Подсегменты hello и hello баз данных, которые служат в качестве сегментов.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-142">A **list shard map** is an association between hello individual key values that identify hello shardlets and hello databases that serve as shards.</span></span>  <span data-ttu-id="2a3fe-143">**Список сопоставлений** явные и различные значения ключа может быть сопоставленных toohello одной базе данных.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-143">**List mappings** are explicit and different key values can be mapped toohello same database.</span></span> <span data-ttu-id="2a3fe-144">Например раздел 1 сопоставляет tooDatabase A и B. база данных ссылаются на значения ключей, 3 и 6</span><span class="sxs-lookup"><span data-stu-id="2a3fe-144">For example, key 1 maps tooDatabase A, and key values 3 and 6 both reference Database B.</span></span>

| <span data-ttu-id="2a3fe-145">Ключ</span><span class="sxs-lookup"><span data-stu-id="2a3fe-145">Key</span></span> | <span data-ttu-id="2a3fe-146">Расположение сегмента</span><span class="sxs-lookup"><span data-stu-id="2a3fe-146">Shard Location</span></span> |
| --- | --- |
| <span data-ttu-id="2a3fe-147">1</span><span class="sxs-lookup"><span data-stu-id="2a3fe-147">1</span></span> |<span data-ttu-id="2a3fe-148">БазаДанных_А</span><span class="sxs-lookup"><span data-stu-id="2a3fe-148">Database_A</span></span> |
| <span data-ttu-id="2a3fe-149">3</span><span class="sxs-lookup"><span data-stu-id="2a3fe-149">3</span></span> |<span data-ttu-id="2a3fe-150">БазаДанных_Б</span><span class="sxs-lookup"><span data-stu-id="2a3fe-150">Database_B</span></span> |
| <span data-ttu-id="2a3fe-151">4.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-151">4</span></span> |<span data-ttu-id="2a3fe-152">БазаДанных_В</span><span class="sxs-lookup"><span data-stu-id="2a3fe-152">Database_C</span></span> |
| <span data-ttu-id="2a3fe-153">6</span><span class="sxs-lookup"><span data-stu-id="2a3fe-153">6</span></span> |<span data-ttu-id="2a3fe-154">БазаДанных_Б</span><span class="sxs-lookup"><span data-stu-id="2a3fe-154">Database_B</span></span> |
| <span data-ttu-id="2a3fe-155">...</span><span class="sxs-lookup"><span data-stu-id="2a3fe-155">...</span></span> |<span data-ttu-id="2a3fe-156">...</span><span class="sxs-lookup"><span data-stu-id="2a3fe-156">...</span></span> |

### <a name="range-shard-maps"></a><span data-ttu-id="2a3fe-157">Диапазонные карты сегментов</span><span class="sxs-lookup"><span data-stu-id="2a3fe-157">Range shard maps</span></span>
<span data-ttu-id="2a3fe-158">В **карта сегментов диапазон**, диапазона ключей hello описан с помощью пары **[высокой стоимости, большое значение)** где hello *высокой стоимости* — минимальный ключ hello в диапазоне hello и hello *Высокое значение* является hello первое значение выше диапазона hello.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-158">In a **range shard map**, hello key range is described by a pair **[Low Value, High Value)** where hello *Low Value* is hello minimum key in hello range, and hello *High Value* is hello first value higher than hello range.</span></span> 

<span data-ttu-id="2a3fe-159">Например **[0, 100)** включает все целые числа, которые больше или равны 0 и меньше 100.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-159">For example, **[0, 100)** includes all integers greater than or equal 0 and less than 100.</span></span> <span data-ttu-id="2a3fe-160">Обратите внимание, что поддерживаются несколько toohello точка может диапазоны же базы данных и несвязанных диапазонов (например, [100,200) и [400,600) обоих точки tooDatabase C в приведенном ниже примере hello.)</span><span class="sxs-lookup"><span data-stu-id="2a3fe-160">Note that multiple ranges can point toohello same database, and disjoint ranges are supported (e.g., [100,200) and [400,600) both point tooDatabase C in hello example below.)</span></span>

| <span data-ttu-id="2a3fe-161">Ключ</span><span class="sxs-lookup"><span data-stu-id="2a3fe-161">Key</span></span> | <span data-ttu-id="2a3fe-162">Расположение сегмента</span><span class="sxs-lookup"><span data-stu-id="2a3fe-162">Shard Location</span></span> |
| --- | --- |
| <span data-ttu-id="2a3fe-163">[1,50)</span><span class="sxs-lookup"><span data-stu-id="2a3fe-163">[1,50)</span></span> |<span data-ttu-id="2a3fe-164">БазаДанных_А</span><span class="sxs-lookup"><span data-stu-id="2a3fe-164">Database_A</span></span> |
| <span data-ttu-id="2a3fe-165">[50,100)</span><span class="sxs-lookup"><span data-stu-id="2a3fe-165">[50,100)</span></span> |<span data-ttu-id="2a3fe-166">БазаДанных_Б</span><span class="sxs-lookup"><span data-stu-id="2a3fe-166">Database_B</span></span> |
| <span data-ttu-id="2a3fe-167">[100,200)</span><span class="sxs-lookup"><span data-stu-id="2a3fe-167">[100,200)</span></span> |<span data-ttu-id="2a3fe-168">БазаДанных_В</span><span class="sxs-lookup"><span data-stu-id="2a3fe-168">Database_C</span></span> |
| <span data-ttu-id="2a3fe-169">[400,600)</span><span class="sxs-lookup"><span data-stu-id="2a3fe-169">[400,600)</span></span> |<span data-ttu-id="2a3fe-170">БазаДанных_В</span><span class="sxs-lookup"><span data-stu-id="2a3fe-170">Database_C</span></span> |
| <span data-ttu-id="2a3fe-171">...</span><span class="sxs-lookup"><span data-stu-id="2a3fe-171">...</span></span> |<span data-ttu-id="2a3fe-172">...</span><span class="sxs-lookup"><span data-stu-id="2a3fe-172">...</span></span> |

<span data-ttu-id="2a3fe-173">Каждый из вышеуказанных таблиц hello является пример **ShardMap** объекта.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-173">Each of hello tables shown above is a conceptual example of a **ShardMap** object.</span></span> <span data-ttu-id="2a3fe-174">Каждая строка является упрощенным примером индивидуального **PointMapping** (для карты сегментов hello списка) или **RangeMapping** (для карты сегментов hello диапазона) объекта.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-174">Each row is a simplified example of an individual **PointMapping** (for hello list shard map) or **RangeMapping** (for hello range shard map) object.</span></span>

## <a name="shard-map-manager"></a><span data-ttu-id="2a3fe-175">Диспетчер карты сегментов</span><span class="sxs-lookup"><span data-stu-id="2a3fe-175">Shard map manager</span></span>
<span data-ttu-id="2a3fe-176">В клиентской библиотеке hello hello диспетчера карты сегментов — это совокупность карт сегментов.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-176">In hello client library, hello shard map  manager is a collection of shard maps.</span></span> <span data-ttu-id="2a3fe-177">Здравствуйте, данные, которыми управляет **ShardMapManager** экземпляр сохраняется в трех местах:</span><span class="sxs-lookup"><span data-stu-id="2a3fe-177">hello data managed by a **ShardMapManager** instance is kept in three places:</span></span> 

1. <span data-ttu-id="2a3fe-178">**Глобальные карты сегментов (GSM)**: укажите tooserve базы данных в качестве hello репозиторий для всех карт сегментов и сопоставления.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-178">**Global Shard Map (GSM)**: You specify a database tooserve as hello repository for all of its shard maps and mappings.</span></span> <span data-ttu-id="2a3fe-179">Специальные таблицы и хранимые процедуры создаются автоматически toomanage hello сведения.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-179">Special tables and stored procedures are automatically created toomanage hello information.</span></span> <span data-ttu-id="2a3fe-180">Это обычно небольшая база данных и в незначительной степени доступ и не должны использоваться для других нужд приложения hello.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-180">This is typically a small database and lightly accessed, and it should not be used for other needs of hello application.</span></span> <span data-ttu-id="2a3fe-181">Hello таблицы расположены в специальной схеме с именем **__ShardManagement**.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-181">hello tables are in a special schema named **__ShardManagement**.</span></span> 
2. <span data-ttu-id="2a3fe-182">**Локальный карты сегментов (LSM)**: каждой базы данных, укажите toobe сегмент — изменить toocontain несколько небольших таблиц и специальные хранимые процедуры, которые содержат и управляют сведения о конкретных toothat сегментов карты сегментов.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-182">**Local Shard Map (LSM)**: Every database that you specify toobe a shard is modified toocontain several small tables and special stored procedures that contain and manage shard map information specific toothat shard.</span></span> <span data-ttu-id="2a3fe-183">Эти сведения являются избыточными сведениями hello в hello GSM и сведений о карте сегментов в кэше toovalidate приложения hello позволяет без помещения любая нагрузка на hello GSM; приложение Hello использует hello LSM toodetermine, если кэшированные сопоставления по-прежнему действителен.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-183">This information is redundant with hello information in hello GSM, and it allows hello application toovalidate cached shard map information without placing any load on hello GSM; hello application uses hello LSM toodetermine if a cached mapping is still valid.</span></span> <span data-ttu-id="2a3fe-184">Hello таблиц соответствующего toohello LSM на каждый сегмент также находятся в схеме hello **__ShardManagement**.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-184">hello tables corresponding toohello LSM on each shard are also in hello schema **__ShardManagement**.</span></span>
3. <span data-ttu-id="2a3fe-185">**Кэш приложения**: каждый экземпляр приложения, у которого есть доступ к объекту **ShardMapManager**, поддерживает локальный кэш своих сопоставлений в памяти.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-185">**Application cache**: Each application instance accessing a **ShardMapManager** object maintains a local in-memory cache of its mappings.</span></span> <span data-ttu-id="2a3fe-186">Хранятся использованные за последнее время сведения о маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-186">It stores routing information that has recently been retrieved.</span></span> 

## <a name="constructing-a-shardmapmanager"></a><span data-ttu-id="2a3fe-187">Создание объекта ShardMapManager</span><span class="sxs-lookup"><span data-stu-id="2a3fe-187">Constructing a ShardMapManager</span></span>
<span data-ttu-id="2a3fe-188">Объект **ShardMapManager** создается с помощью шаблона [фабрики](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) .</span><span class="sxs-lookup"><span data-stu-id="2a3fe-188">A **ShardMapManager** object is constructed using a [factory](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) pattern.</span></span> <span data-ttu-id="2a3fe-189">Hello  **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**  метод принимает учетные данные (включая имя сервера hello и имя базы данных, содержащий hello GSM) в форме hello  **ConnectionString** и возвращает экземпляр класса **ShardMapManager**.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-189">hello **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)** method takes credentials (including hello server name and database name holding hello GSM) in hello form of a **ConnectionString** and returns an instance of a **ShardMapManager**.</span></span>  

<span data-ttu-id="2a3fe-190">**Имейте в виду:** hello **ShardMapManager** должен создаваться только один раз на домен приложения, в код инициализации hello для приложения.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-190">**Please Note:** hello **ShardMapManager** should be instantiated only once per app domain, within hello initialization code for an application.</span></span> <span data-ttu-id="2a3fe-191">Создание дополнительных экземпляров ShardMapManager в hello того же домена приложения, приведет к увеличение памяти и ЦП приложения hello.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-191">Creation of additional instances of ShardMapManager in hello same appdomain, will result in increased memory and CPU utilization of hello application.</span></span> <span data-ttu-id="2a3fe-192">**ShardMapManager** может содержать любое число карт сегментов.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-192">A **ShardMapManager** can contain any number of shard maps.</span></span> <span data-ttu-id="2a3fe-193">Многим приложениям достаточно одной карты сегментов, но в некоторых случаях применяются разные наборы баз данных, которые используются в разных схемах или имеют уникальное назначение. В таком случае желательно использовать несколько карт сегментов.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-193">While a single shard map may be sufficient for many applications, there are times when different sets of databases are used for different schema or for unique purposes; in those cases multiple shard maps may be preferable.</span></span> 

<span data-ttu-id="2a3fe-194">В этом коде приложение попытается tooopen существующий **ShardMapManager** с hello [TryGetSqlShardMapManager метод](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="2a3fe-194">In this code, an application tries tooopen an existing **ShardMapManager** with hello [TryGetSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).</span></span>  <span data-ttu-id="2a3fe-195">Если объекты, представляющие Global **ShardMapManager** (GSM) еще не существует в базе данных hello, hello клиентская библиотека создает их наличие с помощью hello [CreateSqlShardMapManager метод](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="2a3fe-195">If objects representing a Global **ShardMapManager** (GSM) do not yet exist inside hello database, hello client library creates them there using hello [CreateSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).</span></span>

    // Try tooget a reference toohello Shard Map Manager 
     // via hello Shard Map Manager database.  
    // If it doesn't already exist, then create it. 
    ShardMapManager shardMapManager; 
    bool shardMapManagerExists = ShardMapManagerFactory.TryGetSqlShardMapManager(
                                        connectionString, 
                                        ShardMapManagerLoadPolicy.Lazy, 
                                        out shardMapManager); 

    if (shardMapManagerExists) 
     { 
        Console.WriteLine("Shard Map Manager already exists");
    } 
    else
    {
        // Create hello Shard Map Manager. 
        ShardMapManagerFactory.CreateSqlShardMapManager(connectionString);
        Console.WriteLine("Created SqlShardMapManager"); 

        shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager(
            connectionString, 
            ShardMapManagerLoadPolicy.Lazy);

        // hello connectionString contains server name, database name, and admin credentials 
        // for privileges on both hello GSM and hello shards themselves.
    } 

<span data-ttu-id="2a3fe-196">В качестве альтернативы можно использовать Powershell toocreate нового диспетчера карты сегментов.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-196">As an alternative, you can use Powershell toocreate a new Shard Map Manager.</span></span> <span data-ttu-id="2a3fe-197">Пример представлен [здесь](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="2a3fe-197">An example is available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

## <a name="get-a-rangeshardmap-or-listshardmap"></a><span data-ttu-id="2a3fe-198">Получение RangeShardMap или ListShardMap</span><span class="sxs-lookup"><span data-stu-id="2a3fe-198">Get a RangeShardMap or ListShardMap</span></span>
<span data-ttu-id="2a3fe-199">После создания диспетчера карты сегментов, можно получить hello [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) или [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) с помощью hello [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), hello [ TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), или hello [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) метод.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-199">After creating a shard map manager, you can get hello [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) or [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) using hello [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), hello [TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), or hello [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) method.</span></span>

    /// <summary>
    /// Creates a new Range Shard Map with hello specified name, or gets hello Range Shard Map if it already exists.
    /// </summary>
    public static RangeShardMap<T> CreateOrGetRangeShardMap<T>(ShardMapManager shardMapManager, string shardMapName)
    {
        // Try tooget a reference toohello Shard Map.
        RangeShardMap<T> shardMap;
        bool shardMapExists = shardMapManager.TryGetRangeShardMap(shardMapName, out shardMap);

        if (shardMapExists)
        {
            ConsoleUtils.WriteInfo("Shard Map {0} already exists", shardMap.Name);
        }
        else
        {
            // hello Shard Map does not exist, so create it
            shardMap = shardMapManager.CreateRangeShardMap<T>(shardMapName);
            ConsoleUtils.WriteInfo("Created Shard Map {0}", shardMap.Name);
        }

        return shardMap;
    } 

### <a name="shard-map-administration-credentials"></a><span data-ttu-id="2a3fe-200">Учетные данные для администрирования карты сегментов</span><span class="sxs-lookup"><span data-stu-id="2a3fe-200">Shard map administration credentials</span></span>
<span data-ttu-id="2a3fe-201">Приложения, администрирования и управления ими карт сегментов, отличаются от привязок, использующих подключения tooroute карты сегментов hello.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-201">Applications that administer and manipulate shard maps are different from those that use hello shard maps tooroute connections.</span></span> 

<span data-ttu-id="2a3fe-202">Сопоставляет tooadminister сегментов (Добавление или изменение сегментов, карт сегментов, сопоставления сегментов, т. д.) необходимо создать экземпляр hello **ShardMapManager** с помощью **учетные данные, имеющие права на обе базы данных GSM hello и на каждом чтение и запись базы данных, которая служит в качестве сегментом**.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-202">tooadminister shard maps (add or change shards, shard maps, shard mappings, etc.) you must instantiate hello **ShardMapManager** using **credentials that have read/write privileges on both hello GSM database and on each database that serves as a shard**.</span></span> <span data-ttu-id="2a3fe-203">Hello учетные данные необходимо разрешить для записи в таблицах hello в обоих hello GSM и LSM как вводится или изменяется, также как и для создания таблиц LSM на новые сегменты сведений о карте сегментов.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-203">hello credentials must allow for writes against hello tables in both hello GSM and LSM as shard map information is entered or changed, as well as for creating LSM tables on new shards.</span></span>  

<span data-ttu-id="2a3fe-204">В разделе [учетные данные, используемые tooaccess hello эластичной базы данных клиентской библиотеки](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="2a3fe-204">See [Credentials used tooaccess hello Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span>

### <a name="only-metadata-affected"></a><span data-ttu-id="2a3fe-205">Воздействует только на метаданные</span><span class="sxs-lookup"><span data-stu-id="2a3fe-205">Only metadata affected</span></span>
<span data-ttu-id="2a3fe-206">Методы, используемые для заполнения или изменение hello **ShardMapManager** данных не меняйте hello пользователем данные, хранящиеся в сегменты hello сами.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-206">Methods used for populating or changing hello **ShardMapManager** data do not alter hello user data stored in hello shards themselves.</span></span> <span data-ttu-id="2a3fe-207">Например, методы, такие как **CreateShard**, **DeleteShard**, **UpdateMapping**, т. д. влияют на hello сегментов карты только метаданные.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-207">For example, methods such as **CreateShard**, **DeleteShard**, **UpdateMapping**, etc. affect hello shard map metadata only.</span></span> <span data-ttu-id="2a3fe-208">Не удаляйте, добавления или изменения пользовательских данных, содержащихся в сегментах hello.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-208">They do not remove, add, or alter user data contained in hello shards.</span></span> <span data-ttu-id="2a3fe-209">Вместо этого эти методы являются спроектированный toobe используется в сочетании с отдельные операции можно выполнять toocreate и удаления действительных баз данных или переместить строки из одного сегмента tooanother toorebalance сегментированных среды.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-209">Instead, these methods are designed toobe used in conjunction with separate operations you perform toocreate or remove actual databases, or that move rows from one shard tooanother toorebalance a sharded environment.</span></span>  <span data-ttu-id="2a3fe-210">(hello **разделения слияния** средства, включенная в средства эластичной базы данных использует эти API-интерфейсы, а также управляя операциями перемещения фактических данных между сегментами.) В разделе [масштабирования с помощью средства hello разделения эластичной базы данных-слияния](sql-database-elastic-scale-overview-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="2a3fe-210">(hello **split-merge** tool included with elastic database tools makes use of these APIs along with orchestrating actual data movement between shards.) See [Scaling using hello Elastic Database split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md).</span></span>

## <a name="populating-a-shard-map-example"></a><span data-ttu-id="2a3fe-211">Пример заполнения сопоставления сегментов</span><span class="sxs-lookup"><span data-stu-id="2a3fe-211">Populating a shard map example</span></span>
<span data-ttu-id="2a3fe-212">Ниже приведен пример последовательности операций toopopulate карты конкретных сегментов.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-212">An example sequence of operations toopopulate a specific shard map is shown below.</span></span> <span data-ttu-id="2a3fe-213">Hello код выполняет следующие действия.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-213">hello code performs these steps:</span></span> 

1. <span data-ttu-id="2a3fe-214">При помощи диспетчера сопоставления сегментов создается новое сопоставление сегментов.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-214">A new shard map is created within a shard map manager.</span></span> 
2. <span data-ttu-id="2a3fe-215">карта сегментов toohello добавляются метаданные Hello для двух различных сегментах.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-215">hello metadata for two different shards is added toohello shard map.</span></span> 
3. <span data-ttu-id="2a3fe-216">Добавляются различные сопоставления диапазона ключей и hello общее сопоставление сегментов hello отображения.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-216">A variety of key range mappings are added, and hello overall contents of hello shard map are displayed.</span></span> 

<span data-ttu-id="2a3fe-217">Hello код, чтобы метод hello можно перезапустить, если произошла ошибка.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-217">hello code is written so that hello method can be rerun if an error occurs.</span></span> <span data-ttu-id="2a3fe-218">Каждый запрос проверяет, является ли тот или иной сегмент или сопоставление уже существует, прежде чем toocreate его.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-218">Each request tests whether a shard or mapping already exists, before attempting toocreate it.</span></span> <span data-ttu-id="2a3fe-219">Hello коде предполагается, что базы данных с именем **sample_shard_0**, **sample_shard_1** и **sample_shard_2** уже были созданы в hello server ссылается строка **shardServer**.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-219">hello code assumes that databases named **sample_shard_0**, **sample_shard_1** and **sample_shard_2** have already been created in hello server referenced by string **shardServer**.</span></span> 

    public void CreatePopulatedRangeMap(ShardMapManager smm, string mapName) 
        {            
            RangeShardMap<long> sm = null; 

            // check if shardmap exists and if not, create it 
            if (!smm.TryGetRangeShardMap(mapName, out sm)) 
            { 
                sm = smm.CreateRangeShardMap<long>(mapName); 
            } 

            Shard shard0 = null, shard1=null; 
            // Check if shard exists and if not, 
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetShard(new ShardLocation(
                                     shardServer, 
                                     "sample_shard_0"), 
                                     out shard0)) 
            { 
                Shard0 = sm.CreateShard(new ShardLocation(
                                            shardServer, 
                                            "sample_shard_0")); 
            } 

            if (!sm.TryGetShard(new ShardLocation(
                                    shardServer, 
                                    "sample_shard_1"), 
                                    out shard1)) 
            { 
                Shard1 = sm.CreateShard(new ShardLocation(
                                             shardServer, 
                                            "sample_shard_1"));  
            } 

            RangeMapping<long> rmpg=null; 

            // Check if mapping exists and if not,
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetMappingForKey(0, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                          new RangeMappingCreationInfo<long>
                          (new Range<long>(0, 50), 
                          shard0, 
                          MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(50, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(50, 100), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(100, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long>
                         (new Range<long>(100, 150), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(150, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(150, 200), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(200, out rmpg)) 
            { 
               sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(200, 300), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            // List hello shards and mappings 
            foreach (Shard s in sm.GetShards()
                         .OrderBy(s => s.Location.DataSource)
                         .ThenBy(s => s.Location.Database))
            { 
               Console.WriteLine("shard: "+ s.Location); 
            } 

            foreach (RangeMapping<long> rm in sm.GetMappings()) 
            { 
                Console.WriteLine("range: [" + rm.Value.Low.ToString() + ":" 
                        + rm.Value.High.ToString()+ ")  ==>" +rm.Shard.Location); 
            } 
        } 

<span data-ttu-id="2a3fe-220">Как можно использовать PowerShell вместо сценариев tooachieve hello же результат.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-220">As an alternative you can use PowerShell scripts tooachieve hello same result.</span></span> <span data-ttu-id="2a3fe-221">Некоторые примеры PowerShell образец hello доступны [здесь](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="2a3fe-221">Some of hello sample PowerShell examples are available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>     

<span data-ttu-id="2a3fe-222">После заполнения карт сегментов приложений доступа к данным могут быть созданы или адаптировать toowork с картами hello.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-222">Once shard maps have been populated, data access applications can be created or adapted toowork with hello maps.</span></span> <span data-ttu-id="2a3fe-223">Заполнение и управления данными карты hello не должен появиться пока **макета карты** должен toochange.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-223">Populating or manipulating hello maps need not occur again until **map layout** needs toochange.</span></span>  

## <a name="data-dependent-routing"></a><span data-ttu-id="2a3fe-224">Маршрутизация, зависящая от данных</span><span class="sxs-lookup"><span data-stu-id="2a3fe-224">Data dependent routing</span></span>
<span data-ttu-id="2a3fe-225">диспетчера карты сегментов Hello наиболее будет использоваться в приложениях, требующих операций данных конкретного приложения hello tooperform подключения базы данных.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-225">hello shard map manager will be most used in applications that require database connections tooperform hello app-specific data operations.</span></span> <span data-ttu-id="2a3fe-226">Эти соединения должна быть связана с hello нужную базу данных.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-226">Those connections must be associated with hello correct database.</span></span> <span data-ttu-id="2a3fe-227">Это называется **маршрутизацией, зависимой от данных**.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-227">This is known as **Data Dependent Routing**.</span></span> <span data-ttu-id="2a3fe-228">Для этих приложений создание экземпляра объекта диспетчера карты сегментов из фабрики hello, используя учетные данные, иметь доступ только для чтения данных GSM hello.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-228">For these applications, instantiate a shard map manager object from hello factory using credentials that have read-only access on hello GSM database.</span></span> <span data-ttu-id="2a3fe-229">Отдельные запросы для подключения к более поздней версии предоставить учетные данные, необходимые для соединения базы данных toohello соответствующий сегмент.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-229">Individual requests for later connections supply credentials necessary for connecting toohello appropriate shard database.</span></span>

<span data-ttu-id="2a3fe-230">Обратите внимание, что эти приложения (с помощью **ShardMapManager** открывается с учетными данными только для чтения) не может вносить в них изменения toohello сопоставления или сопоставления.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-230">Note that these applications (using **ShardMapManager** opened with read-only credentials) cannot make changes toohello maps or mappings.</span></span> <span data-ttu-id="2a3fe-231">Для этого создайте специальные административные приложения или сценарии PowerShell, которые будут передавать учетные данные с более высокими правами доступа, как об этом говорилось ранее.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-231">For those needs, create administrative-specific applications or PowerShell scripts that supply higher-privileged credentials as discussed earlier.</span></span> <span data-ttu-id="2a3fe-232">В разделе [учетные данные, используемые tooaccess hello эластичной базы данных клиентской библиотеки](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="2a3fe-232">See [Credentials used tooaccess hello Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span>

<span data-ttu-id="2a3fe-233">Дополнительные сведения см. в статье [Маршрутизация, зависящая от данных](sql-database-elastic-scale-data-dependent-routing.md).</span><span class="sxs-lookup"><span data-stu-id="2a3fe-233">For more details, see [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> 

## <a name="modifying-a-shard-map"></a><span data-ttu-id="2a3fe-234">Изменение карты сегментов</span><span class="sxs-lookup"><span data-stu-id="2a3fe-234">Modifying a shard map</span></span>
<span data-ttu-id="2a3fe-235">Карту сегментов можно изменять различными способами.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-235">A shard map can be changed in different ways.</span></span> <span data-ttu-id="2a3fe-236">Все следующие методы hello изменить hello метаданные, описывающие hello сегментов и их сопоставлений, но физически не изменяют данные в сегменты hello или сделать их создания или удаления hello действительных баз данных.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-236">All of hello following methods modify hello metadata describing hello shards and their mappings, but they do not physically modify data within hello shards, nor do they create or delete hello actual databases.</span></span>  <span data-ttu-id="2a3fe-237">Некоторые операции hello на карте сегментов hello, описанных ниже может понадобиться toobe, координируемых с административные действия, физически переместить данные или, добавлять и удалять базы данных, которые выступают в качестве сегментов.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-237">Some of hello operations on hello shard map described below may need toobe coordinated with administrative actions that physically move data or that add and remove databases serving as shards.</span></span>

<span data-ttu-id="2a3fe-238">Эти методы работают вместе как hello стандартные блоки, доступные для изменения hello общее распределение данных в вашей среде сегментированной базы данных.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-238">These methods work together as hello building blocks available for modifying hello overall distribution of data in your sharded database environment.</span></span>  

* <span data-ttu-id="2a3fe-239">tooadd или удаления сегментов: использовать  **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)**  и  **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)**  из hello [Shardmap класса](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx).</span><span class="sxs-lookup"><span data-stu-id="2a3fe-239">tooadd or remove shards: use **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)** and **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)** of hello [Shardmap class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx).</span></span> 
  
    <span data-ttu-id="2a3fe-240">Hello сервера и базы данных, представляющий целевой сегментов hello должен существовать для tooexecute этих операций.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-240">hello server and database representing hello target shard must already exist for these operations tooexecute.</span></span> <span data-ttu-id="2a3fe-241">Эти методы никак не повлияли на hello самих базах данных, только на метаданные в карте сегментов hello.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-241">These methods do not have any impact on hello databases themselves, only on metadata in hello shard map.</span></span>
* <span data-ttu-id="2a3fe-242">toocreate или удаление точек или диапазоны, которые сопоставляются toohello сегментов: использовать  **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**,  **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)**  из hello [Класса RangeShardMapping](https://msdn.microsoft.com/library/azure/dn807318.aspx), и  **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)**  из hello [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)</span><span class="sxs-lookup"><span data-stu-id="2a3fe-242">toocreate or remove points or ranges that are mapped toohello shards: use **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**, **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)** of hello [RangeShardMapping class](https://msdn.microsoft.com/library/azure/dn807318.aspx), and **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)** of hello [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)</span></span>
  
    <span data-ttu-id="2a3fe-243">Много разных точек или диапазоны могут быть сопоставленных toohello же сегментов.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-243">Many different points or ranges can be mapped toohello same shard.</span></span> <span data-ttu-id="2a3fe-244">Эти методы изменяют только метаданные, но не изменяют данные, хранящиеся в сегментах.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-244">These methods only affect metadata - they do not affect any data that may already be present in shards.</span></span> <span data-ttu-id="2a3fe-245">Если данные должны удаляются из базы данных hello в порядке toobe согласуется с toobe **DeleteMapping** операций, необходимо будет tooperform этих операций отдельно, но вместе с помощью этих методов.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-245">If data needs toobe removed from hello database in order toobe consistent with **DeleteMapping** operations, you will need tooperform those operations separately but in conjunction with using these methods.</span></span>  
* <span data-ttu-id="2a3fe-246">существующий диапазон toosplit в две или слияния соседних диапазонах в один: использовать  **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)**  и  **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-246">toosplit existing ranges into two, or merge adjacent ranges into one: use **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)** and **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.</span></span>  
  
    <span data-ttu-id="2a3fe-247">Обратите внимание, что разбиение и объединение операций **не изменяйте hello сегментов toowhich ключ значения сопоставляются**.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-247">Note that split and merge operations **do not change hello shard toowhich key values are mapped**.</span></span> <span data-ttu-id="2a3fe-248">Разбиения прерывается существующего диапазона на две части, но оставляет и как сопоставленные toohello же сегментов.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-248">A split breaks an existing range into two parts, but leaves both as mapped toohello same shard.</span></span> <span data-ttu-id="2a3fe-249">Слияние работает в двух соседних диапазонах, которые уже сопоставленных toohello же сегменту, объединение их в один диапазон.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-249">A merge operates on two adjacent ranges that are already mapped toohello same shard, coalescing them into a single range.</span></span>  <span data-ttu-id="2a3fe-250">Hello перемещения точек или сами диапазоны между сегментами должен toobe, координируемых с помощью **UpdateMapping** в сочетании с перемещением фактические данные.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-250">hello movement of points or ranges themselves between shards needs toobe coordinated by using **UpdateMapping** in conjunction with actual data movement.</span></span>  <span data-ttu-id="2a3fe-251">Можно использовать hello **разделения или слияния** toocoordinate изменения карты сегментов с перемещением данных службы, который является частью эластичной базы данных в средствах при необходимости перемещения.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-251">You can use hello **Split/Merge** service that is part of elastic database tools toocoordinate shard map changes with data movement, when movement is needed.</span></span> 
* <span data-ttu-id="2a3fe-252">toore карты (или переместите) отдельные точки или диапазоны toodifferent сегменты: использовать  **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-252">toore-map (or move) individual points or ranges toodifferent shards: use **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.</span></span>  
  
    <span data-ttu-id="2a3fe-253">Так как данные могут требовать перемещать из одного сегмента tooanother в порядке toobe согласуется с toobe **UpdateMapping** операций, необходимо будет tooperform изменения отдельно, но вместе с помощью этих методов.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-253">Since data may need toobe moved from one shard tooanother in order toobe consistent with **UpdateMapping** operations, you will need tooperform that movement separately but in conjunction with using these methods.</span></span>
* <span data-ttu-id="2a3fe-254">tootake сопоставления сети и вне сети: использовать  **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)**  и  **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)**  toocontrol hello состояния сети сопоставление.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-254">tootake mappings online and offline: use **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)** and **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)** toocontrol hello online state of a mapping.</span></span> 
  
    <span data-ttu-id="2a3fe-255">Определенные операции для сопоставлений сегментов, включая **UpdateMapping** и **DeleteMapping**, могут выполняться только в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-255">Certain operations on shard mappings are only allowed when a mapping is in an “offline” state, including **UpdateMapping** and **DeleteMapping**.</span></span> <span data-ttu-id="2a3fe-256">Если сопоставление находится в автономном режиме, то запрос данных с ключом, указывающим на это сопоставление, возвратит ошибку.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-256">When a mapping is offline, a data-dependent request based on a key included in that mapping will return an error.</span></span> <span data-ttu-id="2a3fe-257">Кроме того Если диапазон сначала переводится в автономный режим, сегментов toohello затронуты все подключения автоматически будут уничтожены в порядке tooprevent неправильные или неполные результаты запросов направлена диапазоны изменяемое.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-257">In addition, when a range is first taken offline, all connections toohello affected shard are automatically killed in order tooprevent inconsistent or incomplete results for queries directed against ranges being changed.</span></span> 

<span data-ttu-id="2a3fe-258">Сопоставления являются неизменяемыми объектами в .net.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-258">Mappings are immutable objects in .Net.</span></span>  <span data-ttu-id="2a3fe-259">Все hello методы выше, измените сопоставления также недействительными toothem все ссылки в коде.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-259">All of hello methods above that change mappings also invalidate any references toothem in your code.</span></span> <span data-ttu-id="2a3fe-260">toomake ИТ проще tooperform последовательности операций, изменяющих состояние сопоставления, все методы hello, измените сопоставление возвращают новый сопоставление ссылку, поэтому операции могут быть соединены.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-260">toomake it easier tooperform sequences of operations that change a mapping’s state, all of hello methods that change a mapping return a new mapping reference, so operations can be chained.</span></span> <span data-ttu-id="2a3fe-261">Например при toodelete существующее сопоставление в sm shardmap, который содержит ключ hello 25, можно выполнить следующие hello:</span><span class="sxs-lookup"><span data-stu-id="2a3fe-261">For example, toodelete an existing mapping in shardmap sm that contains hello key 25, you can execute hello following:</span></span> 

        sm.DeleteMapping(sm.MarkMappingOffline(sm.GetMappingForKey(25)));

## <a name="adding-a-shard"></a><span data-ttu-id="2a3fe-262">Добавление сегмента</span><span class="sxs-lookup"><span data-stu-id="2a3fe-262">Adding a shard</span></span>
<span data-ttu-id="2a3fe-263">Приложениям часто требуется toosimply добавить новые данные toohandle сегментов, который ожидается от новых ключей или диапазонов ключей для карты сегментов, которая уже существует.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-263">Applications often need toosimply add new shards toohandle data that is expected from new keys or key ranges, for a shard map that already exists.</span></span> <span data-ttu-id="2a3fe-264">Например приложение сегментированных по ИД клиента может потребоваться tooprovision новый сегмент для нового клиента или ежемесячно сегментированных данных может потребоваться новый сегмент подготовить перед запуском hello каждого нового месяца.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-264">For example, an application sharded by Tenant ID may need tooprovision a new shard for a new tenant, or data sharded monthly may need a new shard provisioned before hello start of each new month.</span></span> 

<span data-ttu-id="2a3fe-265">При hello новый диапазон значений ключа еще не частью существующее сопоставление и перемещение данных отсутствует, это очень простой tooadd hello новый сегмент, связать новый ключ hello или диапазон toothat сегментов.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-265">If hello new range of key values is not already part of an existing mapping and no data movement is necessary, it is very simple tooadd hello new shard and associate hello new key or range toothat shard.</span></span> <span data-ttu-id="2a3fe-266">Дополнительные сведения о добавлении новых сегментов см. в статье [Добавление сегмента с использованием средств эластичных баз данных](sql-database-elastic-scale-add-a-shard.md).</span><span class="sxs-lookup"><span data-stu-id="2a3fe-266">For details on adding new shards, see [Adding a new shard](sql-database-elastic-scale-add-a-shard.md).</span></span>

<span data-ttu-id="2a3fe-267">Тем не менее, в сценариях, требующих перемещения данных, средство разделения слияния hello происходит перемещение данных hello необходимые tooorchestrate между сегментами в сочетании с обновления сопоставлений hello необходимые сегментов.</span><span class="sxs-lookup"><span data-stu-id="2a3fe-267">For scenarios that require data movement, however, hello split-merge tool is needed tooorchestrate hello data movement between shards in combination with hello necessary shard map updates.</span></span> <span data-ttu-id="2a3fe-268">Сведения об использовании hello yool разделения слияния, см. в разделе [Обзор разделения слияния](sql-database-elastic-scale-overview-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="2a3fe-268">For details on using hello split-merge yool, see [Overview of split-merge](sql-database-elastic-scale-overview-split-and-merge.md)</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-shard-map-management/listmapping.png
[2]: ./media/sql-database-elastic-scale-shard-map-management/rangemapping.png
[3]: ./media/sql-database-elastic-scale-shard-map-management/multipleonsingledb.png
