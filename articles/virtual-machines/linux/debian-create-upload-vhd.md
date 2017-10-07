---
title: "aaaPrepare Debian Linux VHD в Azure | Документы Microsoft"
description: "Узнайте, как файлы toocreate Debian 7 и 8 виртуального жесткого диска для развертывания в Azure."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: a6de7a7c-cc70-44e7-aed0-2ae6884d401a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: e67d126de3db146357a6509aedb5f478576768f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-debian-vhd-for-azure"></a><span data-ttu-id="df2dc-103">Подготовка виртуального жесткого диска Debian для Azure</span><span class="sxs-lookup"><span data-stu-id="df2dc-103">Prepare a Debian VHD for Azure</span></span>
## <a name="prerequisites"></a><span data-ttu-id="df2dc-104">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="df2dc-104">Prerequisites</span></span>
<span data-ttu-id="df2dc-105">В этом разделе предполагается, что вы уже установили операционной системы Debian Linux ISO-файла, загруженные из hello [Debian веб-сайт](https://www.debian.org/distrib/) tooa виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="df2dc-105">This section assumes that you have already installed a Debian Linux operating system from an .iso file downloaded from hello [Debian website](https://www.debian.org/distrib/) tooa virtual hard disk.</span></span> <span data-ttu-id="df2dc-106">Существуют несколько средства toocreate VHD-файлы; Hyper-V — только один из примеров.</span><span class="sxs-lookup"><span data-stu-id="df2dc-106">Multiple tools exist toocreate .vhd files; Hyper-V is only one example.</span></span> <span data-ttu-id="df2dc-107">Инструкции с помощью Hyper-V см. в разделе [Установка hello роль Hyper-V и настройка виртуальной машины](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="df2dc-107">For instructions using Hyper-V, see [Install hello Hyper-V Role and Configure a Virtual Machine](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

## <a name="installation-notes"></a><span data-ttu-id="df2dc-108">Замечания по установке</span><span class="sxs-lookup"><span data-stu-id="df2dc-108">Installation notes</span></span>
* <span data-ttu-id="df2dc-109">Дополнительные сведения о подготовке Linux для Azure см. в разделе [Общие замечания по установке Linux](create-upload-generic.md#general-linux-installation-notes).</span><span class="sxs-lookup"><span data-stu-id="df2dc-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="df2dc-110">Hello более новый формат VHDX не поддерживается в Azure.</span><span class="sxs-lookup"><span data-stu-id="df2dc-110">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="df2dc-111">Вы можете преобразовать формат tooVHD hello диска, с помощью диспетчера Hyper-V или hello **convert-vhd** командлета.</span><span class="sxs-lookup"><span data-stu-id="df2dc-111">You can convert hello disk tooVHD format using Hyper-V Manager or hello **convert-vhd** cmdlet.</span></span>
* <span data-ttu-id="df2dc-112">При установке системы Linux hello рекомендуется использовать стандартный секции, а не LVM (часто hello по умолчанию для многих установок).</span><span class="sxs-lookup"><span data-stu-id="df2dc-112">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="df2dc-113">Это позволит избежать конфликтов имен LVM с клонированные виртуальные машины, особенно в том случае, если на диске ОС никогда не требуется tooanother toobe присоединенного виртуальной Машины для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="df2dc-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="df2dc-114">Для дисков данных можно использовать [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) или [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="df2dc-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="df2dc-115">Не настраивайте переключения секции на диске ОС hello.</span><span class="sxs-lookup"><span data-stu-id="df2dc-115">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="df2dc-116">агент Azure Linux Hello может быть настроенный toocreate файл подкачки на диске временного ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="df2dc-116">hello Azure Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span> <span data-ttu-id="df2dc-117">Дополнительные сведения об этом можно найти в hello описанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="df2dc-117">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="df2dc-118">Все виртуальные жесткие диски hello должны иметь размеры, кратные 1 МБ.</span><span class="sxs-lookup"><span data-stu-id="df2dc-118">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="use-azure-manage-toocreate-debian-vhds"></a><span data-ttu-id="df2dc-119">Используйте Управление Azure toocreate Debian виртуальных жестких дисков</span><span class="sxs-lookup"><span data-stu-id="df2dc-119">Use Azure-Manage toocreate Debian VHDs</span></span>
<span data-ttu-id="df2dc-120">Существуют средства для создания Debian виртуальных жестких дисков для Azure, такие как hello [azure — управление](https://github.com/credativ/azure-manage) сценариев из [credativ](http://www.credativ.com/).</span><span class="sxs-lookup"><span data-stu-id="df2dc-120">There are tools available for generating Debian VHDs for Azure, such as hello [azure-manage](https://github.com/credativ/azure-manage) scripts from [credativ](http://www.credativ.com/).</span></span> <span data-ttu-id="df2dc-121">Это рекомендованный подход и создании образа с нуля hello.</span><span class="sxs-lookup"><span data-stu-id="df2dc-121">This is hello recommended approach versus creating an image from scratch.</span></span> <span data-ttu-id="df2dc-122">Например toocreate Debian 8 VHD запустите следующие команды, управлять azure toodownload hello (и зависимостях) и выполните сценарий azure_build_image hello:</span><span class="sxs-lookup"><span data-stu-id="df2dc-122">For example, toocreate a Debian 8 VHD run hello following commands toodownload azure-manage (and dependencies) and run hello azure_build_image script:</span></span>

    # sudo apt-get update
    # sudo apt-get install git qemu-utils mbr kpartx debootstrap

    # sudo apt-get install python3-pip python3-dateutil python3-cryptography
    # sudo pip3 install azure-storage azure-servicemanagement-legacy azure-common pytest pyyaml
    # git clone https://github.com/credativ/azure-manage.git
    # cd azure-manage
    # sudo pip3 install .

    # sudo azure_build_image --option release=jessie --option image_size_gb=30 --option image_prefix=debian-jessie-azure section


## <a name="manually-prepare-a-debian-vhd"></a><span data-ttu-id="df2dc-123">Подготовка виртуального жесткого диска Debian вручную</span><span class="sxs-lookup"><span data-stu-id="df2dc-123">Manually prepare a Debian VHD</span></span>
1. <span data-ttu-id="df2dc-124">В диспетчере Hyper-V выберите виртуальную машину hello.</span><span class="sxs-lookup"><span data-stu-id="df2dc-124">In Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="df2dc-125">Нажмите кнопку **Connect** tooopen окно консоли для виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="df2dc-125">Click **Connect** tooopen a console window for hello virtual machine.</span></span>
3. <span data-ttu-id="df2dc-126">Закомментируйте строку hello для **deb cdrom** в `/etc/apt/source.list` Если вы настроили hello виртуальной Машины к ISO-файла.</span><span class="sxs-lookup"><span data-stu-id="df2dc-126">Comment out hello line for **deb cdrom** in `/etc/apt/source.list` if you set up hello VM against an ISO file.</span></span>
4. <span data-ttu-id="df2dc-127">Изменить hello `/etc/default/grub` файл и измените hello **GRUB_CMDLINE_LINUX** параметр следующим образом: tooinclude дополнительных системных параметров для Azure.</span><span class="sxs-lookup"><span data-stu-id="df2dc-127">Edit hello `/etc/default/grub` file and modify hello **GRUB_CMDLINE_LINUX** parameter as follows tooinclude additional kernel parameters for Azure.</span></span>
   
        GRUB_CMDLINE_LINUX="console=tty0 console=ttyS0,115200 earlyprintk=ttyS0,115200 rootdelay=30"
5. <span data-ttu-id="df2dc-128">Перестроение hello grub и выполните:</span><span class="sxs-lookup"><span data-stu-id="df2dc-128">Rebuild hello grub and run:</span></span>
   
        # sudo update-grub
6. <span data-ttu-id="df2dc-129">Добавление элемента Debian Azure репозиториев too/etc/apt/sources.list для Debian 7 или 8:</span><span class="sxs-lookup"><span data-stu-id="df2dc-129">Add Debian's Azure repositories too/etc/apt/sources.list for either Debian 7 or 8:</span></span>
   
    <span data-ttu-id="df2dc-130">**Debian 7.x "Wheezy"**</span><span class="sxs-lookup"><span data-stu-id="df2dc-130">**Debian 7.x "Wheezy"**</span></span>
   
        deb http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb-src http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure wheezy main
        deb-src http://debian-archive.trafficmanager.net/debian-azure wheezy main

    <span data-ttu-id="df2dc-131">**Debian 8.x "Jessie"**</span><span class="sxs-lookup"><span data-stu-id="df2dc-131">**Debian 8.x "Jessie"**</span></span>

        deb http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb-src http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure jessie main
        deb-src http://debian-archive.trafficmanager.net/debian-azure jessie main


1. <span data-ttu-id="df2dc-132">Установите агент Azure Linux hello:</span><span class="sxs-lookup"><span data-stu-id="df2dc-132">Install hello Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install waagent
2. <span data-ttu-id="df2dc-133">Debian 7 — ядра на основе 3.16 необходимые toorun hello из репозитория wheezy backports hello.</span><span class="sxs-lookup"><span data-stu-id="df2dc-133">For Debian 7, it is required toorun hello 3.16-based kernel from hello wheezy-backports repository.</span></span> <span data-ttu-id="df2dc-134">Сначала создайте файл с именем /etc/apt/preferences.d/linux.pref с hello после содержимого:</span><span class="sxs-lookup"><span data-stu-id="df2dc-134">First create a file called /etc/apt/preferences.d/linux.pref with hello following contents:</span></span>
   
        Package: linux-image-amd64 initramfs-tools
        Pin: release n=wheezy-backports
        Pin-Priority: 500
   
    <span data-ttu-id="df2dc-135">Затем запустите «sudo apt get установить linux, изображения, amd64» новое ядро hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="df2dc-135">Then run "sudo apt-get install linux-image-amd64" tooinstall hello new kernel.</span></span>
3. <span data-ttu-id="df2dc-136">Отзыв виртуальной машины hello и подготовить ее для подготовки в Azure и запустить:</span><span class="sxs-lookup"><span data-stu-id="df2dc-136">Deprovision hello virtual machine and prepare it for provisioning on Azure and run:</span></span>
   
        # sudo waagent –force -deprovision
        # export HISTSIZE=0
        # logout
4. <span data-ttu-id="df2dc-137">В диспетчере Hyper-V выберите **Действие** -> Завершение работы.</span><span class="sxs-lookup"><span data-stu-id="df2dc-137">Click **Action** -> Shut Down in Hyper-V Manager.</span></span> <span data-ttu-id="df2dc-138">ДИСК Linux имеет теперь готовы toobe отправлен tooAzure.</span><span class="sxs-lookup"><span data-stu-id="df2dc-138">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="df2dc-139">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="df2dc-139">Next steps</span></span>
<span data-ttu-id="df2dc-140">Вы являетесь теперь готовы toouse Debian виртуальный жесткий диск toocreate новых виртуальных машин в Azure.</span><span class="sxs-lookup"><span data-stu-id="df2dc-140">You're now ready toouse your Debian virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="df2dc-141">Если это первый раз, что идет Отправка tooAzure файл .vhd hello hello см. шаги 2 и 3 в [Создание и передача виртуального жесткого диска, который содержит операционную систему Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="df2dc-141">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

