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
# <a name="configure-and-restore-from-azure-sql-database-long-term-backup-retention"></a><span data-ttu-id="84a3c-103">Настройка долгосрочного хранения резервных копий для Базы данных SQL Azure и восстановление из резервной копии</span><span class="sxs-lookup"><span data-stu-id="84a3c-103">Configure and restore from Azure SQL Database long-term backup retention</span></span>

<span data-ttu-id="84a3c-104">Можно настроить резервные копии баз данных Azure SQL toostore в хранилище служб восстановления Azure hello и затем восстановить базу данных, используя резервные копии хранятся в хранилище, используя hello hello портал Azure или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="84a3c-104">You can configure hello Azure Recovery Services vault toostore Azure SQL database backups and then recover a database using backups retained in hello vault using hello Azure portal or PowerShell.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="84a3c-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="84a3c-105">Azure portal</span></span>

<span data-ttu-id="84a3c-106">следующие разделы Показать вы как хранилище toouse hello Azure портала tooconfigure hello служб восстановления Azure, просмотр резервных копий в хранилище hello и восстановление из хранилища hello Hello.</span><span class="sxs-lookup"><span data-stu-id="84a3c-106">hello following sections show you how toouse hello Azure portal tooconfigure hello Azure Recovery Services vault, view backups in hello vault, and restore from hello vault.</span></span>

### <a name="configure-hello-vault-register-hello-server-and-select-databases"></a><span data-ttu-id="84a3c-107">Настройка хранилища hello, зарегистрируйте сервер hello и выбор баз данных</span><span class="sxs-lookup"><span data-stu-id="84a3c-107">Configure hello vault, register hello server, and select databases</span></span>

<span data-ttu-id="84a3c-108">Вы [Настройка архивации tooretain автоматическое хранилище служб восстановления Azure](sql-database-long-term-retention.md) в течение периода времени, чем срок хранения hello для уровня службы.</span><span class="sxs-lookup"><span data-stu-id="84a3c-108">You [configure an Azure Recovery Services vault tooretain automated backups](sql-database-long-term-retention.md) for a period longer than hello retention period for your service tier.</span></span> 

1. <span data-ttu-id="84a3c-109">Откройте hello **SQL Server** страницы для вашего сервера.</span><span class="sxs-lookup"><span data-stu-id="84a3c-109">Open hello **SQL Server** page for your server.</span></span>

   ![страница sql server](./media/sql-database-get-started-portal/sql-server-blade.png)

2. <span data-ttu-id="84a3c-111">Щелкните **Long-term backup retention** (Долгосрочное хранение резервных копий).</span><span class="sxs-lookup"><span data-stu-id="84a3c-111">Click **Long-term backup retention**.</span></span>

   ![Ссылка Long-term backup retention (Долгосрочное хранение резервных копий)](./media/sql-database-get-started-backup-recovery/long-term-backup-retention-link.png)

