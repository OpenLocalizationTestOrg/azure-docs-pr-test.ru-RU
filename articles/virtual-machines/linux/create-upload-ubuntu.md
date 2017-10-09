---
title: "aaaCreate и отправка виртуального жесткого диска Linux Ubuntu в Azure"
description: "Узнайте toocreate и отправить в Azure виртуального жесткого диска (VHD), содержащий операционную систему, Ubuntu Linux."
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
ms.openlocfilehash: cc546a487f769b32432a7e80ddcd0f6af44e201f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-an-ubuntu-virtual-machine-for-azure"></a><span data-ttu-id="0ee9a-103">Подготовка виртуальной машины Ubuntu для Azure</span><span class="sxs-lookup"><span data-stu-id="0ee9a-103">Prepare an Ubuntu virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="official-ubuntu-cloud-images"></a><span data-ttu-id="0ee9a-104">Официальные образы облаков Ubuntu</span><span class="sxs-lookup"><span data-stu-id="0ee9a-104">Official Ubuntu cloud images</span></span>
<span data-ttu-id="0ee9a-105">Теперь Ubuntu публикует официальные виртуальные жесткие диски Azure, загрузить которые можно по адресу: [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span><span class="sxs-lookup"><span data-stu-id="0ee9a-105">Ubuntu now publishes official Azure VHDs for download at [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span></span> <span data-ttu-id="0ee9a-106">Если требуются специализированные изображения Ubuntu toobuild для Azure, вместо того чтобы использовать hello Ручная процедура под ним рекомендуемые toostart с этих известных работает виртуальных жестких дисков и при необходимости настроить.</span><span class="sxs-lookup"><span data-stu-id="0ee9a-106">If you need toobuild your own specialized Ubuntu image for Azure, rather than use hello manual procedure below it is recommended toostart with these known working VHDs and customize as needed.</span></span> <span data-ttu-id="0ee9a-107">последние версии образа Hello всегда находятся в hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="0ee9a-107">hello latest image releases can always be found at hello following locations:</span></span>

* <span data-ttu-id="0ee9a-108">Ubuntu 12.04/Precise: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="0ee9a-108">Ubuntu 12.04/Precise: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="0ee9a-109">Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="0ee9a-109">Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="0ee9a-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="0ee9a-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ee9a-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0ee9a-111">Prerequisites</span></span>
<span data-ttu-id="0ee9a-112">В этой статье предполагается, что вы уже установили Ubuntu Linux операционной системы tooa виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="0ee9a-112">This article assumes that you have already installed an Ubuntu Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="0ee9a-113">Существуют несколько средства toocreate VHD-файлы, например решение виртуализации, таких как Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="0ee9a-113">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="0ee9a-114">Инструкции см. в разделе [Установка hello роль Hyper-V и настройка виртуальной машины](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="0ee9a-114">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="0ee9a-115">**Замечания по установке Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="0ee9a-115">**Ubuntu installation notes**</span></span>

* <span data-ttu-id="0ee9a-116">Дополнительные сведения о подготовке Linux для Azure см. в разделе [Общие замечания по установке Linux](create-upload-generic.md#general-linux-installation-notes).</span><span class="sxs-lookup"><span data-stu-id="0ee9a-116">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="0ee9a-117">Hello формат VHDX не поддерживается только в Azure, **фиксированный VHD**.</span><span class="sxs-lookup"><span data-stu-id="0ee9a-117">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="0ee9a-118">Можно преобразовать формат tooVHD hello диска, с помощью диспетчера Hyper-V или hello командлет convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="0ee9a-118">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span>
* <span data-ttu-id="0ee9a-119">При установке системы Linux hello рекомендуется использовать стандартный секции, а не LVM (часто hello по умолчанию для многих установок).</span><span class="sxs-lookup"><span data-stu-id="0ee9a-119">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="0ee9a-120">Это позволит избежать конфликтов имен LVM с клонированные виртуальные машины, особенно в том случае, если на диске ОС никогда не требуется tooanother toobe присоединенного виртуальной Машины для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="0ee9a-120">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="0ee9a-121">Для дисков данных можно использовать [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) или [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0ee9a-121">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="0ee9a-122">Не настраивайте переключения секции на диске ОС hello.</span><span class="sxs-lookup"><span data-stu-id="0ee9a-122">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="0ee9a-123">агент Linux Hello может быть настроенный toocreate файл подкачки на диске временного ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="0ee9a-123">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="0ee9a-124">Дополнительные сведения об этом можно найти в hello описанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="0ee9a-124">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="0ee9a-125">Все виртуальные жесткие диски hello должны иметь размеры, кратные 1 МБ.</span><span class="sxs-lookup"><span data-stu-id="0ee9a-125">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="manual-steps"></a><span data-ttu-id="0ee9a-126">Создание вручную</span><span class="sxs-lookup"><span data-stu-id="0ee9a-126">Manual steps</span></span>
> [!NOTE]
> <span data-ttu-id="0ee9a-127">Прежде чем toocreate собственное изображение Ubuntu для Azure, возможно, следует с помощью hello предварительно построение и тестирование образов из [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) вместо него.</span><span class="sxs-lookup"><span data-stu-id="0ee9a-127">Before attempting toocreate your own custom Ubuntu image for Azure, please consider using hello pre-built and tested images from [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) instead.</span></span>
> 
> 

1. <span data-ttu-id="0ee9a-128">Hello центральной панели диспетчера Hyper-V выберите виртуальную машину hello.</span><span class="sxs-lookup"><span data-stu-id="0ee9a-128">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="0ee9a-129">Нажмите кнопку **Connect** окна hello tooopen для hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0ee9a-129">Click **Connect** tooopen hello window for hello virtual machine.</span></span>

3. <span data-ttu-id="0ee9a-130">Замените hello текущего репозитории в Azure репозиториев hello изображения toouse Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="0ee9a-130">Replace hello current repositories in hello image toouse Ubuntu's Azure repos.</span></span> <span data-ttu-id="0ee9a-131">Hello шаги будут немного отличаться в зависимости от версии Ubuntu hello.</span><span class="sxs-lookup"><span data-stu-id="0ee9a-131">hello steps vary slightly depending on hello Ubuntu version.</span></span>
   
    <span data-ttu-id="0ee9a-132">Прежде чем изменять `/etc/apt/sources.list`, это рекомендуемое toomake резервной копии:</span><span class="sxs-lookup"><span data-stu-id="0ee9a-132">Before editing `/etc/apt/sources.list`, it is recommended toomake a backup:</span></span>
   
        # sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

    <span data-ttu-id="0ee9a-133">Ubuntu 12,04:</span><span class="sxs-lookup"><span data-stu-id="0ee9a-133">Ubuntu 12.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="0ee9a-134">Ubuntu 14.04:</span><span class="sxs-lookup"><span data-stu-id="0ee9a-134">Ubuntu 14.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="0ee9a-135">Ubuntu 16.04:</span><span class="sxs-lookup"><span data-stu-id="0ee9a-135">Ubuntu 16.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

4. <span data-ttu-id="0ee9a-136">Hello Ubuntu Azure изображения теперь подписаны hello *включения оборудования* ядра (HWE).</span><span class="sxs-lookup"><span data-stu-id="0ee9a-136">hello Ubuntu Azure images are now following hello *hardware enablement* (HWE) kernel.</span></span> <span data-ttu-id="0ee9a-137">Обновление ядра последнюю toohello операционной системы hello, выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="0ee9a-137">Update hello operating system toohello latest kernel by running hello following commands:</span></span>

    <span data-ttu-id="0ee9a-138">Ubuntu 12,04:</span><span class="sxs-lookup"><span data-stu-id="0ee9a-138">Ubuntu 12.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-generic-lts-trusty linux-cloud-tools-generic-lts-trusty
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot
   
    <span data-ttu-id="0ee9a-139">Ubuntu 14.04:</span><span class="sxs-lookup"><span data-stu-id="0ee9a-139">Ubuntu 14.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-virtual-lts-vivid linux-lts-vivid-tools-common
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot

    <span data-ttu-id="0ee9a-140">Ubuntu 16.04:</span><span class="sxs-lookup"><span data-stu-id="0ee9a-140">Ubuntu 16.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-generic-hwe-16.04 linux-cloud-tools-generic-hwe-16.04
        (recommended) sudo apt-get dist-upgrade

        # sudo reboot

    <span data-ttu-id="0ee9a-141">**См. также:**</span><span class="sxs-lookup"><span data-stu-id="0ee9a-141">**See also:**</span></span>
    - [<span data-ttu-id="0ee9a-142">https://wiki.ubuntu.com/Kernel/LTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="0ee9a-142">https://wiki.ubuntu.com/Kernel/LTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/LTSEnablementStack)
    - [<span data-ttu-id="0ee9a-143">https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="0ee9a-143">https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack)


5. <span data-ttu-id="0ee9a-144">Измените строку загрузки ядра hello Grub tooinclude дополнительных системных параметров для Azure.</span><span class="sxs-lookup"><span data-stu-id="0ee9a-144">Modify hello kernel boot line for Grub tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="0ee9a-145">этом откройте toodo `/etc/default/grub` в текстовом редакторе, найдите hello переменную с именем `GRUB_CMDLINE_LINUX_DEFAULT` (или добавьте ее при необходимости) и изменить его hello tooinclude следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="0ee9a-145">toodo this open `/etc/default/grub` in a text editor, find hello variable called `GRUB_CMDLINE_LINUX_DEFAULT` (or add it if needed) and edit it tooinclude hello following parameters:</span></span>
   
        GRUB_CMDLINE_LINUX_DEFAULT="console=tty1 console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300"

    <span data-ttu-id="0ee9a-146">Сохраните и закройте файл, а затем выполните команду `sudo update-grub`.</span><span class="sxs-lookup"><span data-stu-id="0ee9a-146">Save and close this file, and then run `sudo update-grub`.</span></span> <span data-ttu-id="0ee9a-147">Это позволит гарантировать, что все сообщения консоли отправляются toohello первый последовательный порт, который может помочь Azure технической поддержки с отладки проблем с.</span><span class="sxs-lookup"><span data-stu-id="0ee9a-147">This will ensure all console messages are sent toohello first serial port, which can assist Azure technical support with debugging issues.</span></span>

6. <span data-ttu-id="0ee9a-148">Убедитесь, что hello SSH сервер установлен и настроен toostart во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="0ee9a-148">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="0ee9a-149">Обычно это происходит по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="0ee9a-149">This is usually hello default.</span></span>

7. <span data-ttu-id="0ee9a-150">Установите агент Azure Linux hello:</span><span class="sxs-lookup"><span data-stu-id="0ee9a-150">Install hello Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install walinuxagent

    >[!Note]
    <span data-ttu-id="0ee9a-151">Hello `walinuxagent` пакет может удалять hello `NetworkManager` и `NetworkManager-gnome` пакеты, если они установлены.</span><span class="sxs-lookup"><span data-stu-id="0ee9a-151">hello `walinuxagent` package may remove hello `NetworkManager` and `NetworkManager-gnome` packages, if they are installed.</span></span>

8. <span data-ttu-id="0ee9a-152">Запустите следующие команды toodeprovision hello виртуальной машины hello и подготовить его для подготовки в Azure:</span><span class="sxs-lookup"><span data-stu-id="0ee9a-152">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

9. <span data-ttu-id="0ee9a-153">В диспетчере Hyper-V выберите **Действие -> Завершение работы**.</span><span class="sxs-lookup"><span data-stu-id="0ee9a-153">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="0ee9a-154">ДИСК Linux имеет теперь готовы toobe отправлен tooAzure.</span><span class="sxs-lookup"><span data-stu-id="0ee9a-154">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ee9a-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0ee9a-155">Next steps</span></span>
<span data-ttu-id="0ee9a-156">Вы являетесь теперь готовы toouse Ubuntu Linux виртуальный жесткий диск toocreate новых виртуальных машин в Azure.</span><span class="sxs-lookup"><span data-stu-id="0ee9a-156">You're now ready toouse your Ubuntu Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="0ee9a-157">Если это первый раз, что идет Отправка tooAzure файл .vhd hello hello см. шаги 2 и 3 в [Создание и передача виртуального жесткого диска, который содержит операционную систему Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0ee9a-157">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="references"></a><span data-ttu-id="0ee9a-158">Ссылки</span><span class="sxs-lookup"><span data-stu-id="0ee9a-158">References</span></span>
<span data-ttu-id="0ee9a-159">Ядро Ubuntu с расширенной поддержкой оборудования (HWE):</span><span class="sxs-lookup"><span data-stu-id="0ee9a-159">Ubuntu hardware enablement (HWE) kernel:</span></span>

* [<span data-ttu-id="0ee9a-160">http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html</span><span class="sxs-lookup"><span data-stu-id="0ee9a-160">http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html</span></span>](http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html)
* [<span data-ttu-id="0ee9a-161">http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html</span><span class="sxs-lookup"><span data-stu-id="0ee9a-161">http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html</span></span>](http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html)

