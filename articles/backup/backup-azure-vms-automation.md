---
title: "Развертывание резервных копий виртуальных машин, развернутых с использованием Resource Manager, и управление ими с помощью PowerShell | Документация Майкрософт"
description: "Использование PowerShell для развертывания архивации виртуальных машин, развернутых посредством Resource Manager, и управления ею"
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
ms.openlocfilehash: 861346a50df6641abb9e454644228146e14b4078
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="use-azurermrecoveryservicesbackup-cmdlets-to-back-up-virtual-machines"></a><span data-ttu-id="74d85-103">Архивация виртуальных машин с помощью командлетов AzureRM.RecoveryServices.Backup</span><span class="sxs-lookup"><span data-stu-id="74d85-103">Use AzureRM.RecoveryServices.Backup cmdlets to back up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="74d85-104">Диспетчер ресурсов</span><span class="sxs-lookup"><span data-stu-id="74d85-104">Resource Manager</span></span>](backup-azure-vms-automation.md)
> * [<span data-ttu-id="74d85-105">Классический</span><span class="sxs-lookup"><span data-stu-id="74d85-105">Classic</span></span>](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="74d85-106">В этой статье показано, как выполнять архивацию и восстановление виртуальной машины Azure из хранилища служб восстановления с помощью командлетов Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="74d85-106">This article shows you how to use Azure PowerShell cmdlets to back up and recover an Azure virtual machine (VM) from a Recovery Services vault.</span></span> <span data-ttu-id="74d85-107">Хранилище служб восстановления — это ресурс Azure Resource Manager, используемый для защиты данных и ресурсов-контейнеров в службе архивации Azure и службах Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="74d85-107">A Recovery Services vault is an Azure Resource Manager resource and is used to protect data and assets in both Azure Backup and Azure Site Recovery services.</span></span> <span data-ttu-id="74d85-108">Это хранилище позволяет защитить виртуальные машины, развернутые с помощью Azure Service Manager и Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="74d85-108">You can use a Recovery Services vault to protect Azure Service Manager-deployed VMs, and Azure Resource Manager-deployed VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="74d85-109">В Azure предусмотрены две модели развертывания, позволяющие создавать ресурсы и работать с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="74d85-109">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="74d85-110">В этой статье рассматривается использование виртуальных машин, созданных с помощью модели Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="74d85-110">This article is for use with VMs created using the Resource Manager model.</span></span>
>
>

<span data-ttu-id="74d85-111">В этой статье описано, как использовать PowerShell для защиты виртуальной машины и восстановления данных из точки восстановления.</span><span class="sxs-lookup"><span data-stu-id="74d85-111">This article walks you through using PowerShell to protect a VM, and restore data from a recovery point.</span></span>

## <a name="concepts"></a><span data-ttu-id="74d85-112">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="74d85-112">Concepts</span></span>
<span data-ttu-id="74d85-113">Если вы не знакомы со службой архивации Azure, общие сведения о службе см. в статье [Что такое служба архивации Azure?](backup-introduction-to-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="74d85-113">If you are not familiar with the Azure Backup service, for an overview of the service, check out [What is Azure Backup?](backup-introduction-to-azure-backup.md)</span></span> <span data-ttu-id="74d85-114">Перед началом работы убедитесь, что вам известны предварительные требования для работы со службой архивации Azure и ограничения, применяемые к текущему решению для архивации виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="74d85-114">Before you start, ensure that you cover the essentials about the prerequisites needed to work with Azure Backup, and the limitations of the current VM backup solution.</span></span>

<span data-ttu-id="74d85-115">Чтобы эффективно использовать PowerShell, необходимо понимать иерархию объектов и знать, с чего следует начать.</span><span class="sxs-lookup"><span data-stu-id="74d85-115">To use PowerShell effectively, it is necessary to understand the hierarchy of objects and from where to start.</span></span>

![Иерархия объектов служб восстановления](./media/backup-azure-vms-arm-automation/recovery-services-object-hierarchy.png)

<span data-ttu-id="74d85-117">Справку по командлету PowerShell AzureRm.RecoveryServices.Backup см. в статье [Azure Backup — Recovery Services Cmdlets](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) (Командлеты служб архивации и восстановления Azure) в библиотеке Azure.</span><span class="sxs-lookup"><span data-stu-id="74d85-117">To view the AzureRm.RecoveryServices.Backup PowerShell cmdlet reference, see the [Azure Backup - Recovery Services Cmdlets](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) in the Azure library.</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="74d85-118">Настройка и регистрация</span><span class="sxs-lookup"><span data-stu-id="74d85-118">Setup and Registration</span></span>
<span data-ttu-id="74d85-119">Чтобы начать работу, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="74d85-119">To begin:</span></span>

1. <span data-ttu-id="74d85-120">[Скачайте последнюю версию PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (минимальная требуемая версия — 1.4.0).</span><span class="sxs-lookup"><span data-stu-id="74d85-120">[Download the latest version of PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (the minimum version required is: 1.4.0)</span></span>
2. <span data-ttu-id="74d85-121">Чтобы получить список доступных командлетов PowerShell для службы архивации Azure, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="74d85-121">Find the Azure Backup PowerShell cmdlets available by typing the following command:</span></span>

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


<span data-ttu-id="74d85-122">С помощью PowerShell можно автоматизировать следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="74d85-122">The following tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="74d85-123">Создание хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="74d85-123">Create a Recovery Services vault</span></span>
* <span data-ttu-id="74d85-124">Резервное копирование виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="74d85-124">Back up Azure VMs</span></span>
* <span data-ttu-id="74d85-125">активация задания архивации;</span><span class="sxs-lookup"><span data-stu-id="74d85-125">Trigger a backup job</span></span>
* <span data-ttu-id="74d85-126">наблюдение за выполнением задания архивации;</span><span class="sxs-lookup"><span data-stu-id="74d85-126">Monitor a backup job</span></span>
* <span data-ttu-id="74d85-127">Восстановление виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="74d85-127">Restore an Azure VM</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="74d85-128">Создание хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="74d85-128">Create a recovery services vault</span></span>
<span data-ttu-id="74d85-129">Чтобы создать хранилище служб восстановления, выполните описанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="74d85-129">The following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="74d85-130">Хранилище служб восстановления отличается от хранилища службы архивации.</span><span class="sxs-lookup"><span data-stu-id="74d85-130">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="74d85-131">Если вы используете службу архивации Azure впервые, выполните командлет **[Register-AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)**, чтобы зарегистрировать поставщик служб восстановления Azure в своей подписке.</span><span class="sxs-lookup"><span data-stu-id="74d85-131">If you are using Azure Backup for the first time, you must use the **[Register-AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)** cmdlet to register the Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="74d85-132">Хранилище служб восстановления представляет собой ресурс Resource Manager, поэтому вам потребуется разместить его в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="74d85-132">The Recovery Services vault is a Resource Manager resource, so you need to place it within a resource group.</span></span> <span data-ttu-id="74d85-133">Вы можете использовать имеющуюся группу ресурсов или создать новую, выполнив командлет **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)**.</span><span class="sxs-lookup"><span data-stu-id="74d85-133">You can use an existing resource group, or create a resource group with the **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)** cmdlet.</span></span> <span data-ttu-id="74d85-134">При создании группы ресурсов укажите ее имя и расположение.</span><span class="sxs-lookup"><span data-stu-id="74d85-134">When creating a resource group, specify the name and location for the resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="74d85-135">Воспользуйтесь командлетом **[New-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)**, чтобы создать хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="74d85-135">Use the **[New-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)** cmdlet to create the Recovery Services vault.</span></span> <span data-ttu-id="74d85-136">Разместите хранилище там же, где находится группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="74d85-136">Be sure to specify the same location for the vault as was used for the resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="74d85-137">Укажите необходимый тип избыточности хранилища: [локально избыточное (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) или [геоизбыточное (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="74d85-137">Specify the type of storage redundancy to use; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="74d85-138">В следующем примере показано, что для параметра BackupStorageRedundancy для testvault задано значение GeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="74d85-138">The following example shows the -BackupStorageRedundancy option for testvault is set to GeoRedundant.</span></span>

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testvault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -Vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

   > [!TIP]
   > <span data-ttu-id="74d85-139">Для многих командлетов службы архивации Azure требуется объект хранилища служб восстановления в качестве входных данных.</span><span class="sxs-lookup"><span data-stu-id="74d85-139">Many Azure Backup cmdlets require the Recovery Services vault object as an input.</span></span> <span data-ttu-id="74d85-140">По этой причине объект хранилища служб восстановления резервных копий удобно хранить в переменной.</span><span class="sxs-lookup"><span data-stu-id="74d85-140">For this reason, it is convenient to store the Backup Recovery Services vault object in a variable.</span></span>
   >
   >

## <a name="view-the-vaults-in-a-subscription"></a><span data-ttu-id="74d85-141">Просмотр хранилищ в подписке</span><span class="sxs-lookup"><span data-stu-id="74d85-141">View the vaults in a subscription</span></span>
<span data-ttu-id="74d85-142">Чтобы получить список всех хранилищ в текущей подписке, используйте командлет **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)**.</span><span class="sxs-lookup"><span data-stu-id="74d85-142">Use **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)** to view the list of all vaults in the current subscription.</span></span> <span data-ttu-id="74d85-143">Он позволяет убедиться в том, что хранилище создано, и увидеть, какие хранилища доступны в подписке.</span><span class="sxs-lookup"><span data-stu-id="74d85-143">You can use this command to check that a new vault was created, or to see the available vaults in the subscription.</span></span>

<span data-ttu-id="74d85-144">Выполнив команду Get-AzureRmRecoveryServicesVault, вы получите список всех хранилищ в подписке.</span><span class="sxs-lookup"><span data-stu-id="74d85-144">Run the command, Get-AzureRmRecoveryServicesVault, to view all vaults in the subscription.</span></span> <span data-ttu-id="74d85-145">В следующем примере показаны сведения по каждому хранилищу.</span><span class="sxs-lookup"><span data-stu-id="74d85-145">The following example shows the information displayed for each vault.</span></span>

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


## <a name="back-up-azure-vms"></a><span data-ttu-id="74d85-146">Резервное копирование виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="74d85-146">Back up Azure VMs</span></span>
<span data-ttu-id="74d85-147">Используйте хранилище служб восстановления для защиты виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="74d85-147">Use a Recovery Services vault to protect your virtual machines.</span></span> <span data-ttu-id="74d85-148">Прежде чем применить защиту, задайте контекст хранилища (тип данных, защиту которых обеспечивает хранилище) и проверьте политику защиты.</span><span class="sxs-lookup"><span data-stu-id="74d85-148">Before you apply the protection, set the vault context (the type of data protected in the vault), and verify the protection policy.</span></span> <span data-ttu-id="74d85-149">Политика защиты — это график выполнения заданий резервного копирования и срок хранения каждого моментального снимка резервной копии.</span><span class="sxs-lookup"><span data-stu-id="74d85-149">The protection policy is the schedule when the backup jobs run, and how long each backup snapshot is retained.</span></span>

### <a name="set-vault-context"></a><span data-ttu-id="74d85-150">Задание контекста хранилища</span><span class="sxs-lookup"><span data-stu-id="74d85-150">Set vault context</span></span>
<span data-ttu-id="74d85-151">Перед включением защиты на виртуальной машине выполните командлет **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**, чтобы задать контекст хранилища.</span><span class="sxs-lookup"><span data-stu-id="74d85-151">Before enabling protection on a VM, use **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** to set the vault context.</span></span> <span data-ttu-id="74d85-152">Заданный контекст хранилища применяется ко всем последующим командлетам.</span><span class="sxs-lookup"><span data-stu-id="74d85-152">Once the vault context is set, it applies to all subsequent cmdlets.</span></span> <span data-ttu-id="74d85-153">В следующем примере задается контекст для хранилища *testvault*.</span><span class="sxs-lookup"><span data-stu-id="74d85-153">The following example sets the vault context for the vault, *testvault*.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesVault -Name "testvault" | Set-AzureRmRecoveryServicesVaultContext
```

### <a name="create-a-protection-policy"></a><span data-ttu-id="74d85-154">Создание политики защиты</span><span class="sxs-lookup"><span data-stu-id="74d85-154">Create a protection policy</span></span>
<span data-ttu-id="74d85-155">Создаваемое хранилище служб восстановления поставляется с политиками защиты и хранения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="74d85-155">When you create a Recovery Services vault, it comes with default protection and retention policies.</span></span> <span data-ttu-id="74d85-156">Политика защиты по умолчанию запускает задание резервного копирования каждый день в указанное время.</span><span class="sxs-lookup"><span data-stu-id="74d85-156">The default protection policy triggers a backup job each day at a specified time.</span></span> <span data-ttu-id="74d85-157">Политика хранения по умолчанию хранит ежедневную точку восстановления в течение 30 дней.</span><span class="sxs-lookup"><span data-stu-id="74d85-157">The default retention policy retains the daily recovery point for 30 days.</span></span> <span data-ttu-id="74d85-158">С помощью политики по умолчанию можно быстро защитить виртуальную машину. Кроме того, политику можно изменить позже, задав другие сведения.</span><span class="sxs-lookup"><span data-stu-id="74d85-158">You can use the default policy to quickly protect your VM and edit the policy later with different details.</span></span>

<span data-ttu-id="74d85-159">Для получения списка политик хранения в хранилище используется командлет **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)**.</span><span class="sxs-lookup"><span data-stu-id="74d85-159">Use **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)** to view the protection policies in the vault.</span></span> <span data-ttu-id="74d85-160">С его помощью можно получить конкретную политику или просмотреть политики, связанные с типом рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="74d85-160">You can use this cmdlet to get a specific policy, or to view the policies associated with a workload type.</span></span> <span data-ttu-id="74d85-161">В следующем примере возвращаются политики для типа рабочей нагрузки AzureVM.</span><span class="sxs-lookup"><span data-stu-id="74d85-161">The following example gets policies for workload type, AzureVM.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesBackupProtectionPolicy -WorkloadType "AzureVM"
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
DefaultPolicy        AzureVM            AzureVM              4/14/2016 5:00:00 PM
```

> [!NOTE]
> <span data-ttu-id="74d85-162">Часовой пояс поля BackupTime в PowerShell — UTC.</span><span class="sxs-lookup"><span data-stu-id="74d85-162">The timezone of the BackupTime field in PowerShell is UTC.</span></span> <span data-ttu-id="74d85-163">Однако при отображении времени архивации на портале Azure время меняется в соответствии с локальным часовым поясом.</span><span class="sxs-lookup"><span data-stu-id="74d85-163">However, when the backup time is shown in the Azure portal, the time is adjusted to your local timezone.</span></span>
>
>

<span data-ttu-id="74d85-164">Политика защиты архивации связана по крайней мере с одной политикой хранения.</span><span class="sxs-lookup"><span data-stu-id="74d85-164">A backup protection policy is associated with at least one retention policy.</span></span> <span data-ttu-id="74d85-165">Политика хранения определяет продолжительность хранения точки восстановления до ее удаления.</span><span class="sxs-lookup"><span data-stu-id="74d85-165">Retention policy defines how long a recovery point is kept before it is deleted.</span></span> <span data-ttu-id="74d85-166">Для просмотра политики хранения по умолчанию используется командлет **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)**.</span><span class="sxs-lookup"><span data-stu-id="74d85-166">Use **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)** to view the default retention policy.</span></span>  <span data-ttu-id="74d85-167">Аналогичным образом, для получения политики расписания по умолчанию используется командлет **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)**.</span><span class="sxs-lookup"><span data-stu-id="74d85-167">Similarly you can use **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)** to obtain the default schedule policy.</span></span> <span data-ttu-id="74d85-168">Командлет **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** создает объект PowerShell, который содержит сведения о политике архивации.</span><span class="sxs-lookup"><span data-stu-id="74d85-168">The **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="74d85-169">Объекты политик расписания и хранения используются в качестве входных данных в командлете **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**.</span><span class="sxs-lookup"><span data-stu-id="74d85-169">The schedule and retention policy objects are used as inputs to the **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet.</span></span> <span data-ttu-id="74d85-170">В следующем примере показано сохранение политик расписания и хранения в переменных.</span><span class="sxs-lookup"><span data-stu-id="74d85-170">The following example stores the schedule policy and the retention policy in variables.</span></span> <span data-ttu-id="74d85-171">В примере эти переменные используются для определения параметров при создании политики защиты *NewPolicy*.</span><span class="sxs-lookup"><span data-stu-id="74d85-171">The example uses those variables to define the parameters when creating a protection policy, *NewPolicy*.</span></span>

