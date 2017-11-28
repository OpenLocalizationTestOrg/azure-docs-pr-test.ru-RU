---
title: "PowerShell: создание эластичного пула SQL Azure и управление им | Документация Майкрософт"
description: "Узнайте, как toomanage toouse PowerShell эластичного пула."
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 61289770-69b9-4ae3-9252-d0e94d709331
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: data-management
ms.date: 06/06/2017
ms.author: srinia
ms.openlocfilehash: 92de2a4b243dcc74502064e9d2c31682691753d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-powershell"></a><span data-ttu-id="e9762-103">Создание эластичного пула и управление им с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="e9762-103">Create and manage an elastic pool with PowerShell</span></span>
<span data-ttu-id="e9762-104">В этом разделе показано, как toocreate и управления ими масштабируемой [эластичные пулы](sql-database-elastic-pool.md) с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e9762-104">This topic shows you how toocreate and manage scalable [elastic pools](sql-database-elastic-pool.md) with PowerShell.</span></span>  <span data-ttu-id="e9762-105">Можно также создать и управлять Azure эластичного пула, с помощью hello [портал Azure](https://portal.azure.com/), REST API или [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="e9762-105">You can also create and manage an Azure elastic pool using hello [Azure portal](https://portal.azure.com/), REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="e9762-106">Вы также можете использовать [Transact-SQL](sql-database-elastic-pool-manage-tsql.md), чтобы создавать новые базы данных в эластичных пулах и перемещать базы данных в пулы и обратно.</span><span class="sxs-lookup"><span data-stu-id="e9762-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

[!INCLUDE [Start your PowerShell session](../../includes/sql-database-powershell.md)]

