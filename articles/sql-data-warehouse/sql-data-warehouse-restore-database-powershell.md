---
title: "aaaRestore хранилище данных SQL Azure (PowerShell) | Документы Microsoft"
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
ms.openlocfilehash: aa29a315080b1ed477cc6a051ce15a3202630cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="e1fe6-103">Восстановление хранилища данных SQL Azure (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="e1fe6-103">Restore an Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="e1fe6-104">[Обзор][Overview]</span><span class="sxs-lookup"><span data-stu-id="e1fe6-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="e1fe6-105">[Портал][Portal]</span><span class="sxs-lookup"><span data-stu-id="e1fe6-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="e1fe6-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="e1fe6-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="e1fe6-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="e1fe6-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="e1fe6-108">В этой статье вы узнаете, как toorestore Azure SQL в хранилище данных с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e1fe6-108">In this article you will learn how toorestore an Azure SQL Data Warehouse using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e1fe6-109">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="e1fe6-109">Before you begin</span></span>
<span data-ttu-id="e1fe6-110">**Проверьте ресурсы DTU.**</span><span class="sxs-lookup"><span data-stu-id="e1fe6-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="e1fe6-111">Каждое хранилище данных SQL размещается на сервере SQL Server (например, myserver.database.windows.net), которому выделена квота DTU по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e1fe6-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="e1fe6-112">Перед началом восстановления хранилища данных SQL, убедитесь, что hello, SQL server имеет достаточно оставшиеся квоту DTU для hello восстанавливаемой базы данных.</span><span class="sxs-lookup"><span data-stu-id="e1fe6-112">Before you can restore a SQL Data Warehouse, verify that hello your SQL server has enough remaining DTU quota for hello database being restored.</span></span> <span data-ttu-id="e1fe6-113">toolearn как необходимые toocalculate DTU или toorequest дополнительные DTU см [запроса на изменение квоты DTU][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="e1fe6-113">toolearn how toocalculate DTU needed or toorequest more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="e1fe6-114">Установка PowerShell</span><span class="sxs-lookup"><span data-stu-id="e1fe6-114">Install PowerShell</span></span>
<span data-ttu-id="e1fe6-115">В порядке toouse Azure PowerShell с хранилищем данных SQL нужно будет tooinstall Azure PowerShell версии 1.0 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="e1fe6-115">In order toouse Azure PowerShell with SQL Data Warehouse, you will need tooinstall Azure PowerShell version 1.0 or greater.</span></span>  <span data-ttu-id="e1fe6-116">Чтобы узнать текущую версию, выполните командлет **Get-Module -ListAvailable -Name AzureRM**.</span><span class="sxs-lookup"><span data-stu-id="e1fe6-116">You can check your version by running **Get-Module -ListAvailable -Name AzureRM**.</span></span>  <span data-ttu-id="e1fe6-117">может быть установлена последняя версия Hello из [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="e1fe6-117">hello latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="e1fe6-118">Дополнительные сведения об установке последней версии hello см. в разделе [как tooinstall и настройка Azure PowerShell][How tooinstall and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="e1fe6-118">For more information on installing hello latest version, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="e1fe6-119">Восстановление активной или приостановленной базы данных</span><span class="sxs-lookup"><span data-stu-id="e1fe6-119">Restore an active or paused database</span></span>
<span data-ttu-id="e1fe6-120">использовать базу данных из моментального снимка toorestore hello [восстановления AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] командлета PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e1fe6-120">toorestore a database from a snapshot use hello [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] PowerShell cmdlet.</span></span>

1. <span data-ttu-id="e1fe6-121">Откройте Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e1fe6-121">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="e1fe6-122">Подключите tooyour учетная запись Azure и вывод списка всех подписок hello, связанные с учетной записью.</span><span class="sxs-lookup"><span data-stu-id="e1fe6-122">Connect tooyour Azure account and list all hello subscriptions associated with your account.</span></span>
3. <span data-ttu-id="e1fe6-123">Выберите подписку hello, содержащий toobe базы данных hello восстановлена.</span><span class="sxs-lookup"><span data-stu-id="e1fe6-123">Select hello subscription that contains hello database toobe restored.</span></span>
4. <span data-ttu-id="e1fe6-124">Список hello восстановить точки hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="e1fe6-124">List hello restore points for hello database.</span></span>
5. <span data-ttu-id="e1fe6-125">Выберите точку восстановления hello требуемого hello RestorePointCreationDate с помощью.</span><span class="sxs-lookup"><span data-stu-id="e1fe6-125">Pick hello desired restore point using hello RestorePointCreationDate.</span></span>
6. <span data-ttu-id="e1fe6-126">Hello базы данных требуемого toohello восстановления точку восстановления.</span><span class="sxs-lookup"><span data-stu-id="e1fe6-126">Restore hello database toohello desired restore point.</span></span>
7. <span data-ttu-id="e1fe6-127">Убедитесь, что hello восстановления базы данных находится в оперативном режиме.</span><span class="sxs-lookup"><span data-stu-id="e1fe6-127">Verify that hello restored database is online.</span></span>

```Powershell

$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# List hello last 10 database restore points
((Get-AzureRMSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName ($DatabaseName).RestorePointCreationDate)[-10 .. -1]

# Or list all restore points
Get-AzureRmSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Get hello specific database toorestore
$Database = Get-AzureRmSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Pick desired restore point using RestorePointCreationDate
$PointInTime="<RestorePointCreationDate>"  

# Restore database from a restore point
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromPointInTimeBackup –PointInTime $PointInTime -ResourceGroupName $Database.ResourceGroupName -ServerName $Database.$ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $Database.ResourceID

# Verify hello status of restored database
$RestoredDatabase.status

```

> [!NOTE]
> <span data-ttu-id="e1fe6-128">После завершения восстановления hello восстановленной базы данных можно настроить, выполнив [настроить базу данных после восстановления][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="e1fe6-128">After hello restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="e1fe6-129">Восстановление удаленной базы данных.</span><span class="sxs-lookup"><span data-stu-id="e1fe6-129">Restore a deleted database</span></span>
<span data-ttu-id="e1fe6-130">toorestore удаленной базы данных, используйте hello [восстановления AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] командлета.</span><span class="sxs-lookup"><span data-stu-id="e1fe6-130">toorestore a deleted database, use hello [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="e1fe6-131">Откройте Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e1fe6-131">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="e1fe6-132">Подключите tooyour учетная запись Azure и вывод списка всех подписок hello, связанные с учетной записью.</span><span class="sxs-lookup"><span data-stu-id="e1fe6-132">Connect tooyour Azure account and list all hello subscriptions associated with your account.</span></span>
3. <span data-ttu-id="e1fe6-133">Выберите подписку hello, содержащий toobe базы данных удалены hello восстановлена.</span><span class="sxs-lookup"><span data-stu-id="e1fe6-133">Select hello subscription that contains hello deleted database toobe restored.</span></span>
4. <span data-ttu-id="e1fe6-134">Получите hello конкретных удалить базу данных.</span><span class="sxs-lookup"><span data-stu-id="e1fe6-134">Get hello specific deleted database.</span></span>
5. <span data-ttu-id="e1fe6-135">Восстановление базы данных удалены hello.</span><span class="sxs-lookup"><span data-stu-id="e1fe6-135">Restore hello deleted database.</span></span>
6. <span data-ttu-id="e1fe6-136">Убедитесь, что hello восстановления базы данных находится в оперативном режиме.</span><span class="sxs-lookup"><span data-stu-id="e1fe6-136">Verify that hello restored database is online.</span></span>

```Powershell
$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# Get hello deleted database toorestore
$DeletedDatabase = Get-AzureRmSqlDeletedDatabaseBackup -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Restore deleted database
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromDeletedDatabaseBackup –DeletionDate $DeletedDatabase.DeletionDate -ResourceGroupName $DeletedDatabase.ResourceGroupName -ServerName $DeletedDatabase.ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $DeletedDatabase.ResourceID

# Verify hello status of restored database
$RestoredDatabase.status
```

> [!NOTE]
> <span data-ttu-id="e1fe6-137">После завершения восстановления hello восстановленной базы данных можно настроить, выполнив [настроить базу данных после восстановления][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="e1fe6-137">After hello restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-from-an-azure-geographical-region"></a><span data-ttu-id="e1fe6-138">Восстановление из географического региона Azure</span><span class="sxs-lookup"><span data-stu-id="e1fe6-138">Restore from an Azure geographical region</span></span>
<span data-ttu-id="e1fe6-139">toorecover базы данных, используйте hello [восстановления AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] командлета.</span><span class="sxs-lookup"><span data-stu-id="e1fe6-139">toorecover a database, use hello [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="e1fe6-140">Откройте Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e1fe6-140">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="e1fe6-141">Подключите tooyour учетная запись Azure и вывод списка всех подписок hello, связанные с учетной записью.</span><span class="sxs-lookup"><span data-stu-id="e1fe6-141">Connect tooyour Azure account and list all hello subscriptions associated with your account.</span></span>
3. <span data-ttu-id="e1fe6-142">Выберите подписку hello, содержащий toobe базы данных hello восстановлена.</span><span class="sxs-lookup"><span data-stu-id="e1fe6-142">Select hello subscription that contains hello database toobe restored.</span></span>
4. <span data-ttu-id="e1fe6-143">Получите toorecover нужная база данных hello.</span><span class="sxs-lookup"><span data-stu-id="e1fe6-143">Get hello database you want toorecover.</span></span>
5. <span data-ttu-id="e1fe6-144">Создание запроса hello восстановления для базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="e1fe6-144">Create hello recovery request for hello database.</span></span>
6. <span data-ttu-id="e1fe6-145">Проверьте состояние базы данных восстановлена geo hello hello.</span><span class="sxs-lookup"><span data-stu-id="e1fe6-145">Verify hello status of hello geo-restored database.</span></span>

```Powershell
Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName "<Subscription_name>"

# Get hello database you want toorecover
$GeoBackup = Get-AzureRmSqlDatabaseGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourServerName>" -DatabaseName "<YourDatabaseName>"

# Recover database
$GeoRestoredDatabase = Restore-AzureRmSqlDatabase –FromGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourTargetServer>" -TargetDatabaseName "<NewDatabaseName>" –ResourceId $GeoBackup.ResourceID

# Verify that hello geo-restored database is online
$GeoRestoredDatabase.status
```

> [!NOTE]
> <span data-ttu-id="e1fe6-146">см. базы данных после завершения восстановления hello tooconfigure [настроить базу данных после восстановления][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="e1fe6-146">tooconfigure your database after hello restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

<span data-ttu-id="e1fe6-147">Hello восстановленной базы данных будет включено прозрачное шифрование данных, если база данных-источник hello включено прозрачное шифрование данных.</span><span class="sxs-lookup"><span data-stu-id="e1fe6-147">hello recovered database will be TDE-enabled if hello source database is TDE-enabled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1fe6-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e1fe6-148">Next steps</span></span>
<span data-ttu-id="e1fe6-149">toolearn о функциях обеспечения непрерывности бизнеса hello выпусков базы данных SQL Azure, прочитайте hello [непрерывности бизнес-базы данных SQL Azure обзора][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="e1fe6-149">toolearn about hello business continuity features of Azure SQL Database editions, please read hello [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
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