```
PS C:\> $schPol = Get-AzureRmRecoveryServicesBackupSchedulePolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> New-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy" -WorkloadType "AzureVM" -RetentionPolicy $retPol -SchedulePolicy $schPol
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
NewPolicy           AzureVM            AzureVM              4/24/2016 1:30:00 AM
```


### <a name="enable-protection"></a><span data-ttu-id="74d85-172">Включить защиту</span><span class="sxs-lookup"><span data-stu-id="74d85-172">Enable protection</span></span>
<span data-ttu-id="74d85-173">После определения политики защиты архивации по-прежнему необходимо включить политику для элемента.</span><span class="sxs-lookup"><span data-stu-id="74d85-173">Once you have defined the backup protection policy, you still must enable the policy for an item.</span></span> <span data-ttu-id="74d85-174">Для включения защиты используйте командлет **[Enable-AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)**.</span><span class="sxs-lookup"><span data-stu-id="74d85-174">Use **[Enable-AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)** to enable protection.</span></span> <span data-ttu-id="74d85-175">Защита включается для двух объектов: элемента и политики.</span><span class="sxs-lookup"><span data-stu-id="74d85-175">Enabling protection requires two objects - the item and the policy.</span></span> <span data-ttu-id="74d85-176">После того как политика сопоставится с хранилищем, рабочий процесс архивации будет активироваться по времени, определенному в политике расписания.</span><span class="sxs-lookup"><span data-stu-id="74d85-176">Once the policy has been associated with the vault, the backup workflow is triggered at the time defined in the policy schedule.</span></span>

