---
title: "aaaCreate и отправка виртуального жесткого диска SUSE Linux в Azure"
description: "Узнайте toocreate и отправить в Azure виртуального жесткого диска (VHD), содержащий операционной системы SUSE Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 066d01a6-2a54-4718-bcd0-90fe7a5303a1
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: szark
ms.openlocfilehash: 9185c7e67279357f00db0f43e944e96c58f0dd60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-sles-or-opensuse-virtual-machine-for-azure"></a>Подготовка виртуальной машины SLES или openSUSE для Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a>Предварительные требования
В этой статье предполагается, что вы уже установили SUSE или openSUSE Linux tooa виртуального жесткого диска операционной системы. Существуют несколько средства toocreate VHD-файлы, например решение виртуализации, таких как Hyper-V. Инструкции см. в разделе [Установка hello роль Hyper-V и настройка виртуальной машины](http://technet.microsoft.com/library/hh846766.aspx).

### <a name="sles--opensuse-installation-notes"></a>Замечания по установке SLES и openSUSE
* Дополнительные сведения о подготовке Linux для Azure см. в разделе [Общие замечания по установке Linux](create-upload-generic.md#general-linux-installation-notes).
* Hello формат VHDX не поддерживается только в Azure, **фиксированный VHD**.  Можно преобразовать формат tooVHD hello диска, с помощью диспетчера Hyper-V или hello командлет convert-vhd.
* При установке системы Linux hello рекомендуется использовать стандартный секции, а не LVM (часто hello по умолчанию для многих установок). Это позволит избежать конфликтов имен LVM с клонированные виртуальные машины, особенно в том случае, если на диске ОС никогда не требуется tooanother toobe присоединенного виртуальной Машины для устранения неполадок. Для дисков данных можно использовать [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) или [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Не настраивайте переключения секции на диске ОС hello. агент Linux Hello может быть настроенный toocreate файл подкачки на диске временного ресурса hello.  Дополнительные сведения об этом можно найти в hello описанные ниже действия.
* Все виртуальные жесткие диски hello должны иметь размеры, кратные 1 МБ.

## <a name="use-suse-studio"></a>Использование SUSE Studio
[SUSE Studio](http://www.susestudio.com) можно с легкостью использовать для создания образов SLES и openSUSE для Azure и Hyper-V, а также для управления этими образами. Это рекомендованный подход для настройки свои собственные образы SLES и openSUSE hello.

Как альтернативный toobuilding собственного виртуального жесткого диска, SUSE также публикует изображения BYOS (переведите свои собственные подписки) для SLES на [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).

## <a name="prepare-suse-linux-enterprise-server-11-sp4"></a>Подготовка SUSE Linux Enterprise Server 11 с пакетом обновления 4 (SP4)
1. Hello центральной панели диспетчера Hyper-V выберите виртуальную машину hello.
2. Нажмите кнопку **Connect** окна hello tooopen для hello виртуальной машины.
3. Регистрация вашего tooallow системы SUSE Linux Enterprise его toodownload обновления и пакеты установки.
4. Обновите систему hello hello последние обновления системы:
   
        # sudo zypper update
5. Установите агент Azure Linux hello из репозитория SLES hello:
   
        # sudo zypper install WALinuxAgent
6. Проверьте Если запущена команда waagent задано слишком «on» в chkconfig и если нет, включить его для автоматического запуска:
   
        # sudo chkconfig waagent on
7. Убедитесь, что служба waagent работает. Если она не работает, запустите ее: 
   
        # sudo service waagent start
8. Измените строку загрузки ядра hello в параметры grub tooinclude дополнительные ядра для Azure. toodo этом откройте «/ boot/grub/menu.lst» в текстовом редакторе, убедитесь, что ядра по умолчанию hello включает hello следующие параметры:
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
   
    Это обеспечит все консоли сообщения отправляются toohello первый последовательный порт, который может помочь Azure поддержка с помощью отладки проблем.
9. Убедитесь, что /boot/grub/menu.lst и/etc/fstab оба диска hello ссылка, с помощью его идентификатора UUID (с uuid) вместо диска с Идентификатором hello (по идентификатору). 
   
    Получение UUID диска
   
        # ls /dev/disk/by-uuid/
   
    Если /dev/disk/by-id / — используется, обновления /boot/grub/menu.lst и/etc/fstab правильную uuid по значению hello
   
    Перед изменением
   
        root=/dev/disk/by-id/SCSI-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxxx-part1
   
    После изменения
   
        root=/dev/disk/by-uuid/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
10. Измените tooavoid правила udev создания статические правила для hello интерфейсы Ethernet. Эти правила приводят к появлению проблем при клонировании виртуальной машины в Microsoft Azure или Hyper-V:
    
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
11. Рекомендуется tooedit hello файл «/ и т. д/sysconfig/сети и dhcp» и измените hello `DHCLIENT_SET_HOSTNAME` toohello следующий параметр:
    
     DHCLIENT_SET_HOSTNAME="no"
12. В «/ etc/sudoers» закомментируйте или удалите следующие строки, если они существуют hello:
    
     По умолчанию targetpw # запрашивать пароль hello hello целевого пользователя, т. е. все ALL=(ALL) всех корневых # предупреждение! Используйте только вместе с Defaults targetpw!
13. Убедитесь, что hello SSH сервер установлен и настроен toostart во время загрузки.  Обычно это происходит по умолчанию hello.
14. Не создавайте подкачки на диске ОС hello.
    
    Hello Azure Linux Agent может автоматически настроить подкачки с помощью hello локальный диск ресурсов, toohello подключенных виртуальных Машин после подготовки в Azure. Обратите внимание, что hello локальный диск ресурсов *временные* диск, а также может очищаться при отмененной подготовкой hello виртуальной Машины. После установки hello Azure Linux Agent (см. выше), измените соответствующим образом следующие параметры в /etc/waagent.conf hello:
    
     ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048;# Примечание: задать этот toowhatever он нужен toobe.
15. Запустите следующие команды toodeprovision hello виртуальной машины hello и подготовить его для подготовки в Azure:
    
    # <a name="sudo-waagent--force--deprovision"></a>sudo waagent -force -deprovision
    # <a name="export-histsize0"></a>export HISTSIZE=0
    # <a name="logout"></a>logout
16. В диспетчере Hyper-V выберите **Действие -> Завершение работы**. ДИСК Linux имеет теперь готовы toobe отправлен tooAzure.

- - -
## <a name="prepare-opensuse-131"></a>Подготовка openSUSE 13.1+
1. Hello центральной панели диспетчера Hyper-V выберите виртуальную машину hello.
2. Нажмите кнопку **Connect** окна hello tooopen для hello виртуальной машины.
3. Оболочка hello, запустите команду hello "`zypper lr`". Если эта команда возвращает выходные данные примерно следующие, репозиториев hello настроены должным образом--каких-либо корректировок необходимы toohello (Обратите внимание, что номера версий могут различаться):
   
        # | Alias                 | Name                  | Enabled | Refresh
        --+-----------------------+-----------------------+---------+--------
        1 | Cloud:Tools_13.1      | Cloud:Tools_13.1      | Yes     | Yes
        2 | openSUSE_13.1_OSS     | openSUSE_13.1_OSS     | Yes     | Yes
        3 | openSUSE_13.1_Updates | openSUSE_13.1_Updates | Yes     | Yes
   
    Если hello команда возвращает «Нет репозиториев определенные...» выполните следующие команды tooadd hello эти репозиториев.
   
        # sudo zypper ar -f http://download.opensuse.org/repositories/Cloud:Tools/openSUSE_13.1 Cloud:Tools_13.1
        # sudo zypper ar -f http://download.opensuse.org/distribution/13.1/repo/oss openSUSE_13.1_OSS
        # sudo zypper ar -f http://download.opensuse.org/update/13.1 openSUSE_13.1_Updates
   
    Затем можно проверить, были добавлены репозиториев hello, выполнив команду hello "`zypper lr`" еще раз. В случае, если один из репозиториев существенные обновления hello не включена, включите его с помощью следующей команды:
   
        # sudo zypper mr -e [NUMBER OF REPOSITORY]
4. Обновление hello ядра toohello последней доступной версии:
   
        # sudo zypper up kernel-default
   
    Или системы hello tooupdate все последние обновления системы hello:
   
        # sudo zypper update
5. Установите агент Azure Linux hello.
   
   # <a name="sudo-zypper-install-walinuxagent"></a>sudo zypper install WALinuxAgent
6. Измените строку загрузки ядра hello в параметры grub tooinclude дополнительные ядра для Azure. toodo, откройте «/ boot/grub/menu.lst» в текстовом редакторе, убедитесь, что ядра по умолчанию hello включает hello следующие параметры:
   
     console=ttyS0 earlyprintk=ttyS0 rootdelay=300
   
   Это обеспечит все консоли сообщения отправляются toohello первый последовательный порт, который может помочь Azure поддержка с помощью отладки проблем. Кроме того удалите hello следующие параметры из строки загрузки ядра hello, если они существуют.
   
     libata.atapi_enabled=0 reserve=0x1f0,0x8
7. Рекомендуется tooedit hello файл «/ и т. д/sysconfig/сети и dhcp» и измените hello `DHCLIENT_SET_HOSTNAME` toohello следующий параметр:
   
     DHCLIENT_SET_HOSTNAME="no"
8. **Важно:** в «/ etc/sudoers», закомментируйте или удалите следующие строки, если они существуют hello:
   
     По умолчанию targetpw # запрашивать пароль hello hello целевого пользователя, т. е. все ALL=(ALL) всех корневых # предупреждение! Используйте только вместе с Defaults targetpw!
9. Убедитесь, что hello SSH сервер установлен и настроен toostart во время загрузки.  Обычно это происходит по умолчанию hello.
10. Не создавайте подкачки на диске ОС hello.
    
    Hello Azure Linux Agent может автоматически настроить подкачки с помощью hello локальный диск ресурсов, toohello подключенных виртуальных Машин после подготовки в Azure. Обратите внимание, что hello локальный диск ресурсов *временные* диск, а также может очищаться при отмененной подготовкой hello виртуальной Машины. После установки hello Azure Linux Agent (см. выше), измените соответствующим образом следующие параметры в /etc/waagent.conf hello:
    
     ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048;# Примечание: задать этот toowhatever он нужен toobe.
11. Запустите следующие команды toodeprovision hello виртуальной машины hello и подготовить его для подготовки в Azure:
    
    # <a name="sudo-waagent--force--deprovision"></a>sudo waagent -force -deprovision
    # <a name="export-histsize0"></a>export HISTSIZE=0
    # <a name="logout"></a>logout
12. Убедитесь, приветствия запускается агент Azure Linux при загрузке:
    
        # sudo systemctl enable waagent.service
13. В диспетчере Hyper-V выберите **Действие -> Завершение работы**. ДИСК Linux имеет теперь готовы toobe отправлен tooAzure.

## <a name="next-steps"></a>Дальнейшие действия
Вы являетесь теперь готовы toouse SUSE Linux виртуальный жесткий диск toocreate новых виртуальных машин в Azure. Если это первый раз, что идет Отправка tooAzure файл .vhd hello hello см. шаги 2 и 3 в [Создание и передача виртуального жесткого диска, который содержит операционную систему Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

