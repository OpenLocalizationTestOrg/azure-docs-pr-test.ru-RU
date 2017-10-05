---
title: "Настройка долгосрочного хранения резервных копий для Базы данных SQL Azure | Документация Майкрософт"
description: "Узнайте, как сохранять создаваемые автоматически резервные копии в хранилище служб восстановления Azure, а также как восстанавливать из хранилища служб восстановления Azure."
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
ms.openlocfilehash: ed9f74a59f0ca512e2758c6db4c5c9075030f859
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-restore-from-azure-sql-database-long-term-backup-retention"></a><span data-ttu-id="eea6a-103">Настройка долгосрочного хранения резервных копий для Базы данных SQL Azure и восстановление из резервной копии</span><span class="sxs-lookup"><span data-stu-id="eea6a-103">Configure and restore from Azure SQL Database long-term backup retention</span></span>

<span data-ttu-id="eea6a-104">Вы можете настроить хранилище служб восстановления Azure для хранения резервных копий баз данных SQL Azure, а затем восстановить базы данных из сохраненных резервных копий, используя портал Azure или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="eea6a-104">You can configure the Azure Recovery Services vault to store Azure SQL database backups and then recover a database using backups retained in the vault using the Azure portal or PowerShell.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="eea6a-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="eea6a-105">Azure portal</span></span>

<span data-ttu-id="eea6a-106">В следующих разделах показывается, как с помощью портала Azure настроить хранилище служб восстановления Azure, просмотреть резервные копии в хранилище и выполнить восстановление из хранилища.</span><span class="sxs-lookup"><span data-stu-id="eea6a-106">The following sections show you how to use the Azure portal to configure the Azure Recovery Services vault, view backups in the vault, and restore from the vault.</span></span>

### <a name="configure-the-vault-register-the-server-and-select-databases"></a><span data-ttu-id="eea6a-107">Настройка хранилища, регистрация сервера и выбор баз данных</span><span class="sxs-lookup"><span data-stu-id="eea6a-107">Configure the vault, register the server, and select databases</span></span>

<span data-ttu-id="eea6a-108">Вы [настроите более длительный срок хранения создаваемых автоматически резервных копий в хранилище служб восстановления Azure](sql-database-long-term-retention.md), чем для вашего уровня служб.</span><span class="sxs-lookup"><span data-stu-id="eea6a-108">You [configure an Azure Recovery Services vault to retain automated backups](sql-database-long-term-retention.md) for a period longer than the retention period for your service tier.</span></span> 

1. <span data-ttu-id="eea6a-109">Откройте страницу **SQL Server** для своего сервера.</span><span class="sxs-lookup"><span data-stu-id="eea6a-109">Open the **SQL Server** page for your server.</span></span>

   ![страница sql server](./media/sql-database-get-started-portal/sql-server-blade.png)

2. <span data-ttu-id="eea6a-111">Щелкните **Long-term backup retention** (Долгосрочное хранение резервных копий).</span><span class="sxs-lookup"><span data-stu-id="eea6a-111">Click **Long-term backup retention**.</span></span>

   ![Ссылка Long-term backup retention (Долгосрочное хранение резервных копий)](./media/sql-database-get-started-backup-recovery/long-term-backup-retention-link.png)

3. <span data-ttu-id="eea6a-113">На странице **Долгосрочное хранение архивных копий** для вашего сервера просмотрите и примите условия использования предварительной версии (если вы этого еще не сделали или эта функция по-прежнему находится на этапе предварительной версии).</span><span class="sxs-lookup"><span data-stu-id="eea6a-113">On the **Long-term backup retention** page for your server, review and accept the preview terms (unless you have already done so - or this feature is no longer in preview).</span></span>

   ![Принятие условий использования предварительной версии](./media/sql-database-get-started-backup-recovery/accept-the-preview-terms.png)

