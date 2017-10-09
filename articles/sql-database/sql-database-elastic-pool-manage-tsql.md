---
title: "T-SQL: управление пулом эластичных баз данных SQL Azure | Документация Майкрософт"
description: "С помощью T-SQL toomanage пул эластичных баз данных SQL Azure."
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
ms.openlocfilehash: 666f131b2c88849a1a9ea83381bbc27548e93599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-an-elastic-pool-with-transact-sql"></a><span data-ttu-id="fe633-103">Мониторинг пула эластичных баз данных и управление им с помощью Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="fe633-103">Monitor and manage an elastic pool with Transact-SQL</span></span>
<span data-ttu-id="fe633-104">В этом разделе показано, как масштабируемой toomanage [эластичные пулы](sql-database-elastic-pool.md) с помощью Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="fe633-104">This topic shows you how toomanage scalable [elastic pools](sql-database-elastic-pool.md) with Transact-SQL.</span></span>  <span data-ttu-id="fe633-105">Можно также создать и управлять hello Azure эластичного пула [портал Azure](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello REST API или [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="fe633-105">You can also create and manage an Azure elastic pool hello [Azure portal](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="fe633-106">Вы также можете использовать [Transact-SQL](sql-database-elastic-pool-manage-tsql.md), чтобы создавать новые базы данных в эластичных пулах и перемещать базы данных в пулы и обратно.</span><span class="sxs-lookup"><span data-stu-id="fe633-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>


<span data-ttu-id="fe633-107">Используйте hello [Create Database (база данных SQL Azure)](https://msdn.microsoft.com/library/dn268335.aspx) и [Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) команды toocreate и перемещения баз данных в действие и из эластичные пулы.</span><span class="sxs-lookup"><span data-stu-id="fe633-107">Use hello [Create Database (Azure SQL Database)](https://msdn.microsoft.com/library/dn268335.aspx) and [Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) commands toocreate and move databases into and out of elastic pools.</span></span> <span data-ttu-id="fe633-108">Hello эластичного пула должен существовать, прежде чем использовать эти команды.</span><span class="sxs-lookup"><span data-stu-id="fe633-108">hello elastic pool must exist before you can use these commands.</span></span> <span data-ttu-id="fe633-109">Эти команды влияют только на базы данных.</span><span class="sxs-lookup"><span data-stu-id="fe633-109">These commands affect only databases.</span></span> <span data-ttu-id="fe633-110">Создание новых групп и приветствия свойств пула (например, min и max Edtu) нельзя изменить с помощью команды T-SQL.</span><span class="sxs-lookup"><span data-stu-id="fe633-110">Creation of new pools and hello setting of pool properties (such as min and max eDTUs) cannot be changed with T-SQL commands.</span></span>

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="fe633-111">Создание базы данных внутри эластичного пула</span><span class="sxs-lookup"><span data-stu-id="fe633-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="fe633-112">Команда CREATE DATABASE hello с hello SERVICE_OBJECTIVE параметр.</span><span class="sxs-lookup"><span data-stu-id="fe633-112">Use hello CREATE DATABASE command with hello SERVICE_OBJECTIVE option.</span></span>   

    CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3M100] ));
    -- Create a database named db1 in an elastic named S3M100.

<span data-ttu-id="fe633-113">Все базы данных в пуле эластичных наследуют уровень обслуживания hello hello эластичного пула (Basic, Standard, Premium).</span><span class="sxs-lookup"><span data-stu-id="fe633-113">All databases in an elastic pool inherit hello service tier of hello elastic pool (Basic, Standard, Premium).</span></span> 

## <a name="move-a-database-between-elastic-pools"></a><span data-ttu-id="fe633-114">Перемещение базы данных между пулами эластичных БД</span><span class="sxs-lookup"><span data-stu-id="fe633-114">Move a database between elastic pools</span></span>
<span data-ttu-id="fe633-115">Используйте команду ALTER DATABASE hello с hello изменить и настроить службу\_цели параметр как ГИБКОМУ\_ПУЛА.</span><span class="sxs-lookup"><span data-stu-id="fe633-115">Use hello ALTER DATABASE command with hello MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC\_POOL.</span></span> <span data-ttu-id="fe633-116">Задайте имя toohello имя hello hello целевого пула.</span><span class="sxs-lookup"><span data-stu-id="fe633-116">Set hello name toohello name of hello target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [PM125] ));
    -- Move hello database named db1 tooan elastic named P1M125  

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="fe633-117">Перемещение базы данных в пул эластичных БД</span><span class="sxs-lookup"><span data-stu-id="fe633-117">Move a database into an elastic pool</span></span>
<span data-ttu-id="fe633-118">Используйте команду ALTER DATABASE hello с hello изменить и настроить службу\_цели параметр как ELASTIC_POOL.</span><span class="sxs-lookup"><span data-stu-id="fe633-118">Use hello ALTER DATABASE command with hello MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC_POOL.</span></span> <span data-ttu-id="fe633-119">Задайте имя toohello имя hello hello целевого пула.</span><span class="sxs-lookup"><span data-stu-id="fe633-119">Set hello name toohello name of hello target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3100] ));
    -- Move hello database named db1 tooan elastic named S3100.

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="fe633-120">Перемещение базы данных из пула эластичных БД</span><span class="sxs-lookup"><span data-stu-id="fe633-120">Move a database out of an elastic pool</span></span>
<span data-ttu-id="fe633-121">Используйте команду ALTER DATABASE hello и установите tooone SERVICE_OBJECTIVE hello hello уровней производительности (например S0 или S1).</span><span class="sxs-lookup"><span data-stu-id="fe633-121">Use hello ALTER DATABASE command and set hello SERVICE_OBJECTIVE tooone of hello performance levels (such as S0 or S1).</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = 'S1');
    -- Changes hello database into a stand-alone database with hello service objective S1.

