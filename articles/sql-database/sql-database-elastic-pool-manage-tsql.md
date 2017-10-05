---
title: "T-SQL: управление пулом эластичных баз данных SQL Azure | Документация Майкрософт"
description: "Использование T-SQL для управления пулом эластичных баз данных SQL Azure."
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 4e288e17-bc3e-4255-9fbe-0a2ac0dbd7dd
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 05/27/2016
ms.author: srinia
ms.openlocfilehash: c6b64e4a7fd91283a37a792b294965064d653003
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-manage-an-elastic-pool-with-transact-sql"></a><span data-ttu-id="ca613-103">Мониторинг пула эластичных баз данных и управление им с помощью Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="ca613-103">Monitor and manage an elastic pool with Transact-SQL</span></span>
<span data-ttu-id="ca613-104">В этой статье показано, как с помощью Transact-SQL администрировать масштабируемые [эластичные пулы](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="ca613-104">This topic shows you how to manage scalable [elastic pools](sql-database-elastic-pool.md) with Transact-SQL.</span></span>  <span data-ttu-id="ca613-105">Для создания эластичных пулов Azure и управления ими можно также использовать [портал Azure](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), REST API или [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="ca613-105">You can also create and manage an Azure elastic pool the [Azure portal](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), the REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="ca613-106">Вы также можете использовать [Transact-SQL](sql-database-elastic-pool-manage-tsql.md), чтобы создавать новые базы данных в эластичных пулах и перемещать базы данных в пулы и обратно.</span><span class="sxs-lookup"><span data-stu-id="ca613-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>


<span data-ttu-id="ca613-107">Для создания и перемещения баз данных в эластичные пулы и обратно используйте команды [Create Database (база данных SQL Azure)](https://msdn.microsoft.com/library/dn268335.aspx) и [Alter Database (база данных SQL Azure)](https://msdn.microsoft.com/library/mt574871.aspx).</span><span class="sxs-lookup"><span data-stu-id="ca613-107">Use the [Create Database (Azure SQL Database)](https://msdn.microsoft.com/library/dn268335.aspx) and [Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) commands to create and move databases into and out of elastic pools.</span></span> <span data-ttu-id="ca613-108">Прежде чем использовать эти команды, следует создать пул эластичных БД.</span><span class="sxs-lookup"><span data-stu-id="ca613-108">The elastic pool must exist before you can use these commands.</span></span> <span data-ttu-id="ca613-109">Эти команды влияют только на базы данных.</span><span class="sxs-lookup"><span data-stu-id="ca613-109">These commands affect only databases.</span></span> <span data-ttu-id="ca613-110">С помощью команд T-SQL нельзя внести изменения при создании новых пулов и настройке свойств пула (таких как минимальное и максимальное количество eDTU).</span><span class="sxs-lookup"><span data-stu-id="ca613-110">Creation of new pools and the setting of pool properties (such as min and max eDTUs) cannot be changed with T-SQL commands.</span></span>

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="ca613-111">Создание базы данных внутри эластичного пула</span><span class="sxs-lookup"><span data-stu-id="ca613-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="ca613-112">Используйте команду CREATE DATABASE с параметром SERVICE_OBJECTIVE.</span><span class="sxs-lookup"><span data-stu-id="ca613-112">Use the CREATE DATABASE command with the SERVICE_OBJECTIVE option.</span></span>   

    CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3M100] ));
    -- Create a database named db1 in an elastic named S3M100.

<span data-ttu-id="ca613-113">Все базы данных в пуле эластичных БД наследуют уровень служб пула эластичных БД ("Базовый", "Стандартный" или "Премиум").</span><span class="sxs-lookup"><span data-stu-id="ca613-113">All databases in an elastic pool inherit the service tier of the elastic pool (Basic, Standard, Premium).</span></span> 

## <a name="move-a-database-between-elastic-pools"></a><span data-ttu-id="ca613-114">Перемещение базы данных между пулами эластичных БД</span><span class="sxs-lookup"><span data-stu-id="ca613-114">Move a database between elastic pools</span></span>
<span data-ttu-id="ca613-115">Используйте команду ALTER DATABASE с инструкцией MODIFY и параметром SERVICE\_OBJECTIVE, для которого задано значение ELASTIC\_POOL.</span><span class="sxs-lookup"><span data-stu-id="ca613-115">Use the ALTER DATABASE command with the MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC\_POOL.</span></span> <span data-ttu-id="ca613-116">Присвойте имя целевому пулу.</span><span class="sxs-lookup"><span data-stu-id="ca613-116">Set the name to the name of the target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [PM125] ));
    -- Move the database named db1 to an elastic named P1M125  

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="ca613-117">Перемещение базы данных в пул эластичных БД</span><span class="sxs-lookup"><span data-stu-id="ca613-117">Move a database into an elastic pool</span></span>
<span data-ttu-id="ca613-118">Используйте команду ALTER DATABASE с инструкцией MODIFY и параметром SERVICE\_OBJECTIVE, для которого задано значение ELASTIC_POOL.</span><span class="sxs-lookup"><span data-stu-id="ca613-118">Use the ALTER DATABASE command with the MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC_POOL.</span></span> <span data-ttu-id="ca613-119">Присвойте имя целевому пулу.</span><span class="sxs-lookup"><span data-stu-id="ca613-119">Set the name to the name of the target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3100] ));
    -- Move the database named db1 to an elastic named S3100.

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="ca613-120">Перемещение базы данных из пула эластичных БД</span><span class="sxs-lookup"><span data-stu-id="ca613-120">Move a database out of an elastic pool</span></span>
<span data-ttu-id="ca613-121">Используйте команду ALTER DATABASE и задайте для параметра SERVICE_OBJECTIVE уровень производительности (например, S0 или S1).</span><span class="sxs-lookup"><span data-stu-id="ca613-121">Use the ALTER DATABASE command and set the SERVICE_OBJECTIVE to one of the performance levels (such as S0 or S1).</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = 'S1');
    -- Changes the database into a stand-alone database with the service objective S1.

