---
title: "Создание и передача виртуального жесткого диска Oracle Linux | Документация Майкрософт"
description: "Узнайте, как создать и передать виртуальный жесткий диск (VHD-файл) Azure, содержащий операционную систему Oracle Linux."
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
ms.openlocfilehash: c631ddf3acf6df7364c03eb4691b78be0493e0d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-an-oracle-linux-virtual-machine-for-azure"></a><span data-ttu-id="1fd92-103">Подготовка виртуальной машины Oracle Linux для Azure</span><span class="sxs-lookup"><span data-stu-id="1fd92-103">Prepare an Oracle Linux virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="1fd92-104">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1fd92-104">Prerequisites</span></span>
<span data-ttu-id="1fd92-105">В этой статье предполагается, что вы уже установили операционную систему Oracle Linux на виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="1fd92-105">This article assumes that you have already installed an Oracle Linux operating system to a virtual hard disk.</span></span> <span data-ttu-id="1fd92-106">Существует несколько средств для создания VHD-файлов, например решение для виртуализации, такое как Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="1fd92-106">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="1fd92-107">Инструкции см. в разделе [Установка роли Hyper-V и настройка виртуальной машины](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="1fd92-107">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="oracle-linux-installation-notes"></a><span data-ttu-id="1fd92-108">Замечания по установке Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="1fd92-108">Oracle Linux installation notes</span></span>
* <span data-ttu-id="1fd92-109">Дополнительные сведения о подготовке Linux для Azure см. в разделе [Общие замечания по установке Linux](create-upload-generic.md#general-linux-installation-notes).</span><span class="sxs-lookup"><span data-stu-id="1fd92-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="1fd92-110">В Hyper-V и Azure поддерживаются совместимое ядро Oracle Red Hat и его UEK3 (Unbreakable Enterprise Kernel).</span><span class="sxs-lookup"><span data-stu-id="1fd92-110">Oracle's Red Hat compatible kernel and their UEK3 (Unbreakable Enterprise Kernel) are both supported on Hyper-V and Azure.</span></span> <span data-ttu-id="1fd92-111">Для достижения наилучших результатов при подготовке виртуального жесткого диска Oracle Linux обновите ядро до последней версии.</span><span class="sxs-lookup"><span data-stu-id="1fd92-111">For best results, please be sure to update to the latest kernel while preparing your Oracle Linux VHD.</span></span>
* <span data-ttu-id="1fd92-112">Oracle UEK2 не поддерживается в Hyper-V и Azure, поскольку не включает необходимые драйверы.</span><span class="sxs-lookup"><span data-stu-id="1fd92-112">Oracle's UEK2 is not supported on Hyper-V and Azure as it does not include the required drivers.</span></span>
* <span data-ttu-id="1fd92-113">Формат VHDX не поддерживается в Azure, поддерживается только **постоянный VHD**.</span><span class="sxs-lookup"><span data-stu-id="1fd92-113">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="1fd92-114">Можно преобразовать диск в формат VHD с помощью диспетчера Hyper-V или командлета convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="1fd92-114">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span></span>
* <span data-ttu-id="1fd92-115">При установке системы Linux рекомендуется использовать стандартные разделы, а не LVM (как правило, значение по умолчанию во многих дистрибутивах).</span><span class="sxs-lookup"><span data-stu-id="1fd92-115">When installing the Linux system it is recommended that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="1fd92-116">Это позволит избежать конфликта имен LVM при клонировании виртуальных машин, особенно если диск с OC может быть подключен к другой ВМ в целях устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="1fd92-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another VM for troubleshooting.</span></span> <span data-ttu-id="1fd92-117">Для дисков данных можно использовать [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) или [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1fd92-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="1fd92-118">NUMA не поддерживается для виртуальных машин большего размера из-за ошибки ядра Linux в версиях ниже 2.6.37.</span><span class="sxs-lookup"><span data-stu-id="1fd92-118">NUMA is not supported for larger VM sizes due to a bug in Linux kernel versions below 2.6.37.</span></span> <span data-ttu-id="1fd92-119">Эта проблема влияет в основном на дистрибутивы, в которых используется исходное ядро Red Hat 2.6.32.</span><span class="sxs-lookup"><span data-stu-id="1fd92-119">This issue primarily impacts distributions using the upstream Red Hat 2.6.32 kernel.</span></span> <span data-ttu-id="1fd92-120">При ручной установке агента Azure Linux (waagent) NUMA автоматически отключается в конфигурации GRUB для ядра Linux.</span><span class="sxs-lookup"><span data-stu-id="1fd92-120">Manual installation of the Azure Linux agent (waagent) will automatically disable NUMA in the GRUB configuration for the Linux kernel.</span></span> <span data-ttu-id="1fd92-121">Дополнительные сведения описаны далее.</span><span class="sxs-lookup"><span data-stu-id="1fd92-121">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="1fd92-122">Не настраивайте раздел подкачки на диске с ОС.</span><span class="sxs-lookup"><span data-stu-id="1fd92-122">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="1fd92-123">Можно настроить агент Linux для создания файла подкачки на временном диске ресурсов.</span><span class="sxs-lookup"><span data-stu-id="1fd92-123">The Linux agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="1fd92-124">Дополнительные сведения описаны далее.</span><span class="sxs-lookup"><span data-stu-id="1fd92-124">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="1fd92-125">Все VHD-диски должны иметь размер, кратный 1 МБ.</span><span class="sxs-lookup"><span data-stu-id="1fd92-125">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>
* <span data-ttu-id="1fd92-126">Убедитесь, что `Addons` включен репозиторий.</span><span class="sxs-lookup"><span data-stu-id="1fd92-126">Make sure that the `Addons` repository is enabled.</span></span> <span data-ttu-id="1fd92-127">Измените файл `/etc/yum.repo.d/public-yum-ol7.repo` (Oracle Linux 6) или `enabled=0` (Oracle Linux) и замените в нем строку `enabled=1` строкой **в разделе `/etc/yum.repo.d/public-yum-ol6.repo`[ol6_addons]** или **[ol7_addons]**.</span><span class="sxs-lookup"><span data-stu-id="1fd92-127">Edit the file `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux ), and change the line `enabled=0` to `enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

## <a name="oracle-linux-64"></a><span data-ttu-id="1fd92-128">Oracle Linux 6.4+</span><span class="sxs-lookup"><span data-stu-id="1fd92-128">Oracle Linux 6.4+</span></span>
<span data-ttu-id="1fd92-129">Необходимо выполнить определенные действия с конфигурацией операционной системы, чтобы виртуальная машина запускалась в среде Azure.</span><span class="sxs-lookup"><span data-stu-id="1fd92-129">You must complete specific configuration steps in the operating system for the virtual machine to run in Azure.</span></span>

1. <span data-ttu-id="1fd92-130">На центральной панели диспетчера Hyper-V выберите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="1fd92-130">In the center pane of Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="1fd92-131">Щелкните **Подключение** , чтобы открыть окно виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="1fd92-131">Click **Connect** to open the window for the virtual machine.</span></span>
3. <span data-ttu-id="1fd92-132">Удалите NetworkManager, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1fd92-132">Uninstall NetworkManager by running the following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager
   
    <span data-ttu-id="1fd92-133">**Примечание.** Если пакет еще не установлен, эта команда завершится с сообщением об ошибке.</span><span class="sxs-lookup"><span data-stu-id="1fd92-133">**Note:** If the package is not already installed, this command will fail with an error message.</span></span> <span data-ttu-id="1fd92-134">Это ожидаемое поведение.</span><span class="sxs-lookup"><span data-stu-id="1fd92-134">This is expected.</span></span>
4. <span data-ttu-id="1fd92-135">Создайте файл с именем **network** в каталоге `/etc/sysconfig/`. Файл должен содержать следующий текст:</span><span class="sxs-lookup"><span data-stu-id="1fd92-135">Create a file named **network** in the `/etc/sysconfig/` directory that contains the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
5. <span data-ttu-id="1fd92-136">Создайте файл с именем **ifcfg-eth0** в каталоге `/etc/sysconfig/network-scripts/`. Файл должен содержать следующий текст:</span><span class="sxs-lookup"><span data-stu-id="1fd92-136">Create a file named **ifcfg-eth0** in the `/etc/sysconfig/network-scripts/` directory that contains the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
6. <span data-ttu-id="1fd92-137">Переместите или удалите правила udev, чтобы не создавать статические правила для интерфейса Ethernet.</span><span class="sxs-lookup"><span data-stu-id="1fd92-137">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="1fd92-138">Эти правила приводят к появлению проблем при клонировании виртуальной машины в Microsoft Azure или Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="1fd92-138">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
7. <span data-ttu-id="1fd92-139">Убедитесь, что сетевая служба запускается во время загрузки, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1fd92-139">Ensure the network service will start at boot time by running the following command:</span></span>
   
        # chkconfig network on
8. <span data-ttu-id="1fd92-140">Установите python-pyasn1, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1fd92-140">Install python-pyasn1 by running the following command:</span></span>
   
        # sudo yum install python-pyasn1
9. <span data-ttu-id="1fd92-141">Измените строку загрузки ядра в конфигурации grub, чтобы включить дополнительные параметры ядра для Azure.</span><span class="sxs-lookup"><span data-stu-id="1fd92-141">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="1fd92-142">Для этого откройте файл "/boot/grub/menu.lst" в текстовом редакторе и убедитесь, что ядро по умолчанию включает следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="1fd92-142">To do this open "/boot/grub/menu.lst" in a text editor and ensure that the default kernel includes the following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300 numa=off
   
   <span data-ttu-id="1fd92-143">Это также гарантирует отправку всех сообщений консоли на первый последовательный порт, что может помочь технической поддержке Azure в плане отладки.</span><span class="sxs-lookup"><span data-stu-id="1fd92-143">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="1fd92-144">При этом NUMA будет отключен вследствие ошибки в совместимом ядре Oracle Red Hat.</span><span class="sxs-lookup"><span data-stu-id="1fd92-144">This will disable NUMA due to a bug in Oracle's Red Hat compatible kernel.</span></span>
   
   <span data-ttu-id="1fd92-145">Помимо вышесказанного, рекомендуется *удалить* следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="1fd92-145">In addition to the above, it is recommended to *remove* the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
   <span data-ttu-id="1fd92-146">Графическая и "тихая" загрузка бесполезны в облачной среде, в которой нам нужно, чтобы все журналы отправлялись на последовательный порт.</span><span class="sxs-lookup"><span data-stu-id="1fd92-146">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span>
   
   <span data-ttu-id="1fd92-147">При желании можно настроить параметр `crashkernel`, однако учитывайте, что он сокращает объем доступной памяти в виртуальной машине на 128 МБ или более, что может оказаться проблемой в виртуальных машинах небольшого размера.</span><span class="sxs-lookup"><span data-stu-id="1fd92-147">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span></span>
10. <span data-ttu-id="1fd92-148">Убедитесь, что SSH-сервер установлен и настроен для включения во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="1fd92-148">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="1fd92-149">Обычно это сделано по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1fd92-149">This is usually the default.</span></span>
11. <span data-ttu-id="1fd92-150">Установите агент Linux для Azure, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="1fd92-150">Install the Azure Linux Agent by running the following command.</span></span> <span data-ttu-id="1fd92-151">Последней является версия 2.0.15.</span><span class="sxs-lookup"><span data-stu-id="1fd92-151">The latest version is 2.0.15.</span></span>
    
        # sudo yum install WALinuxAgent
    
    <span data-ttu-id="1fd92-152">Обратите внимание, что установка пакета WALinuxAgent приведет к удалению пакетов NetworkManager и NetworkManager-gnome, если они еще не были удалены, как описано в шаге 2.</span><span class="sxs-lookup"><span data-stu-id="1fd92-152">Note that installing the WALinuxAgent package will remove the NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 2.</span></span>
12. <span data-ttu-id="1fd92-153">Не создавайте пространство подкачки на диске с ОС.</span><span class="sxs-lookup"><span data-stu-id="1fd92-153">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="1fd92-154">Агент Linux для Azure может автоматически настраивать пространство подкачки с использованием диска на локальном ресурсе, подключенном к виртуальной машине после подготовки для работы в среде Azure.</span><span class="sxs-lookup"><span data-stu-id="1fd92-154">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="1fd92-155">Следует отметить, что локальный диск ресурсов является *временным* диском и должен быть очищен при отмене подготовки виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="1fd92-155">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="1fd92-156">После установки агента Linux для Azure (см. предыдущий шаг) измените следующие параметры в /etc/waagent.conf соответствующим образом:</span><span class="sxs-lookup"><span data-stu-id="1fd92-156">After installing the Azure Linux Agent (see previous step), modify the following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.
13. <span data-ttu-id="1fd92-157">Выполните следующие команды, чтобы отменить подготовку виртуальной машины и подготовить ее в Azure:</span><span class="sxs-lookup"><span data-stu-id="1fd92-157">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
14. <span data-ttu-id="1fd92-158">В диспетчере Hyper-V выберите **Действие -> Завершение работы**.</span><span class="sxs-lookup"><span data-stu-id="1fd92-158">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="1fd92-159">Виртуальный жесткий диск Linux готов к передаче в Azure.</span><span class="sxs-lookup"><span data-stu-id="1fd92-159">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

- - -
## <a name="oracle-linux-70"></a><span data-ttu-id="1fd92-160">Oracle Linux 7.0+</span><span class="sxs-lookup"><span data-stu-id="1fd92-160">Oracle Linux 7.0+</span></span>
<span data-ttu-id="1fd92-161">**Изменения в Oracle Linux 7**</span><span class="sxs-lookup"><span data-stu-id="1fd92-161">**Changes in Oracle Linux 7**</span></span>

<span data-ttu-id="1fd92-162">Подготовка виртуальной машины Oracle Linux 7 для Azure в значительной степени аналогична версии Oracle Linux 6, однако есть несколько важных отличий:</span><span class="sxs-lookup"><span data-stu-id="1fd92-162">Preparing an Oracle Linux 7 virtual machine for Azure is very similar to Oracle Linux 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="1fd92-163">В Azure поддерживается и совместимое ядро Red Hat, и Oracle UEK3.</span><span class="sxs-lookup"><span data-stu-id="1fd92-163">Both the Red Hat compatible kernel and Oracle's UEK3 are supported in Azure.</span></span>  <span data-ttu-id="1fd92-164">Рекомендуется использовать ядро UEK3.</span><span class="sxs-lookup"><span data-stu-id="1fd92-164">The UEK3 kernel is recommended.</span></span>
* <span data-ttu-id="1fd92-165">Пакет NetworkManager больше не конфликтует с агентом Azure Linux.</span><span class="sxs-lookup"><span data-stu-id="1fd92-165">The NetworkManager package no longer conflicts with the Azure Linux agent.</span></span> <span data-ttu-id="1fd92-166">Этот пакет устанавливается по умолчанию, и мы рекомендуем не удалять его.</span><span class="sxs-lookup"><span data-stu-id="1fd92-166">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="1fd92-167">В качестве загрузчика по умолчанию теперь используется GRUB2, поэтому изменилась процедура правки параметров ядра (см. ниже).</span><span class="sxs-lookup"><span data-stu-id="1fd92-167">GRUB2 is now used as the default bootloader, so the procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="1fd92-168">XFS теперь является файловой системой по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1fd92-168">XFS is now the default file system.</span></span> <span data-ttu-id="1fd92-169">При желании можно продолжать использование файловой системы ext4.</span><span class="sxs-lookup"><span data-stu-id="1fd92-169">The ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="1fd92-170">**Этапы настройки**</span><span class="sxs-lookup"><span data-stu-id="1fd92-170">**Configuration steps**</span></span>

1. <span data-ttu-id="1fd92-171">В диспетчере Hyper-V выберите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="1fd92-171">In Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="1fd92-172">Щелкните **Подключение** , чтобы открыть окно консоли для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="1fd92-172">Click **Connect** to open a console window for the virtual machine.</span></span>
3. <span data-ttu-id="1fd92-173">Создайте файл с именем **network** в каталоге `/etc/sysconfig/`. Файл должен содержать следующий текст:</span><span class="sxs-lookup"><span data-stu-id="1fd92-173">Create a file named **network** in the `/etc/sysconfig/` directory that contains the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
4. <span data-ttu-id="1fd92-174">Создайте файл с именем **ifcfg-eth0** в каталоге `/etc/sysconfig/network-scripts/`. Файл должен содержать следующий текст:</span><span class="sxs-lookup"><span data-stu-id="1fd92-174">Create a file named **ifcfg-eth0** in the `/etc/sysconfig/network-scripts/` directory that contains the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
5. <span data-ttu-id="1fd92-175">Переместите или удалите правила udev, чтобы не создавать статические правила для интерфейса Ethernet.</span><span class="sxs-lookup"><span data-stu-id="1fd92-175">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="1fd92-176">Эти правила приводят к появлению проблем при клонировании виртуальной машины в Microsoft Azure или Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="1fd92-176">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
6. <span data-ttu-id="1fd92-177">Убедитесь, что сетевая служба запускается во время загрузки, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1fd92-177">Ensure the network service will start at boot time by running the following command:</span></span>
   
        # sudo chkconfig network on
7. <span data-ttu-id="1fd92-178">Установите пакет python-pyasn1, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1fd92-178">Install the python-pyasn1 package by running the following command:</span></span>
   
        # sudo yum install python-pyasn1
8. <span data-ttu-id="1fd92-179">Выполните следующую команду, чтобы очистить текущие метаданные yum и установить все обновления:</span><span class="sxs-lookup"><span data-stu-id="1fd92-179">Run the following command to clear the current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all
        # sudo yum -y update
9. <span data-ttu-id="1fd92-180">Измените строку загрузки ядра в конфигурации grub, чтобы включить дополнительные параметры ядра для Azure.</span><span class="sxs-lookup"><span data-stu-id="1fd92-180">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="1fd92-181">Для этого откройте файл /etc/default/grub в текстовом редакторе и измените параметр `GRUB_CMDLINE_LINUX`, например:</span><span class="sxs-lookup"><span data-stu-id="1fd92-181">To do this open "/etc/default/grub" in a text editor and edit the `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="1fd92-182">Это также гарантирует отправку всех сообщений консоли на первый последовательный порт, что может помочь технической поддержке Azure в плане отладки.</span><span class="sxs-lookup"><span data-stu-id="1fd92-182">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="1fd92-183">Также будут отключены новые соглашения OEL 7 об именовании для сетевых адаптеров.</span><span class="sxs-lookup"><span data-stu-id="1fd92-183">It also turns off the new OEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="1fd92-184">Помимо вышесказанного, рекомендуется *удалить* следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="1fd92-184">In addition to the above, it is recommended to *remove* the following parameters:</span></span>
   
       rhgb quiet crashkernel=auto
   
   <span data-ttu-id="1fd92-185">Графическая и "тихая" загрузка бесполезны в облачной среде, в которой нам нужно, чтобы все журналы отправлялись на последовательный порт.</span><span class="sxs-lookup"><span data-stu-id="1fd92-185">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span>
   
   <span data-ttu-id="1fd92-186">При желании можно настроить параметр `crashkernel`, однако учитывайте, что он сокращает объем доступной памяти в виртуальной машине на 128 МБ или более, что может оказаться проблемой в виртуальных машинах небольшого размера.</span><span class="sxs-lookup"><span data-stu-id="1fd92-186">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span></span>
10. <span data-ttu-id="1fd92-187">После внесения изменений в файл "/etc/default/grub", как указано выше, выполните следующую команду для повторного создания конфигурации grub:</span><span class="sxs-lookup"><span data-stu-id="1fd92-187">Once you are done editing "/etc/default/grub" per above, run the following command to rebuild the grub configuration:</span></span>
    
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg
11. <span data-ttu-id="1fd92-188">Убедитесь, что SSH-сервер установлен и настроен для включения во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="1fd92-188">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="1fd92-189">Обычно это сделано по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1fd92-189">This is usually the default.</span></span>
12. <span data-ttu-id="1fd92-190">Установите агент Linux для Azure, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1fd92-190">Install the Azure Linux Agent by running the following command:</span></span>
    
        # sudo yum install WALinuxAgent
        # sudo systemctl enable waagent
13. <span data-ttu-id="1fd92-191">Не создавайте пространство подкачки на диске с ОС.</span><span class="sxs-lookup"><span data-stu-id="1fd92-191">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="1fd92-192">Агент Linux для Azure может автоматически настраивать пространство подкачки с использованием диска на локальном ресурсе, подключенном к виртуальной машине после подготовки для работы в среде Azure.</span><span class="sxs-lookup"><span data-stu-id="1fd92-192">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="1fd92-193">Следует отметить, что локальный диск ресурсов является *временным* диском и должен быть очищен при отмене подготовки виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="1fd92-193">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="1fd92-194">После установки агента Linux для Azure (см. предыдущий шаг) измените следующие параметры в /etc/waagent.conf соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="1fd92-194">After installing the Azure Linux Agent (see the previous step), modify the following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.
14. <span data-ttu-id="1fd92-195">Выполните следующие команды, чтобы отменить подготовку виртуальной машины и подготовить ее в Azure:</span><span class="sxs-lookup"><span data-stu-id="1fd92-195">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
15. <span data-ttu-id="1fd92-196">В диспетчере Hyper-V выберите **Действие -> Завершение работы**.</span><span class="sxs-lookup"><span data-stu-id="1fd92-196">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="1fd92-197">Виртуальный жесткий диск Linux готов к передаче в Azure.</span><span class="sxs-lookup"><span data-stu-id="1fd92-197">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1fd92-198">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1fd92-198">Next steps</span></span>
<span data-ttu-id="1fd92-199">Теперь вы можете создавать новые виртуальные машины в Azure с помощью VHD-файла системы Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="1fd92-199">You're now ready to use your Oracle Linux .vhd to create new virtual machines in Azure.</span></span> <span data-ttu-id="1fd92-200">Если вы загружаете VHD-файл в Azure впервые, обратитесь к шагам 2 и 3 в статье [Создание и загрузка виртуального жесткого диска, содержащего операционную систему Linux](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1fd92-200">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

