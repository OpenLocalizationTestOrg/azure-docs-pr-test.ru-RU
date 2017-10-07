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
# <a name="prepare-a-centos-based-virtual-machine-for-azure"></a>Подготовка виртуальной машины на основе CentOS для Azure
* [Подготовка виртуальной машины CentOS 6.x для Azure](#centos-6x)
* [Подготовка виртуальной машины CentOS 7.0+ для Azure](#centos-70)

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a>Предварительные требования
В этой статье предполагается, что вы уже установили CentOS (или аналогичные производных) Linux tooa виртуального жесткого диска операционной системы. Существуют несколько средства toocreate VHD-файлы, например решение виртуализации, таких как Hyper-V. Инструкции см. в разделе [Установка hello роль Hyper-V и настройка виртуальной машины](http://technet.microsoft.com/library/hh846766.aspx).

**Замечания по установке CentOS**

* Дополнительные сведения о подготовке Linux для Azure см. в разделе [Общие замечания по установке Linux](create-upload-generic.md#general-linux-installation-notes).
* Hello формат VHDX не поддерживается только в Azure, **фиксированный VHD**.  Можно преобразовать формат tooVHD hello диска, с помощью диспетчера Hyper-V или hello командлет convert-vhd. Если вы используете VirtualBox этого нужно выбрать **фиксированный размер** в отличие от toohello по умолчанию динамически назначаемых при создании диска hello.
* При установке системы Linux hello *рекомендуется* использовать стандартные секции, а не LVM (часто hello по умолчанию для многих установок). Это позволит избежать конфликтов имен LVM с клонированные виртуальные машины, особенно в том случае, если диска ОС, когда-либо должен tooanother toobe присоединенного идентичные виртуальной Машины для устранения неполадок. Для дисков данных можно использовать [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) или [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Требуется поддержка ядра для монтирования файловых систем UDF. При первой загрузке в Azure hello настройке подготовки передается через формате UDF носителей, присоединенных toohello гостевой toohello виртуальной Машины с Linux. агент Azure Linux Hello должно быть может toomount hello UDF файл системы tooread свою конфигурацию и подготовить hello виртуальной Машины.
* Версии ядра Linux ниже 2.6.37 не поддерживают NUMA в Hyper-V с виртуальными машинами большего размера. Эту проблему в основном влияет на старых распределения, с использованием hello вышестоящих ядра Red Hat 2.6.32 и была исправлена в RHEL 6.6 (ядра 2.6.32 504). Здравствуйте, систем под управлением старше 2.6.37 пользовательские ядер или на основе RHEL версии ядра более старые, чем 2.6.32-504 необходимо задать параметр загрузки `numa=off` командной строки в grub.conf ядра hello. Дополнительные сведения см. в статье базы знаний Red Hat [KB 436883](https://access.redhat.com/solutions/436883).
* Не настраивайте переключения секции на диске ОС hello. агент Linux Hello может быть настроенный toocreate файл подкачки на диске временного ресурса hello.  Дополнительные сведения об этом можно найти в hello описанные ниже действия.
* Все виртуальные жесткие диски hello должны иметь размеры, кратные 1 МБ.

## <a name="centos-6x"></a>CentOS 6.x

1. В диспетчере Hyper-V выберите виртуальную машину hello.

2. Нажмите кнопку **Connect** tooopen окно консоли для виртуальной машины hello.

3. CentOS 6 NetworkManager могут помешать hello агента Azure Linux. Удаление этого пакета, выполнив следующую команду hello:
   
        # sudo rpm -e --nodeps NetworkManager

4. Создание или изменение файла hello `/etc/sysconfig/network` и добавьте следующий текст hello:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Создание или изменение файла hello `/etc/sysconfig/network-scripts/ifcfg-eth0` и добавьте следующий текст hello:
   
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
   
        # sudo chkconfig network on

8. При желании toouse hello OpenLogic зеркала, размещенных в hello центрами обработки данных Azure, затем замените hello `/etc/yum.repos.d/CentOS-Base.repo` файл с hello следующих репозиториев.  Также будет добавлен hello **[openlogic]** репозитории, которая включает в себя дополнительные пакеты, такие как агент Azure Linux hello:

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
    Hello остальные разделы руководства предполагается используется по крайней мере hello `[openlogic]` репозитория, в которой будет используется tooinstall hello Azure Linux agent ниже.


9. Добавьте следующие строки too/etc/yum.conf hello:
    
        http_caching=packages

10. Выполните hello, следующая команда tooclear hello текущей yum метаданных и обновления hello системы hello последние пакеты:
    
        # yum clean all

    При создании изображения для более ранней версии CentOS рекомендуется tooupdate, все hello последние пакеты toohello:

        # sudo yum -y update

    После выполнения этой команды может потребоваться перезагрузка.

11. (Необязательно) Установите драйверы hello hello службы интеграции Linux (LIS).
   
    >[!IMPORTANT]
    шаг Hello — **необходимые** для CentOS 6,3 и более ранних и необязательным для более поздних версий.

        # sudo rpm -e hypervkvpd  ## (may return error if not installed, that's OK)
        # sudo yum install microsoft-hyper-v

    Кроме того, необходимо выполнить инструкции по ручной установке hello hello [страница загрузки LIS](https://go.microsoft.com/fwlink/?linkid=403033) tooinstall hello RPM на ВМ.
 
12. Установите агент Azure Linux hello и зависимости:
    
        # sudo yum install python-pyasn1 WALinuxAgent
    
    пакет WALinuxAgent Hello приведет к удалению hello NetworkManager и NetworkManager gnome пакеты, если они не были уже удалены как описано в шаге 3.


13. Измените строку загрузки ядра hello в параметры grub tooinclude дополнительные ядра для Azure. toodo, откройте `/boot/grub/menu.lst` в текстовом редакторе, убедитесь, что ядра по умолчанию hello включает hello следующие параметры:
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    Это также гарантирует все консоли сообщения отправляются toohello первый последовательный порт, который может помочь Azure поддержка с помощью отладки проблем.
    
    В дополнение к этому toohello выше, рекомендуется слишком*удалить* hello следующие параметры:
    
        rhgb quiet crashkernel=auto
    
    Графический quiet начальной загрузки, не используются в облачной среде, где мы хотим, чтобы все журналы toobe hello, отправляемых toohello последовательного порта.  Hello `crashkernel` возможность влево, при желании настроить, но следует заметить, что этот параметр приведет к уменьшению hello объем доступной памяти в hello виртуальная машина по 128 МБ или больше, которое может быть проблематично на hello меньшего размера виртуальной Машины.

    >[!Important]
    CentOS версии 6.5 и более ранних версиях необходимо также задать параметр ядра hello `numa=off`. См. посвященный Red Hat [раздел 436883](https://access.redhat.com/solutions/436883).

14. Убедитесь, что hello SSH сервер установлен и настроен toostart во время загрузки.  Обычно это происходит по умолчанию hello.

15. Не создавайте подкачки на диске ОС hello.
    
    Hello Azure Linux Agent может автоматически настроить подкачки с помощью hello локальный диск ресурсов, toohello подключенных виртуальных Машин после подготовки в Azure. Обратите внимание, что hello локальный диск ресурсов *временные* диск, а также может очищаться при отмененной подготовкой hello виртуальной Машины. После установки hello Azure Linux Agent (см. выше), измените следующие параметры в hello `/etc/waagent.conf` соответствующим образом:
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. Запустите следующие команды toodeprovision hello виртуальной машины hello и подготовить его для подготовки в Azure:
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

17. В диспетчере Hyper-V выберите **Действие -> Завершение работы**. ДИСК Linux имеет теперь готовы toobe отправлен tooAzure.


- - -
## <a name="centos-70"></a>CentOS 7.0+
**Изменения в CentOS 7 (и аналогичных производных версиях)**

Подготовка виртуальной машины CentOS 7 для Azure — очень похожа tooCentOS 6, однако существует несколько важных различий, обратите внимание:

* Hello NetworkManager пакета больше не конфликтует с агентом Azure Linux hello. Этот пакет устанавливается по умолчанию, и мы рекомендуем не удалять его.
* GRUB2 сейчас используется как hello загрузчика по умолчанию, поэтому hello процедуру для редактирования параметров ядра изменилась (см. ниже).
* XFS сейчас файловой системы по умолчанию hello. по-прежнему можно использовать Hello ext4 файловой системы, при необходимости.

**Этапы настройки**

1. В диспетчере Hyper-V выберите виртуальную машину hello.

2. Нажмите кнопку **Connect** tooopen окно консоли для виртуальной машины hello.

3. Создание или изменение файла hello `/etc/sysconfig/network` и добавьте следующий текст hello:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. Создание или изменение файла hello `/etc/sysconfig/network-scripts/ifcfg-eth0` и добавьте следующий текст hello:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. Измените tooavoid правила udev создания статические правила для hello интерфейсы Ethernet. Эти правила приводят к появлению проблем при клонировании виртуальной машины в Microsoft Azure или Hyper-V:
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

6. При желании toouse hello OpenLogic зеркала, размещенных в hello центрами обработки данных Azure, затем замените hello `/etc/yum.repos.d/CentOS-Base.repo` файл с hello следующих репозиториев.  Также будет добавлен hello **[openlogic]** репозитории, которая содержит пакеты для агента Azure Linux hello:
   
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
    Hello остальные разделы руководства предполагается используется по крайней мере hello `[openlogic]` репозитория, в которой будет используется tooinstall hello Azure Linux agent ниже.

7. Выполнения hello следующую команду текущих метаданных yum tooclear hello и установке обновлений:
   
        # sudo yum clean all

    При создании изображения для более ранней версии CentOS рекомендуется tooupdate, все hello последние пакеты toohello:

        # sudo yum -y update

    После выполнения этой команды может потребоваться перезагрузка.

8. Измените строку загрузки ядра hello в параметры grub tooinclude дополнительные ядра для Azure. toodo, откройте `/etc/default/grub` в текстовом редакторе и измените hello `GRUB_CMDLINE_LINUX` параметра, например:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Это также гарантирует все консоли сообщения отправляются toohello первый последовательный порт, который может помочь Azure поддержка с помощью отладки проблем. Он также отключает новые соглашения об именах hello CentOS 7 для сетевых адаптеров. В дополнение к этому toohello выше, рекомендуется слишком*удалить* hello следующие параметры:
   
        rhgb quiet crashkernel=auto
   
    Графический quiet начальной загрузки, не используются в облачной среде, где мы хотим, чтобы все журналы toobe hello, отправляемых toohello последовательного порта. Hello `crashkernel` возможность влево, при желании настроить, но следует заметить, что этот параметр приведет к уменьшению hello объем доступной памяти в hello виртуальная машина по 128 МБ или больше, которое может быть проблематично на hello меньшего размера виртуальной Машины.

9. После завершения редактирования `/etc/default/grub` каждого выше, запустите hello, следующая команда toorebuild hello grub конфигурация:
   
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

10. Если создание образа hello из **VMWare, VirtualBox или KVM:** драйверы hello Hyper-V убедитесь, что включены в hello initramfs:
   
   Измените файл `/etc/dracut.conf`, добавив в него следующее содержимое:
   
        add_drivers+=”hv_vmbus hv_netvsc hv_storvsc”
   
   Заново создать hello initramfs.
   
        # sudo dracut –f -v

11. Установите агент Azure Linux hello и зависимости:

        # sudo yum install python-pyasn1 WALinuxAgent
        # sudo systemctl enable waagent

12. Не создавайте подкачки на диске ОС hello.
   
   Hello Azure Linux Agent может автоматически настроить подкачки с помощью hello локальный диск ресурсов, toohello подключенных виртуальных Машин после подготовки в Azure. Обратите внимание, что hello локальный диск ресурсов *временные* диск, а также может очищаться при отмененной подготовкой hello виртуальной Машины. После установки hello Azure Linux Agent (см. выше), измените следующие параметры в hello `/etc/waagent.conf` соответствующим образом:
   
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

## <a name="next-steps"></a>Дальнейшие действия
Вы являетесь теперь готовы toouse CentOS Linux виртуальный жесткий диск toocreate новых виртуальных машин в Azure. Если это первый раз, что идет Отправка tooAzure файл .vhd hello hello см. шаги 2 и 3 в [Создание и передача виртуального жесткого диска, который содержит операционную систему Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

