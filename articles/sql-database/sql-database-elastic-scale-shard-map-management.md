---
title: "Развертывание базы данных SQL Azure | Документация Майкрософт"
description: "Использование ShardMapManager, клиентской библиотеки гибких базы данных"
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
ms.openlocfilehash: f626cf417d8b3f1761f3c900d49039b3ff83b093
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="scale-out-databases-with-the-shard-map-manager"></a><span data-ttu-id="80907-103">Развертывание баз данных с использованием диспетчера карты сегментов</span><span class="sxs-lookup"><span data-stu-id="80907-103">Scale out databases with the shard map manager</span></span>
<span data-ttu-id="80907-104">Используйте диспетчер карты сегментов, чтобы легко развертывать базы данных в SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="80907-104">To easily scale out databases on SQL Azure, use a shard map manager.</span></span> <span data-ttu-id="80907-105">Диспетчер карты сегментов — это специальная база данных, которая хранит глобальную информацию о сопоставлении всех сегментов (баз данных), входящих в набор сегментов.</span><span class="sxs-lookup"><span data-stu-id="80907-105">The shard map manager is a special database that maintains global mapping information about all shards (databases) in a shard set.</span></span> <span data-ttu-id="80907-106">Метаданные позволяют приложению подключаться к нужной базе данных, которая определяется по значению **ключа сегментирования**.</span><span class="sxs-lookup"><span data-stu-id="80907-106">The metadata allows an application to connect to the correct database based upon the value of the **sharding key**.</span></span> <span data-ttu-id="80907-107">Кроме того, каждый сегмент в наборе содержит карты, отслеживающие локальные сегменты данных ( **шардлеты**).</span><span class="sxs-lookup"><span data-stu-id="80907-107">In addition, every shard in the set contains maps that track the local shard data (known as **shardlets**).</span></span> 

![Управление размещением сегментов](./media/sql-database-elastic-scale-shard-map-management/glossary.png)

<span data-ttu-id="80907-109">Для управления картами сегментов важно понимать их структуру.</span><span class="sxs-lookup"><span data-stu-id="80907-109">Understanding how these maps are constructed is essential to shard map management.</span></span> <span data-ttu-id="80907-110">Для этого используйте [класс ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx), входящий в [клиентскую библиотеку эластичной базы данных](sql-database-elastic-database-client-library.md). Он позволяет управлять картами сегментов.</span><span class="sxs-lookup"><span data-stu-id="80907-110">This is done using the [ShardMapManager class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx), found in the [Elastic Database client library](sql-database-elastic-database-client-library.md) to manage shard maps.</span></span>  

## <a name="shard-maps-and-shard-mappings"></a><span data-ttu-id="80907-111">Карты сегментов и сопоставление сегментов</span><span class="sxs-lookup"><span data-stu-id="80907-111">Shard maps and shard mappings</span></span>
<span data-ttu-id="80907-112">Для каждого сегмента следует выбрать тип создаваемой карты сегментов.</span><span class="sxs-lookup"><span data-stu-id="80907-112">For each shard, you must select the type of shard map to create.</span></span> <span data-ttu-id="80907-113">Этот выбор зависит от архитектуры базы данных.</span><span class="sxs-lookup"><span data-stu-id="80907-113">The choice depends on the database architecture:</span></span> 

1. <span data-ttu-id="80907-114">По одному клиенту для каждой базы данных.</span><span class="sxs-lookup"><span data-stu-id="80907-114">Single tenant per database</span></span>  
2. <span data-ttu-id="80907-115">Несколько клиентов на одну базу данных (два типа):</span><span class="sxs-lookup"><span data-stu-id="80907-115">Multiple tenants per database (two types):</span></span>
   1. <span data-ttu-id="80907-116">Сопоставление по спискам</span><span class="sxs-lookup"><span data-stu-id="80907-116">List mapping</span></span>
   2. <span data-ttu-id="80907-117">Сопоставление по диапазонам</span><span class="sxs-lookup"><span data-stu-id="80907-117">Range mapping</span></span>

<span data-ttu-id="80907-118">Для модели с одним клиентом создайте карту сегментов с **сопоставлением по списку** .</span><span class="sxs-lookup"><span data-stu-id="80907-118">For a single-tenant model, create a **list mapping** shard map.</span></span> <span data-ttu-id="80907-119">В модели с одним клиентом каждому клиенту назначается по одной базе данных.</span><span class="sxs-lookup"><span data-stu-id="80907-119">The single-tenant model assigns one database per tenant.</span></span> <span data-ttu-id="80907-120">Эта модель подходит для разработчиков SaaS, так как она упрощает управление.</span><span class="sxs-lookup"><span data-stu-id="80907-120">This is an effective model for SaaS developers as it simplifies management.</span></span>

![Сопоставление по спискам][1]

<span data-ttu-id="80907-122">В модели базы данных с несколькими клиентами для одной базы данных назначается несколько клиентов (а группы клиентов можно распределять по нескольким базам данных).</span><span class="sxs-lookup"><span data-stu-id="80907-122">The multi-tenant model assigns several tenants to a single database (and you can distribute groups of tenants across multiple databases).</span></span> <span data-ttu-id="80907-123">Эту модель можно использовать, когда у каждого отдельного клиента низкие потребности в обработке данных.</span><span class="sxs-lookup"><span data-stu-id="80907-123">Use this model when you expect each tenant to have small data needs.</span></span> <span data-ttu-id="80907-124">В этой модели клиенты соотносятся с базой данных с использованием **сопоставления по диапазонам**.</span><span class="sxs-lookup"><span data-stu-id="80907-124">In this model, we assign a range of tenants to a database using **range mapping**.</span></span> 

![Сопоставление по диапазонам][2]