## <a name="create-an-elastic-pool"></a><span data-ttu-id="e9762-107">Создание эластичного пула</span><span class="sxs-lookup"><span data-stu-id="e9762-107">Create an elastic pool</span></span>
<span data-ttu-id="e9762-108">Hello [New AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) создает пул эластичных БД.</span><span class="sxs-lookup"><span data-stu-id="e9762-108">hello [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet creates an elastic pool.</span></span> <span data-ttu-id="e9762-109">значения Hello eDTU на пул, min и max Dtu, ограничены hello значение уровня службы (Basic, Standard, Premium или Premium RS).</span><span class="sxs-lookup"><span data-stu-id="e9762-109">hello values for eDTU per pool, min, and max DTUs are constrained by hello service tier value (Basic, Standard, Premium, or Premium RS).</span></span> <span data-ttu-id="e9762-110">См. раздел [eDTU и размеры хранилища для пулов эластичных БД](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span><span class="sxs-lookup"><span data-stu-id="e9762-110">See [eDTU and storage limits for elastic pools and pooled databases](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span></span>

```PowerShell
New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100
```

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="e9762-111">Создание базы данных внутри эластичного пула</span><span class="sxs-lookup"><span data-stu-id="e9762-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="e9762-112">Используйте hello [New AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) командлета и набор hello **ElasticPoolName** параметр toohello целевой пул.</span><span class="sxs-lookup"><span data-stu-id="e9762-112">Use hello [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet and set hello **ElasticPoolName** parameter toohello target pool.</span></span> <span data-ttu-id="e9762-113">toomove существующей базы данных в эластичный пул, в разделе [перемещение базы данных в эластичный пул](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span><span class="sxs-lookup"><span data-stu-id="e9762-113">toomove an existing database into an elastic pool, see [Move a database into an elastic pool](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span></span>

```PowerShell
New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

### <a name="complete-script"></a><span data-ttu-id="e9762-114">Полный скрипт</span><span class="sxs-lookup"><span data-stu-id="e9762-114">Complete script</span></span>
<span data-ttu-id="e9762-115">Этот скрипт создает группу ресурсов Azure и сервер.</span><span class="sxs-lookup"><span data-stu-id="e9762-115">This script creates an Azure resource group and a server.</span></span> <span data-ttu-id="e9762-116">При появлении запроса укажите имя пользователя администратора и пароль для нового сервера hello (не учетные данные Azure).</span><span class="sxs-lookup"><span data-stu-id="e9762-116">When prompted, supply an administrator username and password for hello new server (not your Azure credentials).</span></span>

```PowerShell
$subscriptionId = '<your Azure subscription id>'
$resourceGroupName = '<resource group name>'
$location = '<datacenter location>'
$serverName = '<server name>'
$poolName = '<pool name>'
$databaseName = '<database name>'

Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $serverName -Location $location -ServerVersion "12.0"
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $serverName -FirewallRuleName "rule1" -StartIpAddress "192.168.0.198" -EndIpAddress "192.168.0.199"

New-AzureRmSqlElasticPool -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100

New-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -ElasticPoolName $poolName -MaxSizeBytes 10GB
```

## <a name="create-an-elastic-pool-and-add-multiple-pooled-databases"></a><span data-ttu-id="e9762-117">Создание эластичного пула и добавление нескольких баз данных в пул</span><span class="sxs-lookup"><span data-stu-id="e9762-117">Create an elastic pool and add multiple pooled databases</span></span>
<span data-ttu-id="e9762-118">Создание много баз данных в пуле эластичных БД может занять время после завершения с помощью портала hello или командлеты PowerShell, одновременно создать только одну базу данных.</span><span class="sxs-lookup"><span data-stu-id="e9762-118">Creation of many databases in an elastic pool can take time when done using hello portal or PowerShell cmdlets that create only a single database at a time.</span></span> <span data-ttu-id="e9762-119">Создание tooautomate в пуле эластичных БД. в разделе [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span><span class="sxs-lookup"><span data-stu-id="e9762-119">tooautomate creation into an elastic pool, see [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="e9762-120">Перемещение базы данных в пул эластичных БД</span><span class="sxs-lookup"><span data-stu-id="e9762-120">Move a database into an elastic pool</span></span>
<span data-ttu-id="e9762-121">Можно переместить базу данных в таблицу или из пула эластичных БД с hello [AzureRmSqlDatabase набор](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span><span class="sxs-lookup"><span data-stu-id="e9762-121">You can move a database into or out of an elastic pool with hello [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span></span>

```PowerShell
Set-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="e9762-122">Изменение параметров производительности эластичного пула</span><span class="sxs-lookup"><span data-stu-id="e9762-122">Change performance settings of an elastic pool</span></span>
<span data-ttu-id="e9762-123">Если производительность снижается, можно изменять параметры hello hello пула tooaccommodate роста.</span><span class="sxs-lookup"><span data-stu-id="e9762-123">When performance suffers, you can change hello settings of hello pool tooaccommodate growth.</span></span> <span data-ttu-id="e9762-124">Используйте hello [AzureRmSqlElasticPool набор](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) командлета.</span><span class="sxs-lookup"><span data-stu-id="e9762-124">Use hello [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet.</span></span> <span data-ttu-id="e9762-125">Задайте параметр toohello hello - Dtu edtu, которое каждого пула.</span><span class="sxs-lookup"><span data-stu-id="e9762-125">Set hello -Dtu parameter toohello eDTUs per pool.</span></span> <span data-ttu-id="e9762-126">Возможные значения приведены в разделе [eDTU и размеры хранилища для эластичных баз данных и пулов эластичных баз данных](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span><span class="sxs-lookup"><span data-stu-id="e9762-126">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1” -Dtu 1200 -DatabaseDtuMax 100 -DatabaseDtuMin 50
```

## <a name="change-hello-storage-limit-for-an-elastic-pool"></a><span data-ttu-id="e9762-127">Изменить ограничение hello хранилища для эластичного пула</span><span class="sxs-lookup"><span data-stu-id="e9762-127">Change hello storage limit for an elastic pool</span></span>

<span data-ttu-id="e9762-128">Используйте hello [AzureRmSqlElasticPool набор](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) hello командлет tooset _- StorageMB_ параметра.</span><span class="sxs-lookup"><span data-stu-id="e9762-128">Use hello [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet tooset hello _-StorageMB_ parameter.</span></span> <span data-ttu-id="e9762-129">Укажите максимальный объем дискового пространства hello в МБ (например, 2097152 наборы hello хранилища ограничение too2 ТБ).</span><span class="sxs-lookup"><span data-stu-id="e9762-129">Provide hello storage limit in MB (for example, 2097152 sets hello storage limit too2 TB).</span></span> <span data-ttu-id="e9762-130">Возможные значения приведены в разделе [eDTU и размеры хранилища для эластичных баз данных и пулов эластичных баз данных](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span><span class="sxs-lookup"><span data-stu-id="e9762-130">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e9762-131">хранилища данных max по умолчанию Hello в пул для пулов Premium с edtu, которое 1500 доступна 750 ГБ.</span><span class="sxs-lookup"><span data-stu-id="e9762-131">hello default max data storage per pool for Premium pools with 1500 eDTUs or more is 750 GB.</span></span> <span data-ttu-id="e9762-132">выше hello tooobtain _максимальный размер хранилища данных на пул_, необходимо явно задать ограничение хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="e9762-132">tooobtain hello higher _max data storage size per pool_, hello storage limit must be explicitly set.</span></span> <span data-ttu-id="e9762-133">Пулы Premium с более 750 ГБ хранилища находится в общедоступной предварительной версии в hello следующие области: восточная часть США 2, Запад США, Вирджиния государственных организаций США, Западной Европе, Германия центра, Юго-Восточная Азия, восток Японии, Восточная Австралия, Канады центра и Восточная Канада.</span><span class="sxs-lookup"><span data-stu-id="e9762-133">Premium pools with more than 750 GB of storage is currently in public preview in hello following regions: East US 2, West US, US Gov Virginia, West Europe, Germany Central, Southeast Asia, Japan East, Australia East, Canada Central, and Canada East.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ServerName "server1" -ElasticPoolName “elasticpool1” -StorageMB 2097152
```

## <a name="get-hello-status-of-pool-operations"></a><span data-ttu-id="e9762-134">Получить состояние операции пула hello</span><span class="sxs-lookup"><span data-stu-id="e9762-134">Get hello status of pool operations</span></span>
<span data-ttu-id="e9762-135">Создание эластичного пула может занять некоторое время.</span><span class="sxs-lookup"><span data-stu-id="e9762-135">Creating an elastic pool can take time.</span></span> <span data-ttu-id="e9762-136">состояние пула операций, включая создание и обновления, используйте hello hello tootrack [Get AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) командлета.</span><span class="sxs-lookup"><span data-stu-id="e9762-136">tootrack hello status of pool operations including creation and updates, use hello [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlElasticPoolActivity -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1”
```

## <a name="get-hello-status-of-moving-a-database-into-and-out-of-an-elastic-pool"></a><span data-ttu-id="e9762-137">Получить состояние hello переход базы данных в пуле эластичных БД</span><span class="sxs-lookup"><span data-stu-id="e9762-137">Get hello status of moving a database into and out of an elastic pool</span></span>
<span data-ttu-id="e9762-138">На перемещение базы данных может потребоваться время.</span><span class="sxs-lookup"><span data-stu-id="e9762-138">Moving a database can take time.</span></span> <span data-ttu-id="e9762-139">Отслеживать состояние перемещения, с помощью hello [Get AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) командлета.</span><span class="sxs-lookup"><span data-stu-id="e9762-139">Track a move status using hello [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlDatabaseActivity -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="e9762-140">Получение данных об использовании ресурсов в эластичном пуле</span><span class="sxs-lookup"><span data-stu-id="e9762-140">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="e9762-141">Метрики, которые могут быть получены как процент от максимального пула ресурсов hello:</span><span class="sxs-lookup"><span data-stu-id="e9762-141">Metrics that can be retrieved as a percentage of hello resource pool limit:</span></span>

| <span data-ttu-id="e9762-142">Имя метрики</span><span class="sxs-lookup"><span data-stu-id="e9762-142">Metric name</span></span> | <span data-ttu-id="e9762-143">Описание</span><span class="sxs-lookup"><span data-stu-id="e9762-143">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9762-144">cpu\_percent</span><span class="sxs-lookup"><span data-stu-id="e9762-144">cpu\_percent</span></span> |<span data-ttu-id="e9762-145">Среднее вычислительной мощности в процентах от предела hello hello пула.</span><span class="sxs-lookup"><span data-stu-id="e9762-145">Average compute utilization in percentage of hello limit of hello pool.</span></span> |
| <span data-ttu-id="e9762-146">physical\_data\_read\_percent</span><span class="sxs-lookup"><span data-stu-id="e9762-146">physical\_data\_read\_percent</span></span> |<span data-ttu-id="e9762-147">Среднее использование операций ввода-вывода в процентах от предела hello hello пула.</span><span class="sxs-lookup"><span data-stu-id="e9762-147">Average I/O utilization in percentage based on hello limit of hello pool.</span></span> |
| <span data-ttu-id="e9762-148">log\_write\_percent</span><span class="sxs-lookup"><span data-stu-id="e9762-148">log\_write\_percent</span></span> |<span data-ttu-id="e9762-149">Среднее использование ресурсов записи в процентах от предела hello hello пула.</span><span class="sxs-lookup"><span data-stu-id="e9762-149">Average write resource utilization in percentage of hello limit of hello pool.</span></span> |
| <span data-ttu-id="e9762-150">DTU\_consumption\_percent</span><span class="sxs-lookup"><span data-stu-id="e9762-150">DTU\_consumption\_percent</span></span> |<span data-ttu-id="e9762-151">Использование среднего eDTU в процентах от предела eDTU hello в пуле</span><span class="sxs-lookup"><span data-stu-id="e9762-151">Average eDTU utilization in percentage of eDTU limit for hello pool</span></span> |
| <span data-ttu-id="e9762-152">storage\_percent</span><span class="sxs-lookup"><span data-stu-id="e9762-152">storage\_percent</span></span> |<span data-ttu-id="e9762-153">Среднее использование хранилища в процентах от hello ограничение хранилища пула hello.</span><span class="sxs-lookup"><span data-stu-id="e9762-153">Average storage utilization in percentage of hello storage limit of hello pool.</span></span> |
| <span data-ttu-id="e9762-154">workers\_percent</span><span class="sxs-lookup"><span data-stu-id="e9762-154">workers\_percent</span></span> |<span data-ttu-id="e9762-155">Максимальная одновременных рабочих процессов (запросов) в процентах от предела hello hello пула.</span><span class="sxs-lookup"><span data-stu-id="e9762-155">Maximum concurrent workers (requests) in percentage based on hello limit of hello pool.</span></span> |
| <span data-ttu-id="e9762-156">sessions\_percent</span><span class="sxs-lookup"><span data-stu-id="e9762-156">sessions\_percent</span></span> |<span data-ttu-id="e9762-157">Максимальное число одновременных сеансов в процентах от предела hello hello пула.</span><span class="sxs-lookup"><span data-stu-id="e9762-157">Maximum concurrent sessions in percentage based on hello limit of hello pool.</span></span> |
| <span data-ttu-id="e9762-158">eDTU_limit</span><span class="sxs-lookup"><span data-stu-id="e9762-158">eDTU_limit</span></span> |<span data-ttu-id="e9762-159">Текущее максимальное значение параметра DTU для этого пула эластичных БД в течение этого интервала.</span><span class="sxs-lookup"><span data-stu-id="e9762-159">Current max elastic pool DTU setting for this elastic pool during this interval.</span></span> |
| <span data-ttu-id="e9762-160">storage\_limit</span><span class="sxs-lookup"><span data-stu-id="e9762-160">storage\_limit</span></span> |<span data-ttu-id="e9762-161">Текущее максимальное значение размера хранилища в мегабайтах для этого пула эластичных БД в течение этого интервала.</span><span class="sxs-lookup"><span data-stu-id="e9762-161">Current max elastic pool storage limit setting for this elastic pool in megabytes during this interval.</span></span> |
| <span data-ttu-id="e9762-162">eDTU\_used</span><span class="sxs-lookup"><span data-stu-id="e9762-162">eDTU\_used</span></span> |<span data-ttu-id="e9762-163">Среднее число Edtu, занятый пулом hello в этот промежуток времени.</span><span class="sxs-lookup"><span data-stu-id="e9762-163">Average eDTUs used by hello pool in this interval.</span></span> |
| <span data-ttu-id="e9762-164">storage\_used</span><span class="sxs-lookup"><span data-stu-id="e9762-164">storage\_used</span></span> |<span data-ttu-id="e9762-165">Среднее хранилища, используемый пулом hello в этот промежуток времени, в байтах</span><span class="sxs-lookup"><span data-stu-id="e9762-165">Average storage used by hello pool in this interval in bytes</span></span> |

<span data-ttu-id="e9762-166">**Детализация показателей и сроки хранения:**</span><span class="sxs-lookup"><span data-stu-id="e9762-166">**Metrics granularity/retention periods:**</span></span>

* <span data-ttu-id="e9762-167">Детализация данных с точностью до 5 минут.</span><span class="sxs-lookup"><span data-stu-id="e9762-167">Data is returned at 5-minute granularity.</span></span>  
* <span data-ttu-id="e9762-168">Срок хранения данных — 35 дней.</span><span class="sxs-lookup"><span data-stu-id="e9762-168">Data retention is 35 days.</span></span>  

<span data-ttu-id="e9762-169">Этот командлет и API ограничивает hello число строк, которые могут быть извлечены в одном вызове too1000 строк (около 3 дня данных на уровне гранулярности 5 минут).</span><span class="sxs-lookup"><span data-stu-id="e9762-169">This cmdlet and API limits hello number of rows that can be retrieved in one call too1000 rows (about 3 days of data at 5-minute granularity).</span></span> <span data-ttu-id="e9762-170">Эта команда может вызываться несколько раз с tooretrieve интервалы времени различных начала и окончания больше данных, но</span><span class="sxs-lookup"><span data-stu-id="e9762-170">But this command can be called multiple times with different start/end time intervals tooretrieve more data</span></span>

<span data-ttu-id="e9762-171">метрики tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="e9762-171">tooretrieve hello metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/elasticPools/franchisepool -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="get-resource-usage-data-for-a-database-in-an-elastic-pool"></a><span data-ttu-id="e9762-172">Получение данных об использовании ресурсов для базы данных в эластичном пуле</span><span class="sxs-lookup"><span data-stu-id="e9762-172">Get resource usage data for a database in an elastic pool</span></span>
<span data-ttu-id="e9762-173">Эти API-интерфейсы так же, как hello API, используемые для наблюдения за использованием ресурсов hello одной базы данных, за исключением следующих семантической разницы hello hello: получить метрики выраженное в процентах hello на максимальное число Edtu базы данных (или эквивалентный cap для hello основной метрики, как ЦП или ввода-ВЫВОДА) установить для этого пула.</span><span class="sxs-lookup"><span data-stu-id="e9762-173">These APIs are hello same as hello APIs used for monitoring hello resource utilization of a single database, except for hello following semantic difference: metrics retrieved are expressed as a percentage of hello per database max eDTUs (or equivalent cap for hello underlying metric like CPU or IO) set for that pool.</span></span> <span data-ttu-id="e9762-174">Например 50% использования любой из этих метрик указывает конкретный ресурс потребления hello 50% от hello лимит cap базы данных для этого ресурса в hello родительского пула.</span><span class="sxs-lookup"><span data-stu-id="e9762-174">For example, 50% utilization of any of these metrics indicates that hello specific resource consumption is at 50% of hello per database cap limit for that resource in hello parent pool.</span></span>

<span data-ttu-id="e9762-175">метрики tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="e9762-175">tooretrieve hello metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/databases/myDB -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="add-an-alert-tooan-elastic-pool-resource"></a><span data-ttu-id="e9762-176">Добавление оповещений tooan эластичного пула ресурсов</span><span class="sxs-lookup"><span data-stu-id="e9762-176">Add an alert tooan elastic pool resource</span></span>
<span data-ttu-id="e9762-177">Можно добавить правила оповещения toosend эластичного пула tooan уведомления по электронной почте или создание предупреждений строки слишком[конечные точки URL-адрес](https://msdn.microsoft.com/library/mt718036.aspx) при эластичного пула hello достигает порогового значения использования, можно настроить.</span><span class="sxs-lookup"><span data-stu-id="e9762-177">You can add alert rules tooan elastic pool toosend email notifications or alert strings too[URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when hello elastic pool hits a utilization threshold that you set up.</span></span> <span data-ttu-id="e9762-178">С помощью командлета Add-AzureRmMetricAlertRule hello.</span><span class="sxs-lookup"><span data-stu-id="e9762-178">Use hello Add-AzureRmMetricAlertRule cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e9762-179">Для данных мониторинга использования ресурсов в эластичных пулах задержка как минимум 5 минут является нормальной.</span><span class="sxs-lookup"><span data-stu-id="e9762-179">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="e9762-180">Настройка интервала менее 10 минут для оповещений об эластичных пулах сейчас не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="e9762-180">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="e9762-181">Все оповещения, заданных для эластичных пулов с периодом (параметр с именем «-WindowSize» в PowerShell API) меньше, чем 10 минут может не запуститься.</span><span class="sxs-lookup"><span data-stu-id="e9762-181">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="e9762-182">Проследите, чтобы во всех оповещениях, определяемых для эластичных пулов, использовался интервал (WindowSize) не менее 10 минут.</span><span class="sxs-lookup"><span data-stu-id="e9762-182">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>
>

<span data-ttu-id="e9762-183">Этот пример добавляет оповещение, уведомляющее, когда потребление eDTU в эластичном пуле выходит за пределы определенного порогового значения.</span><span class="sxs-lookup"><span data-stu-id="e9762-183">This example adds an alert for getting notified when an elastic pool’s eDTU consumption goes above certain threshold.</span></span>

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location =  '<location'                         # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

#$Target Resource ID
$ResourceID = '/subscriptions/' + $subscriptionId + '/resourceGroups/' +$resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticpools/' + $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# create a unique rule name
$alertName = $poolName + "- DTU consumption rule"

# Create an alert rule for DTU_consumption_percent
Add-AzureRMMetricAlertRule -Name $alertName -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $ResourceID -MetricName "DTU_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail
```

<span data-ttu-id="e9762-184">Дополнительные сведения см. в статье [Создание оповещений для базы данных SQL Azure с помощью портала Azure](sql-database-insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e9762-184">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="add-alerts-tooall-databases-in-an-elastic-pool"></a><span data-ttu-id="e9762-185">Добавлять базы данных tooall оповещения в пуле эластичных БД</span><span class="sxs-lookup"><span data-stu-id="e9762-185">Add alerts tooall databases in an elastic pool</span></span>
<span data-ttu-id="e9762-186">Можно добавить правила оповещения tooall базы данных в эластичный пул toosend уведомления по электронной почте или предупреждения строки слишком[конечные точки URL-адрес](https://msdn.microsoft.com/library/mt718036.aspx) когда ресурс достигает порогового значения использования настроить предупреждения hello.</span><span class="sxs-lookup"><span data-stu-id="e9762-186">You can add alert rules tooall database in an elastic pool toosend email notifications or alert strings too[URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when a resource hits a utilization threshold set up by hello alert.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e9762-187">Для данных мониторинга использования ресурсов в эластичных пулах задержка как минимум 5 минут является нормальной.</span><span class="sxs-lookup"><span data-stu-id="e9762-187">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="e9762-188">Настройка интервала менее 10 минут для оповещений об эластичных пулах сейчас не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="e9762-188">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="e9762-189">Все оповещения, заданных для эластичных пулов с периодом (параметр с именем «-WindowSize» в PowerShell API) меньше, чем 10 минут может не запуститься.</span><span class="sxs-lookup"><span data-stu-id="e9762-189">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="e9762-190">Проследите, чтобы во всех оповещениях, определяемых для эластичных пулов, использовался интервал (WindowSize) не менее 10 минут.</span><span class="sxs-lookup"><span data-stu-id="e9762-190">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>

<span data-ttu-id="e9762-191">Этот пример добавляет предупреждения tooeach hello баз данных в пуле эластичных БД для получения уведомления, когда потребления DTU в этой базе данных выходит за пределы определенного порогового значения.</span><span class="sxs-lookup"><span data-stu-id="e9762-191">This example adds an alert tooeach of hello databases in an elastic pool for getting notified when that database’s DTU consumption goes above certain threshold.</span></span>

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location = '<location'                          # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

# Get hello list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# Get resource usage metrics for a database in an elastic pool for hello specified time interval.
foreach ($db in $dbList)
{
    $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName

    # create a unique rule name
    $alertName = $db.DatabaseName + "- DTU consumption rule"

    # Create an alert rule for DTU_consumption_percent
    Add-AzureRMMetricAlertRule -Name $alertName  -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $dbResourceId -MetricName "dtu_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail

    # drop hello alert rule
    #Remove-AzureRmAlertRule -ResourceGroup $resourceGroupName -Name $alertName
}
```

## <a name="collect-and-monitor-resource-usage-data-across-multiple-pools-in-a-subscription"></a><span data-ttu-id="e9762-192">Сбор и отслеживание данных об использовании ресурсов для нескольких пулов в подписке</span><span class="sxs-lookup"><span data-stu-id="e9762-192">Collect and monitor resource usage data across multiple pools in a subscription</span></span>
<span data-ttu-id="e9762-193">Когда имеется несколько баз данных в подписке, это сложно toomonitor каждого гибкому пул отдельно.</span><span class="sxs-lookup"><span data-stu-id="e9762-193">When you have many databases in a subscription, it is cumbersome toomonitor each elastic pool separately.</span></span> <span data-ttu-id="e9762-194">Вместо этого командлеты PowerShell для базы данных SQL и запросами T-SQL могут быть toocollect объединенных данных об использовании ресурсов несколько пулов и их базы данных для мониторинга и анализа использования ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e9762-194">Instead, SQL database PowerShell cmdlets and T-SQL queries can be combined toocollect resource usage data from multiple pools and their databases for monitoring and analysis of resource usage.</span></span> <span data-ttu-id="e9762-195">Объект [образец реализации](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) набора из powershell сценарии можно найти в репозитории примеров hello GitHub SQL Server вместе с документацией на действие и как toouse его.</span><span class="sxs-lookup"><span data-stu-id="e9762-195">A [sample implementation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) of such a set of powershell scripts can be found in hello GitHub SQL Server samples repository along with documentation on what it does and how toouse it.</span></span>

<span data-ttu-id="e9762-196">toouse этот образец реализации, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e9762-196">toouse this sample implementation, follow these steps.</span></span>

1. <span data-ttu-id="e9762-197">Загрузите hello [сценарии и документация](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span><span class="sxs-lookup"><span data-stu-id="e9762-197">Download hello [scripts and documentation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span></span>
2. <span data-ttu-id="e9762-198">Измените скрипты hello для вашей среды.</span><span class="sxs-lookup"><span data-stu-id="e9762-198">Modify hello scripts for your environment.</span></span> <span data-ttu-id="e9762-199">Укажите один или несколько серверов, на которых размещаются пулы эластичных баз данных.</span><span class="sxs-lookup"><span data-stu-id="e9762-199">Specify one or more servers on which elastic pools are hosted.</span></span>
3. <span data-ttu-id="e9762-200">Укажите базу данных телеметрии, где hello собранные показатели, toobe хранятся.</span><span class="sxs-lookup"><span data-stu-id="e9762-200">Specify a telemetry database where hello collected metrics are toobe stored.</span></span>
4. <span data-ttu-id="e9762-201">Настройте hello toospecify сценария hello продолжительность выполнения скриптов hello.</span><span class="sxs-lookup"><span data-stu-id="e9762-201">Customize hello script toospecify hello duration of hello scripts' execution.</span></span>

<span data-ttu-id="e9762-202">На высоком уровне сценарии hello hello следующие:</span><span class="sxs-lookup"><span data-stu-id="e9762-202">At a high level, hello scripts do hello following:</span></span>

* <span data-ttu-id="e9762-203">перечисляют все серверы в указанной подписке Azure (или в указанном списке серверов);</span><span class="sxs-lookup"><span data-stu-id="e9762-203">Enumerates all servers in a given Azure subscription (or a specified list of servers).</span></span>
* <span data-ttu-id="e9762-204">запускают фоновое задание для каждого сервера.</span><span class="sxs-lookup"><span data-stu-id="e9762-204">Runs a background job for each server.</span></span> <span data-ttu-id="e9762-205">Hello задание выполняется в цикле через регулярные интервалы и собирает данные телеметрии для всех пулов hello в hello server.</span><span class="sxs-lookup"><span data-stu-id="e9762-205">hello job runs in a loop at regular intervals and collects telemetry data for all hello pools in hello server.</span></span> <span data-ttu-id="e9762-206">Затем она загружает hello собранные данные в базу данных указанного телеметрии hello.</span><span class="sxs-lookup"><span data-stu-id="e9762-206">It then loads hello collected data into hello specified telemetry database.</span></span>
* <span data-ttu-id="e9762-207">Перечисляет список баз данных в каждом пуле toocollect hello базы данных данные об использовании ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e9762-207">Enumerates a list of databases in each pool toocollect hello database resource usage data.</span></span> <span data-ttu-id="e9762-208">Затем она загружает hello собранные данные в базу данных телеметрии hello.</span><span class="sxs-lookup"><span data-stu-id="e9762-208">It then loads hello collected data into hello telemetry database.</span></span>

<span data-ttu-id="e9762-209">Hello собранных метрики телеметрии базы данных hello может быть проанализировано toomonitor hello исправности эластичные пулы и hello базы данных в ней.</span><span class="sxs-lookup"><span data-stu-id="e9762-209">hello collected metrics in hello telemetry database can be analyzed toomonitor hello health of elastic pools and hello databases in it.</span></span> <span data-ttu-id="e9762-210">Hello скрипт устанавливает предварительно определенных возвращающей табличное значение функции (TVF) hello метрики телеметрии базы данных toohelp статистические hello для указанного интервала времени.</span><span class="sxs-lookup"><span data-stu-id="e9762-210">hello script also installs a pre-defined Table-Value function (TVF) in hello telemetry database toohelp aggregate hello metrics for a specified time window.</span></span> <span data-ttu-id="e9762-211">Например, результаты hello возвращающей табличное значение функции можно использовать tooshow «первые N пулах эластичных БД с загрузкой максимального числа eDTU hello в за заданный период времени.»</span><span class="sxs-lookup"><span data-stu-id="e9762-211">For example, results of hello TVF can be used tooshow “top N elastic pools with hello maximum eDTU utilization in a given time window.”</span></span> <span data-ttu-id="e9762-212">При необходимости использовать аналитические средства, такие как Excel или Power BI tooquery и анализа hello собранных данных.</span><span class="sxs-lookup"><span data-stu-id="e9762-212">Optionally, use analytic tools like Excel or Power BI tooquery and analyze hello collected data.</span></span>

### <a name="example-retrieve-resource-consumption-metrics-for-an-elastic-pool-and-its-databases"></a><span data-ttu-id="e9762-213">Пример. Получение метрик потребления ресурсов в эластичном пуле и его базах данных</span><span class="sxs-lookup"><span data-stu-id="e9762-213">Example: retrieve resource consumption metrics for an elastic pool and its databases</span></span>
<span data-ttu-id="e9762-214">В этом примере извлекается hello метрики потребления для данного пула эластичных БД и все его базы данных.</span><span class="sxs-lookup"><span data-stu-id="e9762-214">This example retrieves hello consumption metrics for a given elastic pool and all its databases.</span></span> <span data-ttu-id="e9762-215">Собранные данные форматируются и записываются в файл CSV-файл tooa.</span><span class="sxs-lookup"><span data-stu-id="e9762-215">Collected data is formatted and written tooa .csv formatted file.</span></span> <span data-ttu-id="e9762-216">Hello файл можно просмотреть с помощью Excel.</span><span class="sxs-lookup"><span data-stu-id="e9762-216">hello file can be browsed with Excel.</span></span>

```PowerShell
$subscriptionId = '<Azure subscription id>'          # Azure subscription ID
$resourceGroupName = '<resource group name>'             # Resource Group
$serverName = <server name>                              # server name
$poolName = <elastic pool name>                          # pool name

# Login tooAzure account and select hello subscription.
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

# Get resource usage metrics for an elastic pool for hello specified time interval.
$startTime = '4/27/2016 00:00:00'  # start time in UTC
$endTime = '4/27/2016 01:00:00'    # end time in UTC

# Construct hello pool resource ID and retrive pool metrics at 5-minute granularity.
$poolResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticPools/' + $poolName
$poolMetrics = (Get-AzureRmMetric -ResourceId $poolResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)

# Get hello list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Get resource usage metrics for a database in an elastic pool for hello specified time interval.
$dbMetrics = @()
foreach ($db in $dbList)
{
     $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName
     $dbMetrics = $dbMetrics + (Get-AzureRmMetric -ResourceId $dbResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)
}

#Optionally you can format hello metrics and output as .csv file using hello following script block.
$command = {
param($metricList, $outputFile)

# Format metrics into a table.
$table = @()
foreach($metric in $metricList) {
   foreach($metricValue in $metric.MetricValues) {
      $sx = New-Object PSObject -Property @{
      Timestamp = $metricValue.Timestamp.ToString()
      MetricName = $metric.Name;
      Average = $metricValue.Average;
      ResourceID = $metric.ResourceId
   }$table = $table += $sx
   }
}

# Output hello metrics into a .csv file.
write-output $table | Export-csv -Path $outputFile -Append -NoTypeInformation
}

# Format and output pool metrics
Invoke-Command -ScriptBlock $command -ArgumentList $poolMetrics,c:\temp\poolmetrics.csv

# Format and output database metrics
Invoke-Command -ScriptBlock $command -ArgumentList $dbMetrics,c:\temp\dbmetrics.csv
```

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="e9762-217">Задержка операций эластичного пула</span><span class="sxs-lookup"><span data-stu-id="e9762-217">Latency of elastic pool operations</span></span>
* <span data-ttu-id="e9762-218">Изменение hello min edtu, которое каждой базы данных или максимальное число Edtu на базу данных обычно завершает более 5 минут.</span><span class="sxs-lookup"><span data-stu-id="e9762-218">Changing hello min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="e9762-219">Изменение hello число Edtu на пул, зависит от hello общий объем пространства, используемого всех баз данных в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="e9762-219">Changing hello eDTUs per pool depends on hello total amount of space used by all databases in hello pool.</span></span> <span data-ttu-id="e9762-220">Изменение занимает порядка 90 минут или меньше на каждые 100 ГБ.</span><span class="sxs-lookup"><span data-stu-id="e9762-220">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="e9762-221">Например если hello общее пространство, занимаемое всех баз данных в пуле hello составляет 200 ГБ, то hello ожидаемого задержка для изменения hello eDTU пула на пул — 3 часа или менее.</span><span class="sxs-lookup"><span data-stu-id="e9762-221">For example, if hello total space used by all databases in hello pool is 200 GB, then hello expected latency for changing hello pool eDTU per pool is 3 hours or less.</span></span>



## <a name="next-steps"></a><span data-ttu-id="e9762-222">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e9762-222">Next steps</span></span>
* <span data-ttu-id="e9762-223">[Создать эластичный задания](sql-database-elastic-jobs-overview.md) эластичной заданий позволяют выполняться любое количество баз данных в пуле hello скриптов T-SQL.</span><span class="sxs-lookup"><span data-stu-id="e9762-223">[Create elastic jobs](sql-database-elastic-jobs-overview.md) Elastic jobs let you run T-SQL scripts against any number of databases in hello pool.</span></span>
* <span data-ttu-id="e9762-224">В разделе [горизонтального масштабирования с базой данных SQL Azure](sql-database-elastic-scale-introduction.md): использовать эластичной средства tooscale out, перемещение данных, запроса или создания транзакции.</span><span class="sxs-lookup"><span data-stu-id="e9762-224">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic tools tooscale out, move data, query, or create transactions.</span></span>
