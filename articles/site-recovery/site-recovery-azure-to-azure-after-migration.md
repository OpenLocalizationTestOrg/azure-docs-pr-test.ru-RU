---
title: "tooset машины aaaPrepare настройки аварийного восстановления между регионами Azure после миграции tooAzure с помощью Site Recovery | Документы Microsoft"
description: "В этой статье описывается, как tooprepare машины tooset настройки аварийного восстановления между регионами Azure после миграции tooAzure с помощью Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: ponatara
ms.openlocfilehash: b6274e3df210c1d8a7b8289cc85868ee6414e523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-tooanother-region-after-migration-tooazure-by-using-azure-site-recovery"></a><span data-ttu-id="478cd-103">Реплицировать виртуальные машины Azure tooanother области после миграции tooAzure с помощью Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="478cd-103">Replicate Azure VMs tooanother region after migration tooAzure by using Azure Site Recovery</span></span>

>[!NOTE]
> <span data-ttu-id="478cd-104">Репликация Azure Site Recovery для виртуальных машин Azure сейчас доступна в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="478cd-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

## <a name="overview"></a><span data-ttu-id="478cd-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="478cd-105">Overview</span></span>

<span data-ttu-id="478cd-106">Эта статья поможет вам подготовить виртуальные машины Azure для репликации между двумя регионах Azure, после завершения переноса из локальной среды tooAzure этих компьютеров с помощью Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="478cd-106">This article helps you prepare Azure virtual machines for replication between two Azure regions after these machines have been migrated from an on-premises environment tooAzure by using Azure Site Recovery.</span></span>

## <a name="disaster-recovery-and-compliance"></a><span data-ttu-id="478cd-107">Аварийное восстановление и соответствие</span><span class="sxs-lookup"><span data-stu-id="478cd-107">Disaster recovery and compliance</span></span>
<span data-ttu-id="478cd-108">В настоящее время больше и больше предприятий перемещение их tooAzure рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="478cd-108">Today, more and more enterprises are moving their workloads tooAzure.</span></span> <span data-ttu-id="478cd-109">С предприятий перемещение критически важных в локальной рабочей tooAzure рабочих нагрузок, Настройка аварийного восстановления для этих рабочих нагрузок является обязательным для обеспечения соответствия и toosafeguard от перерывов в регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="478cd-109">With enterprises moving mission-critical on-premises production workloads tooAzure, setting up disaster recovery for these workloads is mandatory for compliance and toosafeguard against any disruptions in an Azure region.</span></span>

## <a name="steps-for-preparing-migrated-machines-for-replication"></a><span data-ttu-id="478cd-110">Шаги по подготовке перенесенных виртуальных машин для репликации</span><span class="sxs-lookup"><span data-stu-id="478cd-110">Steps for preparing migrated machines for replication</span></span>
<span data-ttu-id="478cd-111">tooprepare перенести машины для настройки репликации tooanother регион Azure.</span><span class="sxs-lookup"><span data-stu-id="478cd-111">tooprepare migrated machines for setting up replication tooanother Azure region:</span></span>

1. <span data-ttu-id="478cd-112">Завершите миграцию.</span><span class="sxs-lookup"><span data-stu-id="478cd-112">Complete migration.</span></span>
2. <span data-ttu-id="478cd-113">Установите агент Azure, при необходимости hello.</span><span class="sxs-lookup"><span data-stu-id="478cd-113">Install hello Azure agent if needed.</span></span>
3. <span data-ttu-id="478cd-114">Удалите службу Mobility hello.</span><span class="sxs-lookup"><span data-stu-id="478cd-114">Remove hello Mobility service.</span></span>  
4. <span data-ttu-id="478cd-115">Перезапустите hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="478cd-115">Restart hello VM.</span></span>

<span data-ttu-id="478cd-116">Эти действия описаны более подробно в следующих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="478cd-116">These steps are described in more detail in hello following sections.</span></span>

### <a name="step-1-migrate-workloads-running-on-hyper-v-vms-vmware-vms-and-physical-servers-toorun-on-azure-vms"></a><span data-ttu-id="478cd-117">Шаг 1: Перенос рабочих нагрузок на виртуальных машин Hyper-V, виртуальных машин VMware и физических серверов toorun на виртуальных машинах Azure</span><span class="sxs-lookup"><span data-stu-id="478cd-117">Step 1: Migrate workloads running on Hyper-V VMs, VMware VMs, and physical servers toorun on Azure VMs</span></span>

