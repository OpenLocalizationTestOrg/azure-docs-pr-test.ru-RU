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
# <a name="prepare-a-red-hat-based-virtual-machine-for-azure"></a>Подготовка виртуальной машины на основе Red Hat для Azure
В этой статье вы узнаете, как tooprepare Red Hat Enterprise Linux (RHEL) виртуальной машины для использования в Azure. 6.7 + и 7.1 +, являются Hello версии RHEL, описанных в этой статье. Hello низкоуровневые оболочки для подготовки, описанных в этой статье, Hyper-V, на основе ядра виртуальной машины (KVM) и VMware. Подробнее о требованиях к участникам в программе Red Hat Cloud Access см. на [веб-сайте Red Hat Cloud Access](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) и странице [запуска RHEL в Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).

## <a name="prepare-a-red-hat-based-virtual-machine-from-hyper-v-manager"></a>Подготовка виртуальной машины под управлением Red Hat в диспетчере Hyper-V

### <a name="prerequisites"></a>Предварительные требования
В этом разделе предполагается, что ISO-файл уже получен из веб-сайта hello Red Hat и установленных hello RHEL изображения tooa виртуального жесткого диска (VHD). Дополнительные сведения о том, как tooinstall диспетчера Hyper-V toouse образа операционной системы в разделе [Установка hello роль Hyper-V и настройка виртуальной машины](http://technet.microsoft.com/library/hh846766.aspx).

**Замечания по установке RHEL**

* Azure не поддерживает формат VHDX hello. В Azure поддерживается только формат фиксированного виртуального жесткого диска. Можно использовать формат tooVHD диска hello tooconvert диспетчера Hyper-V, или можно использовать командлет convert-vhd hello. Если вы используете VirtualBox, выберите **фиксированный размер** в отличие от toohello динамически назначаемых параметр при создании hello диска по умолчанию.
* В Azure поддерживаются только виртуальные машины поколения 1. Виртуальные машины поколения 1 можно преобразовать из формата файла виртуального жесткого диска toohello VHDX и динамически расширяемый tooa диск фиксированного размера. Вы не можете изменить поколение виртуальной машины. Дополнительные сведения см. в статье [Необходимо создать виртуальную машину поколения 1 или 2 в Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).
* Hello максимальный размер, допустимый для hello виртуального жесткого диска — 1023 ГБ.
* При установке операционной системы Linux hello, рекомендуется использовать стандартный секции, а не логические тома Manager (LVM), что часто является по умолчанию hello для многих установок. Данная методика позволит избежать конфликтов имен LVM с клоны виртуальных машин, особенно в том случае, если вы захотите tooattach операционной системы диска tooanother идентичную виртуальную машину для устранения неполадок. Для дисков данных можно использовать [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) или [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Требуется поддержка ядра для подключения файловых систем UDF. При первой загрузке в Azure, hello формате UDF носителя, который будет гостевой вложенного toohello передает подготовки hello toohello конфигурации виртуальной машины Linux. Hello Azure Linux Agent должен быть доступ toomount hello UDF файл системы tooread свою конфигурацию и подготовки виртуальной машины hello.
* Версии ядра Linux hello, или более поздних версиях 2.6.37 не поддерживают доступ к неоднородной памяти (NUMA) на узле Hyper-V с большие размеры виртуальных машин. Эту проблему в основном влияет на старых дистрибутивы использовать hello вышестоящих ядра Red Hat 2.6.32 и была исправлена в RHEL 6.6 (ядра 2.6.32 504). Системы, использующие пользовательские ядер, которые старше 2.6.37 или на основе RHEL ядер, возраст которых превышает 2.6.32-504 необходимо задать hello `numa=off` параметр загрузки hello ядра в командной строке grub.conf. Дополнительные сведения см. на странице о [проблемах гостевой машины Red Hat Enterprise Linux 6 на виртуальной машине Microsoft Hyper-V](https://access.redhat.com/solutions/436883).
* Не настраивайте переключения секции на диске операционной системы hello. Hello агент для Linux можно toocreate настроенный файл подкачки на диске временного ресурса hello.  Дополнительные сведения об этом можно найти в hello следующие шаги.
* Все VHD-диски должны иметь размер, кратный 1 МБ.

### <a name="prepare-a-rhel-6-virtual-machine-from-hyper-v-manager"></a>Подготовка виртуальной машины RHEL 6 в диспетчере Hyper-V

1. В диспетчере Hyper-V выберите виртуальную машину hello.

2. Нажмите кнопку **Connect** tooopen окно консоли для виртуальной машины hello.

3. В RHEL 6 NetworkManager могут помешать hello агента Azure Linux. Удаление этого пакета, выполнив следующую команду hello:
   
        # sudo rpm -e --nodeps NetworkManager

4. Создание или изменение hello `/etc/sysconfig/network` и добавьте следующий текст hello:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Создание или изменение hello `/etc/sysconfig/network-scripts/ifcfg-eth0` и добавьте следующий текст hello:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. Переместить (или удалить) hello udev правила tooavoid создания статические правила для интерфейса Ethernet hello. Эти правила приводят к появлению проблем при клонировании виртуальной машины в Microsoft Azure или Hyper-V:

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. Убедитесь, сетевая служба hello начнется во время загрузки, выполнив следующую команду hello:

        # sudo chkconfig network on

8. Зарегистрируйте подписку Red Hat tooenable hello установку пакетов из репозитория RHEL hello, выполнив следующую команду hello:

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

9. пакет WALinuxAgent Hello, `WALinuxAgent-<version>`, переданное toohello Red Hat дополнения репозитория. Включите hello дополнения репозиторий, выполнив следующую команду hello:

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

10. Измените строку загрузки ядра hello в параметры grub tooinclude дополнительные ядра для Azure. toodo этого изменения, откройте `/boot/grub/menu.lst` в текстовом редакторе, убедитесь, что ядра по умолчанию hello включает hello следующие параметры:
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    Это также позволит гарантировать, что все сообщения консоли отправляются toohello первый последовательный порт, который может помочь Azure поддержка с помощью отладки проблем.
    
    Кроме того рекомендуется удалить hello следующие параметры:
    
        rhgb quiet crashkernel=auto
    
    Графический quiet начальной загрузки, не используются в облачной среде, где мы хотим, чтобы все журналы toobe hello, отправляемых toohello последовательного порта.  Можно оставить hello `crashkernel` параметр настроен, при необходимости. Обратите внимание, что этот параметр уменьшает hello объем доступной памяти на виртуальной машине hello 128 МБ или больше. Это может оказаться проблемой для виртуальных машин небольшого размера.

    >[!Important]
    RHEL версии 6.5 и более ранних версиях необходимо также задать hello `numa=off` параметр ядра. См. посвященный Red Hat [раздел 436883](https://access.redhat.com/solutions/436883).

11. Убедитесь, этот сервер hello безопасного shell (SSH) установлен и настроен toostart во время загрузки, которой обычно является по умолчанию hello. Измените hello tooinclude /etc/ssh/sshd_config следующей строкой:

        ClientAliveInterval 180

12. Установите агент Azure Linux hello, выполнив hello следующую команду:

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

    Установка пакета WALinuxAgent hello удаляет hello NetworkManager и NetworkManager gnome пакеты, если они не были уже удалены в шаге 3.

13. Не создавайте подкачки на диске операционной системы hello.

    Hello Azure Linux Agent подкачки может автоматически настроить с помощью hello локальный диск ресурсов, которые toohello подключенных виртуальных машин после подготовки виртуальной машины hello в Azure. Обратите внимание, что hello локальный диск ресурсов является временной и, он может очищаться при отозваны hello виртуальной машины. После установки hello Azure Linux Agent в предыдущем шаге hello, измените соответствующим образом следующие параметры в /etc/waagent.conf hello.

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

14. Отменить регистрацию подписки hello (при необходимости), выполнив следующую команду hello:

        # sudo subscription-manager unregister

15. Запустите следующие команды toodeprovision hello виртуальной машины hello и подготовить его для подготовки в Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

16. В диспетчере Hyper-V выберите **Действие** > **Завершение работы**. ДИСК Linux имеет теперь готовы toobe отправлен tooAzure.


### <a name="prepare-a-rhel-7-virtual-machine-from-hyper-v-manager"></a>Подготовка виртуальной машины RHEL 7 в диспетчере Hyper-V

1. В диспетчере Hyper-V выберите виртуальную машину hello.

2. Нажмите кнопку **Connect** tooopen окно консоли для виртуальной машины hello.

3. Создание или изменение hello `/etc/sysconfig/network` и добавьте следующий текст hello:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. Создание или изменение hello `/etc/sysconfig/network-scripts/ifcfg-eth0` и добавьте следующий текст hello:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. Убедитесь, сетевая служба hello начнется во время загрузки, выполнив следующую команду hello:

        # sudo chkconfig network on

6. Зарегистрируйте подписку Red Hat tooenable hello установку пакетов из репозитория RHEL hello, выполнив следующую команду hello:

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. Измените строку загрузки ядра hello в параметры grub tooinclude дополнительные ядра для Azure. toodo этого изменения, откройте `/etc/default/grub` в текстовом редакторе и изменить hello `GRUB_CMDLINE_LINUX` параметра. Например:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Это также позволит гарантировать, что все сообщения консоли отправляются toohello первый последовательный порт, который может помочь Azure поддержка с помощью отладки проблем. Эта конфигурация также отключает новые соглашения об именах hello RHEL 7 для сетевых адаптеров. Кроме того рекомендуется удалить hello следующие параметры:
   
        rhgb quiet crashkernel=auto
   
    Графический quiet начальной загрузки, не используются в облачной среде, где мы хотим, чтобы все журналы toobe hello, отправляемых toohello последовательного порта. Можно оставить hello `crashkernel` параметр настроен, при необходимости. Обратите внимание, что этот параметр уменьшает hello объем доступной памяти на виртуальной машине hello 128 МБ или более, которой может быть проблематичным на меньшие размеры виртуальной машины.

8. После завершения редактирования `/etc/default/grub`, запустите hello следующие конфигурацию grub hello toorebuild команды:

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

9. Убедитесь, что hello SSH сервер установлен и настроен toostart во время загрузки, которой обычно является по умолчанию hello. Изменить `/etc/ssh/sshd_config` tooinclude hello, следующей строкой:

        ClientAliveInterval 180

10. пакет WALinuxAgent Hello, `WALinuxAgent-<version>`, переданное toohello Red Hat дополнения репозитория. Включите hello дополнения репозиторий, выполнив следующую команду hello:

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

11. Установите агент Azure Linux hello, выполнив hello следующую команду:

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

12. Не создавайте подкачки на диске операционной системы hello.

    Hello Azure Linux Agent подкачки может автоматически настроить с помощью hello локальный диск ресурсов, которые toohello подключенных виртуальных машин после подготовки виртуальной машины hello в Azure. Обратите внимание, что hello локальный диск ресурсов — временный диск может очищаться при отмененной подготовкой hello виртуальной машины. После установки hello Azure Linux Agent в предыдущем шаге hello, изменить следующие параметры в hello `/etc/waagent.conf` соответствующим образом:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. Если необходимо toounregister hello подписки, запустите hello следующую команду:

        # sudo subscription-manager unregister

14. Запустите следующие команды toodeprovision hello виртуальной машины hello и подготовить его для подготовки в Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. В диспетчере Hyper-V выберите **Действие** > **Завершение работы**. ДИСК Linux имеет теперь готовы toobe отправлен tooAzure.


## <a name="prepare-a-red-hat-based-virtual-machine-from-kvm"></a>Подготовка виртуальной машины под управлением Red Hat в KVM
### <a name="prepare-a-rhel-6-virtual-machine-from-kvm"></a>Подготовка виртуальной машины RHEL 6 в KVM

1. Загрузите с веб-сайта Red Hat hello изображение KVM hello RHEL 6.

2. Задайте пароль пользователя root.

    Создать зашифрованный пароль и скопировать hello выходные данные команды hello:

        # openssl passwd -1 changeme

    Установите корневой пароль с помощью Guestfish:
        
        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   Изменение hello второе поле hello привилегированного пользователя из «!» toohello зашифрованный пароль.

3. Создание виртуальной машины в KVM из образа qcow2 hello. Задайте тип диска hello слишком**qcow2**и задать модель hello виртуального сетевого интерфейса устройства слишком**virtio**. Затем запустите hello виртуальную машину и войдите в качестве корневого.

4. Создание или изменение hello `/etc/sysconfig/network` и добавьте следующий текст hello:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Создание или изменение hello `/etc/sysconfig/network-scripts/ifcfg-eth0` и добавьте следующий текст hello:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. Переместить (или удалить) hello udev правила tooavoid создания статические правила для интерфейса Ethernet hello. Эти правила приводят к появлению проблем при клонировании виртуальной машины в Azure или Hyper-V:

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. Убедитесь, сетевая служба hello начнется во время загрузки, выполнив следующую команду hello:

        # chkconfig network on

8. Зарегистрируйте подписку Red Hat tooenable hello установку пакетов из репозитория RHEL hello, выполнив следующую команду hello:

        # subscription-manager register --auto-attach --username=XXX --password=XXX

9. Измените строку загрузки ядра hello в параметры grub tooinclude дополнительные ядра для Azure. toodo этой конфигурации, откройте `/boot/grub/menu.lst` в текстовом редакторе, убедитесь, что ядра по умолчанию hello включает hello следующие параметры:
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    Это также позволит гарантировать, что все сообщения консоли отправляются toohello первый последовательный порт, который может помочь Azure поддержка с помощью отладки проблем.
    
    Кроме того рекомендуется удалить hello следующие параметры:
    
        rhgb quiet crashkernel=auto
    
    Графический quiet начальной загрузки, не используются в облачной среде, где мы хотим, чтобы все журналы toobe hello, отправляемых toohello последовательного порта. Можно оставить hello `crashkernel` параметр настроен, при необходимости. Обратите внимание, что этот параметр уменьшает hello объем доступной памяти на виртуальной машине hello 128 МБ или более, которой может быть проблематичным на меньшие размеры виртуальной машины.

    >[!Important]
    RHEL версии 6.5 и более ранних версиях необходимо также задать hello `numa=off` параметр ядра. См. посвященный Red Hat [раздел 436883](https://access.redhat.com/solutions/436883).

10. Добавьте tooinitramfs модули Hyper-V.  

    Изменить `/etc/dracut.conf`и добавьте следующие содержимое hello:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Повторно создайте initramfs:

        # dracut -f -v

11. Удаление cloud-init:

        # yum remove cloud-init

12. Убедитесь, что hello SSH сервер установлен и настроен toostart во время загрузки:

        # chkconfig sshd on

    Измените hello tooinclude /etc/ssh/sshd_config следующие строки:

        PasswordAuthentication yes
        ClientAliveInterval 180

13. пакет WALinuxAgent Hello, `WALinuxAgent-<version>`, переданное toohello Red Hat дополнения репозитория. Включите hello дополнения репозиторий, выполнив следующую команду hello:

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

14. Установите агент Azure Linux hello, выполнив hello следующую команду:

        # yum install WALinuxAgent

        # chkconfig waagent on

15. Hello Azure Linux Agent подкачки может автоматически настроить с помощью hello локальный диск ресурсов, которые toohello подключенных виртуальных машин после подготовки виртуальной машины hello в Azure. Обратите внимание, что hello локальный диск ресурсов — временный диск может очищаться при отмененной подготовкой hello виртуальной машины. После установки hello Azure Linux Agent в предыдущем шаге hello, изменить следующие параметры в hello **/etc/waagent.conf** соответствующим образом:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. Отменить регистрацию подписки hello (при необходимости), выполнив следующую команду hello:

        # subscription-manager unregister

17. Запустите следующие команды toodeprovision hello виртуальной машины hello и подготовить его для подготовки в Azure:

        # waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. Завершите работу виртуальной машины hello в KVM.

19. Преобразуйте формат виртуального жесткого диска toohello изображения qcow2 hello.

    Сначала преобразовать формат tooraw hello изображения:

        # qemu-img convert -f qcow2 -O raw rhel-6.8.qcow2 rhel-6.8.raw

    Убедитесь, что размер hello hello необработанные изображения выравнивается 1 МБ. В противном случае округлять hello размер tooalign с 1 МБ:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Преобразовать tooa hello неподготовленный диск фиксированного размера виртуального жесткого диска:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd


### <a name="prepare-a-rhel-7-virtual-machine-from-kvm"></a>Подготовка виртуальной машины RHEL 7 в KVM

1. Загрузите с веб-сайта Red Hat hello изображение KVM hello RHEL 7. В этой процедуре используется RHEL 7 в качестве примера hello.

2. Задайте пароль пользователя root.

    Создать зашифрованный пароль и скопировать hello выходные данные команды hello:

        # openssl passwd -1 changeme

    Установите корневой пароль с помощью Guestfish:

        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   Изменение hello второе поле привилегированного пользователя из «!» toohello зашифрованный пароль.

3. Создание виртуальной машины в KVM из образа qcow2 hello. Задайте тип диска hello слишком**qcow2**и задать модель hello виртуального сетевого интерфейса устройства слишком**virtio**. Затем запустите hello виртуальную машину и войдите в качестве корневого.

4. Создание или изменение hello `/etc/sysconfig/network` и добавьте следующий текст hello:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Создание или изменение hello `/etc/sysconfig/network-scripts/ifcfg-eth0` и добавьте следующий текст hello:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

6. Убедитесь, сетевая служба hello начнется во время загрузки, выполнив следующую команду hello:

        # chkconfig network on

7. Зарегистрируйте подписку Red Hat tooenable установку пакетов из репозитория RHEL hello, выполнив следующую команду hello:

        # subscription-manager register --auto-attach --username=XXX --password=XXX

8. Измените строку загрузки ядра hello в параметры grub tooinclude дополнительные ядра для Azure. toodo этой конфигурации, откройте `/etc/default/grub` в текстовом редакторе и изменить hello `GRUB_CMDLINE_LINUX` параметра. Например:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Эта команда также гарантирует, что все сообщения консоли отправляются toohello первый последовательный порт, который может помочь Azure поддержка с помощью отладки проблем. Hello команда также отключает новые соглашения об именах hello RHEL 7 для сетевых адаптеров. Кроме того рекомендуется удалить hello следующие параметры:
   
        rhgb quiet crashkernel=auto
   
    Графический quiet начальной загрузки, не используются в облачной среде, где мы хотим, чтобы все журналы toobe hello, отправляемых toohello последовательного порта. Можно оставить hello `crashkernel` параметр настроен, при необходимости. Обратите внимание, что этот параметр уменьшает hello объем доступной памяти на виртуальной машине hello 128 МБ или более, которой может быть проблематичным на меньшие размеры виртуальной машины.

9. После завершения редактирования `/etc/default/grub`, запустите hello следующие конфигурацию grub hello toorebuild команды:

        # grub2-mkconfig -o /boot/grub2/grub.cfg

10. Добавьте модули Hyper-V в initramfs.

    Измените файл `/etc/dracut.conf` , добавив в него следующее содержимое:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Повторно создайте initramfs:

        # dracut -f -v

11. Удаление cloud-init:

        # yum remove cloud-init

12. Убедитесь, что hello SSH сервер установлен и настроен toostart во время загрузки:

        # systemctl enable sshd

    Измените hello tooinclude /etc/ssh/sshd_config следующие строки:

        PasswordAuthentication yes
        ClientAliveInterval 180

13. пакет WALinuxAgent Hello, `WALinuxAgent-<version>`, переданное toohello Red Hat дополнения репозитория. Включите hello дополнения репозиторий, выполнив следующую команду hello:

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

14. Установите агент Azure Linux hello, выполнив hello следующую команду:

        # yum install WALinuxAgent

    Включите службу hello waagent:

        # systemctl enable waagent.service

15. Не создавайте подкачки на диске операционной системы hello.

    Hello Azure Linux Agent подкачки может автоматически настроить с помощью hello локальный диск ресурсов, которые toohello подключенных виртуальных машин после подготовки виртуальной машины hello в Azure. Обратите внимание, что hello локальный диск ресурсов — временный диск может очищаться при отмененной подготовкой hello виртуальной машины. После установки hello Azure Linux Agent в предыдущем шаге hello, изменить следующие параметры в hello `/etc/waagent.conf` соответствующим образом:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. Отменить регистрацию подписки hello (при необходимости), выполнив следующую команду hello:

        # subscription-manager unregister

17. Запустите следующие команды toodeprovision hello виртуальной машины hello и подготовить его для подготовки в Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. Завершите работу виртуальной машины hello в KVM.

19. Преобразуйте формат виртуального жесткого диска toohello изображения qcow2 hello.

    Сначала преобразовать формат tooraw hello изображения:

        # qemu-img convert -f qcow2 -O raw rhel-7.3.qcow2 rhel-7.3.raw

    Убедитесь, что размер hello hello необработанные изображения выравнивается 1 МБ. В противном случае округлять hello размер tooalign с 1 МБ:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Преобразовать tooa hello неподготовленный диск фиксированного размера виртуального жесткого диска:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-vmware"></a>Подготовка виртуальной машины под управлением Red Hat в VMware
### <a name="prerequisites"></a>Предварительные требования
В этом разделе предполагается, что вы уже установили виртуальную машину RHEL в VMWare. Дополнительные сведения о том, как tooinstall операционной системы в VMware, отображается [руководство по установке VMware гостевой операционной системы](http://partnerweb.vmware.com/GOSIG/home.html).

* При установке операционной системы Linux hello, рекомендуется использовать стандартный секции, а не LVM, что часто является по умолчанию hello для многих установок. Это позволит избежать конфликтов имен LVM с клонированной виртуальной машины, особенно в том случае, если диск операционной системы никогда не должен toobe присоединенного tooanother виртуальной машины для устранения неполадок. При желании на дисках с данными можно использовать LVM или RAID.
* Не настраивайте переключения секции на диске операционной системы hello. Вы можете настроить toocreate агент Linux hello в файл подкачки на диске временного ресурса hello. Дополнительные сведения об этом можно найти в hello, описанных ниже.
* При создании виртуального жесткого диска hello выбрать **виртуального диска хранилища в одном файле**.

### <a name="prepare-a-rhel-6-virtual-machine-from-vmware"></a>Подготовка виртуальной машины RHEL 6 в VMware
1. В RHEL 6 NetworkManager могут помешать hello агента Azure Linux. Удаление этого пакета, выполнив следующую команду hello:
   
        # sudo rpm -e --nodeps NetworkManager

2. Создайте файл с именем **сети** в hello/etc/sysconfig/каталог, содержащий hello следующий текст:

        NETWORKING=yes
        HOSTNAME=localhost.localdomain

3. Создание или изменение hello `/etc/sysconfig/network-scripts/ifcfg-eth0` и добавьте следующий текст hello:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

4. Переместить (или удалить) hello udev правила tooavoid создания статические правила для интерфейса Ethernet hello. Эти правила приводят к появлению проблем при клонировании виртуальной машины в Azure или Hyper-V:

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

5. Убедитесь, сетевая служба hello начнется во время загрузки, выполнив следующую команду hello:

        # sudo chkconfig network on

6. Зарегистрируйте подписку Red Hat tooenable hello установку пакетов из репозитория RHEL hello, выполнив следующую команду hello:

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. пакет WALinuxAgent Hello, `WALinuxAgent-<version>`, переданное toohello Red Hat дополнения репозитория. Включите hello дополнения репозиторий, выполнив следующую команду hello:

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

8. Измените строку загрузки ядра hello в параметры grub tooinclude дополнительные ядра для Azure. toodo, откройте `/etc/default/grub` в текстовом редакторе и изменить hello `GRUB_CMDLINE_LINUX` параметра. Например:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0"
   
   Это также позволит гарантировать, что все сообщения консоли отправляются toohello первый последовательный порт, который может помочь Azure поддержка с помощью отладки проблем. Кроме того рекомендуется удалить hello следующие параметры:
   
        rhgb quiet crashkernel=auto
   
    Графический quiet начальной загрузки, не используются в облачной среде, где мы хотим, чтобы все журналы toobe hello, отправляемых toohello последовательного порта. Можно оставить hello `crashkernel` параметр настроен, при необходимости. Обратите внимание, что этот параметр уменьшает hello объем доступной памяти на виртуальной машине hello 128 МБ или более, которой может быть проблематичным на меньшие размеры виртуальной машины.

9. Добавьте tooinitramfs модули Hyper-V.

    Изменить `/etc/dracut.conf`и добавьте следующие содержимое hello:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Повторно создайте initramfs:

        # dracut -f -v

10. Убедитесь, что hello SSH сервер установлен и настроен toostart во время загрузки, которой обычно является по умолчанию hello. Изменить `/etc/ssh/sshd_config` tooinclude hello, следующей строкой:

    ClientAliveInterval 180

11. Установите агент Azure Linux hello, выполнив hello следующую команду:

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

12. Не создавайте подкачки на диске операционной системы hello.

    Hello Azure Linux Agent подкачки может автоматически настроить с помощью hello локальный диск ресурсов, которые toohello подключенных виртуальных машин после подготовки виртуальной машины hello в Azure. Обратите внимание, что hello локальный диск ресурсов — временный диск может очищаться при отмененной подготовкой hello виртуальной машины. После установки hello Azure Linux Agent в предыдущем шаге hello, изменить следующие параметры в hello `/etc/waagent.conf` соответствующим образом:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. Отменить регистрацию подписки hello (при необходимости), выполнив следующую команду hello:

        # sudo subscription-manager unregister

14. Запустите следующие команды toodeprovision hello виртуальной машины hello и подготовить его для подготовки в Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. Завершите работу виртуальной машины hello и преобразуйте hello VMDK файл tooa VHD-файл.

    Сначала преобразовать формат tooraw hello изображения:

        # qemu-img convert -f vmdk -O raw rhel-6.8.vmdk rhel-6.8.raw

    Убедитесь, что размер hello hello необработанные изображения выравнивается 1 МБ. В противном случае округлять hello размер tooalign с 1 МБ:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Преобразовать tooa hello неподготовленный диск фиксированного размера виртуального жесткого диска:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd

### <a name="prepare-a-rhel-7-virtual-machine-from-vmware"></a>Подготовка виртуальной машины RHEL 7 в VMware
1. Создание или изменение hello `/etc/sysconfig/network` и добавьте следующий текст hello:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

2. Создание или изменение hello `/etc/sysconfig/network-scripts/ifcfg-eth0` и добавьте следующий текст hello:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

3. Убедитесь, сетевая служба hello начнется во время загрузки, выполнив следующую команду hello:

        # sudo chkconfig network on

4. Зарегистрируйте подписку Red Hat tooenable hello установку пакетов из репозитория RHEL hello, выполнив следующую команду hello:

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

5. Измените строку загрузки ядра hello в параметры grub tooinclude дополнительные ядра для Azure. toodo этого изменения, откройте `/etc/default/grub` в текстовом редакторе и изменить hello `GRUB_CMDLINE_LINUX` параметра. Например:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Такая конфигурация гарантирует, что все сообщения консоли отправляются toohello первый последовательный порт, который может помочь Azure поддержка с помощью отладки проблем. Он также отключает новые соглашения об именах hello RHEL 7 для сетевых адаптеров. Кроме того рекомендуется удалить hello следующие параметры:
   
        rhgb quiet crashkernel=auto
   
    Графический quiet начальной загрузки, не используются в облачной среде, где мы хотим, чтобы все журналы toobe hello, отправляемых toohello последовательного порта. Можно оставить hello `crashkernel` параметр настроен, при необходимости. Обратите внимание, что этот параметр уменьшает hello объем доступной памяти на виртуальной машине hello 128 МБ или более, которой может быть проблематичным на меньшие размеры виртуальной машины.

6. После завершения редактирования `/etc/default/grub`, запустите hello следующие конфигурацию grub hello toorebuild команды:

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

7. Добавьте tooinitramfs модули Hyper-V.

    Измените файл `/etc/dracut.conf`, добавив в него следующее содержимое:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    Повторно создайте initramfs:

        # dracut -f -v

8. Убедитесь, что hello SSH сервер установлен и настроен toostart во время загрузки. Этот параметр обычно является по умолчанию hello. Изменить `/etc/ssh/sshd_config` tooinclude hello, следующей строкой:

        ClientAliveInterval 180

9. пакет WALinuxAgent Hello, `WALinuxAgent-<version>`, переданное toohello Red Hat дополнения репозитория. Включите hello дополнения репозиторий, выполнив следующую команду hello:

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

10. Установите агент Azure Linux hello, выполнив hello следующую команду:

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

11. Не создавайте подкачки на диске операционной системы hello.

    Hello Azure Linux Agent подкачки может автоматически настроить с помощью hello локальный диск ресурсов, которые toohello подключенных виртуальных машин после подготовки виртуальной машины hello в Azure. Обратите внимание, что hello локальный диск ресурсов — временный диск может очищаться при отмененной подготовкой hello виртуальной машины. После установки hello Azure Linux Agent в предыдущем шаге hello, изменить следующие параметры в hello `/etc/waagent.conf` соответствующим образом:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

12. Если необходимо toounregister hello подписки, запустите hello следующую команду:

        # sudo subscription-manager unregister

13. Запустите следующие команды toodeprovision hello виртуальной машины hello и подготовить его для подготовки в Azure:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

14. Завершите работу виртуальной машины hello и преобразовать формат VHD toohello файл VMDK hello.

    Сначала преобразовать формат tooraw hello изображения:

        # qemu-img convert -f vmdk -O raw rhel-7.3.vmdk rhel-7.3.raw

    Убедитесь, что размер hello hello необработанные изображения выравнивается 1 МБ. В противном случае округлять hello размер tooalign с 1 МБ:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Преобразовать tooa hello неподготовленный диск фиксированного размера виртуального жесткого диска:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-an-iso-by-using-a-kickstart-file-automatically"></a>Подготовка виртуальной машины под управлением Red Hat из ISO-образа с помощью автоматического использования файла kickstart
### <a name="prepare-a-rhel-7-virtual-machine-from-a-kickstart-file"></a>Подготовка виртуальной машины RHEL 7 из файла kickstart

1.  Создайте файл пуска, включающий следующие содержимое hello и сохраните файл hello. Дополнительные сведения об установке пуска см. в разделе hello [руководство по установке пуска](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).

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

2. Поместите файл пуска hello, где hello установки системы к нему возможен доступ.

3. Создайте новую виртуальную машину в диспетчере Hyper-V. На hello **подключить виртуальный жесткий диск** выберите **подключить виртуальный жесткий диск позднее**и завершения приветствия мастера создания виртуальной машины.

4. Откройте параметры виртуальной машины hello:

    а.  Присоедините новую виртуальную машину toohello виртуального жесткого диска. Убедитесь, что tooselect **формат VHD** и **фиксированного размера**.

    b.  Присоедините hello установки ISO toohello DVD-дисковод.

    c.  Задать hello BIOS tooboot с компакт-диска.

5. Запустите виртуальную машину hello. После появления руководство по установке hello **вкладка** параметры загрузки tooconfigure hello.

6. Ввод `inst.ks=<hello location of hello kickstart file>` в конце hello hello варианты загрузки и нажмите клавишу **ввод**.

7. Дождитесь установки toofinish hello. После завершения, hello виртуальной машины будет завершена автоматически. ДИСК Linux имеет теперь готовы toobe отправлен tooAzure.

## <a name="known-issues"></a>Известные проблемы
### <a name="hello-hyper-v-driver-could-not-be-included-in-hello-initial-ram-disk-when-using-a-non-hyper-v-hypervisor"></a>драйвер Hello Hyper-V не будут включены в начальной Электронный диск hello, при использовании низкоуровневая оболочка не Hyper-V

В некоторых случаях Linux установщики могут не включать hello драйверы для Hyper-V в hello начальной Электронный диск (initrd или initramfs) Если Linux обнаружит, что он работает в среде Hyper-V.

При использовании tooprepare системы (то есть Virtualbox, Xen, т. д.) другой виртуализации образа Linux, может потребоваться tooensure initrd toorebuild, по крайней мере hello hv_vmbus и модули ядра hv_storvsc доступен на hello начальной Электронный диск. Это известная проблема по крайней мере в системах, основанных на вышестоящий Red Hat распространения hello.

tooresolve эту проблему, добавьте tooinitramfs модули Hyper-V и перестроить его:

Изменить `/etc/dracut.conf`и добавьте следующие содержимое hello:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

Повторно создайте initramfs:

        # dracut -f -v

Дополнительные сведения см. в разделе hello сведения [перестроение initramfs](https://access.redhat.com/solutions/1958).

## <a name="next-steps"></a>Дальнейшие действия
Вы являетесь теперь готовы toouse Red Hat Enterprise Linux виртуальный жесткий диск toocreate новых виртуальных машин в Azure. Если это первый раз, что идет Отправка tooAzure файл .vhd hello hello см. шаги 2 и 3 в [Создание и передача виртуального жесткого диска, который содержит операционную систему Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

Дополнительные сведения о hello низкоуровневых оболочках, которые являются сертифицированным toorun Red Hat Enterprise Linux, см. в разделе [веб-сайта hello Red Hat](https://access.redhat.com/certified-hypervisors).
