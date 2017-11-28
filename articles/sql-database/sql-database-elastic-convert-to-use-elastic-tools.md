---
title: "Перенос имеющихся баз данных для масштабирования | Документация Майкрософт"
description: "Преобразование сегментированных баз данных для использования средств эластичной базы данных путем создания диспетчера сопоставления сегментов"
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 8c851d8e-8fd5-4327-89c1-9178b20ddd69
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 099f40d00753b7c86ba726a818f17d440a125221
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-existing-databases-to-scale-out"></a><span data-ttu-id="9b37f-103">Перенос существующих баз данных для масштабирования</span><span class="sxs-lookup"><span data-stu-id="9b37f-103">Migrate existing databases to scale-out</span></span>
<span data-ttu-id="9b37f-104">Вы можете легко управлять существующими масштабируемыми сегментированными базами данных с помощью средств базы данных SQL Azure (таких как [клиентская библиотека для эластичных баз данных](sql-database-elastic-database-client-library.md)).</span><span class="sxs-lookup"><span data-stu-id="9b37f-104">Easily manage your existing scaled-out sharded databases using Azure SQL Database database tools (such as the [Elastic Database client library](sql-database-elastic-database-client-library.md)).</span></span> <span data-ttu-id="9b37f-105">Для использования [диспетчера карты сегментов](sql-database-elastic-scale-shard-map-management.md)следует сначала преобразовать существующий набор баз данных.</span><span class="sxs-lookup"><span data-stu-id="9b37f-105">You must first convert an existing set of databases to use the [shard map manager](sql-database-elastic-scale-shard-map-management.md).</span></span> 

## <a name="overview"></a><span data-ttu-id="9b37f-106">Обзор</span><span class="sxs-lookup"><span data-stu-id="9b37f-106">Overview</span></span>
<span data-ttu-id="9b37f-107">Для переноса существующей сегментированной базы данных выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9b37f-107">To migrate an existing sharded database:</span></span> 