## <a name="list-databases-in-an-elastic-pool"></a><span data-ttu-id="ca613-122">Получение списка баз данных в пуле эластичных БД</span><span class="sxs-lookup"><span data-stu-id="ca613-122">List databases in an elastic pool</span></span>
<span data-ttu-id="ca613-123">Чтобы получить список всех баз данных в пуле эластичных БД, используйте представление [sys.database\_service\_objectives](https://msdn.microsoft.com/library/mt712619).</span><span class="sxs-lookup"><span data-stu-id="ca613-123">Use the [sys.database\_service \_objectives view](https://msdn.microsoft.com/library/mt712619) to list all the databases in an elastic pool.</span></span> <span data-ttu-id="ca613-124">Войдите в базу данных master, чтобы отправить запрос на представление.</span><span class="sxs-lookup"><span data-stu-id="ca613-124">Log in to the master database to query the view.</span></span>

    SELECT d.name, slo.*  
    FROM sys.databases d 
    JOIN sys.database_service_objectives slo  
    ON d.database_id = slo.database_id
    WHERE elastic_pool_name = 'MyElasticPool'; 

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="ca613-125">Получение данных об использовании ресурсов в эластичном пуле</span><span class="sxs-lookup"><span data-stu-id="ca613-125">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="ca613-126">Проанализировать статистику использования ресурсов в пуле эластичных БД на логическом сервере можно в [представлении sys.elastic\_pool \_resource\_stats](https://msdn.microsoft.com/library/mt280062.aspx).</span><span class="sxs-lookup"><span data-stu-id="ca613-126">Use the [sys.elastic\_pool \_resource \_stats view](https://msdn.microsoft.com/library/mt280062.aspx) to examine the resource usage statistics of an elastic pool on a logical server.</span></span> <span data-ttu-id="ca613-127">Войдите в базу данных master, чтобы отправить запрос на представление.</span><span class="sxs-lookup"><span data-stu-id="ca613-127">Log in to the master database to query the view.</span></span>

    SELECT * FROM sys.elastic_pool_resource_stats 
    WHERE elastic_pool_name = 'MyElasticPool'
    ORDER BY end_time DESC;

## <a name="get-resource-usage-for-a-pooled-database"></a><span data-ttu-id="ca613-128">Получение данных об использовании ресурсов в базе данных, которая находится в пуле</span><span class="sxs-lookup"><span data-stu-id="ca613-128">Get resource usage for a pooled database</span></span>
<span data-ttu-id="ca613-129">Проанализировать статистику использования ресурсов базы данных в эластичном пуле можно в [представлении sys.dm\_db\_resource\_stats](https://msdn.microsoft.com/library/dn800981.aspx) или [sys.resource\_stats](https://msdn.microsoft.com/library/dn269979.aspx).</span><span class="sxs-lookup"><span data-stu-id="ca613-129">Use the [sys.dm\_ db\_ resource\_stats view](https://msdn.microsoft.com/library/dn800981.aspx) or [sys.resource \_stats view](https://msdn.microsoft.com/library/dn269979.aspx) to examine the resource usage statistics of a database in an elastic pool.</span></span> <span data-ttu-id="ca613-130">Этот процесс аналогичен отправке запроса на использование ресурсов для любой отдельной базы данных.</span><span class="sxs-lookup"><span data-stu-id="ca613-130">This process is similar to querying resource usage for a single database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca613-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ca613-131">Next steps</span></span>
<span data-ttu-id="ca613-132">После создания эластичного пула вы можете управлять его эластичными базами данных путем создания эластичных заданий.</span><span class="sxs-lookup"><span data-stu-id="ca613-132">After creating an elastic pool, you can manage elastic databases in the pool by creating elastic jobs.</span></span> <span data-ttu-id="ca613-133">Эластичные задания позволяют легко и быстро выполнять сценарии T-SQL в любом количестве баз данных в пуле.</span><span class="sxs-lookup"><span data-stu-id="ca613-133">Elastic jobs facilitate running T-SQL scripts against any number of databases in the pool.</span></span> <span data-ttu-id="ca613-134">Дополнительные сведения можно узнать в статье [Обзор службы заданий эластичной базы данных](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ca613-134">For more information, see [Elastic database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

<span data-ttu-id="ca613-135">Ознакомьтесь с инструкциями по [масштабированию базы данных SQL Azure](sql-database-elastic-scale-introduction.md). Вы узнаете, как использовать средства эластичной базы данных для масштабирования, перемещения данных, выполнения запросов и создания транзакций.</span><span class="sxs-lookup"><span data-stu-id="ca613-135">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic database tools to scale out, move data, query, or create transactions.</span></span>

