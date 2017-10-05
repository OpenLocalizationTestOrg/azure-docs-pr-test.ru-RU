---
title: "PowerShell: создание эластичного пула SQL Azure и управление им | Документация Майкрософт"
description: "Узнайте, как управлять пулом эластичных баз данных с помощью PowerShell."
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
ms.openlocfilehash: 5e76397c62e5a6ff7fb356bd81218c307f3fda31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-an-elastic-pool-with-powershell"></a><span data-ttu-id="961fe-103">Создание эластичного пула и управление им с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="961fe-103">Create and manage an elastic pool with PowerShell</span></span>
<span data-ttu-id="961fe-104">В этой статье показано, как с помощью PowerShell создавать масштабируемые [эластичные пулы](sql-database-elastic-pool.md) и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="961fe-104">This topic shows you how to create and manage scalable [elastic pools](sql-database-elastic-pool.md) with PowerShell.</span></span>  <span data-ttu-id="961fe-105">Для создания эластичных пулов Azure и управления ими можно также использовать [портал Azure](https://portal.azure.com/), REST API или [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="961fe-105">You can also create and manage an Azure elastic pool using the [Azure portal](https://portal.azure.com/), REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="961fe-106">Вы также можете использовать [Transact-SQL](sql-database-elastic-pool-manage-tsql.md), чтобы создавать новые базы данных в эластичных пулах и перемещать базы данных в пулы и обратно.</span><span class="sxs-lookup"><span data-stu-id="961fe-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

[!INCLUDE [Start your PowerShell session](../../includes/sql-database-powershell.md)]

## <a name="create-an-elastic-pool"></a><span data-ttu-id="961fe-107">Создание эластичного пула</span><span class="sxs-lookup"><span data-stu-id="961fe-107">Create an elastic pool</span></span>
<span data-ttu-id="961fe-108">Эластичный пул создается с помощью командлета [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool).</span><span class="sxs-lookup"><span data-stu-id="961fe-108">The [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet creates an elastic pool.</span></span> <span data-ttu-id="961fe-109">Значения eDTU на пул, а также минимальные и максимальные значения DTU ограничены значением уровня службы ("Базовый", "Стандартный", "Премиум" или "Премиум RS").</span><span class="sxs-lookup"><span data-stu-id="961fe-109">The values for eDTU per pool, min, and max DTUs are constrained by the service tier value (Basic, Standard, Premium, or Premium RS).</span></span> <span data-ttu-id="961fe-110">См. раздел [eDTU и размеры хранилища для пулов эластичных БД](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span><span class="sxs-lookup"><span data-stu-id="961fe-110">See [eDTU and storage limits for elastic pools and pooled databases](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span></span>

```PowerShell
New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100
```

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="961fe-111">Создание базы данных внутри эластичного пула</span><span class="sxs-lookup"><span data-stu-id="961fe-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="961fe-112">Используйте командлет [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) и укажите целевой пул в качестве параметра **ElasticPoolName**.</span><span class="sxs-lookup"><span data-stu-id="961fe-112">Use the [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet and set the **ElasticPoolName** parameter to the target pool.</span></span> <span data-ttu-id="961fe-113">Сведения о перемещении существующей базы данных в эластичный пул см. в разделе [Перемещение базы данных в пул эластичных БД](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span><span class="sxs-lookup"><span data-stu-id="961fe-113">To move an existing database into an elastic pool, see [Move a database into an elastic pool](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span></span>

```PowerShell
New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

### <a name="complete-script"></a><span data-ttu-id="961fe-114">Полный скрипт</span><span class="sxs-lookup"><span data-stu-id="961fe-114">Complete script</span></span>
<span data-ttu-id="961fe-115">Этот скрипт создает группу ресурсов Azure и сервер.</span><span class="sxs-lookup"><span data-stu-id="961fe-115">This script creates an Azure resource group and a server.</span></span> <span data-ttu-id="961fe-116">При появлении запроса укажите имя и пароль пользователя-администратора для нового сервера (не свои учетные данные Azure).</span><span class="sxs-lookup"><span data-stu-id="961fe-116">When prompted, supply an administrator username and password for the new server (not your Azure credentials).</span></span>

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

## <a name="create-an-elastic-pool-and-add-multiple-pooled-databases"></a><span data-ttu-id="961fe-117">Создание эластичного пула и добавление нескольких баз данных в пул</span><span class="sxs-lookup"><span data-stu-id="961fe-117">Create an elastic pool and add multiple pooled databases</span></span>
<span data-ttu-id="961fe-118">Создание большого количества баз данных в эластичном пуле может занять некоторое время, если эта операция выполняется с помощью портала или командлетов PowerShell, которые создают базы данных поочередно.</span><span class="sxs-lookup"><span data-stu-id="961fe-118">Creation of many databases in an elastic pool can take time when done using the portal or PowerShell cmdlets that create only a single database at a time.</span></span> <span data-ttu-id="961fe-119">Сведения об автоматическом создании баз данных в эластичном пуле см. в документе [CreateOrUpdateElasticPoolAndPopulate](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span><span class="sxs-lookup"><span data-stu-id="961fe-119">To automate creation into an elastic pool, see [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="961fe-120">Перемещение базы данных в пул эластичных БД</span><span class="sxs-lookup"><span data-stu-id="961fe-120">Move a database into an elastic pool</span></span>
<span data-ttu-id="961fe-121">Переместить базу данных в эластичный пул или из него можно с помощью командлета [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span><span class="sxs-lookup"><span data-stu-id="961fe-121">You can move a database into or out of an elastic pool with the [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span></span>

```PowerShell
Set-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="961fe-122">Изменение параметров производительности эластичного пула</span><span class="sxs-lookup"><span data-stu-id="961fe-122">Change performance settings of an elastic pool</span></span>
<span data-ttu-id="961fe-123">Если производительность недостаточна, можно изменить параметры пула в соответствии с ростом нагрузки.</span><span class="sxs-lookup"><span data-stu-id="961fe-123">When performance suffers, you can change the settings of the pool to accommodate growth.</span></span> <span data-ttu-id="961fe-124">Используйте командлет [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span><span class="sxs-lookup"><span data-stu-id="961fe-124">Use the [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet.</span></span> <span data-ttu-id="961fe-125">Присвойте параметру -Dtu значение eDTU, выделяемых на пул.</span><span class="sxs-lookup"><span data-stu-id="961fe-125">Set the -Dtu parameter to the eDTUs per pool.</span></span> <span data-ttu-id="961fe-126">Возможные значения приведены в разделе [eDTU и размеры хранилища для эластичных баз данных и пулов эластичных баз данных](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span><span class="sxs-lookup"><span data-stu-id="961fe-126">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1” -Dtu 1200 -DatabaseDtuMax 100 -DatabaseDtuMin 50
```

## <a name="change-the-storage-limit-for-an-elastic-pool"></a><span data-ttu-id="961fe-127">Изменение предельного размера хранилища для эластичного пула</span><span class="sxs-lookup"><span data-stu-id="961fe-127">Change the storage limit for an elastic pool</span></span>

<span data-ttu-id="961fe-128">Используйте командлет [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool), чтобы задать параметр _-StorageMB_.</span><span class="sxs-lookup"><span data-stu-id="961fe-128">Use the [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet to set the _-StorageMB_ parameter.</span></span> <span data-ttu-id="961fe-129">Укажите максимальный объем хранилища в мегабайтах (например, если указать значение 2097152, будет задан объем 2 ТБ).</span><span class="sxs-lookup"><span data-stu-id="961fe-129">Provide the storage limit in MB (for example, 2097152 sets the storage limit to 2 TB).</span></span> <span data-ttu-id="961fe-130">Возможные значения приведены в разделе [eDTU и размеры хранилища для эластичных баз данных и пулов эластичных баз данных](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span><span class="sxs-lookup"><span data-stu-id="961fe-130">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="961fe-131">По умолчанию максимальный объем хранилища данных на пул для пулов уровня "Премиум" с 1500 eDTU или больше равен 750 ГБ.</span><span class="sxs-lookup"><span data-stu-id="961fe-131">The default max data storage per pool for Premium pools with 1500 eDTUs or more is 750 GB.</span></span> <span data-ttu-id="961fe-132">Чтобы увеличить _максимальный объем хранилища данных на пул_, необходимо явно задать предельный размер хранилища.</span><span class="sxs-lookup"><span data-stu-id="961fe-132">To obtain the higher _max data storage size per pool_, the storage limit must be explicitly set.</span></span> <span data-ttu-id="961fe-133">Сейчас пулы уровня "Премиум" с объемом хранилища свыше 750 ГБ доступны в общедоступной предварительной версии в следующих регионах: восточная часть США 2, западная часть США, Виргиния (для обслуживания государственных организаций США), Западная Европа, Центральная Германия, Юго-Восточная Азия, восточная Япония, восточная Австралия, Центральная Канада и Восточная Канада.</span><span class="sxs-lookup"><span data-stu-id="961fe-133">Premium pools with more than 750 GB of storage is currently in public preview in the following regions: East US 2, West US, US Gov Virginia, West Europe, Germany Central, Southeast Asia, Japan East, Australia East, Canada Central, and Canada East.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ServerName "server1" -ElasticPoolName “elasticpool1” -StorageMB 2097152
```

## <a name="get-the-status-of-pool-operations"></a><span data-ttu-id="961fe-134">Получение состояния операций пула</span><span class="sxs-lookup"><span data-stu-id="961fe-134">Get the status of pool operations</span></span>
<span data-ttu-id="961fe-135">Создание эластичного пула может занять некоторое время.</span><span class="sxs-lookup"><span data-stu-id="961fe-135">Creating an elastic pool can take time.</span></span> <span data-ttu-id="961fe-136">Отслеживать состояние операций пула, включая создание и обновление, можно с помощью командлета [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity).</span><span class="sxs-lookup"><span data-stu-id="961fe-136">To track the status of pool operations including creation and updates, use the [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlElasticPoolActivity -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1”
```

## <a name="get-the-status-of-moving-a-database-into-and-out-of-an-elastic-pool"></a><span data-ttu-id="961fe-137">Получение состояния перемещения базы данных в эластичный пул и из него</span><span class="sxs-lookup"><span data-stu-id="961fe-137">Get the status of moving a database into and out of an elastic pool</span></span>
<span data-ttu-id="961fe-138">На перемещение базы данных может потребоваться время.</span><span class="sxs-lookup"><span data-stu-id="961fe-138">Moving a database can take time.</span></span> <span data-ttu-id="961fe-139">Отслеживать состояние перемещения можно с помощью командлета [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity).</span><span class="sxs-lookup"><span data-stu-id="961fe-139">Track a move status using the [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlDatabaseActivity -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="961fe-140">Получение данных об использовании ресурсов в эластичном пуле</span><span class="sxs-lookup"><span data-stu-id="961fe-140">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="961fe-141">Показатели, которые могут быть возвращены в виде процента от предельного значения пула ресурсов:</span><span class="sxs-lookup"><span data-stu-id="961fe-141">Metrics that can be retrieved as a percentage of the resource pool limit:</span></span>

| <span data-ttu-id="961fe-142">Имя метрики</span><span class="sxs-lookup"><span data-stu-id="961fe-142">Metric name</span></span> | <span data-ttu-id="961fe-143">Описание</span><span class="sxs-lookup"><span data-stu-id="961fe-143">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="961fe-144">cpu\_percent</span><span class="sxs-lookup"><span data-stu-id="961fe-144">cpu\_percent</span></span> |<span data-ttu-id="961fe-145">Среднее использование вычислительных ресурсов в процентах от предела пула.</span><span class="sxs-lookup"><span data-stu-id="961fe-145">Average compute utilization in percentage of the limit of the pool.</span></span> |
| <span data-ttu-id="961fe-146">physical\_data\_read\_percent</span><span class="sxs-lookup"><span data-stu-id="961fe-146">physical\_data\_read\_percent</span></span> |<span data-ttu-id="961fe-147">Среднее использование ввода-вывода в процентах от предела пула.</span><span class="sxs-lookup"><span data-stu-id="961fe-147">Average I/O utilization in percentage based on the limit of the pool.</span></span> |
| <span data-ttu-id="961fe-148">log\_write\_percent</span><span class="sxs-lookup"><span data-stu-id="961fe-148">log\_write\_percent</span></span> |<span data-ttu-id="961fe-149">Среднее использование записи ресурсов в процентах от предела пула.</span><span class="sxs-lookup"><span data-stu-id="961fe-149">Average write resource utilization in percentage of the limit of the pool.</span></span> |
| <span data-ttu-id="961fe-150">DTU\_consumption\_percent</span><span class="sxs-lookup"><span data-stu-id="961fe-150">DTU\_consumption\_percent</span></span> |<span data-ttu-id="961fe-151">Среднее использование eDTU в процентах от предела пула.</span><span class="sxs-lookup"><span data-stu-id="961fe-151">Average eDTU utilization in percentage of eDTU limit for the pool</span></span> |
| <span data-ttu-id="961fe-152">storage\_percent</span><span class="sxs-lookup"><span data-stu-id="961fe-152">storage\_percent</span></span> |<span data-ttu-id="961fe-153">Среднее использование хранилища в процентах от предела пула.</span><span class="sxs-lookup"><span data-stu-id="961fe-153">Average storage utilization in percentage of the storage limit of the pool.</span></span> |
| <span data-ttu-id="961fe-154">workers\_percent</span><span class="sxs-lookup"><span data-stu-id="961fe-154">workers\_percent</span></span> |<span data-ttu-id="961fe-155">Максимальное число одновременных рабочих ролей (запросов) в процентах от предела пула.</span><span class="sxs-lookup"><span data-stu-id="961fe-155">Maximum concurrent workers (requests) in percentage based on the limit of the pool.</span></span> |
| <span data-ttu-id="961fe-156">sessions\_percent</span><span class="sxs-lookup"><span data-stu-id="961fe-156">sessions\_percent</span></span> |<span data-ttu-id="961fe-157">Максимальное число одновременных сеансов в процентах от предела пула.</span><span class="sxs-lookup"><span data-stu-id="961fe-157">Maximum concurrent sessions in percentage based on the limit of the pool.</span></span> |
| <span data-ttu-id="961fe-158">eDTU_limit</span><span class="sxs-lookup"><span data-stu-id="961fe-158">eDTU_limit</span></span> |<span data-ttu-id="961fe-159">Текущее максимальное значение параметра DTU для этого пула эластичных БД в течение этого интервала.</span><span class="sxs-lookup"><span data-stu-id="961fe-159">Current max elastic pool DTU setting for this elastic pool during this interval.</span></span> |
| <span data-ttu-id="961fe-160">storage\_limit</span><span class="sxs-lookup"><span data-stu-id="961fe-160">storage\_limit</span></span> |<span data-ttu-id="961fe-161">Текущее максимальное значение размера хранилища в мегабайтах для этого пула эластичных БД в течение этого интервала.</span><span class="sxs-lookup"><span data-stu-id="961fe-161">Current max elastic pool storage limit setting for this elastic pool in megabytes during this interval.</span></span> |
| <span data-ttu-id="961fe-162">eDTU\_used</span><span class="sxs-lookup"><span data-stu-id="961fe-162">eDTU\_used</span></span> |<span data-ttu-id="961fe-163">Среднее число eDTU, использованных пулом на этом интервале.</span><span class="sxs-lookup"><span data-stu-id="961fe-163">Average eDTUs used by the pool in this interval.</span></span> |
| <span data-ttu-id="961fe-164">storage\_used</span><span class="sxs-lookup"><span data-stu-id="961fe-164">storage\_used</span></span> |<span data-ttu-id="961fe-165">Средняя емкость хранилища, использованная пулом на этом интервале.</span><span class="sxs-lookup"><span data-stu-id="961fe-165">Average storage used by the pool in this interval in bytes</span></span> |

<span data-ttu-id="961fe-166">**Детализация показателей и сроки хранения:**</span><span class="sxs-lookup"><span data-stu-id="961fe-166">**Metrics granularity/retention periods:**</span></span>

* <span data-ttu-id="961fe-167">Детализация данных с точностью до 5 минут.</span><span class="sxs-lookup"><span data-stu-id="961fe-167">Data is returned at 5-minute granularity.</span></span>  
* <span data-ttu-id="961fe-168">Срок хранения данных — 35 дней.</span><span class="sxs-lookup"><span data-stu-id="961fe-168">Data retention is 35 days.</span></span>  

<span data-ttu-id="961fe-169">Этот командлет и API-интерфейс ограничивают количество строк, которые могут быть получены за один вызов, до 1000 строк (данные приблизительно за 3 дня при детализации с точностью до 5 минут).</span><span class="sxs-lookup"><span data-stu-id="961fe-169">This cmdlet and API limits the number of rows that can be retrieved in one call to 1000 rows (about 3 days of data at 5-minute granularity).</span></span> <span data-ttu-id="961fe-170">Однако эта команда может быть вызвана несколько раз с различными начальным и конечным интервалами, чтобы получить дополнительные данные.</span><span class="sxs-lookup"><span data-stu-id="961fe-170">But this command can be called multiple times with different start/end time intervals to retrieve more data</span></span>

<span data-ttu-id="961fe-171">Вот как можно получить метрики.</span><span class="sxs-lookup"><span data-stu-id="961fe-171">To retrieve the metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/elasticPools/franchisepool -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="get-resource-usage-data-for-a-database-in-an-elastic-pool"></a><span data-ttu-id="961fe-172">Получение данных об использовании ресурсов для базы данных в эластичном пуле</span><span class="sxs-lookup"><span data-stu-id="961fe-172">Get resource usage data for a database in an elastic pool</span></span>
<span data-ttu-id="961fe-173">Эти API-интерфейсы совпадают с текущими API-интерфейсами, используемыми для мониторинга использования ресурсов отдельной базой данных, за исключением следующего семантического различия: полученные метрики выражаются в процентах от максимального количества eDTU для каждой базы данных (или в виде эквивалентного предельного значения для базовой метрики, такой как производительность ЦП или операции ввода-вывода), установленного для данного пула.</span><span class="sxs-lookup"><span data-stu-id="961fe-173">These APIs are the same as the APIs used for monitoring the resource utilization of a single database, except for the following semantic difference: metrics retrieved are expressed as a percentage of the per database max eDTUs (or equivalent cap for the underlying metric like CPU or IO) set for that pool.</span></span> <span data-ttu-id="961fe-174">Например, загрузка в 50 % для любого из этих показателей указывает, что потребление данного ресурса составляет 50 % от предельного значения потребления этого ресурса на одну базу данных для этого ресурса в родительском пуле.</span><span class="sxs-lookup"><span data-stu-id="961fe-174">For example, 50% utilization of any of these metrics indicates that the specific resource consumption is at 50% of the per database cap limit for that resource in the parent pool.</span></span>

<span data-ttu-id="961fe-175">Вот как можно получить метрики.</span><span class="sxs-lookup"><span data-stu-id="961fe-175">To retrieve the metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/databases/myDB -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="add-an-alert-to-an-elastic-pool-resource"></a><span data-ttu-id="961fe-176">Добавление оповещения для ресурса эластичного пула</span><span class="sxs-lookup"><span data-stu-id="961fe-176">Add an alert to an elastic pool resource</span></span>
<span data-ttu-id="961fe-177">Для эластичного пула можно добавить правила генерации оповещений, чтобы отправлять по электронной почте уведомления или строки оповещения в [конечные точки URL-адресов](https://msdn.microsoft.com/library/mt718036.aspx), когда эластичный пул достигает заданного порогового значения использования.</span><span class="sxs-lookup"><span data-stu-id="961fe-177">You can add alert rules to an elastic pool to send email notifications or alert strings to [URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when the elastic pool hits a utilization threshold that you set up.</span></span> <span data-ttu-id="961fe-178">Используйте командлет Add-AzureRmMetricAlertRule.</span><span class="sxs-lookup"><span data-stu-id="961fe-178">Use the Add-AzureRmMetricAlertRule cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="961fe-179">Для данных мониторинга использования ресурсов в эластичных пулах задержка как минимум 5 минут является нормальной.</span><span class="sxs-lookup"><span data-stu-id="961fe-179">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="961fe-180">Настройка интервала менее 10 минут для оповещений об эластичных пулах сейчас не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="961fe-180">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="961fe-181">Все оповещения, заданных для эластичных пулов с периодом (параметр с именем «-WindowSize» в PowerShell API) меньше, чем 10 минут может не запуститься.</span><span class="sxs-lookup"><span data-stu-id="961fe-181">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="961fe-182">Проследите, чтобы во всех оповещениях, определяемых для эластичных пулов, использовался интервал (WindowSize) не менее 10 минут.</span><span class="sxs-lookup"><span data-stu-id="961fe-182">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>
>

<span data-ttu-id="961fe-183">Этот пример добавляет оповещение, уведомляющее, когда потребление eDTU в эластичном пуле выходит за пределы определенного порогового значения.</span><span class="sxs-lookup"><span data-stu-id="961fe-183">This example adds an alert for getting notified when an elastic pool’s eDTU consumption goes above certain threshold.</span></span>

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

<span data-ttu-id="961fe-184">Дополнительные сведения см. в статье [Создание оповещений для базы данных SQL Azure с помощью портала Azure](sql-database-insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="961fe-184">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="add-alerts-to-all-databases-in-an-elastic-pool"></a><span data-ttu-id="961fe-185">Добавление оповещений для всех баз данных в эластичном пуле</span><span class="sxs-lookup"><span data-stu-id="961fe-185">Add alerts to all databases in an elastic pool</span></span>
<span data-ttu-id="961fe-186">Для всех баз данных в пуле эластичных БД можно добавить правила генерации оповещений, чтобы отправлять по электронной почте уведомления или строки оповещения в [конечные точки URL-адресов](https://msdn.microsoft.com/library/mt718036.aspx) , когда ресурс достигает порогового значения использования, определенного в оповещении.</span><span class="sxs-lookup"><span data-stu-id="961fe-186">You can add alert rules to all database in an elastic pool to send email notifications or alert strings to [URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when a resource hits a utilization threshold set up by the alert.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="961fe-187">Для данных мониторинга использования ресурсов в эластичных пулах задержка как минимум 5 минут является нормальной.</span><span class="sxs-lookup"><span data-stu-id="961fe-187">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="961fe-188">Настройка интервала менее 10 минут для оповещений об эластичных пулах сейчас не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="961fe-188">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="961fe-189">Все оповещения, заданных для эластичных пулов с периодом (параметр с именем «-WindowSize» в PowerShell API) меньше, чем 10 минут может не запуститься.</span><span class="sxs-lookup"><span data-stu-id="961fe-189">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="961fe-190">Проследите, чтобы во всех оповещениях, определяемых для эластичных пулов, использовался интервал (WindowSize) не менее 10 минут.</span><span class="sxs-lookup"><span data-stu-id="961fe-190">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>

<span data-ttu-id="961fe-191">Этот пример добавляет оповещение для каждой базы данных в эластичном пуле, которое уведомляет, когда потребление DTU в этой базе данных превышает определенное пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="961fe-191">This example adds an alert to each of the databases in an elastic pool for getting notified when that database’s DTU consumption goes above certain threshold.</span></span>

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location = '<location'                          # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

# Get the list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# Get resource usage metrics for a database in an elastic pool for the specified time interval.
foreach ($db in $dbList)
{
    $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName

    # create a unique rule name
    $alertName = $db.DatabaseName + "- DTU consumption rule"

    # Create an alert rule for DTU_consumption_percent
    Add-AzureRMMetricAlertRule -Name $alertName  -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $dbResourceId -MetricName "dtu_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail

    # drop the alert rule
    #Remove-AzureRmAlertRule -ResourceGroup $resourceGroupName -Name $alertName
}
```

## <a name="collect-and-monitor-resource-usage-data-across-multiple-pools-in-a-subscription"></a><span data-ttu-id="961fe-192">Сбор и отслеживание данных об использовании ресурсов для нескольких пулов в подписке</span><span class="sxs-lookup"><span data-stu-id="961fe-192">Collect and monitor resource usage data across multiple pools in a subscription</span></span>
<span data-ttu-id="961fe-193">Если в вашей подписке много баз данных, отслеживать отдельно каждый эластичный пул становится затруднительно.</span><span class="sxs-lookup"><span data-stu-id="961fe-193">When you have many databases in a subscription, it is cumbersome to monitor each elastic pool separately.</span></span> <span data-ttu-id="961fe-194">Вместо этого с помощью командлетов PowerShell базы данных SQL и запросов T-SQL можно собирать данные об использовании ресурсов по нескольким пулам и базам данных. Это упрощает мониторинг и анализ использования ресурсов.</span><span class="sxs-lookup"><span data-stu-id="961fe-194">Instead, SQL database PowerShell cmdlets and T-SQL queries can be combined to collect resource usage data from multiple pools and their databases for monitoring and analysis of resource usage.</span></span> <span data-ttu-id="961fe-195">В репозитории примеров для SQL Server на сайте GitHub вы найдете [пример реализации](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) набора сценариев PowerShell вместе с документацией по назначению и методам использования этого набора.</span><span class="sxs-lookup"><span data-stu-id="961fe-195">A [sample implementation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) of such a set of powershell scripts can be found in the GitHub SQL Server samples repository along with documentation on what it does and how to use it.</span></span>

<span data-ttu-id="961fe-196">Чтобы использовать этот пример реализации, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="961fe-196">To use this sample implementation, follow these steps.</span></span>

1. <span data-ttu-id="961fe-197">Скачайте [сценарии и документацию](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools).</span><span class="sxs-lookup"><span data-stu-id="961fe-197">Download the [scripts and documentation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span></span>
2. <span data-ttu-id="961fe-198">Измените скрипты, указав параметры своей среды.</span><span class="sxs-lookup"><span data-stu-id="961fe-198">Modify the scripts for your environment.</span></span> <span data-ttu-id="961fe-199">Укажите один или несколько серверов, на которых размещаются пулы эластичных баз данных.</span><span class="sxs-lookup"><span data-stu-id="961fe-199">Specify one or more servers on which elastic pools are hosted.</span></span>
3. <span data-ttu-id="961fe-200">Укажите базу данных телеметрии, где будут храниться собранные метрики.</span><span class="sxs-lookup"><span data-stu-id="961fe-200">Specify a telemetry database where the collected metrics are to be stored.</span></span>
4. <span data-ttu-id="961fe-201">Укажите лимит времени на выполнение скриптов.</span><span class="sxs-lookup"><span data-stu-id="961fe-201">Customize the script to specify the duration of the scripts' execution.</span></span>

<span data-ttu-id="961fe-202">Основные действия, которые выполняют эти скрипты:</span><span class="sxs-lookup"><span data-stu-id="961fe-202">At a high level, the scripts do the following:</span></span>

* <span data-ttu-id="961fe-203">перечисляют все серверы в указанной подписке Azure (или в указанном списке серверов);</span><span class="sxs-lookup"><span data-stu-id="961fe-203">Enumerates all servers in a given Azure subscription (or a specified list of servers).</span></span>
* <span data-ttu-id="961fe-204">запускают фоновое задание для каждого сервера.</span><span class="sxs-lookup"><span data-stu-id="961fe-204">Runs a background job for each server.</span></span> <span data-ttu-id="961fe-205">Задание выполняется в цикле через регулярные интервалы и собирает данные телеметрии для всех пулов на сервере.</span><span class="sxs-lookup"><span data-stu-id="961fe-205">The job runs in a loop at regular intervals and collects telemetry data for all the pools in the server.</span></span> <span data-ttu-id="961fe-206">Затем собранные данные загружаются в указанную базу данных телеметрии;</span><span class="sxs-lookup"><span data-stu-id="961fe-206">It then loads the collected data into the specified telemetry database.</span></span>
* <span data-ttu-id="961fe-207">перечисляют список баз данных в каждом пуле, чтобы собрать данные об использовании ресурсов базы данных.</span><span class="sxs-lookup"><span data-stu-id="961fe-207">Enumerates a list of databases in each pool to collect the database resource usage data.</span></span> <span data-ttu-id="961fe-208">Затем собранные данные загружаются в базу данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="961fe-208">It then loads the collected data into the telemetry database.</span></span>

<span data-ttu-id="961fe-209">Собранные в базе данных телеметрии метрики можно анализировать для контроля состояния пулов эластичных баз данных и входящих в них баз данных.</span><span class="sxs-lookup"><span data-stu-id="961fe-209">The collected metrics in the telemetry database can be analyzed to monitor the health of elastic pools and the databases in it.</span></span> <span data-ttu-id="961fe-210">Также скрипт определяет в базе данных телеметрии функцию, возвращающую табличное значение, которая помогает обрабатывать значения метрик за указанный интервал времени.</span><span class="sxs-lookup"><span data-stu-id="961fe-210">The script also installs a pre-defined Table-Value function (TVF) in the telemetry database to help aggregate the metrics for a specified time window.</span></span> <span data-ttu-id="961fe-211">Например, с помощью этой функции можно отобразить N эластичных пулов с максимальной загрузкой eDTU за заданный период.</span><span class="sxs-lookup"><span data-stu-id="961fe-211">For example, results of the TVF can be used to show “top N elastic pools with the maximum eDTU utilization in a given time window.”</span></span> <span data-ttu-id="961fe-212">Также вы можете использовать для получения и анализа собранных данных любой аналитический инструмент, например Excel или Power BI.</span><span class="sxs-lookup"><span data-stu-id="961fe-212">Optionally, use analytic tools like Excel or Power BI to query and analyze the collected data.</span></span>

### <a name="example-retrieve-resource-consumption-metrics-for-an-elastic-pool-and-its-databases"></a><span data-ttu-id="961fe-213">Пример. Получение метрик потребления ресурсов в эластичном пуле и его базах данных</span><span class="sxs-lookup"><span data-stu-id="961fe-213">Example: retrieve resource consumption metrics for an elastic pool and its databases</span></span>
<span data-ttu-id="961fe-214">В этом примере извлекаются метрики потребления для данного пула эластичных БД и всех его баз данных.</span><span class="sxs-lookup"><span data-stu-id="961fe-214">This example retrieves the consumption metrics for a given elastic pool and all its databases.</span></span> <span data-ttu-id="961fe-215">Собранные данные форматируются и записываются в CSV-файл.</span><span class="sxs-lookup"><span data-stu-id="961fe-215">Collected data is formatted and written to a .csv formatted file.</span></span> <span data-ttu-id="961fe-216">Этот файл можно просмотреть в Excel.</span><span class="sxs-lookup"><span data-stu-id="961fe-216">The file can be browsed with Excel.</span></span>

```PowerShell
$subscriptionId = '<Azure subscription id>'          # Azure subscription ID
$resourceGroupName = '<resource group name>'             # Resource Group
$serverName = <server name>                              # server name
$poolName = <elastic pool name>                          # pool name

# Login to Azure account and select the subscription.
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

# Get resource usage metrics for an elastic pool for the specified time interval.
$startTime = '4/27/2016 00:00:00'  # start time in UTC
$endTime = '4/27/2016 01:00:00'    # end time in UTC

# Construct the pool resource ID and retrive pool metrics at 5-minute granularity.
$poolResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticPools/' + $poolName
$poolMetrics = (Get-AzureRmMetric -ResourceId $poolResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)

# Get the list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Get resource usage metrics for a database in an elastic pool for the specified time interval.
$dbMetrics = @()
foreach ($db in $dbList)
{
     $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName
     $dbMetrics = $dbMetrics + (Get-AzureRmMetric -ResourceId $dbResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)
}

#Optionally you can format the metrics and output as .csv file using the following script block.
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

# Output the metrics into a .csv file.
write-output $table | Export-csv -Path $outputFile -Append -NoTypeInformation
}

# Format and output pool metrics
Invoke-Command -ScriptBlock $command -ArgumentList $poolMetrics,c:\temp\poolmetrics.csv

# Format and output database metrics
Invoke-Command -ScriptBlock $command -ArgumentList $dbMetrics,c:\temp\dbmetrics.csv
```

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="961fe-217">Задержка операций эластичного пула</span><span class="sxs-lookup"><span data-stu-id="961fe-217">Latency of elastic pool operations</span></span>
* <span data-ttu-id="961fe-218">Изменение минимального или максимального числа eDTU для базы данных обычно завершается за 5 минут.</span><span class="sxs-lookup"><span data-stu-id="961fe-218">Changing the min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="961fe-219">Изменение числа eDTU на пул зависит от общей емкости, используемой всеми базами данных в пуле.</span><span class="sxs-lookup"><span data-stu-id="961fe-219">Changing the eDTUs per pool depends on the total amount of space used by all databases in the pool.</span></span> <span data-ttu-id="961fe-220">Изменение занимает порядка 90 минут или меньше на каждые 100 ГБ.</span><span class="sxs-lookup"><span data-stu-id="961fe-220">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="961fe-221">Например, если общее пространство, используемое всеми базами данных в пуле, равно 200 ГБ, то ожидаемая задержка при изменении числа eDTU для пула составит до 3 часов.</span><span class="sxs-lookup"><span data-stu-id="961fe-221">For example, if the total space used by all databases in the pool is 200 GB, then the expected latency for changing the pool eDTU per pool is 3 hours or less.</span></span>



## <a name="next-steps"></a><span data-ttu-id="961fe-222">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="961fe-222">Next steps</span></span>
* <span data-ttu-id="961fe-223">[Управление масштабируемыми облачными базами данных](sql-database-elastic-jobs-overview.md). Задания обработки для эластичных баз данных упрощают выполнение сценариев T-SQL для любого количества баз данных в пуле.</span><span class="sxs-lookup"><span data-stu-id="961fe-223">[Create elastic jobs](sql-database-elastic-jobs-overview.md) Elastic jobs let you run T-SQL scripts against any number of databases in the pool.</span></span>
* <span data-ttu-id="961fe-224">См. статью [Развертывание с помощью базы данных SQL Azure](sql-database-elastic-scale-introduction.md). В ней описывается использование инструментов эластичной базы данных для развертывания, перемещения данных, выполнения запросов и создания транзакций.</span><span class="sxs-lookup"><span data-stu-id="961fe-224">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic tools to scale out, move data, query, or create transactions.</span></span>
