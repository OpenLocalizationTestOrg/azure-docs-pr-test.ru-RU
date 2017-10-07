---
title: "Настройка долгосрочного хранения резервных копий для Базы данных SQL Azure | Документация Майкрософт"
description: "Узнайте, как toostore автоматизировать резервных копий в хранилище служб восстановления Azure hello и toorestore из hello в хранилище служб восстановления Azure"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: aeb8c4c3-6ae2-45f7-b2c3-fa13e3752eed
ms.service: sql-database
ms.custom: business continuity
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: carlrab
ms.openlocfilehash: 603f4dd21cee4407d46f749655aba8f9ef3322c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-restore-from-azure-sql-database-long-term-backup-retention"></a>Настройка долгосрочного хранения резервных копий для Базы данных SQL Azure и восстановление из резервной копии

Можно настроить резервные копии баз данных Azure SQL toostore в хранилище служб восстановления Azure hello и затем восстановить базу данных, используя резервные копии хранятся в хранилище, используя hello hello портал Azure или PowerShell.

## <a name="azure-portal"></a>Портал Azure

следующие разделы Показать вы как хранилище toouse hello Azure портала tooconfigure hello служб восстановления Azure, просмотр резервных копий в хранилище hello и восстановление из хранилища hello Hello.

### <a name="configure-hello-vault-register-hello-server-and-select-databases"></a>Настройка хранилища hello, зарегистрируйте сервер hello и выбор баз данных

Вы [Настройка архивации tooretain автоматическое хранилище служб восстановления Azure](sql-database-long-term-retention.md) в течение периода времени, чем срок хранения hello для уровня службы. 

1. Откройте hello **SQL Server** страницы для вашего сервера.

   ![страница sql server](./media/sql-database-get-started-portal/sql-server-blade.png)

2. Щелкните **Long-term backup retention** (Долгосрочное хранение резервных копий).

   ![Ссылка Long-term backup retention (Долгосрочное хранение резервных копий)](./media/sql-database-get-started-backup-recovery/long-term-backup-retention-link.png)

3. На hello **долгосрочного хранения резервной копии** сервера просмотрите и примите условия предварительной версии hello (Если вы еще - или эта функция больше не предварительная версия).

   ![Примите условия предварительной версии hello](./media/sql-database-get-started-backup-recovery/accept-the-preview-terms.png)