<span data-ttu-id="80907-126">Вы можете также реализовать модель с несколькими клиентами с помощью *сопоставления по списку* , в котором одной базе данных соответствует несколько клиентов.</span><span class="sxs-lookup"><span data-stu-id="80907-126">Or you can implement a multi-tenant database model using a *list mapping* to assign multiple tenants to a single database.</span></span> <span data-ttu-id="80907-127">Например, база данных DB1 используется для хранения информации о клиенте 1 и 5, а DB2 хранит данные о клиенте 7 и 10.</span><span class="sxs-lookup"><span data-stu-id="80907-127">For example, DB1 is used to store information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span></span> 

![Несколько клиентов для одной базы данных][3] 

### <a name="supported-net-types-for-sharding-keys"></a><span data-ttu-id="80907-129">Поддерживаемые типы .net для ключей сегментирования</span><span class="sxs-lookup"><span data-stu-id="80907-129">Supported .Net types for sharding keys</span></span>
<span data-ttu-id="80907-130">Средство эластичного масштабирования поддерживает следующие типы .Net Framework в качестве ключей сегментирования.</span><span class="sxs-lookup"><span data-stu-id="80907-130">Elastic Scale support the following .Net Framework types as sharding keys:</span></span>

* <span data-ttu-id="80907-131">целое число</span><span class="sxs-lookup"><span data-stu-id="80907-131">integer</span></span>
* <span data-ttu-id="80907-132">длинное целое число</span><span class="sxs-lookup"><span data-stu-id="80907-132">long</span></span>
* <span data-ttu-id="80907-133">guid</span><span class="sxs-lookup"><span data-stu-id="80907-133">guid</span></span>
* <span data-ttu-id="80907-134">byte[]</span><span class="sxs-lookup"><span data-stu-id="80907-134">byte[]</span></span>  
* <span data-ttu-id="80907-135">datetime;</span><span class="sxs-lookup"><span data-stu-id="80907-135">datetime</span></span>
* <span data-ttu-id="80907-136">интервал времени</span><span class="sxs-lookup"><span data-stu-id="80907-136">timespan</span></span>
* <span data-ttu-id="80907-137">datetimeoffset;</span><span class="sxs-lookup"><span data-stu-id="80907-137">datetimeoffset</span></span>

### <a name="list-and-range-shard-maps"></a><span data-ttu-id="80907-138">Списочные и диапазонные карты сегментов</span><span class="sxs-lookup"><span data-stu-id="80907-138">List and range shard maps</span></span>
<span data-ttu-id="80907-139">Карты сегментов могут быть созданы с использованием **списков индивидуальных величин сегментных ключей** или с использованием **диапазонов величин сегментных ключей**.</span><span class="sxs-lookup"><span data-stu-id="80907-139">Shard maps can be constructed using **lists of individual sharding key values**, or they can be constructed using **ranges of sharding key values**.</span></span> 

### <a name="list-shard-maps"></a><span data-ttu-id="80907-140">Списочные карты сегментов</span><span class="sxs-lookup"><span data-stu-id="80907-140">List shard maps</span></span>
<span data-ttu-id="80907-141">**Сегменты** содержат **шардлеты**, и сопоставление шардлетов сегментам производится с помощью карты сегментов.</span><span class="sxs-lookup"><span data-stu-id="80907-141">**Shards** contain **shardlets** and the mapping of shardlets to shards is maintained by a shard map.</span></span> <span data-ttu-id="80907-142">**Списочная карта сегментов** представляет ассоциацию между отдельными значениями ключа, определяющими шардлеты, и базами данных, обслуживающими сегменты.</span><span class="sxs-lookup"><span data-stu-id="80907-142">A **list shard map** is an association between the individual key values that identify the shardlets and the databases that serve as shards.</span></span>  <span data-ttu-id="80907-143">**Сопоставления по списку** — это явные и разные значения ключей, которые могут сопоставляться с одной базой данных.</span><span class="sxs-lookup"><span data-stu-id="80907-143">**List mappings** are explicit and different key values can be mapped to the same database.</span></span> <span data-ttu-id="80907-144">Например, ключ 1 соответствует базе данных A, а значения ключей 3 и 6 ссылаются на базу данных B.</span><span class="sxs-lookup"><span data-stu-id="80907-144">For example, key 1 maps to Database A, and key values 3 and 6 both reference Database B.</span></span>

| <span data-ttu-id="80907-145">Ключ</span><span class="sxs-lookup"><span data-stu-id="80907-145">Key</span></span> | <span data-ttu-id="80907-146">Расположение сегмента</span><span class="sxs-lookup"><span data-stu-id="80907-146">Shard Location</span></span> |
| --- | --- |
| <span data-ttu-id="80907-147">1</span><span class="sxs-lookup"><span data-stu-id="80907-147">1</span></span> |<span data-ttu-id="80907-148">БазаДанных_А</span><span class="sxs-lookup"><span data-stu-id="80907-148">Database_A</span></span> |
| <span data-ttu-id="80907-149">3</span><span class="sxs-lookup"><span data-stu-id="80907-149">3</span></span> |<span data-ttu-id="80907-150">БазаДанных_Б</span><span class="sxs-lookup"><span data-stu-id="80907-150">Database_B</span></span> |
| <span data-ttu-id="80907-151">4.</span><span class="sxs-lookup"><span data-stu-id="80907-151">4</span></span> |<span data-ttu-id="80907-152">БазаДанных_В</span><span class="sxs-lookup"><span data-stu-id="80907-152">Database_C</span></span> |
| <span data-ttu-id="80907-153">6</span><span class="sxs-lookup"><span data-stu-id="80907-153">6</span></span> |<span data-ttu-id="80907-154">БазаДанных_Б</span><span class="sxs-lookup"><span data-stu-id="80907-154">Database_B</span></span> |
| <span data-ttu-id="80907-155">...</span><span class="sxs-lookup"><span data-stu-id="80907-155">...</span></span> |<span data-ttu-id="80907-156">...</span><span class="sxs-lookup"><span data-stu-id="80907-156">...</span></span> |

