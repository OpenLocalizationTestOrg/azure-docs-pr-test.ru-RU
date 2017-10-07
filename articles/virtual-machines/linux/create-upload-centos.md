---
title: "aaaCreate и передачи на основе CentOS Linux VHD в Azure"
description: "Узнайте toocreate и отправить в Azure виртуального жесткого диска (VHD), содержащий операционную систему на основе CentOS Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 0e518e92-e981-43f4-b12c-9cba1064c4bb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 78f36be1d36e3d44cb836c912d143f2c9a72aab5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-centos-based-virtual-machine-for-azure"></a><span data-ttu-id="7cbea-103">Подготовка виртуальной машины на основе CentOS для Azure</span><span class="sxs-lookup"><span data-stu-id="7cbea-103">Prepare a CentOS-based virtual machine for Azure</span></span>
* [<span data-ttu-id="7cbea-104">Подготовка виртуальной машины CentOS 6.x для Azure</span><span class="sxs-lookup"><span data-stu-id="7cbea-104">Prepare a CentOS 6.x virtual machine for Azure</span></span>](#centos-6x)
* [<span data-ttu-id="7cbea-105">Подготовка виртуальной машины CentOS 7.0+ для Azure</span><span class="sxs-lookup"><span data-stu-id="7cbea-105">Prepare a CentOS 7.0+ virtual machine for Azure</span></span>](#centos-70)

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="7cbea-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7cbea-106">Prerequisites</span></span>
<span data-ttu-id="7cbea-107">В этой статье предполагается, что вы уже установили CentOS (или аналогичные производных) Linux tooa виртуального жесткого диска операционной системы.</span><span class="sxs-lookup"><span data-stu-id="7cbea-107">This article assumes that you have already installed a CentOS (or similar derivative) Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="7cbea-108">Существуют несколько средства toocreate VHD-файлы, например решение виртуализации, таких как Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="7cbea-108">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="7cbea-109">Инструкции см. в разделе [Установка hello роль Hyper-V и настройка виртуальной машины](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="7cbea-109">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="7cbea-110">**Замечания по установке CentOS**</span><span class="sxs-lookup"><span data-stu-id="7cbea-110">**CentOS installation notes**</span></span>

* <span data-ttu-id="7cbea-111">Дополнительные сведения о подготовке Linux для Azure см. в разделе [Общие замечания по установке Linux](create-upload-generic.md#general-linux-installation-notes).</span><span class="sxs-lookup"><span data-stu-id="7cbea-111">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="7cbea-112">Hello формат VHDX не поддерживается только в Azure, **фиксированный VHD**.</span><span class="sxs-lookup"><span data-stu-id="7cbea-112">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="7cbea-113">Можно преобразовать формат tooVHD hello диска, с помощью диспетчера Hyper-V или hello командлет convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="7cbea-113">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span> <span data-ttu-id="7cbea-114">Если вы используете VirtualBox этого нужно выбрать **фиксированный размер** в отличие от toohello по умолчанию динамически назначаемых при создании диска hello.</span><span class="sxs-lookup"><span data-stu-id="7cbea-114">If you are using VirtualBox this means selecting **Fixed size** as opposed toohello default dynamically allocated when creating hello disk.</span></span>
* <span data-ttu-id="7cbea-115">При установке системы Linux hello *рекомендуется* использовать стандартные секции, а не LVM (часто hello по умолчанию для многих установок).</span><span class="sxs-lookup"><span data-stu-id="7cbea-115">When installing hello Linux system it is *recommended* that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="7cbea-116">Это позволит избежать конфликтов имен LVM с клонированные виртуальные машины, особенно в том случае, если диска ОС, когда-либо должен tooanother toobe присоединенного идентичные виртуальной Машины для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="7cbea-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother identical VM for troubleshooting.</span></span> <span data-ttu-id="7cbea-117">Для дисков данных можно использовать [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) или [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7cbea-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="7cbea-118">Требуется поддержка ядра для монтирования файловых систем UDF.</span><span class="sxs-lookup"><span data-stu-id="7cbea-118">Kernel support for mounting UDF file systems is required.</span></span> <span data-ttu-id="7cbea-119">При первой загрузке в Azure hello настройке подготовки передается через формате UDF носителей, присоединенных toohello гостевой toohello виртуальной Машины с Linux.</span><span class="sxs-lookup"><span data-stu-id="7cbea-119">At first boot on Azure hello provisioning configuration is passed toohello Linux VM via UDF-formatted media that is attached toohello guest.</span></span> <span data-ttu-id="7cbea-120">агент Azure Linux Hello должно быть может toomount hello UDF файл системы tooread свою конфигурацию и подготовить hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="7cbea-120">hello Azure Linux agent must be able toomount hello UDF file system tooread its configuration and provision hello VM.</span></span>
* <span data-ttu-id="7cbea-121">Версии ядра Linux ниже 2.6.37 не поддерживают NUMA в Hyper-V с виртуальными машинами большего размера.</span><span class="sxs-lookup"><span data-stu-id="7cbea-121">Linux kernel versions below 2.6.37 do not support NUMA on Hyper-V with larger VM sizes.</span></span> <span data-ttu-id="7cbea-122">Эту проблему в основном влияет на старых распределения, с использованием hello вышестоящих ядра Red Hat 2.6.32 и была исправлена в RHEL 6.6 (ядра 2.6.32 504).</span><span class="sxs-lookup"><span data-stu-id="7cbea-122">This issue primarily impacts older distributions using hello upstream Red Hat 2.6.32 kernel, and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="7cbea-123">Здравствуйте, систем под управлением старше 2.6.37 пользовательские ядер или на основе RHEL версии ядра более старые, чем 2.6.32-504 необходимо задать параметр загрузки `numa=off` командной строки в grub.conf ядра hello.</span><span class="sxs-lookup"><span data-stu-id="7cbea-123">Systems running custom kernels older than 2.6.37, or RHEL-based kernels older than 2.6.32-504 must set hello boot parameter `numa=off` on hello kernel command-line in grub.conf.</span></span> <span data-ttu-id="7cbea-124">Дополнительные сведения см. в статье базы знаний Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="7cbea-124">For more information see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="7cbea-125">Не настраивайте переключения секции на диске ОС hello.</span><span class="sxs-lookup"><span data-stu-id="7cbea-125">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="7cbea-126">агент Linux Hello может быть настроенный toocreate файл подкачки на диске временного ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="7cbea-126">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="7cbea-127">Дополнительные сведения об этом можно найти в hello описанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="7cbea-127">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="7cbea-128">Все виртуальные жесткие диски hello должны иметь размеры, кратные 1 МБ.</span><span class="sxs-lookup"><span data-stu-id="7cbea-128">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="centos-6x"></a><span data-ttu-id="7cbea-129">CentOS 6.x</span><span class="sxs-lookup"><span data-stu-id="7cbea-129">CentOS 6.x</span></span>

1. <span data-ttu-id="7cbea-130">В диспетчере Hyper-V выберите виртуальную машину hello.</span><span class="sxs-lookup"><span data-stu-id="7cbea-130">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="7cbea-131">Нажмите кнопку **Connect** tooopen окно консоли для виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="7cbea-131">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="7cbea-132">CentOS 6 NetworkManager могут помешать hello агента Azure Linux.</span><span class="sxs-lookup"><span data-stu-id="7cbea-132">In CentOS 6, NetworkManager can interfere with hello Azure Linux agent.</span></span> <span data-ttu-id="7cbea-133">Удаление этого пакета, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="7cbea-133">Uninstall this package by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="7cbea-134">Создание или изменение файла hello `/etc/sysconfig/network` и добавьте следующий текст hello:</span><span class="sxs-lookup"><span data-stu-id="7cbea-134">Create or edit hello file `/etc/sysconfig/network` and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="7cbea-135">Создание или изменение файла hello `/etc/sysconfig/network-scripts/ifcfg-eth0` и добавьте следующий текст hello:</span><span class="sxs-lookup"><span data-stu-id="7cbea-135">Create or edit hello file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="7cbea-136">Измените tooavoid правила udev создания статические правила для hello интерфейсы Ethernet.</span><span class="sxs-lookup"><span data-stu-id="7cbea-136">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="7cbea-137">Эти правила приводят к появлению проблем при клонировании виртуальной машины в Microsoft Azure или Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="7cbea-137">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="7cbea-138">Убедитесь, что hello сети служба будет запущена во время загрузки, выполнив следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="7cbea-138">Ensure hello network service will start at boot time by running hello following command:</span></span>
   
        # sudo chkconfig network on

8. <span data-ttu-id="7cbea-139">При желании toouse hello OpenLogic зеркала, размещенных в hello центрами обработки данных Azure, затем замените hello `/etc/yum.repos.d/CentOS-Base.repo` файл с hello следующих репозиториев.</span><span class="sxs-lookup"><span data-stu-id="7cbea-139">If you would like toouse hello OpenLogic mirrors that are hosted within hello Azure datacenters, then replace hello `/etc/yum.repos.d/CentOS-Base.repo` file with hello following repositories.</span></span>  <span data-ttu-id="7cbea-140">Также будет добавлен hello **[openlogic]** репозитории, которая включает в себя дополнительные пакеты, такие как агент Azure Linux hello:</span><span class="sxs-lookup"><span data-stu-id="7cbea-140">This will also add hello **[openlogic]** repository that includes additional packages such as hello Azure Linux agent:</span></span>

        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #contrib - packages by Centos Users
        [contrib]
        name=CentOS-$releasever - Contrib
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=contrib&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/contrib/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

    >[!Note]
    <span data-ttu-id="7cbea-141">Hello остальные разделы руководства предполагается используется по крайней мере hello `[openlogic]` репозитория, в которой будет используется tooinstall hello Azure Linux agent ниже.</span><span class="sxs-lookup"><span data-stu-id="7cbea-141">hello rest of this guide will assume you are using at least hello `[openlogic]` repo, which will be used tooinstall hello Azure Linux agent below.</span></span>


9. <span data-ttu-id="7cbea-142">Добавьте следующие строки too/etc/yum.conf hello:</span><span class="sxs-lookup"><span data-stu-id="7cbea-142">Add hello following line too/etc/yum.conf:</span></span>
    
        http_caching=packages

10. <span data-ttu-id="7cbea-143">Выполните hello, следующая команда tooclear hello текущей yum метаданных и обновления hello системы hello последние пакеты:</span><span class="sxs-lookup"><span data-stu-id="7cbea-143">Run hello following command tooclear hello current yum metadata and update hello system with hello latest packages:</span></span>
    
        # yum clean all

    <span data-ttu-id="7cbea-144">При создании изображения для более ранней версии CentOS рекомендуется tooupdate, все hello последние пакеты toohello:</span><span class="sxs-lookup"><span data-stu-id="7cbea-144">Unless you are creating an image for an older version of CentOS, it is recommended tooupdate all hello packages toohello latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="7cbea-145">После выполнения этой команды может потребоваться перезагрузка.</span><span class="sxs-lookup"><span data-stu-id="7cbea-145">A reboot may be required after running this command.</span></span>

11. <span data-ttu-id="7cbea-146">(Необязательно) Установите драйверы hello hello службы интеграции Linux (LIS).</span><span class="sxs-lookup"><span data-stu-id="7cbea-146">(Optional) Install hello drivers for hello Linux Integration Services (LIS).</span></span>
   
    >[!IMPORTANT]
    <span data-ttu-id="7cbea-147">шаг Hello — **необходимые** для CentOS 6,3 и более ранних и необязательным для более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="7cbea-147">hello step is **required** for CentOS 6.3 and earlier, and optional for later releases.</span></span>

        # sudo rpm -e hypervkvpd  ## (may return error if not installed, that's OK)
        # sudo yum install microsoft-hyper-v

    <span data-ttu-id="7cbea-148">Кроме того, необходимо выполнить инструкции по ручной установке hello hello [страница загрузки LIS](https://go.microsoft.com/fwlink/?linkid=403033) tooinstall hello RPM на ВМ.</span><span class="sxs-lookup"><span data-stu-id="7cbea-148">Alternatively, you can follow hello manual installation instructions on hello [LIS download page](https://go.microsoft.com/fwlink/?linkid=403033) tooinstall hello RPM onto your VM.</span></span>
 
12. <span data-ttu-id="7cbea-149">Установите агент Azure Linux hello и зависимости:</span><span class="sxs-lookup"><span data-stu-id="7cbea-149">Install hello Azure Linux Agent and dependencies:</span></span>
    
        # sudo yum install python-pyasn1 WALinuxAgent
    
    <span data-ttu-id="7cbea-150">пакет WALinuxAgent Hello приведет к удалению hello NetworkManager и NetworkManager gnome пакеты, если они не были уже удалены как описано в шаге 3.</span><span class="sxs-lookup"><span data-stu-id="7cbea-150">hello WALinuxAgent package will remove hello NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 3.</span></span>


13. <span data-ttu-id="7cbea-151">Измените строку загрузки ядра hello в параметры grub tooinclude дополнительные ядра для Azure.</span><span class="sxs-lookup"><span data-stu-id="7cbea-151">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="7cbea-152">toodo, откройте `/boot/grub/menu.lst` в текстовом редакторе, убедитесь, что ядра по умолчанию hello включает hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="7cbea-152">toodo this, open `/boot/grub/menu.lst` in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="7cbea-153">Это также гарантирует все консоли сообщения отправляются toohello первый последовательный порт, который может помочь Azure поддержка с помощью отладки проблем.</span><span class="sxs-lookup"><span data-stu-id="7cbea-153">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="7cbea-154">В дополнение к этому toohello выше, рекомендуется слишком*удалить* hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="7cbea-154">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="7cbea-155">Графический quiet начальной загрузки, не используются в облачной среде, где мы хотим, чтобы все журналы toobe hello, отправляемых toohello последовательного порта.</span><span class="sxs-lookup"><span data-stu-id="7cbea-155">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>  <span data-ttu-id="7cbea-156">Hello `crashkernel` возможность влево, при желании настроить, но следует заметить, что этот параметр приведет к уменьшению hello объем доступной памяти в hello виртуальная машина по 128 МБ или больше, которое может быть проблематично на hello меньшего размера виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="7cbea-156">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>

    >[!Important]
    <span data-ttu-id="7cbea-157">CentOS версии 6.5 и более ранних версиях необходимо также задать параметр ядра hello `numa=off`.</span><span class="sxs-lookup"><span data-stu-id="7cbea-157">CentOS 6.5 and earlier must also set hello kernel parameter `numa=off`.</span></span> <span data-ttu-id="7cbea-158">См. посвященный Red Hat [раздел 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="7cbea-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

14. <span data-ttu-id="7cbea-159">Убедитесь, что hello SSH сервер установлен и настроен toostart во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="7cbea-159">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="7cbea-160">Обычно это происходит по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="7cbea-160">This is usually hello default.</span></span>

15. <span data-ttu-id="7cbea-161">Не создавайте подкачки на диске ОС hello.</span><span class="sxs-lookup"><span data-stu-id="7cbea-161">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="7cbea-162">Hello Azure Linux Agent может автоматически настроить подкачки с помощью hello локальный диск ресурсов, toohello подключенных виртуальных Машин после подготовки в Azure.</span><span class="sxs-lookup"><span data-stu-id="7cbea-162">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="7cbea-163">Обратите внимание, что hello локальный диск ресурсов *временные* диск, а также может очищаться при отмененной подготовкой hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="7cbea-163">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="7cbea-164">После установки hello Azure Linux Agent (см. выше), измените следующие параметры в hello `/etc/waagent.conf` соответствующим образом:</span><span class="sxs-lookup"><span data-stu-id="7cbea-164">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. <span data-ttu-id="7cbea-165">Запустите следующие команды toodeprovision hello виртуальной машины hello и подготовить его для подготовки в Azure:</span><span class="sxs-lookup"><span data-stu-id="7cbea-165">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

17. <span data-ttu-id="7cbea-166">В диспетчере Hyper-V выберите **Действие -> Завершение работы**.</span><span class="sxs-lookup"><span data-stu-id="7cbea-166">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="7cbea-167">ДИСК Linux имеет теперь готовы toobe отправлен tooAzure.</span><span class="sxs-lookup"><span data-stu-id="7cbea-167">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>


- - -
## <a name="centos-70"></a><span data-ttu-id="7cbea-168">CentOS 7.0+</span><span class="sxs-lookup"><span data-stu-id="7cbea-168">CentOS 7.0+</span></span>
<span data-ttu-id="7cbea-169">**Изменения в CentOS 7 (и аналогичных производных версиях)**</span><span class="sxs-lookup"><span data-stu-id="7cbea-169">**Changes in CentOS 7 (and similar derivatives)**</span></span>

<span data-ttu-id="7cbea-170">Подготовка виртуальной машины CentOS 7 для Azure — очень похожа tooCentOS 6, однако существует несколько важных различий, обратите внимание:</span><span class="sxs-lookup"><span data-stu-id="7cbea-170">Preparing a CentOS 7 virtual machine for Azure is very similar tooCentOS 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="7cbea-171">Hello NetworkManager пакета больше не конфликтует с агентом Azure Linux hello.</span><span class="sxs-lookup"><span data-stu-id="7cbea-171">hello NetworkManager package no longer conflicts with hello Azure Linux agent.</span></span> <span data-ttu-id="7cbea-172">Этот пакет устанавливается по умолчанию, и мы рекомендуем не удалять его.</span><span class="sxs-lookup"><span data-stu-id="7cbea-172">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="7cbea-173">GRUB2 сейчас используется как hello загрузчика по умолчанию, поэтому hello процедуру для редактирования параметров ядра изменилась (см. ниже).</span><span class="sxs-lookup"><span data-stu-id="7cbea-173">GRUB2 is now used as hello default bootloader, so hello procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="7cbea-174">XFS сейчас файловой системы по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="7cbea-174">XFS is now hello default file system.</span></span> <span data-ttu-id="7cbea-175">по-прежнему можно использовать Hello ext4 файловой системы, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="7cbea-175">hello ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="7cbea-176">**Этапы настройки**</span><span class="sxs-lookup"><span data-stu-id="7cbea-176">**Configuration Steps**</span></span>

1. <span data-ttu-id="7cbea-177">В диспетчере Hyper-V выберите виртуальную машину hello.</span><span class="sxs-lookup"><span data-stu-id="7cbea-177">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="7cbea-178">Нажмите кнопку **Connect** tooopen окно консоли для виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="7cbea-178">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="7cbea-179">Создание или изменение файла hello `/etc/sysconfig/network` и добавьте следующий текст hello:</span><span class="sxs-lookup"><span data-stu-id="7cbea-179">Create or edit hello file `/etc/sysconfig/network` and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="7cbea-180">Создание или изменение файла hello `/etc/sysconfig/network-scripts/ifcfg-eth0` и добавьте следующий текст hello:</span><span class="sxs-lookup"><span data-stu-id="7cbea-180">Create or edit hello file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="7cbea-181">Измените tooavoid правила udev создания статические правила для hello интерфейсы Ethernet.</span><span class="sxs-lookup"><span data-stu-id="7cbea-181">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="7cbea-182">Эти правила приводят к появлению проблем при клонировании виртуальной машины в Microsoft Azure или Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="7cbea-182">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

6. <span data-ttu-id="7cbea-183">При желании toouse hello OpenLogic зеркала, размещенных в hello центрами обработки данных Azure, затем замените hello `/etc/yum.repos.d/CentOS-Base.repo` файл с hello следующих репозиториев.</span><span class="sxs-lookup"><span data-stu-id="7cbea-183">If you would like toouse hello OpenLogic mirrors that are hosted within hello Azure datacenters, then replace hello `/etc/yum.repos.d/CentOS-Base.repo` file with hello following repositories.</span></span>  <span data-ttu-id="7cbea-184">Также будет добавлен hello **[openlogic]** репозитории, которая содержит пакеты для агента Azure Linux hello:</span><span class="sxs-lookup"><span data-stu-id="7cbea-184">This will also add hello **[openlogic]** repository that includes packages for hello Azure Linux agent:</span></span>
   
        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

    >[!Note]
    <span data-ttu-id="7cbea-185">Hello остальные разделы руководства предполагается используется по крайней мере hello `[openlogic]` репозитория, в которой будет используется tooinstall hello Azure Linux agent ниже.</span><span class="sxs-lookup"><span data-stu-id="7cbea-185">hello rest of this guide will assume you are using at least hello `[openlogic]` repo, which will be used tooinstall hello Azure Linux agent below.</span></span>

7. <span data-ttu-id="7cbea-186">Выполнения hello следующую команду текущих метаданных yum tooclear hello и установке обновлений:</span><span class="sxs-lookup"><span data-stu-id="7cbea-186">Run hello following command tooclear hello current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all

    <span data-ttu-id="7cbea-187">При создании изображения для более ранней версии CentOS рекомендуется tooupdate, все hello последние пакеты toohello:</span><span class="sxs-lookup"><span data-stu-id="7cbea-187">Unless you are creating an image for an older version of CentOS, it is recommended tooupdate all hello packages toohello latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="7cbea-188">После выполнения этой команды может потребоваться перезагрузка.</span><span class="sxs-lookup"><span data-stu-id="7cbea-188">A reboot maybe required after running this command.</span></span>

8. <span data-ttu-id="7cbea-189">Измените строку загрузки ядра hello в параметры grub tooinclude дополнительные ядра для Azure.</span><span class="sxs-lookup"><span data-stu-id="7cbea-189">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="7cbea-190">toodo, откройте `/etc/default/grub` в текстовом редакторе и измените hello `GRUB_CMDLINE_LINUX` параметра, например:</span><span class="sxs-lookup"><span data-stu-id="7cbea-190">toodo this, open `/etc/default/grub` in a text editor and edit hello `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="7cbea-191">Это также гарантирует все консоли сообщения отправляются toohello первый последовательный порт, который может помочь Azure поддержка с помощью отладки проблем.</span><span class="sxs-lookup"><span data-stu-id="7cbea-191">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="7cbea-192">Он также отключает новые соглашения об именах hello CentOS 7 для сетевых адаптеров.</span><span class="sxs-lookup"><span data-stu-id="7cbea-192">It also turns off hello new CentOS 7 naming conventions for NICs.</span></span> <span data-ttu-id="7cbea-193">В дополнение к этому toohello выше, рекомендуется слишком*удалить* hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="7cbea-193">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="7cbea-194">Графический quiet начальной загрузки, не используются в облачной среде, где мы хотим, чтобы все журналы toobe hello, отправляемых toohello последовательного порта.</span><span class="sxs-lookup"><span data-stu-id="7cbea-194">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="7cbea-195">Hello `crashkernel` возможность влево, при желании настроить, но следует заметить, что этот параметр приведет к уменьшению hello объем доступной памяти в hello виртуальная машина по 128 МБ или больше, которое может быть проблематично на hello меньшего размера виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="7cbea-195">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>

9. <span data-ttu-id="7cbea-196">После завершения редактирования `/etc/default/grub` каждого выше, запустите hello, следующая команда toorebuild hello grub конфигурация:</span><span class="sxs-lookup"><span data-stu-id="7cbea-196">Once you are done editing `/etc/default/grub` per above, run hello following command toorebuild hello grub configuration:</span></span>
   
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="7cbea-197">Если создание образа hello из **VMWare, VirtualBox или KVM:** драйверы hello Hyper-V убедитесь, что включены в hello initramfs:</span><span class="sxs-lookup"><span data-stu-id="7cbea-197">If building hello image from **VMWare, VirtualBox or KVM:** Ensure hello Hyper-V drivers are included in hello initramfs:</span></span>
   
   <span data-ttu-id="7cbea-198">Измените файл `/etc/dracut.conf`, добавив в него следующее содержимое:</span><span class="sxs-lookup"><span data-stu-id="7cbea-198">Edit `/etc/dracut.conf`, add content:</span></span>
   
        add_drivers+=”hv_vmbus hv_netvsc hv_storvsc”
   
   <span data-ttu-id="7cbea-199">Заново создать hello initramfs.</span><span class="sxs-lookup"><span data-stu-id="7cbea-199">Rebuild hello initramfs:</span></span>
   
        # sudo dracut –f -v

11. <span data-ttu-id="7cbea-200">Установите агент Azure Linux hello и зависимости:</span><span class="sxs-lookup"><span data-stu-id="7cbea-200">Install hello Azure Linux Agent and dependencies:</span></span>

        # sudo yum install python-pyasn1 WALinuxAgent
        # sudo systemctl enable waagent

12. <span data-ttu-id="7cbea-201">Не создавайте подкачки на диске ОС hello.</span><span class="sxs-lookup"><span data-stu-id="7cbea-201">Do not create swap space on hello OS disk.</span></span>
   
   <span data-ttu-id="7cbea-202">Hello Azure Linux Agent может автоматически настроить подкачки с помощью hello локальный диск ресурсов, toohello подключенных виртуальных Машин после подготовки в Azure.</span><span class="sxs-lookup"><span data-stu-id="7cbea-202">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="7cbea-203">Обратите внимание, что hello локальный диск ресурсов *временные* диск, а также может очищаться при отмененной подготовкой hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="7cbea-203">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="7cbea-204">После установки hello Azure Linux Agent (см. выше), измените следующие параметры в hello `/etc/waagent.conf` соответствующим образом:</span><span class="sxs-lookup"><span data-stu-id="7cbea-204">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>
   
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. <span data-ttu-id="7cbea-205">Запустите следующие команды toodeprovision hello виртуальной машины hello и подготовить его для подготовки в Azure:</span><span class="sxs-lookup"><span data-stu-id="7cbea-205">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

14. <span data-ttu-id="7cbea-206">В диспетчере Hyper-V выберите **Действие -> Завершение работы**.</span><span class="sxs-lookup"><span data-stu-id="7cbea-206">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="7cbea-207">ДИСК Linux имеет теперь готовы toobe отправлен tooAzure.</span><span class="sxs-lookup"><span data-stu-id="7cbea-207">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7cbea-208">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7cbea-208">Next steps</span></span>
<span data-ttu-id="7cbea-209">Вы являетесь теперь готовы toouse CentOS Linux виртуальный жесткий диск toocreate новых виртуальных машин в Azure.</span><span class="sxs-lookup"><span data-stu-id="7cbea-209">You're now ready toouse your CentOS Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="7cbea-210">Если это первый раз, что идет Отправка tooAzure файл .vhd hello hello см. шаги 2 и 3 в [Создание и передача виртуального жесткого диска, который содержит операционную систему Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7cbea-210">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