## <a name="list-databases-in-an-elastic-pool"></a><span data-ttu-id="fe633-122">Получение списка баз данных в пуле эластичных БД</span><span class="sxs-lookup"><span data-stu-id="fe633-122">List databases in an elastic pool</span></span>
<span data-ttu-id="fe633-123">Используйте hello [sys.database\_службы \_целей представление](https://msdn.microsoft.com/library/mt712619) toolist все hello баз данных в пуле эластичных БД.</span><span class="sxs-lookup"><span data-stu-id="fe633-123">Use hello [sys.database\_service \_objectives view](https://msdn.microsoft.com/library/mt712619) toolist all hello databases in an elastic pool.</span></span> <span data-ttu-id="fe633-124">Войдите в базе данных master toohello представление hello tooquery базы данных.</span><span class="sxs-lookup"><span data-stu-id="fe633-124">Log in toohello master database tooquery hello view.</span></span>

    SELECT d.name, slo.*  
    FROM sys.databases d 
    JOIN sys.database_service_objectives slo  
    ON d.database_id = slo.database_id
    WHERE elastic_pool_name = 'MyElasticPool'; 

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="fe633-125">Получение данных об использовании ресурсов в эластичном пуле</span><span class="sxs-lookup"><span data-stu-id="fe633-125">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="fe633-126">Используйте hello [sys.elastic\_пула \_ресурсов \_представление stats](https://msdn.microsoft.com/library/mt280062.aspx) tooexamine hello Статистика использования ресурсов для эластичного пула на логическом сервере.</span><span class="sxs-lookup"><span data-stu-id="fe633-126">Use hello [sys.elastic\_pool \_resource \_stats view](https://msdn.microsoft.com/library/mt280062.aspx) tooexamine hello resource usage statistics of an elastic pool on a logical server.</span></span> <span data-ttu-id="fe633-127">Войдите в базе данных master toohello представление hello tooquery базы данных.</span><span class="sxs-lookup"><span data-stu-id="fe633-127">Log in toohello master database tooquery hello view.</span></span>

    SELECT * FROM sys.elastic_pool_resource_stats 
    WHERE elastic_pool_name = 'MyElasticPool'
    ORDER BY end_time DESC;

## <a name="get-resource-usage-for-a-pooled-database"></a><span data-ttu-id="fe633-128">Получение данных об использовании ресурсов в базе данных, которая находится в пуле</span><span class="sxs-lookup"><span data-stu-id="fe633-128">Get resource usage for a pooled database</span></span>
<span data-ttu-id="fe633-129">Используйте hello [sys.dm\_ db\_ ресурсов\_stats представление](https://msdn.microsoft.com/library/dn800981.aspx) или [sys.resource \_представление stats](https://msdn.microsoft.com/library/dn269979.aspx) Статистика использования ресурсов tooexamine hello объекта База данных в пуле эластичных БД.</span><span class="sxs-lookup"><span data-stu-id="fe633-129">Use hello [sys.dm\_ db\_ resource\_stats view](https://msdn.microsoft.com/library/dn800981.aspx) or [sys.resource \_stats view](https://msdn.microsoft.com/library/dn269979.aspx) tooexamine hello resource usage statistics of a database in an elastic pool.</span></span> <span data-ttu-id="fe633-130">Этот процесс является аналогичные использования tooquerying ресурсов для одной базы данных.</span><span class="sxs-lookup"><span data-stu-id="fe633-130">This process is similar tooquerying resource usage for a single database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe633-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fe633-131">Next steps</span></span>
<span data-ttu-id="fe633-132">После создания эластичного пула, можно управлять путем создания эластичной заданий эластичных баз данных в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="fe633-132">After creating an elastic pool, you can manage elastic databases in hello pool by creating elastic jobs.</span></span> <span data-ttu-id="fe633-133">Эластичный заданий облегчают выполнение скриптов T-SQL для любого количества баз данных в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="fe633-133">Elastic jobs facilitate running T-SQL scripts against any number of databases in hello pool.</span></span> <span data-ttu-id="fe633-134">Дополнительные сведения можно узнать в статье [Обзор службы заданий эластичной базы данных](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fe633-134">For more information, see [Elastic database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

<span data-ttu-id="fe633-135">В разделе [горизонтального масштабирования с базой данных SQL Azure](sql-database-elastic-scale-introduction.md): использовать эластичной базы данных средства tooscale out, перемещение данных, запроса или создания транзакции.</span><span class="sxs-lookup"><span data-stu-id="fe633-135">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic database tools tooscale out, move data, query, or create transactions.</span></span>

