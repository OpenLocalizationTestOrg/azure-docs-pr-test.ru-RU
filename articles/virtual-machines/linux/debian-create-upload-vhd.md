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
# <a name="prepare-a-debian-vhd-for-azure"></a>Подготовка виртуального жесткого диска Debian для Azure
## <a name="prerequisites"></a>Предварительные требования
В этом разделе предполагается, что вы уже установили операционной системы Debian Linux ISO-файла, загруженные из hello [Debian веб-сайт](https://www.debian.org/distrib/) tooa виртуального жесткого диска. Существуют несколько средства toocreate VHD-файлы; Hyper-V — только один из примеров. Инструкции с помощью Hyper-V см. в разделе [Установка hello роль Hyper-V и настройка виртуальной машины](https://technet.microsoft.com/library/hh846766.aspx).

## <a name="installation-notes"></a>Замечания по установке
* Дополнительные сведения о подготовке Linux для Azure см. в разделе [Общие замечания по установке Linux](create-upload-generic.md#general-linux-installation-notes).
* Hello более новый формат VHDX не поддерживается в Azure. Вы можете преобразовать формат tooVHD hello диска, с помощью диспетчера Hyper-V или hello **convert-vhd** командлета.
* При установке системы Linux hello рекомендуется использовать стандартный секции, а не LVM (часто hello по умолчанию для многих установок). Это позволит избежать конфликтов имен LVM с клонированные виртуальные машины, особенно в том случае, если на диске ОС никогда не требуется tooanother toobe присоединенного виртуальной Машины для устранения неполадок. Для дисков данных можно использовать [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) или [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Не настраивайте переключения секции на диске ОС hello. агент Azure Linux Hello может быть настроенный toocreate файл подкачки на диске временного ресурса hello. Дополнительные сведения об этом можно найти в hello описанные ниже действия.
* Все виртуальные жесткие диски hello должны иметь размеры, кратные 1 МБ.

## <a name="use-azure-manage-toocreate-debian-vhds"></a>Используйте Управление Azure toocreate Debian виртуальных жестких дисков
Существуют средства для создания Debian виртуальных жестких дисков для Azure, такие как hello [azure — управление](https://github.com/credativ/azure-manage) сценариев из [credativ](http://www.credativ.com/). Это рекомендованный подход и создании образа с нуля hello. Например toocreate Debian 8 VHD запустите следующие команды, управлять azure toodownload hello (и зависимостях) и выполните сценарий azure_build_image hello:

    # sudo apt-get update
    # sudo apt-get install git qemu-utils mbr kpartx debootstrap

    # sudo apt-get install python3-pip python3-dateutil python3-cryptography
    # sudo pip3 install azure-storage azure-servicemanagement-legacy azure-common pytest pyyaml
    # git clone https://github.com/credativ/azure-manage.git
    # cd azure-manage
    # sudo pip3 install .

    # sudo azure_build_image --option release=jessie --option image_size_gb=30 --option image_prefix=debian-jessie-azure section


## <a name="manually-prepare-a-debian-vhd"></a>Подготовка виртуального жесткого диска Debian вручную
1. В диспетчере Hyper-V выберите виртуальную машину hello.
2. Нажмите кнопку **Connect** tooopen окно консоли для виртуальной машины hello.
3. Закомментируйте строку hello для **deb cdrom** в `/etc/apt/source.list` Если вы настроили hello виртуальной Машины к ISO-файла.
4. Изменить hello `/etc/default/grub` файл и измените hello **GRUB_CMDLINE_LINUX** параметр следующим образом: tooinclude дополнительных системных параметров для Azure.
   
        GRUB_CMDLINE_LINUX="console=tty0 console=ttyS0,115200 earlyprintk=ttyS0,115200 rootdelay=30"
5. Перестроение hello grub и выполните:
   
        # sudo update-grub
6. Добавление элемента Debian Azure репозиториев too/etc/apt/sources.list для Debian 7 или 8:
   
    **Debian 7.x "Wheezy"**
   
        deb http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb-src http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure wheezy main
        deb-src http://debian-archive.trafficmanager.net/debian-azure wheezy main

    **Debian 8.x "Jessie"**

        deb http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb-src http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure jessie main
        deb-src http://debian-archive.trafficmanager.net/debian-azure jessie main


1. Установите агент Azure Linux hello:
   
        # sudo apt-get update
        # sudo apt-get install waagent
2. Debian 7 — ядра на основе 3.16 необходимые toorun hello из репозитория wheezy backports hello. Сначала создайте файл с именем /etc/apt/preferences.d/linux.pref с hello после содержимого:
   
        Package: linux-image-amd64 initramfs-tools
        Pin: release n=wheezy-backports
        Pin-Priority: 500
   
    Затем запустите «sudo apt get установить linux, изображения, amd64» новое ядро hello tooinstall.
3. Отзыв виртуальной машины hello и подготовить ее для подготовки в Azure и запустить:
   
        # sudo waagent –force -deprovision
        # export HISTSIZE=0
        # logout
4. В диспетчере Hyper-V выберите **Действие** -> Завершение работы. ДИСК Linux имеет теперь готовы toobe отправлен tooAzure.

## <a name="next-steps"></a>Дальнейшие действия
Вы являетесь теперь готовы toouse Debian виртуальный жесткий диск toocreate новых виртуальных машин в Azure. Если это первый раз, что идет Отправка tooAzure файл .vhd hello hello см. шаги 2 и 3 в [Создание и передача виртуального жесткого диска, который содержит операционную систему Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