### <a name="range-shard-maps"></a><span data-ttu-id="80907-157">Диапазонные карты сегментов</span><span class="sxs-lookup"><span data-stu-id="80907-157">Range shard maps</span></span>
<span data-ttu-id="80907-158">В **картах сегментов по диапазонам** диапазон ключей описывается парой **[нижнее значение, верхнее значение)**, где *нижнее значение* — минимальный ключ в диапазоне, а *верхнее значение* — первое значение, превышающее диапазон.</span><span class="sxs-lookup"><span data-stu-id="80907-158">In a **range shard map**, the key range is described by a pair **[Low Value, High Value)** where the *Low Value* is the minimum key in the range, and the *High Value* is the first value higher than the range.</span></span> 

<span data-ttu-id="80907-159">Например **[0, 100)** включает все целые числа, которые больше или равны 0 и меньше 100.</span><span class="sxs-lookup"><span data-stu-id="80907-159">For example, **[0, 100)** includes all integers greater than or equal 0 and less than 100.</span></span> <span data-ttu-id="80907-160">Обратите внимание, что несколько диапазонов могут указывать на одну и ту же базу данных, а также поддерживаются перекрытие диапазонов (например, в примере ниже оба диапазона [100,200) и [400,600) указывают на базы данных C).</span><span class="sxs-lookup"><span data-stu-id="80907-160">Note that multiple ranges can point to the same database, and disjoint ranges are supported (e.g., [100,200) and [400,600) both point to Database C in the example below.)</span></span>

| <span data-ttu-id="80907-161">Ключ</span><span class="sxs-lookup"><span data-stu-id="80907-161">Key</span></span> | <span data-ttu-id="80907-162">Расположение сегмента</span><span class="sxs-lookup"><span data-stu-id="80907-162">Shard Location</span></span> |
| --- | --- |
| <span data-ttu-id="80907-163">[1,50)</span><span class="sxs-lookup"><span data-stu-id="80907-163">[1,50)</span></span> |<span data-ttu-id="80907-164">БазаДанных_А</span><span class="sxs-lookup"><span data-stu-id="80907-164">Database_A</span></span> |
| <span data-ttu-id="80907-165">[50,100)</span><span class="sxs-lookup"><span data-stu-id="80907-165">[50,100)</span></span> |<span data-ttu-id="80907-166">БазаДанных_Б</span><span class="sxs-lookup"><span data-stu-id="80907-166">Database_B</span></span> |
| <span data-ttu-id="80907-167">[100,200)</span><span class="sxs-lookup"><span data-stu-id="80907-167">[100,200)</span></span> |<span data-ttu-id="80907-168">БазаДанных_В</span><span class="sxs-lookup"><span data-stu-id="80907-168">Database_C</span></span> |
| <span data-ttu-id="80907-169">[400,600)</span><span class="sxs-lookup"><span data-stu-id="80907-169">[400,600)</span></span> |<span data-ttu-id="80907-170">БазаДанных_В</span><span class="sxs-lookup"><span data-stu-id="80907-170">Database_C</span></span> |
| <span data-ttu-id="80907-171">...</span><span class="sxs-lookup"><span data-stu-id="80907-171">...</span></span> |<span data-ttu-id="80907-172">...</span><span class="sxs-lookup"><span data-stu-id="80907-172">...</span></span> |

<span data-ttu-id="80907-173">Каждая из приведенных выше таблиц является концептуальным примером объекта **ShardMap** .</span><span class="sxs-lookup"><span data-stu-id="80907-173">Each of the tables shown above is a conceptual example of a **ShardMap** object.</span></span> <span data-ttu-id="80907-174">Каждая строка представляет упрощенный пример отдельного **PointMapping** (для карты списка сегментов) или **RangeMapping** (для карты диапазона сегментов) объекта.</span><span class="sxs-lookup"><span data-stu-id="80907-174">Each row is a simplified example of an individual **PointMapping** (for the list shard map) or **RangeMapping** (for the range shard map) object.</span></span>

## <a name="shard-map-manager"></a><span data-ttu-id="80907-175">Диспетчер карты сегментов</span><span class="sxs-lookup"><span data-stu-id="80907-175">Shard map manager</span></span>
<span data-ttu-id="80907-176">В клиентской библиотеке диспетчер карты сегментов — это набор карт сегментов.</span><span class="sxs-lookup"><span data-stu-id="80907-176">In the client library, the shard map  manager is a collection of shard maps.</span></span> <span data-ttu-id="80907-177">Данные, контролируемые объектом **ShardMapManager** , хранятся в трех местах.</span><span class="sxs-lookup"><span data-stu-id="80907-177">The data managed by a **ShardMapManager** instance is kept in three places:</span></span> 