4. <span data-ttu-id="eea6a-115">Чтобы настроить долгосрочное хранение резервных копий, выберите эту базу данных в таблице и щелкните **Настройка** на панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="eea6a-115">To configure long-term backup retention, select that database in the grid and then click **Configure** on the toolbar.</span></span>

   ![Выбор базы данных для настройки долгосрочного хранения резервных копий](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

5. <span data-ttu-id="eea6a-117">На странице **Настройка** в разделе **Хранилище служб восстановления** щелкните **Настройка обязательных параметров**.</span><span class="sxs-lookup"><span data-stu-id="eea6a-117">On the **Configure** page, click **Configure required settings** under **Recovery service vault**.</span></span>

   ![Ссылка для настройки хранилища](./media/sql-database-get-started-backup-recovery/configure-vault-link.png)

6. <span data-ttu-id="eea6a-119">На странице **Хранилище служб восстановления** выберите имеющееся хранилище (при наличии).</span><span class="sxs-lookup"><span data-stu-id="eea6a-119">On the **Recovery services vault** page, select an existing vault, if any.</span></span> <span data-ttu-id="eea6a-120">Если хранилище служб восстановления отсутствует, щелкните, чтобы выйти, и создайте хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="eea6a-120">Otherwise, if no recovery services vault found for your subscription, click to exit the flow and create a recovery services vault.</span></span>

   ![ссылка на создание хранилища](./media/sql-database-get-started-backup-recovery/create-new-vault-link.png)

7. <span data-ttu-id="eea6a-122">На странице **Хранилища служб восстановления** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="eea6a-122">On the **Recovery Services vaults** page, click **Add**.</span></span>

   ![ссылка на добавление хранилища](./media/sql-database-get-started-backup-recovery/add-new-vault-link.png)
   
8. <span data-ttu-id="eea6a-124">На странице **Хранилище служб восстановления** введите допустимое имя для хранилища служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="eea6a-124">On the **Recovery Services vault** page, provide a valid name for the Recovery Services vault.</span></span>

   ![Имя нового хранилища](./media/sql-database-get-started-backup-recovery/new-vault-name.png)

9. <span data-ttu-id="eea6a-126">Выберите подписку и группу ресурсов, а затем выберите расположение хранилища.</span><span class="sxs-lookup"><span data-stu-id="eea6a-126">Select your subscription and resource group, and then select the location for the vault.</span></span> <span data-ttu-id="eea6a-127">По завершении нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="eea6a-127">When done, click **Create**.</span></span>

   ![создание хранилища](./media/sql-database-get-started-backup-recovery/create-new-vault.png)

   > [!IMPORTANT]
   > <span data-ttu-id="eea6a-129">Хранилище должно находиться в том же регионе, что и логический сервер Azure SQL Server, и использовать ту же группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="eea6a-129">The vault must be located in the same region as the Azure SQL logical server, and must use the same resource group as the logical server.</span></span>
   >

10. <span data-ttu-id="eea6a-130">После создания хранилища вернитесь на страницу **Хранилище служб восстановления**.</span><span class="sxs-lookup"><span data-stu-id="eea6a-130">After the new vault is created, execute the necessary steps to return to the **Recovery services vault** page.</span></span>

11. <span data-ttu-id="eea6a-131">На странице **Хранилище служб восстановления** щелкните хранилище, а затем нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="eea6a-131">On the **Recovery services vault** page, click the vault and then click **Select**.</span></span>

   ![Выбор имеющегося хранилища](./media/sql-database-get-started-backup-recovery/select-existing-vault.png)

12. <span data-ttu-id="eea6a-133">На странице **Настройка** введите допустимое имя для новой политики хранения, измените ее должным образом и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="eea6a-133">On the **Configure** page, provide a valid name for the new retention policy, modify the default retention policy as appropriate, and then click **OK**.</span></span>

   ![Определение политики хранения](./media/sql-database-get-started-backup-recovery/define-retention-policy.png)

13. <span data-ttu-id="eea6a-135">На странице **Долгосрочное хранение архивных копий** для вашей базы данных щелкните **Сохранить**, а затем нажмите кнопку **ОК**, чтобы применить политику долгосрочного хранения резервных копий ко всем выбранным базам данных.</span><span class="sxs-lookup"><span data-stu-id="eea6a-135">On the **Long-term backup retention** page for your database, click **Save** and then click **OK** to apply the long-term backup retention policy to all selected databases.</span></span>

   ![Определение политики хранения](./media/sql-database-get-started-backup-recovery/save-retention-policy.png)

14. <span data-ttu-id="eea6a-137">Щелкните **Сохранить**, чтобы включить новую политику долгосрочного хранения резервных копий в настроенном хранилище служб восстановления Azure.</span><span class="sxs-lookup"><span data-stu-id="eea6a-137">Click **Save** to enable long-term backup retention using this new policy to the Azure Recovery Services vault that you configured.</span></span>

   ![Определение политики хранения](./media/sql-database-get-started-backup-recovery/enable-long-term-retention.png)

> [!IMPORTANT]
> <span data-ttu-id="eea6a-139">После настройки резервные копии появятся в хранилище в течение следующих семи дней.</span><span class="sxs-lookup"><span data-stu-id="eea6a-139">Once configured, backups show up in the vault within next seven days.</span></span> <span data-ttu-id="eea6a-140">Не выполняйте следующие этапы до появления резервных копий в хранилище.</span><span class="sxs-lookup"><span data-stu-id="eea6a-140">Do not continue this tutorial until backups show up in the vault.</span></span>
>

### <a name="view-backups-in-long-term-retention-using-azure-portal"></a><span data-ttu-id="eea6a-141">Просмотр резервных копий долгосрочного хранения с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="eea6a-141">View backups in long-term retention using Azure portal</span></span>

<span data-ttu-id="eea6a-142">Просмотрите сведения о резервных копиях базы данных в хранилище с включенной функцией [долгосрочного хранения резервных копий](sql-database-long-term-retention.md).</span><span class="sxs-lookup"><span data-stu-id="eea6a-142">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span></span> 

1. <span data-ttu-id="eea6a-143">На портале Azure откройте хранилище служб восстановления Azure, где хранятся резервные копии вашей базы данных (щелкните **Все ресурсы** и выберите его из списка ресурсов вашей подписки), чтобы просмотреть сведения об объеме хранилища, используемого для хранения резервных копий базы данных.</span><span class="sxs-lookup"><span data-stu-id="eea6a-143">In the Azure portal, open your Azure Recovery Services vault for your database backups (go to **All resources** and select it from the list of resources for your subscription) to view the amount of storage used by your database backups in the vault.</span></span>

   ![Просмотр хранилища служб восстановления с резервными копиями](./media/sql-database-get-started-backup-recovery/view-recovery-services-vault-with-data.png)

2. <span data-ttu-id="eea6a-145">Откройте страницу **База данных SQL** для своей базы данных.</span><span class="sxs-lookup"><span data-stu-id="eea6a-145">Open the **SQL database** page for your database.</span></span>

   ![страница нового примера базы данных](./media/sql-database-get-started-portal/new-sample-db-blade.png)

3. <span data-ttu-id="eea6a-147">На панели инструментов щелкните **Восстановить**.</span><span class="sxs-lookup"><span data-stu-id="eea6a-147">On the toolbar, click **Restore**.</span></span>

   ![Элемент "Восстановить" на панели инструментов](./media/sql-database-get-started-backup-recovery/restore-toolbar.png)

4. <span data-ttu-id="eea6a-149">На странице "Восстановление" щелкните **Долгосрочные**.</span><span class="sxs-lookup"><span data-stu-id="eea6a-149">On the Restore page, click **Long-term**.</span></span>

5. <span data-ttu-id="eea6a-150">В разделе Azure vault backups (Резервные копии хранилища Azure) щелкните **Выберите архив**, чтобы просмотреть список доступных резервных копий с долгосрочным хранением.</span><span class="sxs-lookup"><span data-stu-id="eea6a-150">Under Azure vault backups, click **Select a backup** to view the available database backups in long-term backup retention.</span></span>

   ![Резервные копии в хранилище](./media/sql-database-get-started-backup-recovery/view-backups-in-vault.png)

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention-using-the-azure-portal"></a><span data-ttu-id="eea6a-152">Восстановление базы данных из резервной копии долгосрочного хранения с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="eea6a-152">Restore a database from a backup in long-term backup retention using the Azure portal</span></span>

<span data-ttu-id="eea6a-153">Вы восстановите имеющуюся базу данных из резервной копии, расположенной в хранилище служб восстановления Azure, в новую базу данных.</span><span class="sxs-lookup"><span data-stu-id="eea6a-153">You restore the database to a new database from a backup in the Azure Recovery Services vault.</span></span>

1. <span data-ttu-id="eea6a-154">На странице **Архивные копии в хранилище Azure** щелкните резервную копию, которую необходимо восстановить, а затем нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="eea6a-154">On the **Azure vault backups** page, click the backup to restore and then click **Select**.</span></span>

   ![Выбор резервной копии в хранилище](./media/sql-database-get-started-backup-recovery/select-backup-in-vault.png)

2. <span data-ttu-id="eea6a-156">В текстовом поле **Имя базы данных** введите имя для восстановленной базы данных.</span><span class="sxs-lookup"><span data-stu-id="eea6a-156">In the **Database name** text box, provide the name for the restored database.</span></span>

   ![Имя новой базы данных](./media/sql-database-get-started-backup-recovery/new-database-name.png)

3. <span data-ttu-id="eea6a-158">Нажмите кнопку **ОК**, чтобы восстановить базу данных из резервной копии, расположенной в хранилище, в новую базу данных.</span><span class="sxs-lookup"><span data-stu-id="eea6a-158">Click **OK** to restore your database from the backup in the vault to the new database.</span></span>

4. <span data-ttu-id="eea6a-159">На панели инструментов щелкните значок уведомления, чтобы просмотреть состояние задания восстановления.</span><span class="sxs-lookup"><span data-stu-id="eea6a-159">On the toolbar, click the notification icon to view the status of the restore job.</span></span>

   ![Ход выполнения задания восстановления из хранилища](./media/sql-database-get-started-backup-recovery/restore-job-progress-long-term.png)

5. <span data-ttu-id="eea6a-161">После завершения задания откройте страницу **Базы данных SQL**, чтобы просмотреть восстановленную базу данных.</span><span class="sxs-lookup"><span data-stu-id="eea6a-161">When the restore job is completed, open the **SQL databases** page to view the newly restored database.</span></span>

   ![Имя базы данных, восстановленной из хранилища](./media/sql-database-get-started-backup-recovery/restored-database-from-vault.png)

> [!NOTE]
> <span data-ttu-id="eea6a-163">Здесь вы можете подключиться к восстановленной базе данных с помощью SQL Server Management Studio и выполнить необходимые задания, например [извлечь часть данных из восстановленной базы данных, чтобы скопировать их в имеющуюся базу данных, или удалить имеющуюся базу данных и присвоить ее имя восстановленной базе данных](sql-database-recovery-using-backups.md#point-in-time-restore).</span><span class="sxs-lookup"><span data-stu-id="eea6a-163">From here, you can connect to the restored database using SQL Server Management Studio to perform needed tasks, such as to [extract a bit of data from the restored database to copy into the existing database or to delete the existing database and rename the restored database to the existing database name](sql-database-recovery-using-backups.md#point-in-time-restore).</span></span>
>

## <a name="powershell"></a><span data-ttu-id="eea6a-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="eea6a-164">PowerShell</span></span>

<span data-ttu-id="eea6a-165">В следующих разделах показывается, как с помощью PowerShell настроить хранилище служб восстановления Azure, просмотреть резервные копии в хранилище и выполнить восстановление из хранилища.</span><span class="sxs-lookup"><span data-stu-id="eea6a-165">The following sections show you how to use PowerShell to configure the Azure Recovery Services vault, view backups in the vault, and restore from the vault.</span></span>

### <a name="create-a-recovery-services-vault"></a><span data-ttu-id="eea6a-166">Создание хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="eea6a-166">Create a recovery services vault</span></span>

<span data-ttu-id="eea6a-167">Воспользуйтесь командлетом [New-AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault), чтобы создать хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="eea6a-167">Use the [New-AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) to create a recovery services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eea6a-168">Хранилище должно находиться в том же регионе, что и логический сервер Azure SQL Server, и использовать ту же группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="eea6a-168">The vault must be located in the same region as the Azure SQL logical server, and must use the same resource group as the logical server.</span></span>

```PowerShell
# Create a recovery services vault

#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$serverLocation = (Get-AzureRmSqlServer -ServerName $serverName -ResourceGroupName $resourceGroupName).Location
$recoveryServiceVaultName = "{new-vault-name}"

$vault = New-AzureRmRecoveryServicesVault -Name $recoveryServiceVaultName -ResourceGroupName $ResourceGroupName -Location $serverLocation 
Set-AzureRmRecoveryServicesBackupProperties -BackupStorageRedundancy LocallyRedundant -Vault $vault
```

### <a name="set-your-server-to-use-the-recovery-vault-for-its-long-term-retention-backups"></a><span data-ttu-id="eea6a-169">Настройка сервера на использование хранилища служб восстановления для долгосрочного хранения резервных копий</span><span class="sxs-lookup"><span data-stu-id="eea6a-169">Set your server to use the recovery vault for its long-term retention backups</span></span>

<span data-ttu-id="eea6a-170">Воспользуйтесь командлетом [Set-AzureRmSqlServerBackupLongTermRetentionVault](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault), чтобы связать созданное ранее хранилище служб восстановления с определенным сервером SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="eea6a-170">Use the [Set-AzureRmSqlServerBackupLongTermRetentionVault](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) cmdlet to associate a previously created recovery services vault with a specific Azure SQL server.</span></span>

```PowerShell
# Set your server to use the vault to for long-term backup retention 

Set-AzureRmSqlServerBackupLongTermRetentionVault -ResourceGroupName $resourceGroupName -ServerName $serverName -ResourceId $vault.Id
```

### <a name="create-a-retention-policy"></a><span data-ttu-id="eea6a-171">Создание политики хранения</span><span class="sxs-lookup"><span data-stu-id="eea6a-171">Create a retention policy</span></span>

<span data-ttu-id="eea6a-172">Политика хранения определяет срок хранения резервной копии базы данных.</span><span class="sxs-lookup"><span data-stu-id="eea6a-172">A retention policy is where you set how long to keep a database backup.</span></span> <span data-ttu-id="eea6a-173">Воспользуйтесь командлетом [Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject), чтобы получить политику хранения по умолчанию. Она будет использоваться как шаблон при создании других политик.</span><span class="sxs-lookup"><span data-stu-id="eea6a-173">Use the [Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) cmdlet to get the default retention policy to use as the template for creating policies.</span></span> <span data-ttu-id="eea6a-174">В этом шаблоне для срока хранения задано значение 2 года.</span><span class="sxs-lookup"><span data-stu-id="eea6a-174">In this template, the retention period is set for 2 years.</span></span> <span data-ttu-id="eea6a-175">Затем выполните командлет [New-AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy), чтобы создать политику.</span><span class="sxs-lookup"><span data-stu-id="eea6a-175">Next, run the [New-AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) to finally create the policy.</span></span> 

> [!NOTE]
> <span data-ttu-id="eea6a-176">Для некоторых командлетов необходимо настроить контекст хранилища перед выполнением ([Set-AzureRmRecoveryServicesVaultContext](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)). Поэтому вы увидите этот командлет в нескольких связанных фрагментах кода.</span><span class="sxs-lookup"><span data-stu-id="eea6a-176">Some cmdlets require that you set the vault context before running ([Set-AzureRmRecoveryServicesVaultContext](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)) so you see this cmdlet in a few related snippets.</span></span> <span data-ttu-id="eea6a-177">Контекст необходимо настроить, так как политика является частью хранилища.</span><span class="sxs-lookup"><span data-stu-id="eea6a-177">You set the context because the policy is part of the vault.</span></span> <span data-ttu-id="eea6a-178">Вы можете создать несколько политик хранения для каждого хранилища, а затем применять требуемую политику для указанных баз данных.</span><span class="sxs-lookup"><span data-stu-id="eea6a-178">You can create multiple retention policies for each vault and then apply the desired policy to specific databases.</span></span> 


```PowerShell
# Retrieve the default retention policy for the AzureSQLDatabase workload type
$retentionPolicy = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType AzureSQLDatabase

# Set the retention value to two years (you can set to any time between 1 week and 10 years)
$retentionPolicy.RetentionDurationType = "Years"
$retentionPolicy.RetentionCount = 2
$retentionPolicyName = "my2YearRetentionPolicy"

# Set the vault context to the vault you are creating the policy for
Set-AzureRmRecoveryServicesVaultContext -Vault $vault

# Create the new policy
$policy = New-AzureRmRecoveryServicesBackupProtectionPolicy -name $retentionPolicyName -WorkloadType AzureSQLDatabase -retentionPolicy $retentionPolicy
$policy
```

### <a name="configure-a-database-to-use-the-previously-defined-retention-policy"></a><span data-ttu-id="eea6a-179">Настройка базы данных для использования ранее определенной политики хранения</span><span class="sxs-lookup"><span data-stu-id="eea6a-179">Configure a database to use the previously defined retention policy</span></span>

<span data-ttu-id="eea6a-180">Воспользуйтесь командлетом [Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy), чтобы применить новую политику к определенной базе данных.</span><span class="sxs-lookup"><span data-stu-id="eea6a-180">Use the [Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) cmdlet to apply the new policy to a specific database.</span></span>

```PowerShell
# Enable long-term retention for a specific SQL database
$policyState = "enabled"
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -State $policyState -ResourceId $policy.Id
```

### <a name="view-backup-info-and-backups-in-long-term-retention"></a><span data-ttu-id="eea6a-181">Просмотр сведений о резервных копиях с включенной функцией долгосрочного хранения</span><span class="sxs-lookup"><span data-stu-id="eea6a-181">View backup info, and backups in long-term retention</span></span>

<span data-ttu-id="eea6a-182">Просмотрите сведения о резервных копиях базы данных в хранилище с включенной функцией [долгосрочного хранения резервных копий](sql-database-long-term-retention.md).</span><span class="sxs-lookup"><span data-stu-id="eea6a-182">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span></span> 

<span data-ttu-id="eea6a-183">Воспользуйтесь следующими командлетами для просмотра сведений о резервных копиях:</span><span class="sxs-lookup"><span data-stu-id="eea6a-183">Use the following cmdlets to view backup information:</span></span>

- [<span data-ttu-id="eea6a-184">Get-AzureRmRecoveryServicesBackupContainer</span><span class="sxs-lookup"><span data-stu-id="eea6a-184">Get-AzureRmRecoveryServicesBackupContainer</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)
- [<span data-ttu-id="eea6a-185">Get-AzureRmRecoveryServicesBackupItem</span><span class="sxs-lookup"><span data-stu-id="eea6a-185">Get-AzureRmRecoveryServicesBackupItem</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)
- [<span data-ttu-id="eea6a-186">Get-AzureRmRecoveryServicesBackupRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="eea6a-186">Get-AzureRmRecoveryServicesBackupRecoveryPoint</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)

```PowerShell
#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$databaseNeedingRestore = $databaseName

# Set the vault context to the vault we want to restore from
#$vault = Get-AzureRmRecoveryServicesVault -ResourceGroupName $resourceGroupName
Set-AzureRmRecoveryServicesVaultContext -Vault $vault

# the following commands find the container associated with the server 'myserver' under resource group 'myresourcegroup'
$container = Get-AzureRmRecoveryServicesBackupContainer -ContainerType AzureSQL -FriendlyName $vault.Name

# Get the long-term retention metadata associated with a specific database
$item = Get-AzureRmRecoveryServicesBackupItem -Container $container -WorkloadType AzureSQLDatabase -Name $databaseNeedingRestore

# Get all available backups for the previously indicated database
# Optionally, set the -StartDate and -EndDate parameters to return backups within a specific time period
$availableBackups = Get-AzureRmRecoveryServicesBackupRecoveryPoint -Item $item
$availableBackups
```

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention"></a><span data-ttu-id="eea6a-187">Восстановление базы данных из резервной копии с долгосрочным хранением</span><span class="sxs-lookup"><span data-stu-id="eea6a-187">Restore a database from a backup in long-term backup retention</span></span>

<span data-ttu-id="eea6a-188">Для восстановления из резервной копии долгосрочного хранения используется командлет [Restore-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase).</span><span class="sxs-lookup"><span data-stu-id="eea6a-188">Restoring from long-term backup retention uses the [Restore-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) cmdlet.</span></span>

```PowerShell
# Restore the most recent backup: $availableBackups[0]
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
> <span data-ttu-id="eea6a-189">Здесь вы можете подключиться к восстановленной базе данных с помощью SQL Server Management Studio и выполнить необходимые задания, например извлечь часть данных из восстановленной базы данных, чтобы скопировать их в имеющуюся базу данных или удалить имеющуюся базу данных и присвоить ее имя восстановленной базе данных.</span><span class="sxs-lookup"><span data-stu-id="eea6a-189">From here, you can connect to the restored database using SQL Server Management Studio to perform needed tasks, such as to extract a bit of data from the restored database to copy into the existing database or to delete the existing database and rename the restored database to the existing database name.</span></span> <span data-ttu-id="eea6a-190">Ознакомьтесь с [восстановлением до точки во времени](sql-database-recovery-using-backups.md#point-in-time-restore).</span><span class="sxs-lookup"><span data-stu-id="eea6a-190">See [point in time restore](sql-database-recovery-using-backups.md#point-in-time-restore).</span></span>

## <a name="next-steps"></a><span data-ttu-id="eea6a-191">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="eea6a-191">Next steps</span></span>

- <span data-ttu-id="eea6a-192">Дополнительные сведения о резервных копиях базы данных, создаваемых автоматически службой, см. в [этой статье](sql-database-automated-backups.md).</span><span class="sxs-lookup"><span data-stu-id="eea6a-192">To learn about service-generated automatic backups, see [automatic backups](sql-database-automated-backups.md)</span></span>
- <span data-ttu-id="eea6a-193">Дополнительные сведения о долгосрочном хранении резервных копий см. в статье [Хранение резервных копий базы данных SQL Azure до 10 лет](sql-database-long-term-retention.md).</span><span class="sxs-lookup"><span data-stu-id="eea6a-193">To learn about long-term backup retention, see [long-term backup retention](sql-database-long-term-retention.md)</span></span>
- <span data-ttu-id="eea6a-194">Дополнительные сведения о восстановлении из резервных копий см. в статье [Восстановление базы данных Azure SQL с помощью создаваемых автоматически резервных копий](sql-database-recovery-using-backups.md).</span><span class="sxs-lookup"><span data-stu-id="eea6a-194">To learn about restoring from backups, see [restore from backup](sql-database-recovery-using-backups.md)</span></span>