<span data-ttu-id="74d85-177">В следующем примере включается защита для элемента V2VM с помощью политики NewPolicy.</span><span class="sxs-lookup"><span data-stu-id="74d85-177">The following example enables protection for the item, V2VM, using the policy, NewPolicy.</span></span> <span data-ttu-id="74d85-178">Включение защиты на виртуальных машинах Resource Manager без шифрования</span><span class="sxs-lookup"><span data-stu-id="74d85-178">To enable the protection on non-encrypted Resource Manager VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="74d85-179">Чтобы включить защиту на зашифрованных виртуальных машинах (зашифрованных с помощью BEK и KEK), необходимо предоставить службе архивации Azure разрешения на доступ для чтения ключей и секретов из хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="74d85-179">To enable the protection on encrypted VMs (encrypted using BEK and KEK), you need to give the Azure Backup service permission to read keys and secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToKeys backup,get,list -PermissionsToSecrets get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="74d85-180">Чтобы включить защиту на зашифрованных виртуальных машинах (зашифрованных только с помощью BEK), необходимо предоставить службе Azure Backup разрешение на доступ для чтения секретов из хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="74d85-180">To enable the protection on encrypted VMs (encrypted using BEK only), you need to give the Azure Backup service permission to read secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToSecrets backup,get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

