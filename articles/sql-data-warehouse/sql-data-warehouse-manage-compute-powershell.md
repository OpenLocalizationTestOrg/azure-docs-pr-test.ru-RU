---
title: "aaaManage вычислительная мощность в хранилище данных SQL Azure (PowerShell) | Документы Microsoft"
description: "PowerShell задачи toomanage вычислительной мощности. Масштабирование вычислительных ресурсов путем изменения числа единиц DWU. Или, приостанавливать и возобновлять toosave затраты вычислительных ресурсов."
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
ms.openlocfilehash: 8b379d4cf89570649767f6896d2c630d4f1111d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="52588-105">Управление вычислительными ресурсами в хранилище данных SQL Azure (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="52588-105">Manage compute power in Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="52588-106">Обзор</span><span class="sxs-lookup"><span data-stu-id="52588-106">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="52588-107">Портал</span><span class="sxs-lookup"><span data-stu-id="52588-107">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="52588-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="52588-108">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="52588-109">REST</span><span class="sxs-lookup"><span data-stu-id="52588-109">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="52588-110">TSQL</span><span class="sxs-lookup"><span data-stu-id="52588-110">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

## <a name="before-you-begin"></a><span data-ttu-id="52588-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="52588-111">Before you begin</span></span>
### <a name="install-hello-latest-version-of-azure-powershell"></a><span data-ttu-id="52588-112">Установите последнюю версию Azure PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="52588-112">Install hello latest version of Azure PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="52588-113">toouse Azure PowerShell с хранилищем данных SQL необходимо Azure PowerShell версия 1.0.3 или выше.</span><span class="sxs-lookup"><span data-stu-id="52588-113">toouse Azure PowerShell with SQL Data Warehouse, you need Azure PowerShell version 1.0.3 or greater.</span></span>  <span data-ttu-id="52588-114">tooverify текущей версии выполните команду hello **Get-Module - ListAvailable-Name Azure**.</span><span class="sxs-lookup"><span data-stu-id="52588-114">tooverify your current version run hello command **Get-Module -ListAvailable -Name Azure**.</span></span> <span data-ttu-id="52588-115">Можно установить последнюю версию hello с [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="52588-115">You can install hello latest version from [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="52588-116">Дополнительные сведения см. в разделе [как tooinstall и настройка Azure PowerShell][How tooinstall and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="52588-116">For more information, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>
>
> 

### <a name="get-started-with-azure-powershell-cmdlets"></a><span data-ttu-id="52588-117">Приступая к работе с командлетами Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="52588-117">Get started with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="52588-118">tooget работы.</span><span class="sxs-lookup"><span data-stu-id="52588-118">tooget started:</span></span>

1. <span data-ttu-id="52588-119">Откройте Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="52588-119">Open Azure PowerShell.</span></span>
2. <span data-ttu-id="52588-120">В командной строке PowerShell hello запустите эти команды toosign в toohello диспетчера ресурсов Azure и выберите подписку.</span><span class="sxs-lookup"><span data-stu-id="52588-120">At hello PowerShell prompt, run these commands toosign in toohello Azure Resource Manager and select your subscription.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a><span data-ttu-id="52588-121">Масштабирование вычислительных ресурсов</span><span class="sxs-lookup"><span data-stu-id="52588-121">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="52588-122">hello toochange Dwu, использовать hello [набор AzureRmSqlDatabase] [ Set-AzureRmSqlDatabase] командлета PowerShell.</span><span class="sxs-lookup"><span data-stu-id="52588-122">toochange hello DWUs, use hello [Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase] PowerShell cmdlet.</span></span> <span data-ttu-id="52588-123">Hello следующем примере hello службы уровня цели tooDW1000 для базы данных hello MySQLDW, который размещается на сервере MyServer.</span><span class="sxs-lookup"><span data-stu-id="52588-123">hello following example sets hello service level objective tooDW1000 for hello database MySQLDW which is hosted on server MyServer.</span></span>

```Powershell
Set-AzureRmSqlDatabase -DatabaseName "MySQLDW" -ServerName "MyServer" -RequestedServiceObjectiveName "DW1000"
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="52588-124">Приостановка работы вычислительных ресурсов</span><span class="sxs-lookup"><span data-stu-id="52588-124">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="52588-125">toopause базы данных, используйте hello [Suspend AzureRmSqlDatabase] [ Suspend-AzureRmSqlDatabase] командлета.</span><span class="sxs-lookup"><span data-stu-id="52588-125">toopause a database, use hello [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase] cmdlet.</span></span> <span data-ttu-id="52588-126">Hello следующем примере показана Приостановка базы данных с именем Database02, размещенный на сервере с именем Server01.</span><span class="sxs-lookup"><span data-stu-id="52588-126">hello following example pauses a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="52588-127">Hello сервер находится в группе ресурсов Azure с именем ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="52588-127">hello server is in an Azure resource group named ResourceGroup1.</span></span>

> [!NOTE]
> <span data-ttu-id="52588-128">Обратите внимание, что если сервер является foo.database.windows.net, используйте «foo» как hello - ServerName в командлеты PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="52588-128">Note that if your server is foo.database.windows.net, use "foo" as hello -ServerName in hello PowerShell cmdlets.</span></span>
>
> 

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
```
<span data-ttu-id="52588-129">Вариант, в следующем примере извлекает hello базы данных в hello $database объекта.</span><span class="sxs-lookup"><span data-stu-id="52588-129">A variation, this next example retrieves hello database into hello $database object.</span></span> <span data-ttu-id="52588-130">Затем он передает hello объекта слишком[Suspend AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="52588-130">It then pipes hello object too[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span></span> <span data-ttu-id="52588-131">Hello результаты сохраняются в resultDatabase hello объекта.</span><span class="sxs-lookup"><span data-stu-id="52588-131">hello results are stored in hello object resultDatabase.</span></span> <span data-ttu-id="52588-132">Последняя команда Hello показывает результаты hello.</span><span class="sxs-lookup"><span data-stu-id="52588-132">hello final command shows hello results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="52588-133">Возобновление работы вычислительных ресурсов</span><span class="sxs-lookup"><span data-stu-id="52588-133">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="52588-134">toostart базы данных, используйте hello [Resume AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] командлета.</span><span class="sxs-lookup"><span data-stu-id="52588-134">toostart a database, use hello [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] cmdlet.</span></span> <span data-ttu-id="52588-135">Hello следующий пример запускает базы данных с именем Database02, размещенный на сервере с именем Server01.</span><span class="sxs-lookup"><span data-stu-id="52588-135">hello following example starts a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="52588-136">Hello сервер находится в группе ресурсов Azure с именем ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="52588-136">hello server is in an Azure resource group named ResourceGroup1.</span></span>

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" -DatabaseName "Database02"
```

<span data-ttu-id="52588-137">Вариант, в следующем примере извлекает hello базы данных в hello $database объекта.</span><span class="sxs-lookup"><span data-stu-id="52588-137">A variation, this next example retrieves hello database into hello $database object.</span></span> <span data-ttu-id="52588-138">Затем он передает hello объекта слишком[Resume AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] и сохраняет результаты hello в $resultDatabase.</span><span class="sxs-lookup"><span data-stu-id="52588-138">It then pipes hello object too[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] and stores hello results in $resultDatabase.</span></span> <span data-ttu-id="52588-139">Последняя команда Hello показывает результаты hello.</span><span class="sxs-lookup"><span data-stu-id="52588-139">hello final command shows hello results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
$resultDatabase
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="52588-140">Проверка состояния базы данных</span><span class="sxs-lookup"><span data-stu-id="52588-140">Check database state</span></span>

<span data-ttu-id="52588-141">Как показано в hello выше примерах, можно использовать [Get AzureRmSqlDatabase] [ Get-AzureRmSqlDatabase] командлет tooget сведения из базы данных, тем самым Проверка состояния hello, но toouse в качестве аргумента.</span><span class="sxs-lookup"><span data-stu-id="52588-141">As shown in hello above examples, one can use [Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase] cmdlet tooget information on a database, thereby checking hello status, but also toouse as an argument.</span></span> 

```powershell
Get-AzureRmSqlDatabase [-ResourceGroupName] <String> [-ServerName] <String> [[-DatabaseName] <String>]
 [-InformationAction <ActionPreference>] [-InformationVariable <String>] [-Confirm] [-WhatIf]
 [<CommonParameters>]
```

<span data-ttu-id="52588-142">Ниже приведен пример результата при таком использовании.</span><span class="sxs-lookup"><span data-stu-id="52588-142">Which will result in something like</span></span> 

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

<span data-ttu-id="52588-143">Которой затем можно проверить toosee hello *состояние* hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="52588-143">Where you can then check toosee hello *Status* of hello database.</span></span> <span data-ttu-id="52588-144">Как видите, в этом случае база данных находится в сети (Online).</span><span class="sxs-lookup"><span data-stu-id="52588-144">In this case, you can see that this database is online.</span></span> 

<span data-ttu-id="52588-145">При выполнении этой команды должно отобразиться одно из следующих значений состояния: "Online" (В сети), "Pausing" (Приостановка), "Resuming" (Возобновление), "Scaling" (Масштабирование) и "Paused" (Приостановлена).</span><span class="sxs-lookup"><span data-stu-id="52588-145">When you run this command, you should receive a Status value of either Online, Pausing, Resuming, Scaling, and Paused.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="52588-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="52588-146">Next steps</span></span>
<span data-ttu-id="52588-147">Сведения о других задачах управления см. в статье [Управление базами данных в хранилище данных SQL Azure][Management overview].</span><span class="sxs-lookup"><span data-stu-id="52588-147">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->
[Resume-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619347.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Get-AzureRmSqlDatabase]: /powershell/servicemanagement/azure.sqldatabase/v1.6.1/get-azuresqldatabase

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[Azure portal]: http://portal.azure.com/
