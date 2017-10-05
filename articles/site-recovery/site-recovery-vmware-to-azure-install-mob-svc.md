---
title: "Установка службы Mobility Service (из виртуальных машин VMware или физических серверов в Azure) | Документация Майкрософт"
description: "Узнайте, как установить агент службы Mobility Service для защиты локальных компьютеров."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 848284f37ae2470a169d8f8a8c9c0bb5b926abe3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="install-mobility-service-vmware-or-physical-to-azure"></a><span data-ttu-id="2955c-103">Установка службы Mobility Service (из виртуальных машин VMware или физических серверов в Azure)</span><span class="sxs-lookup"><span data-stu-id="2955c-103">Install Mobility Service (VMware or physical to Azure)</span></span>
<span data-ttu-id="2955c-104">Служба Mobility Service Azure Site Recovery фиксирует операции записи данных, выполняемые на компьютере, и передает их на сервер обработки.</span><span class="sxs-lookup"><span data-stu-id="2955c-104">Azure Site Recovery Mobility Service captures data writes on a computer, and then forwards them to the process server.</span></span> <span data-ttu-id="2955c-105">Разверните службу Mobility Service на каждом компьютере (виртуальная машина или физический сервер VMware), который требуется реплицировать в Azure.</span><span class="sxs-lookup"><span data-stu-id="2955c-105">Deploy Mobility Service to every computer (VMware VM or physical server) that you want to replicate to Azure.</span></span> <span data-ttu-id="2955c-106">Службы Mobility Service можно развернуть на серверах, которые необходимо защитить, следующими способами:</span><span class="sxs-lookup"><span data-stu-id="2955c-106">You can deploy Mobility Service to the servers that you want to protect by using the following methods:</span></span>