1. <span data-ttu-id="9b37f-108">Подготовка [базы данных диспетчера карты сегментов](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="9b37f-108">Prepare the [shard map manager database](sql-database-elastic-scale-shard-map-management.md).</span></span>
2. <span data-ttu-id="9b37f-109">Создание карты сегментов.</span><span class="sxs-lookup"><span data-stu-id="9b37f-109">Create the shard map.</span></span>
3. <span data-ttu-id="9b37f-110">Подготовка отдельных сегментов.</span><span class="sxs-lookup"><span data-stu-id="9b37f-110">Prepare the individual shards.</span></span>  
4. <span data-ttu-id="9b37f-111">Добавление сопоставлений на карту сегментов.</span><span class="sxs-lookup"><span data-stu-id="9b37f-111">Add mappings to the shard map.</span></span>

<span data-ttu-id="9b37f-112">Эти методы можно реализовать с помощью [клиентской библиотеки .NET Framework](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) или сценариев PowerShell, которые можно найти на странице [Azure SQL DB — Elastic Database tools scripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db) (База данных SQL Azure — сценарии для инструментов эластичной базы данных).</span><span class="sxs-lookup"><span data-stu-id="9b37f-112">These techniques can be implemented using either the [.NET Framework client library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), or the PowerShell scripts found at [Azure SQL DB - Elastic Database tools scripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span> <span data-ttu-id="9b37f-113">В приведенных здесь примерах используются скрипты PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9b37f-113">The examples here use the PowerShell scripts.</span></span>

<span data-ttu-id="9b37f-114">Чтобы больше узнать о ShardMapManager, ознакомьтесь с [управлением картами сегментов](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="9b37f-114">For more information about the ShardMapManager, see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="9b37f-115">Общие сведения об инструментах эластичной базы данных см. в [обзоре возможностей эластичных баз данных](sql-database-elastic-scale-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9b37f-115">For an overview of the elastic database tools, see [Elastic Database features overview](sql-database-elastic-scale-introduction.md).</span></span>

## <a name="prepare-the-shard-map-manager-database"></a><span data-ttu-id="9b37f-116">Подготовка базы данных диспетчера карты сегментов</span><span class="sxs-lookup"><span data-stu-id="9b37f-116">Prepare the shard map manager database</span></span>
<span data-ttu-id="9b37f-117">Диспетчер карты сегментов — это специальная база данных, хранящая данные для управления масштабируемыми базами данных.</span><span class="sxs-lookup"><span data-stu-id="9b37f-117">The shard map manager is a special database that contains the data to manage scaled-out databases.</span></span> <span data-ttu-id="9b37f-118">Можно использовать существующую базу данных или создать новую.</span><span class="sxs-lookup"><span data-stu-id="9b37f-118">You can use an existing database, or create a new database.</span></span> <span data-ttu-id="9b37f-119">Обратите внимание, что для диспетчера карты сегментов и для сегмента следует использовать разные базы данных.</span><span class="sxs-lookup"><span data-stu-id="9b37f-119">Note that a database acting as shard map manager should not be the same database as a shard.</span></span> <span data-ttu-id="9b37f-120">Также помните, что скрипт PowerShell не создает базу данных.</span><span class="sxs-lookup"><span data-stu-id="9b37f-120">Also note that the PowerShell script does not create the database for you.</span></span> 

## <a name="step-1-create-a-shard-map-manager"></a><span data-ttu-id="9b37f-121">Шаг 1. Создание диспетчера сопоставления сегментов</span><span class="sxs-lookup"><span data-stu-id="9b37f-121">Step 1: create a shard map manager</span></span>
    # Create a shard map manager. 
    New-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 
    #<server_name> and <smm_db_name> are the server name and database name 
    # for the new or existing database that should be used for storing 
    # tenant-database mapping information.

### <a name="to-retrieve-the-shard-map-manager"></a><span data-ttu-id="9b37f-122">Извлечение диспетчера сопоставления сегментов</span><span class="sxs-lookup"><span data-stu-id="9b37f-122">To retrieve the shard map manager</span></span>
<span data-ttu-id="9b37f-123">Созданный диспетчер сопоставления сегментов можно извлечь с помощью этого командлета.</span><span class="sxs-lookup"><span data-stu-id="9b37f-123">After creation, you can retrieve the shard map manager with this cmdlet.</span></span> <span data-ttu-id="9b37f-124">Этот шаг требуется выполнять при каждом использовании объекта ShardMapManager.</span><span class="sxs-lookup"><span data-stu-id="9b37f-124">This step is needed every time you need to use the ShardMapManager object.</span></span>

    # Try to get a reference to the Shard Map Manager  
    $ShardMapManager = Get-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 


## <a name="step-2-create-the-shard-map"></a><span data-ttu-id="9b37f-125">Шаг 2. Создание карты сегментов</span><span class="sxs-lookup"><span data-stu-id="9b37f-125">Step 2: create the shard map</span></span>
<span data-ttu-id="9b37f-126">Следует выбрать тип создаваемой карты сегментов.</span><span class="sxs-lookup"><span data-stu-id="9b37f-126">You must select the type of shard map to create.</span></span> <span data-ttu-id="9b37f-127">Этот выбор зависит от архитектуры базы данных.</span><span class="sxs-lookup"><span data-stu-id="9b37f-127">The choice depends on the database architecture:</span></span> 

1. <span data-ttu-id="9b37f-128">Один клиент на базу данных (определения терминов см. в [глоссарии](sql-database-elastic-scale-glossary.md)).</span><span class="sxs-lookup"><span data-stu-id="9b37f-128">Single tenant per database (For terms, see the [glossary](sql-database-elastic-scale-glossary.md).)</span></span> 
2. <span data-ttu-id="9b37f-129">Несколько клиентов на одну базу данных (два типа):</span><span class="sxs-lookup"><span data-stu-id="9b37f-129">Multiple tenants per database (two types):</span></span>
   1. <span data-ttu-id="9b37f-130">Сопоставление по спискам</span><span class="sxs-lookup"><span data-stu-id="9b37f-130">List mapping</span></span>
   2. <span data-ttu-id="9b37f-131">Сопоставление по диапазонам</span><span class="sxs-lookup"><span data-stu-id="9b37f-131">Range mapping</span></span>

<span data-ttu-id="9b37f-132">Для модели с одним клиентом создайте карту сегментов с **сопоставлением по списку** .</span><span class="sxs-lookup"><span data-stu-id="9b37f-132">For a single-tenant model, create a **list mapping** shard map.</span></span> <span data-ttu-id="9b37f-133">В модели с одним клиентом каждому клиенту назначается по одной базе данных.</span><span class="sxs-lookup"><span data-stu-id="9b37f-133">The single-tenant model assigns one database per tenant.</span></span> <span data-ttu-id="9b37f-134">Эта модель подходит для разработчиков SaaS, так как она упрощает управление.</span><span class="sxs-lookup"><span data-stu-id="9b37f-134">This is an effective model for SaaS developers as it simplifies management.</span></span>

![Сопоставление по спискам][1]

<span data-ttu-id="9b37f-136">В модели базы данных с несколькими клиентами для одной базы данных назначается несколько клиентов (а группы клиентов можно распределять по нескольким базам данных).</span><span class="sxs-lookup"><span data-stu-id="9b37f-136">The multi-tenant model assigns several tenants to a single database (and you can distribute groups of tenants across multiple databases).</span></span> <span data-ttu-id="9b37f-137">Эту модель можно использовать, когда у каждого отдельного клиента низкие потребности в обработке данных.</span><span class="sxs-lookup"><span data-stu-id="9b37f-137">Use this model when you expect each tenant to have small data needs.</span></span> <span data-ttu-id="9b37f-138">В этой модели клиенты соотносятся с базой данных с использованием **сопоставления по диапазонам**.</span><span class="sxs-lookup"><span data-stu-id="9b37f-138">In this model, we assign a range of tenants to a database using **range mapping**.</span></span> 

![Сопоставление по диапазонам][2]

<span data-ttu-id="9b37f-140">Вы можете также реализовать модель с несколькими клиентами с помощью *сопоставления по списку* , в котором одной базе данных соответствует несколько клиентов.</span><span class="sxs-lookup"><span data-stu-id="9b37f-140">Or you can implement a multi-tenant database model using a *list mapping* to assign multiple tenants to a single database.</span></span> <span data-ttu-id="9b37f-141">Например, база данных DB1 используется для хранения информации о клиенте 1 и 5, а DB2 хранит данные о клиенте 7 и 10.</span><span class="sxs-lookup"><span data-stu-id="9b37f-141">For example, DB1 is used to store information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span></span> 

![Несколько клиентов для одной базы данных][3] 

<span data-ttu-id="9b37f-143">**Выберите один из вариантов, соответствующий вашему выбору.**</span><span class="sxs-lookup"><span data-stu-id="9b37f-143">**Based on your choice, choose one of these options:**</span></span>

### <a name="option-1-create-a-shard-map-for-a-list-mapping"></a><span data-ttu-id="9b37f-144">Вариант 1. Создание карты сегментов для сопоставления по списку</span><span class="sxs-lookup"><span data-stu-id="9b37f-144">Option 1: create a shard map for a list mapping</span></span>
<span data-ttu-id="9b37f-145">Создайте карту сегментов, используя объект ShardMapManager.</span><span class="sxs-lookup"><span data-stu-id="9b37f-145">Create a shard map using the ShardMapManager object.</span></span> 

    # $ShardMapManager is the shard map manager object. 
    $ShardMap = New-ListShardMap -KeyType $([int]) 
    -ListShardMapName 'ListShardMap' 
    -ShardMapManager $ShardMapManager 


### <a name="option-2-create-a-shard-map-for-a-range-mapping"></a><span data-ttu-id="9b37f-146">Вариант 2. Создание карты сегментов для сопоставления по диапазонам</span><span class="sxs-lookup"><span data-stu-id="9b37f-146">Option 2: create a shard map for a range mapping</span></span>
<span data-ttu-id="9b37f-147">Обратите внимание, что для использования этого шаблона сопоставления потребуются непрерывные диапазоны значений идентификаторов клиентов. Кроме того, можно не включать все диапазоны и просто пропустить один из них при создании базы данных.</span><span class="sxs-lookup"><span data-stu-id="9b37f-147">Note that to utilize this mapping pattern, tenant id values needs to be continuous ranges, and it is acceptable to have gap in the ranges by simply skipping the range when creating the databases.</span></span>

    # $ShardMapManager is the shard map manager object 
    # 'RangeShardMap' is the unique identifier for the range shard map.  
    $ShardMap = New-RangeShardMap 
    -KeyType $([int]) 
    -RangeShardMapName 'RangeShardMap' 
    -ShardMapManager $ShardMapManager 

### <a name="option-3-list-mappings-on-a-single-database"></a><span data-ttu-id="9b37f-148">Вариант 3. Сопоставление по списку для одной базы данных</span><span class="sxs-lookup"><span data-stu-id="9b37f-148">Option 3: List mappings on a single database</span></span>
<span data-ttu-id="9b37f-149">Для настройки этого шаблона также требуется создать карту списков, как показано в разделе "Шаг 2, вариант 1".</span><span class="sxs-lookup"><span data-stu-id="9b37f-149">Setting up this pattern also requires creation of a list map as shown in step 2, option 1.</span></span>

## <a name="step-3-prepare-individual-shards"></a><span data-ttu-id="9b37f-150">Шаг 3. Подготовка отдельных сегментов</span><span class="sxs-lookup"><span data-stu-id="9b37f-150">Step 3: Prepare individual shards</span></span>
<span data-ttu-id="9b37f-151">Добавьте каждый сегмент (база данных) в диспетчер сопоставления сегментов.</span><span class="sxs-lookup"><span data-stu-id="9b37f-151">Add each shard (database) to the shard map manager.</span></span> <span data-ttu-id="9b37f-152">Таким образом отдельные базы данных будут подготовлены для хранения сведений о сопоставлении.</span><span class="sxs-lookup"><span data-stu-id="9b37f-152">This prepares the individual databases for storing mapping information.</span></span> <span data-ttu-id="9b37f-153">Подготовьте так каждый сегмент.</span><span class="sxs-lookup"><span data-stu-id="9b37f-153">Execute this method on each shard.</span></span>

    Add-Shard 
    -ShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>'
    # The $ShardMap is the shard map created in step 2.


## <a name="step-4-add-mappings"></a><span data-ttu-id="9b37f-154">Шаг 4. Добавление сопоставлений</span><span class="sxs-lookup"><span data-stu-id="9b37f-154">Step 4: Add mappings</span></span>
<span data-ttu-id="9b37f-155">Добавление сопоставлений зависит от вида созданной карты сегментов.</span><span class="sxs-lookup"><span data-stu-id="9b37f-155">The addition of mappings depends on the kind of shard map you created.</span></span> <span data-ttu-id="9b37f-156">Если создана карта списков, нужно добавить сопоставления по спискам.</span><span class="sxs-lookup"><span data-stu-id="9b37f-156">If you created a list map, you add list mappings.</span></span> <span data-ttu-id="9b37f-157">Если создана карта диапазонов, нужно добавить сопоставления по диапазонам.</span><span class="sxs-lookup"><span data-stu-id="9b37f-157">If you created a range map, you add range mappings.</span></span>

### <a name="option-1-map-the-data-for-a-list-mapping"></a><span data-ttu-id="9b37f-158">Вариант 1. Сопоставление данных для сопоставления по списку</span><span class="sxs-lookup"><span data-stu-id="9b37f-158">Option 1: map the data for a list mapping</span></span>
<span data-ttu-id="9b37f-159">Сопоставьте данные, добавив сопоставление по спискам для каждого клиента.</span><span class="sxs-lookup"><span data-stu-id="9b37f-159">Map the data by adding a list mapping for each tenant.</span></span>  

    # Create the mappings and associate it with the new shards 
    Add-ListMapping 
    -KeyType $([int]) 
    -ListPoint '<tenant_id>' 
    -ListShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 

### <a name="option-2-map-the-data-for-a-range-mapping"></a><span data-ttu-id="9b37f-160">Вариант 2. Сопоставление данных для сопоставления по диапазонам</span><span class="sxs-lookup"><span data-stu-id="9b37f-160">Option 2: map the data for a range mapping</span></span>
<span data-ttu-id="9b37f-161">Добавьте сопоставления по диапазонам для всех связанных диапазонов идентификаторов клиентов и баз данных:</span><span class="sxs-lookup"><span data-stu-id="9b37f-161">Add the range mappings for all the tenant id range - database associations:</span></span>

    # Create the mappings and associate it with the new shards 
    Add-RangeMapping 
    -KeyType $([int]) 
    -RangeHigh '5' 
    -RangeLow '1' 
    -RangeShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 


### <a name="step-4-option-3-map-the-data-for-multiple-tenants-on-a-single-database"></a><span data-ttu-id="9b37f-162">Шаг 4, вариант 3. Сопоставление данных для нескольких клиентов в одной базе данных</span><span class="sxs-lookup"><span data-stu-id="9b37f-162">Step 4 option 3: map the data for multiple tenants on a single database</span></span>
<span data-ttu-id="9b37f-163">Для каждого клиента следует выполнить функцию Add-ListMapping (вариант 1 выше).</span><span class="sxs-lookup"><span data-stu-id="9b37f-163">For each tenant, run the Add-ListMapping (option 1, above).</span></span> 

## <a name="checking-the-mappings"></a><span data-ttu-id="9b37f-164">Проверка сопоставлений</span><span class="sxs-lookup"><span data-stu-id="9b37f-164">Checking the mappings</span></span>
<span data-ttu-id="9b37f-165">Сведения о существующих сегментах и сопоставлениях, связанных с ними, можно запросить с помощью следующих команд:</span><span class="sxs-lookup"><span data-stu-id="9b37f-165">Information about the existing shards and the mappings associated with them can be queried using following commands:</span></span>  

    # List the shards and mappings 
    Get-Shards -ShardMap $ShardMap 
    Get-Mappings -ShardMap $ShardMap 

## <a name="summary"></a><span data-ttu-id="9b37f-166">Резюме</span><span class="sxs-lookup"><span data-stu-id="9b37f-166">Summary</span></span>
<span data-ttu-id="9b37f-167">После завершения настройки можно начать работу с клиентской библиотекой эластичной базы данных.</span><span class="sxs-lookup"><span data-stu-id="9b37f-167">Once you have completed the setup, you can begin to use the Elastic Database client library.</span></span> <span data-ttu-id="9b37f-168">Кроме того, можно воспользоваться [маршрутизацией, зависящей от данных](sql-database-elastic-scale-data-dependent-routing.md), и [формированием многосегментных запросов](sql-database-elastic-scale-multishard-querying.md).</span><span class="sxs-lookup"><span data-stu-id="9b37f-168">You can also use [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) and [multi-shard query](sql-database-elastic-scale-multishard-querying.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b37f-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9b37f-169">Next steps</span></span>
<span data-ttu-id="9b37f-170">Скачайте скрипты PowerShell на странице [Azure SQL DB-Elastic Database tools scripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db)(База данных SQL Azure — скрипты для средств эластичной базы данных).</span><span class="sxs-lookup"><span data-stu-id="9b37f-170">Get the PowerShell scripts from [Azure SQL DB-Elastic Database tools sripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

<span data-ttu-id="9b37f-171">Средства также доступны на сайте GitHub: [Azure/elastic-db-tools](https://github.com/Azure/elastic-db-tools).</span><span class="sxs-lookup"><span data-stu-id="9b37f-171">The tools are also on GitHub: [Azure/elastic-db-tools](https://github.com/Azure/elastic-db-tools).</span></span>

<span data-ttu-id="9b37f-172">Используйте средство разбиения и слияния для перемещения данных из модели с несколькими клиентами в модель с одним клиентом и наоборот.</span><span class="sxs-lookup"><span data-stu-id="9b37f-172">Use the split-merge tool to move data to or from a multi-tenant model to a single tenant model.</span></span> <span data-ttu-id="9b37f-173">Ознакомьтесь со статьей о [средстве разбиения и объединения](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9b37f-173">See [Split merge tool](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9b37f-174">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9b37f-174">Additional resources</span></span>
<span data-ttu-id="9b37f-175">Сведения о распространенных шаблонах архитектуры данных для мультитенантных приложений базы данных SaaS см. в статье [Шаблоны разработки для мультитенантных приложений SaaS с использованием базы данных Azure SQL](sql-database-design-patterns-multi-tenancy-saas-applications.md).</span><span class="sxs-lookup"><span data-stu-id="9b37f-175">For information on common data architecture patterns of multi-tenant software-as-a-service (SaaS) database applications, see [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md).</span></span>

## <a name="questions-and-feature-requests"></a><span data-ttu-id="9b37f-176">Вопросы и запросы на функции</span><span class="sxs-lookup"><span data-stu-id="9b37f-176">Questions and Feature Requests</span></span>
<span data-ttu-id="9b37f-177">Все возникшие вопросы задавайте на [форуме по базам данных SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted), а запросы новых функций оставляйте на [форуме отзывов и предложений по базам данных SQL](https://feedback.azure.com/forums/217321-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="9b37f-177">For questions, please reach out to us on the [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them to the [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-convert-to-use-elastic-tools/listmapping.png
[2]: ./media/sql-database-elastic-convert-to-use-elastic-tools/rangemapping.png
[3]: ./media/sql-database-elastic-convert-to-use-elastic-tools/multipleonsingledb.png

