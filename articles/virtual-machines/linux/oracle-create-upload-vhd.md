---
title: "aaaCreate и отправка виртуального жесткого диска Oracle Linux | Документы Microsoft"
description: "Узнайте toocreate и отправить в Azure виртуального жесткого диска (VHD), содержащий операционную систему, Oracle Linux."
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
ms.openlocfilehash: be9cf284d7f5e7122a106506a343e53e9f1ac56e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-an-oracle-linux-virtual-machine-for-azure"></a>Подготовка виртуальной машины Oracle Linux для Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a>Предварительные требования
В этой статье предполагается, что вы уже установили Oracle Linux операционной системы tooa виртуального жесткого диска. Существуют несколько средства toocreate VHD-файлы, например решение виртуализации, таких как Hyper-V. Инструкции см. в разделе [Установка hello роль Hyper-V и настройка виртуальной машины](http://technet.microsoft.com/library/hh846766.aspx).

### <a name="oracle-linux-installation-notes"></a>Замечания по установке Oracle Linux
* Дополнительные сведения о подготовке Linux для Azure см. в разделе [Общие замечания по установке Linux](create-upload-generic.md#general-linux-installation-notes).
* В Hyper-V и Azure поддерживаются совместимое ядро Oracle Red Hat и его UEK3 (Unbreakable Enterprise Kernel). Для получения наилучших результатов следует убедиться, что tooupdate toohello последние ядра при подготовке вашего виртуального жесткого диска Oracle Linux.
* UEK2 Oracle не поддерживается в Hyper-V и Azure содержит hello необходимые драйверы.
* Hello формат VHDX не поддерживается только в Azure, **фиксированный VHD**.  Можно преобразовать формат tooVHD hello диска, с помощью диспетчера Hyper-V или hello командлет convert-vhd.
* При установке системы Linux hello рекомендуется использовать стандартный секции, а не LVM (часто hello по умолчанию для многих установок). Это позволит избежать конфликтов имен LVM с клонированные виртуальные машины, особенно в том случае, если на диске ОС никогда не требуется tooanother toobe присоединенного виртуальной Машины для устранения неполадок. Для дисков данных можно использовать [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) или [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Для больших размеров виртуальной Машины из-за ошибки tooa в версии ядра Linux ниже 2.6.37 NUMA не поддерживается. Эту проблему в основном влияет на распределения с использованием hello вышестоящего Red Hat 2.6.32 ядра. Ручная установка агента Azure Linux hello (waagent) будет автоматически отключена NUMA в конфигурации GRUB hello для ядра Linux hello. Дополнительные сведения об этом можно найти в hello описанные ниже действия.
* Не настраивайте переключения секции на диске ОС hello. агент Linux Hello может быть настроенный toocreate файл подкачки на диске временного ресурса hello.  Дополнительные сведения об этом можно найти в hello описанные ниже действия.
* Все виртуальные жесткие диски hello должны иметь размеры, кратные 1 МБ.
* Убедитесь в том, что hello `Addons` репозитория включена. Измените файл hello `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) или `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux) и измените строку hello `enabled=0` слишком`enabled=1` под **[ol6_addons]** или **[ol7_addons]** в этом файл.

## <a name="oracle-linux-64"></a>Oracle Linux 6.4+
Необходимо выполнить определенную конфигурацию действия в операционной системе hello для hello toorun виртуальной машины в Azure.

1. Hello центральной панели диспетчера Hyper-V выберите виртуальную машину hello.
2. Нажмите кнопку **Connect** окна hello tooopen для hello виртуальной машины.
3. Удалите NetworkManager, выполнив следующую команду hello.
   
        # sudo rpm -e --nodeps NetworkManager
   
    **Примечание:** Если hello пакет не установлен, эта команда завершится ошибкой с сообщением об ошибке. Это ожидаемое поведение.
4. Создайте файл с именем **сети** в hello `/etc/sysconfig/` каталог, содержащий hello следующий текст:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
5. Создайте файл с именем **ifcfg eth0** в hello `/etc/sysconfig/network-scripts/` каталог, содержащий hello следующий текст:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
6. Измените tooavoid правила udev создания статические правила для hello интерфейсы Ethernet. Эти правила приводят к появлению проблем при клонировании виртуальной машины в Microsoft Azure или Hyper-V:
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
7. Убедитесь, что hello сети служба будет запущена во время загрузки, выполнив следующую команду hello.
   
        # chkconfig network on
8. Установите python pyasn1, выполнив следующую команду hello:
   
        # sudo yum install python-pyasn1
9. Измените строку загрузки ядра hello в параметры grub tooinclude дополнительные ядра для Azure. toodo этом откройте «/ boot/grub/menu.lst» в текстовом редакторе, убедитесь, что ядра по умолчанию hello включает hello следующие параметры:
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300 numa=off
   
   Это также гарантирует все консоли сообщения отправляются toohello первый последовательный порт, который может помочь Azure поддержка с помощью отладки проблем. NUMA будут отключены из-за ошибки tooa совместимость ядра Oracle в Red Hat.
   
   В дополнение к этому toohello выше, рекомендуется слишком*удалить* hello следующие параметры:
   
        rhgb quiet crashkernel=auto
   
   Графический quiet начальной загрузки, не используются в облачной среде, где мы хотим, чтобы все журналы toobe hello, отправляемых toohello последовательного порта.
   
   Hello `crashkernel` возможность влево, при желании настроить, но следует заметить, что этот параметр приведет к уменьшению hello объем доступной памяти в hello виртуальная машина по 128 МБ или больше, которое может быть проблематично на hello меньшего размера виртуальной Машины.
10. Убедитесь, что hello SSH сервер установлен и настроен toostart во время загрузки.  Обычно это происходит по умолчанию hello.
11. Установите агент Azure Linux hello, выполнив следующую команду hello. Последняя версия Hello — 2.0.15.
    
        # sudo yum install WALinuxAgent
    
    Обратите внимание, что установка пакета WALinuxAgent hello приведет к удалению hello NetworkManager NetworkManager gnome пакеты, если они не были уже удалены как описано на шаге 2.
12. Не создавайте подкачки на диске ОС hello.
    
    Hello Azure Linux Agent может автоматически настроить подкачки с помощью hello локальный диск ресурсов, toohello подключенных виртуальных Машин после подготовки в Azure. Обратите внимание, что hello локальный диск ресурсов *временные* диск, а также может очищаться при отмененной подготовкой hello виртуальной Машины. После установки hello Azure Linux Agent (см. выше), измените соответствующим образом следующие параметры в /etc/waagent.conf hello:
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
13. Запустите следующие команды toodeprovision hello виртуальной машины hello и подготовить его для подготовки в Azure:
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
14. В диспетчере Hyper-V выберите **Действие -> Завершение работы**. ДИСК Linux имеет теперь готовы toobe отправлен tooAzure.

- - -
## <a name="oracle-linux-70"></a>Oracle Linux 7.0+
**Изменения в Oracle Linux 7**

Подготовка виртуальной машине Oracle Linux 7 для Azure — очень похожа tooOracle Linux 6, однако существует несколько важных различий, обратите внимание:

* Совместимость ядра Red Hat hello и UEK3 Oracle поддерживаются в Azure.  Рекомендуется использовать Hello UEK3 ядра.
* Hello NetworkManager пакета больше не конфликтует с агентом Azure Linux hello. Этот пакет устанавливается по умолчанию, и мы рекомендуем не удалять его.
* GRUB2 сейчас используется как hello загрузчика по умолчанию, поэтому hello процедуру для редактирования параметров ядра изменилась (см. ниже).
* XFS сейчас файловой системы по умолчанию hello. по-прежнему можно использовать Hello ext4 файловой системы, при необходимости.

**Этапы настройки**

1. В диспетчере Hyper-V выберите виртуальную машину hello.
2. Нажмите кнопку **Connect** tooopen окно консоли для виртуальной машины hello.
3. Создайте файл с именем **сети** в hello `/etc/sysconfig/` каталог, содержащий hello следующий текст:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
4. Создайте файл с именем **ifcfg eth0** в hello `/etc/sysconfig/network-scripts/` каталог, содержащий hello следующий текст:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
5. Измените tooavoid правила udev создания статические правила для hello интерфейсы Ethernet. Эти правила приводят к появлению проблем при клонировании виртуальной машины в Microsoft Azure или Hyper-V:
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
6. Убедитесь, что hello сети служба будет запущена во время загрузки, выполнив следующую команду hello.
   
        # sudo chkconfig network on
7. Установка пакета python pyasn1 hello, выполнив следующую команду hello:
   
        # sudo yum install python-pyasn1
8. Выполнения hello следующую команду текущих метаданных yum tooclear hello и установке обновлений:
   
        # sudo yum clean all
        # sudo yum -y update
9. Измените строку загрузки ядра hello в параметры grub tooinclude дополнительные ядра для Azure. toodo этом откройте «/ и т. д, по умолчанию или grub» в текстовом редакторе и измените hello `GRUB_CMDLINE_LINUX` параметра, например:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Это также гарантирует все консоли сообщения отправляются toohello первый последовательный порт, который может помочь Azure поддержка с помощью отладки проблем. Он также отключает новые соглашения об именах hello OEL 7 для сетевых адаптеров. В дополнение к этому toohello выше, рекомендуется слишком*удалить* hello следующие параметры:
   
       rhgb quiet crashkernel=auto
   
   Графический quiet начальной загрузки, не используются в облачной среде, где мы хотим, чтобы все журналы toobe hello, отправляемых toohello последовательного порта.
   
   Hello `crashkernel` возможность влево, при желании настроить, но следует заметить, что этот параметр приведет к уменьшению hello объем доступной памяти в hello виртуальная машина по 128 МБ или больше, которое может быть проблематично на hello меньшего размера виртуальной Машины.
10. После завершения редактирования «/ и т. д, по умолчанию или grub» каждого выше, запустите hello, следующая команда toorebuild hello grub конфигурация:
    
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg
11. Убедитесь, что hello SSH сервер установлен и настроен toostart во время загрузки.  Обычно это происходит по умолчанию hello.
12. Установите агент Azure Linux hello, выполнив hello следующую команду:
    
        # sudo yum install WALinuxAgent
        # sudo systemctl enable waagent
13. Не создавайте подкачки на диске ОС hello.
    
    Hello Azure Linux Agent может автоматически настроить подкачки с помощью hello локальный диск ресурсов, toohello подключенных виртуальных Машин после подготовки в Azure. Обратите внимание, что hello локальный диск ресурсов *временные* диск, а также может очищаться при отмененной подготовкой hello виртуальной Машины. После установки hello Azure Linux Agent (см. предыдущий шаг hello), измените соответствующим образом следующие параметры в /etc/waagent.conf hello:
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
14. Запустите следующие команды toodeprovision hello виртуальной машины hello и подготовить его для подготовки в Azure:
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
15. В диспетчере Hyper-V выберите **Действие -> Завершение работы**. ДИСК Linux имеет теперь готовы toobe отправлен tooAzure.

## <a name="next-steps"></a>Дальнейшие действия
Вы являетесь теперь готовы toouse Oracle Linux .vhd toocreate новых виртуальных машин в Azure. Если это первый раз, что идет Отправка tooAzure файл .vhd hello hello см. шаги 2 и 3 в [Создание и передача виртуального жесткого диска, который содержит операционную систему Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

