---
title: "aaaCreate и отправка виртуального жесткого диска SUSE Linux в Azure"
description: "Узнайте toocreate и отправить в Azure виртуального жесткого диска (VHD), содержащий операционной системы SUSE Linux."
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
ms.openlocfilehash: 9185c7e67279357f00db0f43e944e96c58f0dd60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-sles-or-opensuse-virtual-machine-for-azure"></a><span data-ttu-id="8971a-103">Подготовка виртуальной машины SLES или openSUSE для Azure</span><span class="sxs-lookup"><span data-stu-id="8971a-103">Prepare a SLES or openSUSE virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="8971a-104">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8971a-104">Prerequisites</span></span>
<span data-ttu-id="8971a-105">В этой статье предполагается, что вы уже установили SUSE или openSUSE Linux tooa виртуального жесткого диска операционной системы.</span><span class="sxs-lookup"><span data-stu-id="8971a-105">This article assumes that you have already installed a SUSE or openSUSE Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="8971a-106">Существуют несколько средства toocreate VHD-файлы, например решение виртуализации, таких как Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="8971a-106">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="8971a-107">Инструкции см. в разделе [Установка hello роль Hyper-V и настройка виртуальной машины](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="8971a-107">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="sles--opensuse-installation-notes"></a><span data-ttu-id="8971a-108">Замечания по установке SLES и openSUSE</span><span class="sxs-lookup"><span data-stu-id="8971a-108">SLES / openSUSE installation notes</span></span>
* <span data-ttu-id="8971a-109">Дополнительные сведения о подготовке Linux для Azure см. в разделе [Общие замечания по установке Linux](create-upload-generic.md#general-linux-installation-notes).</span><span class="sxs-lookup"><span data-stu-id="8971a-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="8971a-110">Hello формат VHDX не поддерживается только в Azure, **фиксированный VHD**.</span><span class="sxs-lookup"><span data-stu-id="8971a-110">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="8971a-111">Можно преобразовать формат tooVHD hello диска, с помощью диспетчера Hyper-V или hello командлет convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="8971a-111">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span>
* <span data-ttu-id="8971a-112">При установке системы Linux hello рекомендуется использовать стандартный секции, а не LVM (часто hello по умолчанию для многих установок).</span><span class="sxs-lookup"><span data-stu-id="8971a-112">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="8971a-113">Это позволит избежать конфликтов имен LVM с клонированные виртуальные машины, особенно в том случае, если на диске ОС никогда не требуется tooanother toobe присоединенного виртуальной Машины для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="8971a-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="8971a-114">Для дисков данных можно использовать [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) или [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8971a-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="8971a-115">Не настраивайте переключения секции на диске ОС hello.</span><span class="sxs-lookup"><span data-stu-id="8971a-115">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="8971a-116">агент Linux Hello может быть настроенный toocreate файл подкачки на диске временного ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="8971a-116">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="8971a-117">Дополнительные сведения об этом можно найти в hello описанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="8971a-117">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="8971a-118">Все виртуальные жесткие диски hello должны иметь размеры, кратные 1 МБ.</span><span class="sxs-lookup"><span data-stu-id="8971a-118">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="use-suse-studio"></a><span data-ttu-id="8971a-119">Использование SUSE Studio</span><span class="sxs-lookup"><span data-stu-id="8971a-119">Use SUSE Studio</span></span>
<span data-ttu-id="8971a-120">[SUSE Studio](http://www.susestudio.com) можно с легкостью использовать для создания образов SLES и openSUSE для Azure и Hyper-V, а также для управления этими образами.</span><span class="sxs-lookup"><span data-stu-id="8971a-120">[SUSE Studio](http://www.susestudio.com) can easily create and manage your SLES and openSUSE images for Azure and Hyper-V.</span></span> <span data-ttu-id="8971a-121">Это рекомендованный подход для настройки свои собственные образы SLES и openSUSE hello.</span><span class="sxs-lookup"><span data-stu-id="8971a-121">This is hello recommended approach for customizing your own SLES and openSUSE images.</span></span>

<span data-ttu-id="8971a-122">Как альтернативный toobuilding собственного виртуального жесткого диска, SUSE также публикует изображения BYOS (переведите свои собственные подписки) для SLES на [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).</span><span class="sxs-lookup"><span data-stu-id="8971a-122">As an alternative toobuilding your own VHD, SUSE also publishes BYOS (Bring Your Own Subscription) images for SLES at [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).</span></span>

## <a name="prepare-suse-linux-enterprise-server-11-sp4"></a><span data-ttu-id="8971a-123">Подготовка SUSE Linux Enterprise Server 11 с пакетом обновления 4 (SP4)</span><span class="sxs-lookup"><span data-stu-id="8971a-123">Prepare SUSE Linux Enterprise Server 11 SP4</span></span>
1. <span data-ttu-id="8971a-124">Hello центральной панели диспетчера Hyper-V выберите виртуальную машину hello.</span><span class="sxs-lookup"><span data-stu-id="8971a-124">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="8971a-125">Нажмите кнопку **Connect** окна hello tooopen для hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="8971a-125">Click **Connect** tooopen hello window for hello virtual machine.</span></span>
3. <span data-ttu-id="8971a-126">Регистрация вашего tooallow системы SUSE Linux Enterprise его toodownload обновления и пакеты установки.</span><span class="sxs-lookup"><span data-stu-id="8971a-126">Register your SUSE Linux Enterprise system tooallow it toodownload updates and install packages.</span></span>
4. <span data-ttu-id="8971a-127">Обновите систему hello hello последние обновления системы:</span><span class="sxs-lookup"><span data-stu-id="8971a-127">Update hello system with hello latest patches:</span></span>
   
        # sudo zypper update
5. <span data-ttu-id="8971a-128">Установите агент Azure Linux hello из репозитория SLES hello:</span><span class="sxs-lookup"><span data-stu-id="8971a-128">Install hello Azure Linux Agent from hello SLES repository:</span></span>
   
        # sudo zypper install WALinuxAgent
6. <span data-ttu-id="8971a-129">Проверьте Если запущена команда waagent задано слишком «on» в chkconfig и если нет, включить его для автоматического запуска:</span><span class="sxs-lookup"><span data-stu-id="8971a-129">Check if waagent is set too"on" in chkconfig, and if not, enable it for autostart:</span></span>
   
        # sudo chkconfig waagent on
7. <span data-ttu-id="8971a-130">Убедитесь, что служба waagent работает. Если она не работает, запустите ее:</span><span class="sxs-lookup"><span data-stu-id="8971a-130">Check if waagent service is running, and if not, start it:</span></span> 
   
        # sudo service waagent start
8. <span data-ttu-id="8971a-131">Измените строку загрузки ядра hello в параметры grub tooinclude дополнительные ядра для Azure.</span><span class="sxs-lookup"><span data-stu-id="8971a-131">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="8971a-132">toodo этом откройте «/ boot/grub/menu.lst» в текстовом редакторе, убедитесь, что ядра по умолчанию hello включает hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="8971a-132">toodo this open "/boot/grub/menu.lst" in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
   
    <span data-ttu-id="8971a-133">Это обеспечит все консоли сообщения отправляются toohello первый последовательный порт, который может помочь Azure поддержка с помощью отладки проблем.</span><span class="sxs-lookup"><span data-stu-id="8971a-133">This will ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
9. <span data-ttu-id="8971a-134">Убедитесь, что /boot/grub/menu.lst и/etc/fstab оба диска hello ссылка, с помощью его идентификатора UUID (с uuid) вместо диска с Идентификатором hello (по идентификатору).</span><span class="sxs-lookup"><span data-stu-id="8971a-134">Confirm that /boot/grub/menu.lst and /etc/fstab both reference hello disk using its UUID (by-uuid) instead of hello disk ID (by-id).</span></span> 
   
    <span data-ttu-id="8971a-135">Получение UUID диска</span><span class="sxs-lookup"><span data-stu-id="8971a-135">Get disk UUID</span></span>
   
        # ls /dev/disk/by-uuid/
   
    <span data-ttu-id="8971a-136">Если /dev/disk/by-id / — используется, обновления /boot/grub/menu.lst и/etc/fstab правильную uuid по значению hello</span><span class="sxs-lookup"><span data-stu-id="8971a-136">If /dev/disk/by-id/ is used, update both /boot/grub/menu.lst and /etc/fstab with hello proper by-uuid value</span></span>
   
    <span data-ttu-id="8971a-137">Перед изменением</span><span class="sxs-lookup"><span data-stu-id="8971a-137">Before change</span></span>
   
        root=/dev/disk/by-id/SCSI-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxxx-part1
   
    <span data-ttu-id="8971a-138">После изменения</span><span class="sxs-lookup"><span data-stu-id="8971a-138">After change</span></span>
   
        root=/dev/disk/by-uuid/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
10. <span data-ttu-id="8971a-139">Измените tooavoid правила udev создания статические правила для hello интерфейсы Ethernet.</span><span class="sxs-lookup"><span data-stu-id="8971a-139">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="8971a-140">Эти правила приводят к появлению проблем при клонировании виртуальной машины в Microsoft Azure или Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="8971a-140">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
    
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
11. <span data-ttu-id="8971a-141">Рекомендуется tooedit hello файл «/ и т. д/sysconfig/сети и dhcp» и измените hello `DHCLIENT_SET_HOSTNAME` toohello следующий параметр:</span><span class="sxs-lookup"><span data-stu-id="8971a-141">It is recommended tooedit hello file "/etc/sysconfig/network/dhcp" and change hello `DHCLIENT_SET_HOSTNAME` parameter toohello following:</span></span>
    
     <span data-ttu-id="8971a-142">DHCLIENT_SET_HOSTNAME="no"</span><span class="sxs-lookup"><span data-stu-id="8971a-142">DHCLIENT_SET_HOSTNAME="no"</span></span>
12. <span data-ttu-id="8971a-143">В «/ etc/sudoers» закомментируйте или удалите следующие строки, если они существуют hello:</span><span class="sxs-lookup"><span data-stu-id="8971a-143">In "/etc/sudoers", comment out or remove hello following lines if they exist:</span></span>
    
     <span data-ttu-id="8971a-144">По умолчанию targetpw # запрашивать пароль hello hello целевого пользователя, т. е. все ALL=(ALL) всех корневых # предупреждение!</span><span class="sxs-lookup"><span data-stu-id="8971a-144">Defaults targetpw   # ask for hello password of hello target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span></span> <span data-ttu-id="8971a-145">Используйте только вместе с Defaults targetpw!</span><span class="sxs-lookup"><span data-stu-id="8971a-145">Only use this together with 'Defaults targetpw'!</span></span>
13. <span data-ttu-id="8971a-146">Убедитесь, что hello SSH сервер установлен и настроен toostart во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="8971a-146">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="8971a-147">Обычно это происходит по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="8971a-147">This is usually hello default.</span></span>
14. <span data-ttu-id="8971a-148">Не создавайте подкачки на диске ОС hello.</span><span class="sxs-lookup"><span data-stu-id="8971a-148">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="8971a-149">Hello Azure Linux Agent может автоматически настроить подкачки с помощью hello локальный диск ресурсов, toohello подключенных виртуальных Машин после подготовки в Azure.</span><span class="sxs-lookup"><span data-stu-id="8971a-149">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="8971a-150">Обратите внимание, что hello локальный диск ресурсов *временные* диск, а также может очищаться при отмененной подготовкой hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="8971a-150">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="8971a-151">После установки hello Azure Linux Agent (см. выше), измените соответствующим образом следующие параметры в /etc/waagent.conf hello:</span><span class="sxs-lookup"><span data-stu-id="8971a-151">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
     <span data-ttu-id="8971a-152">ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048;# Примечание: задать этот toowhatever он нужен toobe.</span><span class="sxs-lookup"><span data-stu-id="8971a-152">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.</span></span>
15. <span data-ttu-id="8971a-153">Запустите следующие команды toodeprovision hello виртуальной машины hello и подготовить его для подготовки в Azure:</span><span class="sxs-lookup"><span data-stu-id="8971a-153">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
    # <a name="sudo-waagent--force--deprovision"></a><span data-ttu-id="8971a-154">sudo waagent -force -deprovision</span><span class="sxs-lookup"><span data-stu-id="8971a-154">sudo waagent -force -deprovision</span></span>
    # <a name="export-histsize0"></a><span data-ttu-id="8971a-155">export HISTSIZE=0</span><span class="sxs-lookup"><span data-stu-id="8971a-155">export HISTSIZE=0</span></span>
    # <a name="logout"></a><span data-ttu-id="8971a-156">logout</span><span class="sxs-lookup"><span data-stu-id="8971a-156">logout</span></span>
16. <span data-ttu-id="8971a-157">В диспетчере Hyper-V выберите **Действие -> Завершение работы**.</span><span class="sxs-lookup"><span data-stu-id="8971a-157">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="8971a-158">ДИСК Linux имеет теперь готовы toobe отправлен tooAzure.</span><span class="sxs-lookup"><span data-stu-id="8971a-158">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

- - -
## <a name="prepare-opensuse-131"></a><span data-ttu-id="8971a-159">Подготовка openSUSE 13.1+</span><span class="sxs-lookup"><span data-stu-id="8971a-159">Prepare openSUSE 13.1+</span></span>
1. <span data-ttu-id="8971a-160">Hello центральной панели диспетчера Hyper-V выберите виртуальную машину hello.</span><span class="sxs-lookup"><span data-stu-id="8971a-160">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="8971a-161">Нажмите кнопку **Connect** окна hello tooopen для hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="8971a-161">Click **Connect** tooopen hello window for hello virtual machine.</span></span>
3. <span data-ttu-id="8971a-162">Оболочка hello, запустите команду hello "`zypper lr`".</span><span class="sxs-lookup"><span data-stu-id="8971a-162">On hello shell, run hello command '`zypper lr`'.</span></span> <span data-ttu-id="8971a-163">Если эта команда возвращает выходные данные примерно следующие, репозиториев hello настроены должным образом--каких-либо корректировок необходимы toohello (Обратите внимание, что номера версий могут различаться):</span><span class="sxs-lookup"><span data-stu-id="8971a-163">If this command returns output similar toohello following, then hello repositories are configured as expected--no adjustments are necessary (note that version numbers may vary):</span></span>
   
        # | Alias                 | Name                  | Enabled | Refresh
        --+-----------------------+-----------------------+---------+--------
        1 | Cloud:Tools_13.1      | Cloud:Tools_13.1      | Yes     | Yes
        2 | openSUSE_13.1_OSS     | openSUSE_13.1_OSS     | Yes     | Yes
        3 | openSUSE_13.1_Updates | openSUSE_13.1_Updates | Yes     | Yes
   
    <span data-ttu-id="8971a-164">Если hello команда возвращает «Нет репозиториев определенные...» выполните следующие команды tooadd hello эти репозиториев.</span><span class="sxs-lookup"><span data-stu-id="8971a-164">If hello command returns "No repositories defined..." then use hello following commands tooadd these repos:</span></span>
   
        # sudo zypper ar -f http://download.opensuse.org/repositories/Cloud:Tools/openSUSE_13.1 Cloud:Tools_13.1
        # sudo zypper ar -f http://download.opensuse.org/distribution/13.1/repo/oss openSUSE_13.1_OSS
        # sudo zypper ar -f http://download.opensuse.org/update/13.1 openSUSE_13.1_Updates
   
    <span data-ttu-id="8971a-165">Затем можно проверить, были добавлены репозиториев hello, выполнив команду hello "`zypper lr`" еще раз.</span><span class="sxs-lookup"><span data-stu-id="8971a-165">You can then verify hello repositories have been added by running hello command '`zypper lr`' again.</span></span> <span data-ttu-id="8971a-166">В случае, если один из репозиториев существенные обновления hello не включена, включите его с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="8971a-166">In case one of hello relevant update repositories is not enabled, enable it with following command:</span></span>
   
        # sudo zypper mr -e [NUMBER OF REPOSITORY]
4. <span data-ttu-id="8971a-167">Обновление hello ядра toohello последней доступной версии:</span><span class="sxs-lookup"><span data-stu-id="8971a-167">Update hello kernel toohello latest available version:</span></span>
   
        # sudo zypper up kernel-default
   
    <span data-ttu-id="8971a-168">Или системы hello tooupdate все последние обновления системы hello:</span><span class="sxs-lookup"><span data-stu-id="8971a-168">Or tooupdate hello system with all hello latest patches:</span></span>
   
        # sudo zypper update
5. <span data-ttu-id="8971a-169">Установите агент Azure Linux hello.</span><span class="sxs-lookup"><span data-stu-id="8971a-169">Install hello Azure Linux Agent.</span></span>
   
   # <a name="sudo-zypper-install-walinuxagent"></a><span data-ttu-id="8971a-170">sudo zypper install WALinuxAgent</span><span class="sxs-lookup"><span data-stu-id="8971a-170">sudo zypper install WALinuxAgent</span></span>
6. <span data-ttu-id="8971a-171">Измените строку загрузки ядра hello в параметры grub tooinclude дополнительные ядра для Azure.</span><span class="sxs-lookup"><span data-stu-id="8971a-171">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="8971a-172">toodo, откройте «/ boot/grub/menu.lst» в текстовом редакторе, убедитесь, что ядра по умолчанию hello включает hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="8971a-172">toodo this, open "/boot/grub/menu.lst" in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
   
     <span data-ttu-id="8971a-173">console=ttyS0 earlyprintk=ttyS0 rootdelay=300</span><span class="sxs-lookup"><span data-stu-id="8971a-173">console=ttyS0 earlyprintk=ttyS0 rootdelay=300</span></span>
   
   <span data-ttu-id="8971a-174">Это обеспечит все консоли сообщения отправляются toohello первый последовательный порт, который может помочь Azure поддержка с помощью отладки проблем.</span><span class="sxs-lookup"><span data-stu-id="8971a-174">This will ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="8971a-175">Кроме того удалите hello следующие параметры из строки загрузки ядра hello, если они существуют.</span><span class="sxs-lookup"><span data-stu-id="8971a-175">In addition, remove hello following parameters from hello kernel boot line if they exist:</span></span>
   
     <span data-ttu-id="8971a-176">libata.atapi_enabled=0 reserve=0x1f0,0x8</span><span class="sxs-lookup"><span data-stu-id="8971a-176">libata.atapi_enabled=0 reserve=0x1f0,0x8</span></span>
7. <span data-ttu-id="8971a-177">Рекомендуется tooedit hello файл «/ и т. д/sysconfig/сети и dhcp» и измените hello `DHCLIENT_SET_HOSTNAME` toohello следующий параметр:</span><span class="sxs-lookup"><span data-stu-id="8971a-177">It is recommended tooedit hello file "/etc/sysconfig/network/dhcp" and change hello `DHCLIENT_SET_HOSTNAME` parameter toohello following:</span></span>
   
     <span data-ttu-id="8971a-178">DHCLIENT_SET_HOSTNAME="no"</span><span class="sxs-lookup"><span data-stu-id="8971a-178">DHCLIENT_SET_HOSTNAME="no"</span></span>
8. <span data-ttu-id="8971a-179">**Важно:** в «/ etc/sudoers», закомментируйте или удалите следующие строки, если они существуют hello:</span><span class="sxs-lookup"><span data-stu-id="8971a-179">**Important:** In "/etc/sudoers", comment out or remove hello following lines if they exist:</span></span>
   
     <span data-ttu-id="8971a-180">По умолчанию targetpw # запрашивать пароль hello hello целевого пользователя, т. е. все ALL=(ALL) всех корневых # предупреждение!</span><span class="sxs-lookup"><span data-stu-id="8971a-180">Defaults targetpw   # ask for hello password of hello target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span></span> <span data-ttu-id="8971a-181">Используйте только вместе с Defaults targetpw!</span><span class="sxs-lookup"><span data-stu-id="8971a-181">Only use this together with 'Defaults targetpw'!</span></span>
9. <span data-ttu-id="8971a-182">Убедитесь, что hello SSH сервер установлен и настроен toostart во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="8971a-182">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="8971a-183">Обычно это происходит по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="8971a-183">This is usually hello default.</span></span>
10. <span data-ttu-id="8971a-184">Не создавайте подкачки на диске ОС hello.</span><span class="sxs-lookup"><span data-stu-id="8971a-184">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="8971a-185">Hello Azure Linux Agent может автоматически настроить подкачки с помощью hello локальный диск ресурсов, toohello подключенных виртуальных Машин после подготовки в Azure.</span><span class="sxs-lookup"><span data-stu-id="8971a-185">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="8971a-186">Обратите внимание, что hello локальный диск ресурсов *временные* диск, а также может очищаться при отмененной подготовкой hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="8971a-186">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="8971a-187">После установки hello Azure Linux Agent (см. выше), измените соответствующим образом следующие параметры в /etc/waagent.conf hello:</span><span class="sxs-lookup"><span data-stu-id="8971a-187">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
     <span data-ttu-id="8971a-188">ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048;# Примечание: задать этот toowhatever он нужен toobe.</span><span class="sxs-lookup"><span data-stu-id="8971a-188">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.</span></span>
11. <span data-ttu-id="8971a-189">Запустите следующие команды toodeprovision hello виртуальной машины hello и подготовить его для подготовки в Azure:</span><span class="sxs-lookup"><span data-stu-id="8971a-189">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
    # <a name="sudo-waagent--force--deprovision"></a><span data-ttu-id="8971a-190">sudo waagent -force -deprovision</span><span class="sxs-lookup"><span data-stu-id="8971a-190">sudo waagent -force -deprovision</span></span>
    # <a name="export-histsize0"></a><span data-ttu-id="8971a-191">export HISTSIZE=0</span><span class="sxs-lookup"><span data-stu-id="8971a-191">export HISTSIZE=0</span></span>
    # <a name="logout"></a><span data-ttu-id="8971a-192">logout</span><span class="sxs-lookup"><span data-stu-id="8971a-192">logout</span></span>
12. <span data-ttu-id="8971a-193">Убедитесь, приветствия запускается агент Azure Linux при загрузке:</span><span class="sxs-lookup"><span data-stu-id="8971a-193">Ensure hello Azure Linux Agent runs at startup:</span></span>
    
        # sudo systemctl enable waagent.service
13. <span data-ttu-id="8971a-194">В диспетчере Hyper-V выберите **Действие -> Завершение работы**.</span><span class="sxs-lookup"><span data-stu-id="8971a-194">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="8971a-195">ДИСК Linux имеет теперь готовы toobe отправлен tooAzure.</span><span class="sxs-lookup"><span data-stu-id="8971a-195">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8971a-196">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8971a-196">Next steps</span></span>
<span data-ttu-id="8971a-197">Вы являетесь теперь готовы toouse SUSE Linux виртуальный жесткий диск toocreate новых виртуальных машин в Azure.</span><span class="sxs-lookup"><span data-stu-id="8971a-197">You're now ready toouse your SUSE Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="8971a-198">Если это первый раз, что идет Отправка tooAzure файл .vhd hello hello см. шаги 2 и 3 в [Создание и передача виртуального жесткого диска, который содержит операционную систему Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8971a-198">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

