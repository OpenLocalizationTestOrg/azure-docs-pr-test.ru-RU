---
title: "Восстановление хранилища данных SQL Azure (PowerShell) | Документация Майкрософт"
description: "Задачи PowerShell для восстановления хранилища данных SQL."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: ac62f154-c8b0-4c33-9c42-f480808aa1d2
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: 6286c0e682bae2d3bf0435a25b8077a53b117b25
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="restore-an-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="b45ef-103">Восстановление хранилища данных SQL Azure (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="b45ef-103">Restore an Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="b45ef-104">[Обзор][Overview]</span><span class="sxs-lookup"><span data-stu-id="b45ef-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="b45ef-105">[Портал][Portal]</span><span class="sxs-lookup"><span data-stu-id="b45ef-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="b45ef-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="b45ef-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="b45ef-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="b45ef-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="b45ef-108">Из этой статьи вы узнаете, как восстановить хранилище данных SQL Azure с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b45ef-108">In this article you will learn how to restore an Azure SQL Data Warehouse using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b45ef-109">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="b45ef-109">Before you begin</span></span>
<span data-ttu-id="b45ef-110">**Проверьте ресурсы DTU.**</span><span class="sxs-lookup"><span data-stu-id="b45ef-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="b45ef-111">Каждое хранилище данных SQL размещается на сервере SQL Server (например, myserver.database.windows.net), которому выделена квота DTU по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b45ef-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="b45ef-112">Перед восстановлением хранилища данных SQL убедитесь, что у сервера SQL Server осталась достаточная квота DTU для восстанавливаемой базы данных.</span><span class="sxs-lookup"><span data-stu-id="b45ef-112">Before you can restore a SQL Data Warehouse, verify that the your SQL server has enough remaining DTU quota for the database being restored.</span></span> <span data-ttu-id="b45ef-113">Чтобы узнать, как вычислить необходимое количество DTU или запросить дополнительные единицы DTU, ознакомьтесь с разделом [Создание запроса в службу поддержки][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="b45ef-113">To learn how to calculate DTU needed or to request more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="b45ef-114">Установка PowerShell</span><span class="sxs-lookup"><span data-stu-id="b45ef-114">Install PowerShell</span></span>
<span data-ttu-id="b45ef-115">Чтобы использовать Azure PowerShell с хранилищем данных SQL, установите Azure PowerShell 1.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="b45ef-115">In order to use Azure PowerShell with SQL Data Warehouse, you will need to install Azure PowerShell version 1.0 or greater.</span></span>  <span data-ttu-id="b45ef-116">Чтобы узнать текущую версию, выполните командлет **Get-Module -ListAvailable -Name AzureRM**.</span><span class="sxs-lookup"><span data-stu-id="b45ef-116">You can check your version by running **Get-Module -ListAvailable -Name AzureRM**.</span></span>  <span data-ttu-id="b45ef-117">Последнюю версию можно установить с помощью [установщика веб-платформы Майкрософт][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="b45ef-117">The latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="b45ef-118">Дополнительные сведения об установке последней версии Azure PowerShell см. в статье [Как установить и настроить Azure PowerShell][How to install and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="b45ef-118">For more information on installing the latest version, see [How to install and configure Azure PowerShell][How to install and configure Azure PowerShell].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="b45ef-119">Восстановление активной или приостановленной базы данных</span><span class="sxs-lookup"><span data-stu-id="b45ef-119">Restore an active or paused database</span></span>
<span data-ttu-id="b45ef-120">Для восстановления базы данных из моментального снимка используйте командлет PowerShell [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="b45ef-120">To restore a database from a snapshot use the [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] PowerShell cmdlet.</span></span>

1. <span data-ttu-id="b45ef-121">Откройте Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b45ef-121">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="b45ef-122">Подключитесь к своей учетной записи Azure и выведите список всех подписок, связанных с ней.</span><span class="sxs-lookup"><span data-stu-id="b45ef-122">Connect to your Azure account and list all the subscriptions associated with your account.</span></span>
3. <span data-ttu-id="b45ef-123">Выберите подписку, содержащую базу данных, которую нужно восстановить.</span><span class="sxs-lookup"><span data-stu-id="b45ef-123">Select the subscription that contains the database to be restored.</span></span>
4. <span data-ttu-id="b45ef-124">Выведите список точек восстановления для базы данных.</span><span class="sxs-lookup"><span data-stu-id="b45ef-124">List the restore points for the database.</span></span>
5. <span data-ttu-id="b45ef-125">Выберите нужные точки восстановления с помощью свойства RestorePointCreationDate.</span><span class="sxs-lookup"><span data-stu-id="b45ef-125">Pick the desired restore point using the RestorePointCreationDate.</span></span>
6. <span data-ttu-id="b45ef-126">Восстановите базу данных в желаемой точке восстановления.</span><span class="sxs-lookup"><span data-stu-id="b45ef-126">Restore the database to the desired restore point.</span></span>
7. <span data-ttu-id="b45ef-127">Убедитесь, что восстановленная база данных подключена к сети.</span><span class="sxs-lookup"><span data-stu-id="b45ef-127">Verify that the restored database is online.</span></span>

```Powershell

$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# List the last 10 database restore points
((Get-AzureRMSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName ($DatabaseName).RestorePointCreationDate)[-10 .. -1]

# Or list all restore points
Get-AzureRmSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Get the specific database to restore
$Database = Get-AzureRmSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Pick desired restore point using RestorePointCreationDate
$PointInTime="<RestorePointCreationDate>"  

# Restore database from a restore point
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromPointInTimeBackup –PointInTime $PointInTime -ResourceGroupName $Database.ResourceGroupName -ServerName $Database.$ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $Database.ResourceID

# Verify the status of restored database
$RestoredDatabase.status

```

> [!NOTE]
> <span data-ttu-id="b45ef-128">Чтобы настроить базу данных после восстановления, см. раздел [Настройка базы данных после восстановления][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="b45ef-128">After the restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="b45ef-129">Восстановление удаленной базы данных.</span><span class="sxs-lookup"><span data-stu-id="b45ef-129">Restore a deleted database</span></span>
<span data-ttu-id="b45ef-130">Для восстановления удаленной базы данных используйте командлет [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="b45ef-130">To restore a deleted database, use the [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="b45ef-131">Откройте Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b45ef-131">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="b45ef-132">Подключитесь к своей учетной записи Azure и выведите список всех подписок, связанных с ней.</span><span class="sxs-lookup"><span data-stu-id="b45ef-132">Connect to your Azure account and list all the subscriptions associated with your account.</span></span>
3. <span data-ttu-id="b45ef-133">Выберите подписку, содержащую удаленную базу данных, которую нужно восстановить.</span><span class="sxs-lookup"><span data-stu-id="b45ef-133">Select the subscription that contains the deleted database to be restored.</span></span>
4. <span data-ttu-id="b45ef-134">Получите конкретную удаленную базу данных.</span><span class="sxs-lookup"><span data-stu-id="b45ef-134">Get the specific deleted database.</span></span>
5. <span data-ttu-id="b45ef-135">Восстановите удаленную базу данных.</span><span class="sxs-lookup"><span data-stu-id="b45ef-135">Restore the deleted database.</span></span>
6. <span data-ttu-id="b45ef-136">Убедитесь, что восстановленная база данных подключена к сети.</span><span class="sxs-lookup"><span data-stu-id="b45ef-136">Verify that the restored database is online.</span></span>

```Powershell
$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# Get the deleted database to restore
$DeletedDatabase = Get-AzureRmSqlDeletedDatabaseBackup -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Restore deleted database
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromDeletedDatabaseBackup –DeletionDate $DeletedDatabase.DeletionDate -ResourceGroupName $DeletedDatabase.ResourceGroupName -ServerName $DeletedDatabase.ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $DeletedDatabase.ResourceID

# Verify the status of restored database
$RestoredDatabase.status
```

> [!NOTE]
> <span data-ttu-id="b45ef-137">Чтобы настроить базу данных после восстановления, см. раздел [Настройка базы данных после восстановления][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="b45ef-137">After the restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-from-an-azure-geographical-region"></a><span data-ttu-id="b45ef-138">Восстановление из географического региона Azure</span><span class="sxs-lookup"><span data-stu-id="b45ef-138">Restore from an Azure geographical region</span></span>
<span data-ttu-id="b45ef-139">Для восстановления базы данных используйте командлет [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="b45ef-139">To recover a database, use the [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="b45ef-140">Откройте Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b45ef-140">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="b45ef-141">Подключитесь к своей учетной записи Azure и выведите список всех подписок, связанных с ней.</span><span class="sxs-lookup"><span data-stu-id="b45ef-141">Connect to your Azure account and list all the subscriptions associated with your account.</span></span>
3. <span data-ttu-id="b45ef-142">Выберите подписку, содержащую базу данных, которую нужно восстановить.</span><span class="sxs-lookup"><span data-stu-id="b45ef-142">Select the subscription that contains the database to be restored.</span></span>
4. <span data-ttu-id="b45ef-143">Получите базу данных, которую требуется восстановить.</span><span class="sxs-lookup"><span data-stu-id="b45ef-143">Get the database you want to recover.</span></span>
5. <span data-ttu-id="b45ef-144">Создайте запрос на восстановление базы данных.</span><span class="sxs-lookup"><span data-stu-id="b45ef-144">Create the recovery request for the database.</span></span>
6. <span data-ttu-id="b45ef-145">Проверьте состояние геовосстановленной базы данных.</span><span class="sxs-lookup"><span data-stu-id="b45ef-145">Verify the status of the geo-restored database.</span></span>

```Powershell
Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName "<Subscription_name>"

# Get the database you want to recover
$GeoBackup = Get-AzureRmSqlDatabaseGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourServerName>" -DatabaseName "<YourDatabaseName>"

# Recover database
$GeoRestoredDatabase = Restore-AzureRmSqlDatabase –FromGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourTargetServer>" -TargetDatabaseName "<NewDatabaseName>" –ResourceId $GeoBackup.ResourceID

# Verify that the geo-restored database is online
$GeoRestoredDatabase.status
```

> [!NOTE]
> <span data-ttu-id="b45ef-146">Чтобы настроить базу данных после восстановления, см. раздел [Настройка базы данных после восстановления][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="b45ef-146">To configure your database after the restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

<span data-ttu-id="b45ef-147">Восстановленная база данных будет поддерживать прозрачное шифрование данных, если исходная база данных поддерживает прозрачное шифрование данных.</span><span class="sxs-lookup"><span data-stu-id="b45ef-147">The recovered database will be TDE-enabled if the source database is TDE-enabled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b45ef-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b45ef-148">Next steps</span></span>
<span data-ttu-id="b45ef-149">Дополнительные сведения о функциях, обеспечивающих непрерывность бизнес-процессов в выпусках Базы данных SQL Azure, см. в статье [Обзор обеспечения непрерывности бизнес-процессов с помощью базы данных SQL Azure][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="b45ef-149">To learn about the business continuity features of Azure SQL Database editions, please read the [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How to install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery

<!--MSDN references-->
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
