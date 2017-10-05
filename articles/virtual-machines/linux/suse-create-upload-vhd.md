---
title: "Создание и передача виртуального жесткого диска с операционной системой SUSE Linux в Azure"
description: "Узнайте, как создать и передать виртуальный жесткий диск (VHD-файл) Azure, содержащий операционную систему SUSE Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 066d01a6-2a54-4718-bcd0-90fe7a5303a1
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: szark
ms.openlocfilehash: c829f5d9a90b4260c6f41b2d9e511a0c6cb48f18
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-a-sles-or-opensuse-virtual-machine-for-azure"></a><span data-ttu-id="26b35-103">Подготовка виртуальной машины SLES или openSUSE для Azure</span><span class="sxs-lookup"><span data-stu-id="26b35-103">Prepare a SLES or openSUSE virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="26b35-104">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="26b35-104">Prerequisites</span></span>
<span data-ttu-id="26b35-105">В этой статье предполагается, что вы уже установили операционную систему SUSE или openSUSE Linux на виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="26b35-105">This article assumes that you have already installed a SUSE or openSUSE Linux operating system to a virtual hard disk.</span></span> <span data-ttu-id="26b35-106">Существует несколько средств для создания VHD-файлов, например решение для виртуализации, такое как Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="26b35-106">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="26b35-107">Инструкции см. в разделе [Установка роли Hyper-V и настройка виртуальной машины](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="26b35-107">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="sles--opensuse-installation-notes"></a><span data-ttu-id="26b35-108">Замечания по установке SLES и openSUSE</span><span class="sxs-lookup"><span data-stu-id="26b35-108">SLES / openSUSE installation notes</span></span>
* <span data-ttu-id="26b35-109">Дополнительные сведения о подготовке Linux для Azure см. в разделе [Общие замечания по установке Linux](create-upload-generic.md#general-linux-installation-notes).</span><span class="sxs-lookup"><span data-stu-id="26b35-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="26b35-110">Формат VHDX не поддерживается в Azure, поддерживается только **фиксированный VHD**.</span><span class="sxs-lookup"><span data-stu-id="26b35-110">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="26b35-111">Можно преобразовать диск в формат VHD с помощью диспетчера Hyper-V или командлета convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="26b35-111">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span></span>
* <span data-ttu-id="26b35-112">При установке системы Linux рекомендуется использовать стандартные разделы, а не LVM (как правило, значение по умолчанию во многих дистрибутивах).</span><span class="sxs-lookup"><span data-stu-id="26b35-112">When installing the Linux system it is recommended that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="26b35-113">Это позволит избежать конфликта имен LVM при клонировании виртуальных машин, особенно если диск с OC может быть подключен к другой ВМ в целях устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="26b35-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another VM for troubleshooting.</span></span> <span data-ttu-id="26b35-114">Для дисков данных можно использовать [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) или [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="26b35-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="26b35-115">Не настраивайте раздел подкачки на диске с ОС.</span><span class="sxs-lookup"><span data-stu-id="26b35-115">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="26b35-116">Можно настроить агент Linux для создания файла подкачки на временном диске ресурсов.</span><span class="sxs-lookup"><span data-stu-id="26b35-116">The Linux agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="26b35-117">Дополнительные сведения описаны далее.</span><span class="sxs-lookup"><span data-stu-id="26b35-117">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="26b35-118">Все VHD-диски должны иметь размер, кратный 1 МБ.</span><span class="sxs-lookup"><span data-stu-id="26b35-118">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="use-suse-studio"></a><span data-ttu-id="26b35-119">Использование SUSE Studio</span><span class="sxs-lookup"><span data-stu-id="26b35-119">Use SUSE Studio</span></span>
<span data-ttu-id="26b35-120">[SUSE Studio](http://www.susestudio.com) можно с легкостью использовать для создания образов SLES и openSUSE для Azure и Hyper-V, а также для управления этими образами.</span><span class="sxs-lookup"><span data-stu-id="26b35-120">[SUSE Studio](http://www.susestudio.com) can easily create and manage your SLES and openSUSE images for Azure and Hyper-V.</span></span> <span data-ttu-id="26b35-121">Этот подход рекомендуется для настройки собственных образов SLES и openSUSE.</span><span class="sxs-lookup"><span data-stu-id="26b35-121">This is the recommended approach for customizing your own SLES and openSUSE images.</span></span>

<span data-ttu-id="26b35-122">Вместо того чтобы создать собственный виртуальный жесткий диск, SUSE публикует образы BYOS (использование собственной подписки) для SLES в каталоге [VM Depot](https://vmdepot.msopentech.com/User/Show?user=1007).</span><span class="sxs-lookup"><span data-stu-id="26b35-122">As an alternative to building your own VHD, SUSE also publishes BYOS (Bring Your Own Subscription) images for SLES at [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).</span></span>

## <a name="prepare-suse-linux-enterprise-server-11-sp4"></a><span data-ttu-id="26b35-123">Подготовка SUSE Linux Enterprise Server 11 с пакетом обновления 4 (SP4)</span><span class="sxs-lookup"><span data-stu-id="26b35-123">Prepare SUSE Linux Enterprise Server 11 SP4</span></span>
1. <span data-ttu-id="26b35-124">На центральной панели диспетчера Hyper-V выберите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="26b35-124">In the center pane of Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="26b35-125">Щелкните **Подключение** , чтобы открыть окно виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="26b35-125">Click **Connect** to open the window for the virtual machine.</span></span>
3. <span data-ttu-id="26b35-126">Зарегистрируйте систему SUSE Linux Enterprise, чтобы позволить ей скачивать обновления и устанавливать пакеты.</span><span class="sxs-lookup"><span data-stu-id="26b35-126">Register your SUSE Linux Enterprise system to allow it to download updates and install packages.</span></span>
4. <span data-ttu-id="26b35-127">Установите в системе последние исправления:</span><span class="sxs-lookup"><span data-stu-id="26b35-127">Update the system with the latest patches:</span></span>
   
        # sudo zypper update
5. <span data-ttu-id="26b35-128">Установите агент Linux для Azure из репозитория SLES:</span><span class="sxs-lookup"><span data-stu-id="26b35-128">Install the Azure Linux Agent from the SLES repository:</span></span>
   
        # sudo zypper install WALinuxAgent
6. <span data-ttu-id="26b35-129">Убедитесь, что waagent в chkconfig имеет значение on. Если указано другое значение, включите для службы waagent автоматический запуск.</span><span class="sxs-lookup"><span data-stu-id="26b35-129">Check if waagent is set to "on" in chkconfig, and if not, enable it for autostart:</span></span>
   
        # sudo chkconfig waagent on
7. <span data-ttu-id="26b35-130">Убедитесь, что служба waagent работает. Если она не работает, запустите ее:</span><span class="sxs-lookup"><span data-stu-id="26b35-130">Check if waagent service is running, and if not, start it:</span></span> 
   
        # sudo service waagent start
8. <span data-ttu-id="26b35-131">Измените строку загрузки ядра в конфигурации grub, чтобы включить дополнительные параметры ядра для Azure.</span><span class="sxs-lookup"><span data-stu-id="26b35-131">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="26b35-132">Для этого откройте файл "/boot/grub/menu.lst" в текстовом редакторе и убедитесь, что ядро по умолчанию включает следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="26b35-132">To do this open "/boot/grub/menu.lst" in a text editor and ensure that the default kernel includes the following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
   
    <span data-ttu-id="26b35-133">Это гарантирует отправку всех сообщений консоли на первый последовательный порт, что может помочь технической поддержке Azure в плане отладки.</span><span class="sxs-lookup"><span data-stu-id="26b35-133">This will ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span>
9. <span data-ttu-id="26b35-134">Убедитесь, что файлы /boot/grub/menu.lst и /etc/fstab ссылаются на диск с помощью его UUID (by-uuid), а не с помощью идентификатора диска (by-id).</span><span class="sxs-lookup"><span data-stu-id="26b35-134">Confirm that /boot/grub/menu.lst and /etc/fstab both reference the disk using its UUID (by-uuid) instead of the disk ID (by-id).</span></span> 
   
    <span data-ttu-id="26b35-135">Получение UUID диска</span><span class="sxs-lookup"><span data-stu-id="26b35-135">Get disk UUID</span></span>
   
        # ls /dev/disk/by-uuid/
   
    <span data-ttu-id="26b35-136">Если используется /dev/disk/by-id, обновите файлы /boot/grub/menu.lst и /etc/fstab правильным значением uuid.</span><span class="sxs-lookup"><span data-stu-id="26b35-136">If /dev/disk/by-id/ is used, update both /boot/grub/menu.lst and /etc/fstab with the proper by-uuid value</span></span>
   
    <span data-ttu-id="26b35-137">Перед изменением</span><span class="sxs-lookup"><span data-stu-id="26b35-137">Before change</span></span>
   
        root=/dev/disk/by-id/SCSI-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxxx-part1
   
    <span data-ttu-id="26b35-138">После изменения</span><span class="sxs-lookup"><span data-stu-id="26b35-138">After change</span></span>
   
        root=/dev/disk/by-uuid/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
10. <span data-ttu-id="26b35-139">Переместите или удалите правила udev, чтобы не создавать статические правила для интерфейса Ethernet.</span><span class="sxs-lookup"><span data-stu-id="26b35-139">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="26b35-140">Эти правила приводят к появлению проблем при клонировании виртуальной машины в Microsoft Azure или Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="26b35-140">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
    
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
11. <span data-ttu-id="26b35-141">Рекомендуется отредактировать файл /etc/sysconfig/network/dhcp и изменить параметр `DHCLIENT_SET_HOSTNAME` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="26b35-141">It is recommended to edit the file "/etc/sysconfig/network/dhcp" and change the `DHCLIENT_SET_HOSTNAME` parameter to the following:</span></span>
    
     <span data-ttu-id="26b35-142">DHCLIENT_SET_HOSTNAME="no"</span><span class="sxs-lookup"><span data-stu-id="26b35-142">DHCLIENT_SET_HOSTNAME="no"</span></span>
12. <span data-ttu-id="26b35-143">В "/etc/sudoers" закомментируйте или удалите следующие строки, если они существуют:</span><span class="sxs-lookup"><span data-stu-id="26b35-143">In "/etc/sudoers", comment out or remove the following lines if they exist:</span></span>
    
     <span data-ttu-id="26b35-144">Defaults targetpw   # ask for the password of the target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span><span class="sxs-lookup"><span data-stu-id="26b35-144">Defaults targetpw   # ask for the password of the target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span></span> <span data-ttu-id="26b35-145">Используйте только вместе с Defaults targetpw!</span><span class="sxs-lookup"><span data-stu-id="26b35-145">Only use this together with 'Defaults targetpw'!</span></span>
13. <span data-ttu-id="26b35-146">Убедитесь, что SSH-сервер установлен и настроен для включения во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="26b35-146">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="26b35-147">Обычно это сделано по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="26b35-147">This is usually the default.</span></span>
14. <span data-ttu-id="26b35-148">Не создавайте пространство подкачки на диске с ОС.</span><span class="sxs-lookup"><span data-stu-id="26b35-148">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="26b35-149">Агент Linux для Azure может автоматически настраивать пространство подкачки с использованием диска на локальном ресурсе, подключенном к виртуальной машине после подготовки для работы в среде Azure.</span><span class="sxs-lookup"><span data-stu-id="26b35-149">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="26b35-150">Следует отметить, что локальный диск ресурсов является *временным* диском и должен быть очищен при отмене подготовки виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="26b35-150">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="26b35-151">После установки агента Linux для Azure (см. предыдущий шаг) измените следующие параметры в /etc/waagent.conf соответствующим образом:</span><span class="sxs-lookup"><span data-stu-id="26b35-151">After installing the Azure Linux Agent (see previous step), modify the following parameters in /etc/waagent.conf appropriately:</span></span>
    
     <span data-ttu-id="26b35-152">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.</span><span class="sxs-lookup"><span data-stu-id="26b35-152">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.</span></span>
15. <span data-ttu-id="26b35-153">Выполните следующие команды, чтобы отменить подготовку виртуальной машины и подготовить ее в Azure:</span><span class="sxs-lookup"><span data-stu-id="26b35-153">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
    # <a name="sudo-waagent--force--deprovision"></a><span data-ttu-id="26b35-154">sudo waagent -force -deprovision</span><span class="sxs-lookup"><span data-stu-id="26b35-154">sudo waagent -force -deprovision</span></span>
    # <a name="export-histsize0"></a><span data-ttu-id="26b35-155">export HISTSIZE=0</span><span class="sxs-lookup"><span data-stu-id="26b35-155">export HISTSIZE=0</span></span>
    # <a name="logout"></a><span data-ttu-id="26b35-156">logout</span><span class="sxs-lookup"><span data-stu-id="26b35-156">logout</span></span>
16. <span data-ttu-id="26b35-157">В диспетчере Hyper-V выберите **Действие -> Завершение работы**.</span><span class="sxs-lookup"><span data-stu-id="26b35-157">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="26b35-158">Виртуальный жесткий диск Linux готов к передаче в Azure.</span><span class="sxs-lookup"><span data-stu-id="26b35-158">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

- - -
## <a name="prepare-opensuse-131"></a><span data-ttu-id="26b35-159">Подготовка openSUSE 13.1+</span><span class="sxs-lookup"><span data-stu-id="26b35-159">Prepare openSUSE 13.1+</span></span>
1. <span data-ttu-id="26b35-160">На центральной панели диспетчера Hyper-V выберите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="26b35-160">In the center pane of Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="26b35-161">Щелкните **Подключение** , чтобы открыть окно виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="26b35-161">Click **Connect** to open the window for the virtual machine.</span></span>
3. <span data-ttu-id="26b35-162">В консоли оболочки выполните команду`zypper lr`.</span><span class="sxs-lookup"><span data-stu-id="26b35-162">On the shell, run the command '`zypper lr`'.</span></span> <span data-ttu-id="26b35-163">Если эта команда возвращает результат следующего вида, то репозитории настроены надлежащим образом, и никаких изменений не требуется (обратите внимание, что номера версий могут отличаться):</span><span class="sxs-lookup"><span data-stu-id="26b35-163">If this command returns output similar to the following, then the repositories are configured as expected--no adjustments are necessary (note that version numbers may vary):</span></span>
   
        # | Alias                 | Name                  | Enabled | Refresh
        --+-----------------------+-----------------------+---------+--------
        1 | Cloud:Tools_13.1      | Cloud:Tools_13.1      | Yes     | Yes
        2 | openSUSE_13.1_OSS     | openSUSE_13.1_OSS     | Yes     | Yes
        3 | openSUSE_13.1_Updates | openSUSE_13.1_Updates | Yes     | Yes
   
    <span data-ttu-id="26b35-164">Если команда возвращает сообщение "No repositories defined..." (Репозитории не определены...), используйте следующие команды для добавления этих репозиториев:</span><span class="sxs-lookup"><span data-stu-id="26b35-164">If the command returns "No repositories defined..." then use the following commands to add these repos:</span></span>
   
        # sudo zypper ar -f http://download.opensuse.org/repositories/Cloud:Tools/openSUSE_13.1 Cloud:Tools_13.1
        # sudo zypper ar -f http://download.opensuse.org/distribution/13.1/repo/oss openSUSE_13.1_OSS
        # sudo zypper ar -f http://download.opensuse.org/update/13.1 openSUSE_13.1_Updates
   
    <span data-ttu-id="26b35-165">Чтобы убедиться, что репозитории добавлены, можно еще раз выполнить команду`zypper lr`.</span><span class="sxs-lookup"><span data-stu-id="26b35-165">You can then verify the repositories have been added by running the command '`zypper lr`' again.</span></span> <span data-ttu-id="26b35-166">Если один из соответствующих репозиториев обновлений не включен, включите его, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="26b35-166">In case one of the relevant update repositories is not enabled, enable it with following command:</span></span>
   
        # sudo zypper mr -e [NUMBER OF REPOSITORY]
4. <span data-ttu-id="26b35-167">Обновите ядро до последней доступной версии:</span><span class="sxs-lookup"><span data-stu-id="26b35-167">Update the kernel to the latest available version:</span></span>
   
        # sudo zypper up kernel-default
   
    <span data-ttu-id="26b35-168">Либо установите в системе все последние исправления:</span><span class="sxs-lookup"><span data-stu-id="26b35-168">Or to update the system with all the latest patches:</span></span>
   
        # sudo zypper update
5. <span data-ttu-id="26b35-169">Установите агент Linux для Azure.</span><span class="sxs-lookup"><span data-stu-id="26b35-169">Install the Azure Linux Agent.</span></span>
   
   # <a name="sudo-zypper-install-walinuxagent"></a><span data-ttu-id="26b35-170">sudo zypper install WALinuxAgent</span><span class="sxs-lookup"><span data-stu-id="26b35-170">sudo zypper install WALinuxAgent</span></span>
6. <span data-ttu-id="26b35-171">Измените строку загрузки ядра в конфигурации grub, чтобы включить дополнительные параметры ядра для Azure.</span><span class="sxs-lookup"><span data-stu-id="26b35-171">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="26b35-172">Для этого откройте файл /boot/grub/menu.lst в текстовом редакторе и убедитесь, что ядро по умолчанию включает следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="26b35-172">To do this, open "/boot/grub/menu.lst" in a text editor and ensure that the default kernel includes the following parameters:</span></span>
   
     <span data-ttu-id="26b35-173">console=ttyS0 earlyprintk=ttyS0 rootdelay=300</span><span class="sxs-lookup"><span data-stu-id="26b35-173">console=ttyS0 earlyprintk=ttyS0 rootdelay=300</span></span>
   
   <span data-ttu-id="26b35-174">Это гарантирует отправку всех сообщений консоли на первый последовательный порт, что может помочь технической поддержке Azure в плане отладки.</span><span class="sxs-lookup"><span data-stu-id="26b35-174">This will ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="26b35-175">Кроме того, удалите следующие параметры из строки загрузки ядра, если таковые существуют:</span><span class="sxs-lookup"><span data-stu-id="26b35-175">In addition, remove the following parameters from the kernel boot line if they exist:</span></span>
   
     <span data-ttu-id="26b35-176">libata.atapi_enabled=0 reserve=0x1f0,0x8</span><span class="sxs-lookup"><span data-stu-id="26b35-176">libata.atapi_enabled=0 reserve=0x1f0,0x8</span></span>
7. <span data-ttu-id="26b35-177">Рекомендуется отредактировать файл /etc/sysconfig/network/dhcp и изменить параметр `DHCLIENT_SET_HOSTNAME` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="26b35-177">It is recommended to edit the file "/etc/sysconfig/network/dhcp" and change the `DHCLIENT_SET_HOSTNAME` parameter to the following:</span></span>
   
     <span data-ttu-id="26b35-178">DHCLIENT_SET_HOSTNAME="no"</span><span class="sxs-lookup"><span data-stu-id="26b35-178">DHCLIENT_SET_HOSTNAME="no"</span></span>
8. <span data-ttu-id="26b35-179">**Внимание!** В файле /etc/sudoers закомментируйте или удалите следующие строки, если они существуют:</span><span class="sxs-lookup"><span data-stu-id="26b35-179">**Important:** In "/etc/sudoers", comment out or remove the following lines if they exist:</span></span>
   
     <span data-ttu-id="26b35-180">Defaults targetpw   # ask for the password of the target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span><span class="sxs-lookup"><span data-stu-id="26b35-180">Defaults targetpw   # ask for the password of the target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span></span> <span data-ttu-id="26b35-181">Используйте только вместе с Defaults targetpw!</span><span class="sxs-lookup"><span data-stu-id="26b35-181">Only use this together with 'Defaults targetpw'!</span></span>
9. <span data-ttu-id="26b35-182">Убедитесь, что SSH-сервер установлен и настроен для включения во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="26b35-182">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="26b35-183">Обычно это сделано по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="26b35-183">This is usually the default.</span></span>
10. <span data-ttu-id="26b35-184">Не создавайте пространство подкачки на диске с ОС.</span><span class="sxs-lookup"><span data-stu-id="26b35-184">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="26b35-185">Агент Linux для Azure может автоматически настраивать пространство подкачки с использованием диска на локальном ресурсе, подключенном к виртуальной машине после подготовки для работы в среде Azure.</span><span class="sxs-lookup"><span data-stu-id="26b35-185">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="26b35-186">Следует отметить, что локальный диск ресурсов является *временным* диском и должен быть очищен при отмене подготовки виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="26b35-186">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="26b35-187">После установки агента Linux для Azure (см. предыдущий шаг) измените следующие параметры в /etc/waagent.conf соответствующим образом:</span><span class="sxs-lookup"><span data-stu-id="26b35-187">After installing the Azure Linux Agent (see previous step), modify the following parameters in /etc/waagent.conf appropriately:</span></span>
    
     <span data-ttu-id="26b35-188">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.</span><span class="sxs-lookup"><span data-stu-id="26b35-188">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.</span></span>
11. <span data-ttu-id="26b35-189">Выполните следующие команды, чтобы отменить подготовку виртуальной машины и подготовить ее в Azure:</span><span class="sxs-lookup"><span data-stu-id="26b35-189">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
    # <a name="sudo-waagent--force--deprovision"></a><span data-ttu-id="26b35-190">sudo waagent -force -deprovision</span><span class="sxs-lookup"><span data-stu-id="26b35-190">sudo waagent -force -deprovision</span></span>
    # <a name="export-histsize0"></a><span data-ttu-id="26b35-191">export HISTSIZE=0</span><span class="sxs-lookup"><span data-stu-id="26b35-191">export HISTSIZE=0</span></span>
    # <a name="logout"></a><span data-ttu-id="26b35-192">logout</span><span class="sxs-lookup"><span data-stu-id="26b35-192">logout</span></span>
12. <span data-ttu-id="26b35-193">Убедитесь, что агент Linux для Azure запускается при загрузке:</span><span class="sxs-lookup"><span data-stu-id="26b35-193">Ensure the Azure Linux Agent runs at startup:</span></span>
    
        # sudo systemctl enable waagent.service
13. <span data-ttu-id="26b35-194">В диспетчере Hyper-V выберите **Действие -> Завершение работы**.</span><span class="sxs-lookup"><span data-stu-id="26b35-194">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="26b35-195">Виртуальный жесткий диск Linux готов к передаче в Azure.</span><span class="sxs-lookup"><span data-stu-id="26b35-195">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26b35-196">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="26b35-196">Next steps</span></span>
<span data-ttu-id="26b35-197">Теперь виртуальный жесткий диск SUSE Linux можно использовать для создания новых виртуальных машин Azure.</span><span class="sxs-lookup"><span data-stu-id="26b35-197">You're now ready to use your SUSE Linux virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="26b35-198">Если вы загружаете VHD-файл в Azure впервые, обратитесь к шагам 2 и 3 в статье [Создание и загрузка виртуального жесткого диска, содержащего операционную систему Linux](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="26b35-198">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

