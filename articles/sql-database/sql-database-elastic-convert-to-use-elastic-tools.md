---
title: "aaaMigrate существующих баз данных вне tooscale | Документы Microsoft"
description: "Преобразование Сервис эластичной базы данных toouse сегментированных баз данных путем создания диспетчера карты сегментов"
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
ms.openlocfilehash: fa2c9e3699f30667cf547d1faadf4504609199be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-existing-databases-tooscale-out"></a><span data-ttu-id="ca565-103">Миграция существующих баз данных tooscale масштабированием</span><span class="sxs-lookup"><span data-stu-id="ca565-103">Migrate existing databases tooscale-out</span></span>
<span data-ttu-id="ca565-104">Легко управлять существующих масштабируемых сегментированных баз данных с помощью базы данных SQL Azure инструменты для баз данных (таких как hello [клиентской библиотеке эластичной базы данных](sql-database-elastic-database-client-library.md)).</span><span class="sxs-lookup"><span data-stu-id="ca565-104">Easily manage your existing scaled-out sharded databases using Azure SQL Database database tools (such as hello [Elastic Database client library](sql-database-elastic-database-client-library.md)).</span></span> <span data-ttu-id="ca565-105">Необходимо сначала преобразовать существующий набор баз данных toouse hello [диспетчера карты сегментов](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="ca565-105">You must first convert an existing set of databases toouse hello [shard map manager](sql-database-elastic-scale-shard-map-management.md).</span></span> 

## <a name="overview"></a><span data-ttu-id="ca565-106">Обзор</span><span class="sxs-lookup"><span data-stu-id="ca565-106">Overview</span></span>
<span data-ttu-id="ca565-107">toomigrate сегментированной базы данных:</span><span class="sxs-lookup"><span data-stu-id="ca565-107">toomigrate an existing sharded database:</span></span> 

1. <span data-ttu-id="ca565-108">Подготовка hello [базы данных диспетчера карты сегментов](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="ca565-108">Prepare hello [shard map manager database](sql-database-elastic-scale-shard-map-management.md).</span></span>
2. <span data-ttu-id="ca565-109">Создание карты сегментов hello.</span><span class="sxs-lookup"><span data-stu-id="ca565-109">Create hello shard map.</span></span>
3. <span data-ttu-id="ca565-110">Подготовьте hello отдельные сегменты.</span><span class="sxs-lookup"><span data-stu-id="ca565-110">Prepare hello individual shards.</span></span>  
4. <span data-ttu-id="ca565-111">Добавление карты сегментов toohello сопоставления.</span><span class="sxs-lookup"><span data-stu-id="ca565-111">Add mappings toohello shard map.</span></span>

<span data-ttu-id="ca565-112">Эти методы можно реализовать с помощью либо hello [клиентская библиотека .NET Framework](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), или скрипты PowerShell hello, обнаруженным в [база данных SQL Azure — скриптов средств эластичной базы данных](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="ca565-112">These techniques can be implemented using either hello [.NET Framework client library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), or hello PowerShell scripts found at [Azure SQL DB - Elastic Database tools scripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span> <span data-ttu-id="ca565-113">Приведенные здесь примеры Hello использовать скрипты PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="ca565-113">hello examples here use hello PowerShell scripts.</span></span>

<span data-ttu-id="ca565-114">Дополнительные сведения о hello ShardMapManager см. в разделе [управления карты сегментов](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="ca565-114">For more information about hello ShardMapManager, see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="ca565-115">Обзор средств hello эластичной базы данных см. в разделе [Общие сведения о возможностях эластичной базы данных](sql-database-elastic-scale-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ca565-115">For an overview of hello elastic database tools, see [Elastic Database features overview](sql-database-elastic-scale-introduction.md).</span></span>

## <a name="prepare-hello-shard-map-manager-database"></a><span data-ttu-id="ca565-116">Подготовка базы данных диспетчера карты сегментов hello</span><span class="sxs-lookup"><span data-stu-id="ca565-116">Prepare hello shard map manager database</span></span>
<span data-ttu-id="ca565-117">диспетчера карты сегментов Hello является специальная база данных, содержащей данные toomanage hello масштабируемых-базы данных.</span><span class="sxs-lookup"><span data-stu-id="ca565-117">hello shard map manager is a special database that contains hello data toomanage scaled-out databases.</span></span> <span data-ttu-id="ca565-118">Можно использовать существующую базу данных или создать новую.</span><span class="sxs-lookup"><span data-stu-id="ca565-118">You can use an existing database, or create a new database.</span></span> <span data-ttu-id="ca565-119">Обратите внимание, что база данных выступает в роли диспетчера карты сегментов не должно быть hello же базы данных, как тот или иной сегмент.</span><span class="sxs-lookup"><span data-stu-id="ca565-119">Note that a database acting as shard map manager should not be hello same database as a shard.</span></span> <span data-ttu-id="ca565-120">Также Обратите внимание, что скрипт PowerShell hello не создаются hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="ca565-120">Also note that hello PowerShell script does not create hello database for you.</span></span> 

## <a name="step-1-create-a-shard-map-manager"></a><span data-ttu-id="ca565-121">Шаг 1. Создание диспетчера сопоставления сегментов</span><span class="sxs-lookup"><span data-stu-id="ca565-121">Step 1: create a shard map manager</span></span>
    # Create a shard map manager. 
    New-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 
    #<server_name> and <smm_db_name> are hello server name and database name 
    # for hello new or existing database that should be used for storing 
    # tenant-database mapping information.

### <a name="tooretrieve-hello-shard-map-manager"></a><span data-ttu-id="ca565-122">диспетчера карты сегментов tooretrieve hello</span><span class="sxs-lookup"><span data-stu-id="ca565-122">tooretrieve hello shard map manager</span></span>
<span data-ttu-id="ca565-123">После создания можно извлечь hello диспетчера карты сегментов с этим командлетом.</span><span class="sxs-lookup"><span data-stu-id="ca565-123">After creation, you can retrieve hello shard map manager with this cmdlet.</span></span> <span data-ttu-id="ca565-124">Этот шаг требуется каждый раз, когда необходимо toouse hello ShardMapManager объекта.</span><span class="sxs-lookup"><span data-stu-id="ca565-124">This step is needed every time you need toouse hello ShardMapManager object.</span></span>

    # Try tooget a reference toohello Shard Map Manager  
    $ShardMapManager = Get-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 


## <a name="step-2-create-hello-shard-map"></a><span data-ttu-id="ca565-125">Шаг 2: Создание карты сегментов hello</span><span class="sxs-lookup"><span data-stu-id="ca565-125">Step 2: create hello shard map</span></span>
<span data-ttu-id="ca565-126">Необходимо выбрать тип hello toocreate карты сегментов.</span><span class="sxs-lookup"><span data-stu-id="ca565-126">You must select hello type of shard map toocreate.</span></span> <span data-ttu-id="ca565-127">Выбор Hello зависит от архитектуры hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="ca565-127">hello choice depends on hello database architecture:</span></span> 

1. <span data-ttu-id="ca565-128">Для каждой базы данных одного клиента (условия, в разделе hello [Глоссарий](sql-database-elastic-scale-glossary.md).)</span><span class="sxs-lookup"><span data-stu-id="ca565-128">Single tenant per database (For terms, see hello [glossary](sql-database-elastic-scale-glossary.md).)</span></span> 
2. <span data-ttu-id="ca565-129">Несколько клиентов на одну базу данных (два типа):</span><span class="sxs-lookup"><span data-stu-id="ca565-129">Multiple tenants per database (two types):</span></span>
   1. <span data-ttu-id="ca565-130">Сопоставление по спискам</span><span class="sxs-lookup"><span data-stu-id="ca565-130">List mapping</span></span>
   2. <span data-ttu-id="ca565-131">Сопоставление по диапазонам</span><span class="sxs-lookup"><span data-stu-id="ca565-131">Range mapping</span></span>

<span data-ttu-id="ca565-132">Для модели с одним клиентом создайте карту сегментов с **сопоставлением по списку** .</span><span class="sxs-lookup"><span data-stu-id="ca565-132">For a single-tenant model, create a **list mapping** shard map.</span></span> <span data-ttu-id="ca565-133">модель одного клиента Hello назначает одной базы данных на клиенте.</span><span class="sxs-lookup"><span data-stu-id="ca565-133">hello single-tenant model assigns one database per tenant.</span></span> <span data-ttu-id="ca565-134">Эта модель подходит для разработчиков SaaS, так как она упрощает управление.</span><span class="sxs-lookup"><span data-stu-id="ca565-134">This is an effective model for SaaS developers as it simplifies management.</span></span>

![Сопоставление по спискам][1]

<span data-ttu-id="ca565-136">Hello мультитенантной модели назначает несколько клиентов tooa одной базы данных (и групп клиентов можно распределить по нескольким базам данных).</span><span class="sxs-lookup"><span data-stu-id="ca565-136">hello multi-tenant model assigns several tenants tooa single database (and you can distribute groups of tenants across multiple databases).</span></span> <span data-ttu-id="ca565-137">Эту модель можно используйте, когда предполагается, что данные, toohave небольшой каждого клиента.</span><span class="sxs-lookup"><span data-stu-id="ca565-137">Use this model when you expect each tenant toohave small data needs.</span></span> <span data-ttu-id="ca565-138">В этой модели мы назначает диапазон клиентов tooa базы данных с помощью **сопоставления диапазона**.</span><span class="sxs-lookup"><span data-stu-id="ca565-138">In this model, we assign a range of tenants tooa database using **range mapping**.</span></span> 

![Сопоставление по диапазонам][2]

<span data-ttu-id="ca565-140">Или можно применить модель базы данных нескольких клиентов с помощью *сопоставление списка* tooassign несколько клиентов tooa одной базы данных.</span><span class="sxs-lookup"><span data-stu-id="ca565-140">Or you can implement a multi-tenant database model using a *list mapping* tooassign multiple tenants tooa single database.</span></span> <span data-ttu-id="ca565-141">Например используется toostore сведения об ИД клиента 1 и 5 — DB1 и DB2 хранит данные для клиента 7 и 10 клиента.</span><span class="sxs-lookup"><span data-stu-id="ca565-141">For example, DB1 is used toostore information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span></span> 

![Несколько клиентов для одной базы данных][3] 

<span data-ttu-id="ca565-143">**Выберите один из вариантов, соответствующий вашему выбору.**</span><span class="sxs-lookup"><span data-stu-id="ca565-143">**Based on your choice, choose one of these options:**</span></span>

### <a name="option-1-create-a-shard-map-for-a-list-mapping"></a><span data-ttu-id="ca565-144">Вариант 1. Создание карты сегментов для сопоставления по списку</span><span class="sxs-lookup"><span data-stu-id="ca565-144">Option 1: create a shard map for a list mapping</span></span>
<span data-ttu-id="ca565-145">Создайте карту сегментов, с помощью объекта ShardMapManager hello.</span><span class="sxs-lookup"><span data-stu-id="ca565-145">Create a shard map using hello ShardMapManager object.</span></span> 

    # $ShardMapManager is hello shard map manager object. 
    $ShardMap = New-ListShardMap -KeyType $([int]) 
    -ListShardMapName 'ListShardMap' 
    -ShardMapManager $ShardMapManager 


### <a name="option-2-create-a-shard-map-for-a-range-mapping"></a><span data-ttu-id="ca565-146">Вариант 2. Создание карты сегментов для сопоставления по диапазонам</span><span class="sxs-lookup"><span data-stu-id="ca565-146">Option 2: create a shard map for a range mapping</span></span>
<span data-ttu-id="ca565-147">Обратите внимание, что tooutilize этот шаблон для сопоставления, значения идентификатора клиента должен toobe непрерывного диапазона, и он является приемлемым toohave разрыв в диапазонах hello пропустив просто hello диапазона при создании баз данных hello.</span><span class="sxs-lookup"><span data-stu-id="ca565-147">Note that tooutilize this mapping pattern, tenant id values needs toobe continuous ranges, and it is acceptable toohave gap in hello ranges by simply skipping hello range when creating hello databases.</span></span>

    # $ShardMapManager is hello shard map manager object 
    # 'RangeShardMap' is hello unique identifier for hello range shard map.  
    $ShardMap = New-RangeShardMap 
    -KeyType $([int]) 
    -RangeShardMapName 'RangeShardMap' 
    -ShardMapManager $ShardMapManager 

### <a name="option-3-list-mappings-on-a-single-database"></a><span data-ttu-id="ca565-148">Вариант 3. Сопоставление по списку для одной базы данных</span><span class="sxs-lookup"><span data-stu-id="ca565-148">Option 3: List mappings on a single database</span></span>
<span data-ttu-id="ca565-149">Для настройки этого шаблона также требуется создать карту списков, как показано в разделе "Шаг 2, вариант 1".</span><span class="sxs-lookup"><span data-stu-id="ca565-149">Setting up this pattern also requires creation of a list map as shown in step 2, option 1.</span></span>

## <a name="step-3-prepare-individual-shards"></a><span data-ttu-id="ca565-150">Шаг 3. Подготовка отдельных сегментов</span><span class="sxs-lookup"><span data-stu-id="ca565-150">Step 3: Prepare individual shards</span></span>
<span data-ttu-id="ca565-151">Добавьте каждый диспетчера карты сегментов toohello сегментов (база данных).</span><span class="sxs-lookup"><span data-stu-id="ca565-151">Add each shard (database) toohello shard map manager.</span></span> <span data-ttu-id="ca565-152">Это подготавливает hello отдельных баз данных для хранения сведений о сопоставлении.</span><span class="sxs-lookup"><span data-stu-id="ca565-152">This prepares hello individual databases for storing mapping information.</span></span> <span data-ttu-id="ca565-153">Подготовьте так каждый сегмент.</span><span class="sxs-lookup"><span data-stu-id="ca565-153">Execute this method on each shard.</span></span>

    Add-Shard 
    -ShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>'
    # hello $ShardMap is hello shard map created in step 2.


## <a name="step-4-add-mappings"></a><span data-ttu-id="ca565-154">Шаг 4. Добавление сопоставлений</span><span class="sxs-lookup"><span data-stu-id="ca565-154">Step 4: Add mappings</span></span>
<span data-ttu-id="ca565-155">Добавление Hello сопоставлений зависит от вида hello карта сегментов, созданный.</span><span class="sxs-lookup"><span data-stu-id="ca565-155">hello addition of mappings depends on hello kind of shard map you created.</span></span> <span data-ttu-id="ca565-156">Если создана карта списков, нужно добавить сопоставления по спискам.</span><span class="sxs-lookup"><span data-stu-id="ca565-156">If you created a list map, you add list mappings.</span></span> <span data-ttu-id="ca565-157">Если создана карта диапазонов, нужно добавить сопоставления по диапазонам.</span><span class="sxs-lookup"><span data-stu-id="ca565-157">If you created a range map, you add range mappings.</span></span>

### <a name="option-1-map-hello-data-for-a-list-mapping"></a><span data-ttu-id="ca565-158">Вариант 1: данные hello карты для отображения списка</span><span class="sxs-lookup"><span data-stu-id="ca565-158">Option 1: map hello data for a list mapping</span></span>
<span data-ttu-id="ca565-159">Сопоставление данных hello, добавив сопоставление списка для каждого клиента.</span><span class="sxs-lookup"><span data-stu-id="ca565-159">Map hello data by adding a list mapping for each tenant.</span></span>  

    # Create hello mappings and associate it with hello new shards 
    Add-ListMapping 
    -KeyType $([int]) 
    -ListPoint '<tenant_id>' 
    -ListShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 

### <a name="option-2-map-hello-data-for-a-range-mapping"></a><span data-ttu-id="ca565-160">Вариант 2: данные hello карты для сопоставления диапазона</span><span class="sxs-lookup"><span data-stu-id="ca565-160">Option 2: map hello data for a range mapping</span></span>
<span data-ttu-id="ca565-161">Добавьте hello диапазон сопоставления для всех диапазон идентификаторов клиента hello - связи баз данных:</span><span class="sxs-lookup"><span data-stu-id="ca565-161">Add hello range mappings for all hello tenant id range - database associations:</span></span>

    # Create hello mappings and associate it with hello new shards 
    Add-RangeMapping 
    -KeyType $([int]) 
    -RangeHigh '5' 
    -RangeLow '1' 
    -RangeShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 


### <a name="step-4-option-3-map-hello-data-for-multiple-tenants-on-a-single-database"></a><span data-ttu-id="ca565-162">Вариант 3. шаг 4: сопоставление hello данных для нескольких клиентов в одной базе данных</span><span class="sxs-lookup"><span data-stu-id="ca565-162">Step 4 option 3: map hello data for multiple tenants on a single database</span></span>
<span data-ttu-id="ca565-163">Для каждого клиента, запустите hello добавить ListMapping (параметр 1, выше).</span><span class="sxs-lookup"><span data-stu-id="ca565-163">For each tenant, run hello Add-ListMapping (option 1, above).</span></span> 

## <a name="checking-hello-mappings"></a><span data-ttu-id="ca565-164">Проверка сопоставления hello</span><span class="sxs-lookup"><span data-stu-id="ca565-164">Checking hello mappings</span></span>
<span data-ttu-id="ca565-165">Сведения о существующих сегментов hello и сопоставления hello, связанные с ними можно запросить с помощью следующих команд:</span><span class="sxs-lookup"><span data-stu-id="ca565-165">Information about hello existing shards and hello mappings associated with them can be queried using following commands:</span></span>  

    # List hello shards and mappings 
    Get-Shards -ShardMap $ShardMap 
    Get-Mappings -ShardMap $ShardMap 

## <a name="summary"></a><span data-ttu-id="ca565-166">Сводка</span><span class="sxs-lookup"><span data-stu-id="ca565-166">Summary</span></span>
<span data-ttu-id="ca565-167">После завершения установки hello, можно начать toouse hello эластичной базы данных клиентской библиотеки.</span><span class="sxs-lookup"><span data-stu-id="ca565-167">Once you have completed hello setup, you can begin toouse hello Elastic Database client library.</span></span> <span data-ttu-id="ca565-168">Кроме того, можно воспользоваться [маршрутизацией, зависящей от данных](sql-database-elastic-scale-data-dependent-routing.md), и [формированием многосегментных запросов](sql-database-elastic-scale-multishard-querying.md).</span><span class="sxs-lookup"><span data-stu-id="ca565-168">You can also use [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) and [multi-shard query](sql-database-elastic-scale-multishard-querying.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca565-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ca565-169">Next steps</span></span>
<span data-ttu-id="ca565-170">Получение скриптов PowerShell hello из [базы данных эластичных БД SQL Azure средств sripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="ca565-170">Get hello PowerShell scripts from [Azure SQL DB-Elastic Database tools sripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

<span data-ttu-id="ca565-171">Hello средства доступны на сайте GitHub: [Azure/гибкому db-tools](https://github.com/Azure/elastic-db-tools).</span><span class="sxs-lookup"><span data-stu-id="ca565-171">hello tools are also on GitHub: [Azure/elastic-db-tools](https://github.com/Azure/elastic-db-tools).</span></span>

<span data-ttu-id="ca565-172">Используйте tooor hello средство слияния разбиение toomove данных из одного клиента модели tooa мультитенантной модели.</span><span class="sxs-lookup"><span data-stu-id="ca565-172">Use hello split-merge tool toomove data tooor from a multi-tenant model tooa single tenant model.</span></span> <span data-ttu-id="ca565-173">Ознакомьтесь со статьей о [средстве разбиения и объединения](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ca565-173">See [Split merge tool](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ca565-174">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ca565-174">Additional resources</span></span>
<span data-ttu-id="ca565-175">Сведения о распространенных шаблонах архитектуры данных для мультитенантных приложений базы данных SaaS см. в статье [Шаблоны разработки для мультитенантных приложений SaaS с использованием базы данных Azure SQL](sql-database-design-patterns-multi-tenancy-saas-applications.md).</span><span class="sxs-lookup"><span data-stu-id="ca565-175">For information on common data architecture patterns of multi-tenant software-as-a-service (SaaS) database applications, see [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md).</span></span>

## <a name="questions-and-feature-requests"></a><span data-ttu-id="ca565-176">Вопросы и запросы на функции</span><span class="sxs-lookup"><span data-stu-id="ca565-176">Questions and Feature Requests</span></span>
<span data-ttu-id="ca565-177">Ответить на вопросы, пожалуйста направляться на hello toous [форум базы данных SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) и для запросов, компонент, добавьте их toohello [форуме обратной связи в базе данных SQL](https://feedback.azure.com/forums/217321-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="ca565-177">For questions, please reach out toous on hello [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them toohello [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-convert-to-use-elastic-tools/listmapping.png
[2]: ./media/sql-database-elastic-convert-to-use-elastic-tools/rangemapping.png
[3]: ./media/sql-database-elastic-convert-to-use-elastic-tools/multipleonsingledb.png