1. <span data-ttu-id="80907-178">**Глобальная карта сегментов (GSM)**: вы указываете базу данных для хранения всех карт сегментов и сопоставлений.</span><span class="sxs-lookup"><span data-stu-id="80907-178">**Global Shard Map (GSM)**: You specify a database to serve as the repository for all of its shard maps and mappings.</span></span> <span data-ttu-id="80907-179">Для управления этой информацией автоматически создаются специальные таблицы и хранимые процедуры.</span><span class="sxs-lookup"><span data-stu-id="80907-179">Special tables and stored procedures are automatically created to manage the information.</span></span> <span data-ttu-id="80907-180">Обычно это база данных небольшая и с простым доступом, и её не рекомендуется использовать для других прикладных задач.</span><span class="sxs-lookup"><span data-stu-id="80907-180">This is typically a small database and lightly accessed, and it should not be used for other needs of the application.</span></span> <span data-ttu-id="80907-181">Таблицы расположены в специальной схеме с именем **__ShardManagement**.</span><span class="sxs-lookup"><span data-stu-id="80907-181">The tables are in a special schema named **__ShardManagement**.</span></span> 
2. <span data-ttu-id="80907-182">**Локальная карта сегментов (LSM)**: в каждую указанную вами в качестве сегмента базу данных будут добавлены несколько небольших таблиц и специальных хранимых процедур, которые содержат информацию о карте сегментов, относящуюся к этому сегменту, и управляют этой информацией.</span><span class="sxs-lookup"><span data-stu-id="80907-182">**Local Shard Map (LSM)**: Every database that you specify to be a shard is modified to contain several small tables and special stored procedures that contain and manage shard map information specific to that shard.</span></span> <span data-ttu-id="80907-183">Эта информация является избыточной для информации, размещенной в глобальной карте сегментов, и позволяет приложению проверять кэшированные данные карты сегментов без нагрузки на глобальную карту сегментов; при помощи локальной карты сегментов приложение проверяет правильность кэшированного сопоставления.</span><span class="sxs-lookup"><span data-stu-id="80907-183">This information is redundant with the information in the GSM, and it allows the application to validate cached shard map information without placing any load on the GSM; the application uses the LSM to determine if a cached mapping is still valid.</span></span> <span data-ttu-id="80907-184">Таблицы, соответствующие локальной карте сегментов в каждом сегменте, также находятся в схеме **__ShardManagement**.</span><span class="sxs-lookup"><span data-stu-id="80907-184">The tables corresponding to the LSM on each shard are also in the schema **__ShardManagement**.</span></span>
3. <span data-ttu-id="80907-185">**Кэш приложения**: каждый экземпляр приложения, у которого есть доступ к объекту **ShardMapManager**, поддерживает локальный кэш своих сопоставлений в памяти.</span><span class="sxs-lookup"><span data-stu-id="80907-185">**Application cache**: Each application instance accessing a **ShardMapManager** object maintains a local in-memory cache of its mappings.</span></span> <span data-ttu-id="80907-186">Хранятся использованные за последнее время сведения о маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="80907-186">It stores routing information that has recently been retrieved.</span></span> 

## <a name="constructing-a-shardmapmanager"></a><span data-ttu-id="80907-187">Создание объекта ShardMapManager</span><span class="sxs-lookup"><span data-stu-id="80907-187">Constructing a ShardMapManager</span></span>
<span data-ttu-id="80907-188">Объект **ShardMapManager** создается с помощью шаблона [фабрики](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) .</span><span class="sxs-lookup"><span data-stu-id="80907-188">A **ShardMapManager** object is constructed using a [factory](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) pattern.</span></span> <span data-ttu-id="80907-189">Метод **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)** принимает учетные данные (включая имя сервера и имя базы данных, содержащей глобальную карту сегментов) в формате строки подключения **ConnectionString** и возвращает экземпляр объекта **ShardMapManager**.</span><span class="sxs-lookup"><span data-stu-id="80907-189">The **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)** method takes credentials (including the server name and database name holding the GSM) in the form of a **ConnectionString** and returns an instance of a **ShardMapManager**.</span></span>  

<span data-ttu-id="80907-190">**Обратите внимание:** экземпляр **ShardMapManager** должен создаваться только один раз для каждого домена приложения в коде инициализации приложения.</span><span class="sxs-lookup"><span data-stu-id="80907-190">**Please Note:** The **ShardMapManager** should be instantiated only once per app domain, within the initialization code for an application.</span></span> <span data-ttu-id="80907-191">Создание дополнительных экземпляров ShardMapManager в том же домене приложения приведет к повышенному потреблению ресурсов памяти и ЦП приложением.</span><span class="sxs-lookup"><span data-stu-id="80907-191">Creation of additional instances of ShardMapManager in the same appdomain, will result in increased memory and CPU utilization of the application.</span></span> <span data-ttu-id="80907-192">**ShardMapManager** может содержать любое число карт сегментов.</span><span class="sxs-lookup"><span data-stu-id="80907-192">A **ShardMapManager** can contain any number of shard maps.</span></span> <span data-ttu-id="80907-193">Многим приложениям достаточно одной карты сегментов, но в некоторых случаях применяются разные наборы баз данных, которые используются в разных схемах или имеют уникальное назначение. В таком случае желательно использовать несколько карт сегментов.</span><span class="sxs-lookup"><span data-stu-id="80907-193">While a single shard map may be sufficient for many applications, there are times when different sets of databases are used for different schema or for unique purposes; in those cases multiple shard maps may be preferable.</span></span> 

