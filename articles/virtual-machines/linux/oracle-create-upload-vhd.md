---
title: "aaaCreate и отправка виртуального жесткого диска Oracle Linux | Документы Microsoft"
description: "Узнайте toocreate и отправить в Azure виртуального жесткого диска (VHD), содержащий операционную систему, Oracle Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-service-management,azure-resource-manager
ms.assetid: dd96f771-26eb-4391-9a89-8c8b6d691822
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: szark
ms.openlocfilehash: be9cf284d7f5e7122a106506a343e53e9f1ac56e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-an-oracle-linux-virtual-machine-for-azure"></a><span data-ttu-id="be05d-103">Подготовка виртуальной машины Oracle Linux для Azure</span><span class="sxs-lookup"><span data-stu-id="be05d-103">Prepare an Oracle Linux virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="be05d-104">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="be05d-104">Prerequisites</span></span>
<span data-ttu-id="be05d-105">В этой статье предполагается, что вы уже установили Oracle Linux операционной системы tooa виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="be05d-105">This article assumes that you have already installed an Oracle Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="be05d-106">Существуют несколько средства toocreate VHD-файлы, например решение виртуализации, таких как Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="be05d-106">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="be05d-107">Инструкции см. в разделе [Установка hello роль Hyper-V и настройка виртуальной машины](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="be05d-107">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="oracle-linux-installation-notes"></a><span data-ttu-id="be05d-108">Замечания по установке Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="be05d-108">Oracle Linux installation notes</span></span>
* <span data-ttu-id="be05d-109">Дополнительные сведения о подготовке Linux для Azure см. в разделе [Общие замечания по установке Linux](create-upload-generic.md#general-linux-installation-notes).</span><span class="sxs-lookup"><span data-stu-id="be05d-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="be05d-110">В Hyper-V и Azure поддерживаются совместимое ядро Oracle Red Hat и его UEK3 (Unbreakable Enterprise Kernel).</span><span class="sxs-lookup"><span data-stu-id="be05d-110">Oracle's Red Hat compatible kernel and their UEK3 (Unbreakable Enterprise Kernel) are both supported on Hyper-V and Azure.</span></span> <span data-ttu-id="be05d-111">Для получения наилучших результатов следует убедиться, что tooupdate toohello последние ядра при подготовке вашего виртуального жесткого диска Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="be05d-111">For best results, please be sure tooupdate toohello latest kernel while preparing your Oracle Linux VHD.</span></span>
* <span data-ttu-id="be05d-112">UEK2 Oracle не поддерживается в Hyper-V и Azure содержит hello необходимые драйверы.</span><span class="sxs-lookup"><span data-stu-id="be05d-112">Oracle's UEK2 is not supported on Hyper-V and Azure as it does not include hello required drivers.</span></span>
* <span data-ttu-id="be05d-113">Hello формат VHDX не поддерживается только в Azure, **фиксированный VHD**.</span><span class="sxs-lookup"><span data-stu-id="be05d-113">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="be05d-114">Можно преобразовать формат tooVHD hello диска, с помощью диспетчера Hyper-V или hello командлет convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="be05d-114">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span>
* <span data-ttu-id="be05d-115">При установке системы Linux hello рекомендуется использовать стандартный секции, а не LVM (часто hello по умолчанию для многих установок).</span><span class="sxs-lookup"><span data-stu-id="be05d-115">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="be05d-116">Это позволит избежать конфликтов имен LVM с клонированные виртуальные машины, особенно в том случае, если на диске ОС никогда не требуется tooanother toobe присоединенного виртуальной Машины для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="be05d-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="be05d-117">Для дисков данных можно использовать [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) или [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="be05d-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="be05d-118">Для больших размеров виртуальной Машины из-за ошибки tooa в версии ядра Linux ниже 2.6.37 NUMA не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="be05d-118">NUMA is not supported for larger VM sizes due tooa bug in Linux kernel versions below 2.6.37.</span></span> <span data-ttu-id="be05d-119">Эту проблему в основном влияет на распределения с использованием hello вышестоящего Red Hat 2.6.32 ядра.</span><span class="sxs-lookup"><span data-stu-id="be05d-119">This issue primarily impacts distributions using hello upstream Red Hat 2.6.32 kernel.</span></span> <span data-ttu-id="be05d-120">Ручная установка агента Azure Linux hello (waagent) будет автоматически отключена NUMA в конфигурации GRUB hello для ядра Linux hello.</span><span class="sxs-lookup"><span data-stu-id="be05d-120">Manual installation of hello Azure Linux agent (waagent) will automatically disable NUMA in hello GRUB configuration for hello Linux kernel.</span></span> <span data-ttu-id="be05d-121">Дополнительные сведения об этом можно найти в hello описанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="be05d-121">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="be05d-122">Не настраивайте переключения секции на диске ОС hello.</span><span class="sxs-lookup"><span data-stu-id="be05d-122">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="be05d-123">агент Linux Hello может быть настроенный toocreate файл подкачки на диске временного ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="be05d-123">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="be05d-124">Дополнительные сведения об этом можно найти в hello описанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="be05d-124">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="be05d-125">Все виртуальные жесткие диски hello должны иметь размеры, кратные 1 МБ.</span><span class="sxs-lookup"><span data-stu-id="be05d-125">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>
* <span data-ttu-id="be05d-126">Убедитесь в том, что hello `Addons` репозитория включена.</span><span class="sxs-lookup"><span data-stu-id="be05d-126">Make sure that hello `Addons` repository is enabled.</span></span> <span data-ttu-id="be05d-127">Измените файл hello `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) или `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux) и измените строку hello `enabled=0` слишком`enabled=1` под **[ol6_addons]** или **[ol7_addons]** в этом файл.</span><span class="sxs-lookup"><span data-stu-id="be05d-127">Edit hello file `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux ), and change hello line `enabled=0` too`enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

## <a name="oracle-linux-64"></a><span data-ttu-id="be05d-128">Oracle Linux 6.4+</span><span class="sxs-lookup"><span data-stu-id="be05d-128">Oracle Linux 6.4+</span></span>
<span data-ttu-id="be05d-129">Необходимо выполнить определенную конфигурацию действия в операционной системе hello для hello toorun виртуальной машины в Azure.</span><span class="sxs-lookup"><span data-stu-id="be05d-129">You must complete specific configuration steps in hello operating system for hello virtual machine toorun in Azure.</span></span>

1. <span data-ttu-id="be05d-130">Hello центральной панели диспетчера Hyper-V выберите виртуальную машину hello.</span><span class="sxs-lookup"><span data-stu-id="be05d-130">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="be05d-131">Нажмите кнопку **Connect** окна hello tooopen для hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="be05d-131">Click **Connect** tooopen hello window for hello virtual machine.</span></span>
3. <span data-ttu-id="be05d-132">Удалите NetworkManager, выполнив следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="be05d-132">Uninstall NetworkManager by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager
   
    <span data-ttu-id="be05d-133">**Примечание:** Если hello пакет не установлен, эта команда завершится ошибкой с сообщением об ошибке.</span><span class="sxs-lookup"><span data-stu-id="be05d-133">**Note:** If hello package is not already installed, this command will fail with an error message.</span></span> <span data-ttu-id="be05d-134">Это ожидаемое поведение.</span><span class="sxs-lookup"><span data-stu-id="be05d-134">This is expected.</span></span>
4. <span data-ttu-id="be05d-135">Создайте файл с именем **сети** в hello `/etc/sysconfig/` каталог, содержащий hello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="be05d-135">Create a file named **network** in hello `/etc/sysconfig/` directory that contains hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
5. <span data-ttu-id="be05d-136">Создайте файл с именем **ifcfg eth0** в hello `/etc/sysconfig/network-scripts/` каталог, содержащий hello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="be05d-136">Create a file named **ifcfg-eth0** in hello `/etc/sysconfig/network-scripts/` directory that contains hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
6. <span data-ttu-id="be05d-137">Измените tooavoid правила udev создания статические правила для hello интерфейсы Ethernet.</span><span class="sxs-lookup"><span data-stu-id="be05d-137">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="be05d-138">Эти правила приводят к появлению проблем при клонировании виртуальной машины в Microsoft Azure или Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="be05d-138">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
7. <span data-ttu-id="be05d-139">Убедитесь, что hello сети служба будет запущена во время загрузки, выполнив следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="be05d-139">Ensure hello network service will start at boot time by running hello following command:</span></span>
   
        # chkconfig network on
8. <span data-ttu-id="be05d-140">Установите python pyasn1, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="be05d-140">Install python-pyasn1 by running hello following command:</span></span>
   
        # sudo yum install python-pyasn1
9. <span data-ttu-id="be05d-141">Измените строку загрузки ядра hello в параметры grub tooinclude дополнительные ядра для Azure.</span><span class="sxs-lookup"><span data-stu-id="be05d-141">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="be05d-142">toodo этом откройте «/ boot/grub/menu.lst» в текстовом редакторе, убедитесь, что ядра по умолчанию hello включает hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="be05d-142">toodo this open "/boot/grub/menu.lst" in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300 numa=off
   
   <span data-ttu-id="be05d-143">Это также гарантирует все консоли сообщения отправляются toohello первый последовательный порт, который может помочь Azure поддержка с помощью отладки проблем.</span><span class="sxs-lookup"><span data-stu-id="be05d-143">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="be05d-144">NUMA будут отключены из-за ошибки tooa совместимость ядра Oracle в Red Hat.</span><span class="sxs-lookup"><span data-stu-id="be05d-144">This will disable NUMA due tooa bug in Oracle's Red Hat compatible kernel.</span></span>
   
   <span data-ttu-id="be05d-145">В дополнение к этому toohello выше, рекомендуется слишком*удалить* hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="be05d-145">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
   <span data-ttu-id="be05d-146">Графический quiet начальной загрузки, не используются в облачной среде, где мы хотим, чтобы все журналы toobe hello, отправляемых toohello последовательного порта.</span><span class="sxs-lookup"><span data-stu-id="be05d-146">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>
   
   <span data-ttu-id="be05d-147">Hello `crashkernel` возможность влево, при желании настроить, но следует заметить, что этот параметр приведет к уменьшению hello объем доступной памяти в hello виртуальная машина по 128 МБ или больше, которое может быть проблематично на hello меньшего размера виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="be05d-147">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>
10. <span data-ttu-id="be05d-148">Убедитесь, что hello SSH сервер установлен и настроен toostart во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="be05d-148">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="be05d-149">Обычно это происходит по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="be05d-149">This is usually hello default.</span></span>
11. <span data-ttu-id="be05d-150">Установите агент Azure Linux hello, выполнив следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="be05d-150">Install hello Azure Linux Agent by running hello following command.</span></span> <span data-ttu-id="be05d-151">Последняя версия Hello — 2.0.15.</span><span class="sxs-lookup"><span data-stu-id="be05d-151">hello latest version is 2.0.15.</span></span>
    
        # sudo yum install WALinuxAgent
    
    <span data-ttu-id="be05d-152">Обратите внимание, что установка пакета WALinuxAgent hello приведет к удалению hello NetworkManager NetworkManager gnome пакеты, если они не были уже удалены как описано на шаге 2.</span><span class="sxs-lookup"><span data-stu-id="be05d-152">Note that installing hello WALinuxAgent package will remove hello NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 2.</span></span>
12. <span data-ttu-id="be05d-153">Не создавайте подкачки на диске ОС hello.</span><span class="sxs-lookup"><span data-stu-id="be05d-153">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="be05d-154">Hello Azure Linux Agent может автоматически настроить подкачки с помощью hello локальный диск ресурсов, toohello подключенных виртуальных Машин после подготовки в Azure.</span><span class="sxs-lookup"><span data-stu-id="be05d-154">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="be05d-155">Обратите внимание, что hello локальный диск ресурсов *временные* диск, а также может очищаться при отмененной подготовкой hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="be05d-155">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="be05d-156">После установки hello Azure Linux Agent (см. выше), измените соответствующим образом следующие параметры в /etc/waagent.conf hello:</span><span class="sxs-lookup"><span data-stu-id="be05d-156">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
13. <span data-ttu-id="be05d-157">Запустите следующие команды toodeprovision hello виртуальной машины hello и подготовить его для подготовки в Azure:</span><span class="sxs-lookup"><span data-stu-id="be05d-157">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
14. <span data-ttu-id="be05d-158">В диспетчере Hyper-V выберите **Действие -> Завершение работы**.</span><span class="sxs-lookup"><span data-stu-id="be05d-158">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="be05d-159">ДИСК Linux имеет теперь готовы toobe отправлен tooAzure.</span><span class="sxs-lookup"><span data-stu-id="be05d-159">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

- - -
## <a name="oracle-linux-70"></a><span data-ttu-id="be05d-160">Oracle Linux 7.0+</span><span class="sxs-lookup"><span data-stu-id="be05d-160">Oracle Linux 7.0+</span></span>
<span data-ttu-id="be05d-161">**Изменения в Oracle Linux 7**</span><span class="sxs-lookup"><span data-stu-id="be05d-161">**Changes in Oracle Linux 7**</span></span>

<span data-ttu-id="be05d-162">Подготовка виртуальной машине Oracle Linux 7 для Azure — очень похожа tooOracle Linux 6, однако существует несколько важных различий, обратите внимание:</span><span class="sxs-lookup"><span data-stu-id="be05d-162">Preparing an Oracle Linux 7 virtual machine for Azure is very similar tooOracle Linux 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="be05d-163">Совместимость ядра Red Hat hello и UEK3 Oracle поддерживаются в Azure.</span><span class="sxs-lookup"><span data-stu-id="be05d-163">Both hello Red Hat compatible kernel and Oracle's UEK3 are supported in Azure.</span></span>  <span data-ttu-id="be05d-164">Рекомендуется использовать Hello UEK3 ядра.</span><span class="sxs-lookup"><span data-stu-id="be05d-164">hello UEK3 kernel is recommended.</span></span>
* <span data-ttu-id="be05d-165">Hello NetworkManager пакета больше не конфликтует с агентом Azure Linux hello.</span><span class="sxs-lookup"><span data-stu-id="be05d-165">hello NetworkManager package no longer conflicts with hello Azure Linux agent.</span></span> <span data-ttu-id="be05d-166">Этот пакет устанавливается по умолчанию, и мы рекомендуем не удалять его.</span><span class="sxs-lookup"><span data-stu-id="be05d-166">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="be05d-167">GRUB2 сейчас используется как hello загрузчика по умолчанию, поэтому hello процедуру для редактирования параметров ядра изменилась (см. ниже).</span><span class="sxs-lookup"><span data-stu-id="be05d-167">GRUB2 is now used as hello default bootloader, so hello procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="be05d-168">XFS сейчас файловой системы по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="be05d-168">XFS is now hello default file system.</span></span> <span data-ttu-id="be05d-169">по-прежнему можно использовать Hello ext4 файловой системы, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="be05d-169">hello ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="be05d-170">**Этапы настройки**</span><span class="sxs-lookup"><span data-stu-id="be05d-170">**Configuration steps**</span></span>

1. <span data-ttu-id="be05d-171">В диспетчере Hyper-V выберите виртуальную машину hello.</span><span class="sxs-lookup"><span data-stu-id="be05d-171">In Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="be05d-172">Нажмите кнопку **Connect** tooopen окно консоли для виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="be05d-172">Click **Connect** tooopen a console window for hello virtual machine.</span></span>
3. <span data-ttu-id="be05d-173">Создайте файл с именем **сети** в hello `/etc/sysconfig/` каталог, содержащий hello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="be05d-173">Create a file named **network** in hello `/etc/sysconfig/` directory that contains hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
4. <span data-ttu-id="be05d-174">Создайте файл с именем **ifcfg eth0** в hello `/etc/sysconfig/network-scripts/` каталог, содержащий hello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="be05d-174">Create a file named **ifcfg-eth0** in hello `/etc/sysconfig/network-scripts/` directory that contains hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
5. <span data-ttu-id="be05d-175">Измените tooavoid правила udev создания статические правила для hello интерфейсы Ethernet.</span><span class="sxs-lookup"><span data-stu-id="be05d-175">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="be05d-176">Эти правила приводят к появлению проблем при клонировании виртуальной машины в Microsoft Azure или Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="be05d-176">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
6. <span data-ttu-id="be05d-177">Убедитесь, что hello сети служба будет запущена во время загрузки, выполнив следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="be05d-177">Ensure hello network service will start at boot time by running hello following command:</span></span>
   
        # sudo chkconfig network on
7. <span data-ttu-id="be05d-178">Установка пакета python pyasn1 hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="be05d-178">Install hello python-pyasn1 package by running hello following command:</span></span>
   
        # sudo yum install python-pyasn1
8. <span data-ttu-id="be05d-179">Выполнения hello следующую команду текущих метаданных yum tooclear hello и установке обновлений:</span><span class="sxs-lookup"><span data-stu-id="be05d-179">Run hello following command tooclear hello current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all
        # sudo yum -y update
9. <span data-ttu-id="be05d-180">Измените строку загрузки ядра hello в параметры grub tooinclude дополнительные ядра для Azure.</span><span class="sxs-lookup"><span data-stu-id="be05d-180">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="be05d-181">toodo этом откройте «/ и т. д, по умолчанию или grub» в текстовом редакторе и измените hello `GRUB_CMDLINE_LINUX` параметра, например:</span><span class="sxs-lookup"><span data-stu-id="be05d-181">toodo this open "/etc/default/grub" in a text editor and edit hello `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="be05d-182">Это также гарантирует все консоли сообщения отправляются toohello первый последовательный порт, который может помочь Azure поддержка с помощью отладки проблем.</span><span class="sxs-lookup"><span data-stu-id="be05d-182">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="be05d-183">Он также отключает новые соглашения об именах hello OEL 7 для сетевых адаптеров.</span><span class="sxs-lookup"><span data-stu-id="be05d-183">It also turns off hello new OEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="be05d-184">В дополнение к этому toohello выше, рекомендуется слишком*удалить* hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="be05d-184">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
   
       rhgb quiet crashkernel=auto
   
   <span data-ttu-id="be05d-185">Графический quiet начальной загрузки, не используются в облачной среде, где мы хотим, чтобы все журналы toobe hello, отправляемых toohello последовательного порта.</span><span class="sxs-lookup"><span data-stu-id="be05d-185">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>
   
   <span data-ttu-id="be05d-186">Hello `crashkernel` возможность влево, при желании настроить, но следует заметить, что этот параметр приведет к уменьшению hello объем доступной памяти в hello виртуальная машина по 128 МБ или больше, которое может быть проблематично на hello меньшего размера виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="be05d-186">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>
10. <span data-ttu-id="be05d-187">После завершения редактирования «/ и т. д, по умолчанию или grub» каждого выше, запустите hello, следующая команда toorebuild hello grub конфигурация:</span><span class="sxs-lookup"><span data-stu-id="be05d-187">Once you are done editing "/etc/default/grub" per above, run hello following command toorebuild hello grub configuration:</span></span>
    
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg
11. <span data-ttu-id="be05d-188">Убедитесь, что hello SSH сервер установлен и настроен toostart во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="be05d-188">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="be05d-189">Обычно это происходит по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="be05d-189">This is usually hello default.</span></span>
12. <span data-ttu-id="be05d-190">Установите агент Azure Linux hello, выполнив hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="be05d-190">Install hello Azure Linux Agent by running hello following command:</span></span>
    
        # sudo yum install WALinuxAgent
        # sudo systemctl enable waagent
13. <span data-ttu-id="be05d-191">Не создавайте подкачки на диске ОС hello.</span><span class="sxs-lookup"><span data-stu-id="be05d-191">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="be05d-192">Hello Azure Linux Agent может автоматически настроить подкачки с помощью hello локальный диск ресурсов, toohello подключенных виртуальных Машин после подготовки в Azure.</span><span class="sxs-lookup"><span data-stu-id="be05d-192">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="be05d-193">Обратите внимание, что hello локальный диск ресурсов *временные* диск, а также может очищаться при отмененной подготовкой hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="be05d-193">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="be05d-194">После установки hello Azure Linux Agent (см. предыдущий шаг hello), измените соответствующим образом следующие параметры в /etc/waagent.conf hello:</span><span class="sxs-lookup"><span data-stu-id="be05d-194">After installing hello Azure Linux Agent (see hello previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
14. <span data-ttu-id="be05d-195">Запустите следующие команды toodeprovision hello виртуальной машины hello и подготовить его для подготовки в Azure:</span><span class="sxs-lookup"><span data-stu-id="be05d-195">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
15. <span data-ttu-id="be05d-196">В диспетчере Hyper-V выберите **Действие -> Завершение работы**.</span><span class="sxs-lookup"><span data-stu-id="be05d-196">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="be05d-197">ДИСК Linux имеет теперь готовы toobe отправлен tooAzure.</span><span class="sxs-lookup"><span data-stu-id="be05d-197">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be05d-198">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="be05d-198">Next steps</span></span>
<span data-ttu-id="be05d-199">Вы являетесь теперь готовы toouse Oracle Linux .vhd toocreate новых виртуальных машин в Azure.</span><span class="sxs-lookup"><span data-stu-id="be05d-199">You're now ready toouse your Oracle Linux .vhd toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="be05d-200">Если это первый раз, что идет Отправка tooAzure файл .vhd hello hello см. шаги 2 и 3 в [Создание и передача виртуального жесткого диска, который содержит операционную систему Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="be05d-200">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

