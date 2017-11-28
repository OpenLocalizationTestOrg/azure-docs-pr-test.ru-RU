---
title: "Создание и передача виртуального жесткого диска с ОС Ubuntu Linux в Azure"
description: "Узнайте, как создать и передать виртуальный жесткий диск (VHD-файл) Azure, содержащий операционную систему Ubuntu Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 3e097959-84fc-4f6a-8cc8-35e087fd1542
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 4496b34ff88ca1e08cc74788ae09d787d4399eaf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="prepare-an-ubuntu-virtual-machine-for-azure"></a><span data-ttu-id="e042a-103">Подготовка виртуальной машины Ubuntu для Azure</span><span class="sxs-lookup"><span data-stu-id="e042a-103">Prepare an Ubuntu virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="official-ubuntu-cloud-images"></a><span data-ttu-id="e042a-104">Официальные образы облаков Ubuntu</span><span class="sxs-lookup"><span data-stu-id="e042a-104">Official Ubuntu cloud images</span></span>
<span data-ttu-id="e042a-105">Теперь Ubuntu публикует официальные виртуальные жесткие диски Azure, загрузить которые можно по адресу: [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span><span class="sxs-lookup"><span data-stu-id="e042a-105">Ubuntu now publishes official Azure VHDs for download at [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span></span> <span data-ttu-id="e042a-106">Если вам нужно создать свой собственный, особый образ Ubuntu для Azure, не выполняйте описанную ниже процедуру, а начните с таких заведомо рабочих виртуальных жестких дисков и настройте их так, как вам требуется.</span><span class="sxs-lookup"><span data-stu-id="e042a-106">If you need to build your own specialized Ubuntu image for Azure, rather than use the manual procedure below it is recommended to start with these known working VHDs and customize as needed.</span></span> <span data-ttu-id="e042a-107">Последние выпуски образов можно всегда найти в следующих расположениях:</span><span class="sxs-lookup"><span data-stu-id="e042a-107">The latest image releases can always be found at the following locations:</span></span>

* <span data-ttu-id="e042a-108">Ubuntu 12.04/Precise: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="e042a-108">Ubuntu 12.04/Precise: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="e042a-109">Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="e042a-109">Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="e042a-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="e042a-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e042a-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e042a-111">Prerequisites</span></span>
<span data-ttu-id="e042a-112">В этой статье предполагается, что вы уже установили операционную систему Ubuntu Linux на виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="e042a-112">This article assumes that you have already installed an Ubuntu Linux operating system to a virtual hard disk.</span></span> <span data-ttu-id="e042a-113">Существует несколько средств для создания VHD-файлов, например решение для виртуализации, такое как Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="e042a-113">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="e042a-114">Инструкции см. в разделе [Установка роли Hyper-V и настройка виртуальной машины](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="e042a-114">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="e042a-115">**Замечания по установке Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="e042a-115">**Ubuntu installation notes**</span></span>

* <span data-ttu-id="e042a-116">Дополнительные сведения о подготовке Linux для Azure см. в разделе [Общие замечания по установке Linux](create-upload-generic.md#general-linux-installation-notes).</span><span class="sxs-lookup"><span data-stu-id="e042a-116">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="e042a-117">Формат VHDX не поддерживается в Azure, поддерживается только **фиксированный VHD**.</span><span class="sxs-lookup"><span data-stu-id="e042a-117">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="e042a-118">Можно преобразовать диск в формат VHD с помощью диспетчера Hyper-V или командлета convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="e042a-118">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span></span>
* <span data-ttu-id="e042a-119">При установке системы Linux рекомендуется использовать стандартные разделы, а не LVM (как правило, значение по умолчанию во многих дистрибутивах).</span><span class="sxs-lookup"><span data-stu-id="e042a-119">When installing the Linux system it is recommended that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="e042a-120">Это позволит избежать конфликта имен LVM при клонировании виртуальных машин, особенно если диск с OC может быть подключен к другой ВМ в целях устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="e042a-120">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another VM for troubleshooting.</span></span> <span data-ttu-id="e042a-121">Для дисков данных можно использовать [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) или [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e042a-121">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="e042a-122">Не настраивайте раздел подкачки на диске с ОС.</span><span class="sxs-lookup"><span data-stu-id="e042a-122">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="e042a-123">Можно настроить агент Linux для создания файла подкачки на временном диске ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e042a-123">The Linux agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="e042a-124">Дополнительные сведения описаны далее.</span><span class="sxs-lookup"><span data-stu-id="e042a-124">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="e042a-125">Все VHD-диски должны иметь размер, кратный 1 МБ.</span><span class="sxs-lookup"><span data-stu-id="e042a-125">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="manual-steps"></a><span data-ttu-id="e042a-126">Создание вручную</span><span class="sxs-lookup"><span data-stu-id="e042a-126">Manual steps</span></span>
> [!NOTE]
> <span data-ttu-id="e042a-127">Прежде чем создавать собственный образ Ubuntu для Azure, рассмотрите возможность применения предварительно созданных и проверенных образов с сайта [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) .</span><span class="sxs-lookup"><span data-stu-id="e042a-127">Before attempting to create your own custom Ubuntu image for Azure, please consider using the pre-built and tested images from [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) instead.</span></span>
> 
> 

1. <span data-ttu-id="e042a-128">На центральной панели диспетчера Hyper-V выберите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="e042a-128">In the center pane of Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="e042a-129">Щелкните **Подключение** , чтобы открыть окно виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e042a-129">Click **Connect** to open the window for the virtual machine.</span></span>

3. <span data-ttu-id="e042a-130">Замените текущие репозитории в образе на репозитории Ubuntu Azure.</span><span class="sxs-lookup"><span data-stu-id="e042a-130">Replace the current repositories in the image to use Ubuntu's Azure repos.</span></span> <span data-ttu-id="e042a-131">Эти действия могут незначительно отличаться в зависимости от версии Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="e042a-131">The steps vary slightly depending on the Ubuntu version.</span></span>
   
    <span data-ttu-id="e042a-132">Перед редактированием `/etc/apt/sources.list` рекомендуется сделать резервную копию:</span><span class="sxs-lookup"><span data-stu-id="e042a-132">Before editing `/etc/apt/sources.list`, it is recommended to make a backup:</span></span>
   
        # sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

    <span data-ttu-id="e042a-133">Ubuntu 12,04:</span><span class="sxs-lookup"><span data-stu-id="e042a-133">Ubuntu 12.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="e042a-134">Ubuntu 14.04:</span><span class="sxs-lookup"><span data-stu-id="e042a-134">Ubuntu 14.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="e042a-135">Ubuntu 16.04:</span><span class="sxs-lookup"><span data-stu-id="e042a-135">Ubuntu 16.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

4. <span data-ttu-id="e042a-136">Теперь образы Azure Ubuntu используют ядро с *расширенной поддержкой оборудования* (HWE).</span><span class="sxs-lookup"><span data-stu-id="e042a-136">The Ubuntu Azure images are now following the *hardware enablement* (HWE) kernel.</span></span> <span data-ttu-id="e042a-137">Обновите операционную систему до последней версии ядра, выполнив следующие команды.</span><span class="sxs-lookup"><span data-stu-id="e042a-137">Update the operating system to the latest kernel by running the following commands:</span></span>

    <span data-ttu-id="e042a-138">Ubuntu 12,04:</span><span class="sxs-lookup"><span data-stu-id="e042a-138">Ubuntu 12.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-generic-lts-trusty linux-cloud-tools-generic-lts-trusty
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot
   
    <span data-ttu-id="e042a-139">Ubuntu 14.04:</span><span class="sxs-lookup"><span data-stu-id="e042a-139">Ubuntu 14.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-virtual-lts-vivid linux-lts-vivid-tools-common
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot

    <span data-ttu-id="e042a-140">Ubuntu 16.04:</span><span class="sxs-lookup"><span data-stu-id="e042a-140">Ubuntu 16.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-generic-hwe-16.04 linux-cloud-tools-generic-hwe-16.04
        (recommended) sudo apt-get dist-upgrade

        # sudo reboot

    <span data-ttu-id="e042a-141">**См. также:**</span><span class="sxs-lookup"><span data-stu-id="e042a-141">**See also:**</span></span>
    - [<span data-ttu-id="e042a-142">https://wiki.ubuntu.com/Kernel/LTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="e042a-142">https://wiki.ubuntu.com/Kernel/LTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/LTSEnablementStack)
    - [<span data-ttu-id="e042a-143">https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="e042a-143">https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack)


5. <span data-ttu-id="e042a-144">Измените строку загрузки ядра в конфигурации Grub, чтобы включить дополнительные параметры ядра для Azure.</span><span class="sxs-lookup"><span data-stu-id="e042a-144">Modify the kernel boot line for Grub to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="e042a-145">Для этого откройте файл `/etc/default/grub` в текстовом редакторе, найдите переменную `GRUB_CMDLINE_LINUX_DEFAULT` (или добавьте ее, если это необходимо) и измените ее, включив следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="e042a-145">To do this open `/etc/default/grub` in a text editor, find the variable called `GRUB_CMDLINE_LINUX_DEFAULT` (or add it if needed) and edit it to include the following parameters:</span></span>
   
        GRUB_CMDLINE_LINUX_DEFAULT="console=tty1 console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300"

    <span data-ttu-id="e042a-146">Сохраните и закройте файл, а затем выполните команду `sudo update-grub`.</span><span class="sxs-lookup"><span data-stu-id="e042a-146">Save and close this file, and then run `sudo update-grub`.</span></span> <span data-ttu-id="e042a-147">Это гарантирует отправку всех сообщений консоли на первый последовательный порт, что может помочь технической поддержке Azure в плане отладки.</span><span class="sxs-lookup"><span data-stu-id="e042a-147">This will ensure all console messages are sent to the first serial port, which can assist Azure technical support with debugging issues.</span></span>

6. <span data-ttu-id="e042a-148">Убедитесь, что SSH-сервер установлен и настроен для включения во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="e042a-148">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="e042a-149">Обычно это сделано по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e042a-149">This is usually the default.</span></span>

7. <span data-ttu-id="e042a-150">Установите агент Linux для Azure:</span><span class="sxs-lookup"><span data-stu-id="e042a-150">Install the Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install walinuxagent

    >[!Note]
    <span data-ttu-id="e042a-151">Установка пакета `walinuxagent` приведет к удалению пакетов `NetworkManager` и `NetworkManager-gnome` (если они установлены).</span><span class="sxs-lookup"><span data-stu-id="e042a-151">The `walinuxagent` package may remove the `NetworkManager` and `NetworkManager-gnome` packages, if they are installed.</span></span>

8. <span data-ttu-id="e042a-152">Выполните следующие команды, чтобы отменить подготовку виртуальной машины и подготовить ее в Azure:</span><span class="sxs-lookup"><span data-stu-id="e042a-152">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

9. <span data-ttu-id="e042a-153">В диспетчере Hyper-V выберите **Действие -> Завершение работы**.</span><span class="sxs-lookup"><span data-stu-id="e042a-153">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="e042a-154">Виртуальный жесткий диск Linux готов к передаче в Azure.</span><span class="sxs-lookup"><span data-stu-id="e042a-154">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e042a-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e042a-155">Next steps</span></span>
<span data-ttu-id="e042a-156">Теперь виртуальный жесткий диск Ubuntu Linux можно использовать для создания новых виртуальных машин Azure.</span><span class="sxs-lookup"><span data-stu-id="e042a-156">You're now ready to use your Ubuntu Linux virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="e042a-157">Если вы загружаете VHD-файл в Azure впервые, обратитесь к шагам 2 и 3 в статье [Создание и загрузка виртуального жесткого диска, содержащего операционную систему Linux](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e042a-157">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="references"></a><span data-ttu-id="e042a-158">Ссылки</span><span class="sxs-lookup"><span data-stu-id="e042a-158">References</span></span>
<span data-ttu-id="e042a-159">Ядро Ubuntu с расширенной поддержкой оборудования (HWE):</span><span class="sxs-lookup"><span data-stu-id="e042a-159">Ubuntu hardware enablement (HWE) kernel:</span></span>

* [<span data-ttu-id="e042a-160">http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html</span><span class="sxs-lookup"><span data-stu-id="e042a-160">http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html</span></span>](http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html)
* [<span data-ttu-id="e042a-161">http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html</span><span class="sxs-lookup"><span data-stu-id="e042a-161">http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html</span></span>](http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html)

