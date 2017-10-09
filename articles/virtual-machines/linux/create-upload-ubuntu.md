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
# <a name="prepare-an-ubuntu-virtual-machine-for-azure"></a>Подготовка виртуальной машины Ubuntu для Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="official-ubuntu-cloud-images"></a>Официальные образы облаков Ubuntu
Теперь Ubuntu публикует официальные виртуальные жесткие диски Azure, загрузить которые можно по адресу: [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/). Если требуются специализированные изображения Ubuntu toobuild для Azure, вместо того чтобы использовать hello Ручная процедура под ним рекомендуемые toostart с этих известных работает виртуальных жестких дисков и при необходимости настроить. последние версии образа Hello всегда находятся в hello следующих элементов:

* Ubuntu 12.04/Precise: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)
* Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)
* Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)

## <a name="prerequisites"></a>Предварительные требования
В этой статье предполагается, что вы уже установили Ubuntu Linux операционной системы tooa виртуального жесткого диска. Существуют несколько средства toocreate VHD-файлы, например решение виртуализации, таких как Hyper-V. Инструкции см. в разделе [Установка hello роль Hyper-V и настройка виртуальной машины](http://technet.microsoft.com/library/hh846766.aspx).

**Замечания по установке Ubuntu**

* Дополнительные сведения о подготовке Linux для Azure см. в разделе [Общие замечания по установке Linux](create-upload-generic.md#general-linux-installation-notes).
* Hello формат VHDX не поддерживается только в Azure, **фиксированный VHD**.  Можно преобразовать формат tooVHD hello диска, с помощью диспетчера Hyper-V или hello командлет convert-vhd.
* При установке системы Linux hello рекомендуется использовать стандартный секции, а не LVM (часто hello по умолчанию для многих установок). Это позволит избежать конфликтов имен LVM с клонированные виртуальные машины, особенно в том случае, если на диске ОС никогда не требуется tooanother toobe присоединенного виртуальной Машины для устранения неполадок. Для дисков данных можно использовать [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) или [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Не настраивайте переключения секции на диске ОС hello. агент Linux Hello может быть настроенный toocreate файл подкачки на диске временного ресурса hello.  Дополнительные сведения об этом можно найти в hello описанные ниже действия.
* Все виртуальные жесткие диски hello должны иметь размеры, кратные 1 МБ.

## <a name="manual-steps"></a>Создание вручную
> [!NOTE]
> Прежде чем toocreate собственное изображение Ubuntu для Azure, возможно, следует с помощью hello предварительно построение и тестирование образов из [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) вместо него.
> 
> 

1. Hello центральной панели диспетчера Hyper-V выберите виртуальную машину hello.

2. Нажмите кнопку **Connect** окна hello tooopen для hello виртуальной машины.

3. Замените hello текущего репозитории в Azure репозиториев hello изображения toouse Ubuntu. Hello шаги будут немного отличаться в зависимости от версии Ubuntu hello.
   
    Прежде чем изменять `/etc/apt/sources.list`, это рекомендуемое toomake резервной копии:
   
        # sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

    Ubuntu 12,04:
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    Ubuntu 14.04:
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    Ubuntu 16.04:
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

4. Hello Ubuntu Azure изображения теперь подписаны hello *включения оборудования* ядра (HWE). Обновление ядра последнюю toohello операционной системы hello, выполнив следующие команды hello:

    Ubuntu 12,04:
   
        # sudo apt-get update
        # sudo apt-get install linux-image-generic-lts-trusty linux-cloud-tools-generic-lts-trusty
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot
   
    Ubuntu 14.04:
   
        # sudo apt-get update
        # sudo apt-get install linux-image-virtual-lts-vivid linux-lts-vivid-tools-common
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot

    Ubuntu 16.04:
   
        # sudo apt-get update
        # sudo apt-get install linux-generic-hwe-16.04 linux-cloud-tools-generic-hwe-16.04
        (recommended) sudo apt-get dist-upgrade

        # sudo reboot

    **См. также:**
    - [https://wiki.ubuntu.com/Kernel/LTSEnablementStack](https://wiki.ubuntu.com/Kernel/LTSEnablementStack)
    - [https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack](https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack)


5. Измените строку загрузки ядра hello Grub tooinclude дополнительных системных параметров для Azure. этом откройте toodo `/etc/default/grub` в текстовом редакторе, найдите hello переменную с именем `GRUB_CMDLINE_LINUX_DEFAULT` (или добавьте ее при необходимости) и изменить его hello tooinclude следующие параметры:
   
        GRUB_CMDLINE_LINUX_DEFAULT="console=tty1 console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300"

    Сохраните и закройте файл, а затем выполните команду `sudo update-grub`. Это позволит гарантировать, что все сообщения консоли отправляются toohello первый последовательный порт, который может помочь Azure технической поддержки с отладки проблем с.

6. Убедитесь, что hello SSH сервер установлен и настроен toostart во время загрузки.  Обычно это происходит по умолчанию hello.

7. Установите агент Azure Linux hello:
   
        # sudo apt-get update
        # sudo apt-get install walinuxagent

    >[!Note]
    Hello `walinuxagent` пакет может удалять hello `NetworkManager` и `NetworkManager-gnome` пакеты, если они установлены.

8. Запустите следующие команды toodeprovision hello виртуальной машины hello и подготовить его для подготовки в Azure:
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

9. В диспетчере Hyper-V выберите **Действие -> Завершение работы**. ДИСК Linux имеет теперь готовы toobe отправлен tooAzure.

## <a name="next-steps"></a>Дальнейшие действия
Вы являетесь теперь готовы toouse Ubuntu Linux виртуальный жесткий диск toocreate новых виртуальных машин в Azure. Если это первый раз, что идет Отправка tooAzure файл .vhd hello hello см. шаги 2 и 3 в [Создание и передача виртуального жесткого диска, который содержит операционную систему Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="references"></a>Ссылки
Ядро Ubuntu с расширенной поддержкой оборудования (HWE):

* [http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html](http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html)
* [http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html](http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html)

