---
title: "aaaDeploy и управление резервным копированием для виртуальных машин Azure с помощью PowerShell | Документы Microsoft"
description: "Узнайте, как toodeploy и управление резервным копированием Azure с помощью PowerShell."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 2e24b1d9-4375-4049-a28d-e3bc01152f32
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: markgal;trinadhk;jimpark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f3ecd3f94c5e3e8fc8018e8786302edd4847744b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azurermbackup-cmdlets-tooback-up-virtual-machines"></a><span data-ttu-id="c5aef-103">Использовать tooback командлеты AzureRM.Backup копирование виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="c5aef-103">Use AzureRM.Backup cmdlets tooback up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c5aef-104">Диспетчер ресурсов</span><span class="sxs-lookup"><span data-stu-id="c5aef-104">Resource Manager</span></span>](backup-azure-vms-automation.md)
> * [<span data-ttu-id="c5aef-105">Классический</span><span class="sxs-lookup"><span data-stu-id="c5aef-105">Classic</span></span>](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="c5aef-106">В этой статье показано, как toouse Azure PowerShell для резервного копирования и восстановления виртуальных машин Azure.</span><span class="sxs-lookup"><span data-stu-id="c5aef-106">This article shows you how toouse Azure PowerShell for backup and recovery of Azure VMs.</span></span> <span data-ttu-id="c5aef-107">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: модель Resource Manager и классическая модель.</span><span class="sxs-lookup"><span data-stu-id="c5aef-107">Azure has two different deployment models for creating and working with resources: Resource Manager and Classic.</span></span> <span data-ttu-id="c5aef-108">В этой статье описан с помощью tooback модели развертывания классический hello копирование данных tooa резервное хранилище.</span><span class="sxs-lookup"><span data-stu-id="c5aef-108">This article covers using hello Classic deployment model tooback up data tooa Backup vault.</span></span> <span data-ttu-id="c5aef-109">Если вы не создали резервное хранилище в вашей подписке, см. раздел hello диспетчера ресурсов версию этой статьи [tooback AzureRM.RecoveryServices.Backup используйте командлеты копирование виртуальных машин](backup-azure-vms-automation.md).</span><span class="sxs-lookup"><span data-stu-id="c5aef-109">If you have not created a Backup vault in your subscription, see hello Resource Manager version of this article, [Use AzureRM.RecoveryServices.Backup cmdlets tooback up virtual machines](backup-azure-vms-automation.md).</span></span> <span data-ttu-id="c5aef-110">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c5aef-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c5aef-111">Теперь можно обновить вашими хранилищами служб tooRecovery хранилища резервной копии.</span><span class="sxs-lookup"><span data-stu-id="c5aef-111">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="c5aef-112">Дополнительные сведения см. в статье hello [обновление tooa хранилища резервной копии, в хранилище служб восстановления](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="c5aef-112">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="c5aef-113">Корпорация Майкрософт рекомендует tooupgrade вашей резервных хранилищ tooRecovery хранилищами служб.</span><span class="sxs-lookup"><span data-stu-id="c5aef-113">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="c5aef-114">После 15 октября 2017 г. нельзя использовать PowerShell toocreate резервное копирование хранилищ.</span><span class="sxs-lookup"><span data-stu-id="c5aef-114">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="c5aef-115">**К 1 ноября 2017 года**:</span><span class="sxs-lookup"><span data-stu-id="c5aef-115">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="c5aef-116">Все оставшиеся хранилища резервной копии будет автоматически обновленные tooRecovery хранилищами служб.</span><span class="sxs-lookup"><span data-stu-id="c5aef-116">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="c5aef-117">Вы не будет возможности tooaccess данные резервной копии hello классического портала.</span><span class="sxs-lookup"><span data-stu-id="c5aef-117">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="c5aef-118">Вместо этого используйте hello Azure портала tooaccess резервного копирования данных в хранилищах службы восстановления.</span><span class="sxs-lookup"><span data-stu-id="c5aef-118">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="concepts"></a><span data-ttu-id="c5aef-119">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="c5aef-119">Concepts</span></span>
<span data-ttu-id="c5aef-120">Эта статья содержит сведения о конкретных toohello командлеты PowerShell tooback копии виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="c5aef-120">This article provides information specific toohello PowerShell cmdlets used tooback up virtual machines.</span></span> <span data-ttu-id="c5aef-121">Чтобы изучить вводные сведения о защите виртуальных машин Azure, ознакомьтесь с разделом [Планирование инфраструктуры резервного копирования виртуальных машин в Azure](backup-azure-vms-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c5aef-121">For introductory information about protecting Azure VMs, please see [Plan your VM backup infrastructure in Azure](backup-azure-vms-introduction.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c5aef-122">Прежде чем начать, познакомьтесь hello [необходимые компоненты](backup-azure-vms-prepare.md) необходимые toowork с резервного копирования Azure и hello [ограничения](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) из текущего решения резервного копирования hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="c5aef-122">Before you start, read hello [prerequisites](backup-azure-vms-prepare.md) required toowork with Azure Backup, and hello [limitations](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) of hello current VM backup solution.</span></span>
>
>

<span data-ttu-id="c5aef-123">toouse PowerShell, по сути, принимают момент иерархии hello toounderstand объектов и откуда toostart.</span><span class="sxs-lookup"><span data-stu-id="c5aef-123">toouse PowerShell effectively, take a moment toounderstand hello hierarchy of objects and from where toostart.</span></span>

![Иерархия объектов](./media/backup-azure-vms-classic-automation/object-hierarchy.png)

<span data-ttu-id="c5aef-125">Hello два самых важных потока включения защиты для виртуальной Машины, а восстановление данных из точки восстановления.</span><span class="sxs-lookup"><span data-stu-id="c5aef-125">hello two most important flows are enabling protection for a VM, and restoring data from a recovery point.</span></span> <span data-ttu-id="c5aef-126">Hello посвящена эта статья является toohelp, вы становитесь детальное представление о работе с tooenable командлеты PowerShell hello эти два сценария.</span><span class="sxs-lookup"><span data-stu-id="c5aef-126">hello focus of this article is toohelp you become adept at working with hello PowerShell cmdlets tooenable these two scenarios.</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="c5aef-127">Настройка и регистрация</span><span class="sxs-lookup"><span data-stu-id="c5aef-127">Setup and Registration</span></span>
<span data-ttu-id="c5aef-128">toobegin:</span><span class="sxs-lookup"><span data-stu-id="c5aef-128">toobegin:</span></span>

1. <span data-ttu-id="c5aef-129">[Скачайте последнюю версию PowerShell](https://github.com/Azure/azure-powershell/releases) (минимальная требуемая версия — 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="c5aef-129">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="c5aef-130">Находите hello доступных командлетов Azure PowerShell резервного копирования с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c5aef-130">Find hello Azure Backup PowerShell cmdlets available by typing hello following command:</span></span>

```
PS C:\> Get-Command *azurermbackup*

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Backup-AzureRmBackupItem                           1.0.1      AzureRM.Backup
Cmdlet          Disable-AzureRmBackupProtection                    1.0.1      AzureRM.Backup
Cmdlet          Enable-AzureRmBackupContainerReregistration        1.0.1      AzureRM.Backup
Cmdlet          Enable-AzureRmBackupProtection                     1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupContainer                         1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupItem                              1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupJob                               1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupJobDetails                        1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupRecoveryPoint                     1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupVaultCredentials                  1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupRetentionPolicyObject             1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Register-AzureRmBackupContainer                    1.0.1      AzureRM.Backup
Cmdlet          Remove-AzureRmBackupProtectionPolicy               1.0.1      AzureRM.Backup
Cmdlet          Remove-AzureRmBackupVault                          1.0.1      AzureRM.Backup
Cmdlet          Restore-AzureRmBackupItem                          1.0.1      AzureRM.Backup
Cmdlet          Set-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          Set-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Stop-AzureRmBackupJob                              1.0.1      AzureRM.Backup
Cmdlet          Unregister-AzureRmBackupContainer                  1.0.1      AzureRM.Backup
Cmdlet          Wait-AzureRmBackupJob                              1.0.1      AzureRM.Backup
```

<span data-ttu-id="c5aef-131">Hello следующие программы установки и регистрации задачи можно автоматизировать с помощью PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c5aef-131">hello following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="c5aef-132">создать хранилище архивации;</span><span class="sxs-lookup"><span data-stu-id="c5aef-132">Create a backup vault</span></span>
* <span data-ttu-id="c5aef-133">Регистрация виртуальных машин hello hello службы архивации Azure</span><span class="sxs-lookup"><span data-stu-id="c5aef-133">Registering hello VMs with hello Azure Backup service</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="c5aef-134">создать хранилище архивации;</span><span class="sxs-lookup"><span data-stu-id="c5aef-134">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="c5aef-135">Для клиентов, использующих Azure Backup для hello первый раз необходимо использовать с вашей подпиской поставщика toobe tooregister hello Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="c5aef-135">For customers using Azure Backup for hello first time, you need tooregister hello Azure Backup provider toobe used with your subscription.</span></span> <span data-ttu-id="c5aef-136">Это можно сделать, выполнив следующую команду hello: Register AzureRmResourceProvider - ProviderNamespace «Microsoft.Backup»</span><span class="sxs-lookup"><span data-stu-id="c5aef-136">This can be done by running hello following command: Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="c5aef-137">Можно создать новое хранилище резервных копий с помощью hello **New AzureRmBackupVault** командлета.</span><span class="sxs-lookup"><span data-stu-id="c5aef-137">You can create a new backup vault using hello **New-AzureRmBackupVault** cmdlet.</span></span> <span data-ttu-id="c5aef-138">резервное хранилище Hello является ресурс ARM, поэтому вам необходимо tooplace его в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c5aef-138">hello backup vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="c5aef-139">В консоли Azure PowerShell с повышенными привилегиями выполните hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="c5aef-139">In an elevated Azure PowerShell console, run hello following commands:</span></span>

```
PS C:\> New-AzureRmResourceGroup –Name “test-rg” –Location “West US”
PS C:\> $backupvault = New-AzureRmBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

<span data-ttu-id="c5aef-140">Можно получить список всех резервных хранилищ hello в данной подписке с помощью hello **Get AzureRmBackupVault** командлета.</span><span class="sxs-lookup"><span data-stu-id="c5aef-140">You can get a list of all hello backup vaults in a given subscription using hello **Get-AzureRmBackupVault** cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="c5aef-141">— Это удобный toostore hello резервного хранилища объект в переменную.</span><span class="sxs-lookup"><span data-stu-id="c5aef-141">It is convenient toostore hello backup vault object into a variable.</span></span> <span data-ttu-id="c5aef-142">Hello объекта хранилища, необходимое в качестве входных данных для многих командлеты службы архивации Azure.</span><span class="sxs-lookup"><span data-stu-id="c5aef-142">hello vault object is needed as an input for many Azure Backup cmdlets.</span></span>
>
>

### <a name="registering-hello-vms"></a><span data-ttu-id="c5aef-143">Регистрация виртуальных машин hello</span><span class="sxs-lookup"><span data-stu-id="c5aef-143">Registering hello VMs</span></span>
<span data-ttu-id="c5aef-144">Hello первым шагом к настройке резервного копирования с помощью службы архивации Azure является tooregister компьютер или ВМ с Azure резервного хранилища.</span><span class="sxs-lookup"><span data-stu-id="c5aef-144">hello first step towards configuring backup with Azure Backup is tooregister your machine or VM with an Azure Backup vault.</span></span> <span data-ttu-id="c5aef-145">Hello **AzureRmBackupContainer регистра** командлет принимает входные данные для hello виртуальной машины Azure IaaS и регистрирует его с указанным хранилищем hello.</span><span class="sxs-lookup"><span data-stu-id="c5aef-145">hello **Register-AzureRmBackupContainer** cmdlet takes hello input information of an Azure IaaS virtual machine and registers it with hello specified vault.</span></span> <span data-ttu-id="c5aef-146">Операция register Hello связывает hello виртуальной машины Azure с резервным хранилищем hello и отслеживает hello ВМ жизненного цикла резервного копирования hello.</span><span class="sxs-lookup"><span data-stu-id="c5aef-146">hello register operation associates hello Azure virtual machine with hello backup vault and tracks hello VM through hello backup lifecycle.</span></span>

<span data-ttu-id="c5aef-147">Регистрация ВМ с hello службы архивации Azure создает объект верхнего уровня контейнера.</span><span class="sxs-lookup"><span data-stu-id="c5aef-147">Registering your VM with hello Azure Backup service creates a top-level container object.</span></span> <span data-ttu-id="c5aef-148">Контейнер обычно содержит несколько элементов, которые можно архивировать, но в случае hello виртуальных машин будет только один элемент резервного копирования для контейнера hello.</span><span class="sxs-lookup"><span data-stu-id="c5aef-148">A container typically contains multiple items that can be backed up, but in hello case of VMs there will be only one backup item for hello container.</span></span>

```
PS C:\> $registerjob = Register-AzureRmBackupContainer -Vault $backupvault -Name "testvm" -ServiceName "testvm"
```

## <a name="backup-azure-vms"></a><span data-ttu-id="c5aef-149">Виртуальные машины службы архивации Azure</span><span class="sxs-lookup"><span data-stu-id="c5aef-149">Backup Azure VMs</span></span>
### <a name="create-a-protection-policy"></a><span data-ttu-id="c5aef-150">Создание политики защиты</span><span class="sxs-lookup"><span data-stu-id="c5aef-150">Create a protection policy</span></span>
<span data-ttu-id="c5aef-151">Это не обязательное toocreate новую резервную копию toostart защиты политики виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="c5aef-151">It is not mandatory toocreate a new protection policy toostart backup of your VMs.</span></span> <span data-ttu-id="c5aef-152">хранилище Hello поставляется с «политика по умолчанию», можно использовать tooquickly включить защиту и затем hello правой сведения изменены позже.</span><span class="sxs-lookup"><span data-stu-id="c5aef-152">hello vault comes with a 'Default Policy' that can be used tooquickly enable protection, and then edited later with hello right details.</span></span> <span data-ttu-id="c5aef-153">Список политик hello, доступных в хранилище hello можно получить с помощью hello **Get AzureRmBackupProtectionPolicy** командлета:</span><span class="sxs-lookup"><span data-stu-id="c5aef-153">You can get a list of hello policies available in hello vault by using hello **Get-AzureRmBackupProtectionPolicy** cmdlet:</span></span>

```
PS C:\> Get-AzureRmBackupProtectionPolicy -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DefaultPolicy             AzureVM            Daily              26-Aug-15 12:30:00 AM
```

> [!NOTE]
> <span data-ttu-id="c5aef-154">часовой пояс Hello поля BackupTime hello в PowerShell — в формате UTC.</span><span class="sxs-lookup"><span data-stu-id="c5aef-154">hello timezone of hello BackupTime field in PowerShell is UTC.</span></span> <span data-ttu-id="c5aef-155">Тем не менее при отображении hello время резервного копирования в hello портал Azure, часовой пояс hello является выровненных tooyour local system вместе со смещением hello UTC.</span><span class="sxs-lookup"><span data-stu-id="c5aef-155">However, when hello backup time is shown in hello Azure portal, hello timezone is aligned tooyour local system along with hello UTC offset.</span></span>
>
>

<span data-ttu-id="c5aef-156">Политика резервного копирования связана по крайней мере с одной политикой хранения.</span><span class="sxs-lookup"><span data-stu-id="c5aef-156">A backup policy is associated with at least one retention policy.</span></span> <span data-ttu-id="c5aef-157">Политика хранения Hello определяет, как долго точки восстановления хранится в службе архивации Azure.</span><span class="sxs-lookup"><span data-stu-id="c5aef-157">hello retention policy defines how long a recovery point is kept with Azure Backup.</span></span> <span data-ttu-id="c5aef-158">Hello **New AzureRmBackupRetentionPolicy** командлет создает объекты PowerShell, которые содержат сведения о политике хранения.</span><span class="sxs-lookup"><span data-stu-id="c5aef-158">hello **New-AzureRmBackupRetentionPolicy** cmdlet creates PowerShell objects that hold retention policy information.</span></span> <span data-ttu-id="c5aef-159">Эти объекты политики хранения используются как входные данные toohello *New AzureRmBackupProtectionPolicy* командлета, или непосредственно с hello *Enable AzureRmBackupProtection* командлета.</span><span class="sxs-lookup"><span data-stu-id="c5aef-159">These retention policy objects are used as inputs toohello *New-AzureRmBackupProtectionPolicy* cmdlet, or directly with hello *Enable-AzureRmBackupProtection* cmdlet.</span></span>

<span data-ttu-id="c5aef-160">Политики резервного копирования определяет, когда и как часто hello выполняется резервное копирование элемента.</span><span class="sxs-lookup"><span data-stu-id="c5aef-160">A backup policy defines when and how often hello backup of an item is done.</span></span> <span data-ttu-id="c5aef-161">Hello **New AzureRmBackupProtectionPolicy** командлет создает объект PowerShell, который содержит сведения о политике резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="c5aef-161">hello **New-AzureRmBackupProtectionPolicy** cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="c5aef-162">Hello политику резервного копирования используется в качестве входного toohello *Enable AzureRmBackupProtection* командлета.</span><span class="sxs-lookup"><span data-stu-id="c5aef-162">hello backup policy is used as an input toohello *Enable-AzureRmBackupProtection* cmdlet.</span></span>

```
PS C:\> $Daily = New-AzureRmBackupRetentionPolicyObject -DailyRetention -Retention 30
PS C:\> $newpolicy = New-AzureRmBackupProtectionPolicy -Name DailyBackup01 -Type AzureVM -Daily -BackupTime ([datetime]"3:30 PM") -RetentionPolicy $Daily -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DailyBackup01             AzureVM            Daily              01-Sep-15 3:30:00 PM
```

### <a name="enable-protection"></a><span data-ttu-id="c5aef-163">Включить защиту</span><span class="sxs-lookup"><span data-stu-id="c5aef-163">Enable protection</span></span>
<span data-ttu-id="c5aef-164">Включение защиты включает в себя два объекта - hello элемента и hello политики и оба toohello toobelong необходимость же хранилища.</span><span class="sxs-lookup"><span data-stu-id="c5aef-164">Enabling protection involves two objects - hello Item and hello Policy, and both need toobelong toohello same vault.</span></span> <span data-ttu-id="c5aef-165">После hello политики связан с элементом hello, рабочий процесс резервного копирования hello включится на определенное расписание hello.</span><span class="sxs-lookup"><span data-stu-id="c5aef-165">Once hello policy has been associated with hello item, hello backup workflow will kick in at hello defined schedule.</span></span>

```
PS C:\> Get-AzureRmBackupContainer -Type AzureVM -Status Registered -Vault $backupvault | Get-AzureRmBackupItem | Enable-AzureRmBackupProtection -Policy $newpolicy
```

### <a name="initial-backup"></a><span data-ttu-id="c5aef-166">Начальное резервное копирование</span><span class="sxs-lookup"><span data-stu-id="c5aef-166">Initial backup</span></span>
<span data-ttu-id="c5aef-167">расписание резервного копирования Hello позаботится сделать hello полной первоначальной копии элемента hello и добавочного копирования hello для hello последующие резервные копии.</span><span class="sxs-lookup"><span data-stu-id="c5aef-167">hello backup schedule will take care of doing hello full initial copy for hello item and hello incremental copy for hello subsequent backups.</span></span> <span data-ttu-id="c5aef-168">Однако если требуется tooforce hello начальной резервной копии toohappen в определенное время или даже немедленно используйте hello **AzureRmBackupItem резервного копирования** командлета:</span><span class="sxs-lookup"><span data-stu-id="c5aef-168">However, if you want tooforce hello initial backup toohappen at a certain time or even immediately then use hello **Backup-AzureRmBackupItem** cmdlet:</span></span>

```
PS C:\> $container = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -Name "testvm"
PS C:\> $backupjob = Get-AzureRmBackupItem -Container $container | Backup-AzureRmBackupItem
PS C:\> $backupjob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

> [!NOTE]
> <span data-ttu-id="c5aef-169">Здравствуйте, часовой пояс hello StartTime и EndTime поля, показанные в PowerShell — в формате UTC.</span><span class="sxs-lookup"><span data-stu-id="c5aef-169">hello timezone of hello StartTime and EndTime fields shown in PowerShell is UTC.</span></span> <span data-ttu-id="c5aef-170">При отображении hello аналогичные сведения в hello портал Azure, часовой пояс hello то, выровненные tooyour локальные системные часы.</span><span class="sxs-lookup"><span data-stu-id="c5aef-170">However, when hello similar information is shown in hello Azure portal, hello timezone is aligned tooyour local system clock.</span></span>
>
>

### <a name="monitoring-a-backup-job"></a><span data-ttu-id="c5aef-171">Наблюдение за выполнением задания резервного копирования</span><span class="sxs-lookup"><span data-stu-id="c5aef-171">Monitoring a backup job</span></span>
<span data-ttu-id="c5aef-172">Большинство длительных операций службы архивации Azure моделируются в виде задания.</span><span class="sxs-lookup"><span data-stu-id="c5aef-172">Most long-running operations in Azure Backup are modelled as a job.</span></span> <span data-ttu-id="c5aef-173">Это позволяет легко tootrack выполняется без необходимости tookeep hello Azure откройте портал в любое время.</span><span class="sxs-lookup"><span data-stu-id="c5aef-173">This makes it easy tootrack progress without having tookeep hello Azure portal open at all times.</span></span>

<span data-ttu-id="c5aef-174">Последнее состояние tooget hello выполняющиеся задания, используйте hello **Get AzureRmBackupJob** командлета.</span><span class="sxs-lookup"><span data-stu-id="c5aef-174">tooget hello latest status of an in-progress job, use hello **Get-AzureRmBackupJob** cmdlet.</span></span>

```
PS C:\> $joblist = Get-AzureRmBackupJob -Vault $backupvault -Status InProgress
PS C:\> $joblist[0]

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

<span data-ttu-id="c5aef-175">Вместо опроса эти задания для завершения — то есть ненужные, дополнительный код - это проще hello toouse **AzureRmBackupJob ожидания** командлета.</span><span class="sxs-lookup"><span data-stu-id="c5aef-175">Instead of polling these jobs for completion - which is unnecessary, additional code - it is simpler toouse hello **Wait-AzureRmBackupJob** cmdlet.</span></span> <span data-ttu-id="c5aef-176">При использовании в скрипте hello командлет приостанавливает hello выполнения до завершения задания hello или hello указано, что достигнуто значение тайм-аута.</span><span class="sxs-lookup"><span data-stu-id="c5aef-176">When used in a script, hello cmdlet will pause hello execution until either hello job completes or hello specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmBackupJob -Job $joblist[0] -Timeout 43200
```


## <a name="restore-an-azure-vm"></a><span data-ttu-id="c5aef-177">Восстановление виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="c5aef-177">Restore an Azure VM</span></span>
<span data-ttu-id="c5aef-178">В порядке toorestore резервных копий данных необходимо tooidentify hello архивных элементов и точки восстановления hello, содержащий данные на момент hello.</span><span class="sxs-lookup"><span data-stu-id="c5aef-178">In order toorestore backup data, you need tooidentify hello backed-up Item and hello Recovery Point that holds hello point-in-time data.</span></span> <span data-ttu-id="c5aef-179">Эта информация является tooinitiate командлет предоставленного toohello восстановление AzureRmBackupItem восстановления данных из учетной записи клиента toohello hello хранилища.</span><span class="sxs-lookup"><span data-stu-id="c5aef-179">This information is supplied toohello Restore-AzureRmBackupItem cmdlet tooinitiate a restore of data from hello vault toohello customer's account.</span></span>

### <a name="select-hello-vm"></a><span data-ttu-id="c5aef-180">Выберите hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="c5aef-180">Select hello VM</span></span>
<span data-ttu-id="c5aef-181">tooget hello PowerShell объект, определяющий Здравствуйте элемент право резервного копирования, вы должны toostart из hello контейнера в хранилище hello и постепенно вниз по иерархии объектов.</span><span class="sxs-lookup"><span data-stu-id="c5aef-181">tooget hello PowerShell object that identifies hello right backup Item, you need toostart from hello Container in hello vault, and work your way down object hierarchy.</span></span> <span data-ttu-id="c5aef-182">tooselect hello контейнера, представляющий hello виртуальной Машины, используйте hello **Get AzureRmBackupContainer** командлета и передать этот toohello **Get AzureRmBackupItem** командлета.</span><span class="sxs-lookup"><span data-stu-id="c5aef-182">tooselect hello container that represents hello VM, use hello **Get-AzureRmBackupContainer** cmdlet and pipe that toohello **Get-AzureRmBackupItem** cmdlet.</span></span>

```
PS C:\> $backupitem = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -name "testvm" | Get-AzureRmBackupItem
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="c5aef-183">Выбор точки восстановления</span><span class="sxs-lookup"><span data-stu-id="c5aef-183">Choose a recovery point</span></span>
<span data-ttu-id="c5aef-184">Теперь можно получить список всех точек восстановления hello hello резервное копирование элемента с помощью hello **Get AzureRmBackupRecoveryPoint** командлет и выберите toorestore точки восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="c5aef-184">You can now list all hello recovery points for hello backup item using hello **Get-AzureRmBackupRecoveryPoint** cmdlet, and choose hello recovery point toorestore.</span></span> <span data-ttu-id="c5aef-185">Обычно пользователи выбирается hello последней *AppConsistent* указывают в списке hello.</span><span class="sxs-lookup"><span data-stu-id="c5aef-185">Typically users pick hello most recent *AppConsistent* point in hello list.</span></span>

```
PS C:\> $rp =  Get-AzureRmBackupRecoveryPoint -Item $backupitem
PS C:\> $rp

RecoveryPointId    RecoveryPointType  RecoveryPointTime      ContainerName
---------------    -----------------  -----------------      -------------
15273496567119     AppConsistent      01-Sep-15 12:27:38 PM  iaasvmcontainer;testvm;testv...
```

<span data-ttu-id="c5aef-186">переменная приветствия ```$rp``` является массивом точек восстановления для hello выбран элемент резервного копирования, сортируются в обратном порядке времени — hello последняя точка восстановления находится по индексу 0.</span><span class="sxs-lookup"><span data-stu-id="c5aef-186">hello variable ```$rp``` is an array of recovery points for hello selected backup item, sorted in reverse order of time - hello latest recovery point is at index 0.</span></span> <span data-ttu-id="c5aef-187">Используйте обычный массив PowerShell индексирования точки восстановления toopick hello.</span><span class="sxs-lookup"><span data-stu-id="c5aef-187">Use standard PowerShell array indexing toopick hello recovery point.</span></span> <span data-ttu-id="c5aef-188">Например: ```$rp[0]``` выберет hello последней точки восстановления.</span><span class="sxs-lookup"><span data-stu-id="c5aef-188">For example: ```$rp[0]``` will select hello latest recovery point.</span></span>

### <a name="restoring-disks"></a><span data-ttu-id="c5aef-189">Восстановление дисков</span><span class="sxs-lookup"><span data-stu-id="c5aef-189">Restoring disks</span></span>
<span data-ttu-id="c5aef-190">Отсутствует ключевое различие между операциями восстановления hello сделать hello портал Azure и Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c5aef-190">There is a key difference between hello restore operations done through hello Azure portal and through Azure PowerShell.</span></span> <span data-ttu-id="c5aef-191">С помощью PowerShell операция восстановления hello останавливается на восстановление из точки восстановления hello hello диски и сведения о конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c5aef-191">With PowerShell, hello restore operation stops at restoring hello disks and config information from hello recovery point.</span></span> <span data-ttu-id="c5aef-192">Она не создает виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="c5aef-192">It does not create a virtual machine.</span></span>

> [!WARNING]
> <span data-ttu-id="c5aef-193">Hello AzureRmBackupItem восстановления не создает виртуальную Машину.</span><span class="sxs-lookup"><span data-stu-id="c5aef-193">hello Restore-AzureRmBackupItem does not create a VM.</span></span> <span data-ttu-id="c5aef-194">Восстанавливает только диски hello toohello указана учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="c5aef-194">It only restores hello disks toohello specified storage account.</span></span> <span data-ttu-id="c5aef-195">Это не является hello такое же поведение, будет наблюдаться в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c5aef-195">This is not hello same behavior you will experience in hello Azure portal.</span></span>
>
>

```
PS C:\> $restorejob = Restore-AzureRmBackupItem -StorageAccountName "DestAccount" -RecoveryPoint $rp[0]
PS C:\> $restorejob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Restore         InProgress      01-Sep-15 1:14:01 PM   01-Jan-01 12:00:00 AM
```

<span data-ttu-id="c5aef-196">Можно получить сведения hello hello операции восстановления, используя hello **Get AzureRmBackupJobDetails** командлета, после завершения задания восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="c5aef-196">You can get hello details of hello restore operation using hello **Get-AzureRmBackupJobDetails** cmdlet once hello Restore job has completed.</span></span> <span data-ttu-id="c5aef-197">Hello *ErrorDetails* свойство будет hello сведения о необходимости toorebuild hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="c5aef-197">hello *ErrorDetails* property will have hello information needed toorebuild hello VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmBackupJobDetails -Job $restorejob
```

### <a name="build-hello-vm"></a><span data-ttu-id="c5aef-198">Построение hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="c5aef-198">Build hello VM</span></span>
<span data-ttu-id="c5aef-199">Построение hello виртуальной Машины из hello восстановить диски можно сделать с помощью старых командлетов Azure Service Management PowerShell hello, hello новых шаблонов диспетчера ресурсов Azure, или даже при использовании hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c5aef-199">Building hello VM out of hello restored disks can be done using hello older Azure Service Management PowerShell cmdlets, hello new Azure Resource Manager templates, or even using hello Azure portal.</span></span> <span data-ttu-id="c5aef-200">В краткий пример, будет показано, как tooget существует, с помощью командлетов для управления службой Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c5aef-200">In a quick example, we will show how tooget there using hello Azure Service Management cmdlets.</span></span>

```
$properties  = $details.Properties

$storageAccountName = $properties["Target Storage Account Name"]
$containerName = $properties["Config Blob Container Name"]
$blobName = $properties["Config Blob Name"]

$keys = Get-AzureStorageKey -StorageAccountName $storageAccountName
$storageAccountKey = $keys.Primary
$storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey


$destination_path = "C:\Users\admin\Desktop\vmconfig.xml"
Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path -Context $storageContext


$obj = [xml](((Get-Content -Path $destination_path -Encoding UniCode)).TrimEnd([char]0x00))
$pvr = $obj.PersistentVMRole
$os = $pvr.OSVirtualHardDisk
$dds = $pvr.DataVirtualHardDisks
$osDisk = Add-AzureDisk -MediaLocation $os.MediaLink -OS $os.OS -DiskName "panbhaosdisk"
$vm = New-AzureVMConfig -Name $pvr.RoleName -InstanceSize $pvr.RoleSize -DiskName $osDisk.DiskName

if (!($dds -eq $null))
{
    foreach($d in $dds.DataVirtualHardDisk)
    {
        $lun = 0
        if(!($d.Lun -eq $null))
        {
            $lun = $d.Lun
        }
        $name = "panbhadataDisk" + $lun
        Add-AzureDisk -DiskName $name -MediaLocation $d.MediaLink
        $vm | Add-AzureDataDisk -Import -DiskName $name -LUN $lun
    }
}

New-AzureVM -ServiceName "panbhasample" -Location "SouthEast Asia" -VM $vm
```

<span data-ttu-id="c5aef-201">Дополнительные сведения о том, как toobuild ВМ с hello восстановления дисков, узнайте, как hello следующие командлеты:</span><span class="sxs-lookup"><span data-stu-id="c5aef-201">For more information on how toobuild a VM from hello restored disks, read about hello following cmdlets:</span></span>

* [<span data-ttu-id="c5aef-202">Add-AzureDisk</span><span class="sxs-lookup"><span data-stu-id="c5aef-202">Add-AzureDisk</span></span>](https://msdn.microsoft.com/library/azure/dn495252.aspx)
* [<span data-ttu-id="c5aef-203">New-AzureVMConfig</span><span class="sxs-lookup"><span data-stu-id="c5aef-203">New-AzureVMConfig</span></span>](https://msdn.microsoft.com/library/azure/dn495159.aspx)
* [<span data-ttu-id="c5aef-204">New-AzureVM</span><span class="sxs-lookup"><span data-stu-id="c5aef-204">New-AzureVM</span></span>](https://msdn.microsoft.com/library/azure/dn495254.aspx)

## <a name="code-samples"></a><span data-ttu-id="c5aef-205">Примеры кода</span><span class="sxs-lookup"><span data-stu-id="c5aef-205">Code samples</span></span>
### <a name="1-get-hello-completion-status-of-job-sub-tasks"></a><span data-ttu-id="c5aef-206">1. Получить состояние завершения hello задания дополнительных задач</span><span class="sxs-lookup"><span data-stu-id="c5aef-206">1. Get hello completion status of job sub-tasks</span></span>
<span data-ttu-id="c5aef-207">состояние завершения hello tootrack отдельных вложенных задач, можно использовать hello **Get AzureRmBackupJobDetails** командлета:</span><span class="sxs-lookup"><span data-stu-id="c5aef-207">tootrack hello completion status of individual sub-tasks, you can use hello **Get-AzureRmBackupJobDetails** cmdlet:</span></span>

```
PS C:\> $details = Get-AzureRmBackupJobDetails -JobId $backupjob.InstanceId -Vault $backupvault
PS C:\> $details.SubTasks

Name                                                        Status
----                                                        ------
Take Snapshot                                               Completed
Transfer data tooBackup vault                               InProgress
```

### <a name="2-create-a-dailyweekly-report-of-backup-jobs"></a><span data-ttu-id="c5aef-208">2. Создание ежедневного или еженедельного отчета для задач резервного копирования</span><span class="sxs-lookup"><span data-stu-id="c5aef-208">2. Create a daily/weekly report of backup jobs</span></span>
<span data-ttu-id="c5aef-209">Администраторы обычно требуется, какие задания резервного копирования выполнялись в hello последние 24 часа, tooknow hello состояние этих заданий резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="c5aef-209">Administrators typically want tooknow what backup jobs ran in hello last 24 hours, hello status of those backup jobs.</span></span> <span data-ttu-id="c5aef-210">Кроме того, hello объем передаваемых данных позволяет администраторам tooestimate способ их ежемесячное использование данных.</span><span class="sxs-lookup"><span data-stu-id="c5aef-210">Additionally, hello amount of data transferred gives administrators a way tooestimate their monthly data usage.</span></span> <span data-ttu-id="c5aef-211">Приведенный ниже сценарий Hello hello необработанные данные извлекаются из службы архивации Azure hello и отображает hello сведения в консоли PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="c5aef-211">hello script below pulls hello raw data from hello Azure Backup service and displays hello information in hello PowerShell console.</span></span>

```
param(  [Parameter(Mandatory=$True,Position=1)]
        [string]$backupvaultname,

        [Parameter(Mandatory=$False,Position=2)]
        [int]$numberofdays = 7)


#Initialize variables
$DAILYBACKUPSTATS = @()
$backupvault = Get-AzureRmBackupVault -Name $backupvaultname
$enddate = ([datetime]::Today).AddDays(1)
$startdate = ([datetime]::Today)

for( $i = 1; $i -le $numberofdays; $i++ )
{
    # We query one day at a time because pulling 7 days of data might be too much
    $dailyjoblist = Get-AzureRmBackupJob -Vault $backupvault -From $startdate -too$enddate -Type AzureVM -Operation Backup
    Write-Progress -Activity "Getting job information for hello last $numberofdays days" -Status "Day -$i" -PercentComplete ([int]([decimal]$i*100/$numberofdays))

    foreach( $job in $dailyjoblist )
    {
        #Extract hello information for hello reports
        $newstatsobj = New-Object System.Object
        $newstatsobj | Add-Member -Type NoteProperty -Name Date -Value $startdate
        $newstatsobj | Add-Member -Type NoteProperty -Name VMName -Value $job.WorkloadName
        $newstatsobj | Add-Member -Type NoteProperty -Name Duration -Value $job.Duration
        $newstatsobj | Add-Member -Type NoteProperty -Name Status -Value $job.Status

        $details = Get-AzureRmBackupJobDetails -Job $job
        $newstatsobj | Add-Member -Type NoteProperty -Name BackupSize -Value $details.Properties["Backup Size"]
        $DAILYBACKUPSTATS += $newstatsobj
    }

    $enddate = $enddate.AddDays(-1)
    $startdate = $startdate.AddDays(-1)
}

$DAILYBACKUPSTATS | Out-GridView
```

<span data-ttu-id="c5aef-212">Tooadd построения диаграмм возможности вывода отчета toothis следует узнать из блога TechNet hello [построения диаграмм с помощью PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)</span><span class="sxs-lookup"><span data-stu-id="c5aef-212">If you want tooadd charting capabilities toothis report output, learn from hello TechNet blog post [Charting with PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5aef-213">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c5aef-213">Next steps</span></span>
<span data-ttu-id="c5aef-214">Если вы предпочитаете PowerShell tooengage с ресурсами Azure, ознакомиться с hello статье PowerShell для защиты Windows Server [развертывание и управление резервного копирования для Windows Server](backup-client-automation-classic.md).</span><span class="sxs-lookup"><span data-stu-id="c5aef-214">If you prefer using PowerShell tooengage with your Azure resources, check out hello PowerShell article for protecting Windows Server, [Deploy and Manage Backup for Windows Server](backup-client-automation-classic.md).</span></span> <span data-ttu-id="c5aef-215">Доступна и другая статья, посвященная тому, как использовать PowerShell для управления службой архивации DPM: [Развертывание службы архивации для DPM и управление ею](backup-dpm-automation-classic.md).</span><span class="sxs-lookup"><span data-stu-id="c5aef-215">There is also a PowerShell article for managing DPM backups, [Deploy and Manage Backup for DPM](backup-dpm-automation-classic.md).</span></span> <span data-ttu-id="c5aef-216">Обе эти статьи имеют две версии — для развертывания с помощью Resource Manager и для классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="c5aef-216">Both of these articles have a version for Resource Manager deployments as well as Classic deployments.</span></span>