<span data-ttu-id="80907-194">В этом коде приложение пытается открыть существующий экземпляр **ShardMapManager** с помощью [метода TryGetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="80907-194">In this code, an application tries to open an existing **ShardMapManager** with the [TryGetSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).</span></span>  <span data-ttu-id="80907-195">Если объекты, представляющие глобальный диспетчер карт **ShardMapManager** (GSM), еще не существуют в базе данных, клиентская библиотека создает их с помощью метода [CreateSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="80907-195">If objects representing a Global **ShardMapManager** (GSM) do not yet exist inside the database, the client library creates them there using the [CreateSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).</span></span>

    // Try to get a reference to the Shard Map Manager 
     // via the Shard Map Manager database.  
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
        // Create the Shard Map Manager. 
        ShardMapManagerFactory.CreateSqlShardMapManager(connectionString);
        Console.WriteLine("Created SqlShardMapManager"); 

        shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager(
            connectionString, 
            ShardMapManagerLoadPolicy.Lazy);

        // The connectionString contains server name, database name, and admin credentials 
        // for privileges on both the GSM and the shards themselves.
    } 

<span data-ttu-id="80907-196">В качестве альтернативы можно использовать PowerShell, чтобы создать новый диспетчер карты сегментов.</span><span class="sxs-lookup"><span data-stu-id="80907-196">As an alternative, you can use Powershell to create a new Shard Map Manager.</span></span> <span data-ttu-id="80907-197">Пример представлен [здесь](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="80907-197">An example is available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

## <a name="get-a-rangeshardmap-or-listshardmap"></a><span data-ttu-id="80907-198">Получение RangeShardMap или ListShardMap</span><span class="sxs-lookup"><span data-stu-id="80907-198">Get a RangeShardMap or ListShardMap</span></span>
<span data-ttu-id="80907-199">После создания диспетчера карты сегментов можно получить объект [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) или [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) с помощью методов [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), [TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx) или [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx).</span><span class="sxs-lookup"><span data-stu-id="80907-199">After creating a shard map manager, you can get the [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) or [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) using the [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), the [TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), or the [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) method.</span></span>

    /// <summary>
    /// Creates a new Range Shard Map with the specified name, or gets the Range Shard Map if it already exists.
    /// </summary>
    public static RangeShardMap<T> CreateOrGetRangeShardMap<T>(ShardMapManager shardMapManager, string shardMapName)
    {
        // Try to get a reference to the Shard Map.
        RangeShardMap<T> shardMap;
        bool shardMapExists = shardMapManager.TryGetRangeShardMap(shardMapName, out shardMap);

        if (shardMapExists)
        {
            ConsoleUtils.WriteInfo("Shard Map {0} already exists", shardMap.Name);
        }
        else
        {
            // The Shard Map does not exist, so create it
            shardMap = shardMapManager.CreateRangeShardMap<T>(shardMapName);
            ConsoleUtils.WriteInfo("Created Shard Map {0}", shardMap.Name);
        }

        return shardMap;
    } 

### <a name="shard-map-administration-credentials"></a><span data-ttu-id="80907-200">Учетные данные для администрирования карты сегментов</span><span class="sxs-lookup"><span data-stu-id="80907-200">Shard map administration credentials</span></span>
<span data-ttu-id="80907-201">Приложения для администрирования и обработки карт сегментов отличаются от приложений, использующих карты сегментов для маршрутизации подключений.</span><span class="sxs-lookup"><span data-stu-id="80907-201">Applications that administer and manipulate shard maps are different from those that use the shard maps to route connections.</span></span> 

<span data-ttu-id="80907-202">Для администрирования карт сегментов (добавления или изменения сегментов, карт сегментов, сопоставлений сегментов и т. д.) необходимо создать экземпляр **ShardMapManager** с использованием **учетных данных, для которых предусмотрены права на чтение и запись в базе GSM и в каждой базе данных, выступающей в качестве сегмента**.</span><span class="sxs-lookup"><span data-stu-id="80907-202">To administer shard maps (add or change shards, shard maps, shard mappings, etc.) you must instantiate the **ShardMapManager** using **credentials that have read/write privileges on both the GSM database and on each database that serves as a shard**.</span></span> <span data-ttu-id="80907-203">Учетные данные должны давать право записи в таблицы в GSM и LSM при вводе или изменения информации карт сегментов, а также право создавать таблицы LSM в новых сегментах.</span><span class="sxs-lookup"><span data-stu-id="80907-203">The credentials must allow for writes against the tables in both the GSM and LSM as shard map information is entered or changed, as well as for creating LSM tables on new shards.</span></span>  

<span data-ttu-id="80907-204">См. статью [Учетные данные для доступа к клиентской библиотеке эластичной базы данных](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="80907-204">See [Credentials used to access the Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span>

### <a name="only-metadata-affected"></a><span data-ttu-id="80907-205">Воздействует только на метаданные</span><span class="sxs-lookup"><span data-stu-id="80907-205">Only metadata affected</span></span>
<span data-ttu-id="80907-206">Методы, используемые для заполнения и изменения данных **ShardMapManager** , не воздействуют на данные пользователя, хранящиеся в самих сегментах.</span><span class="sxs-lookup"><span data-stu-id="80907-206">Methods used for populating or changing the **ShardMapManager** data do not alter the user data stored in the shards themselves.</span></span> <span data-ttu-id="80907-207">Например, такие методы, как **CreateShard**, **DeleteShard**, **UpdateMapping** и другие, влияют только на метаданные карты сегментов.</span><span class="sxs-lookup"><span data-stu-id="80907-207">For example, methods such as **CreateShard**, **DeleteShard**, **UpdateMapping**, etc. affect the shard map metadata only.</span></span> <span data-ttu-id="80907-208">Они не удаляют, не добавляют и не изменяют пользовательские данные, содержащиеся в сегментах.</span><span class="sxs-lookup"><span data-stu-id="80907-208">They do not remove, add, or alter user data contained in the shards.</span></span> <span data-ttu-id="80907-209">На самом деле, эти методы предназначены для использования с отдельными операциями, с помощью которых вы создаете и удаляете фактические базы данных, либо перемещаете строки между сегментами для выравнивания сегментированной среды.</span><span class="sxs-lookup"><span data-stu-id="80907-209">Instead, these methods are designed to be used in conjunction with separate operations you perform to create or remove actual databases, or that move rows from one shard to another to rebalance a sharded environment.</span></span>  <span data-ttu-id="80907-210">(Инструмент **разбиения и объединения**, входящий в состав инструментов эластичных баз данных, использует эти API-интерфейсы и управляет фактическим перемещением данных между сегментами.) (См. статью [Перемещение данных между масштабируемыми облачными базами данных](sql-database-elastic-scale-overview-split-and-merge.md).)</span><span class="sxs-lookup"><span data-stu-id="80907-210">(The **split-merge** tool included with elastic database tools makes use of these APIs along with orchestrating actual data movement between shards.) See [Scaling using the Elastic Database split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md).</span></span>

## <a name="populating-a-shard-map-example"></a><span data-ttu-id="80907-211">Пример заполнения сопоставления сегментов</span><span class="sxs-lookup"><span data-stu-id="80907-211">Populating a shard map example</span></span>
<span data-ttu-id="80907-212">Ниже приведен пример последовательности операций для заполнения конкретной карты сегментов.</span><span class="sxs-lookup"><span data-stu-id="80907-212">An example sequence of operations to populate a specific shard map is shown below.</span></span> <span data-ttu-id="80907-213">Этот код выполняет делает следующее:</span><span class="sxs-lookup"><span data-stu-id="80907-213">The code performs these steps:</span></span> 

1. <span data-ttu-id="80907-214">При помощи диспетчера сопоставления сегментов создается новое сопоставление сегментов.</span><span class="sxs-lookup"><span data-stu-id="80907-214">A new shard map is created within a shard map manager.</span></span> 
2. <span data-ttu-id="80907-215">В сопоставление сегментов добавляются метаданные двух разных сегментов.</span><span class="sxs-lookup"><span data-stu-id="80907-215">The metadata for two different shards is added to the shard map.</span></span> 
3. <span data-ttu-id="80907-216">Добавляется ряд сопоставлений диапазонов ключей, отображается все содержимое сопоставление сегментов.</span><span class="sxs-lookup"><span data-stu-id="80907-216">A variety of key range mappings are added, and the overall contents of the shard map are displayed.</span></span> 

<span data-ttu-id="80907-217">Код написан таким образом, что при возникновении ошибки метод может быть перезапущен.</span><span class="sxs-lookup"><span data-stu-id="80907-217">The code is written so that the method can be rerun if an error occurs.</span></span> <span data-ttu-id="80907-218">Каждый запрос проверяет наличие такого сегмента или сопоставления, прежде чем создавать его.</span><span class="sxs-lookup"><span data-stu-id="80907-218">Each request tests whether a shard or mapping already exists, before attempting to create it.</span></span> <span data-ttu-id="80907-219">В следующем примере кода предполагается, что базы данных с именами **sample_shard_0**, **sample_shard_1** и **sample_shard_2** уже созданы на сервере, на который ссылается строка **shardServer**.</span><span class="sxs-lookup"><span data-stu-id="80907-219">The code assumes that databases named **sample_shard_0**, **sample_shard_1** and **sample_shard_2** have already been created in the server referenced by string **shardServer**.</span></span> 

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

            // List the shards and mappings 
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

<span data-ttu-id="80907-220">В качестве альтернативы для достижения такого же результата можно использовать скрипты PowerShell.</span><span class="sxs-lookup"><span data-stu-id="80907-220">As an alternative you can use PowerShell scripts to achieve the same result.</span></span> <span data-ttu-id="80907-221">Некоторые примеры PowerShell доступны [здесь](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="80907-221">Some of the sample PowerShell examples are available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>     

<span data-ttu-id="80907-222">После заполнения карт сегментов можно создавать приложения для доступа к данным, либо приспособить для работы с этими картами существующие приложения.</span><span class="sxs-lookup"><span data-stu-id="80907-222">Once shard maps have been populated, data access applications can be created or adapted to work with the maps.</span></span> <span data-ttu-id="80907-223">Заполнение карт и управление ими не выполняется до того момента, когда необходимо будет изменить **макет карты** .</span><span class="sxs-lookup"><span data-stu-id="80907-223">Populating or manipulating the maps need not occur again until **map layout** needs to change.</span></span>  

## <a name="data-dependent-routing"></a><span data-ttu-id="80907-224">Маршрутизация, зависящая от данных</span><span class="sxs-lookup"><span data-stu-id="80907-224">Data dependent routing</span></span>
<span data-ttu-id="80907-225">Диспетчер карт сегментов чаще всего используется приложениями, которым требуются подключения к базам данных для выполнения операций с данными конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="80907-225">The shard map manager will be most used in applications that require database connections to perform the app-specific data operations.</span></span> <span data-ttu-id="80907-226">Эти подключения необходимо связать с нужной базой данных.</span><span class="sxs-lookup"><span data-stu-id="80907-226">Those connections must be associated with the correct database.</span></span> <span data-ttu-id="80907-227">Это называется **маршрутизацией, зависимой от данных**.</span><span class="sxs-lookup"><span data-stu-id="80907-227">This is known as **Data Dependent Routing**.</span></span> <span data-ttu-id="80907-228">Для таких приложений необходимо объявить объект диспетчера карт сегментов в фабричном режиме, пользуясь учетными данными с доступом к базе данных GSM только для чтения.</span><span class="sxs-lookup"><span data-stu-id="80907-228">For these applications, instantiate a shard map manager object from the factory using credentials that have read-only access on the GSM database.</span></span> <span data-ttu-id="80907-229">Учетные данные для подключения к нужной базе данных сегментов впоследствии будут передаваться в отдельных запросах подключения.</span><span class="sxs-lookup"><span data-stu-id="80907-229">Individual requests for later connections supply credentials necessary for connecting to the appropriate shard database.</span></span>

<span data-ttu-id="80907-230">Обратите внимание, что эти приложения (использующие **ShardMapManager** в режиме только для чтения) не могут вносить изменения в карты и сопоставления.</span><span class="sxs-lookup"><span data-stu-id="80907-230">Note that these applications (using **ShardMapManager** opened with read-only credentials) cannot make changes to the maps or mappings.</span></span> <span data-ttu-id="80907-231">Для этого создайте специальные административные приложения или сценарии PowerShell, которые будут передавать учетные данные с более высокими правами доступа, как об этом говорилось ранее.</span><span class="sxs-lookup"><span data-stu-id="80907-231">For those needs, create administrative-specific applications or PowerShell scripts that supply higher-privileged credentials as discussed earlier.</span></span> <span data-ttu-id="80907-232">См. статью [Учетные данные для доступа к клиентской библиотеке эластичной базы данных](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="80907-232">See [Credentials used to access the Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span>

<span data-ttu-id="80907-233">Дополнительные сведения см. в статье [Маршрутизация, зависящая от данных](sql-database-elastic-scale-data-dependent-routing.md).</span><span class="sxs-lookup"><span data-stu-id="80907-233">For more details, see [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> 

## <a name="modifying-a-shard-map"></a><span data-ttu-id="80907-234">Изменение карты сегментов</span><span class="sxs-lookup"><span data-stu-id="80907-234">Modifying a shard map</span></span>
<span data-ttu-id="80907-235">Карту сегментов можно изменять различными способами.</span><span class="sxs-lookup"><span data-stu-id="80907-235">A shard map can be changed in different ways.</span></span> <span data-ttu-id="80907-236">Любым из приведенных способов можно изменить метаданные сегментов и сопоставления сегментов, но нельзя изменить данные самих сегментов, создать или удалить базу данных.</span><span class="sxs-lookup"><span data-stu-id="80907-236">All of the following methods modify the metadata describing the shards and their mappings, but they do not physically modify data within the shards, nor do they create or delete the actual databases.</span></span>  <span data-ttu-id="80907-237">Некоторые из описанных ниже операций над сопоставлениями сегментов необходимо выполнять согласованно с административными действиями для физического перемещения данных, добавления и удаления баз данных, выступающих в качестве сегментов.</span><span class="sxs-lookup"><span data-stu-id="80907-237">Some of the operations on the shard map described below may need to be coordinated with administrative actions that physically move data or that add and remove databases serving as shards.</span></span>

<span data-ttu-id="80907-238">Эти методы работают совместно, как строительные блоки, доступные для изменения общего распределения данных в среде сегментированной базы данных.</span><span class="sxs-lookup"><span data-stu-id="80907-238">These methods work together as the building blocks available for modifying the overall distribution of data in your sharded database environment.</span></span>  

* <span data-ttu-id="80907-239">Для добавления или удаления сегментов используйте методы **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)** и **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)** в классе [Shardmap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx).</span><span class="sxs-lookup"><span data-stu-id="80907-239">To add or remove shards: use **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)** and **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)** of the [Shardmap class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx).</span></span> 
  
    <span data-ttu-id="80907-240">Для успешного выполнения этих операций необходимо указать существующие сервер и базу данных, которая играет роль целевого сегмента.</span><span class="sxs-lookup"><span data-stu-id="80907-240">The server and database representing the target shard must already exist for these operations to execute.</span></span> <span data-ttu-id="80907-241">Эти методы не изменяют сами базы данных, они изменяют только метаданные в сопоставлении сегментов.</span><span class="sxs-lookup"><span data-stu-id="80907-241">These methods do not have any impact on the databases themselves, only on metadata in the shard map.</span></span>
* <span data-ttu-id="80907-242">Для создания или удаления точек или диапазонов, сопоставляемых с сегментами, используйте методы **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)** и **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)** класса [RangeShardMapping](https://msdn.microsoft.com/library/azure/dn807318.aspx) и метод **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)** класса [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx).</span><span class="sxs-lookup"><span data-stu-id="80907-242">To create or remove points or ranges that are mapped to the shards: use **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**, **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)** of the [RangeShardMapping class](https://msdn.microsoft.com/library/azure/dn807318.aspx), and **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)** of the [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)</span></span>
  
    <span data-ttu-id="80907-243">Один сегмент может быть сопоставлен со множеством разных точек или диапазонов.</span><span class="sxs-lookup"><span data-stu-id="80907-243">Many different points or ranges can be mapped to the same shard.</span></span> <span data-ttu-id="80907-244">Эти методы изменяют только метаданные, но не изменяют данные, хранящиеся в сегментах.</span><span class="sxs-lookup"><span data-stu-id="80907-244">These methods only affect metadata - they do not affect any data that may already be present in shards.</span></span> <span data-ttu-id="80907-245">Если для обеспечения согласованности с операциями **DeleteMapping** требуется удалить данные из базы данных, необходимо будет выполнить операции удаления отдельно, но с использованием этих методов.</span><span class="sxs-lookup"><span data-stu-id="80907-245">If data needs to be removed from the database in order to be consistent with **DeleteMapping** operations, you will need to perform those operations separately but in conjunction with using these methods.</span></span>  
* <span data-ttu-id="80907-246">Чтобы разбить имеющийся диапазон на два или объединить смежные диапазоны в один, используйте методы **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)** и **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="80907-246">To split existing ranges into two, or merge adjacent ranges into one: use **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)** and **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.</span></span>  
  
    <span data-ttu-id="80907-247">Обратите внимание, что операции разбиения и слияния **не изменяют сегмент, с которым сопоставляются ключевые значения**.</span><span class="sxs-lookup"><span data-stu-id="80907-247">Note that split and merge operations **do not change the shard to which key values are mapped**.</span></span> <span data-ttu-id="80907-248">Функция разбиения разделяет существующий диапазон на две части, но оставляет их обе привязанными к одному сегменту.</span><span class="sxs-lookup"><span data-stu-id="80907-248">A split breaks an existing range into two parts, but leaves both as mapped to the same shard.</span></span> <span data-ttu-id="80907-249">Функция объединения соединяет два соседних диапазона, привязанных к одному сегменту, в один целый диапазон.</span><span class="sxs-lookup"><span data-stu-id="80907-249">A merge operates on two adjacent ranges that are already mapped to the same shard, coalescing them into a single range.</span></span>  <span data-ttu-id="80907-250">Перемещение точек или самих диапазонов между сегментами необходимо координировать с помощью **UpdateMapping** в сочетании с фактическим перемещением данных.</span><span class="sxs-lookup"><span data-stu-id="80907-250">The movement of points or ranges themselves between shards needs to be coordinated by using **UpdateMapping** in conjunction with actual data movement.</span></span>  <span data-ttu-id="80907-251">Для координации изменений в карте сегментов с перемещением данных можно использовать службу **разбиения и слияния** , входящую в состав средств для работы с эластичными базами данных.</span><span class="sxs-lookup"><span data-stu-id="80907-251">You can use the **Split/Merge** service that is part of elastic database tools to coordinate shard map changes with data movement, when movement is needed.</span></span> 
* <span data-ttu-id="80907-252">Для повторного сопоставления (или перемещения) отдельных точек или диапазонов в другие сегменты используйте метод **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="80907-252">To re-map (or move) individual points or ranges to different shards: use **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.</span></span>  
  
    <span data-ttu-id="80907-253">Так как данные придется перемещать из одного сегмента в другой для согласования с операциями **UpdateMapping** , перемещение нужно выполнить отдельно, но с использованием этих методов.</span><span class="sxs-lookup"><span data-stu-id="80907-253">Since data may need to be moved from one shard to another in order to be consistent with **UpdateMapping** operations, you will need to perform that movement separately but in conjunction with using these methods.</span></span>
* <span data-ttu-id="80907-254">Для перевода сопоставлений в сетевой и автономный режим используйте методы **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)** и **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)**. Последний метод также используется для управления сетевым состоянием сопоставления.</span><span class="sxs-lookup"><span data-stu-id="80907-254">To take mappings online and offline: use **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)** and **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)** to control the online state of a mapping.</span></span> 
  
    <span data-ttu-id="80907-255">Определенные операции для сопоставлений сегментов, включая **UpdateMapping** и **DeleteMapping**, могут выполняться только в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="80907-255">Certain operations on shard mappings are only allowed when a mapping is in an “offline” state, including **UpdateMapping** and **DeleteMapping**.</span></span> <span data-ttu-id="80907-256">Если сопоставление находится в автономном режиме, то запрос данных с ключом, указывающим на это сопоставление, возвратит ошибку.</span><span class="sxs-lookup"><span data-stu-id="80907-256">When a mapping is offline, a data-dependent request based on a key included in that mapping will return an error.</span></span> <span data-ttu-id="80907-257">Кроме того, при первом переходе диапазона в автономный режим все соединения с соответствующим сегментом автоматически разрываются с целью предотвращения сбоев и обрыва результатов запросов, направленных на изменяемые диапазоны.</span><span class="sxs-lookup"><span data-stu-id="80907-257">In addition, when a range is first taken offline, all connections to the affected shard are automatically killed in order to prevent inconsistent or incomplete results for queries directed against ranges being changed.</span></span> 

