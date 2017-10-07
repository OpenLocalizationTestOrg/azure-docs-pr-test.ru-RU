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
# <a name="restore-an-azure-sql-data-warehouse-powershell"></a>Восстановление хранилища данных SQL Azure (PowerShell)
> [!div class="op_single_selector"]
> * [Обзор][Overview]
> * [Портал][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
> 
> 

В этой статье вы узнаете, как toorestore Azure SQL в хранилище данных с помощью PowerShell.

## <a name="before-you-begin"></a>Перед началом работы
**Проверьте ресурсы DTU.** Каждое хранилище данных SQL размещается на сервере SQL Server (например, myserver.database.windows.net), которому выделена квота DTU по умолчанию.  Перед началом восстановления хранилища данных SQL, убедитесь, что hello, SQL server имеет достаточно оставшиеся квоту DTU для hello восстанавливаемой базы данных. toolearn как необходимые toocalculate DTU или toorequest дополнительные DTU см [запроса на изменение квоты DTU][Request a DTU quota change].

### <a name="install-powershell"></a>Установка PowerShell
В порядке toouse Azure PowerShell с хранилищем данных SQL нужно будет tooinstall Azure PowerShell версии 1.0 или более поздней.  Чтобы узнать текущую версию, выполните командлет **Get-Module -ListAvailable -Name AzureRM**.  может быть установлена последняя версия Hello из [Microsoft Web Platform Installer][Microsoft Web Platform Installer].  Дополнительные сведения об установке последней версии hello см. в разделе [как tooinstall и настройка Azure PowerShell][How tooinstall and configure Azure PowerShell].

## <a name="restore-an-active-or-paused-database"></a>Восстановление активной или приостановленной базы данных
использовать базу данных из моментального снимка toorestore hello [восстановления AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] командлета PowerShell.

1. Откройте Windows PowerShell.
2. Подключите tooyour учетная запись Azure и вывод списка всех подписок hello, связанные с учетной записью.
3. Выберите подписку hello, содержащий toobe базы данных hello восстановлена.
4. Список hello восстановить точки hello базы данных.
5. Выберите точку восстановления hello требуемого hello RestorePointCreationDate с помощью.
6. Hello базы данных требуемого toohello восстановления точку восстановления.
7. Убедитесь, что hello восстановления базы данных находится в оперативном режиме.

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
> После завершения восстановления hello восстановленной базы данных можно настроить, выполнив [настроить базу данных после восстановления][Configure your database after recovery].
> 
> 

## <a name="restore-a-deleted-database"></a>Восстановление удаленной базы данных.
toorestore удаленной базы данных, используйте hello [восстановления AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] командлета.

1. Откройте Windows PowerShell.
2. Подключите tooyour учетная запись Azure и вывод списка всех подписок hello, связанные с учетной записью.
3. Выберите подписку hello, содержащий toobe базы данных удалены hello восстановлена.
4. Получите hello конкретных удалить базу данных.
5. Восстановление базы данных удалены hello.
6. Убедитесь, что hello восстановления базы данных находится в оперативном режиме.

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
> После завершения восстановления hello восстановленной базы данных можно настроить, выполнив [настроить базу данных после восстановления][Configure your database after recovery].
> 
> 

## <a name="restore-from-an-azure-geographical-region"></a>Восстановление из географического региона Azure
toorecover базы данных, используйте hello [восстановления AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] командлета.

1. Откройте Windows PowerShell.
2. Подключите tooyour учетная запись Azure и вывод списка всех подписок hello, связанные с учетной записью.
3. Выберите подписку hello, содержащий toobe базы данных hello восстановлена.
4. Получите toorecover нужная база данных hello.
5. Создание запроса hello восстановления для базы данных hello.
6. Проверьте состояние базы данных восстановлена geo hello hello.

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
> см. базы данных после завершения восстановления hello tooconfigure [настроить базу данных после восстановления][Configure your database after recovery].
> 
> 

Hello восстановленной базы данных будет включено прозрачное шифрование данных, если база данных-источник hello включено прозрачное шифрование данных.

## <a name="next-steps"></a>Дальнейшие действия
toolearn о функциях обеспечения непрерывности бизнеса hello выпусков базы данных SQL Azure, прочитайте hello [непрерывности бизнес-базы данных SQL Azure обзора][Azure SQL Database business continuity overview].

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
