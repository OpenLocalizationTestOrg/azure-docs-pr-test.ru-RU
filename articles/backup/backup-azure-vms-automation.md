---
title: "aaaDeploy и управлять резервными копиями для развертывания диспетчера ресурсов виртуальных машин с помощью PowerShell | Документы Microsoft"
description: "Использование PowerShell toodeploy и управление ими резервных копий в Azure для развертывания диспетчера ресурсов виртуальных машин"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 68606e4f-536d-4eac-9f80-8a198ea94d52
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/28/2017
ms.author: markgal;trinadhk
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 486fb3ae1902403fe6bf303df57244b76677ab17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azurermrecoveryservicesbackup-cmdlets-tooback-up-virtual-machines"></a><span data-ttu-id="16dfe-103">Использовать tooback командлеты AzureRM.RecoveryServices.Backup копирование виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="16dfe-103">Use AzureRM.RecoveryServices.Backup cmdlets tooback up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="16dfe-104">Диспетчер ресурсов</span><span class="sxs-lookup"><span data-stu-id="16dfe-104">Resource Manager</span></span>](backup-azure-vms-automation.md)
> * [<span data-ttu-id="16dfe-105">Классический</span><span class="sxs-lookup"><span data-stu-id="16dfe-105">Classic</span></span>](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="16dfe-106">В этой статье показано, как хранилище tooback командлеты Azure PowerShell toouse копирование и восстановление из службы восстановления Azure виртуальной машины (VM).</span><span class="sxs-lookup"><span data-stu-id="16dfe-106">This article shows you how toouse Azure PowerShell cmdlets tooback up and recover an Azure virtual machine (VM) from a Recovery Services vault.</span></span> <span data-ttu-id="16dfe-107">Хранилище служб восстановления — ресурс диспетчера ресурсов Azure и tooprotect используемых данных и средств в службах архивации Azure и Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="16dfe-107">A Recovery Services vault is an Azure Resource Manager resource and is used tooprotect data and assets in both Azure Backup and Azure Site Recovery services.</span></span> <span data-ttu-id="16dfe-108">Можно использовать tooprotect хранилище служб восстановления Azure Service Manager развернутые виртуальные машины и виртуальные машины на развертывания диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="16dfe-108">You can use a Recovery Services vault tooprotect Azure Service Manager-deployed VMs, and Azure Resource Manager-deployed VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="16dfe-109">В Azure предусмотрены две модели развертывания, позволяющие создавать ресурсы и работать с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="16dfe-109">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="16dfe-110">Эта статья предназначена для использования с виртуальными машинами, созданных с помощью модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="16dfe-110">This article is for use with VMs created using hello Resource Manager model.</span></span>
>
>

<span data-ttu-id="16dfe-111">В этой статье описывается с помощью PowerShell tooprotect виртуальной Машины и восстановление данных из точки восстановления.</span><span class="sxs-lookup"><span data-stu-id="16dfe-111">This article walks you through using PowerShell tooprotect a VM, and restore data from a recovery point.</span></span>

## <a name="concepts"></a><span data-ttu-id="16dfe-112">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="16dfe-112">Concepts</span></span>
<span data-ttu-id="16dfe-113">Если вы не знакомы с hello службы архивации Azure, общие сведения о службе hello извлечь [возможности резервного копирования Azure?](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="16dfe-113">If you are not familiar with hello Azure Backup service, for an overview of hello service, check out [What is Azure Backup?](backup-introduction-to-azure-backup.md)</span></span> <span data-ttu-id="16dfe-114">Прежде чем начать, убедитесь, что охватывают hello essentials о toowork hello предварительных требований с помощью Azure Backup и hello ограничения текущее решение резервного копирования hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="16dfe-114">Before you start, ensure that you cover hello essentials about hello prerequisites needed toowork with Azure Backup, and hello limitations of hello current VM backup solution.</span></span>

<span data-ttu-id="16dfe-115">toouse PowerShell по сути, это необходимые toounderstand hello иерархия объектов и откуда toostart.</span><span class="sxs-lookup"><span data-stu-id="16dfe-115">toouse PowerShell effectively, it is necessary toounderstand hello hierarchy of objects and from where toostart.</span></span>

![Иерархия объектов служб восстановления](./media/backup-azure-vms-arm-automation/recovery-services-object-hierarchy.png)

<span data-ttu-id="16dfe-117">hello tooview Справочник по командлетам AzureRm.RecoveryServices.Backup PowerShell, в разделе hello [архивации Azure — командлеты служб восстановления](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) в hello библиотека Azure.</span><span class="sxs-lookup"><span data-stu-id="16dfe-117">tooview hello AzureRm.RecoveryServices.Backup PowerShell cmdlet reference, see hello [Azure Backup - Recovery Services Cmdlets](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) in hello Azure library.</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="16dfe-118">Настройка и регистрация</span><span class="sxs-lookup"><span data-stu-id="16dfe-118">Setup and Registration</span></span>
<span data-ttu-id="16dfe-119">toobegin:</span><span class="sxs-lookup"><span data-stu-id="16dfe-119">toobegin:</span></span>

1. <span data-ttu-id="16dfe-120">[Загрузка последней версии PowerShell hello](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (hello Минимальная требуемая версия —: 1.4.0)</span><span class="sxs-lookup"><span data-stu-id="16dfe-120">[Download hello latest version of PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (hello minimum version required is: 1.4.0)</span></span>
2. <span data-ttu-id="16dfe-121">Находите hello доступных командлетов Azure PowerShell резервного копирования с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="16dfe-121">Find hello Azure Backup PowerShell cmdlets available by typing hello following command:</span></span>

```
PS C:\> Get-Command *azurermrecoveryservices*

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Backup-AzureRmRecoveryServicesBackupItem           1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Disable-AzureRmRecoveryServicesBackupProtection    1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Enable-AzureRmRecoveryServicesBackupProtection     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupContainer         1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupItem              1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupJob               1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupJobDetails        1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupManagementServer  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupProperties        1.4.0      AzureRM.RecoveryServices
Cmdlet          Get-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRMRecoveryServicesBackupRecoveryPoint     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupRetentionPolic... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupSchedulePolicy... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesVault                   1.4.0      AzureRM.RecoveryServices
Cmdlet          Get-AzureRmRecoveryServicesVaultSettingsFile       1.4.0      AzureRM.RecoveryServices
Cmdlet          New-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          New-AzureRmRecoveryServicesVault                   1.4.0      AzureRM.RecoveryServices
Cmdlet          Remove-AzureRmRecoveryServicesProtectionPolicy     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Remove-AzureRmRecoveryServicesVault                1.4.0      AzureRM.RecoveryServices
Cmdlet          Restore-AzureRMRecoveryServicesBackupItem          1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Set-AzureRmRecoveryServicesBackupProperties        1.4.0      AzureRM.RecoveryServices
Cmdlet          Set-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Set-AzureRmRecoveryServicesVaultContext            1.4.0      AzureRM.RecoveryServices
Cmdlet          Stop-AzureRmRecoveryServicesBackupJob              1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Unregister-AzureRmRecoveryServicesBackupContainer  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Unregister-AzureRmRecoveryServicesBackupManagem... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Wait-AzureRmRecoveryServicesBackupJob              1.4.0      AzureRM.RecoveryServices.Backup
```


<span data-ttu-id="16dfe-122">с помощью PowerShell можно автоматизировать Hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="16dfe-122">hello following tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="16dfe-123">Создание хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="16dfe-123">Create a Recovery Services vault</span></span>
* <span data-ttu-id="16dfe-124">Резервное копирование виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="16dfe-124">Back up Azure VMs</span></span>
* <span data-ttu-id="16dfe-125">активация задания архивации;</span><span class="sxs-lookup"><span data-stu-id="16dfe-125">Trigger a backup job</span></span>
* <span data-ttu-id="16dfe-126">наблюдение за выполнением задания архивации;</span><span class="sxs-lookup"><span data-stu-id="16dfe-126">Monitor a backup job</span></span>
* <span data-ttu-id="16dfe-127">Восстановление виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="16dfe-127">Restore an Azure VM</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="16dfe-128">Создание хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="16dfe-128">Create a recovery services vault</span></span>
<span data-ttu-id="16dfe-129">Привет, следующие шаги, чтобы привести по созданию хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="16dfe-129">hello following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="16dfe-130">Хранилище служб восстановления отличается от хранилища службы архивации.</span><span class="sxs-lookup"><span data-stu-id="16dfe-130">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="16dfe-131">При использовании резервного копирования Azure для hello первый раз, необходимо использовать hello  **[регистра AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)**  поставщика службы восстановления Azure hello tooregister командлетов с вашей подпиской.</span><span class="sxs-lookup"><span data-stu-id="16dfe-131">If you are using Azure Backup for hello first time, you must use hello **[Register-AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)** cmdlet tooregister hello Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="16dfe-132">Hello хранилище служб восстановления является ресурса диспетчера ресурсов, поэтому вам необходимо tooplace его в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="16dfe-132">hello Recovery Services vault is a Resource Manager resource, so you need tooplace it within a resource group.</span></span> <span data-ttu-id="16dfe-133">Можно использовать существующую группу ресурсов или создайте группу ресурсов с hello  **[New AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)**  командлета.</span><span class="sxs-lookup"><span data-stu-id="16dfe-133">You can use an existing resource group, or create a resource group with hello **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)** cmdlet.</span></span> <span data-ttu-id="16dfe-134">При создании группы ресурсов, укажите hello имя и расположение для группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="16dfe-134">When creating a resource group, specify hello name and location for hello resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="16dfe-135">Используйте hello  **[New AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)**  hello toocreate командлет хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="16dfe-135">Use hello **[New-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)** cmdlet toocreate hello Recovery Services vault.</span></span> <span data-ttu-id="16dfe-136">Убедитесь, что toospecify hello одинаковое расположение для hello хранилище, которое использовалось для группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="16dfe-136">Be sure toospecify hello same location for hello vault as was used for hello resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="16dfe-137">Укажите тип hello toouse избыточности хранилища; можно использовать [локально избыточное хранилище (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) или [географически избыточное хранилище (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="16dfe-137">Specify hello type of storage redundancy toouse; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="16dfe-138">Hello следующий пример демонстрирует hello - BackupStorageRedundancy для testvault был установлен tooGeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="16dfe-138">hello following example shows hello -BackupStorageRedundancy option for testvault is set tooGeoRedundant.</span></span>

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testvault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -Vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

   > [!TIP]
   > <span data-ttu-id="16dfe-139">Многие командлеты службы архивации Azure в качестве входных данных необходим объект хранилища служб восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="16dfe-139">Many Azure Backup cmdlets require hello Recovery Services vault object as an input.</span></span> <span data-ttu-id="16dfe-140">По этой причине — это объект хранилища служб восстановления резервной копии удобный toostore hello в переменной.</span><span class="sxs-lookup"><span data-stu-id="16dfe-140">For this reason, it is convenient toostore hello Backup Recovery Services vault object in a variable.</span></span>
   >
   >

## <a name="view-hello-vaults-in-a-subscription"></a><span data-ttu-id="16dfe-141">Представление hello хранилища в подписке</span><span class="sxs-lookup"><span data-stu-id="16dfe-141">View hello vaults in a subscription</span></span>
<span data-ttu-id="16dfe-142">Используйте  **[Get AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)**  tooview hello список всех хранилищ в текущей подписке hello.</span><span class="sxs-lookup"><span data-stu-id="16dfe-142">Use **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)** tooview hello list of all vaults in hello current subscription.</span></span> <span data-ttu-id="16dfe-143">Можно использовать этот toocheck команд, созданного новое хранилище, или toosee hello хранилищ, доступных в подписке hello.</span><span class="sxs-lookup"><span data-stu-id="16dfe-143">You can use this command toocheck that a new vault was created, or toosee hello available vaults in hello subscription.</span></span>

<span data-ttu-id="16dfe-144">Запустите команду Get-AzureRmRecoveryServicesVault tooview hello всех хранилищ в подписке hello.</span><span class="sxs-lookup"><span data-stu-id="16dfe-144">Run hello command, Get-AzureRmRecoveryServicesVault, tooview all vaults in hello subscription.</span></span> <span data-ttu-id="16dfe-145">Hello пример hello сведений, отображаемых для каждого хранилища.</span><span class="sxs-lookup"><span data-stu-id="16dfe-145">hello following example shows hello information displayed for each vault.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesVault
Name              : Contoso-vault
ID                : /subscriptions/1234
Type              : Microsoft.RecoveryServices/vaults
Location          : WestUS
ResourceGroupName : Contoso-docs-rg
SubscriptionId    : 1234-567f-8910-abc
Properties        : Microsoft.Azure.Commands.RecoveryServices.ARSVaultProperties
```


## <a name="back-up-azure-vms"></a><span data-ttu-id="16dfe-146">Резервное копирование виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="16dfe-146">Back up Azure VMs</span></span>
<span data-ttu-id="16dfe-147">Используйте хранилище служб восстановления tooprotect виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="16dfe-147">Use a Recovery Services vault tooprotect your virtual machines.</span></span> <span data-ttu-id="16dfe-148">Перед установкой защиты hello hello в контексте хранилища (тип данных, защищенных в хранилище hello hello) и проверьте политику защиты hello.</span><span class="sxs-lookup"><span data-stu-id="16dfe-148">Before you apply hello protection, set hello vault context (hello type of data protected in hello vault), and verify hello protection policy.</span></span> <span data-ttu-id="16dfe-149">Политика защиты Hello — hello планирование запуска заданий резервного копирования hello и длительность хранения каждого резервного копирования моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="16dfe-149">hello protection policy is hello schedule when hello backup jobs run, and how long each backup snapshot is retained.</span></span>

### <a name="set-vault-context"></a><span data-ttu-id="16dfe-150">Задание контекста хранилища</span><span class="sxs-lookup"><span data-stu-id="16dfe-150">Set vault context</span></span>
<span data-ttu-id="16dfe-151">Прежде чем включать защиту на виртуальной Машине, используйте  **[набор AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  tooset hello хранилище контекста.</span><span class="sxs-lookup"><span data-stu-id="16dfe-151">Before enabling protection on a VM, use **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** tooset hello vault context.</span></span> <span data-ttu-id="16dfe-152">После установки контекста хранилище hello, оно применяется tooall последующими командлетами.</span><span class="sxs-lookup"><span data-stu-id="16dfe-152">Once hello vault context is set, it applies tooall subsequent cmdlets.</span></span> <span data-ttu-id="16dfe-153">Hello следующий пример устанавливает hello хранилище контекст для хранилища hello *testvault*.</span><span class="sxs-lookup"><span data-stu-id="16dfe-153">hello following example sets hello vault context for hello vault, *testvault*.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesVault -Name "testvault" | Set-AzureRmRecoveryServicesVaultContext
```

### <a name="create-a-protection-policy"></a><span data-ttu-id="16dfe-154">Создание политики защиты</span><span class="sxs-lookup"><span data-stu-id="16dfe-154">Create a protection policy</span></span>
<span data-ttu-id="16dfe-155">Создаваемое хранилище служб восстановления поставляется с политиками защиты и хранения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="16dfe-155">When you create a Recovery Services vault, it comes with default protection and retention policies.</span></span> <span data-ttu-id="16dfe-156">Политика защиты по умолчанию Hello триггеры задания резервного копирования каждый день в указанное время.</span><span class="sxs-lookup"><span data-stu-id="16dfe-156">hello default protection policy triggers a backup job each day at a specified time.</span></span> <span data-ttu-id="16dfe-157">политики хранения по умолчанию Hello хранит hello ежедневных точки восстановления в течение 30 дней.</span><span class="sxs-lookup"><span data-stu-id="16dfe-157">hello default retention policy retains hello daily recovery point for 30 days.</span></span> <span data-ttu-id="16dfe-158">Можно использовать по умолчанию hello tooquickly политики защиты виртуальной Машины и изменение политики hello позже с помощью различных сведений.</span><span class="sxs-lookup"><span data-stu-id="16dfe-158">You can use hello default policy tooquickly protect your VM and edit hello policy later with different details.</span></span>

<span data-ttu-id="16dfe-159">Используйте  **[Get AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)**  tooview политики защиты hello в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="16dfe-159">Use **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)** tooview hello protection policies in hello vault.</span></span> <span data-ttu-id="16dfe-160">Можно использовать этот командлет tooget определенной политике или tooview hello политики, связанные с типом рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="16dfe-160">You can use this cmdlet tooget a specific policy, or tooview hello policies associated with a workload type.</span></span> <span data-ttu-id="16dfe-161">Следующий пример Hello получает политики для типа рабочей нагрузки, AzureVM.</span><span class="sxs-lookup"><span data-stu-id="16dfe-161">hello following example gets policies for workload type, AzureVM.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesBackupProtectionPolicy -WorkloadType "AzureVM"
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
DefaultPolicy        AzureVM            AzureVM              4/14/2016 5:00:00 PM
```

> [!NOTE]
> <span data-ttu-id="16dfe-162">часовой пояс Hello поля BackupTime hello в PowerShell — в формате UTC.</span><span class="sxs-lookup"><span data-stu-id="16dfe-162">hello timezone of hello BackupTime field in PowerShell is UTC.</span></span> <span data-ttu-id="16dfe-163">Тем не менее если в hello портал Azure показано время резервного копирования hello, hello при скорректированное tooyour местном часовом поясе.</span><span class="sxs-lookup"><span data-stu-id="16dfe-163">However, when hello backup time is shown in hello Azure portal, hello time is adjusted tooyour local timezone.</span></span>
>
>

<span data-ttu-id="16dfe-164">Политика защиты архивации связана по крайней мере с одной политикой хранения.</span><span class="sxs-lookup"><span data-stu-id="16dfe-164">A backup protection policy is associated with at least one retention policy.</span></span> <span data-ttu-id="16dfe-165">Политика хранения определяет продолжительность хранения точки восстановления до ее удаления.</span><span class="sxs-lookup"><span data-stu-id="16dfe-165">Retention policy defines how long a recovery point is kept before it is deleted.</span></span> <span data-ttu-id="16dfe-166">Используйте  **[Get AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)**  политики хранения по умолчанию hello tooview.</span><span class="sxs-lookup"><span data-stu-id="16dfe-166">Use **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)** tooview hello default retention policy.</span></span>  <span data-ttu-id="16dfe-167">Аналогично можно использовать  **[Get AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)**  tooobtain hello по умолчанию расписание политики.</span><span class="sxs-lookup"><span data-stu-id="16dfe-167">Similarly you can use **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)** tooobtain hello default schedule policy.</span></span> <span data-ttu-id="16dfe-168">Hello  **[New AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  командлет создает объект PowerShell, который содержит сведения о политике резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="16dfe-168">hello **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="16dfe-169">Hello расписание и хранения объектов политики используются как входные данные toohello  **[New AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  командлета.</span><span class="sxs-lookup"><span data-stu-id="16dfe-169">hello schedule and retention policy objects are used as inputs toohello **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet.</span></span> <span data-ttu-id="16dfe-170">Hello следующий пример сохраняет расписание hello и политика хранения hello в переменных.</span><span class="sxs-lookup"><span data-stu-id="16dfe-170">hello following example stores hello schedule policy and hello retention policy in variables.</span></span> <span data-ttu-id="16dfe-171">пример Hello использует эти переменные toodefine hello параметры при создании политики защиты, *NewPolicy*.</span><span class="sxs-lookup"><span data-stu-id="16dfe-171">hello example uses those variables toodefine hello parameters when creating a protection policy, *NewPolicy*.</span></span>

```
PS C:\> $schPol = Get-AzureRmRecoveryServicesBackupSchedulePolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> New-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy" -WorkloadType "AzureVM" -RetentionPolicy $retPol -SchedulePolicy $schPol
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
NewPolicy           AzureVM            AzureVM              4/24/2016 1:30:00 AM
```


### <a name="enable-protection"></a><span data-ttu-id="16dfe-172">Включить защиту</span><span class="sxs-lookup"><span data-stu-id="16dfe-172">Enable protection</span></span>
<span data-ttu-id="16dfe-173">После определения политики резервного копирования защиты hello по-прежнему необходимо включить hello политики для элемента.</span><span class="sxs-lookup"><span data-stu-id="16dfe-173">Once you have defined hello backup protection policy, you still must enable hello policy for an item.</span></span> <span data-ttu-id="16dfe-174">Используйте  **[Enable AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)**  tooenable защиты.</span><span class="sxs-lookup"><span data-stu-id="16dfe-174">Use **[Enable-AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)** tooenable protection.</span></span> <span data-ttu-id="16dfe-175">Включение защиты требуется два объекта - элемент hello и политики hello.</span><span class="sxs-lookup"><span data-stu-id="16dfe-175">Enabling protection requires two objects - hello item and hello policy.</span></span> <span data-ttu-id="16dfe-176">После hello политики связан с хранилищем hello, во время hello, определенные в расписание политики hello активации рабочего процесса резервного копирования hello.</span><span class="sxs-lookup"><span data-stu-id="16dfe-176">Once hello policy has been associated with hello vault, hello backup workflow is triggered at hello time defined in hello policy schedule.</span></span>

<span data-ttu-id="16dfe-177">После защиты включает пример hello элемента, V2VM, с помощью политики hello NewPolicy Hello.</span><span class="sxs-lookup"><span data-stu-id="16dfe-177">hello following example enables protection for hello item, V2VM, using hello policy, NewPolicy.</span></span> <span data-ttu-id="16dfe-178">tooenable hello защиту для виртуальных машин диспетчера ресурсов без шифрования</span><span class="sxs-lookup"><span data-stu-id="16dfe-178">tooenable hello protection on non-encrypted Resource Manager VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="16dfe-179">tooenable hello защиты на шифрование виртуальных машин (шифрование с помощью BEK и KEK), необходимо toogive hello Azure Backup service разрешение tooread ключи и секретные данные из хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="16dfe-179">tooenable hello protection on encrypted VMs (encrypted using BEK and KEK), you need toogive hello Azure Backup service permission tooread keys and secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToKeys backup,get,list -PermissionsToSecrets get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="16dfe-180">tooenable hello защиты на шифрование виртуальных машин (шифрование только с помощью BEK), необходимо toogive hello Azure Backup service разрешение tooread секретов из хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="16dfe-180">tooenable hello protection on encrypted VMs (encrypted using BEK only), you need toogive hello Azure Backup service permission tooread secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToSecrets backup,get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

> [!NOTE]
> <span data-ttu-id="16dfe-181">При использовании облако Azure для государственных hello, затем использовать ff281ffe-705c-4f53-9f37-a40e6f2c68f3 hello значение для параметра hello **- ServicePrincipalName** в [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) командлета .</span><span class="sxs-lookup"><span data-stu-id="16dfe-181">If you are using hello Azure Government cloud, then use hello value ff281ffe-705c-4f53-9f37-a40e6f2c68f3 for hello parameter **-ServicePrincipalName** in [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet.</span></span>
>
>

<span data-ttu-id="16dfe-182">Классические виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="16dfe-182">For classic VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V1VM" -ServiceName "ServiceName1"
```

### <a name="modify-a-protection-policy"></a><span data-ttu-id="16dfe-183">Изменение политики защиты</span><span class="sxs-lookup"><span data-stu-id="16dfe-183">Modify a protection policy</span></span>
<span data-ttu-id="16dfe-184">Политика защиты hello toomodify, используйте [AzureRmRecoveryServicesBackupProtectionPolicy набор](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) hello toomodify SchedulePolicy или RetentionPolicy объектов.</span><span class="sxs-lookup"><span data-stu-id="16dfe-184">toomodify hello protection policy, use [Set-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) toomodify hello SchedulePolicy or RetentionPolicy objects.</span></span>

<span data-ttu-id="16dfe-185">Hello следующий пример изменяет количество дней too365 хранения точки восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="16dfe-185">hello following example changes hello recovery point retention too365 days.</span></span>

```
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol.DailySchedule.DurationCountInDays = 365
PS C:\> $pol= Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Set-AzureRmRecoveryServicesBackupProtectionPolicy -Policy $pol  -RetentionPolicy $RetPol
```

## <a name="trigger-a-backup"></a><span data-ttu-id="16dfe-186">Активация архивации</span><span class="sxs-lookup"><span data-stu-id="16dfe-186">Trigger a backup</span></span>
<span data-ttu-id="16dfe-187">Можно использовать  **[резервного копирования AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)**  tootrigger задания резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="16dfe-187">You can use **[Backup-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)** tootrigger a backup job.</span></span> <span data-ttu-id="16dfe-188">Если это hello начальной резервной копии, это полное резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="16dfe-188">If it is hello initial backup, it is a full backup.</span></span> <span data-ttu-id="16dfe-189">При последующем выполнении архивации резервная копия будет добавочной.</span><span class="sxs-lookup"><span data-stu-id="16dfe-189">Subsequent backups take an incremental copy.</span></span> <span data-ttu-id="16dfe-190">Быть убедиться, что toouse  **[набор AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  tooset контекст хранилища hello перед тем как запускать задание резервного копирования hello.</span><span class="sxs-lookup"><span data-stu-id="16dfe-190">Be sure toouse **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** tooset hello vault context before triggering hello backup job.</span></span> <span data-ttu-id="16dfe-191">Следующий пример Hello предполагается, что был задан контекст хранилища.</span><span class="sxs-lookup"><span data-stu-id="16dfe-191">hello following example assumes vault context was set.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer -ContainerType "AzureVM" -Status "Registered" -FriendlyName "V2VM"
PS C:\> $item = Get-AzureRmRecoveryServicesBackupItem -Container $namedContainer -WorkloadType "AzureVM"
PS C:\> $job = Backup-AzureRmRecoveryServicesBackupItem -Item $item
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM              Backup               InProgress            4/23/2016 5:00:30 PM                       cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

> [!NOTE]
> <span data-ttu-id="16dfe-192">часовой пояс Hello hello StartTime и EndTime полей в PowerShell — в формате UTC.</span><span class="sxs-lookup"><span data-stu-id="16dfe-192">hello timezone of hello StartTime and EndTime fields in PowerShell is UTC.</span></span> <span data-ttu-id="16dfe-193">Тем не менее если в hello портал Azure показано время hello, hello при скорректированное tooyour местном часовом поясе.</span><span class="sxs-lookup"><span data-stu-id="16dfe-193">However, when hello time is shown in hello Azure portal, hello time is adjusted tooyour local timezone.</span></span>
>
>

## <a name="monitoring-a-backup-job"></a><span data-ttu-id="16dfe-194">Наблюдение за выполнением задания резервного копирования</span><span class="sxs-lookup"><span data-stu-id="16dfe-194">Monitoring a backup job</span></span>
<span data-ttu-id="16dfe-195">Длительные операции, например задания резервного копирования можно отслеживать без использования hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="16dfe-195">You can monitor long-running operations, such as backup jobs, without using hello Azure portal.</span></span> <span data-ttu-id="16dfe-196">состояние hello tooget выполняющиеся задания, используйте hello  **[Get AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)**  командлета.</span><span class="sxs-lookup"><span data-stu-id="16dfe-196">tooget hello status of an in-progress job, use hello **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="16dfe-197">Этот командлет возвращает hello заданий резервного копирования для конкретного хранилища и хранилище, указан в контексте хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="16dfe-197">This cmdlet gets hello backup jobs for a specific vault, and that vault is specified in hello vault context.</span></span> <span data-ttu-id="16dfe-198">Hello следующий пример возвращает hello состояние выполняющегося задания как массив и сохраняет состояние hello в hello $joblist переменной.</span><span class="sxs-lookup"><span data-stu-id="16dfe-198">hello following example gets hello status of an in-progress job as an array, and stores hello status in hello $joblist variable.</span></span>

```
PS C:\> $joblist = Get-AzureRmRecoveryservicesBackupJob –Status "InProgress"
PS C:\> $joblist[0]
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM             Backup               InProgress            4/23/2016 5:00:30 PM           cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="16dfe-199">Вместо опроса эти задания для завершения — которая представляет требуется дополнительный код - использовать hello  **[ожидания AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  командлета.</span><span class="sxs-lookup"><span data-stu-id="16dfe-199">Instead of polling these jobs for completion - which is unnecessary additional code - use hello **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="16dfe-200">Этот командлет приостанавливает работу hello, до завершения задания hello или hello указано, что достигнуто значение тайм-аута.</span><span class="sxs-lookup"><span data-stu-id="16dfe-200">This cmdlet pauses hello execution until either hello job completes or hello specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $joblist[0] -Timeout 43200
```

## <a name="restore-an-azure-vm"></a><span data-ttu-id="16dfe-201">Восстановление виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="16dfe-201">Restore an Azure VM</span></span>
<span data-ttu-id="16dfe-202">Отсутствует ключевое различие между hello восстановление виртуальной Машины с помощью портала Azure hello и восстановление виртуальной Машины с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="16dfe-202">There is a key difference between hello restoring a VM using hello Azure portal and restoring a VM using PowerShell.</span></span> <span data-ttu-id="16dfe-203">С помощью PowerShell hello операция восстановления завершена, создав hello диски и сведения о конфигурации из точки восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="16dfe-203">With PowerShell, hello restore operation is complete once hello disks and configuration information from hello recovery point are created.</span></span>

> [!NOTE]
> <span data-ttu-id="16dfe-204">Операция восстановления Hello не создает виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="16dfe-204">hello restore operation does not create a virtual machine.</span></span>
>
>

<span data-ttu-id="16dfe-205">toocreate виртуальной машины с диска, см. раздел hello [hello Создание виртуальной Машины из хранимых дисков](backup-azure-vms-automation.md#create-a-vm-from-stored-disks).</span><span class="sxs-lookup"><span data-stu-id="16dfe-205">toocreate a virtual machine from disk, see hello section, [Create hello VM from stored disks](backup-azure-vms-automation.md#create-a-vm-from-stored-disks).</span></span> <span data-ttu-id="16dfe-206">приведены основные шаги Hello toorestore ВМ Azure.</span><span class="sxs-lookup"><span data-stu-id="16dfe-206">hello basic steps toorestore an Azure VM are:</span></span>

* <span data-ttu-id="16dfe-207">Выберите hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="16dfe-207">Select hello VM</span></span>
* <span data-ttu-id="16dfe-208">Выбор точки восстановления</span><span class="sxs-lookup"><span data-stu-id="16dfe-208">Choose a recovery point</span></span>
* <span data-ttu-id="16dfe-209">Восстановление дисков hello</span><span class="sxs-lookup"><span data-stu-id="16dfe-209">Restore hello disks</span></span>
* <span data-ttu-id="16dfe-210">Создание виртуальной Машины hello из хранимых дисков</span><span class="sxs-lookup"><span data-stu-id="16dfe-210">Create hello VM from stored disks</span></span>

<span data-ttu-id="16dfe-211">Hello на рисунке показана иерархия hello объекта из hello RecoveryServicesVault вниз toohello BackupRecoveryPoint.</span><span class="sxs-lookup"><span data-stu-id="16dfe-211">hello following graphic shows hello object hierarchy from hello RecoveryServicesVault down toohello BackupRecoveryPoint.</span></span>

![Иерархия объектов служб восстановления с BackupContainer](./media/backup-azure-vms-arm-automation/backuprecoverypoint-only.png)

<span data-ttu-id="16dfe-213">toorestore резервных копий данных, определите hello резервную копию элемента и точки восстановления hello, содержащий данные на момент hello.</span><span class="sxs-lookup"><span data-stu-id="16dfe-213">toorestore backup data, identify hello backed-up item and hello recovery point that holds hello point-in-time data.</span></span> <span data-ttu-id="16dfe-214">Используйте hello  **[восстановления AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  toohello пользовательской учетной записи в хранилище данных toorestore командлета из hello.</span><span class="sxs-lookup"><span data-stu-id="16dfe-214">Use hello **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet toorestore data from hello vault toohello customer's account.</span></span>

### <a name="select-hello-vm"></a><span data-ttu-id="16dfe-215">Выберите hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="16dfe-215">Select hello VM</span></span>
<span data-ttu-id="16dfe-216">tooget hello PowerShell объект, определяющий hello справа резервное копирование элемента, запустите из контейнера hello в хранилище hello и постепенно вниз по иерархии объектов hello.</span><span class="sxs-lookup"><span data-stu-id="16dfe-216">tooget hello PowerShell object that identifies hello right backup item, start from hello container in hello vault, and work your way down hello object hierarchy.</span></span> <span data-ttu-id="16dfe-217">tooselect hello контейнера, представляющий hello виртуальной Машины, используйте hello  **[Get AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)**  командлета и передать этот toohello  **[ Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)**  командлета.</span><span class="sxs-lookup"><span data-stu-id="16dfe-217">tooselect hello container that represents hello VM, use hello **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)** cmdlet and pipe that toohello **[Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)** cmdlet.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer  -ContainerType "AzureVM" –Status "Registered" -FriendlyName "V2VM"
PS C:\> $backupitem = Get-AzureRmRecoveryServicesBackupItem –Container $namedContainer  –WorkloadType "AzureVM"
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="16dfe-218">Выбор точки восстановления</span><span class="sxs-lookup"><span data-stu-id="16dfe-218">Choose a recovery point</span></span>
<span data-ttu-id="16dfe-219">Используйте hello  **[Get AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)**  toolist командлет се точки восстановления для архивации элемента hello.</span><span class="sxs-lookup"><span data-stu-id="16dfe-219">Use hello **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)** cmdlet toolist all recovery points for hello backup item.</span></span> <span data-ttu-id="16dfe-220">Выберите toorestore точки восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="16dfe-220">Then choose hello recovery point toorestore.</span></span> <span data-ttu-id="16dfe-221">Если вы не уверены, какие toouse точки восстановления, это toochoose хорошей практикой hello последней RecoveryPointType = AppConsistent пункт в списке hello.</span><span class="sxs-lookup"><span data-stu-id="16dfe-221">If you are unsure which recovery point toouse, it is a good practice toochoose hello most recent RecoveryPointType = AppConsistent point in hello list.</span></span>

<span data-ttu-id="16dfe-222">В следующий скрипт hello, hello переменной, **$rp**, представляет собой массив из точки восстановления для hello выбранных резервное копирование элемента из hello за последние семь дней.</span><span class="sxs-lookup"><span data-stu-id="16dfe-222">In hello following script, hello variable, **$rp**, is an array of recovery points for hello selected backup item, from hello past seven days.</span></span> <span data-ttu-id="16dfe-223">время с последней точки восстановления hello с индексом 0 Hello массива сортируются в обратном порядке.</span><span class="sxs-lookup"><span data-stu-id="16dfe-223">hello array is sorted in reverse order of time with hello latest recovery point at index 0.</span></span> <span data-ttu-id="16dfe-224">Используйте обычный массив PowerShell индексирования точки восстановления toopick hello.</span><span class="sxs-lookup"><span data-stu-id="16dfe-224">Use standard PowerShell array indexing toopick hello recovery point.</span></span> <span data-ttu-id="16dfe-225">В примере hello $rp [0] выбирает hello последней точки восстановления.</span><span class="sxs-lookup"><span data-stu-id="16dfe-225">In hello example, $rp[0] selects hello latest recovery point.</span></span>

```
PS C:\> $startDate = (Get-Date).AddDays(-7)
PS C:\> $endDate = Get-Date
PS C:\> $rp = Get-AzureRmRecoveryServicesBackupRecoveryPoint -Item $backupitem -StartDate $startdate.ToUniversalTime() -EndDate $enddate.ToUniversalTime()
PS C:\> $rp[0]
RecoveryPointAdditionalInfo :
SourceVMStorageType         : NormalStorage
Name                        : 15260861925810
ItemName                    : VM;iaasvmcontainer;RGName1;V2VM
RecoveryPointId             : /subscriptions/XX/resourceGroups/ RGName1/providers/Microsoft.RecoveryServices/vaults/testvault/backupFabrics/Azure/protectionContainers/IaasVMContainer;iaasvmcontainer;RGName1;V2VM/protectedItems/VM;iaasvmcontainer; RGName1;V2VM/recoveryPoints/15260861925810
RecoveryPointType           : AppConsistent
RecoveryPointTime           : 4/23/2016 5:02:04 PM
WorkloadType                : AzureVM
ContainerName               : IaasVMContainer;iaasvmcontainer; RGName1;V2VM
ContainerType               : AzureVM
BackupManagementType        : AzureVM
```



### <a name="restore-hello-disks"></a><span data-ttu-id="16dfe-226">Восстановление дисков hello</span><span class="sxs-lookup"><span data-stu-id="16dfe-226">Restore hello disks</span></span>
<span data-ttu-id="16dfe-227">Используйте hello  **[восстановления AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  toorestore командлет элемент резервного копирования данных и конфигурации tooa точек восстановления.</span><span class="sxs-lookup"><span data-stu-id="16dfe-227">Use hello **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet toorestore a backup item's data and configuration tooa recovery point.</span></span> <span data-ttu-id="16dfe-228">После идентификации точки восстановления используется в качестве hello значения для hello **- RecoveryPoint** параметра.</span><span class="sxs-lookup"><span data-stu-id="16dfe-228">Once you have identified a recovery point, use it as hello value for hello **-RecoveryPoint** parameter.</span></span> <span data-ttu-id="16dfe-229">В предыдущем примере кода hello **$rp [0]** было toouse точки восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="16dfe-229">In hello previous sample code, **$rp[0]** was hello recovery point toouse.</span></span> <span data-ttu-id="16dfe-230">В следующий пример кода hello **$rp [0]** — hello toouse точки восстановления для восстановления диска hello.</span><span class="sxs-lookup"><span data-stu-id="16dfe-230">In hello following sample code, **$rp[0]** is hello recovery point toouse for restoring hello disk.</span></span>

<span data-ttu-id="16dfe-231">toorestore hello диски и сведения о конфигурации:</span><span class="sxs-lookup"><span data-stu-id="16dfe-231">toorestore hello disks and configuration information:</span></span>

```
PS C:\> $restorejob = Restore-AzureRmRecoveryServicesBackupItem -RecoveryPoint $rp[0] -StorageAccountName "DestAccount" -StorageAccountResourceGroupName "DestRG"
PS C:\> $restorejob
WorkloadName     Operation          Status               StartTime                 EndTime            JobID
------------     ---------          ------               ---------                 -------          ----------
V2VM              Restore           InProgress           4/23/2016 5:00:30 PM                        cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="16dfe-232">Используйте hello  **[ожидания AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  toowait командлет для задания toocomplete hello восстановления.</span><span class="sxs-lookup"><span data-stu-id="16dfe-232">Use hello **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet toowait for hello Restore job toocomplete.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $restorejob -Timeout 43200
```

<span data-ttu-id="16dfe-233">После завершения задания восстановления hello использовать hello  **[Get AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)**  командлет tooget hello и подробные сведения о hello операции восстановления.</span><span class="sxs-lookup"><span data-stu-id="16dfe-233">Once hello Restore job has completed, use hello **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)** cmdlet tooget hello details of hello restore operation.</span></span> <span data-ttu-id="16dfe-234">Hello JobDetails свойство имеет hello toorebuild необходимые сведения hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="16dfe-234">hello JobDetails property has hello information needed toorebuild hello VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmRecoveryServicesBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmRecoveryServicesBackupJobDetails -Job $restorejob
```

<span data-ttu-id="16dfe-235">После восстановления дисков hello перехода toohello Далее раздел toocreate hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="16dfe-235">Once you restore hello disks, go toohello next section toocreate hello VM.</span></span>

## <a name="create-a-vm-from-restored-disks"></a><span data-ttu-id="16dfe-236">Создание виртуальной машины с восстановленного диска</span><span class="sxs-lookup"><span data-stu-id="16dfe-236">Create a VM from restored disks</span></span>
<span data-ttu-id="16dfe-237">После восстановления дисков hello, выполните эти шаги toocreate и настроить hello виртуальную машину с диска.</span><span class="sxs-lookup"><span data-stu-id="16dfe-237">After you have restored hello disks, use these steps toocreate and configure hello virtual machine from disk.</span></span>

> [!NOTE]
> <span data-ttu-id="16dfe-238">toocreate шифрования виртуальные машины с восстановленные диски, роли Azure должен иметь действие hello tooperform разрешения, **Microsoft.KeyVault/vaults/deploy/action**.</span><span class="sxs-lookup"><span data-stu-id="16dfe-238">toocreate encrypted VMs from restored disks, your Azure role must have permission tooperform hello action, **Microsoft.KeyVault/vaults/deploy/action**.</span></span> <span data-ttu-id="16dfe-239">Если у роли нет этого разрешения, создайте пользовательскую роль с этим действием.</span><span class="sxs-lookup"><span data-stu-id="16dfe-239">If your role does not have this permission, create a custom role with this action.</span></span> <span data-ttu-id="16dfe-240">Дополнительные сведения см. в разделе [Пользовательские роли в Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="16dfe-240">For more information, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>
>
>

1. <span data-ttu-id="16dfe-241">Запрос hello восстановить свойства диска для сведений о задании hello.</span><span class="sxs-lookup"><span data-stu-id="16dfe-241">Query hello restored disk properties for hello job details.</span></span>

  ```
  PS C:\> $properties = $details.properties
  PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
  PS C:\> $containerName = $properties["Config Blob Container Name"]
  PS C:\> $blobName = $properties["Config Blob Name"]
  ```

2. <span data-ttu-id="16dfe-242">Задать контекст хранилища Azure hello и восстановите файл конфигурации JSON hello.</span><span class="sxs-lookup"><span data-stu-id="16dfe-242">Set hello Azure storage context and restore hello JSON configuration file.</span></span>

    ```
    PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName "testvault"
    PS C:\> $destination_path = "C:\vmconfig.json"
    PS C:\> Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path
    PS C:\> $obj = ((Get-Content -Path $destination_path -Raw -Encoding Unicode)).TrimEnd([char]0x00) | ConvertFrom-Json
    ```

3. <span data-ttu-id="16dfe-243">Используйте hello файл конфигурации JSON toocreate конфигурацию виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="16dfe-243">Use hello JSON configuration file toocreate hello VM configuration.</span></span>

    ```
   PS C:\> $vm = New-AzureRmVMConfig -VMSize $obj.'properties.hardwareProfile'.vmSize -VMName "testrestore"
    ```

4. <span data-ttu-id="16dfe-244">Присоедините диск hello ОС и дисков данных.</span><span class="sxs-lookup"><span data-stu-id="16dfe-244">Attach hello OS disk and data disks.</span></span> <span data-ttu-id="16dfe-245">В зависимости от конфигурации hello виртуальных машин щелкните hello соответствующую ссылку tooview соответствующих командлетов:</span><span class="sxs-lookup"><span data-stu-id="16dfe-245">Depending on hello configuration of your VMs, click on hello relevant link tooview respective cmdlets:</span></span> 
    - [<span data-ttu-id="16dfe-246">Неуправляемые, без шифрования виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="16dfe-246">Non-managed, non-encrypted VMs</span></span>](#non-managed-non-encrypted-vms)
    - [<span data-ttu-id="16dfe-247">Неуправляемые, зашифрованный виртуальных машин (BEK)</span><span class="sxs-lookup"><span data-stu-id="16dfe-247">Non-managed, encrypted VMs (BEK only)</span></span>](#non-managed-encrypted-vms-bek-only)
    - [<span data-ttu-id="16dfe-248">Виртуальные машины неуправляемые, зашифрованный (BEK и Ключами)</span><span class="sxs-lookup"><span data-stu-id="16dfe-248">Non-managed, encrypted VMs (BEK and KEK)</span></span>](#non-managed-encrypted-vms-bek-and-kek)
    - [<span data-ttu-id="16dfe-249">Управляемые без шифрования виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="16dfe-249">Managed, non-encrypted VMs</span></span>](#managed-non-encrypted-vms)
    - [<span data-ttu-id="16dfe-250">Виртуальные машины управляемых, зашифрованный (BEK и Ключами)</span><span class="sxs-lookup"><span data-stu-id="16dfe-250">Managed, encrypted VMs (BEK and KEK)</span></span>](#managed-encrypted-vms-bek-and-kek)
    
    #### <a name="non-managed-non-encrypted-vms"></a><span data-ttu-id="16dfe-251">Неуправляемые незашифрованные виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="16dfe-251">Non-managed, non-encrypted VMs</span></span>

    <span data-ttu-id="16dfe-252">Используйте следующий пример для виртуальных машин под управлением, незашифрованные hello.</span><span class="sxs-lookup"><span data-stu-id="16dfe-252">Use hello following sample for non-managed, non-encrypted VMs.</span></span>

    ```
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.StorageProfile'.osDisk.vhd.Uri -CreateOption "Attach"
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.StorageProfile'.OsDisk.OsType
    PS C:\> foreach($dd in $obj.'properties.StorageProfile'.DataDisks)
    {
    $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="non-managed-encrypted-vms-bek-only"></a><span data-ttu-id="16dfe-253">Неуправляемые зашифрованные виртуальные машины (только BEK)</span><span class="sxs-lookup"><span data-stu-id="16dfe-253">Non-managed, encrypted VMs (BEK only)</span></span>

    <span data-ttu-id="16dfe-254">Для неуправляемых, зашифрованный ВМ (шифрование только с помощью BEK) необходимо toorestore hello toohello секретного ключа хранилища для присоединения дисков.</span><span class="sxs-lookup"><span data-stu-id="16dfe-254">For non-managed, encrypted VMs (encrypted using BEK only), you need toorestore hello secret toohello key vault before you can attach disks.</span></span> <span data-ttu-id="16dfe-255">Дополнительные сведения см. в разделе статьи hello [восстановление зашифрованных виртуальной машине из точки восстановления в Azure Backup](backup-azure-restore-key-secret.md).</span><span class="sxs-lookup"><span data-stu-id="16dfe-255">For more information, please see hello article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="16dfe-256">Следующий образец Hello показан способ tooattach ОС и дисков данных для шифрования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="16dfe-256">hello following sample shows how tooattach OS and data disks for encrypted VMs.</span></span>

    ```
    PS C:\> $dekUrl = "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007/xx000000xx0849999f3xx30000003163"
    PS C:\> $keyVaultId = "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.storageProfile'.osDisk.vhd.uri -DiskEncryptionKeyUrl $dekUrl -DiskEncryptionKeyVaultId $keyVaultId -CreateOption "Attach" -Windows
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.storageProfile'.osDisk.osType
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
     }
    ```

    #### <a name="non-managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="16dfe-257">Неуправляемые зашифрованные виртуальные машины (BEK и KEK)</span><span class="sxs-lookup"><span data-stu-id="16dfe-257">Non-managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="16dfe-258">Для неуправляемых, зашифрованный ВМ (шифрование с помощью BEK и Ключами) требуется ключ toorestore hello и toohello секрета хранилища ключей для присоединения дисков.</span><span class="sxs-lookup"><span data-stu-id="16dfe-258">For non-managed, encrypted VMs (encrypted using BEK and KEK), you need toorestore hello key and secret toohello key vault before you can attach disks.</span></span> <span data-ttu-id="16dfe-259">Дополнительные сведения см. в разделе статьи hello [восстановление зашифрованных виртуальной машине из точки восстановления в Azure Backup](backup-azure-restore-key-secret.md).</span><span class="sxs-lookup"><span data-stu-id="16dfe-259">For more information, please see hello article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="16dfe-260">Следующий образец Hello показан способ tooattach ОС и дисков данных для шифрования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="16dfe-260">hello following sample shows how tooattach OS and data disks for encrypted VMs.</span></span>

    ```
    PS C:\> $dekUrl = "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007/xx000000xx0849999f3xx30000003163"
    PS C:\> $kekUrl = "https://ContosoKeyVault.vault.azure.net:443/keys/ContosoKey007/x9xxx00000x0000x9b9949999xx0x006"
    PS C:\> $keyVaultId = "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.storageProfile'.osDisk.vhd.uri -DiskEncryptionKeyUrl $dekUrl -DiskEncryptionKeyVaultId $keyVaultId -KeyEncryptionKeyUrl $kekUrl -KeyEncryptionKeyVaultId $keyVaultId -CreateOption "Attach" -Windows
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.storageProfile'.osDisk.osType
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
     }
    ```

    #### <a name="managed-non-encrypted-vms"></a><span data-ttu-id="16dfe-261">Управляемые незашифрованные виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="16dfe-261">Managed, non-encrypted VMs</span></span>

    <span data-ttu-id="16dfe-262">Для управляемых незашифрованные виртуальных машин будет необходимо управлять toocreate диска из хранилища больших двоичных объектов, а затем подключите диски hello.</span><span class="sxs-lookup"><span data-stu-id="16dfe-262">For managed non-encrypted VMs, you'll need toocreate managed disks from blob storage, and then attach hello disks.</span></span> <span data-ttu-id="16dfe-263">Подробные сведения см. в статье hello, [присоединения tooa диска данных виртуальной Машины Windows с помощью PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="16dfe-263">For in-depth information, see hello article, [Attach a data disk tooa Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="16dfe-264">Привет, следующий пример кода показывает, как tooattach hello диски данных для управляемых виртуальных машин без шифрования.</span><span class="sxs-lookup"><span data-stu-id="16dfe-264">hello following sample code shows how tooattach hello data disks for managed non-encrypted VMs.</span></span>

    ```
    PS C:\> $storageType = "StandardLRS"
    PS C:\> $osDiskName = $vm.Name + "_osdisk"
    PS C:\> $osVhdUri = $obj.'properties.storageProfile'.osDisk.vhd.uri
    PS C:\> $diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $osVhdUri
    PS C:\> $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk $diskConfig -ResourceGroupName "test"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -CreateOption "Attach" -Windows
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $dataDiskName = $vm.Name + $dd.name ;
     $dataVhdUri = $dd.vhd.uri ;
     $dataDiskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $dataVhdUri ;
     $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $dataDiskConfig -ResourceGroupName "test" ;
     Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -ManagedDiskId $dataDisk2.Id -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="16dfe-265">Управляемые зашифрованные виртуальные машины (BEK и KEK)</span><span class="sxs-lookup"><span data-stu-id="16dfe-265">Managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="16dfe-266">Для управляемых зашифрованные виртуальных машин (шифрование с помощью BEK и Ключами) будет требуется toocreate управляемых дисков из хранилища больших двоичных объектов, а затем подключите диски hello.</span><span class="sxs-lookup"><span data-stu-id="16dfe-266">For managed encrypted VMs (encrypted using BEK and KEK), you'll need toocreate managed disks from blob storage, and then attach hello disks.</span></span> <span data-ttu-id="16dfe-267">Подробные сведения см. в статье hello, [присоединения tooa диска данных виртуальной Машины Windows с помощью PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="16dfe-267">For in-depth information, see hello article, [Attach a data disk tooa Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="16dfe-268">Hello следующем образце кода показано, как tooattach hello диски с данными для виртуальных машин, управляемых зашифрованные.</span><span class="sxs-lookup"><span data-stu-id="16dfe-268">hello following sample code shows how tooattach hello data disks for managed encrypted VMs.</span></span>

     ```
    PS C:\> $dekUrl = "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007/xx000000xx0849999f3xx30000003163"
    PS C:\> $kekUrl = "https://ContosoKeyVault.vault.azure.net:443/keys/ContosoKey007/x9xxx00000x0000x9b9949999xx0x006"
    PS C:\> $keyVaultId = "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault"
    PS C:\> $storageType = "StandardLRS"
    PS C:\> $osDiskName = $vm.Name + "_osdisk"
    PS C:\> $osVhdUri = $obj.'properties.storageProfile'.osDisk.vhd.uri
    PS C:\> $diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $osVhdUri
    PS C:\> $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk $diskConfig -ResourceGroupName "test"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -DiskEncryptionKeyUrl $dekUrl -DiskEncryptionKeyVaultId $keyVaultId -KeyEncryptionKeyUrl $kekUrl -KeyEncryptionKeyVaultId $keyVaultId -CreateOption "Attach" -Windows
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $dataDiskName = $vm.Name + $dd.name ;
     $dataVhdUri = $dd.vhd.uri ;
     $dataDiskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $dataVhdUri ;
     $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $dataDiskConfig -ResourceGroupName "test" ;
     Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -ManagedDiskId $dataDisk2.Id -Lun $dd.Lun -CreateOption "Attach"
     }
    ```

5. <span data-ttu-id="16dfe-269">Чтобы задайте параметры сети hello.</span><span class="sxs-lookup"><span data-stu-id="16dfe-269">Set hello Network settings.</span></span>

    ```
    PS C:\> $nicName="p1234"
    PS C:\> $pip = New-AzureRmPublicIpAddress -Name $nicName -ResourceGroupName "test" -Location "WestUS" -AllocationMethod Dynamic
    PS C:\> $vnet = Get-AzureRmVirtualNetwork -Name "testvNET" -ResourceGroupName "test"
    PS C:\> $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName "test" -Location "WestUS" -SubnetId $vnet.Subnets[$subnetindex].Id -PublicIpAddressId $pip.Id
    PS C:\> $vm=Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    ```
6. <span data-ttu-id="16dfe-270">Создайте виртуальную машину hello.</span><span class="sxs-lookup"><span data-stu-id="16dfe-270">Create hello virtual machine.</span></span>

    ```    
    PS C:\> New-AzureRmVM -ResourceGroupName "test" -Location "WestUS" -VM $vm
    ```

## <a name="next-steps"></a><span data-ttu-id="16dfe-271">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="16dfe-271">Next steps</span></span>
<span data-ttu-id="16dfe-272">Если вы предпочитаете toouse PowerShell tooengage с ресурсами Azure, см статью PowerShell hello, [развертывание и управление резервного копирования для Windows Server](backup-client-automation.md).</span><span class="sxs-lookup"><span data-stu-id="16dfe-272">If you prefer toouse PowerShell tooengage with your Azure resources, see hello PowerShell article, [Deploy and Manage Backup for Windows Server](backup-client-automation.md).</span></span> <span data-ttu-id="16dfe-273">Если вы управляете операции резервного копирования DPM, см. в статье hello [развертывание и управление резервным копированием для DPM](backup-dpm-automation.md).</span><span class="sxs-lookup"><span data-stu-id="16dfe-273">If you manage DPM backups, see hello article, [Deploy and Manage Backup for DPM](backup-dpm-automation.md).</span></span> <span data-ttu-id="16dfe-274">Обе эти статьи имеют две версии — для развертывания с помощью Resource Manager и для классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="16dfe-274">Both of these articles have a version for Resource Manager deployments and Classic deployments.</span></span>  