3. <span data-ttu-id="84a3c-113">На hello **долгосрочного хранения резервной копии** сервера просмотрите и примите условия предварительной версии hello (Если вы еще - или эта функция больше не предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="84a3c-113">On hello **Long-term backup retention** page for your server, review and accept hello preview terms (unless you have already done so - or this feature is no longer in preview).</span></span>

   ![Примите условия предварительной версии hello](./media/sql-database-get-started-backup-recovery/accept-the-preview-terms.png)

4. <span data-ttu-id="84a3c-115">tooconfigure долгосрочного хранения резервной копии, выберите эту базу данных в сетке hello и нажмите кнопку **Настройка** на панели инструментов hello.</span><span class="sxs-lookup"><span data-stu-id="84a3c-115">tooconfigure long-term backup retention, select that database in hello grid and then click **Configure** on hello toolbar.</span></span>

   ![Выбор базы данных для настройки долгосрочного хранения резервных копий](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

5. <span data-ttu-id="84a3c-117">На hello **Настройка** щелкните **настроить необходимые параметры** под **хранилище службы восстановления**.</span><span class="sxs-lookup"><span data-stu-id="84a3c-117">On hello **Configure** page, click **Configure required settings** under **Recovery service vault**.</span></span>

   ![Ссылка для настройки хранилища](./media/sql-database-get-started-backup-recovery/configure-vault-link.png)

6. <span data-ttu-id="84a3c-119">На hello **хранилище служб восстановления** выберите существующем хранилище, если таковые имеются.</span><span class="sxs-lookup"><span data-stu-id="84a3c-119">On hello **Recovery services vault** page, select an existing vault, if any.</span></span> <span data-ttu-id="84a3c-120">В противном случае если хранилище служб восстановления не найден для вашей подписки, щелкните tooexit hello потока и создайте хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="84a3c-120">Otherwise, if no recovery services vault found for your subscription, click tooexit hello flow and create a recovery services vault.</span></span>

   ![ссылка на создание хранилища](./media/sql-database-get-started-backup-recovery/create-new-vault-link.png)

7. <span data-ttu-id="84a3c-122">На hello **хранилищ служб восстановления** щелкните **добавить**.</span><span class="sxs-lookup"><span data-stu-id="84a3c-122">On hello **Recovery Services vaults** page, click **Add**.</span></span>

   ![ссылка на добавление хранилища](./media/sql-database-get-started-backup-recovery/add-new-vault-link.png)
   
8. <span data-ttu-id="84a3c-124">На hello **хранилище служб восстановления** укажите допустимое имя для службы восстановления hello в хранилище.</span><span class="sxs-lookup"><span data-stu-id="84a3c-124">On hello **Recovery Services vault** page, provide a valid name for hello Recovery Services vault.</span></span>

   ![Имя нового хранилища](./media/sql-database-get-started-backup-recovery/new-vault-name.png)

9. <span data-ttu-id="84a3c-126">Выберите подписку и группе ресурсов и выберите расположение хранилища hello hello.</span><span class="sxs-lookup"><span data-stu-id="84a3c-126">Select your subscription and resource group, and then select hello location for hello vault.</span></span> <span data-ttu-id="84a3c-127">По завершении нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="84a3c-127">When done, click **Create**.</span></span>

   ![создание хранилища](./media/sql-database-get-started-backup-recovery/create-new-vault.png)

   > [!IMPORTANT]
   > <span data-ttu-id="84a3c-129">Hello хранилища должен быть расположен в hello же регионе, что логический сервер Azure SQL hello и необходимо использовать hello же группе ресурсов, что hello логического сервера.</span><span class="sxs-lookup"><span data-stu-id="84a3c-129">hello vault must be located in hello same region as hello Azure SQL logical server, and must use hello same resource group as hello logical server.</span></span>
   >

10. <span data-ttu-id="84a3c-130">После создания нового хранилища hello выполнение hello необходимые шаги tooreturn toohello **хранилище служб восстановления** страницы.</span><span class="sxs-lookup"><span data-stu-id="84a3c-130">After hello new vault is created, execute hello necessary steps tooreturn toohello **Recovery services vault** page.</span></span>

11. <span data-ttu-id="84a3c-131">На hello **хранилище служб восстановления** выберите хранилище hello и нажмите кнопку **выберите**.</span><span class="sxs-lookup"><span data-stu-id="84a3c-131">On hello **Recovery services vault** page, click hello vault and then click **Select**.</span></span>

   ![Выбор имеющегося хранилища](./media/sql-database-get-started-backup-recovery/select-existing-vault.png)

12. <span data-ttu-id="84a3c-133">На hello **Настройка** страницы, укажите допустимое имя для новой политики хранения hello, изменение политики хранения по умолчанию hello соответствующим образом и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="84a3c-133">On hello **Configure** page, provide a valid name for hello new retention policy, modify hello default retention policy as appropriate, and then click **OK**.</span></span>

   ![Определение политики хранения](./media/sql-database-get-started-backup-recovery/define-retention-policy.png)

13. <span data-ttu-id="84a3c-135">На hello **долгосрочного хранения резервной копии** для базы данных и щелкните **Сохранить** и нажмите кнопку **ОК** tooapply hello долгосрочной политики tooall хранения резервных копий, которые выбраны базы данных.</span><span class="sxs-lookup"><span data-stu-id="84a3c-135">On hello **Long-term backup retention** page for your database, click **Save** and then click **OK** tooapply hello long-term backup retention policy tooall selected databases.</span></span>

   ![Определение политики хранения](./media/sql-database-get-started-backup-recovery/save-retention-policy.png)

14. <span data-ttu-id="84a3c-137">Нажмите кнопку **Сохранить** tooenable долгосрочного хранения резервной копии с помощью этого нового хранилища служб восстановления Azure toohello политики, настроенной.</span><span class="sxs-lookup"><span data-stu-id="84a3c-137">Click **Save** tooenable long-term backup retention using this new policy toohello Azure Recovery Services vault that you configured.</span></span>

   ![Определение политики хранения](./media/sql-database-get-started-backup-recovery/enable-long-term-retention.png)

> [!IMPORTANT]
> <span data-ttu-id="84a3c-139">После настройки резервного копирования, отображаются в хранилище hello в течение следующих семи дней.</span><span class="sxs-lookup"><span data-stu-id="84a3c-139">Once configured, backups show up in hello vault within next seven days.</span></span> <span data-ttu-id="84a3c-140">Не следует продолжать этого учебника, пока не отображаются резервные копии в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="84a3c-140">Do not continue this tutorial until backups show up in hello vault.</span></span>
>

### <a name="view-backups-in-long-term-retention-using-azure-portal"></a><span data-ttu-id="84a3c-141">Просмотр резервных копий долгосрочного хранения с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="84a3c-141">View backups in long-term retention using Azure portal</span></span>

<span data-ttu-id="84a3c-142">Просмотрите сведения о резервных копиях базы данных в хранилище с включенной функцией [долгосрочного хранения резервных копий](sql-database-long-term-retention.md).</span><span class="sxs-lookup"><span data-stu-id="84a3c-142">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span></span> 

1. <span data-ttu-id="84a3c-143">В hello портал Azure, откройте ваше хранилище служб восстановления Azure для резервного копирования базы данных (go слишком**все ресурсы** и выберите его из списка hello ресурсов по подписке) tooview hello объем хранилища, используемых в вашей базе данных Создание резервных копий в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="84a3c-143">In hello Azure portal, open your Azure Recovery Services vault for your database backups (go too**All resources** and select it from hello list of resources for your subscription) tooview hello amount of storage used by your database backups in hello vault.</span></span>

   ![Просмотр хранилища служб восстановления с резервными копиями](./media/sql-database-get-started-backup-recovery/view-recovery-services-vault-with-data.png)

2. <span data-ttu-id="84a3c-145">Откройте hello **базы данных SQL** страницу для базы данных.</span><span class="sxs-lookup"><span data-stu-id="84a3c-145">Open hello **SQL database** page for your database.</span></span>

   ![страница нового примера базы данных](./media/sql-database-get-started-portal/new-sample-db-blade.png)

3. <span data-ttu-id="84a3c-147">На панели инструментов hello, нажмите кнопку **восстановить**.</span><span class="sxs-lookup"><span data-stu-id="84a3c-147">On hello toolbar, click **Restore**.</span></span>

   ![Элемент "Восстановить" на панели инструментов](./media/sql-database-get-started-backup-recovery/restore-toolbar.png)

4. <span data-ttu-id="84a3c-149">На странице приветствия восстановления, нажмите кнопку **долгосрочной**.</span><span class="sxs-lookup"><span data-stu-id="84a3c-149">On hello Restore page, click **Long-term**.</span></span>

5. <span data-ttu-id="84a3c-150">Резервные копии в хранилище Azure, установите для **выберите архив** tooview hello доступные резервные копии в долгосрочного хранения резервной копии.</span><span class="sxs-lookup"><span data-stu-id="84a3c-150">Under Azure vault backups, click **Select a backup** tooview hello available database backups in long-term backup retention.</span></span>

   ![Резервные копии в хранилище](./media/sql-database-get-started-backup-recovery/view-backups-in-vault.png)

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention-using-hello-azure-portal"></a><span data-ttu-id="84a3c-152">Восстановление базы данных из резервной копии в долгосрочного хранения резервной копии с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="84a3c-152">Restore a database from a backup in long-term backup retention using hello Azure portal</span></span>

<span data-ttu-id="84a3c-153">Восстановить базы данных hello tooa новую базу данных из резервной копии в хранилище служб восстановления Azure hello.</span><span class="sxs-lookup"><span data-stu-id="84a3c-153">You restore hello database tooa new database from a backup in hello Azure Recovery Services vault.</span></span>

1. <span data-ttu-id="84a3c-154">На hello **резервных копий в хранилище Azure** выберите резервного копирования toorestore hello и нажмите кнопку **выберите**.</span><span class="sxs-lookup"><span data-stu-id="84a3c-154">On hello **Azure vault backups** page, click hello backup toorestore and then click **Select**.</span></span>

   ![Выбор резервной копии в хранилище](./media/sql-database-get-started-backup-recovery/select-backup-in-vault.png)

2. <span data-ttu-id="84a3c-156">В hello **имя базы данных** текста введите имя hello hello восстановления базы данных.</span><span class="sxs-lookup"><span data-stu-id="84a3c-156">In hello **Database name** text box, provide hello name for hello restored database.</span></span>

   ![Имя новой базы данных](./media/sql-database-get-started-backup-recovery/new-database-name.png)

3. <span data-ttu-id="84a3c-158">Нажмите кнопку **ОК** toorestore базы данных из резервной копии hello в хранилище hello toohello новой базы данных.</span><span class="sxs-lookup"><span data-stu-id="84a3c-158">Click **OK** toorestore your database from hello backup in hello vault toohello new database.</span></span>

4. <span data-ttu-id="84a3c-159">На панели инструментов hello щелкните hello уведомления значок tooview hello состояние задания восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="84a3c-159">On hello toolbar, click hello notification icon tooview hello status of hello restore job.</span></span>

   ![Ход выполнения задания восстановления из хранилища](./media/sql-database-get-started-backup-recovery/restore-job-progress-long-term.png)

5. <span data-ttu-id="84a3c-161">После завершения задания восстановления Привет открыть hello **баз данных SQL** базы данных недавно восстановленных hello tooview страницы.</span><span class="sxs-lookup"><span data-stu-id="84a3c-161">When hello restore job is completed, open hello **SQL databases** page tooview hello newly restored database.</span></span>

   ![Имя базы данных, восстановленной из хранилища](./media/sql-database-get-started-backup-recovery/restored-database-from-vault.png)

> [!NOTE]
> <span data-ttu-id="84a3c-163">Здесь можно подключиться toohello восстановить базы данных с помощью SQL Server Management Studio tooperform необходимые задачи, такие как слишком[Извлеките бит данных из toocopy базы данных восстановлена hello в hello существующей базы данных или имеющиеся hello toodelete базы данных и существующие toohello переименования hello восстановления базы данных имя базы данных](sql-database-recovery-using-backups.md#point-in-time-restore).</span><span class="sxs-lookup"><span data-stu-id="84a3c-163">From here, you can connect toohello restored database using SQL Server Management Studio tooperform needed tasks, such as too[extract a bit of data from hello restored database toocopy into hello existing database or toodelete hello existing database and rename hello restored database toohello existing database name](sql-database-recovery-using-backups.md#point-in-time-restore).</span></span>
>

## <a name="powershell"></a><span data-ttu-id="84a3c-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="84a3c-164">PowerShell</span></span>

<span data-ttu-id="84a3c-165">Привет, в следующих разделах показано, как хранилище служб восстановления Azure hello tooconfigure PowerShell toouse, просмотр резервных копий в хранилище hello и восстановление из хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="84a3c-165">hello following sections show you how toouse PowerShell tooconfigure hello Azure Recovery Services vault, view backups in hello vault, and restore from hello vault.</span></span>

### <a name="create-a-recovery-services-vault"></a><span data-ttu-id="84a3c-166">Создание хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="84a3c-166">Create a recovery services vault</span></span>

<span data-ttu-id="84a3c-167">Используйте hello [New AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) хранилища служб toocreate во время операции восстановления.</span><span class="sxs-lookup"><span data-stu-id="84a3c-167">Use hello [New-AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) toocreate a recovery services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="84a3c-168">Hello хранилища должен быть расположен в hello же регионе, что логический сервер Azure SQL hello и необходимо использовать hello же группе ресурсов, что hello логического сервера.</span><span class="sxs-lookup"><span data-stu-id="84a3c-168">hello vault must be located in hello same region as hello Azure SQL logical server, and must use hello same resource group as hello logical server.</span></span>

```PowerShell
# Create a recovery services vault

#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$serverLocation = (Get-AzureRmSqlServer -ServerName $serverName -ResourceGroupName $resourceGroupName).Location
$recoveryServiceVaultName = "{new-vault-name}"

$vault = New-AzureRmRecoveryServicesVault -Name $recoveryServiceVaultName -ResourceGroupName $ResourceGroupName -Location $serverLocation 
Set-AzureRmRecoveryServicesBackupProperties -BackupStorageRedundancy LocallyRedundant -Vault $vault
```

### <a name="set-your-server-toouse-hello-recovery-vault-for-its-long-term-retention-backups"></a><span data-ttu-id="84a3c-169">Задать hello восстановления сервера toouse хранилище для резервных копиях ее долгосрочного хранения</span><span class="sxs-lookup"><span data-stu-id="84a3c-169">Set your server toouse hello recovery vault for its long-term retention backups</span></span>

<span data-ttu-id="84a3c-170">Используйте hello [AzureRmSqlServerBackupLongTermRetentionVault набор](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) командлет tooassociate ранее созданное хранилище служб восстановления с конкретным сервером Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="84a3c-170">Use hello [Set-AzureRmSqlServerBackupLongTermRetentionVault](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) cmdlet tooassociate a previously created recovery services vault with a specific Azure SQL server.</span></span>

```PowerShell
# Set your server toouse hello vault toofor long-term backup retention 

Set-AzureRmSqlServerBackupLongTermRetentionVault -ResourceGroupName $resourceGroupName -ServerName $serverName -ResourceId $vault.Id
```

### <a name="create-a-retention-policy"></a><span data-ttu-id="84a3c-171">Создание политики хранения</span><span class="sxs-lookup"><span data-stu-id="84a3c-171">Create a retention policy</span></span>

<span data-ttu-id="84a3c-172">Политика хранения не задаются как долго tookeep резервной копии базы данных.</span><span class="sxs-lookup"><span data-stu-id="84a3c-172">A retention policy is where you set how long tookeep a database backup.</span></span> <span data-ttu-id="84a3c-173">Используйте hello [Get AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) командлет tooget hello по умолчанию хранения политики toouse как hello шаблон для создания политик.</span><span class="sxs-lookup"><span data-stu-id="84a3c-173">Use hello [Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) cmdlet tooget hello default retention policy toouse as hello template for creating policies.</span></span> <span data-ttu-id="84a3c-174">В этом шаблоне срок хранения hello задан для 2 года.</span><span class="sxs-lookup"><span data-stu-id="84a3c-174">In this template, hello retention period is set for 2 years.</span></span> <span data-ttu-id="84a3c-175">Затем выполните hello [New AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) toofinally Создание политики hello.</span><span class="sxs-lookup"><span data-stu-id="84a3c-175">Next, run hello [New-AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) toofinally create hello policy.</span></span> 

> [!NOTE]
> <span data-ttu-id="84a3c-176">Некоторые командлеты, требуют настройки контекст хранилища hello перед запуском ([AzureRmRecoveryServicesVaultContext набор](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)), вы видите этот командлет в несколько связанных фрагментов кода.</span><span class="sxs-lookup"><span data-stu-id="84a3c-176">Some cmdlets require that you set hello vault context before running ([Set-AzureRmRecoveryServicesVaultContext](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)) so you see this cmdlet in a few related snippets.</span></span> <span data-ttu-id="84a3c-177">Можно задать контекст hello, так как политика hello является частью хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="84a3c-177">You set hello context because hello policy is part of hello vault.</span></span> <span data-ttu-id="84a3c-178">Можно создать несколько политик хранения для каждого хранилища и применить политики hello требуемого toospecific-базы данных.</span><span class="sxs-lookup"><span data-stu-id="84a3c-178">You can create multiple retention policies for each vault and then apply hello desired policy toospecific databases.</span></span> 


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

### <a name="configure-a-database-toouse-hello-previously-defined-retention-policy"></a><span data-ttu-id="84a3c-179">Настроить политику хранения toouse hello ранее определенные базы данных</span><span class="sxs-lookup"><span data-stu-id="84a3c-179">Configure a database toouse hello previously defined retention policy</span></span>

<span data-ttu-id="84a3c-180">Используйте hello [AzureRmSqlDatabaseBackupLongTermRetentionPolicy набор](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) командлет tooapply hello новой политики tooa конкретной базы данных.</span><span class="sxs-lookup"><span data-stu-id="84a3c-180">Use hello [Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) cmdlet tooapply hello new policy tooa specific database.</span></span>

```PowerShell
# Enable long-term retention for a specific SQL database
$policyState = "enabled"
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -State $policyState -ResourceId $policy.Id
```

### <a name="view-backup-info-and-backups-in-long-term-retention"></a><span data-ttu-id="84a3c-181">Просмотр сведений о резервных копиях с включенной функцией долгосрочного хранения</span><span class="sxs-lookup"><span data-stu-id="84a3c-181">View backup info, and backups in long-term retention</span></span>

<span data-ttu-id="84a3c-182">Просмотрите сведения о резервных копиях базы данных в хранилище с включенной функцией [долгосрочного хранения резервных копий](sql-database-long-term-retention.md).</span><span class="sxs-lookup"><span data-stu-id="84a3c-182">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span></span> 

<span data-ttu-id="84a3c-183">Используйте следующие сведения о резервном копировании tooview командлеты hello.</span><span class="sxs-lookup"><span data-stu-id="84a3c-183">Use hello following cmdlets tooview backup information:</span></span>

- [<span data-ttu-id="84a3c-184">Get-AzureRmRecoveryServicesBackupContainer</span><span class="sxs-lookup"><span data-stu-id="84a3c-184">Get-AzureRmRecoveryServicesBackupContainer</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)
- [<span data-ttu-id="84a3c-185">Get-AzureRmRecoveryServicesBackupItem</span><span class="sxs-lookup"><span data-stu-id="84a3c-185">Get-AzureRmRecoveryServicesBackupItem</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)
- [<span data-ttu-id="84a3c-186">Get-AzureRmRecoveryServicesBackupRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="84a3c-186">Get-AzureRmRecoveryServicesBackupRecoveryPoint</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)

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

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention"></a><span data-ttu-id="84a3c-187">Восстановление базы данных из резервной копии с долгосрочным хранением</span><span class="sxs-lookup"><span data-stu-id="84a3c-187">Restore a database from a backup in long-term backup retention</span></span>

<span data-ttu-id="84a3c-188">Восстановление из долгосрочного хранения резервной копии используется hello [AzureRmSqlDatabase восстановления](/powershell/module/azurerm.sql/restore-azurermsqldatabase) командлета.</span><span class="sxs-lookup"><span data-stu-id="84a3c-188">Restoring from long-term backup retention uses hello [Restore-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) cmdlet.</span></span>

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
> <span data-ttu-id="84a3c-189">Здесь можно подключить toohello восстановления базы данных с помощью SQL Server Management Studio tooperform необходимые задачи, например tooextract бит данных из hello восстанавливается toocopy базы данных в hello существующей базы данных или существующую базу данных hello toodelete и переименования Hello восстановленной базы данных toohello именем существующей базы данных.</span><span class="sxs-lookup"><span data-stu-id="84a3c-189">From here, you can connect toohello restored database using SQL Server Management Studio tooperform needed tasks, such as tooextract a bit of data from hello restored database toocopy into hello existing database or toodelete hello existing database and rename hello restored database toohello existing database name.</span></span> <span data-ttu-id="84a3c-190">Ознакомьтесь с [восстановлением до точки во времени](sql-database-recovery-using-backups.md#point-in-time-restore).</span><span class="sxs-lookup"><span data-stu-id="84a3c-190">See [point in time restore](sql-database-recovery-using-backups.md#point-in-time-restore).</span></span>

## <a name="next-steps"></a><span data-ttu-id="84a3c-191">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="84a3c-191">Next steps</span></span>

- <span data-ttu-id="84a3c-192">toolearn о создан службы автоматического резервного копирования, в разделе [автоматического резервного копирования](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="84a3c-192">toolearn about service-generated automatic backups, see [automatic backups](sql-database-automated-backups.md)</span></span>
- <span data-ttu-id="84a3c-193">toolearn о долгосрочного хранения резервной копии, в разделе [долгосрочного хранения резервной копии](sql-database-long-term-retention.md)</span><span class="sxs-lookup"><span data-stu-id="84a3c-193">toolearn about long-term backup retention, see [long-term backup retention](sql-database-long-term-retention.md)</span></span>
- <span data-ttu-id="84a3c-194">в разделе toolearn о восстановлении из резервных копий, [восстановление из резервной копии](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="84a3c-194">toolearn about restoring from backups, see [restore from backup](sql-database-recovery-using-backups.md)</span></span>
