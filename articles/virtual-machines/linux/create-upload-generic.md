---
title: "aaaCreate и передача виртуального жесткого диска Linux в Azure"
description: "Узнайте toocreate и отправить в Azure виртуального жесткого диска (VHD), содержащий операционную систему Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: d351396c-95a0-4092-b7bf-c6aae0bbd112
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 208e15c035edb5520fc29ba8e4e71c42b041864d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="information-for-non-endorsed-distributions"></a>Информация о нерекомендованных дистрибутивах
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Hello платформы Azure соглашения об уровне ОБСЛУЖИВАНИЯ применяется toovirtual компьютеров под управлением ОС Linux только в том случае, когда один hello объекта hello [одобренных распределения](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) используется. Все дистрибутивы Linux, которые предоставляются в hello Azure являются коллекции образов, одобренных распределения с требуемой конфигурацией hello.

* [Linux в Azure — рекомендованные дистрибутивы](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Поддержка образов Linux в Microsoft Azure](https://support.microsoft.com/kb/2941892)

Все распределения, работающих в Azure, потребуется toomeet количество необходимых компонентов toohave tooproperly вероятность того, работает на платформе hello.  В этой статье далеко не является исчерпывающим, как у каждого распределения отличаются; и вполне возможно, что даже если выполнены все hello критериям по-прежнему нужно toosignificantly настроить вашей tooensure системы Linux, где он выполняется должным образом на платформе hello.

Именно по этой причине мы рекомендуем по возможности начать работу с одним из [рекомендованных дистрибутивов Linux в Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) . Hello ниже статьях поможет как tooprepare hello различных одобренных дистрибутивы Linux, которые поддерживаются в Azure:

* **[Дистрибутивы на основе CentOS](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[SLES и OpenSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**

Hello оставшейся части этой статьи будет использован Общие рекомендации по запуску дистрибутива Linux в Azure.

## <a name="general-linux-installation-notes"></a>Общие замечания по установке Linux
* Hello формат VHDX не поддерживается только в Azure, **фиксированный VHD**.  Можно преобразовать формат tooVHD hello диска, с помощью диспетчера Hyper-V или hello командлет convert-vhd. Если вы используете VirtualBox этого нужно выбрать **фиксированный размер** в отличие от toohello по умолчанию динамически назначаемых при создании диска hello.
* Azure поддерживает только виртуальные машины поколения 1. Вы можете преобразовать поколение 1 виртуальная машина из формат файла виртуального жесткого диска toohello VHDX и динамически расширяемые tooa фиксированного размера диска. Но вы не можете изменить поколение виртуальной машины. Дополнительные сведения см. в статье о том, [как выбрать поколение для виртуальной машины в Hyper-V](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).
* Максимальный размер Hello разрешена для hello виртуального жесткого диска — 1023 ГБ.
* При установке системы Linux hello *рекомендуется* использовать стандартные секции, а не LVM (часто hello по умолчанию для многих установок). Это позволит избежать конфликтов имен LVM с клонированные виртуальные машины, особенно в том случае, если диска ОС, когда-либо должен tooanother toobe присоединенного идентичные виртуальной Машины для устранения неполадок. Для дисков данных можно использовать [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) или [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Требуется поддержка ядра для монтирования файловых систем UDF. При первой загрузке в Azure hello настройке подготовки передается через формате UDF носителей, присоединенных toohello гостевой toohello виртуальной Машины с Linux. агент Azure Linux Hello должно быть может toomount hello UDF файл системы tooread свою конфигурацию и подготовить hello виртуальной Машины.
* Версии ядра Linux ниже 2.6.37 не поддерживают NUMA в Hyper-V с виртуальными машинами большего размера. Эту проблему в основном влияет на старых распределения, с использованием hello вышестоящих ядра Red Hat 2.6.32 и была исправлена в RHEL 6.6 (ядра 2.6.32 504). Здравствуйте, систем под управлением старше 2.6.37 пользовательские ядер или на основе RHEL версии ядра более старые, чем 2.6.32-504 необходимо задать параметр загрузки `numa=off` командной строки в grub.conf ядра hello. Дополнительные сведения см. в статье базы знаний Red Hat [KB 436883](https://access.redhat.com/solutions/436883).
* Не настраивайте переключения секции на диске ОС hello. агент Linux Hello может быть настроенный toocreate файл подкачки на диске временного ресурса hello.  Дополнительные сведения об этом можно найти в hello описанные ниже действия.
* Все виртуальные жесткие диски hello должны иметь размеры, кратные 1 МБ.

### <a name="installing-kernel-modules-without-hyper-v"></a>Установка модулей ядра без Hyper-V
Azure работает на hello низкоуровневая оболочка Hyper-V, поэтому Linux требует установку определенных модулей ядра в порядке toorun в Azure. При наличии виртуальной Машины, в которой был создан за пределами Hyper-V hello Linux установщики могут не содержат hello драйверы для Hyper-V в начальной ramdisk hello (initrd или initramfs) если обнаружит, что он работает в среде Hyper-V. При использовании образа Linux tooprepare различных виртуализации системы (т. е. Virtualbox, KVM, т. д.), может потребоваться toorebuild hello initrd tooensure, по крайней мере hello `hv_vmbus` и `hv_storvsc` на начальной ramdisk hello доступны модули ядра.  Это известная проблема по крайней мере в системах на базе hello вышестоящего Red Hat распространения.

механизм Hello hello initrd или initramfs образа может зависеть от распространения hello. Обратитесь к документации на распределение или поддержка hello соответствующие процедуры.  Ниже приведен пример, как toorebuild hello initrd с помощью hello `mkinitrd` программы:

Во-первых резервное копирование существующего образа initrd hello:

    # cd /boot
    # sudo cp initrd-`uname -r`.img  initrd-`uname -r`.img.bak

Затем перестроить initrd hello с hello `hv_vmbus` и `hv_storvsc` модули ядра:

    # sudo mkinitrd --preload=hv_storvsc --preload=hv_vmbus -v -f initrd-`uname -r`.img `uname -r`


### <a name="resizing-vhds"></a>Изменение размера VHD
Образы виртуальных жестких ДИСКОВ в Azure должен иметь too1MB размер виртуальной памяти по краю.  Как правило, размер VHD, созданных с помощью Hyper-V, настроен правильно.  Если виртуальный жесткий ДИСК hello выровнено неправильно, может возникнуть ошибка сообщение аналогичные toohello следующие при попытке toocreate *изображения* из вашего виртуального жесткого диска:

    "hello VHD http://<mystorageaccount>.blob.core.windows.net/vhds/MyLinuxVM.vhd has an unsupported virtual size of 21475270656 bytes. hello size must be a whole number (in MBs).”

tooremedy Здравствуйте, это можно изменить размер виртуальной Машины с помощью консоли диспетчера Hyper-V hello или hello [Resize-VHD](http://technet.microsoft.com/library/hh848535.aspx) командлета Powershell.  Если вы не работает в среде Windows, то рекомендуемые toouse qemu img tooconvert (при необходимости) и hello изменения размера виртуального жесткого диска.

> [!NOTE]
> В команде qemu-img версии 2.2.1 и более поздних версиях есть ошибка, которая приводит к созданию неверного формата VHD. Hello проблема была устранена в QEMU 2.6. Рекомендуется toouse qemu-img 2.2.0 или нижней или too2.6 обновления или более поздней версии. Ссылки: https://bugs.launchpad.net/qemu/+bug/1490611.
> 
> 

1. Изменение размера виртуального жесткого диска, непосредственно с помощью средств, например "hello" `qemu-img` или `vbox-manage` может привести к невозможности загрузки виртуального жесткого диска.  Поэтому рекомендуется hello convert toofirst образ дисковыми tooa виртуального жесткого диска.  Если образ виртуальной Машины hello уже был создан как изображение НЕПОДГОТОВЛЕННЫЙ диск (hello по умолчанию некоторые низкоуровневые оболочки, такие как KVM) может пропустить этот шаг:
   
       # qemu-img convert -f vpc -O raw MyLinuxVM.vhd MyLinuxVM.raw

2. Вычислите размер tooensure образ диска hello, hello размер виртуальной памяти не выровненные too1MB обязательных hello.  Следующий сценарий оболочки bash Hello может помочь с данным.  Hello скрипт использует "`qemu-img info`" toodetermine hello виртуальный размер образа диска hello и вычисляет размер toohello hello далее 1 МБ:
   
       rawdisk="MyLinuxVM.raw"
       vhddisk="MyLinuxVM.vhd"
   
       MB=$((1024*1024))
       size=$(qemu-img info -f raw --output json "$rawdisk" | \
              gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')
   
       rounded_size=$((($size/$MB + 1)*$MB))
       echo "Rounded Size = $rounded_size"

3. Изменение размера hello неподготовленный диск с помощью $rounded_size, указанное на hello выше сценария:
   
       # qemu-img resize MyLinuxVM.raw $rounded_size

4. Преобразован задней tooa hello НЕПОДГОТОВЛЕННЫЙ диск фиксированного размера виртуального жесткого диска:
   
       # qemu-img convert -f raw -o subformat=fixed -O vpc MyLinuxVM.raw MyLinuxVM.vhd

   Или с версией qemu **2.6 +** включают hello `force_size` параметр:

       # qemu-img convert -f raw -o subformat=fixed,force_size -O vpc MyLinuxVM.raw MyLinuxVM.vhd

## <a name="linux-kernel-requirements"></a>Рекомендации по ядру Linux
Hello службы интеграции Linux (LIS) драйверы для Hyper-V и Azure предоставляются непосредственно toohello вышестоящего ядра Linux. Во многих дистрибутивах, которые включают последнюю версию ядра Linux (то есть 3.x), эти драйверы уже будут доступны, или же в ядре предоставляются их более ранние версии.  Эти драйверы постоянно обновляются hello вышестоящего ядра новых исправлений и возможностей, поэтому по возможности рекомендуется toorun [одобренных распространения](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) , будет включать эти исправления и обновления.

Если вы используете вариант Red Hat Enterprise Linux версии **6.0 6.3**, вам потребуется tooinstall hello последние версии драйверов LIS для Hyper-V. Hello драйверов можно найти [в этом месте](http://go.microsoft.com/fwlink/p/?LinkID=254263&clcid=0x409). Начиная с RHEL **6.4 +** (и производные) hello LIS драйверы входят уже ядра hello и без дополнительной установки пакетов являются необходимые toorun этих систем в Azure.

При необходимости пользовательский ядра, это рекомендуемое toouse более новая версия ядра (т. е. **3.8 +**). Для этих распределений или поставщиков, обслуживать собственные ядра некоторые усилия будут необходимые tooregularly backport hello LIS драйверы hello вышестоящего ядра tooyour пользовательские ядра.  Даже если вы уже используете относительно новые версии ядра, настоятельно рекомендуется отслеживать tookeep любого вышестоящих исправления в драйверы LIS hello и backport их при необходимости. расположение Hello исходные файлы драйверов LIS hello доступен в hello [программы ОБСЛУЖИВАНИЯ](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/MAINTAINERS) файл в дерево исходного кода hello Linux ядра:

    F:    arch/x86/include/asm/mshyperv.h
    F:    arch/x86/include/uapi/asm/hyperv.h
    F:    arch/x86/kernel/cpu/mshyperv.c
    F:    drivers/hid/hid-hyperv.c
    F:    drivers/hv/
    F:    drivers/input/serio/hyperv-keyboard.c
    F:    drivers/net/hyperv/
    F:    drivers/scsi/storvsc_drv.c
    F:    drivers/video/fbdev/hyperv_fb.c
    F:    include/linux/hyperv.h
    F:    tools/hv/

По крайней мере отсутствие hello hello после исправления известные проблемы toocause в Azure и поэтому они должны быть включены в hello ядра. Этот список ни в коем случае не является исчерпывающим и полным для всех дистрибутивов:

* [ata_piix: отложить драйверы toohello Hyper-V дисков по умолчанию](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/drivers/ata/ata_piix.c?id=cd006086fa5d91414d8ff9ff2b78fbb593878e3c)
* [storvsc: учетная запись для пакетов во время передачи в пути СБРОСА hello](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/drivers/scsi/storvsc_drv.c?id=5c1b10ab7f93d24f29b5630286e323d1c5802d5c)
* [storvsc: предотвращение использования WRITE_SAME;](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=3e8f4f4065901c8dfc51407e1984495e1748c090)
* [storvsc: отключение WRITE SAME для драйверов RAID и адаптеров виртуальных узлов;](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=54b2b50c20a61b51199bedb6e5d2f8ec2568fb43)
* [storvsc: исправление разыменования пустого указателя;](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=b12bb60d6c350b348a4e1460cd68f97ccae9822e)
* [storvsc: ошибки кольцевого буфера могут привести к заморозке операций ввода-вывода.](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=e86fb5e8ab95f10ec5f2e9430119d5d35020c951)
* [scsi_sysfs: защита от двойного выполнения __scsi_remove_device.](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/scsi_sysfs.c?id=be821fd8e62765de43cc4f0e2db363d0e30a7e9b)

## <a name="hello-azure-linux-agent"></a>Hello Azure Linux Agent
Hello [Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (waagent) требуется tooproperly подготовки виртуальной машины Linux в Azure. Получить последнюю версию hello, файл проблемы или отправлять запросы на включение внесенных изменений в hello [в репозитории GitHub агент Linux](https://github.com/Azure/WALinuxAgent).

* агент Linux Hello освобождается по лицензии Apache 2.0 hello. Большинство установок уже обеспечивают RPM или deb пакеты агента hello и поэтому в некоторых случаях это могут быть установлены и обновлены с минимальными усилиями.
* Hello Azure Linux Agent требует Python v2.6 +.
* Hello агент также требует наличия модуля python pyasn1 hello. В большинстве дистрибутивов он предоставляется в виде отдельно устанавливаемого пакета.
* В некоторых случаях hello Azure Linux Agent могут оказаться несовместимыми с NetworkManager. Многие пакеты RPM или Deb hello, предоставляемые распределения настройте NetworkManager как пакет waagent toohello конфликтов и таким образом удалит NetworkManager при установке пакета агента Linux hello.

## <a name="general-linux-system-requirements"></a>Общие системные требования для Linux

* Измените строку загрузки ядра hello в GRUB или GRUB2 hello tooinclude следующие параметры. Это также гарантирует все консоли сообщения отправляются toohello первый последовательный порт, который может помочь Azure поддержка с помощью отладки проблем:
  
        console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300
  
    Это также гарантирует все консоли сообщения отправляются toohello первый последовательный порт, который может помочь Azure поддержка с помощью отладки проблем.
  
    В дополнение к этому toohello выше, рекомендуется слишком*удалить* hello следующие параметры, если они существуют:
  
        rhgb quiet crashkernel=auto
  
    Графический quiet начальной загрузки, не используются в облачной среде, где мы хотим, чтобы все журналы toobe hello, отправляемых toohello последовательного порта. Hello `crashkernel` возможность влево, при желании настроить, но следует заметить, что этот параметр приведет к уменьшению hello объем доступной памяти в hello виртуальная машина по 128 МБ или больше, которое может быть проблематично на hello меньшего размера виртуальной Машины.

* Установка агента Azure Linux hello
  
    для подготовки образа Linux на платформе Azure требуется Hello агент Azure Linux.  Большинство установок предоставляют агента hello как пакет RPM или Deb (hello пакет обычно называется «WALinuxAgent» или «walinuxagent»).  Hello агент также можно установить вручную, следуя указаниям hello hello [руководство агент Linux](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

* Убедитесь, что hello SSH сервер установлен и настроен toostart во время загрузки.  Обычно это происходит по умолчанию hello.

* Не создавайте подкачки на диске ОС hello
  
    Hello Azure Linux Agent может автоматически настроить подкачки с помощью hello локальный диск ресурсов, toohello подключенных виртуальных Машин после подготовки в Azure. Обратите внимание, что hello локальный диск ресурсов *временные* диск, а также может очищаться при отмененной подготовкой hello виртуальной Машины. После установки hello Azure Linux Agent (см. выше), измените соответствующим образом следующие параметры в /etc/waagent.conf hello:
  
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

* В качестве последнего шага выполните следующие команды toodeprovision hello виртуальной машины hello:
  
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
  
  > [!NOTE]
  > На Virtualbox может появиться следующая ошибка после выполнения hello "waagent-force - deprovision": `[Errno 5] Input/output error`. Это сообщение об ошибке не является важным и может быть пропущено.
  > 
  > 

* Затем может потребоваться tooshut работу hello виртуальной машины и передать tooAzure hello виртуального жесткого диска.