<span data-ttu-id="478cd-118">tooset Настройка репликации и перенести вашей локальной Hyper-V, VMware и физических рабочих нагрузок tooAzure, приведенным ниже инструкциям hello в hello [Azure IaaS перенос виртуальных машин между регионами Azure с помощью Azure Site Recovery](site-recovery-migrate-to-azure.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="478cd-118">tooset up replication and migrate your on-premises Hyper-V, VMware, and physical workloads tooAzure, follow hello steps in hello [Migrate Azure IaaS virtual machines between Azure regions with Azure Site Recovery](site-recovery-migrate-to-azure.md) article.</span></span> 

<span data-ttu-id="478cd-119">После миграции не требуется toocommit или удалить отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="478cd-119">After migration, you don't need toocommit or delete a failover.</span></span> <span data-ttu-id="478cd-120">Вместо этого выберите hello **выполнения миграции** параметр для каждого компьютера требуется toomigrate:</span><span class="sxs-lookup"><span data-stu-id="478cd-120">Instead, select hello **Complete Migration** option for each machine you want toomigrate:</span></span>
1. <span data-ttu-id="478cd-121">В **реплицируются элементы**, щелкните правой кнопкой мыши hello виртуальной Машины и нажмите кнопку **выполнения миграции**.</span><span class="sxs-lookup"><span data-stu-id="478cd-121">In **Replicated Items**, right-click hello VM, and click **Complete Migration**.</span></span> <span data-ttu-id="478cd-122">Нажмите кнопку **ОК** toocomplete hello шаг.</span><span class="sxs-lookup"><span data-stu-id="478cd-122">Click **OK** toocomplete hello step.</span></span> <span data-ttu-id="478cd-123">Вы можете отслеживать ход выполнения в свойствах виртуальной Машины hello по следящего задания выполнения миграции hello в **задания Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="478cd-123">You can track progress in hello VM properties by monitoring hello Complete Migration job in **Site Recovery jobs**.</span></span>
2. <span data-ttu-id="478cd-124">Hello **выполнения миграции** действие завершения процесса миграции hello, удаляет репликацию для машины hello и приостанавливает выставление счетов Site Recovery для машины hello.</span><span class="sxs-lookup"><span data-stu-id="478cd-124">hello **Complete Migration** action completes hello migration process, removes replication for hello machine, and stops Site Recovery billing for hello machine.</span></span>

   ![completemigration](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

### <a name="step-2-install-hello-azure-vm-agent-on-hello-virtual-machine"></a><span data-ttu-id="478cd-126">Шаг 2: Установите агент ВМ Azure hello на виртуальной машине hello</span><span class="sxs-lookup"><span data-stu-id="478cd-126">Step 2: Install hello Azure VM agent on hello virtual machine</span></span>
<span data-ttu-id="478cd-127">Hello Azure [агент виртуальной Машины](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) должны устанавливаться на виртуальной машине hello за toowork расширения hello Site Recovery и toohelp hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="478cd-127">hello Azure [VM agent](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) must be installed on hello virtual machine for hello Site Recovery extension toowork and toohelp protect hello VM.</span></span>

>[!IMPORTANT]
><span data-ttu-id="478cd-128">Начиная с версии 9.7.0.0, на виртуальных машинах Windows hello установщика службы Mobility service также устанавливает hello последние доступные агент ВМ Azure.</span><span class="sxs-lookup"><span data-stu-id="478cd-128">Beginning with version 9.7.0.0, on Windows virtual machines, hello Mobility service installer also installs hello latest available Azure VM agent.</span></span> <span data-ttu-id="478cd-129">Для миграции hello виртуальной машины соответствует необходимым компонентом для любого расширения виртуальной Машины, включая расширение hello Site Recovery с помощью установки агента.</span><span class="sxs-lookup"><span data-stu-id="478cd-129">On migration, hello virtual machine meets the agent installation prerequisite for using any VM extension, including hello Site Recovery extension.</span></span> <span data-ttu-id="478cd-130">Hello агента ВМ Azure потребностей toobe, установленные вручную только в том случае, если служба мобильности на hello hello перенесли машины — 9,6 или более ранней версии.</span><span class="sxs-lookup"><span data-stu-id="478cd-130">hello Azure VM agent needs toobe manually installed only if hello Mobility service installed on hello migrated machine is version 9.6 or earlier.</span></span>

<span data-ttu-id="478cd-131">Hello Следующая таблица предоставляет дополнительные сведения об установке агента ВМ hello и проверка того, что он был установлен:</span><span class="sxs-lookup"><span data-stu-id="478cd-131">hello following table provides additional information about installing hello VM agent and validating that it was installed:</span></span>

| <span data-ttu-id="478cd-132">**Операция**</span><span class="sxs-lookup"><span data-stu-id="478cd-132">**Operation**</span></span> | <span data-ttu-id="478cd-133">**Windows**</span><span class="sxs-lookup"><span data-stu-id="478cd-133">**Windows**</span></span> | <span data-ttu-id="478cd-134">**Linux**</span><span class="sxs-lookup"><span data-stu-id="478cd-134">**Linux**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="478cd-135">Установка агента ВМ hello</span><span class="sxs-lookup"><span data-stu-id="478cd-135">Installing hello VM agent</span></span> |<span data-ttu-id="478cd-136">Загрузите и установите hello [MSI агента](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="478cd-136">Download and install hello [agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <span data-ttu-id="478cd-137">Требуется установка hello toocomplete права администратора.</span><span class="sxs-lookup"><span data-stu-id="478cd-137">You need administrator privileges toocomplete hello installation.</span></span> |<span data-ttu-id="478cd-138">Установить последние hello [агент Linux](../virtual-machines/linux/agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="478cd-138">Install hello latest [Linux agent](../virtual-machines/linux/agent-user-guide.md).</span></span> <span data-ttu-id="478cd-139">Требуется установка hello toocomplete права администратора.</span><span class="sxs-lookup"><span data-stu-id="478cd-139">You need administrator privileges toocomplete hello installation.</span></span> <span data-ttu-id="478cd-140">Мы рекомендуем установить агент hello из репозитория распространения.</span><span class="sxs-lookup"><span data-stu-id="478cd-140">We recommend installing hello agent from your distribution repository.</span></span> <span data-ttu-id="478cd-141">Мы *не рекомендует* hello агент виртуальной Машины Linux при установке непосредственно из GitHub.</span><span class="sxs-lookup"><span data-stu-id="478cd-141">We *do not recommend* installing hello Linux VM agent directly from GitHub.</span></span>  |
| <span data-ttu-id="478cd-142">Проверка установки агента виртуальной Машины hello</span><span class="sxs-lookup"><span data-stu-id="478cd-142">Validating hello VM agent installation</span></span> |<span data-ttu-id="478cd-143">1. Обзор папки C:\WindowsAzure\Packages toohello в hello виртуальной Машине Azure.</span><span class="sxs-lookup"><span data-stu-id="478cd-143">1. Browse toohello C:\WindowsAzure\Packages folder in hello Azure VM.</span></span> <span data-ttu-id="478cd-144">Вы должны увидеть файл WaAppAgent.exe hello.</span><span class="sxs-lookup"><span data-stu-id="478cd-144">You should see hello WaAppAgent.exe file.</span></span> <br><span data-ttu-id="478cd-145">2. Правой кнопкой мыши файл hello, перейдите в слишком**свойства**и затем выберите hello **сведения** hello вкладку **версия продукта** поле должно быть 2.6.1198.718 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="478cd-145">2. Right-click hello file, go too**Properties**, and then select hello **Details** tab. hello **Product Version** field should be 2.6.1198.718 or higher.</span></span> |<span data-ttu-id="478cd-146">Недоступно</span><span class="sxs-lookup"><span data-stu-id="478cd-146">N/A</span></span> |


### <a name="step-3-remove-hello-mobility-service-from-hello-migrated-virtual-machine"></a><span data-ttu-id="478cd-147">Шаг 3: Удаление hello службы Mobility service из hello перенесенные виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="478cd-147">Step 3: Remove hello Mobility service from hello migrated virtual machine</span></span>

<span data-ttu-id="478cd-148">При переносе вашей локальной машины VMware или физических серверов в Windows и Linux необходимо toomanually/uninstall удаление hello службы Mobility service из hello перенесенной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="478cd-148">If you have migrated your on-premises VMware machines or physical servers on Windows/Linux, you need toomanually remove/uninstall hello Mobility service from hello migrated virtual machine.</span></span>

>[!IMPORTANT]
><span data-ttu-id="478cd-149">Этот шаг не является обязательным для tooAzure перенесенных виртуальных машин Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="478cd-149">This step is not required for Hyper-V VMs migrated tooAzure.</span></span>

#### <a name="uninstall-hello-mobility-service-on-a-windows-server-vm"></a><span data-ttu-id="478cd-150">Удалите hello Mobility service на виртуальной Машине Windows Server</span><span class="sxs-lookup"><span data-stu-id="478cd-150">Uninstall hello Mobility service on a Windows Server VM</span></span>
<span data-ttu-id="478cd-151">Используйте одну из hello следующие методы toouninstall hello Mobility service на компьютере Windows Server.</span><span class="sxs-lookup"><span data-stu-id="478cd-151">Use one of hello following methods toouninstall hello Mobility service on a Windows Server computer.</span></span>

##### <a name="uninstall-by-using-hello-windows-ui"></a><span data-ttu-id="478cd-152">Удаление с помощью пользовательского интерфейса Windows hello</span><span class="sxs-lookup"><span data-stu-id="478cd-152">Uninstall by using hello Windows UI</span></span>
1. <span data-ttu-id="478cd-153">В hello панели управления выберите **программы**.</span><span class="sxs-lookup"><span data-stu-id="478cd-153">In hello Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="478cd-154">Выберите **Microsoft Azure Site Recovery Mobility Service / главный целевой сервер** и нажмите кнопку **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="478cd-154">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

##### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="478cd-155">Удаление из командной строки</span><span class="sxs-lookup"><span data-stu-id="478cd-155">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="478cd-156">Откройте окно командной строки с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="478cd-156">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="478cd-157">toouninstall hello службы Mobility service, запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="478cd-157">toouninstall hello Mobility service, run hello following command:</span></span>

   ```
   MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
   ```

#### <a name="uninstall-hello-mobility-service-on-a-linux-computer"></a><span data-ttu-id="478cd-158">Удалите hello Mobility service на компьютере Linux</span><span class="sxs-lookup"><span data-stu-id="478cd-158">Uninstall hello Mobility service on a Linux computer</span></span>
1. <span data-ttu-id="478cd-159">На сервере Linux войдите как **привилегированный** пользователь.</span><span class="sxs-lookup"><span data-stu-id="478cd-159">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="478cd-160">В конечном перейдите слишком/пользователя/локальной/ASR.</span><span class="sxs-lookup"><span data-stu-id="478cd-160">In a terminal, go too/user/local/ASR.</span></span>
3. <span data-ttu-id="478cd-161">toouninstall hello службы Mobility service, запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="478cd-161">toouninstall hello Mobility service, run hello following command:</span></span>

   ```
   uninstall.sh -Y
   ```

### <a name="step-4-restart-hello-vm"></a><span data-ttu-id="478cd-162">Шаг 4: Перезапустите hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="478cd-162">Step 4: Restart hello VM</span></span>

<span data-ttu-id="478cd-163">После установки службы Mobility hello перезапуска hello виртуальной Машины, прежде чем настроить tooanother репликации регион Azure.</span><span class="sxs-lookup"><span data-stu-id="478cd-163">After you uninstall hello Mobility service, restart hello VM before you set up replication tooanother Azure region.</span></span>


## <a name="next-steps"></a><span data-ttu-id="478cd-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="478cd-164">Next steps</span></span>
- <span data-ttu-id="478cd-165">Включите защиту рабочих нагрузок, [выполнив репликацию виртуальных машин Azure](site-recovery-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="478cd-165">Start protecting your workloads by [replicating Azure virtual machines](site-recovery-azure-to-azure.md).</span></span>
- <span data-ttu-id="478cd-166">Ознакомьтесь со статьей [Руководство по организации сети для репликации виртуальных машин Azure](site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="478cd-166">Learn more about [networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
