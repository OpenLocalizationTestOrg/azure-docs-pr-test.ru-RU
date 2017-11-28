---
title: "aaaInstall службы Mobility Service (VMware или физических tooAzure) | Документы Microsoft"
description: "Узнайте, как tooinstall hello tooprotect агент службы Mobility Service на локальных компьютерах."
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
ms.openlocfilehash: f7836e6b35d3838bae1eff927838ce4b245b9f56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-mobility-service-vmware-or-physical-tooazure"></a><span data-ttu-id="07385-103">Установка службы Mobility Service (VMware или физических tooAzure)</span><span class="sxs-lookup"><span data-stu-id="07385-103">Install Mobility Service (VMware or physical tooAzure)</span></span>
<span data-ttu-id="07385-104">Мобильность службе Azure Site Recovery захватывает записи данных на компьютере и пересылает их toohello сервер обработки.</span><span class="sxs-lookup"><span data-stu-id="07385-104">Azure Site Recovery Mobility Service captures data writes on a computer, and then forwards them toohello process server.</span></span> <span data-ttu-id="07385-105">Развертывание компьютер tooevery службы Mobility Service (виртуальной Машины VMware или физических серверов), которые должны tooreplicate tooAzure.</span><span class="sxs-lookup"><span data-stu-id="07385-105">Deploy Mobility Service tooevery computer (VMware VM or physical server) that you want tooreplicate tooAzure.</span></span> <span data-ttu-id="07385-106">Можно развернуть серверы toohello службы Mobility Service требуется tooprotect с помощью hello следующие методы:</span><span class="sxs-lookup"><span data-stu-id="07385-106">You can deploy Mobility Service toohello servers that you want tooprotect by using hello following methods:</span></span>