<span data-ttu-id="80907-258">Сопоставления являются неизменяемыми объектами в .net.</span><span class="sxs-lookup"><span data-stu-id="80907-258">Mappings are immutable objects in .Net.</span></span>  <span data-ttu-id="80907-259">Все описанные выше методы, изменяющие сопоставление, также проверяют все ссылки на них в коде.</span><span class="sxs-lookup"><span data-stu-id="80907-259">All of the methods above that change mappings also invalidate any references to them in your code.</span></span> <span data-ttu-id="80907-260">Для облегчения выполнения последовательности операций, изменяющих состояние сопоставления, все методы, изменяющие сопоставление, возвращают новую ссылку сопоставления, так что операции могут быть объединены в цепочку.</span><span class="sxs-lookup"><span data-stu-id="80907-260">To make it easier to perform sequences of operations that change a mapping’s state, all of the methods that change a mapping return a new mapping reference, so operations can be chained.</span></span> <span data-ttu-id="80907-261">Например, для удаления существующего сопоставления в sm shardmap, содержащего ключ 25, можно выполнить следующее:</span><span class="sxs-lookup"><span data-stu-id="80907-261">For example, to delete an existing mapping in shardmap sm that contains the key 25, you can execute the following:</span></span> 

        sm.DeleteMapping(sm.MarkMappingOffline(sm.GetMappingForKey(25)));