> [!NOTE]
> <span data-ttu-id="74d85-181">Если вы работаете в облаке Azure для государственных организаций, используйте значение ff281ffe-705c-4f53-9f37-a40e6f2c68f3 для параметра **-ServicePrincipalName** в командлете [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy).</span><span class="sxs-lookup"><span data-stu-id="74d85-181">If you are using the Azure Government cloud, then use the value ff281ffe-705c-4f53-9f37-a40e6f2c68f3 for the parameter **-ServicePrincipalName** in [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet.</span></span>
>
>

<span data-ttu-id="74d85-182">Классические виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="74d85-182">For classic VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V1VM" -ServiceName "ServiceName1"
```

### <a name="modify-a-protection-policy"></a><span data-ttu-id="74d85-183">Изменение политики защиты</span><span class="sxs-lookup"><span data-stu-id="74d85-183">Modify a protection policy</span></span>
<span data-ttu-id="74d85-184">Чтобы изменить политику защиты, используйте командлет [Set-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) для изменения объектов SchedulePolicy или RetentionPolicy.</span><span class="sxs-lookup"><span data-stu-id="74d85-184">To modify the protection policy, use [Set-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) to modify the SchedulePolicy or RetentionPolicy objects.</span></span>

<span data-ttu-id="74d85-185">В следующем примере количество дней хранения точки восстановления изменяется на 365.</span><span class="sxs-lookup"><span data-stu-id="74d85-185">The following example changes the recovery point retention to 365 days.</span></span>

```
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol.DailySchedule.DurationCountInDays = 365
PS C:\> $pol= Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Set-AzureRmRecoveryServicesBackupProtectionPolicy -Policy $pol  -RetentionPolicy $RetPol
```

## <a name="trigger-a-backup"></a><span data-ttu-id="74d85-186">Активация архивации</span><span class="sxs-lookup"><span data-stu-id="74d85-186">Trigger a backup</span></span>
<span data-ttu-id="74d85-187">Для запуска задания резервного копирования используйте командлет **[Backup-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)**.</span><span class="sxs-lookup"><span data-stu-id="74d85-187">You can use **[Backup-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)** to trigger a backup job.</span></span> <span data-ttu-id="74d85-188">Если это начальная архивация, она является полной.</span><span class="sxs-lookup"><span data-stu-id="74d85-188">If it is the initial backup, it is a full backup.</span></span> <span data-ttu-id="74d85-189">При последующем выполнении архивации резервная копия будет добавочной.</span><span class="sxs-lookup"><span data-stu-id="74d85-189">Subsequent backups take an incremental copy.</span></span> <span data-ttu-id="74d85-190">Перед запуском задания резервного копирования выполните командлет **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**, чтобы задать контекст хранилища.</span><span class="sxs-lookup"><span data-stu-id="74d85-190">Be sure to use **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** to set the vault context before triggering the backup job.</span></span> <span data-ttu-id="74d85-191">В следующем примере предполагается, что контекст хранилища был задан.</span><span class="sxs-lookup"><span data-stu-id="74d85-191">The following example assumes vault context was set.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer -ContainerType "AzureVM" -Status "Registered" -FriendlyName "V2VM"
PS C:\> $item = Get-AzureRmRecoveryServicesBackupItem -Container $namedContainer -WorkloadType "AzureVM"
PS C:\> $job = Backup-AzureRmRecoveryServicesBackupItem -Item $item
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM              Backup               InProgress            4/23/2016 5:00:30 PM                       cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

> [!NOTE]
> <span data-ttu-id="74d85-192">Часовой пояс для полей StartTime и EndTime в PowerShell — UTC.</span><span class="sxs-lookup"><span data-stu-id="74d85-192">The timezone of the StartTime and EndTime fields in PowerShell is UTC.</span></span> <span data-ttu-id="74d85-193">Однако при отображении времени на портале Azure время меняется в соответствии с локальным часовым поясом.</span><span class="sxs-lookup"><span data-stu-id="74d85-193">However, when the time is shown in the Azure portal, the time is adjusted to your local timezone.</span></span>
>
>

## <a name="monitoring-a-backup-job"></a><span data-ttu-id="74d85-194">Наблюдение за выполнением задания резервного копирования</span><span class="sxs-lookup"><span data-stu-id="74d85-194">Monitoring a backup job</span></span>
<span data-ttu-id="74d85-195">Вы можете отслеживать длительные операции, например задания резервного копирования, без использования портала Azure.</span><span class="sxs-lookup"><span data-stu-id="74d85-195">You can monitor long-running operations, such as backup jobs, without using the Azure portal.</span></span> <span data-ttu-id="74d85-196">Чтобы получить последнее состояние выполняющегося задания, используйте командлет **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)**.</span><span class="sxs-lookup"><span data-stu-id="74d85-196">To get the status of an in-progress job, use the **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="74d85-197">Этот командлет возвращает задания резервного копирования для конкретного хранилища, и это хранилище указывается в контексте хранилища.</span><span class="sxs-lookup"><span data-stu-id="74d85-197">This cmdlet gets the backup jobs for a specific vault, and that vault is specified in the vault context.</span></span> <span data-ttu-id="74d85-198">Следующий пример возвращает состояние выполняющегося задания в виде массива и сохраняет состояние в переменной $joblist.</span><span class="sxs-lookup"><span data-stu-id="74d85-198">The following example gets the status of an in-progress job as an array, and stores the status in the $joblist variable.</span></span>

```
PS C:\> $joblist = Get-AzureRmRecoveryservicesBackupJob –Status "InProgress"
PS C:\> $joblist[0]
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM             Backup               InProgress            4/23/2016 5:00:30 PM           cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="74d85-199">Вместо опроса этих заданий о ходе их выполнения, который требует выполнения дополнительного кода, используйте командлет **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**.</span><span class="sxs-lookup"><span data-stu-id="74d85-199">Instead of polling these jobs for completion - which is unnecessary additional code - use the **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="74d85-200">Он приостанавливает выполнение сценария до завершения задания или до достижения конкретного значения времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="74d85-200">This cmdlet pauses the execution until either the job completes or the specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $joblist[0] -Timeout 43200
```

## <a name="restore-an-azure-vm"></a><span data-ttu-id="74d85-201">Восстановление виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="74d85-201">Restore an Azure VM</span></span>
<span data-ttu-id="74d85-202">Операции восстановления виртуальной машины через портал Azure и с помощью Azure PowerShell существенно отличаются.</span><span class="sxs-lookup"><span data-stu-id="74d85-202">There is a key difference between the restoring a VM using the Azure portal and restoring a VM using PowerShell.</span></span> <span data-ttu-id="74d85-203">При использовании PowerShell операция восстановления завершается созданием дисков и сведений о конфигурации из точки восстановления.</span><span class="sxs-lookup"><span data-stu-id="74d85-203">With PowerShell, the restore operation is complete once the disks and configuration information from the recovery point are created.</span></span>

> [!NOTE]
> <span data-ttu-id="74d85-204">Виртуальная машина при этом не создается,</span><span class="sxs-lookup"><span data-stu-id="74d85-204">The restore operation does not create a virtual machine.</span></span>
>
>

<span data-ttu-id="74d85-205">Чтобы создать виртуальную машину с диска, см. сведения в разделе [Создание виртуальной машины с хранимых дисков](backup-azure-vms-automation.md#create-a-vm-from-stored-disks).</span><span class="sxs-lookup"><span data-stu-id="74d85-205">To create a virtual machine from disk, see the section, [Create the VM from stored disks](backup-azure-vms-automation.md#create-a-vm-from-stored-disks).</span></span> <span data-ttu-id="74d85-206">Ниже перечислены основные шаги для восстановления виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="74d85-206">The basic steps to restore an Azure VM are:</span></span>

* <span data-ttu-id="74d85-207">Выбор виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="74d85-207">Select the VM</span></span>
* <span data-ttu-id="74d85-208">Выбор точки восстановления</span><span class="sxs-lookup"><span data-stu-id="74d85-208">Choose a recovery point</span></span>
* <span data-ttu-id="74d85-209">Восстановление дисков</span><span class="sxs-lookup"><span data-stu-id="74d85-209">Restore the disks</span></span>
* <span data-ttu-id="74d85-210">Создание виртуальной машины с хранимых дисков</span><span class="sxs-lookup"><span data-stu-id="74d85-210">Create the VM from stored disks</span></span>

<span data-ttu-id="74d85-211">На представленной ниже схеме показана иерархия объектов от RecoveryServicesVault до BackupRecoveryPoint.</span><span class="sxs-lookup"><span data-stu-id="74d85-211">The following graphic shows the object hierarchy from the RecoveryServicesVault down to the BackupRecoveryPoint.</span></span>

![Иерархия объектов служб восстановления с BackupContainer](./media/backup-azure-vms-arm-automation/backuprecoverypoint-only.png)

<span data-ttu-id="74d85-213">Чтобы восстановить данные резервной копии, определите архивный элемент и точку восстановления, которая содержит данные на определенный момент времени.</span><span class="sxs-lookup"><span data-stu-id="74d85-213">To restore backup data, identify the backed-up item and the recovery point that holds the point-in-time data.</span></span> <span data-ttu-id="74d85-214">Выполните командлет **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**, чтобы восстановить данные из хранилища в учетную запись клиента.</span><span class="sxs-lookup"><span data-stu-id="74d85-214">Use the **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet to restore data from the vault to the customer's account.</span></span>

### <a name="select-the-vm"></a><span data-ttu-id="74d85-215">Выбор виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="74d85-215">Select the VM</span></span>
<span data-ttu-id="74d85-216">Чтобы получить объект PowerShell, определяющий правильный архивный элемент, начните с контейнера в хранилище и пройдите постепенно вниз по иерархии объектов.</span><span class="sxs-lookup"><span data-stu-id="74d85-216">To get the PowerShell object that identifies the right backup item, start from the container in the vault, and work your way down the object hierarchy.</span></span> <span data-ttu-id="74d85-217">Чтобы выбрать контейнер, который представляет виртуальную машину, используйте командлет **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)** и передайте найденный контейнер в командлет **[Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)**.</span><span class="sxs-lookup"><span data-stu-id="74d85-217">To select the container that represents the VM, use the **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)** cmdlet and pipe that to the **[Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)** cmdlet.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer  -ContainerType "AzureVM" –Status "Registered" -FriendlyName "V2VM"
PS C:\> $backupitem = Get-AzureRmRecoveryServicesBackupItem –Container $namedContainer  –WorkloadType "AzureVM"
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="74d85-218">Выбор точки восстановления</span><span class="sxs-lookup"><span data-stu-id="74d85-218">Choose a recovery point</span></span>
<span data-ttu-id="74d85-219">Выполните командлет **[Get-AzureRMRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)**, чтобы получить полный список точек восстановления.</span><span class="sxs-lookup"><span data-stu-id="74d85-219">Use the **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)** cmdlet to list all recovery points for the backup item.</span></span> <span data-ttu-id="74d85-220">Выберите нужную точку восстановления.</span><span class="sxs-lookup"><span data-stu-id="74d85-220">Then choose the recovery point to restore.</span></span> <span data-ttu-id="74d85-221">Если вы не знаете, какую точку восстановления выбрать, используйте последнюю точку RecoveryPointType = AppConsistent в списке.</span><span class="sxs-lookup"><span data-stu-id="74d85-221">If you are unsure which recovery point to use, it is a good practice to choose the most recent RecoveryPointType = AppConsistent point in the list.</span></span>

<span data-ttu-id="74d85-222">В следующем сценарии переменная **$rp**представляет собой массив точек восстановления для выбранного архивного элемента за последние семь дней.</span><span class="sxs-lookup"><span data-stu-id="74d85-222">In the following script, the variable, **$rp**, is an array of recovery points for the selected backup item, from the past seven days.</span></span> <span data-ttu-id="74d85-223">Массив сортируется по времени в обратном порядке, так что последняя точка восстановления получает индекс 0.</span><span class="sxs-lookup"><span data-stu-id="74d85-223">The array is sorted in reverse order of time with the latest recovery point at index 0.</span></span> <span data-ttu-id="74d85-224">Используйте стандартное индексирование массива PowerShell для выбора точки восстановления.</span><span class="sxs-lookup"><span data-stu-id="74d85-224">Use standard PowerShell array indexing to pick the recovery point.</span></span> <span data-ttu-id="74d85-225">Например, $rp[0] обозначает последнюю точку восстановления.</span><span class="sxs-lookup"><span data-stu-id="74d85-225">In the example, $rp[0] selects the latest recovery point.</span></span>

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



### <a name="restore-the-disks"></a><span data-ttu-id="74d85-226">Восстановление дисков</span><span class="sxs-lookup"><span data-stu-id="74d85-226">Restore the disks</span></span>
<span data-ttu-id="74d85-227">Выполните командлет **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**, чтобы восстановить данные и конфигурацию архивного элемента до точки восстановления.</span><span class="sxs-lookup"><span data-stu-id="74d85-227">Use the **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet to restore a backup item's data and configuration to a recovery point.</span></span> <span data-ttu-id="74d85-228">Используйте выбранную точку восстановления как значение для параметра **-RecoveryPoint**.</span><span class="sxs-lookup"><span data-stu-id="74d85-228">Once you have identified a recovery point, use it as the value for the **-RecoveryPoint** parameter.</span></span> <span data-ttu-id="74d85-229">В предыдущем примере кода была выбрана точка восстановления **$rp[0]**.</span><span class="sxs-lookup"><span data-stu-id="74d85-229">In the previous sample code, **$rp[0]** was the recovery point to use.</span></span> <span data-ttu-id="74d85-230">В следующем примере кода **$rp[0]** является точкой восстановления, которая используется для восстановления диска.</span><span class="sxs-lookup"><span data-stu-id="74d85-230">In the following sample code, **$rp[0]** is the recovery point to use for restoring the disk.</span></span>

<span data-ttu-id="74d85-231">Восстановление дисков и сведений о конфигурации</span><span class="sxs-lookup"><span data-stu-id="74d85-231">To restore the disks and configuration information:</span></span>

```
PS C:\> $restorejob = Restore-AzureRmRecoveryServicesBackupItem -RecoveryPoint $rp[0] -StorageAccountName "DestAccount" -StorageAccountResourceGroupName "DestRG"
PS C:\> $restorejob
WorkloadName     Operation          Status               StartTime                 EndTime            JobID
------------     ---------          ------               ---------                 -------          ----------
V2VM              Restore           InProgress           4/23/2016 5:00:30 PM                        cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="74d85-232">С помощью командлета **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** можно дождаться завершения задания восстановления.</span><span class="sxs-lookup"><span data-stu-id="74d85-232">Use the **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet to wait for the Restore job to complete.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $restorejob -Timeout 43200
```

<span data-ttu-id="74d85-233">Когда задание восстановления будет выполнено, выполните командлет **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)**, чтобы получить сведения об операции восстановления.</span><span class="sxs-lookup"><span data-stu-id="74d85-233">Once the Restore job has completed, use the **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)** cmdlet to get the details of the restore operation.</span></span> <span data-ttu-id="74d85-234">Свойство JobDetails содержит сведения, необходимые для повторного создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="74d85-234">The JobDetails property has the information needed to rebuild the VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmRecoveryServicesBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmRecoveryServicesBackupJobDetails -Job $restorejob
```

<span data-ttu-id="74d85-235">Восстановив диски, перейдите к следующему разделу по созданию виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="74d85-235">Once you restore the disks, go to the next section to create the VM.</span></span>

## <a name="create-a-vm-from-restored-disks"></a><span data-ttu-id="74d85-236">Создание виртуальной машины с восстановленного диска</span><span class="sxs-lookup"><span data-stu-id="74d85-236">Create a VM from restored disks</span></span>
<span data-ttu-id="74d85-237">После восстановления дисков создайте и настройте виртуальную машину с диска, выполнив описанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="74d85-237">After you have restored the disks, use these steps to create and configure the virtual machine from disk.</span></span>

> [!NOTE]
> <span data-ttu-id="74d85-238">При создании зашифрованных виртуальных машин с помощью восстановленных дисков у роли Azure должно быть разрешение на выполнение действия **Microsoft.KeyVault/vaults/deploy/action**.</span><span class="sxs-lookup"><span data-stu-id="74d85-238">To create encrypted VMs from restored disks, your Azure role must have permission to perform the action, **Microsoft.KeyVault/vaults/deploy/action**.</span></span> <span data-ttu-id="74d85-239">Если у роли нет этого разрешения, создайте пользовательскую роль с этим действием.</span><span class="sxs-lookup"><span data-stu-id="74d85-239">If your role does not have this permission, create a custom role with this action.</span></span> <span data-ttu-id="74d85-240">Дополнительные сведения см. в разделе [Пользовательские роли в Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="74d85-240">For more information, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>
>
>

1. <span data-ttu-id="74d85-241">Запросите свойства восстановленного диска для получения сведений о задании.</span><span class="sxs-lookup"><span data-stu-id="74d85-241">Query the restored disk properties for the job details.</span></span>

  ```
  PS C:\> $properties = $details.properties
  PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
  PS C:\> $containerName = $properties["Config Blob Container Name"]
  PS C:\> $blobName = $properties["Config Blob Name"]
  ```

2. <span data-ttu-id="74d85-242">Задайте контекст хранилища Azure и восстановите файл конфигурации JSON.</span><span class="sxs-lookup"><span data-stu-id="74d85-242">Set the Azure storage context and restore the JSON configuration file.</span></span>

    ```
    PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName "testvault"
    PS C:\> $destination_path = "C:\vmconfig.json"
    PS C:\> Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path
    PS C:\> $obj = ((Get-Content -Path $destination_path -Raw -Encoding Unicode)).TrimEnd([char]0x00) | ConvertFrom-Json
    ```

3. <span data-ttu-id="74d85-243">Используйте файл конфигурации JSON для создания конфигурации виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="74d85-243">Use the JSON configuration file to create the VM configuration.</span></span>

    ```
   PS C:\> $vm = New-AzureRmVMConfig -VMSize $obj.'properties.hardwareProfile'.vmSize -VMName "testrestore"
    ```

4. <span data-ttu-id="74d85-244">Подключите диск операционной системы и диски данных.</span><span class="sxs-lookup"><span data-stu-id="74d85-244">Attach the OS disk and data disks.</span></span> <span data-ttu-id="74d85-245">В зависимости от конфигурации виртуальных машин щелкните соответствующую ссылку для просмотра соответствующих командлетов:</span><span class="sxs-lookup"><span data-stu-id="74d85-245">Depending on the configuration of your VMs, click on the relevant link to view respective cmdlets:</span></span> 
    - [<span data-ttu-id="74d85-246">Неуправляемые, без шифрования виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="74d85-246">Non-managed, non-encrypted VMs</span></span>](#non-managed-non-encrypted-vms)
    - [<span data-ttu-id="74d85-247">Неуправляемые, зашифрованный виртуальных машин (BEK)</span><span class="sxs-lookup"><span data-stu-id="74d85-247">Non-managed, encrypted VMs (BEK only)</span></span>](#non-managed-encrypted-vms-bek-only)
    - [<span data-ttu-id="74d85-248">Виртуальные машины неуправляемые, зашифрованный (BEK и Ключами)</span><span class="sxs-lookup"><span data-stu-id="74d85-248">Non-managed, encrypted VMs (BEK and KEK)</span></span>](#non-managed-encrypted-vms-bek-and-kek)
    - [<span data-ttu-id="74d85-249">Управляемые без шифрования виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="74d85-249">Managed, non-encrypted VMs</span></span>](#managed-non-encrypted-vms)
    - [<span data-ttu-id="74d85-250">Виртуальные машины управляемых, зашифрованный (BEK и Ключами)</span><span class="sxs-lookup"><span data-stu-id="74d85-250">Managed, encrypted VMs (BEK and KEK)</span></span>](#managed-encrypted-vms-bek-and-kek)
    
    #### <a name="non-managed-non-encrypted-vms"></a><span data-ttu-id="74d85-251">Неуправляемые незашифрованные виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="74d85-251">Non-managed, non-encrypted VMs</span></span>

    <span data-ttu-id="74d85-252">Используйте следующий пример для неуправляемой виртуальной машины без шифрования.</span><span class="sxs-lookup"><span data-stu-id="74d85-252">Use the following sample for non-managed, non-encrypted VMs.</span></span>

    ```
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.StorageProfile'.osDisk.vhd.Uri -CreateOption "Attach"
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.StorageProfile'.OsDisk.OsType
    PS C:\> foreach($dd in $obj.'properties.StorageProfile'.DataDisks)
    {
    $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="non-managed-encrypted-vms-bek-only"></a><span data-ttu-id="74d85-253">Неуправляемые зашифрованные виртуальные машины (только BEK)</span><span class="sxs-lookup"><span data-stu-id="74d85-253">Non-managed, encrypted VMs (BEK only)</span></span>

    <span data-ttu-id="74d85-254">Для неуправляемых зашифрованных виртуальных машин (зашифрованных только с помощью BEK) необходимо восстановить секрет в хранилище ключей до подключения дисков.</span><span class="sxs-lookup"><span data-stu-id="74d85-254">For non-managed, encrypted VMs (encrypted using BEK only), you need to restore the secret to the key vault before you can attach disks.</span></span> <span data-ttu-id="74d85-255">Дополнительные сведения см. в статье [Восстановление зашифрованной виртуальной машины из точки восстановления службы архивации Azure](backup-azure-restore-key-secret.md).</span><span class="sxs-lookup"><span data-stu-id="74d85-255">For more information, please see the article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="74d85-256">В следующем примере показано, как подключить диски операционной системы и диски данных к зашифрованной виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="74d85-256">The following sample shows how to attach OS and data disks for encrypted VMs.</span></span>

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

    #### <a name="non-managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="74d85-257">Неуправляемые зашифрованные виртуальные машины (BEK и KEK)</span><span class="sxs-lookup"><span data-stu-id="74d85-257">Non-managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="74d85-258">Для неуправляемых зашифрованных виртуальных машин (зашифрованных с помощью BEK и KEK) необходимо восстановить ключ и секрет в хранилище ключей до подключения дисков.</span><span class="sxs-lookup"><span data-stu-id="74d85-258">For non-managed, encrypted VMs (encrypted using BEK and KEK), you need to restore the key and secret to the key vault before you can attach disks.</span></span> <span data-ttu-id="74d85-259">Дополнительные сведения см. в статье [Восстановление зашифрованной виртуальной машины из точки восстановления службы архивации Azure](backup-azure-restore-key-secret.md).</span><span class="sxs-lookup"><span data-stu-id="74d85-259">For more information, please see the article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="74d85-260">В следующем примере показано, как подключить диски операционной системы и диски данных к зашифрованной виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="74d85-260">The following sample shows how to attach OS and data disks for encrypted VMs.</span></span>

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

    #### <a name="managed-non-encrypted-vms"></a><span data-ttu-id="74d85-261">Управляемые незашифрованные виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="74d85-261">Managed, non-encrypted VMs</span></span>

    <span data-ttu-id="74d85-262">Для незашифрованных управляемых виртуальных машин следует создать управляемые диски из хранилища BLOB-объектов, а затем подключить их.</span><span class="sxs-lookup"><span data-stu-id="74d85-262">For managed non-encrypted VMs, you'll need to create managed disks from blob storage, and then attach the disks.</span></span> <span data-ttu-id="74d85-263">Более подробные сведения см. в статье [Подключение диска данных к виртуальной машине Windows с помощью PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="74d85-263">For in-depth information, see the article, [Attach a data disk to a Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="74d85-264">В следующем примере кода показано, как подключить диски данных к управляемой незашифрованной виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="74d85-264">The following sample code shows how to attach the data disks for managed non-encrypted VMs.</span></span>

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

    #### <a name="managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="74d85-265">Управляемые зашифрованные виртуальные машины (BEK и KEK)</span><span class="sxs-lookup"><span data-stu-id="74d85-265">Managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="74d85-266">Для зашифрованных управляемых виртуальных машин (зашифрованных с помощью BEK и KEK) следует создать управляемые диски из хранилища BLOB-объектов, а затем подключить эти диски.</span><span class="sxs-lookup"><span data-stu-id="74d85-266">For managed encrypted VMs (encrypted using BEK and KEK), you'll need to create managed disks from blob storage, and then attach the disks.</span></span> <span data-ttu-id="74d85-267">Более подробные сведения см. в статье [Подключение диска данных к виртуальной машине Windows с помощью PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="74d85-267">For in-depth information, see the article, [Attach a data disk to a Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="74d85-268">В следующем примере кода показано, как подключить диски данных к управляемой зашифрованной виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="74d85-268">The following sample code shows how to attach the data disks for managed encrypted VMs.</span></span>

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

5. <span data-ttu-id="74d85-269">Задайте параметры сети.</span><span class="sxs-lookup"><span data-stu-id="74d85-269">Set the Network settings.</span></span>

    ```
    PS C:\> $nicName="p1234"
    PS C:\> $pip = New-AzureRmPublicIpAddress -Name $nicName -ResourceGroupName "test" -Location "WestUS" -AllocationMethod Dynamic
    PS C:\> $vnet = Get-AzureRmVirtualNetwork -Name "testvNET" -ResourceGroupName "test"
    PS C:\> $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName "test" -Location "WestUS" -SubnetId $vnet.Subnets[$subnetindex].Id -PublicIpAddressId $pip.Id
    PS C:\> $vm=Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    ```
6. <span data-ttu-id="74d85-270">Создайте виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="74d85-270">Create the virtual machine.</span></span>

    ```    
    PS C:\> New-AzureRmVM -ResourceGroupName "test" -Location "WestUS" -VM $vm
    ```

## <a name="next-steps"></a><span data-ttu-id="74d85-271">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="74d85-271">Next steps</span></span>
<span data-ttu-id="74d85-272">Если вы предпочитаете использовать PowerShell для взаимодействия с ресурсами Azure, см. статью [Развертывание резервного копирования в Azure для Windows Server или клиента Windows и управление им с помощью PowerShell](backup-client-automation.md).</span><span class="sxs-lookup"><span data-stu-id="74d85-272">If you prefer to use PowerShell to engage with your Azure resources, see the PowerShell article, [Deploy and Manage Backup for Windows Server](backup-client-automation.md).</span></span> <span data-ttu-id="74d85-273">Сведения об управлении резервными копиями DPM см. в статье [Развертывание службы архивации для DPM и управление ею](backup-dpm-automation.md).</span><span class="sxs-lookup"><span data-stu-id="74d85-273">If you manage DPM backups, see the article, [Deploy and Manage Backup for DPM](backup-dpm-automation.md).</span></span> <span data-ttu-id="74d85-274">Обе эти статьи имеют две версии — для развертывания с помощью Resource Manager и для классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="74d85-274">Both of these articles have a version for Resource Manager deployments and Classic deployments.</span></span>  