* <span data-ttu-id="07385-107">[Установка с помощью инструментов развертывания программного обеспечения, таких как System Center Configuration Manager](site-recovery-install-mobility-service-using-sccm.md).</span><span class="sxs-lookup"><span data-stu-id="07385-107">[Install Mobility Service by using software deployment tools like System Center Configuration Manager](site-recovery-install-mobility-service-using-sccm.md)</span></span>
* <span data-ttu-id="07385-108">[Установка с помощью службы автоматизации Azure и настройки требуемого состояния (DSC службы автоматизации)](site-recovery-automate-mobility-service-install.md).</span><span class="sxs-lookup"><span data-stu-id="07385-108">[Install Mobility Service by using Azure Automation and Desired State Configuration (Automation DSC)](site-recovery-automate-mobility-service-install.md)</span></span>
* [<span data-ttu-id="07385-109">Установка службы Mobility Service вручную с помощью hello графический интерфейс пользователя (GUI)</span><span class="sxs-lookup"><span data-stu-id="07385-109">Install Mobility Service manually by using hello graphical user interface (GUI)</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)
* <span data-ttu-id="07385-110">[Установка Mobility Service в командной строке вручную](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span><span class="sxs-lookup"><span data-stu-id="07385-110">[Install Mobility Service manually at a command prompt](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)</span></span>
* <span data-ttu-id="07385-111">[Принудительная установка Mobility Service из Azure Site Recovery](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery).</span><span class="sxs-lookup"><span data-stu-id="07385-111">[Install Mobility Service by push installation from Azure Site Recovery](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)</span></span>


>[!IMPORTANT]
> <span data-ttu-id="07385-112">Начиная с версии 9.7.0.0, на виртуальных машинах (ВМ), программу установки службы Mobility hello также устанавливает hello последние доступные [агент ВМ Azure](../virtual-machines/windows/extensions-features.md#azure-vm-agent).</span><span class="sxs-lookup"><span data-stu-id="07385-112">Beginning with version 9.7.0.0, on Windows virtual machines (VMs), hello Mobility Service installer also installs hello latest available [Azure VM agent](../virtual-machines/windows/extensions-features.md#azure-vm-agent).</span></span> <span data-ttu-id="07385-113">При сбое компьютера через tooAzure, hello компьютер соответствует необходимым компонентом для любого расширения виртуальной Машины с помощью установки агента hello.</span><span class="sxs-lookup"><span data-stu-id="07385-113">When a computer fails over tooAzure, hello computer meets hello agent installation prerequisite for using any VM extension.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07385-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="07385-114">Prerequisites</span></span>
<span data-ttu-id="07385-115">Перед установкой службы Mobility Service вручную на сервере выполните следующие обязательные действия:</span><span class="sxs-lookup"><span data-stu-id="07385-115">Complete these prerequisite steps before you manually install Mobility Service on your server:</span></span>
1. <span data-ttu-id="07385-116">Войдите в сервер tooyour конфигурации, а затем откройте окно командной строки с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="07385-116">Sign in tooyour configuration server, and then open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="07385-117">Перейдите в папку bin toohello hello каталога и создайте файл с парольной фразой:</span><span class="sxs-lookup"><span data-stu-id="07385-117">Change hello directory toohello bin folder, and then create a passphrase file:</span></span>

    ```
    cd %ProgramData%\ASR\home\svsystems\bin
    genpassphrase.exe -v > MobSvc.passphrase
    ```
3. <span data-ttu-id="07385-118">Сохраните файл hello парольную фразу в безопасном месте.</span><span class="sxs-lookup"><span data-stu-id="07385-118">Store hello passphrase file in a secure location.</span></span> <span data-ttu-id="07385-119">Файл hello используется во время установки службы Mobility hello.</span><span class="sxs-lookup"><span data-stu-id="07385-119">You use hello file during hello Mobility Service installation.</span></span>
4. <span data-ttu-id="07385-120">Мобильные службы установщики для всех поддерживаемых операционных системах, в папке %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository hello.</span><span class="sxs-lookup"><span data-stu-id="07385-120">Mobility Service installers for all supported operating systems are in hello %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository folder.</span></span>

### <a name="mobility-service-installer-to-operating-system-mapping"></a><span data-ttu-id="07385-121">Сопоставление установщика Mobility Service с операционной системой</span><span class="sxs-lookup"><span data-stu-id="07385-121">Mobility Service installer-to-operating system mapping</span></span>

| <span data-ttu-id="07385-122">Имя шаблона файла установщика</span><span class="sxs-lookup"><span data-stu-id="07385-122">Installer file template name</span></span>| <span data-ttu-id="07385-123">операционная система</span><span class="sxs-lookup"><span data-stu-id="07385-123">Operating system</span></span> |
|---|--|
|<span data-ttu-id="07385-124">Microsoft-ASR\_UA\*Windows\*release.exe</span><span class="sxs-lookup"><span data-stu-id="07385-124">Microsoft-ASR\_UA\*Windows\*release.exe</span></span> | <span data-ttu-id="07385-125">Windows Server 2008 R2 с пакетом обновления 1 (64-разрядная версия)</span><span class="sxs-lookup"><span data-stu-id="07385-125">Windows Server 2008 R2 SP1 (64-bit)</span></span> </br> <span data-ttu-id="07385-126">Windows Server 2012 (64-разрядная версия)</span><span class="sxs-lookup"><span data-stu-id="07385-126">Windows Server 2012 (64-bit)</span></span> </br> <span data-ttu-id="07385-127">Windows Server 2012 R2 (64-разрядная версия)</span><span class="sxs-lookup"><span data-stu-id="07385-127">Windows Server 2012 R2 (64-bit)</span></span> |
|<span data-ttu-id="07385-128">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="07385-128">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>| <span data-ttu-id="07385-129">Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8 (только 64-разрядная версия)</span><span class="sxs-lookup"><span data-stu-id="07385-129">Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> </br> <span data-ttu-id="07385-130">CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (только 64-разрядная версия)</span><span class="sxs-lookup"><span data-stu-id="07385-130">CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> |
|<span data-ttu-id="07385-131">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="07385-131">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span> | <span data-ttu-id="07385-132">Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (только 64-разрядная версия)</span><span class="sxs-lookup"><span data-stu-id="07385-132">Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (64-bit only)</span></span> </br> <span data-ttu-id="07385-133">CentOS 7.0, 7.1, 7.2 (только 64-разрядная версия)</span><span class="sxs-lookup"><span data-stu-id="07385-133">CentOS 7.0, 7.1, 7.2 (64-bit only)</span></span></br> <span data-ttu-id="07385-134">CentOs 7.3 (только миграция)</span><span class="sxs-lookup"><span data-stu-id="07385-134">CentOs 7.3 (migration only)</span></span> |
|<span data-ttu-id="07385-135">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="07385-135">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>| <span data-ttu-id="07385-136">SUSE Linux Enterprise Server 11 SP3 (только 64-разрядная версия)</span><span class="sxs-lookup"><span data-stu-id="07385-136">SUSE Linux Enterprise Server 11 SP3 (64-bit only)</span></span>|
|<span data-ttu-id="07385-137">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="07385-137">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>| <span data-ttu-id="07385-138">SUSE Linux Enterprise Server 11 SP4 (только 64-разрядная версия)</span><span class="sxs-lookup"><span data-stu-id="07385-138">SUSE Linux Enterprise Server 11 SP4 (64-bit only)</span></span>|
|<span data-ttu-id="07385-139">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="07385-139">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span> | <span data-ttu-id="07385-140">Oracle Enterprise Linux 6.4, 6.5 (только 64-разрядная версия)</span><span class="sxs-lookup"><span data-stu-id="07385-140">Oracle Enterprise Linux 6.4, 6.5 (64-bit only)</span></span>|
|<span data-ttu-id="07385-141">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="07385-141">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span> | <span data-ttu-id="07385-142">Ubuntu Linux 14.04 (только 64-разрядная версия)</span><span class="sxs-lookup"><span data-stu-id="07385-142">Ubuntu Linux 14.04 (64-bit only)</span></span>|


## <a name="install-mobility-service-manually-by-using-hello-gui"></a><span data-ttu-id="07385-143">Установка службы Mobility Service вручную с помощью графического интерфейса пользователя hello</span><span class="sxs-lookup"><span data-stu-id="07385-143">Install Mobility Service manually by using hello GUI</span></span>

>[!IMPORTANT]
> <span data-ttu-id="07385-144">Если вы используете **сервер конфигурации** tooreplicate **виртуальные машины Azure IaaS** из одной подписки Azure или регион tooanother, затем **использовать установки из командной строки на основе hello**  метод</span><span class="sxs-lookup"><span data-stu-id="07385-144">If you are using a **Configuration Server** tooreplicate **Azure IaaS virtual machines** from one Azure Subscription/Region tooanother then **use hello Command-line based installation** method</span></span>

[!INCLUDE [site-recovery-install-mob-svc-gui](../../includes/site-recovery-install-mob-svc-gui.md)]

## <a name="install-mobility-service-manually-at-a-command-prompt"></a><span data-ttu-id="07385-145">Установка Mobility Service в командной строке вручную</span><span class="sxs-lookup"><span data-stu-id="07385-145">Install Mobility Service manually at a command prompt</span></span>

### <a name="command-line-installation-on-a-windows-computer"></a><span data-ttu-id="07385-146">Установка из командной строки на компьютере с Windows</span><span class="sxs-lookup"><span data-stu-id="07385-146">Command-line installation on a Windows computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-win-cmd](../../includes/site-recovery-install-mob-svc-win-cmd.md)]

### <a name="command-line-installation-on-a-linux-computer"></a><span data-ttu-id="07385-147">Установка из командной строки на компьютере Linux</span><span class="sxs-lookup"><span data-stu-id="07385-147">Command-line installation on a Linux computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-lin-cmd](../../includes/site-recovery-install-mob-svc-lin-cmd.md)]


## <a name="install-mobility-service-by-push-installation-from-azure-site-recovery"></a><span data-ttu-id="07385-148">Принудительная установка Mobility Service из Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="07385-148">Install Mobility Service by push installation from Azure Site Recovery</span></span>
<span data-ttu-id="07385-149">toodo принудительной установки службы Mobility Service с помощью Site Recovery, все целевые компьютеры должны удовлетворять hello следующие необходимые условия.</span><span class="sxs-lookup"><span data-stu-id="07385-149">toodo a push installation of Mobility Service by using Site Recovery, all target computers must meet hello following prerequisites.</span></span>

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-win](../../includes/site-recovery-prepare-push-install-mob-svc-win.md)]

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-lin](../../includes/site-recovery-prepare-push-install-mob-svc-lin.md)]


