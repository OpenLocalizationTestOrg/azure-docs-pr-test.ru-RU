---
title: "Управление вычислительными ресурсами в хранилище данных SQL Azure (PowerShell) | Документация Майкрософт"
description: "Задачи PowerShell для управления вычислительными ресурсами. Масштабирование вычислительных ресурсов путем изменения числа единиц DWU. Кроме того, можно приостанавливать и возобновлять работу вычислительных ресурсов для сокращения затрат."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 8354a3c1-4e04-4809-933f-db414a8c74dc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 6a185d96447c2e1b0b463439dd062081e783da5f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="94172-105">Управление вычислительными ресурсами в хранилище данных SQL Azure (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="94172-105">Manage compute power in Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="94172-106">Обзор</span><span class="sxs-lookup"><span data-stu-id="94172-106">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="94172-107">Портал</span><span class="sxs-lookup"><span data-stu-id="94172-107">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="94172-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="94172-108">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="94172-109">REST</span><span class="sxs-lookup"><span data-stu-id="94172-109">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="94172-110">TSQL</span><span class="sxs-lookup"><span data-stu-id="94172-110">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

## <a name="before-you-begin"></a><span data-ttu-id="94172-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="94172-111">Before you begin</span></span>
### <a name="install-the-latest-version-of-azure-powershell"></a><span data-ttu-id="94172-112">Установка последней версии Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="94172-112">Install the latest version of Azure PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="94172-113">Чтобы использовать Azure PowerShell с хранилищем данных SQL, установите Azure PowerShell 1.0.3 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="94172-113">To use Azure PowerShell with SQL Data Warehouse, you need Azure PowerShell version 1.0.3 or greater.</span></span>  <span data-ttu-id="94172-114">Чтобы узнать текущую версию, выполните команду **Get-Module -ListAvailable -Name Azure**.</span><span class="sxs-lookup"><span data-stu-id="94172-114">To verify your current version run the command **Get-Module -ListAvailable -Name Azure**.</span></span> <span data-ttu-id="94172-115">Последнюю версию можно установить с помощью [установщика веб-платформы Майкрософт][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="94172-115">You can install the latest version from [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="94172-116">Дополнительные сведения см. в статье [Установка и настройка служб Azure PowerShell][How to install and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="94172-116">For more information, see [How to install and configure Azure PowerShell][How to install and configure Azure PowerShell].</span></span>
>
> 

### <a name="get-started-with-azure-powershell-cmdlets"></a><span data-ttu-id="94172-117">Приступая к работе с командлетами Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="94172-117">Get started with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="94172-118">Чтобы начать работу:</span><span class="sxs-lookup"><span data-stu-id="94172-118">To get started:</span></span>

1. <span data-ttu-id="94172-119">Откройте Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="94172-119">Open Azure PowerShell.</span></span>
2. <span data-ttu-id="94172-120">В командной строке PowerShell выполните приведенные далее команды, чтобы войти в Azure Resource Manager Azure и выбрать свою подписку.</span><span class="sxs-lookup"><span data-stu-id="94172-120">At the PowerShell prompt, run these commands to sign in to the Azure Resource Manager and select your subscription.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a><span data-ttu-id="94172-121">Масштабирование вычислительных ресурсов</span><span class="sxs-lookup"><span data-stu-id="94172-121">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="94172-122">Чтобы изменить число единиц DWU, используйте командлет PowerShell [Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="94172-122">To change the DWUs, use the [Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase] PowerShell cmdlet.</span></span> <span data-ttu-id="94172-123">В приведенном ниже примере для базы данных MySQLDW, размещенной на сервере MyServer, устанавливается цель уровня обслуживания DW1000.</span><span class="sxs-lookup"><span data-stu-id="94172-123">The following example sets the service level objective to DW1000 for the database MySQLDW which is hosted on server MyServer.</span></span>

```Powershell
Set-AzureRmSqlDatabase -DatabaseName "MySQLDW" -ServerName "MyServer" -RequestedServiceObjectiveName "DW1000"
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="94172-124">Приостановка работы вычислительных ресурсов</span><span class="sxs-lookup"><span data-stu-id="94172-124">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="94172-125">Чтобы приостановить работу базы данных, используйте командлет [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="94172-125">To pause a database, use the [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase] cmdlet.</span></span> <span data-ttu-id="94172-126">В приведенном ниже примере приостанавливается работа базы данных с именем Database02, размещенной на сервере с именем Server01.</span><span class="sxs-lookup"><span data-stu-id="94172-126">The following example pauses a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="94172-127">Сервер находится в группе ресурсов Azure с именем ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="94172-127">The server is in an Azure resource group named ResourceGroup1.</span></span>

> [!NOTE]
> <span data-ttu-id="94172-128">Обратите внимание, что если вашим сервером является foo.database.windows.net, в командлетах PowerShell в качестве -ServerName используйте значение "foo".</span><span class="sxs-lookup"><span data-stu-id="94172-128">Note that if your server is foo.database.windows.net, use "foo" as the -ServerName in the PowerShell cmdlets.</span></span>
>
> 

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
```
<span data-ttu-id="94172-129">В следующем примере, являющемся вариантом предыдущего, база данных извлекается в объект $database.</span><span class="sxs-lookup"><span data-stu-id="94172-129">A variation, this next example retrieves the database into the $database object.</span></span> <span data-ttu-id="94172-130">Затем объект передается по конвейеру в командлет [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="94172-130">It then pipes the object to [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span></span> <span data-ttu-id="94172-131">Результаты сохраняются в объекте resultDatabase.</span><span class="sxs-lookup"><span data-stu-id="94172-131">The results are stored in the object resultDatabase.</span></span> <span data-ttu-id="94172-132">Последняя команда отображает результаты.</span><span class="sxs-lookup"><span data-stu-id="94172-132">The final command shows the results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="94172-133">Возобновление работы вычислительных ресурсов</span><span class="sxs-lookup"><span data-stu-id="94172-133">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="94172-134">Чтобы запустить базу данных, используйте командлет [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="94172-134">To start a database, use the [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] cmdlet.</span></span> <span data-ttu-id="94172-135">В приведенном ниже примере запускается база данных с именем Database02, размещенная на сервере с именем Server01.</span><span class="sxs-lookup"><span data-stu-id="94172-135">The following example starts a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="94172-136">Сервер находится в группе ресурсов Azure с именем ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="94172-136">The server is in an Azure resource group named ResourceGroup1.</span></span>

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" -DatabaseName "Database02"
```

<span data-ttu-id="94172-137">В следующем примере, являющемся вариантом предыдущего, база данных извлекается в объект $database.</span><span class="sxs-lookup"><span data-stu-id="94172-137">A variation, this next example retrieves the database into the $database object.</span></span> <span data-ttu-id="94172-138">Затем объект передается в командлет [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase], и результаты сохраняются в объекте $resultDatabase.</span><span class="sxs-lookup"><span data-stu-id="94172-138">It then pipes the object to [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] and stores the results in $resultDatabase.</span></span> <span data-ttu-id="94172-139">Последняя команда отображает результаты.</span><span class="sxs-lookup"><span data-stu-id="94172-139">The final command shows the results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
$resultDatabase
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="94172-140">Проверка состояния базы данных</span><span class="sxs-lookup"><span data-stu-id="94172-140">Check database state</span></span>

<span data-ttu-id="94172-141">Как показано в приведенных выше примерах, командлет [Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase] можно использовать, чтобы получить сведения о базе данных, тем самым проверив ее состояние, но также его можно использовать в качестве аргумента.</span><span class="sxs-lookup"><span data-stu-id="94172-141">As shown in the above examples, one can use [Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase] cmdlet to get information on a database, thereby checking the status, but also to use as an argument.</span></span> 

```powershell
Get-AzureRmSqlDatabase [-ResourceGroupName] <String> [-ServerName] <String> [[-DatabaseName] <String>]
 [-InformationAction <ActionPreference>] [-InformationVariable <String>] [-Confirm] [-WhatIf]
 [<CommonParameters>]
```

<span data-ttu-id="94172-142">Ниже приведен пример результата при таком использовании.</span><span class="sxs-lookup"><span data-stu-id="94172-142">Which will result in something like</span></span> 

```powershell   
ResourceGroupName             : nytrg
ServerName                    : nytsvr
DatabaseName                  : nytdb
Location                      : West US
DatabaseId                    : 86461aae-8e3d-4ded-9389-ac9d4bc69bbb
Edition                       : DataWarehouse
CollationName                 : SQL_Latin1General_CP1CI_AS
CatalogCollation              :
MaxSizeBytes                  : 32212254720
Status                        : Online
CreationDate                  : 10/26/2016 4:33:14 PM
CurrentServiceObjectiveId     : 620323bf-2879-4807-b30d-c2e6d7b3b3aa
CurrentServiceObjectiveName   : System2
RequestedServiceObjectiveId   : 620323bf-2879-4807-b30d-c2e6d7b3b3aa
RequestedServiceObjectiveName :
ElasticPoolName               :
EarliestRestoreDate           : 1/1/0001 12:00:00 AM
```

<span data-ttu-id="94172-143">В котором можно проверить *Status* (Состояние) базы данных.</span><span class="sxs-lookup"><span data-stu-id="94172-143">Where you can then check to see the *Status* of the database.</span></span> <span data-ttu-id="94172-144">Как видите, в этом случае база данных находится в сети (Online).</span><span class="sxs-lookup"><span data-stu-id="94172-144">In this case, you can see that this database is online.</span></span> 

<span data-ttu-id="94172-145">При выполнении этой команды должно отобразиться одно из следующих значений состояния: "Online" (В сети), "Pausing" (Приостановка), "Resuming" (Возобновление), "Scaling" (Масштабирование) и "Paused" (Приостановлена).</span><span class="sxs-lookup"><span data-stu-id="94172-145">When you run this command, you should receive a Status value of either Online, Pausing, Resuming, Scaling, and Paused.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="94172-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="94172-146">Next steps</span></span>
<span data-ttu-id="94172-147">Сведения о других задачах управления см. в статье [Управление базами данных в хранилище данных SQL Azure][Management overview].</span><span class="sxs-lookup"><span data-stu-id="94172-147">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[How to install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->
[Resume-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619347.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Get-AzureRmSqlDatabase]: /powershell/servicemanagement/azure.sqldatabase/v1.6.1/get-azuresqldatabase

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[Azure portal]: http://portal.azure.com/
