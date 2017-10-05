---
title: "Создание и передача виртуального жесткого диска с ОС Linux на основе CentOS в Azure"
description: "Узнайте, как создать и передать виртуальный жесткий диск (VHD-файл) Azure, содержащий операционную систему Linux на основе CentOS"
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
ms.openlocfilehash: 010f4b05b35fa1f31c14f34a5fae9298fcd831e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-a-centos-based-virtual-machine-for-azure"></a><span data-ttu-id="56a89-103">Подготовка виртуальной машины на основе CentOS для Azure</span><span class="sxs-lookup"><span data-stu-id="56a89-103">Prepare a CentOS-based virtual machine for Azure</span></span>
* [<span data-ttu-id="56a89-104">Подготовка виртуальной машины CentOS 6.x для Azure</span><span class="sxs-lookup"><span data-stu-id="56a89-104">Prepare a CentOS 6.x virtual machine for Azure</span></span>](#centos-6x)
* [<span data-ttu-id="56a89-105">Подготовка виртуальной машины CentOS 7.0+ для Azure</span><span class="sxs-lookup"><span data-stu-id="56a89-105">Prepare a CentOS 7.0+ virtual machine for Azure</span></span>](#centos-70)

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="56a89-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="56a89-106">Prerequisites</span></span>
<span data-ttu-id="56a89-107">В этой статье предполагается, что вы уже установили операционную систему CentOS Linux (или аналогичную производную) на виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="56a89-107">This article assumes that you have already installed a CentOS (or similar derivative) Linux operating system to a virtual hard disk.</span></span> <span data-ttu-id="56a89-108">Существует несколько средств для создания VHD-файлов, например решение для виртуализации, такое как Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="56a89-108">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="56a89-109">Инструкции см. в разделе [Установка роли Hyper-V и настройка виртуальной машины](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="56a89-109">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="56a89-110">**Замечания по установке CentOS**</span><span class="sxs-lookup"><span data-stu-id="56a89-110">**CentOS installation notes**</span></span>

* <span data-ttu-id="56a89-111">Дополнительные сведения о подготовке Linux для Azure см. в разделе [Общие замечания по установке Linux](create-upload-generic.md#general-linux-installation-notes).</span><span class="sxs-lookup"><span data-stu-id="56a89-111">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="56a89-112">Формат VHDX не поддерживается в Azure, поддерживается только **фиксированный VHD**.</span><span class="sxs-lookup"><span data-stu-id="56a89-112">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="56a89-113">Можно преобразовать диск в формат VHD с помощью диспетчера Hyper-V или командлета convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="56a89-113">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span></span> <span data-ttu-id="56a89-114">Если вы используете VirtualBox, при создании диска по умолчанию нужно выбрать **фиксированный размер** вместо динамически выделяемого.</span><span class="sxs-lookup"><span data-stu-id="56a89-114">If you are using VirtualBox this means selecting **Fixed size** as opposed to the default dynamically allocated when creating the disk.</span></span>
* <span data-ttu-id="56a89-115">При установке системы Linux *рекомендуется* использовать стандартные разделы, а не LVM (как правило, значение по умолчанию во многих дистрибутивах).</span><span class="sxs-lookup"><span data-stu-id="56a89-115">When installing the Linux system it is *recommended* that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="56a89-116">Это позволит избежать конфликта имен LVM c клонированными виртуальными машинами, особенно если диск с OC может быть подключен к другой идентичной виртуальной машине в целях устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="56a89-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another identical VM for troubleshooting.</span></span> <span data-ttu-id="56a89-117">Для дисков данных можно использовать [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) или [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="56a89-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="56a89-118">Требуется поддержка ядра для монтирования файловых систем UDF.</span><span class="sxs-lookup"><span data-stu-id="56a89-118">Kernel support for mounting UDF file systems is required.</span></span> <span data-ttu-id="56a89-119">При первой загрузке в Azure конфигурация подготовки передается в виртуальную машину Linux через UDF-носитель, подключенный к гостевой машине.</span><span class="sxs-lookup"><span data-stu-id="56a89-119">At first boot on Azure the provisioning configuration is passed to the Linux VM via UDF-formatted media that is attached to the guest.</span></span> <span data-ttu-id="56a89-120">Агент Azure Linux должен иметь возможность подключать файловую систему UDF для считывания конфигурации и подготовки виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="56a89-120">The Azure Linux agent must be able to mount the UDF file system to read its configuration and provision the VM.</span></span>
* <span data-ttu-id="56a89-121">Версии ядра Linux ниже 2.6.37 не поддерживают NUMA в Hyper-V с виртуальными машинами большего размера.</span><span class="sxs-lookup"><span data-stu-id="56a89-121">Linux kernel versions below 2.6.37 do not support NUMA on Hyper-V with larger VM sizes.</span></span> <span data-ttu-id="56a89-122">Эта проблема влияет в основном на дистрибутивы более ранних версий, в которых используется исходное ядро Red Hat 2.6.32, и была исправлена в RHEL 6.6 (kernel-2.6.32-504).</span><span class="sxs-lookup"><span data-stu-id="56a89-122">This issue primarily impacts older distributions using the upstream Red Hat 2.6.32 kernel, and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="56a89-123">В системах под управлением модифицированных ядер старше версии 2.6.37 или ядер RHEL старше 2.6.32-504 в командной строке ядра необходимо задать параметр загрузки `numa=off` в файле grub.conf.</span><span class="sxs-lookup"><span data-stu-id="56a89-123">Systems running custom kernels older than 2.6.37, or RHEL-based kernels older than 2.6.32-504 must set the boot parameter `numa=off` on the kernel command-line in grub.conf.</span></span> <span data-ttu-id="56a89-124">Дополнительные сведения см. в статье базы знаний Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="56a89-124">For more information see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="56a89-125">Не настраивайте раздел подкачки на диске с ОС.</span><span class="sxs-lookup"><span data-stu-id="56a89-125">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="56a89-126">Можно настроить агент Linux для создания файла подкачки на временном диске ресурсов.</span><span class="sxs-lookup"><span data-stu-id="56a89-126">The Linux agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="56a89-127">Дополнительные сведения описаны далее.</span><span class="sxs-lookup"><span data-stu-id="56a89-127">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="56a89-128">Все VHD-диски должны иметь размер, кратный 1 МБ.</span><span class="sxs-lookup"><span data-stu-id="56a89-128">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="centos-6x"></a><span data-ttu-id="56a89-129">CentOS 6.x</span><span class="sxs-lookup"><span data-stu-id="56a89-129">CentOS 6.x</span></span>

1. <span data-ttu-id="56a89-130">В диспетчере Hyper-V выберите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="56a89-130">In Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="56a89-131">Щелкните **Подключение** , чтобы открыть окно консоли для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="56a89-131">Click **Connect** to open a console window for the virtual machine.</span></span>

3. <span data-ttu-id="56a89-132">В CentOS 6 NetworkManager может мешать выполнению агента Linux для Azure.</span><span class="sxs-lookup"><span data-stu-id="56a89-132">In CentOS 6, NetworkManager can interfere with the Azure Linux agent.</span></span> <span data-ttu-id="56a89-133">Установите пакет, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="56a89-133">Uninstall this package by running the following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="56a89-134">Создайте или измените файл `/etc/sysconfig/network`, добавив следующий текст:</span><span class="sxs-lookup"><span data-stu-id="56a89-134">Create or edit the file `/etc/sysconfig/network` and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="56a89-135">Создайте или измените файл `/etc/sysconfig/network-scripts/ifcfg-eth0`, добавив следующий текст:</span><span class="sxs-lookup"><span data-stu-id="56a89-135">Create or edit the file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="56a89-136">Переместите или удалите правила udev, чтобы не создавать статические правила для интерфейса Ethernet.</span><span class="sxs-lookup"><span data-stu-id="56a89-136">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="56a89-137">Эти правила приводят к появлению проблем при клонировании виртуальной машины в Microsoft Azure или Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="56a89-137">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="56a89-138">Убедитесь, что сетевая служба запускается во время загрузки, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="56a89-138">Ensure the network service will start at boot time by running the following command:</span></span>
   
        # sudo chkconfig network on

8. <span data-ttu-id="56a89-139">Если вы хотите использовать зеркала OpenLogic, размещенные в центрах обработки данных Azure, замените файл `/etc/yum.repos.d/CentOS-Base.repo` следующими репозиториями.</span><span class="sxs-lookup"><span data-stu-id="56a89-139">If you would like to use the OpenLogic mirrors that are hosted within the Azure datacenters, then replace the `/etc/yum.repos.d/CentOS-Base.repo` file with the following repositories.</span></span>  <span data-ttu-id="56a89-140">При этом также будет добавлен репозиторий **[openlogic]**, который включает дополнительные пакеты, например для агента Linux для Azure:</span><span class="sxs-lookup"><span data-stu-id="56a89-140">This will also add the **[openlogic]** repository that includes additional packages such as the Azure Linux agent:</span></span>

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
    <span data-ttu-id="56a89-141">В этом руководстве предполагается, что вы используете по крайней мере репозиторий `[openlogic]`, который будет применяться при установке агента Linux для Azure.</span><span class="sxs-lookup"><span data-stu-id="56a89-141">The rest of this guide will assume you are using at least the `[openlogic]` repo, which will be used to install the Azure Linux agent below.</span></span>


9. <span data-ttu-id="56a89-142">Добавьте следующую строку в файл /etc/yum.conf:</span><span class="sxs-lookup"><span data-stu-id="56a89-142">Add the following line to /etc/yum.conf:</span></span>
    
        http_caching=packages

10. <span data-ttu-id="56a89-143">Выполните следующую команду, чтобы очистить текущие метаданные yum и установить в системе последние обновления:</span><span class="sxs-lookup"><span data-stu-id="56a89-143">Run the following command to clear the current yum metadata and update the system with the latest packages:</span></span>
    
        # yum clean all

    <span data-ttu-id="56a89-144">Если создается образ для более ранней версии CentOS, рекомендуется выполнить обновление всех пакетов до последней версии:</span><span class="sxs-lookup"><span data-stu-id="56a89-144">Unless you are creating an image for an older version of CentOS, it is recommended to update all the packages to the latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="56a89-145">После выполнения этой команды может потребоваться перезагрузка.</span><span class="sxs-lookup"><span data-stu-id="56a89-145">A reboot may be required after running this command.</span></span>

11. <span data-ttu-id="56a89-146">(Необязательно) Установите драйверы для служб интеграции Linux.</span><span class="sxs-lookup"><span data-stu-id="56a89-146">(Optional) Install the drivers for the Linux Integration Services (LIS).</span></span>
   
    >[!IMPORTANT]
    <span data-ttu-id="56a89-147">Этот шаг является **обязательным** для CentOS 6.3 и более ранних версий и необязательным для более поздних.</span><span class="sxs-lookup"><span data-stu-id="56a89-147">The step is **required** for CentOS 6.3 and earlier, and optional for later releases.</span></span>

        # sudo rpm -e hypervkvpd  ## (may return error if not installed, that's OK)
        # sudo yum install microsoft-hyper-v

    <span data-ttu-id="56a89-148">Или же следуйте инструкциям по установке на [странице скачивания служб интеграции Linux](https://go.microsoft.com/fwlink/?linkid=403033), чтобы установить RPM в образе.</span><span class="sxs-lookup"><span data-stu-id="56a89-148">Alternatively, you can follow the manual installation instructions on the [LIS download page](https://go.microsoft.com/fwlink/?linkid=403033) to install the RPM onto your VM.</span></span>
 
12. <span data-ttu-id="56a89-149">Установите агент Linux для Azure и зависимости:</span><span class="sxs-lookup"><span data-stu-id="56a89-149">Install the Azure Linux Agent and dependencies:</span></span>
    
        # sudo yum install python-pyasn1 WALinuxAgent
    
    <span data-ttu-id="56a89-150">Установка пакета WALinuxAgent приведет к удалению пакетов NetworkManager и NetworkManager-gnome, если они еще не удалены, как описано в шаге 3.</span><span class="sxs-lookup"><span data-stu-id="56a89-150">The WALinuxAgent package will remove the NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 3.</span></span>


13. <span data-ttu-id="56a89-151">Измените строку загрузки ядра в конфигурации grub, чтобы включить дополнительные параметры ядра для Azure.</span><span class="sxs-lookup"><span data-stu-id="56a89-151">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="56a89-152">Для этого откройте файл `/boot/grub/menu.lst` в текстовом редакторе и укажите для ядра по умолчанию следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="56a89-152">To do this, open `/boot/grub/menu.lst` in a text editor and ensure that the default kernel includes the following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="56a89-153">Это также гарантирует отправку всех сообщений консоли на первый последовательный порт, что может помочь технической поддержке Azure в плане отладки.</span><span class="sxs-lookup"><span data-stu-id="56a89-153">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="56a89-154">Помимо вышесказанного, рекомендуется *удалить* следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="56a89-154">In addition to the above, it is recommended to *remove* the following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="56a89-155">Графическая и "тихая" загрузка бесполезны в облачной среде, в которой нам нужно, чтобы все журналы отправлялись на последовательный порт.</span><span class="sxs-lookup"><span data-stu-id="56a89-155">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span>  <span data-ttu-id="56a89-156">При желании можно настроить параметр `crashkernel` , однако учитывайте, что он сокращает объем доступной памяти в виртуальной машине на 128 МБ или более, что может оказаться проблемой в виртуальных машинах небольшого размера.</span><span class="sxs-lookup"><span data-stu-id="56a89-156">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span></span>

    >[!Important]
    <span data-ttu-id="56a89-157">Для CentOS 6.5 и более ранних версий необходимо также указать параметр ядра `numa=off`.</span><span class="sxs-lookup"><span data-stu-id="56a89-157">CentOS 6.5 and earlier must also set the kernel parameter `numa=off`.</span></span> <span data-ttu-id="56a89-158">См. посвященный Red Hat [раздел 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="56a89-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

14. <span data-ttu-id="56a89-159">Убедитесь, что SSH-сервер установлен и настроен для включения во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="56a89-159">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="56a89-160">Обычно это сделано по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="56a89-160">This is usually the default.</span></span>

15. <span data-ttu-id="56a89-161">Не создавайте пространство подкачки на диске с ОС.</span><span class="sxs-lookup"><span data-stu-id="56a89-161">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="56a89-162">Агент Linux для Azure может автоматически настраивать пространство подкачки с использованием диска на локальном ресурсе, подключенном к виртуальной машине после подготовки для работы в среде Azure.</span><span class="sxs-lookup"><span data-stu-id="56a89-162">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="56a89-163">Следует отметить, что локальный диск ресурсов является *временным* диском и должен быть очищен при отмене подготовки виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="56a89-163">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="56a89-164">После установки агента Linux для Azure (см. предыдущий шаг) соответствующим образом измените следующие параметры в файле `/etc/waagent.conf`.</span><span class="sxs-lookup"><span data-stu-id="56a89-164">After installing the Azure Linux Agent (see previous step), modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

16. <span data-ttu-id="56a89-165">Выполните следующие команды, чтобы отменить подготовку виртуальной машины и подготовить ее в Azure:</span><span class="sxs-lookup"><span data-stu-id="56a89-165">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

17. <span data-ttu-id="56a89-166">В диспетчере Hyper-V выберите **Действие -> Завершение работы**.</span><span class="sxs-lookup"><span data-stu-id="56a89-166">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="56a89-167">Виртуальный жесткий диск Linux готов к передаче в Azure.</span><span class="sxs-lookup"><span data-stu-id="56a89-167">Your Linux VHD is now ready to be uploaded to Azure.</span></span>


- - -
## <a name="centos-70"></a><span data-ttu-id="56a89-168">CentOS 7.0+</span><span class="sxs-lookup"><span data-stu-id="56a89-168">CentOS 7.0+</span></span>
<span data-ttu-id="56a89-169">**Изменения в CentOS 7 (и аналогичных производных версиях)**</span><span class="sxs-lookup"><span data-stu-id="56a89-169">**Changes in CentOS 7 (and similar derivatives)**</span></span>

<span data-ttu-id="56a89-170">Подготовка виртуальной машины CentOS 7 для Azure в значительной степени аналогична версии CentOS 6, однако есть несколько важных отличий:</span><span class="sxs-lookup"><span data-stu-id="56a89-170">Preparing a CentOS 7 virtual machine for Azure is very similar to CentOS 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="56a89-171">Пакет NetworkManager больше не конфликтует с агентом Azure Linux.</span><span class="sxs-lookup"><span data-stu-id="56a89-171">The NetworkManager package no longer conflicts with the Azure Linux agent.</span></span> <span data-ttu-id="56a89-172">Этот пакет устанавливается по умолчанию, и мы рекомендуем не удалять его.</span><span class="sxs-lookup"><span data-stu-id="56a89-172">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="56a89-173">В качестве загрузчика по умолчанию теперь используется GRUB2, поэтому изменилась процедура правки параметров ядра (см. ниже).</span><span class="sxs-lookup"><span data-stu-id="56a89-173">GRUB2 is now used as the default bootloader, so the procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="56a89-174">XFS теперь является файловой системой по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="56a89-174">XFS is now the default file system.</span></span> <span data-ttu-id="56a89-175">При желании можно продолжать использование файловой системы ext4.</span><span class="sxs-lookup"><span data-stu-id="56a89-175">The ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="56a89-176">**Этапы настройки**</span><span class="sxs-lookup"><span data-stu-id="56a89-176">**Configuration Steps**</span></span>

1. <span data-ttu-id="56a89-177">В диспетчере Hyper-V выберите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="56a89-177">In Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="56a89-178">Щелкните **Подключение** , чтобы открыть окно консоли для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="56a89-178">Click **Connect** to open a console window for the virtual machine.</span></span>

3. <span data-ttu-id="56a89-179">Создайте или измените файл `/etc/sysconfig/network`, добавив следующий текст:</span><span class="sxs-lookup"><span data-stu-id="56a89-179">Create or edit the file `/etc/sysconfig/network` and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="56a89-180">Создайте или измените файл `/etc/sysconfig/network-scripts/ifcfg-eth0`, добавив следующий текст:</span><span class="sxs-lookup"><span data-stu-id="56a89-180">Create or edit the file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="56a89-181">Переместите или удалите правила udev, чтобы не создавать статические правила для интерфейса Ethernet.</span><span class="sxs-lookup"><span data-stu-id="56a89-181">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="56a89-182">Эти правила приводят к появлению проблем при клонировании виртуальной машины в Microsoft Azure или Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="56a89-182">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

6. <span data-ttu-id="56a89-183">Если вы хотите использовать зеркала OpenLogic, размещенные в центрах обработки данных Azure, замените файл `/etc/yum.repos.d/CentOS-Base.repo` следующими репозиториями.</span><span class="sxs-lookup"><span data-stu-id="56a89-183">If you would like to use the OpenLogic mirrors that are hosted within the Azure datacenters, then replace the `/etc/yum.repos.d/CentOS-Base.repo` file with the following repositories.</span></span>  <span data-ttu-id="56a89-184">При этом также будет добавлен репозиторий **[openlogic]** , включающий пакеты для агента Linux для Azure:</span><span class="sxs-lookup"><span data-stu-id="56a89-184">This will also add the **[openlogic]** repository that includes packages for the Azure Linux agent:</span></span>
   
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
    <span data-ttu-id="56a89-185">В этом руководстве предполагается, что вы используете по крайней мере репозиторий `[openlogic]`, который будет применяться при установке агента Linux для Azure.</span><span class="sxs-lookup"><span data-stu-id="56a89-185">The rest of this guide will assume you are using at least the `[openlogic]` repo, which will be used to install the Azure Linux agent below.</span></span>

7. <span data-ttu-id="56a89-186">Выполните следующую команду, чтобы очистить текущие метаданные yum и установить все обновления:</span><span class="sxs-lookup"><span data-stu-id="56a89-186">Run the following command to clear the current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all

    <span data-ttu-id="56a89-187">Если создается образ для более ранней версии CentOS, рекомендуется выполнить обновление всех пакетов до последней версии:</span><span class="sxs-lookup"><span data-stu-id="56a89-187">Unless you are creating an image for an older version of CentOS, it is recommended to update all the packages to the latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="56a89-188">После выполнения этой команды может потребоваться перезагрузка.</span><span class="sxs-lookup"><span data-stu-id="56a89-188">A reboot maybe required after running this command.</span></span>

8. <span data-ttu-id="56a89-189">Измените строку загрузки ядра в конфигурации grub, чтобы включить дополнительные параметры ядра для Azure.</span><span class="sxs-lookup"><span data-stu-id="56a89-189">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="56a89-190">Для этого откройте файл `/etc/default/grub` в текстовом редакторе и измените параметр `GRUB_CMDLINE_LINUX`, например:</span><span class="sxs-lookup"><span data-stu-id="56a89-190">To do this, open `/etc/default/grub` in a text editor and edit the `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="56a89-191">Это также гарантирует отправку всех сообщений консоли на первый последовательный порт, что может помочь технической поддержке Azure в плане отладки.</span><span class="sxs-lookup"><span data-stu-id="56a89-191">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="56a89-192">Также будут отключены новые соглашения CentOS 7 об именовании для сетевых адаптеров.</span><span class="sxs-lookup"><span data-stu-id="56a89-192">It also turns off the new CentOS 7 naming conventions for NICs.</span></span> <span data-ttu-id="56a89-193">Помимо вышесказанного, рекомендуется *удалить* следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="56a89-193">In addition to the above, it is recommended to *remove* the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="56a89-194">Графическая и "тихая" загрузка бесполезны в облачной среде, в которой нам нужно, чтобы все журналы отправлялись на последовательный порт.</span><span class="sxs-lookup"><span data-stu-id="56a89-194">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="56a89-195">При желании можно настроить параметр `crashkernel` , однако учитывайте, что он сокращает объем доступной памяти в виртуальной машине на 128 МБ или более, что может оказаться проблемой в виртуальных машинах небольшого размера.</span><span class="sxs-lookup"><span data-stu-id="56a89-195">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span></span>

9. <span data-ttu-id="56a89-196">После внесения изменений в файл `/etc/default/grub` , как указано выше, выполните следующую команду для повторного создания конфигурации grub:</span><span class="sxs-lookup"><span data-stu-id="56a89-196">Once you are done editing `/etc/default/grub` per above, run the following command to rebuild the grub configuration:</span></span>
   
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="56a89-197">Создавая образ из **VMWare, VirtualBox или KVM**, убедитесь что драйверы Hyper-V включены в initramfs:</span><span class="sxs-lookup"><span data-stu-id="56a89-197">If building the image from **VMWare, VirtualBox or KVM:** Ensure the Hyper-V drivers are included in the initramfs:</span></span>
   
   <span data-ttu-id="56a89-198">Измените файл `/etc/dracut.conf`, добавив в него следующее содержимое:</span><span class="sxs-lookup"><span data-stu-id="56a89-198">Edit `/etc/dracut.conf`, add content:</span></span>
   
        add_drivers+=”hv_vmbus hv_netvsc hv_storvsc”
   
   <span data-ttu-id="56a89-199">Выполните сборку initramfs заново:</span><span class="sxs-lookup"><span data-stu-id="56a89-199">Rebuild the initramfs:</span></span>
   
        # sudo dracut –f -v

11. <span data-ttu-id="56a89-200">Установите агент Linux для Azure и зависимости:</span><span class="sxs-lookup"><span data-stu-id="56a89-200">Install the Azure Linux Agent and dependencies:</span></span>

        # sudo yum install python-pyasn1 WALinuxAgent
        # sudo systemctl enable waagent

12. <span data-ttu-id="56a89-201">Не создавайте пространство подкачки на диске с ОС.</span><span class="sxs-lookup"><span data-stu-id="56a89-201">Do not create swap space on the OS disk.</span></span>
   
   <span data-ttu-id="56a89-202">Агент Linux для Azure может автоматически настраивать пространство подкачки с использованием диска на локальном ресурсе, подключенном к виртуальной машине после подготовки для работы в среде Azure.</span><span class="sxs-lookup"><span data-stu-id="56a89-202">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="56a89-203">Следует отметить, что локальный диск ресурсов является *временным* диском и должен быть очищен при отмене подготовки виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="56a89-203">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="56a89-204">После установки агента Linux для Azure (см. предыдущий шаг) соответствующим образом измените следующие параметры в файле `/etc/waagent.conf`.</span><span class="sxs-lookup"><span data-stu-id="56a89-204">After installing the Azure Linux Agent (see previous step), modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>
   
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

13. <span data-ttu-id="56a89-205">Выполните следующие команды, чтобы отменить подготовку виртуальной машины и подготовить ее в Azure:</span><span class="sxs-lookup"><span data-stu-id="56a89-205">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

14. <span data-ttu-id="56a89-206">В диспетчере Hyper-V выберите **Действие -> Завершение работы**.</span><span class="sxs-lookup"><span data-stu-id="56a89-206">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="56a89-207">Виртуальный жесткий диск Linux готов к передаче в Azure.</span><span class="sxs-lookup"><span data-stu-id="56a89-207">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="56a89-208">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="56a89-208">Next steps</span></span>
<span data-ttu-id="56a89-209">Теперь виртуальный жесткий диск CentOS Linux можно использовать для создания новых виртуальных машин Azure.</span><span class="sxs-lookup"><span data-stu-id="56a89-209">You're now ready to use your CentOS Linux virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="56a89-210">Если вы загружаете VHD-файл в Azure впервые, обратитесь к шагам 2 и 3 в статье [Создание и загрузка виртуального жесткого диска, содержащего операционную систему Linux](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="56a89-210">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

