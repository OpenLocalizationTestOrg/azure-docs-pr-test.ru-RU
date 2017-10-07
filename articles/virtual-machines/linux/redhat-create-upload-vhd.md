---
title: "aaaCreate и отправка Red Hat Enterprise Linux виртуального жесткого диска для использования в Azure | Документы Microsoft"
description: "Узнайте toocreate и отправить в Azure виртуального жесткого диска (VHD), содержащий операционную систему Red Hat Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 6c6b8f72-32d3-47fa-be94-6cb54537c69f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/28/2017
ms.author: szark
ms.openlocfilehash: bdd1bbfbee55b5cc61d69a09b06b6bd2c3de362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-red-hat-based-virtual-machine-for-azure"></a><span data-ttu-id="ff7cd-103">Подготовка виртуальной машины на основе Red Hat для Azure</span><span class="sxs-lookup"><span data-stu-id="ff7cd-103">Prepare a Red Hat-based virtual machine for Azure</span></span>
<span data-ttu-id="ff7cd-104">В этой статье вы узнаете, как tooprepare Red Hat Enterprise Linux (RHEL) виртуальной машины для использования в Azure.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-104">In this article, you will learn how tooprepare a Red Hat Enterprise Linux (RHEL) virtual machine for use in Azure.</span></span> <span data-ttu-id="ff7cd-105">6.7 + и 7.1 +, являются Hello версии RHEL, описанных в этой статье.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-105">hello versions of RHEL that are covered in this article are 6.7+ and 7.1+.</span></span> <span data-ttu-id="ff7cd-106">Hello низкоуровневые оболочки для подготовки, описанных в этой статье, Hyper-V, на основе ядра виртуальной машины (KVM) и VMware.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-106">hello hypervisors for preparation that are covered in this article are Hyper-V, kernel-based virtual machine (KVM), and VMware.</span></span> <span data-ttu-id="ff7cd-107">Подробнее о требованиях к участникам в программе Red Hat Cloud Access см. на [веб-сайте Red Hat Cloud Access](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) и странице [запуска RHEL в Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).</span><span class="sxs-lookup"><span data-stu-id="ff7cd-107">For more information about eligibility requirements for participating in Red Hat's Cloud Access program, see [Red Hat's Cloud Access website](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) and [Running RHEL on Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).</span></span>

## <a name="prepare-a-red-hat-based-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="ff7cd-108">Подготовка виртуальной машины под управлением Red Hat в диспетчере Hyper-V</span><span class="sxs-lookup"><span data-stu-id="ff7cd-108">Prepare a Red Hat-based virtual machine from Hyper-V Manager</span></span>