## <a name="adding-a-shard"></a><span data-ttu-id="80907-262">Добавление сегмента</span><span class="sxs-lookup"><span data-stu-id="80907-262">Adding a shard</span></span>
<span data-ttu-id="80907-263">Часто необходимо, чтобы приложение просто добавило в существующую карту сегментов новые сегменты для обработки данных, поступление которых ожидается из новых ключей и диапазонов ключей.</span><span class="sxs-lookup"><span data-stu-id="80907-263">Applications often need to simply add new shards to handle data that is expected from new keys or key ranges, for a shard map that already exists.</span></span> <span data-ttu-id="80907-264">Например, приложение с сегментированием по идентификатору клиента должно подготовить новый сегмент для нового клиента или при обработке данных с сегментированием по месяцам требуется создание нового сегмента перед началом следующего месяца.</span><span class="sxs-lookup"><span data-stu-id="80907-264">For example, an application sharded by Tenant ID may need to provision a new shard for a new tenant, or data sharded monthly may need a new shard provisioned before the start of each new month.</span></span> 

<span data-ttu-id="80907-265">Если новый диапазон ключей не входит в существующую карту и нет необходимости перемещения данных, добавление сегментов и привязка к нему нового ключа или диапазона становится довольно простой задачей.</span><span class="sxs-lookup"><span data-stu-id="80907-265">If the new range of key values is not already part of an existing mapping and no data movement is necessary, it is very simple to add the new shard and associate the new key or range to that shard.</span></span> <span data-ttu-id="80907-266">Дополнительные сведения о добавлении новых сегментов см. в статье [Добавление сегмента с использованием средств эластичных баз данных](sql-database-elastic-scale-add-a-shard.md).</span><span class="sxs-lookup"><span data-stu-id="80907-266">For details on adding new shards, see [Adding a new shard](sql-database-elastic-scale-add-a-shard.md).</span></span>

<span data-ttu-id="80907-267">Однако для случая, когда требуется перемещение данных, необходимо использовать инструмент разбиения и объединения для выполнения перемещения данных между сегментами в сочетании с необходимым обновлением карты сегментов.</span><span class="sxs-lookup"><span data-stu-id="80907-267">For scenarios that require data movement, however, the split-merge tool is needed to orchestrate the data movement between shards in combination with the necessary shard map updates.</span></span> <span data-ttu-id="80907-268">Сведения об использовании средства разбиения и слияния см. в статье [Перемещение данных между масштабируемыми облачными базами данных](sql-database-elastic-scale-overview-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="80907-268">For details on using the split-merge yool, see [Overview of split-merge](sql-database-elastic-scale-overview-split-and-merge.md)</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-shard-map-management/listmapping.png
[2]: ./media/sql-database-elastic-scale-shard-map-management/rangemapping.png
[3]: ./media/sql-database-elastic-scale-shard-map-management/multipleonsingledb.png