* <span data-ttu-id="2955c-107">[Установка с помощью инструментов развертывания программного обеспечения, таких как System Center Configuration Manager](site-recovery-install-mobility-service-using-sccm.md).</span><span class="sxs-lookup"><span data-stu-id="2955c-107">[Install Mobility Service by using software deployment tools like System Center Configuration Manager](site-recovery-install-mobility-service-using-sccm.md)</span></span>
* <span data-ttu-id="2955c-108">[Установка с помощью службы автоматизации Azure и настройки требуемого состояния (DSC службы автоматизации)](site-recovery-automate-mobility-service-install.md).</span><span class="sxs-lookup"><span data-stu-id="2955c-108">[Install Mobility Service by using Azure Automation and Desired State Configuration (Automation DSC)](site-recovery-automate-mobility-service-install.md)</span></span>
* <span data-ttu-id="2955c-109">[Установка вручную с помощью графического пользовательского интерфейса (GUI)](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui).</span><span class="sxs-lookup"><span data-stu-id="2955c-109">[Install Mobility Service manually by using the graphical user interface (GUI)](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)</span></span>
* <span data-ttu-id="2955c-110">[Установка Mobility Service в командной строке вручную](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span><span class="sxs-lookup"><span data-stu-id="2955c-110">[Install Mobility Service manually at a command prompt](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)</span></span>
* <span data-ttu-id="2955c-111">[Принудительная установка Mobility Service из Azure Site Recovery](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery).</span><span class="sxs-lookup"><span data-stu-id="2955c-111">[Install Mobility Service by push installation from Azure Site Recovery](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)</span></span>


>[!IMPORTANT]
> <span data-ttu-id="2955c-112">Начиная с версии 9.7.0.0, установщик службы Mobility Service также устанавливает последнюю доступную версию [агента виртуальных машин Azure](../virtual-machines/windows/extensions-features.md#azure-vm-agent) на виртуальных машинах Windows.</span><span class="sxs-lookup"><span data-stu-id="2955c-112">Beginning with version 9.7.0.0, on Windows virtual machines (VMs), the Mobility Service installer also installs the latest available [Azure VM agent](../virtual-machines/windows/extensions-features.md#azure-vm-agent).</span></span> <span data-ttu-id="2955c-113">Если при отработке отказа компьютер переходит в Azure, выполняется предварительное требование агента, связанное с использованием любого расширения виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="2955c-113">When a computer fails over to Azure, the computer meets the agent installation prerequisite for using any VM extension.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2955c-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2955c-114">Prerequisites</span></span>
<span data-ttu-id="2955c-115">Перед установкой службы Mobility Service вручную на сервере выполните следующие обязательные действия:</span><span class="sxs-lookup"><span data-stu-id="2955c-115">Complete these prerequisite steps before you manually install Mobility Service on your server:</span></span>
1. <span data-ttu-id="2955c-116">Войдите на сервер конфигурации и откройте окно командной строки с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="2955c-116">Sign in to your configuration server, and then open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="2955c-117">Измените каталог на папку bin и создайте файл с парольной фразой.</span><span class="sxs-lookup"><span data-stu-id="2955c-117">Change the directory to the bin folder, and then create a passphrase file:</span></span>

    ```
    cd %ProgramData%\ASR\home\svsystems\bin
    genpassphrase.exe -v > MobSvc.passphrase
    ```
3. <span data-ttu-id="2955c-118">Сохраните файл парольной фразы в безопасном месте.</span><span class="sxs-lookup"><span data-stu-id="2955c-118">Store the passphrase file in a secure location.</span></span> <span data-ttu-id="2955c-119">Используйте файл во время установки службы Mobility Service.</span><span class="sxs-lookup"><span data-stu-id="2955c-119">You use the file during the Mobility Service installation.</span></span>
4. <span data-ttu-id="2955c-120">Установщики службы Mobility Service для всех поддерживаемых операционных систем находятся в папке %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository.</span><span class="sxs-lookup"><span data-stu-id="2955c-120">Mobility Service installers for all supported operating systems are in the %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository folder.</span></span>

### <a name="mobility-service-installer-to-operating-system-mapping"></a><span data-ttu-id="2955c-121">Сопоставление установщика Mobility Service с операционной системой</span><span class="sxs-lookup"><span data-stu-id="2955c-121">Mobility Service installer-to-operating system mapping</span></span>

| <span data-ttu-id="2955c-122">Имя шаблона файла установщика</span><span class="sxs-lookup"><span data-stu-id="2955c-122">Installer file template name</span></span>| <span data-ttu-id="2955c-123">операционная система</span><span class="sxs-lookup"><span data-stu-id="2955c-123">Operating system</span></span> |
|---|--|
|<span data-ttu-id="2955c-124">Microsoft-ASR\_UA\*Windows\*release.exe</span><span class="sxs-lookup"><span data-stu-id="2955c-124">Microsoft-ASR\_UA\*Windows\*release.exe</span></span> | <span data-ttu-id="2955c-125">Windows Server 2008 R2 с пакетом обновления 1 (64-разрядная версия)</span><span class="sxs-lookup"><span data-stu-id="2955c-125">Windows Server 2008 R2 SP1 (64-bit)</span></span> </br> <span data-ttu-id="2955c-126">Windows Server 2012 (64-разрядная версия)</span><span class="sxs-lookup"><span data-stu-id="2955c-126">Windows Server 2012 (64-bit)</span></span> </br> <span data-ttu-id="2955c-127">Windows Server 2012 R2 (64-разрядная версия)</span><span class="sxs-lookup"><span data-stu-id="2955c-127">Windows Server 2012 R2 (64-bit)</span></span> |
|<span data-ttu-id="2955c-128">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="2955c-128">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>| <span data-ttu-id="2955c-129">Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8 (только 64-разрядная версия)</span><span class="sxs-lookup"><span data-stu-id="2955c-129">Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> </br> <span data-ttu-id="2955c-130">CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (только 64-разрядная версия)</span><span class="sxs-lookup"><span data-stu-id="2955c-130">CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> |
|<span data-ttu-id="2955c-131">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="2955c-131">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span> | <span data-ttu-id="2955c-132">Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (только 64-разрядная версия)</span><span class="sxs-lookup"><span data-stu-id="2955c-132">Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (64-bit only)</span></span> </br> <span data-ttu-id="2955c-133">CentOS 7.0, 7.1, 7.2 (только 64-разрядная версия)</span><span class="sxs-lookup"><span data-stu-id="2955c-133">CentOS 7.0, 7.1, 7.2 (64-bit only)</span></span></br> <span data-ttu-id="2955c-134">CentOs 7.3 (только миграция)</span><span class="sxs-lookup"><span data-stu-id="2955c-134">CentOs 7.3 (migration only)</span></span> |
|<span data-ttu-id="2955c-135">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="2955c-135">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>| <span data-ttu-id="2955c-136">SUSE Linux Enterprise Server 11 SP3 (только 64-разрядная версия)</span><span class="sxs-lookup"><span data-stu-id="2955c-136">SUSE Linux Enterprise Server 11 SP3 (64-bit only)</span></span>|
|<span data-ttu-id="2955c-137">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="2955c-137">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>| <span data-ttu-id="2955c-138">SUSE Linux Enterprise Server 11 SP4 (только 64-разрядная версия)</span><span class="sxs-lookup"><span data-stu-id="2955c-138">SUSE Linux Enterprise Server 11 SP4 (64-bit only)</span></span>|
|<span data-ttu-id="2955c-139">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="2955c-139">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span> | <span data-ttu-id="2955c-140">Oracle Enterprise Linux 6.4, 6.5 (только 64-разрядная версия)</span><span class="sxs-lookup"><span data-stu-id="2955c-140">Oracle Enterprise Linux 6.4, 6.5 (64-bit only)</span></span>|
|<span data-ttu-id="2955c-141">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="2955c-141">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span> | <span data-ttu-id="2955c-142">Ubuntu Linux 14.04 (только 64-разрядная версия)</span><span class="sxs-lookup"><span data-stu-id="2955c-142">Ubuntu Linux 14.04 (64-bit only)</span></span>|


## <a name="install-mobility-service-manually-by-using-the-gui"></a><span data-ttu-id="2955c-143">Установка службы Mobility Service вручную с помощью графического пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="2955c-143">Install Mobility Service manually by using the GUI</span></span>

>[!IMPORTANT]
> <span data-ttu-id="2955c-144">Если вы используете **сервер конфигурации** для репликации **виртуальных машин Azure IaaS** из одной подписки (региона) Azure в другую, **воспользуйтесь методом установки с помощью командной строки**.</span><span class="sxs-lookup"><span data-stu-id="2955c-144">If you are using a **Configuration Server** to replicate **Azure IaaS virtual machines** from one Azure Subscription/Region to another then **use the Command-line based installation** method</span></span>

[!INCLUDE [site-recovery-install-mob-svc-gui](../../includes/site-recovery-install-mob-svc-gui.md)]

## <a name="install-mobility-service-manually-at-a-command-prompt"></a><span data-ttu-id="2955c-145">Установка Mobility Service в командной строке вручную</span><span class="sxs-lookup"><span data-stu-id="2955c-145">Install Mobility Service manually at a command prompt</span></span>

### <a name="command-line-installation-on-a-windows-computer"></a><span data-ttu-id="2955c-146">Установка из командной строки на компьютере с Windows</span><span class="sxs-lookup"><span data-stu-id="2955c-146">Command-line installation on a Windows computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-win-cmd](../../includes/site-recovery-install-mob-svc-win-cmd.md)]

### <a name="command-line-installation-on-a-linux-computer"></a><span data-ttu-id="2955c-147">Установка из командной строки на компьютере Linux</span><span class="sxs-lookup"><span data-stu-id="2955c-147">Command-line installation on a Linux computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-lin-cmd](../../includes/site-recovery-install-mob-svc-lin-cmd.md)]


## <a name="install-mobility-service-by-push-installation-from-azure-site-recovery"></a><span data-ttu-id="2955c-148">Принудительная установка Mobility Service из Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="2955c-148">Install Mobility Service by push installation from Azure Site Recovery</span></span>
<span data-ttu-id="2955c-149">Для принудительной установки службы Mobility Service с использованием Site Recovery все для целевых компьютеров следует выполнить следующие предварительные требования.</span><span class="sxs-lookup"><span data-stu-id="2955c-149">To do a push installation of Mobility Service by using Site Recovery, all target computers must meet the following prerequisites.</span></span>

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-win](../../includes/site-recovery-prepare-push-install-mob-svc-win.md)]

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-lin](../../includes/site-recovery-prepare-push-install-mob-svc-lin.md)]