4. tooconfigure долгосрочного хранения резервной копии, выберите эту базу данных в сетке hello и нажмите кнопку **Настройка** на панели инструментов hello.

   ![Выбор базы данных для настройки долгосрочного хранения резервных копий](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

5. На hello **Настройка** щелкните **настроить необходимые параметры** под **хранилище службы восстановления**.

   ![Ссылка для настройки хранилища](./media/sql-database-get-started-backup-recovery/configure-vault-link.png)

6. На hello **хранилище служб восстановления** выберите существующем хранилище, если таковые имеются. В противном случае если хранилище служб восстановления не найден для вашей подписки, щелкните tooexit hello потока и создайте хранилище служб восстановления.

   ![ссылка на создание хранилища](./media/sql-database-get-started-backup-recovery/create-new-vault-link.png)

7. На hello **хранилищ служб восстановления** щелкните **добавить**.

   ![ссылка на добавление хранилища](./media/sql-database-get-started-backup-recovery/add-new-vault-link.png)
   
8. На hello **хранилище служб восстановления** укажите допустимое имя для службы восстановления hello в хранилище.

   ![Имя нового хранилища](./media/sql-database-get-started-backup-recovery/new-vault-name.png)

9. Выберите подписку и группе ресурсов и выберите расположение хранилища hello hello. По завершении нажмите кнопку **Создать**.

   ![создание хранилища](./media/sql-database-get-started-backup-recovery/create-new-vault.png)

   > [!IMPORTANT]
   > Hello хранилища должен быть расположен в hello же регионе, что логический сервер Azure SQL hello и необходимо использовать hello же группе ресурсов, что hello логического сервера.
   >

10. После создания нового хранилища hello выполнение hello необходимые шаги tooreturn toohello **хранилище служб восстановления** страницы.

11. На hello **хранилище служб восстановления** выберите хранилище hello и нажмите кнопку **выберите**.

   ![Выбор имеющегося хранилища](./media/sql-database-get-started-backup-recovery/select-existing-vault.png)

12. На hello **Настройка** страницы, укажите допустимое имя для новой политики хранения hello, изменение политики хранения по умолчанию hello соответствующим образом и нажмите кнопку **ОК**.

   ![Определение политики хранения](./media/sql-database-get-started-backup-recovery/define-retention-policy.png)

13. На hello **долгосрочного хранения резервной копии** для базы данных и щелкните **Сохранить** и нажмите кнопку **ОК** tooapply hello долгосрочной политики tooall хранения резервных копий, которые выбраны базы данных.

   ![Определение политики хранения](./media/sql-database-get-started-backup-recovery/save-retention-policy.png)

14. Нажмите кнопку **Сохранить** tooenable долгосрочного хранения резервной копии с помощью этого нового хранилища служб восстановления Azure toohello политики, настроенной.

   ![Определение политики хранения](./media/sql-database-get-started-backup-recovery/enable-long-term-retention.png)

> [!IMPORTANT]
> После настройки резервного копирования, отображаются в хранилище hello в течение следующих семи дней. Не следует продолжать этого учебника, пока не отображаются резервные копии в хранилище hello.
>

### <a name="view-backups-in-long-term-retention-using-azure-portal"></a>Просмотр резервных копий долгосрочного хранения с помощью портала Azure

Просмотрите сведения о резервных копиях базы данных в хранилище с включенной функцией [долгосрочного хранения резервных копий](sql-database-long-term-retention.md). 

1. В hello портал Azure, откройте ваше хранилище служб восстановления Azure для резервного копирования базы данных (go слишком**все ресурсы** и выберите его из списка hello ресурсов по подписке) tooview hello объем хранилища, используемых в вашей базе данных Создание резервных копий в хранилище hello.

   ![Просмотр хранилища служб восстановления с резервными копиями](./media/sql-database-get-started-backup-recovery/view-recovery-services-vault-with-data.png)

2. Откройте hello **базы данных SQL** страницу для базы данных.

   ![страница нового примера базы данных](./media/sql-database-get-started-portal/new-sample-db-blade.png)

3. На панели инструментов hello, нажмите кнопку **восстановить**.

   ![Элемент "Восстановить" на панели инструментов](./media/sql-database-get-started-backup-recovery/restore-toolbar.png)

4. На странице приветствия восстановления, нажмите кнопку **долгосрочной**.

5. Резервные копии в хранилище Azure, установите для **выберите архив** tooview hello доступные резервные копии в долгосрочного хранения резервной копии.

   ![Резервные копии в хранилище](./media/sql-database-get-started-backup-recovery/view-backups-in-vault.png)

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention-using-hello-azure-portal"></a>Восстановление базы данных из резервной копии в долгосрочного хранения резервной копии с помощью портала Azure hello

Восстановить базы данных hello tooa новую базу данных из резервной копии в хранилище служб восстановления Azure hello.

1. На hello **резервных копий в хранилище Azure** выберите резервного копирования toorestore hello и нажмите кнопку **выберите**.

   ![Выбор резервной копии в хранилище](./media/sql-database-get-started-backup-recovery/select-backup-in-vault.png)

2. В hello **имя базы данных** текста введите имя hello hello восстановления базы данных.

   ![Имя новой базы данных](./media/sql-database-get-started-backup-recovery/new-database-name.png)

3. Нажмите кнопку **ОК** toorestore базы данных из резервной копии hello в хранилище hello toohello новой базы данных.

4. На панели инструментов hello щелкните hello уведомления значок tooview hello состояние задания восстановления hello.

   ![Ход выполнения задания восстановления из хранилища](./media/sql-database-get-started-backup-recovery/restore-job-progress-long-term.png)

5. После завершения задания восстановления Привет открыть hello **баз данных SQL** базы данных недавно восстановленных hello tooview страницы.

   ![Имя базы данных, восстановленной из хранилища](./media/sql-database-get-started-backup-recovery/restored-database-from-vault.png)

> [!NOTE]
> Здесь можно подключиться toohello восстановить базы данных с помощью SQL Server Management Studio tooperform необходимые задачи, такие как слишком[Извлеките бит данных из toocopy базы данных восстановлена hello в hello существующей базы данных или имеющиеся hello toodelete базы данных и существующие toohello переименования hello восстановления базы данных имя базы данных](sql-database-recovery-using-backups.md#point-in-time-restore).
>

## <a name="powershell"></a>PowerShell

Привет, в следующих разделах показано, как хранилище служб восстановления Azure hello tooconfigure PowerShell toouse, просмотр резервных копий в хранилище hello и восстановление из хранилища hello.

### <a name="create-a-recovery-services-vault"></a>Создание хранилища служб восстановления

Используйте hello [New AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) хранилища служб toocreate во время операции восстановления.

> [!IMPORTANT]
> Hello хранилища должен быть расположен в hello же регионе, что логический сервер Azure SQL hello и необходимо использовать hello же группе ресурсов, что hello логического сервера.

```PowerShell
# Create a recovery services vault

#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$serverLocation = (Get-AzureRmSqlServer -ServerName $serverName -ResourceGroupName $resourceGroupName).Location
$recoveryServiceVaultName = "{new-vault-name}"

$vault = New-AzureRmRecoveryServicesVault -Name $recoveryServiceVaultName -ResourceGroupName $ResourceGroupName -Location $serverLocation 
Set-AzureRmRecoveryServicesBackupProperties -BackupStorageRedundancy LocallyRedundant -Vault $vault
```

### <a name="set-your-server-toouse-hello-recovery-vault-for-its-long-term-retention-backups"></a>Задать hello восстановления сервера toouse хранилище для резервных копиях ее долгосрочного хранения

Используйте hello [AzureRmSqlServerBackupLongTermRetentionVault набор](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) командлет tooassociate ранее созданное хранилище служб восстановления с конкретным сервером Azure SQL.

```PowerShell
# Set your server toouse hello vault toofor long-term backup retention 

Set-AzureRmSqlServerBackupLongTermRetentionVault -ResourceGroupName $resourceGroupName -ServerName $serverName -ResourceId $vault.Id
```

### <a name="create-a-retention-policy"></a>Создание политики хранения

Политика хранения не задаются как долго tookeep резервной копии базы данных. Используйте hello [Get AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) командлет tooget hello по умолчанию хранения политики toouse как hello шаблон для создания политик. В этом шаблоне срок хранения hello задан для 2 года. Затем выполните hello [New AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) toofinally Создание политики hello. 

> [!NOTE]
> Некоторые командлеты, требуют настройки контекст хранилища hello перед запуском ([AzureRmRecoveryServicesVaultContext набор](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)), вы видите этот командлет в несколько связанных фрагментов кода. Можно задать контекст hello, так как политика hello является частью хранилища hello. Можно создать несколько политик хранения для каждого хранилища и применить политики hello требуемого toospecific-базы данных. 


```PowerShell
# Retrieve hello default retention policy for hello AzureSQLDatabase workload type
$retentionPolicy = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType AzureSQLDatabase

# Set hello retention value tootwo years (you can set tooany time between 1 week and 10 years)
$retentionPolicy.RetentionDurationType = "Years"
$retentionPolicy.RetentionCount = 2
$retentionPolicyName = "my2YearRetentionPolicy"

# Set hello vault context toohello vault you are creating hello policy for
Set-AzureRmRecoveryServicesVaultContext -Vault $vault

# Create hello new policy
$policy = New-AzureRmRecoveryServicesBackupProtectionPolicy -name $retentionPolicyName -WorkloadType AzureSQLDatabase -retentionPolicy $retentionPolicy
$policy
```

### <a name="configure-a-database-toouse-hello-previously-defined-retention-policy"></a>Настроить политику хранения toouse hello ранее определенные базы данных

Используйте hello [AzureRmSqlDatabaseBackupLongTermRetentionPolicy набор](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) командлет tooapply hello новой политики tooa конкретной базы данных.

```PowerShell
# Enable long-term retention for a specific SQL database
$policyState = "enabled"
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -State $policyState -ResourceId $policy.Id
```

### <a name="view-backup-info-and-backups-in-long-term-retention"></a>Просмотр сведений о резервных копиях с включенной функцией долгосрочного хранения

Просмотрите сведения о резервных копиях базы данных в хранилище с включенной функцией [долгосрочного хранения резервных копий](sql-database-long-term-retention.md). 

Используйте следующие сведения о резервном копировании tooview командлеты hello.

- [Get-AzureRmRecoveryServicesBackupContainer](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)
- [Get-AzureRmRecoveryServicesBackupItem](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)
- [Get-AzureRmRecoveryServicesBackupRecoveryPoint](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)

```PowerShell
#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$databaseNeedingRestore = $databaseName

# Set hello vault context toohello vault we want toorestore from
#$vault = Get-AzureRmRecoveryServicesVault -ResourceGroupName $resourceGroupName
Set-AzureRmRecoveryServicesVaultContext -Vault $vault

# hello following commands find hello container associated with hello server 'myserver' under resource group 'myresourcegroup'
$container = Get-AzureRmRecoveryServicesBackupContainer -ContainerType AzureSQL -FriendlyName $vault.Name

# Get hello long-term retention metadata associated with a specific database
$item = Get-AzureRmRecoveryServicesBackupItem -Container $container -WorkloadType AzureSQLDatabase -Name $databaseNeedingRestore

# Get all available backups for hello previously indicated database
# Optionally, set hello -StartDate and -EndDate parameters tooreturn backups within a specific time period
$availableBackups = Get-AzureRmRecoveryServicesBackupRecoveryPoint -Item $item
$availableBackups
```

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention"></a>Восстановление базы данных из резервной копии с долгосрочным хранением

Восстановление из долгосрочного хранения резервной копии используется hello [AzureRmSqlDatabase восстановления](/powershell/module/azurerm.sql/restore-azurermsqldatabase) командлета.

```PowerShell
# Restore hello most recent backup: $availableBackups[0]
#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$restoredDatabaseName = "{new-database-name}"
$edition = "Basic"
$performanceLevel = "Basic"

$restoredDb = Restore-AzureRmSqlDatabase -FromLongTermRetentionBackup -ResourceId $availableBackups[0].Id -ResourceGroupName $resourceGroupName `
 -ServerName $serverName -TargetDatabaseName $restoredDatabaseName -Edition $edition -ServiceObjectiveName $performanceLevel
$restoredDb
```


> [!NOTE]
> Здесь можно подключить toohello восстановления базы данных с помощью SQL Server Management Studio tooperform необходимые задачи, например tooextract бит данных из hello восстанавливается toocopy базы данных в hello существующей базы данных или существующую базу данных hello toodelete и переименования Hello восстановленной базы данных toohello именем существующей базы данных. Ознакомьтесь с [восстановлением до точки во времени](sql-database-recovery-using-backups.md#point-in-time-restore).

## <a name="next-steps"></a>Дальнейшие действия

- toolearn о создан службы автоматического резервного копирования, в разделе [автоматического резервного копирования](sql-database-automated-backups.md)
- toolearn о долгосрочного хранения резервной копии, в разделе [долгосрочного хранения резервной копии](sql-database-long-term-retention.md)
- в разделе toolearn о восстановлении из резервных копий, [восстановление из резервной копии](sql-database-recovery-using-backups.md)