### <a name="prerequisites"></a><span data-ttu-id="ff7cd-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ff7cd-109">Prerequisites</span></span>
<span data-ttu-id="ff7cd-110">В этом разделе предполагается, что ISO-файл уже получен из веб-сайта hello Red Hat и установленных hello RHEL изображения tooa виртуального жесткого диска (VHD).</span><span class="sxs-lookup"><span data-stu-id="ff7cd-110">This section assumes that you have already obtained an ISO file from hello Red Hat website and installed hello RHEL image tooa virtual hard disk (VHD).</span></span> <span data-ttu-id="ff7cd-111">Дополнительные сведения о том, как tooinstall диспетчера Hyper-V toouse образа операционной системы в разделе [Установка hello роль Hyper-V и настройка виртуальной машины](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="ff7cd-111">For more details about how toouse Hyper-V Manager tooinstall an operating system image, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="ff7cd-112">**Замечания по установке RHEL**</span><span class="sxs-lookup"><span data-stu-id="ff7cd-112">**RHEL installation notes**</span></span>

* <span data-ttu-id="ff7cd-113">Azure не поддерживает формат VHDX hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-113">Azure does not support hello VHDX format.</span></span> <span data-ttu-id="ff7cd-114">В Azure поддерживается только формат фиксированного виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-114">Azure supports only fixed VHD.</span></span> <span data-ttu-id="ff7cd-115">Можно использовать формат tooVHD диска hello tooconvert диспетчера Hyper-V, или можно использовать командлет convert-vhd hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-115">You can use Hyper-V Manager tooconvert hello disk tooVHD format, or you can use hello convert-vhd cmdlet.</span></span> <span data-ttu-id="ff7cd-116">Если вы используете VirtualBox, выберите **фиксированный размер** в отличие от toohello динамически назначаемых параметр при создании hello диска по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-116">If you use VirtualBox, select **Fixed size** as opposed toohello default dynamically allocated option when you create hello disk.</span></span>
* <span data-ttu-id="ff7cd-117">В Azure поддерживаются только виртуальные машины поколения 1.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-117">Azure supports only generation 1 virtual machines.</span></span> <span data-ttu-id="ff7cd-118">Виртуальные машины поколения 1 можно преобразовать из формата файла виртуального жесткого диска toohello VHDX и динамически расширяемый tooa диск фиксированного размера.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-118">You can convert a generation 1 virtual machine from VHDX toohello VHD file format and from dynamically expanding tooa fixed-size disk.</span></span> <span data-ttu-id="ff7cd-119">Вы не можете изменить поколение виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-119">You can't change a virtual machine's generation.</span></span> <span data-ttu-id="ff7cd-120">Дополнительные сведения см. в статье [Необходимо создать виртуальную машину поколения 1 или 2 в Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span><span class="sxs-lookup"><span data-stu-id="ff7cd-120">For more information, see [Should I create a generation 1 or 2 virtual machine in Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span></span>
* <span data-ttu-id="ff7cd-121">Hello максимальный размер, допустимый для hello виртуального жесткого диска — 1023 ГБ.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-121">hello maximum size that's allowed for hello VHD is 1,023 GB.</span></span>
* <span data-ttu-id="ff7cd-122">При установке операционной системы Linux hello, рекомендуется использовать стандартный секции, а не логические тома Manager (LVM), что часто является по умолчанию hello для многих установок.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-122">When you install hello Linux operating system, we recommend that you use standard partitions rather than Logical Volume Manager (LVM), which is often hello default for many installations.</span></span> <span data-ttu-id="ff7cd-123">Данная методика позволит избежать конфликтов имен LVM с клоны виртуальных машин, особенно в том случае, если вы захотите tooattach операционной системы диска tooanother идентичную виртуальную машину для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-123">This practice will avoid LVM name conflicts with cloned virtual machines, particularly if you ever need tooattach an operating system disk tooanother identical virtual machine for troubleshooting.</span></span> <span data-ttu-id="ff7cd-124">Для дисков данных можно использовать [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) или [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ff7cd-124">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="ff7cd-125">Требуется поддержка ядра для подключения файловых систем UDF.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-125">Kernel support for mounting Universal Disk Format (UDF) file systems is required.</span></span> <span data-ttu-id="ff7cd-126">При первой загрузке в Azure, hello формате UDF носителя, который будет гостевой вложенного toohello передает подготовки hello toohello конфигурации виртуальной машины Linux.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-126">At first boot on Azure, hello UDF-formatted media that is attached toohello guest passes hello provisioning configuration toohello Linux virtual machine.</span></span> <span data-ttu-id="ff7cd-127">Hello Azure Linux Agent должен быть доступ toomount hello UDF файл системы tooread свою конфигурацию и подготовки виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-127">hello Azure Linux Agent must be able toomount hello UDF file system tooread its configuration and provision hello virtual machine.</span></span>
* <span data-ttu-id="ff7cd-128">Версии ядра Linux hello, или более поздних версиях 2.6.37 не поддерживают доступ к неоднородной памяти (NUMA) на узле Hyper-V с большие размеры виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-128">Versions of hello Linux kernel that are earlier than 2.6.37 do not support non-uniform memory access (NUMA) on Hyper-V with larger virtual machine sizes.</span></span> <span data-ttu-id="ff7cd-129">Эту проблему в основном влияет на старых дистрибутивы использовать hello вышестоящих ядра Red Hat 2.6.32 и была исправлена в RHEL 6.6 (ядра 2.6.32 504).</span><span class="sxs-lookup"><span data-stu-id="ff7cd-129">This issue primarily impacts older distributions that use hello upstream Red Hat 2.6.32 kernel and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="ff7cd-130">Системы, использующие пользовательские ядер, которые старше 2.6.37 или на основе RHEL ядер, возраст которых превышает 2.6.32-504 необходимо задать hello `numa=off` параметр загрузки hello ядра в командной строке grub.conf.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-130">Systems that run custom kernels that are older than 2.6.37 or RHEL-based kernels that are older than 2.6.32-504 must set hello `numa=off` boot parameter on hello kernel command line in grub.conf.</span></span> <span data-ttu-id="ff7cd-131">Дополнительные сведения см. на странице о [проблемах гостевой машины Red Hat Enterprise Linux 6 на виртуальной машине Microsoft Hyper-V](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="ff7cd-131">For more information, see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="ff7cd-132">Не настраивайте переключения секции на диске операционной системы hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-132">Do not configure a swap partition on hello operating system disk.</span></span> <span data-ttu-id="ff7cd-133">Hello агент для Linux можно toocreate настроенный файл подкачки на диске временного ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-133">hello Linux Agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="ff7cd-134">Дополнительные сведения об этом можно найти в hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-134">More information about this can be found in hello following steps.</span></span>
* <span data-ttu-id="ff7cd-135">Все VHD-диски должны иметь размер, кратный 1 МБ.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-135">All VHDs must have sizes that are multiples of 1 MB.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="ff7cd-136">Подготовка виртуальной машины RHEL 6 в диспетчере Hyper-V</span><span class="sxs-lookup"><span data-stu-id="ff7cd-136">Prepare a RHEL 6 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="ff7cd-137">В диспетчере Hyper-V выберите виртуальную машину hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-137">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="ff7cd-138">Нажмите кнопку **Connect** tooopen окно консоли для виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-138">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="ff7cd-139">В RHEL 6 NetworkManager могут помешать hello агента Azure Linux.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-139">In RHEL 6, NetworkManager can interfere with hello Azure Linux agent.</span></span> <span data-ttu-id="ff7cd-140">Удаление этого пакета, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-140">Uninstall this package by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="ff7cd-141">Создание или изменение hello `/etc/sysconfig/network` и добавьте следующий текст hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-141">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="ff7cd-142">Создание или изменение hello `/etc/sysconfig/network-scripts/ifcfg-eth0` и добавьте следующий текст hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-142">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="ff7cd-143">Переместить (или удалить) hello udev правила tooavoid создания статические правила для интерфейса Ethernet hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-143">Move (or remove) hello udev rules tooavoid generating static rules for hello Ethernet interface.</span></span> <span data-ttu-id="ff7cd-144">Эти правила приводят к появлению проблем при клонировании виртуальной машины в Microsoft Azure или Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-144">These rules cause problems when you clone a virtual machine in Microsoft Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="ff7cd-145">Убедитесь, сетевая служба hello начнется во время загрузки, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-145">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

8. <span data-ttu-id="ff7cd-146">Зарегистрируйте подписку Red Hat tooenable hello установку пакетов из репозитория RHEL hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-146">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="ff7cd-147">пакет WALinuxAgent Hello, `WALinuxAgent-<version>`, переданное toohello Red Hat дополнения репозитория.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-147">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="ff7cd-148">Включите hello дополнения репозиторий, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-148">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

10. <span data-ttu-id="ff7cd-149">Измените строку загрузки ядра hello в параметры grub tooinclude дополнительные ядра для Azure.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-149">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="ff7cd-150">toodo этого изменения, откройте `/boot/grub/menu.lst` в текстовом редакторе, убедитесь, что ядра по умолчанию hello включает hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-150">toodo this modification, open `/boot/grub/menu.lst` in a text editor, and ensure that hello default kernel includes hello following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="ff7cd-151">Это также позволит гарантировать, что все сообщения консоли отправляются toohello первый последовательный порт, который может помочь Azure поддержка с помощью отладки проблем.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-151">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="ff7cd-152">Кроме того рекомендуется удалить hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-152">In addition, we recommended that you remove hello following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="ff7cd-153">Графический quiet начальной загрузки, не используются в облачной среде, где мы хотим, чтобы все журналы toobe hello, отправляемых toohello последовательного порта.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-153">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>  <span data-ttu-id="ff7cd-154">Можно оставить hello `crashkernel` параметр настроен, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-154">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="ff7cd-155">Обратите внимание, что этот параметр уменьшает hello объем доступной памяти на виртуальной машине hello 128 МБ или больше.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-155">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more.</span></span> <span data-ttu-id="ff7cd-156">Это может оказаться проблемой для виртуальных машин небольшого размера.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-156">This configuration might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="ff7cd-157">RHEL версии 6.5 и более ранних версиях необходимо также задать hello `numa=off` параметр ядра.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-157">RHEL 6.5 and earlier must also set hello `numa=off` kernel parameter.</span></span> <span data-ttu-id="ff7cd-158">См. посвященный Red Hat [раздел 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="ff7cd-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

11. <span data-ttu-id="ff7cd-159">Убедитесь, этот сервер hello безопасного shell (SSH) установлен и настроен toostart во время загрузки, которой обычно является по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-159">Ensure that hello secure shell (SSH) server is installed and configured toostart at boot time, which is usually hello default.</span></span> <span data-ttu-id="ff7cd-160">Измените hello tooinclude /etc/ssh/sshd_config следующей строкой:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-160">Modify /etc/ssh/sshd_config tooinclude hello following line:</span></span>

        ClientAliveInterval 180

12. <span data-ttu-id="ff7cd-161">Установите агент Azure Linux hello, выполнив hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-161">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

    <span data-ttu-id="ff7cd-162">Установка пакета WALinuxAgent hello удаляет hello NetworkManager и NetworkManager gnome пакеты, если они не были уже удалены в шаге 3.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-162">Installing hello WALinuxAgent package removes hello NetworkManager and NetworkManager-gnome packages if they were not already removed in step 3.</span></span>

13. <span data-ttu-id="ff7cd-163">Не создавайте подкачки на диске операционной системы hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-163">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="ff7cd-164">Hello Azure Linux Agent подкачки может автоматически настроить с помощью hello локальный диск ресурсов, которые toohello подключенных виртуальных машин после подготовки виртуальной машины hello в Azure.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-164">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="ff7cd-165">Обратите внимание, что hello локальный диск ресурсов является временной и, он может очищаться при отозваны hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-165">Note that hello local resource disk is a temporary disk and that it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="ff7cd-166">После установки hello Azure Linux Agent в предыдущем шаге hello, измените соответствующим образом следующие параметры в /etc/waagent.conf hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-166">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in /etc/waagent.conf appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

14. <span data-ttu-id="ff7cd-167">Отменить регистрацию подписки hello (при необходимости), выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-167">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # sudo subscription-manager unregister

15. <span data-ttu-id="ff7cd-168">Запустите следующие команды toodeprovision hello виртуальной машины hello и подготовить его для подготовки в Azure:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-168">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

16. <span data-ttu-id="ff7cd-169">В диспетчере Hyper-V выберите **Действие** > **Завершение работы**.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-169">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="ff7cd-170">ДИСК Linux имеет теперь готовы toobe отправлен tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-170">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>


### <a name="prepare-a-rhel-7-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="ff7cd-171">Подготовка виртуальной машины RHEL 7 в диспетчере Hyper-V</span><span class="sxs-lookup"><span data-stu-id="ff7cd-171">Prepare a RHEL 7 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="ff7cd-172">В диспетчере Hyper-V выберите виртуальную машину hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-172">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="ff7cd-173">Нажмите кнопку **Connect** tooopen окно консоли для виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-173">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="ff7cd-174">Создание или изменение hello `/etc/sysconfig/network` и добавьте следующий текст hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-174">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="ff7cd-175">Создание или изменение hello `/etc/sysconfig/network-scripts/ifcfg-eth0` и добавьте следующий текст hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-175">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="ff7cd-176">Убедитесь, сетевая служба hello начнется во время загрузки, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-176">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="ff7cd-177">Зарегистрируйте подписку Red Hat tooenable hello установку пакетов из репозитория RHEL hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-177">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="ff7cd-178">Измените строку загрузки ядра hello в параметры grub tooinclude дополнительные ядра для Azure.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-178">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="ff7cd-179">toodo этого изменения, откройте `/etc/default/grub` в текстовом редакторе и изменить hello `GRUB_CMDLINE_LINUX` параметра.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-179">toodo this modification, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="ff7cd-180">Например:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-180">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="ff7cd-181">Это также позволит гарантировать, что все сообщения консоли отправляются toohello первый последовательный порт, который может помочь Azure поддержка с помощью отладки проблем.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-181">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="ff7cd-182">Эта конфигурация также отключает новые соглашения об именах hello RHEL 7 для сетевых адаптеров.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-182">This configuration also turns off hello new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="ff7cd-183">Кроме того рекомендуется удалить hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-183">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="ff7cd-184">Графический quiet начальной загрузки, не используются в облачной среде, где мы хотим, чтобы все журналы toobe hello, отправляемых toohello последовательного порта.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-184">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="ff7cd-185">Можно оставить hello `crashkernel` параметр настроен, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-185">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="ff7cd-186">Обратите внимание, что этот параметр уменьшает hello объем доступной памяти на виртуальной машине hello 128 МБ или более, которой может быть проблематичным на меньшие размеры виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-186">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

8. <span data-ttu-id="ff7cd-187">После завершения редактирования `/etc/default/grub`, запустите hello следующие конфигурацию grub hello toorebuild команды:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-187">After you are done editing `/etc/default/grub`, run hello following command toorebuild hello grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

9. <span data-ttu-id="ff7cd-188">Убедитесь, что hello SSH сервер установлен и настроен toostart во время загрузки, которой обычно является по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-188">Ensure that hello SSH server is installed and configured toostart at boot time, which is usually hello default.</span></span> <span data-ttu-id="ff7cd-189">Изменить `/etc/ssh/sshd_config` tooinclude hello, следующей строкой:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-189">Modify `/etc/ssh/sshd_config` tooinclude hello following line:</span></span>

        ClientAliveInterval 180

10. <span data-ttu-id="ff7cd-190">пакет WALinuxAgent Hello, `WALinuxAgent-<version>`, переданное toohello Red Hat дополнения репозитория.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-190">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="ff7cd-191">Включите hello дополнения репозиторий, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-191">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

11. <span data-ttu-id="ff7cd-192">Установите агент Azure Linux hello, выполнив hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-192">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

12. <span data-ttu-id="ff7cd-193">Не создавайте подкачки на диске операционной системы hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-193">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="ff7cd-194">Hello Azure Linux Agent подкачки может автоматически настроить с помощью hello локальный диск ресурсов, которые toohello подключенных виртуальных машин после подготовки виртуальной машины hello в Azure.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-194">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="ff7cd-195">Обратите внимание, что hello локальный диск ресурсов — временный диск может очищаться при отмененной подготовкой hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-195">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="ff7cd-196">После установки hello Azure Linux Agent в предыдущем шаге hello, изменить следующие параметры в hello `/etc/waagent.conf` соответствующим образом:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-196">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. <span data-ttu-id="ff7cd-197">Если необходимо toounregister hello подписки, запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-197">If you want toounregister hello subscription, run hello following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="ff7cd-198">Запустите следующие команды toodeprovision hello виртуальной машины hello и подготовить его для подготовки в Azure:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-198">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="ff7cd-199">В диспетчере Hyper-V выберите **Действие** > **Завершение работы**.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-199">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="ff7cd-200">ДИСК Linux имеет теперь готовы toobe отправлен tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-200">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>


## <a name="prepare-a-red-hat-based-virtual-machine-from-kvm"></a><span data-ttu-id="ff7cd-201">Подготовка виртуальной машины под управлением Red Hat в KVM</span><span class="sxs-lookup"><span data-stu-id="ff7cd-201">Prepare a Red Hat-based virtual machine from KVM</span></span>
### <a name="prepare-a-rhel-6-virtual-machine-from-kvm"></a><span data-ttu-id="ff7cd-202">Подготовка виртуальной машины RHEL 6 в KVM</span><span class="sxs-lookup"><span data-stu-id="ff7cd-202">Prepare a RHEL 6 virtual machine from KVM</span></span>

1. <span data-ttu-id="ff7cd-203">Загрузите с веб-сайта Red Hat hello изображение KVM hello RHEL 6.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-203">Download hello KVM image of RHEL 6 from hello Red Hat website.</span></span>

2. <span data-ttu-id="ff7cd-204">Задайте пароль пользователя root.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-204">Set a root password.</span></span>

    <span data-ttu-id="ff7cd-205">Создать зашифрованный пароль и скопировать hello выходные данные команды hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-205">Generate an encrypted password, and copy hello output of hello command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="ff7cd-206">Установите корневой пароль с помощью Guestfish:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-206">Set a root password with guestfish:</span></span>
        
        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="ff7cd-207">Изменение hello второе поле hello привилегированного пользователя из «!»</span><span class="sxs-lookup"><span data-stu-id="ff7cd-207">Change hello second field of hello root user from "!!"</span></span> <span data-ttu-id="ff7cd-208">toohello зашифрованный пароль.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-208">toohello encrypted password.</span></span>

3. <span data-ttu-id="ff7cd-209">Создание виртуальной машины в KVM из образа qcow2 hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-209">Create a virtual machine in KVM from hello qcow2 image.</span></span> <span data-ttu-id="ff7cd-210">Задайте тип диска hello слишком**qcow2**и задать модель hello виртуального сетевого интерфейса устройства слишком**virtio**.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-210">Set hello disk type too**qcow2**, and set hello virtual network interface device model too**virtio**.</span></span> <span data-ttu-id="ff7cd-211">Затем запустите hello виртуальную машину и войдите в качестве корневого.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-211">Then, start hello virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="ff7cd-212">Создание или изменение hello `/etc/sysconfig/network` и добавьте следующий текст hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-212">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="ff7cd-213">Создание или изменение hello `/etc/sysconfig/network-scripts/ifcfg-eth0` и добавьте следующий текст hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-213">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="ff7cd-214">Переместить (или удалить) hello udev правила tooavoid создания статические правила для интерфейса Ethernet hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-214">Move (or remove) hello udev rules tooavoid generating static rules for hello Ethernet interface.</span></span> <span data-ttu-id="ff7cd-215">Эти правила приводят к появлению проблем при клонировании виртуальной машины в Azure или Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-215">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="ff7cd-216">Убедитесь, сетевая служба hello начнется во время загрузки, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-216">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # chkconfig network on

8. <span data-ttu-id="ff7cd-217">Зарегистрируйте подписку Red Hat tooenable hello установку пакетов из репозитория RHEL hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-217">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="ff7cd-218">Измените строку загрузки ядра hello в параметры grub tooinclude дополнительные ядра для Azure.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-218">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="ff7cd-219">toodo этой конфигурации, откройте `/boot/grub/menu.lst` в текстовом редакторе, убедитесь, что ядра по умолчанию hello включает hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-219">toodo this configuration, open `/boot/grub/menu.lst` in a text editor, and ensure that hello default kernel includes hello following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="ff7cd-220">Это также позволит гарантировать, что все сообщения консоли отправляются toohello первый последовательный порт, который может помочь Azure поддержка с помощью отладки проблем.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-220">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="ff7cd-221">Кроме того рекомендуется удалить hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-221">In addition, we recommend that you remove hello following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="ff7cd-222">Графический quiet начальной загрузки, не используются в облачной среде, где мы хотим, чтобы все журналы toobe hello, отправляемых toohello последовательного порта.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-222">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="ff7cd-223">Можно оставить hello `crashkernel` параметр настроен, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-223">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="ff7cd-224">Обратите внимание, что этот параметр уменьшает hello объем доступной памяти на виртуальной машине hello 128 МБ или более, которой может быть проблематичным на меньшие размеры виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-224">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="ff7cd-225">RHEL версии 6.5 и более ранних версиях необходимо также задать hello `numa=off` параметр ядра.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-225">RHEL 6.5 and earlier must also set hello `numa=off` kernel parameter.</span></span> <span data-ttu-id="ff7cd-226">См. посвященный Red Hat [раздел 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="ff7cd-226">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

10. <span data-ttu-id="ff7cd-227">Добавьте tooinitramfs модули Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-227">Add Hyper-V modules tooinitramfs:</span></span>  

    <span data-ttu-id="ff7cd-228">Изменить `/etc/dracut.conf`и добавьте следующие содержимое hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-228">Edit `/etc/dracut.conf`, and add hello following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="ff7cd-229">Повторно создайте initramfs:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-229">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="ff7cd-230">Удаление cloud-init:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-230">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="ff7cd-231">Убедитесь, что hello SSH сервер установлен и настроен toostart во время загрузки:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-231">Ensure that hello SSH server is installed and configured toostart at boot time:</span></span>

        # chkconfig sshd on

    <span data-ttu-id="ff7cd-232">Измените hello tooinclude /etc/ssh/sshd_config следующие строки:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-232">Modify /etc/ssh/sshd_config tooinclude hello following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="ff7cd-233">пакет WALinuxAgent Hello, `WALinuxAgent-<version>`, переданное toohello Red Hat дополнения репозитория.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-233">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="ff7cd-234">Включите hello дополнения репозиторий, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-234">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

14. <span data-ttu-id="ff7cd-235">Установите агент Azure Linux hello, выполнив hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-235">Install hello Azure Linux Agent by running hello following command:</span></span>

        # yum install WALinuxAgent

        # chkconfig waagent on

15. <span data-ttu-id="ff7cd-236">Hello Azure Linux Agent подкачки может автоматически настроить с помощью hello локальный диск ресурсов, которые toohello подключенных виртуальных машин после подготовки виртуальной машины hello в Azure.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-236">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="ff7cd-237">Обратите внимание, что hello локальный диск ресурсов — временный диск может очищаться при отмененной подготовкой hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-237">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="ff7cd-238">После установки hello Azure Linux Agent в предыдущем шаге hello, изменить следующие параметры в hello **/etc/waagent.conf** соответствующим образом:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-238">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in **/etc/waagent.conf** appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. <span data-ttu-id="ff7cd-239">Отменить регистрацию подписки hello (при необходимости), выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-239">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="ff7cd-240">Запустите следующие команды toodeprovision hello виртуальной машины hello и подготовить его для подготовки в Azure:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-240">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="ff7cd-241">Завершите работу виртуальной машины hello в KVM.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-241">Shut down hello virtual machine in KVM.</span></span>

19. <span data-ttu-id="ff7cd-242">Преобразуйте формат виртуального жесткого диска toohello изображения qcow2 hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-242">Convert hello qcow2 image toohello VHD format.</span></span>

    <span data-ttu-id="ff7cd-243">Сначала преобразовать формат tooraw hello изображения:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-243">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-6.8.qcow2 rhel-6.8.raw

    <span data-ttu-id="ff7cd-244">Убедитесь, что размер hello hello необработанные изображения выравнивается 1 МБ.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-244">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="ff7cd-245">В противном случае округлять hello размер tooalign с 1 МБ:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-245">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="ff7cd-246">Преобразовать tooa hello неподготовленный диск фиксированного размера виртуального жесткого диска:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-246">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd


### <a name="prepare-a-rhel-7-virtual-machine-from-kvm"></a><span data-ttu-id="ff7cd-247">Подготовка виртуальной машины RHEL 7 в KVM</span><span class="sxs-lookup"><span data-stu-id="ff7cd-247">Prepare a RHEL 7 virtual machine from KVM</span></span>

1. <span data-ttu-id="ff7cd-248">Загрузите с веб-сайта Red Hat hello изображение KVM hello RHEL 7.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-248">Download hello KVM image of RHEL 7 from hello Red Hat website.</span></span> <span data-ttu-id="ff7cd-249">В этой процедуре используется RHEL 7 в качестве примера hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-249">This procedure uses RHEL 7 as hello example.</span></span>

2. <span data-ttu-id="ff7cd-250">Задайте пароль пользователя root.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-250">Set a root password.</span></span>

    <span data-ttu-id="ff7cd-251">Создать зашифрованный пароль и скопировать hello выходные данные команды hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-251">Generate an encrypted password, and copy hello output of hello command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="ff7cd-252">Установите корневой пароль с помощью Guestfish:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-252">Set a root password with guestfish:</span></span>

        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="ff7cd-253">Изменение hello второе поле привилегированного пользователя из «!»</span><span class="sxs-lookup"><span data-stu-id="ff7cd-253">Change hello second field of root user from "!!"</span></span> <span data-ttu-id="ff7cd-254">toohello зашифрованный пароль.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-254">toohello encrypted password.</span></span>

3. <span data-ttu-id="ff7cd-255">Создание виртуальной машины в KVM из образа qcow2 hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-255">Create a virtual machine in KVM from hello qcow2 image.</span></span> <span data-ttu-id="ff7cd-256">Задайте тип диска hello слишком**qcow2**и задать модель hello виртуального сетевого интерфейса устройства слишком**virtio**.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-256">Set hello disk type too**qcow2**, and set hello virtual network interface device model too**virtio**.</span></span> <span data-ttu-id="ff7cd-257">Затем запустите hello виртуальную машину и войдите в качестве корневого.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-257">Then, start hello virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="ff7cd-258">Создание или изменение hello `/etc/sysconfig/network` и добавьте следующий текст hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-258">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="ff7cd-259">Создание или изменение hello `/etc/sysconfig/network-scripts/ifcfg-eth0` и добавьте следующий текст hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-259">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

6. <span data-ttu-id="ff7cd-260">Убедитесь, сетевая служба hello начнется во время загрузки, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-260">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # chkconfig network on

7. <span data-ttu-id="ff7cd-261">Зарегистрируйте подписку Red Hat tooenable установку пакетов из репозитория RHEL hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-261">Register your Red Hat subscription tooenable installation of packages from hello RHEL repository by running hello following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

8. <span data-ttu-id="ff7cd-262">Измените строку загрузки ядра hello в параметры grub tooinclude дополнительные ядра для Azure.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-262">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="ff7cd-263">toodo этой конфигурации, откройте `/etc/default/grub` в текстовом редакторе и изменить hello `GRUB_CMDLINE_LINUX` параметра.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-263">toodo this configuration, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="ff7cd-264">Например:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-264">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="ff7cd-265">Эта команда также гарантирует, что все сообщения консоли отправляются toohello первый последовательный порт, который может помочь Azure поддержка с помощью отладки проблем.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-265">This command also ensures that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="ff7cd-266">Hello команда также отключает новые соглашения об именах hello RHEL 7 для сетевых адаптеров.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-266">hello command also turns off hello new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="ff7cd-267">Кроме того рекомендуется удалить hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-267">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="ff7cd-268">Графический quiet начальной загрузки, не используются в облачной среде, где мы хотим, чтобы все журналы toobe hello, отправляемых toohello последовательного порта.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-268">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="ff7cd-269">Можно оставить hello `crashkernel` параметр настроен, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-269">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="ff7cd-270">Обратите внимание, что этот параметр уменьшает hello объем доступной памяти на виртуальной машине hello 128 МБ или более, которой может быть проблематичным на меньшие размеры виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-270">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="ff7cd-271">После завершения редактирования `/etc/default/grub`, запустите hello следующие конфигурацию grub hello toorebuild команды:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-271">After you are done editing `/etc/default/grub`, run hello following command toorebuild hello grub configuration:</span></span>

        # grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="ff7cd-272">Добавьте модули Hyper-V в initramfs.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-272">Add Hyper-V modules into initramfs.</span></span>

    <span data-ttu-id="ff7cd-273">Измените файл `/etc/dracut.conf` , добавив в него следующее содержимое:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-273">Edit `/etc/dracut.conf` and add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="ff7cd-274">Повторно создайте initramfs:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-274">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="ff7cd-275">Удаление cloud-init:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-275">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="ff7cd-276">Убедитесь, что hello SSH сервер установлен и настроен toostart во время загрузки:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-276">Ensure that hello SSH server is installed and configured toostart at boot time:</span></span>

        # systemctl enable sshd

    <span data-ttu-id="ff7cd-277">Измените hello tooinclude /etc/ssh/sshd_config следующие строки:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-277">Modify /etc/ssh/sshd_config tooinclude hello following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="ff7cd-278">пакет WALinuxAgent Hello, `WALinuxAgent-<version>`, переданное toohello Red Hat дополнения репозитория.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-278">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="ff7cd-279">Включите hello дополнения репозиторий, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-279">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

14. <span data-ttu-id="ff7cd-280">Установите агент Azure Linux hello, выполнив hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-280">Install hello Azure Linux Agent by running hello following command:</span></span>

        # yum install WALinuxAgent

    <span data-ttu-id="ff7cd-281">Включите службу hello waagent:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-281">Enable hello waagent service:</span></span>

        # systemctl enable waagent.service

15. <span data-ttu-id="ff7cd-282">Не создавайте подкачки на диске операционной системы hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-282">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="ff7cd-283">Hello Azure Linux Agent подкачки может автоматически настроить с помощью hello локальный диск ресурсов, которые toohello подключенных виртуальных машин после подготовки виртуальной машины hello в Azure.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-283">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="ff7cd-284">Обратите внимание, что hello локальный диск ресурсов — временный диск может очищаться при отмененной подготовкой hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-284">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="ff7cd-285">После установки hello Azure Linux Agent в предыдущем шаге hello, изменить следующие параметры в hello `/etc/waagent.conf` соответствующим образом:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-285">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. <span data-ttu-id="ff7cd-286">Отменить регистрацию подписки hello (при необходимости), выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-286">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="ff7cd-287">Запустите следующие команды toodeprovision hello виртуальной машины hello и подготовить его для подготовки в Azure:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-287">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="ff7cd-288">Завершите работу виртуальной машины hello в KVM.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-288">Shut down hello virtual machine in KVM.</span></span>

19. <span data-ttu-id="ff7cd-289">Преобразуйте формат виртуального жесткого диска toohello изображения qcow2 hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-289">Convert hello qcow2 image toohello VHD format.</span></span>

    <span data-ttu-id="ff7cd-290">Сначала преобразовать формат tooraw hello изображения:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-290">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-7.3.qcow2 rhel-7.3.raw

    <span data-ttu-id="ff7cd-291">Убедитесь, что размер hello hello необработанные изображения выравнивается 1 МБ.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-291">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="ff7cd-292">В противном случае округлять hello размер tooalign с 1 МБ:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-292">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="ff7cd-293">Преобразовать tooa hello неподготовленный диск фиксированного размера виртуального жесткого диска:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-293">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-vmware"></a><span data-ttu-id="ff7cd-294">Подготовка виртуальной машины под управлением Red Hat в VMware</span><span class="sxs-lookup"><span data-stu-id="ff7cd-294">Prepare a Red Hat-based virtual machine from VMware</span></span>
### <a name="prerequisites"></a><span data-ttu-id="ff7cd-295">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ff7cd-295">Prerequisites</span></span>
<span data-ttu-id="ff7cd-296">В этом разделе предполагается, что вы уже установили виртуальную машину RHEL в VMWare.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-296">This section assumes that you have already installed a RHEL virtual machine in VMware.</span></span> <span data-ttu-id="ff7cd-297">Дополнительные сведения о том, как tooinstall операционной системы в VMware, отображается [руководство по установке VMware гостевой операционной системы](http://partnerweb.vmware.com/GOSIG/home.html).</span><span class="sxs-lookup"><span data-stu-id="ff7cd-297">For details about how tooinstall an operating system in VMware, see [VMware Guest Operating System Installation Guide](http://partnerweb.vmware.com/GOSIG/home.html).</span></span>

* <span data-ttu-id="ff7cd-298">При установке операционной системы Linux hello, рекомендуется использовать стандартный секции, а не LVM, что часто является по умолчанию hello для многих установок.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-298">When you install hello Linux operating system, we recommend that you use standard partitions rather than LVM, which is often hello default for many installations.</span></span> <span data-ttu-id="ff7cd-299">Это позволит избежать конфликтов имен LVM с клонированной виртуальной машины, особенно в том случае, если диск операционной системы никогда не должен toobe присоединенного tooanother виртуальной машины для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-299">This will avoid LVM name conflicts with cloned virtual machine, particularly if an operating system disk ever needs toobe attached tooanother virtual machine for troubleshooting.</span></span> <span data-ttu-id="ff7cd-300">При желании на дисках с данными можно использовать LVM или RAID.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-300">LVM or RAID can be used on data disks if preferred.</span></span>
* <span data-ttu-id="ff7cd-301">Не настраивайте переключения секции на диске операционной системы hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-301">Do not configure a swap partition on hello operating system disk.</span></span> <span data-ttu-id="ff7cd-302">Вы можете настроить toocreate агент Linux hello в файл подкачки на диске временного ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-302">You can configure hello Linux agent toocreate a swap file on hello temporary resource disk.</span></span> <span data-ttu-id="ff7cd-303">Дополнительные сведения об этом можно найти в hello, описанных ниже.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-303">You can find more information about this in hello steps that follow.</span></span>
* <span data-ttu-id="ff7cd-304">При создании виртуального жесткого диска hello выбрать **виртуального диска хранилища в одном файле**.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-304">When you create hello virtual hard disk, select **Store virtual disk as a single file**.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-vmware"></a><span data-ttu-id="ff7cd-305">Подготовка виртуальной машины RHEL 6 в VMware</span><span class="sxs-lookup"><span data-stu-id="ff7cd-305">Prepare a RHEL 6 virtual machine from VMware</span></span>
1. <span data-ttu-id="ff7cd-306">В RHEL 6 NetworkManager могут помешать hello агента Azure Linux.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-306">In RHEL 6, NetworkManager can interfere with hello Azure Linux agent.</span></span> <span data-ttu-id="ff7cd-307">Удаление этого пакета, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-307">Uninstall this package by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

2. <span data-ttu-id="ff7cd-308">Создайте файл с именем **сети** в hello/etc/sysconfig/каталог, содержащий hello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-308">Create a file named **network** in hello /etc/sysconfig/ directory that contains hello following text:</span></span>

        NETWORKING=yes
        HOSTNAME=localhost.localdomain

3. <span data-ttu-id="ff7cd-309">Создание или изменение hello `/etc/sysconfig/network-scripts/ifcfg-eth0` и добавьте следующий текст hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-309">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

4. <span data-ttu-id="ff7cd-310">Переместить (или удалить) hello udev правила tooavoid создания статические правила для интерфейса Ethernet hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-310">Move (or remove) hello udev rules tooavoid generating static rules for hello Ethernet interface.</span></span> <span data-ttu-id="ff7cd-311">Эти правила приводят к появлению проблем при клонировании виртуальной машины в Azure или Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-311">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

5. <span data-ttu-id="ff7cd-312">Убедитесь, сетевая служба hello начнется во время загрузки, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-312">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="ff7cd-313">Зарегистрируйте подписку Red Hat tooenable hello установку пакетов из репозитория RHEL hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-313">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="ff7cd-314">пакет WALinuxAgent Hello, `WALinuxAgent-<version>`, переданное toohello Red Hat дополнения репозитория.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-314">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="ff7cd-315">Включите hello дополнения репозиторий, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-315">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

8. <span data-ttu-id="ff7cd-316">Измените строку загрузки ядра hello в параметры grub tooinclude дополнительные ядра для Azure.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-316">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="ff7cd-317">toodo, откройте `/etc/default/grub` в текстовом редакторе и изменить hello `GRUB_CMDLINE_LINUX` параметра.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-317">toodo this, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="ff7cd-318">Например:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-318">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0"
   
   <span data-ttu-id="ff7cd-319">Это также позволит гарантировать, что все сообщения консоли отправляются toohello первый последовательный порт, который может помочь Azure поддержка с помощью отладки проблем.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-319">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="ff7cd-320">Кроме того рекомендуется удалить hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-320">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="ff7cd-321">Графический quiet начальной загрузки, не используются в облачной среде, где мы хотим, чтобы все журналы toobe hello, отправляемых toohello последовательного порта.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-321">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="ff7cd-322">Можно оставить hello `crashkernel` параметр настроен, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-322">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="ff7cd-323">Обратите внимание, что этот параметр уменьшает hello объем доступной памяти на виртуальной машине hello 128 МБ или более, которой может быть проблематичным на меньшие размеры виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-323">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="ff7cd-324">Добавьте tooinitramfs модули Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-324">Add Hyper-V modules tooinitramfs:</span></span>

    <span data-ttu-id="ff7cd-325">Изменить `/etc/dracut.conf`и добавьте следующие содержимое hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-325">Edit `/etc/dracut.conf`, and add hello following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="ff7cd-326">Повторно создайте initramfs:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-326">Rebuild initramfs:</span></span>

        # dracut -f -v

10. <span data-ttu-id="ff7cd-327">Убедитесь, что hello SSH сервер установлен и настроен toostart во время загрузки, которой обычно является по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-327">Ensure that hello SSH server is installed and configured toostart at boot time, which is usually hello default.</span></span> <span data-ttu-id="ff7cd-328">Изменить `/etc/ssh/sshd_config` tooinclude hello, следующей строкой:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-328">Modify `/etc/ssh/sshd_config` tooinclude hello following line:</span></span>

    <span data-ttu-id="ff7cd-329">ClientAliveInterval 180</span><span class="sxs-lookup"><span data-stu-id="ff7cd-329">ClientAliveInterval 180</span></span>

11. <span data-ttu-id="ff7cd-330">Установите агент Azure Linux hello, выполнив hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-330">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

12. <span data-ttu-id="ff7cd-331">Не создавайте подкачки на диске операционной системы hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-331">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="ff7cd-332">Hello Azure Linux Agent подкачки может автоматически настроить с помощью hello локальный диск ресурсов, которые toohello подключенных виртуальных машин после подготовки виртуальной машины hello в Azure.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-332">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="ff7cd-333">Обратите внимание, что hello локальный диск ресурсов — временный диск может очищаться при отмененной подготовкой hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-333">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="ff7cd-334">После установки hello Azure Linux Agent в предыдущем шаге hello, изменить следующие параметры в hello `/etc/waagent.conf` соответствующим образом:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-334">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. <span data-ttu-id="ff7cd-335">Отменить регистрацию подписки hello (при необходимости), выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-335">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="ff7cd-336">Запустите следующие команды toodeprovision hello виртуальной машины hello и подготовить его для подготовки в Azure:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-336">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="ff7cd-337">Завершите работу виртуальной машины hello и преобразуйте hello VMDK файл tooa VHD-файл.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-337">Shut down hello virtual machine, and convert hello VMDK file tooa .vhd file.</span></span>

    <span data-ttu-id="ff7cd-338">Сначала преобразовать формат tooraw hello изображения:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-338">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-6.8.vmdk rhel-6.8.raw

    <span data-ttu-id="ff7cd-339">Убедитесь, что размер hello hello необработанные изображения выравнивается 1 МБ.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-339">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="ff7cd-340">В противном случае округлять hello размер tooalign с 1 МБ:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-340">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="ff7cd-341">Преобразовать tooa hello неподготовленный диск фиксированного размера виртуального жесткого диска:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-341">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd

### <a name="prepare-a-rhel-7-virtual-machine-from-vmware"></a><span data-ttu-id="ff7cd-342">Подготовка виртуальной машины RHEL 7 в VMware</span><span class="sxs-lookup"><span data-stu-id="ff7cd-342">Prepare a RHEL 7 virtual machine from VMware</span></span>
1. <span data-ttu-id="ff7cd-343">Создание или изменение hello `/etc/sysconfig/network` и добавьте следующий текст hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-343">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

2. <span data-ttu-id="ff7cd-344">Создание или изменение hello `/etc/sysconfig/network-scripts/ifcfg-eth0` и добавьте следующий текст hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-344">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

3. <span data-ttu-id="ff7cd-345">Убедитесь, сетевая служба hello начнется во время загрузки, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-345">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

4. <span data-ttu-id="ff7cd-346">Зарегистрируйте подписку Red Hat tooenable hello установку пакетов из репозитория RHEL hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-346">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

5. <span data-ttu-id="ff7cd-347">Измените строку загрузки ядра hello в параметры grub tooinclude дополнительные ядра для Azure.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-347">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="ff7cd-348">toodo этого изменения, откройте `/etc/default/grub` в текстовом редакторе и изменить hello `GRUB_CMDLINE_LINUX` параметра.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-348">toodo this modification, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="ff7cd-349">Например:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-349">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="ff7cd-350">Такая конфигурация гарантирует, что все сообщения консоли отправляются toohello первый последовательный порт, который может помочь Azure поддержка с помощью отладки проблем.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-350">This configuration also ensures that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="ff7cd-351">Он также отключает новые соглашения об именах hello RHEL 7 для сетевых адаптеров.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-351">It also turns off hello new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="ff7cd-352">Кроме того рекомендуется удалить hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-352">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="ff7cd-353">Графический quiet начальной загрузки, не используются в облачной среде, где мы хотим, чтобы все журналы toobe hello, отправляемых toohello последовательного порта.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-353">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="ff7cd-354">Можно оставить hello `crashkernel` параметр настроен, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-354">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="ff7cd-355">Обратите внимание, что этот параметр уменьшает hello объем доступной памяти на виртуальной машине hello 128 МБ или более, которой может быть проблематичным на меньшие размеры виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-355">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

6. <span data-ttu-id="ff7cd-356">После завершения редактирования `/etc/default/grub`, запустите hello следующие конфигурацию grub hello toorebuild команды:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-356">After you are done editing `/etc/default/grub`, run hello following command toorebuild hello grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

7. <span data-ttu-id="ff7cd-357">Добавьте tooinitramfs модули Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-357">Add Hyper-V modules tooinitramfs.</span></span>

    <span data-ttu-id="ff7cd-358">Измените файл `/etc/dracut.conf`, добавив в него следующее содержимое:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-358">Edit `/etc/dracut.conf`, add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="ff7cd-359">Повторно создайте initramfs:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-359">Rebuild initramfs:</span></span>

        # dracut -f -v

8. <span data-ttu-id="ff7cd-360">Убедитесь, что hello SSH сервер установлен и настроен toostart во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-360">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span> <span data-ttu-id="ff7cd-361">Этот параметр обычно является по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-361">This setting is usually hello default.</span></span> <span data-ttu-id="ff7cd-362">Изменить `/etc/ssh/sshd_config` tooinclude hello, следующей строкой:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-362">Modify `/etc/ssh/sshd_config` tooinclude hello following line:</span></span>

        ClientAliveInterval 180

9. <span data-ttu-id="ff7cd-363">пакет WALinuxAgent Hello, `WALinuxAgent-<version>`, переданное toohello Red Hat дополнения репозитория.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-363">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="ff7cd-364">Включите hello дополнения репозиторий, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-364">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

10. <span data-ttu-id="ff7cd-365">Установите агент Azure Linux hello, выполнив hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-365">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

11. <span data-ttu-id="ff7cd-366">Не создавайте подкачки на диске операционной системы hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-366">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="ff7cd-367">Hello Azure Linux Agent подкачки может автоматически настроить с помощью hello локальный диск ресурсов, которые toohello подключенных виртуальных машин после подготовки виртуальной машины hello в Azure.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-367">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="ff7cd-368">Обратите внимание, что hello локальный диск ресурсов — временный диск может очищаться при отмененной подготовкой hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-368">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="ff7cd-369">После установки hello Azure Linux Agent в предыдущем шаге hello, изменить следующие параметры в hello `/etc/waagent.conf` соответствующим образом:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-369">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

12. <span data-ttu-id="ff7cd-370">Если необходимо toounregister hello подписки, запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-370">If you want toounregister hello subscription, run hello following command:</span></span>

        # sudo subscription-manager unregister

13. <span data-ttu-id="ff7cd-371">Запустите следующие команды toodeprovision hello виртуальной машины hello и подготовить его для подготовки в Azure:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-371">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

14. <span data-ttu-id="ff7cd-372">Завершите работу виртуальной машины hello и преобразовать формат VHD toohello файл VMDK hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-372">Shut down hello virtual machine, and convert hello VMDK file toohello VHD format.</span></span>

    <span data-ttu-id="ff7cd-373">Сначала преобразовать формат tooraw hello изображения:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-373">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-7.3.vmdk rhel-7.3.raw

    <span data-ttu-id="ff7cd-374">Убедитесь, что размер hello hello необработанные изображения выравнивается 1 МБ.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-374">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="ff7cd-375">В противном случае округлять hello размер tooalign с 1 МБ:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-375">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="ff7cd-376">Преобразовать tooa hello неподготовленный диск фиксированного размера виртуального жесткого диска:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-376">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-an-iso-by-using-a-kickstart-file-automatically"></a><span data-ttu-id="ff7cd-377">Подготовка виртуальной машины под управлением Red Hat из ISO-образа с помощью автоматического использования файла kickstart</span><span class="sxs-lookup"><span data-stu-id="ff7cd-377">Prepare a Red Hat-based virtual machine from an ISO by using a kickstart file automatically</span></span>
### <a name="prepare-a-rhel-7-virtual-machine-from-a-kickstart-file"></a><span data-ttu-id="ff7cd-378">Подготовка виртуальной машины RHEL 7 из файла kickstart</span><span class="sxs-lookup"><span data-stu-id="ff7cd-378">Prepare a RHEL 7 virtual machine from a kickstart file</span></span>

1.  <span data-ttu-id="ff7cd-379">Создайте файл пуска, включающий следующие содержимое hello и сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-379">Create a kickstart file that includes hello following content, and save hello file.</span></span> <span data-ttu-id="ff7cd-380">Дополнительные сведения об установке пуска см. в разделе hello [руководство по установке пуска](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span><span class="sxs-lookup"><span data-stu-id="ff7cd-380">For details about kickstart installation, see hello [Kickstart Installation Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span></span>

        # Kickstart for provisioning a RHEL 7 Azure VM

        # System authorization information
          auth --enableshadow --passalgo=sha512

        # Use graphical install
        text

        # Do not run hello Setup Agent on first boot
        firstboot --disable

        # Keyboard layouts
        keyboard --vckeymap=us --xlayouts='us'

        # System language
        lang en_US.UTF-8

        # Network information
        network  --bootproto=dhcp

        # Root password
        rootpw --plaintext "to_be_disabled"

        # System services
        services --enabled="sshd,waagent,NetworkManager"

        # System timezone
        timezone Etc/UTC --isUtc --ntpservers 0.rhel.pool.ntp.org,1.rhel.pool.ntp.org,2.rhel.pool.ntp.org,3.rhel.pool.ntp.org

        # Partition clearing information
        clearpart --all --initlabel

        # Clear hello MBR
        zerombr

        # Disk partitioning information
        part /boot --fstype="xfs" --size=500
        part / --fstyp="xfs" --size=1 --grow --asprimary

        # System bootloader configuration
        bootloader --location=mbr

        # Firewall configuration
        firewall --disabled

        # Enable SELinux
        selinux --enforcing

        # Don't configure X
        skipx

        # Power down hello machine after install
        poweroff

        %packages
        @base
        @console-internet
        chrony
        sudo
        parted
        -dracut-config-rescue

        %end

        %post --log=/var/log/anaconda/post-install.log

        #!/bin/bash

        # Register Red Hat Subscription
        subscription-manager register --username=XXX --password=XXX --auto-attach --force

        # Install latest repo update
        yum update -y

        # Enable extras repo
        subscription-manager repos --enable=rhel-7-server-extras-rpms

        # Install WALinuxAgent
        yum install -y WALinuxAgent

        # Unregister Red Hat subscription
        subscription-manager unregister

        # Enable waaagent at boot-up
        systemctl enable waagent

        # Disable hello root account
        usermod root -p '!!'

        # Configure swap in WALinuxAgent
        sed -i 's/^\(ResourceDisk\.EnableSwap\)=[Nn]$/\1=y/g' /etc/waagent.conf
        sed -i 's/^\(ResourceDisk\.SwapSizeMB\)=[0-9]*$/\1=2048/g' /etc/waagent.conf

        # Set hello cmdline
        sed -i 's/^\(GRUB_CMDLINE_LINUX\)=".*"$/\1="console=tty1 console=ttyS0 earlyprintk=ttyS0 rootdelay=300"/g' /etc/default/grub

        # Enable SSH keepalive
        sed -i 's/^#\(ClientAliveInterval\).*$/\1 180/g' /etc/ssh/sshd_config

        # Build hello grub cfg
        grub2-mkconfig -o /boot/grub2/grub.cfg

        # Configure network
        cat << EOF > /etc/sysconfig/network-scripts/ifcfg-eth0
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no
        EOF

        # Deprovision and prepare for Azure
        waagent -force -deprovision

        %end

2. <span data-ttu-id="ff7cd-381">Поместите файл пуска hello, где hello установки системы к нему возможен доступ.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-381">Place hello kickstart file where hello installation system can access it.</span></span>

3. <span data-ttu-id="ff7cd-382">Создайте новую виртуальную машину в диспетчере Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-382">In Hyper-V Manager, create a new virtual machine.</span></span> <span data-ttu-id="ff7cd-383">На hello **подключить виртуальный жесткий диск** выберите **подключить виртуальный жесткий диск позднее**и завершения приветствия мастера создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-383">On hello **Connect Virtual Hard Disk** page, select **Attach a virtual hard disk later**, and complete hello New Virtual Machine Wizard.</span></span>

4. <span data-ttu-id="ff7cd-384">Откройте параметры виртуальной машины hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-384">Open hello virtual machine settings:</span></span>

    <span data-ttu-id="ff7cd-385">а.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-385">a.</span></span>  <span data-ttu-id="ff7cd-386">Присоедините новую виртуальную машину toohello виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-386">Attach a new virtual hard disk toohello virtual machine.</span></span> <span data-ttu-id="ff7cd-387">Убедитесь, что tooselect **формат VHD** и **фиксированного размера**.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-387">Make sure tooselect **VHD Format** and **Fixed Size**.</span></span>

    <span data-ttu-id="ff7cd-388">b.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-388">b.</span></span>  <span data-ttu-id="ff7cd-389">Присоедините hello установки ISO toohello DVD-дисковод.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-389">Attach hello installation ISO toohello DVD drive.</span></span>

    <span data-ttu-id="ff7cd-390">c.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-390">c.</span></span>  <span data-ttu-id="ff7cd-391">Задать hello BIOS tooboot с компакт-диска.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-391">Set hello BIOS tooboot from CD.</span></span>

5. <span data-ttu-id="ff7cd-392">Запустите виртуальную машину hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-392">Start hello virtual machine.</span></span> <span data-ttu-id="ff7cd-393">После появления руководство по установке hello **вкладка** параметры загрузки tooconfigure hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-393">When hello installation guide appears, press **Tab** tooconfigure hello boot options.</span></span>

6. <span data-ttu-id="ff7cd-394">Ввод `inst.ks=<hello location of hello kickstart file>` в конце hello hello варианты загрузки и нажмите клавишу **ввод**.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-394">Enter `inst.ks=<hello location of hello kickstart file>` at hello end of hello boot options, and press **Enter**.</span></span>

7. <span data-ttu-id="ff7cd-395">Дождитесь установки toofinish hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-395">Wait for hello installation toofinish.</span></span> <span data-ttu-id="ff7cd-396">После завершения, hello виртуальной машины будет завершена автоматически.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-396">When it's finished, hello virtual machine will be shut down automatically.</span></span> <span data-ttu-id="ff7cd-397">ДИСК Linux имеет теперь готовы toobe отправлен tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-397">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="known-issues"></a><span data-ttu-id="ff7cd-398">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="ff7cd-398">Known issues</span></span>
### <a name="hello-hyper-v-driver-could-not-be-included-in-hello-initial-ram-disk-when-using-a-non-hyper-v-hypervisor"></a><span data-ttu-id="ff7cd-399">драйвер Hello Hyper-V не будут включены в начальной Электронный диск hello, при использовании низкоуровневая оболочка не Hyper-V</span><span class="sxs-lookup"><span data-stu-id="ff7cd-399">hello Hyper-V driver could not be included in hello initial RAM disk when using a non-Hyper-V hypervisor</span></span>

<span data-ttu-id="ff7cd-400">В некоторых случаях Linux установщики могут не включать hello драйверы для Hyper-V в hello начальной Электронный диск (initrd или initramfs) Если Linux обнаружит, что он работает в среде Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-400">In some cases, Linux installers might not include hello drivers for Hyper-V in hello initial RAM disk (initrd or initramfs) unless Linux detects that it is running in a Hyper-V environment.</span></span>

<span data-ttu-id="ff7cd-401">При использовании tooprepare системы (то есть Virtualbox, Xen, т. д.) другой виртуализации образа Linux, может потребоваться tooensure initrd toorebuild, по крайней мере hello hv_vmbus и модули ядра hv_storvsc доступен на hello начальной Электронный диск.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-401">When you're using a different virtualization system (that is, Virtualbox, Xen, etc.) tooprepare your Linux image, you might need toorebuild initrd tooensure that at least hello hv_vmbus and hv_storvsc kernel modules are available on hello initial RAM disk.</span></span> <span data-ttu-id="ff7cd-402">Это известная проблема по крайней мере в системах, основанных на вышестоящий Red Hat распространения hello.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-402">This is a known issue at least on systems that are based on hello upstream Red Hat distribution.</span></span>

<span data-ttu-id="ff7cd-403">tooresolve эту проблему, добавьте tooinitramfs модули Hyper-V и перестроить его:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-403">tooresolve this issue, add Hyper-V modules tooinitramfs and rebuild it:</span></span>

<span data-ttu-id="ff7cd-404">Изменить `/etc/dracut.conf`и добавьте следующие содержимое hello:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-404">Edit `/etc/dracut.conf`, and add hello following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

<span data-ttu-id="ff7cd-405">Повторно создайте initramfs:</span><span class="sxs-lookup"><span data-stu-id="ff7cd-405">Rebuild initramfs:</span></span>

        # dracut -f -v

<span data-ttu-id="ff7cd-406">Дополнительные сведения см. в разделе hello сведения [перестроение initramfs](https://access.redhat.com/solutions/1958).</span><span class="sxs-lookup"><span data-stu-id="ff7cd-406">For more details, see hello information about [rebuilding initramfs](https://access.redhat.com/solutions/1958).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff7cd-407">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ff7cd-407">Next steps</span></span>
<span data-ttu-id="ff7cd-408">Вы являетесь теперь готовы toouse Red Hat Enterprise Linux виртуальный жесткий диск toocreate новых виртуальных машин в Azure.</span><span class="sxs-lookup"><span data-stu-id="ff7cd-408">You're now ready toouse your Red Hat Enterprise Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="ff7cd-409">Если это первый раз, что идет Отправка tooAzure файл .vhd hello hello см. шаги 2 и 3 в [Создание и передача виртуального жесткого диска, который содержит операционную систему Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ff7cd-409">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="ff7cd-410">Дополнительные сведения о hello низкоуровневых оболочках, которые являются сертифицированным toorun Red Hat Enterprise Linux, см. в разделе [веб-сайта hello Red Hat](https://access.redhat.com/certified-hypervisors).</span><span class="sxs-lookup"><span data-stu-id="ff7cd-410">For more details about hello hypervisors that are certified toorun Red Hat Enterprise Linux, see [hello Red Hat website](https://access.redhat.com/certified-hypervisors).</span></span>