> [!NOTE]
<span data-ttu-id="2955c-150">После установки службы Mobility Service на портале Azure нажмите кнопку **Репликация**, чтобы приступить к защите виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="2955c-150">After Mobility Service is installed, in the Azure portal, select the **Replicate** button to start protecting these VMs.</span></span>

## <a name="uninstall-mobility-service-on-a-windows-server-computer"></a><span data-ttu-id="2955c-151">Удаление Mobility Service с компьютера Windows Server</span><span class="sxs-lookup"><span data-stu-id="2955c-151">Uninstall Mobility Service on a Windows Server computer</span></span>
<span data-ttu-id="2955c-152">Воспользуйтесь одним из следующих методов для удаления службы Mobility Service на компьютере Windows Server.</span><span class="sxs-lookup"><span data-stu-id="2955c-152">Use one of the following methods to uninstall Mobility Service on a Windows Server computer.</span></span>

### <a name="uninstall-by-using-the-gui"></a><span data-ttu-id="2955c-153">Удаление с помощью графического пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="2955c-153">Uninstall by using the GUI</span></span>
1. <span data-ttu-id="2955c-154">На панели управления выберите **Программы**.</span><span class="sxs-lookup"><span data-stu-id="2955c-154">In Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="2955c-155">Выберите **Microsoft Azure Site Recovery Mobility Service / главный целевой сервер** и нажмите кнопку **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="2955c-155">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="2955c-156">Удаление из командной строки</span><span class="sxs-lookup"><span data-stu-id="2955c-156">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="2955c-157">Откройте окно командной строки с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="2955c-157">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="2955c-158">Выполните следующую команду, чтобы удалить службу Mobility Service.</span><span class="sxs-lookup"><span data-stu-id="2955c-158">To uninstall Mobility Service, run the following command:</span></span>

```
MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
```

## <a name="uninstall-mobility-service-on-a-linux-computer"></a><span data-ttu-id="2955c-159">Удаление службы Mobility на компьютере Linux</span><span class="sxs-lookup"><span data-stu-id="2955c-159">Uninstall Mobility Service on a Linux computer</span></span>
1. <span data-ttu-id="2955c-160">На сервере Linux войдите как **привилегированный** пользователь.</span><span class="sxs-lookup"><span data-stu-id="2955c-160">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="2955c-161">В разделе "Терминал" перейдите к /user/local/ASR.</span><span class="sxs-lookup"><span data-stu-id="2955c-161">In a terminal, go to /user/local/ASR.</span></span>
3. <span data-ttu-id="2955c-162">Выполните следующую команду, чтобы удалить службу Mobility Service.</span><span class="sxs-lookup"><span data-stu-id="2955c-162">To uninstall Mobility Service, run the following command:</span></span>

```
uninstall.sh -Y
```