> [!NOTE]
<span data-ttu-id="07385-150">После установки службы Mobility Service в hello портал Azure, выберите hello **реплицировать** toostart кнопку Защита этих виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="07385-150">After Mobility Service is installed, in hello Azure portal, select hello **Replicate** button toostart protecting these VMs.</span></span>

## <a name="uninstall-mobility-service-on-a-windows-server-computer"></a><span data-ttu-id="07385-151">Удаление Mobility Service с компьютера Windows Server</span><span class="sxs-lookup"><span data-stu-id="07385-151">Uninstall Mobility Service on a Windows Server computer</span></span>
<span data-ttu-id="07385-152">Используйте одну из hello следующие методы toouninstall службы Mobility Service на компьютере Windows Server.</span><span class="sxs-lookup"><span data-stu-id="07385-152">Use one of hello following methods toouninstall Mobility Service on a Windows Server computer.</span></span>

### <a name="uninstall-by-using-hello-gui"></a><span data-ttu-id="07385-153">Удаление с помощью графического интерфейса пользователя hello</span><span class="sxs-lookup"><span data-stu-id="07385-153">Uninstall by using hello GUI</span></span>
1. <span data-ttu-id="07385-154">На панели управления выберите **Программы**.</span><span class="sxs-lookup"><span data-stu-id="07385-154">In Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="07385-155">Выберите **Microsoft Azure Site Recovery Mobility Service / главный целевой сервер** и нажмите кнопку **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="07385-155">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="07385-156">Удаление из командной строки</span><span class="sxs-lookup"><span data-stu-id="07385-156">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="07385-157">Откройте окно командной строки с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="07385-157">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="07385-158">toouninstall службы Mobility Service, запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="07385-158">toouninstall Mobility Service, run hello following command:</span></span>

```
MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
```

## <a name="uninstall-mobility-service-on-a-linux-computer"></a><span data-ttu-id="07385-159">Удаление службы Mobility на компьютере Linux</span><span class="sxs-lookup"><span data-stu-id="07385-159">Uninstall Mobility Service on a Linux computer</span></span>
1. <span data-ttu-id="07385-160">На сервере Linux войдите как **привилегированный** пользователь.</span><span class="sxs-lookup"><span data-stu-id="07385-160">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="07385-161">В конечном перейдите слишком/пользователя/локальной/ASR.</span><span class="sxs-lookup"><span data-stu-id="07385-161">In a terminal, go too/user/local/ASR.</span></span>
3. <span data-ttu-id="07385-162">toouninstall службы Mobility Service, запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="07385-162">toouninstall Mobility Service, run hello following command:</span></span>

```
uninstall.sh -Y
```
