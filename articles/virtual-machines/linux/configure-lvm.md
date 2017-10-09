---
title: "aaaConfigure LVM на виртуальной машине под управлением Linux | Документы Microsoft"
description: "Узнайте, как tooconfigure LVM в Linux в Azure."
services: virtual-machines-linux
documentationcenter: na
author: szarkos
manager: timlt
editor: tysonn
tag: azure-service-management,azure-resource-manager
ms.assetid: 7f533725-1484-479d-9472-6b3098d0aecc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 8daf792d87c6bb3d91a2eddcd01cfab34fd28cff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-lvm-on-a-linux-vm-in-azure"></a>Настройка диспетчера логических томов на виртуальной машине Linux в Azure
В этом документе будут рассматриваться как tooconfigure диспетчер логических томов (LVM) на виртуальной машине Azure. Хотя и существует нецелесообразно tooconfigure LVM на любом диске присоединенного toohello виртуальной машины, по умолчанию большинство облаку изображений не будет LVM настроен на hello диска ОС. Это tooprevent проблем с группами повторяющиеся тома, если диск ОС-нибудь hello присоединенного tooanother виртуальная машина hello одинаковое распределение и тип, т. е. во время восстановления. Поэтому рекомендуется только toouse LVM на дисках данных hello.

## <a name="linear-vs-striped-logical-volumes"></a>Линейные и чередующиеся логические тома
LVM может быть используется toocombine количество физических дисков в одному тому хранилища. По умолчанию LVM обычно создаст линейной логических томах, что означает физическое хранилище hello соединенных вместе. В этом случае операции чтения и записи будет обычно отправляться только одного диска tooa. В отличие от этого, мы также чередующиеся тома могут создаваться логических операций чтения и записи в которых распределенных toomultiple дисков в группе томов hello (т. е. аналогично tooRAID0). Для повышения производительности, скорее всего, вы будете toostripe логических томов, чтобы операции чтения и записи используют все диски данных.

В этом документе описаны как toocombine данные за несколько дисков в одну группу томов и затем создать чередующийся том логического. Hello шаги будут немного обобщенный toowork с большинством дистрибутивов. В большинстве случаев hello служебные программы и рабочие процессы для управления LVM в Azure не отличаются фундаментально от других сред. Для получения дополнительных сведений и рекомендаций по использованию диспетчера логических томов с вашим дистрибутивом обратитесь к поставщику Linux.

## <a name="attaching-data-disks"></a>Присоединение дисков данных
Один часто будут toostart с двумя или более пустые диски для данных при использовании LVM. Исходя из потребностей операции ввода-ВЫВОДА, вы можете tooattach дисков, которые хранятся в нашем стандартное хранилище с вверх too500 операции ввода-ВЫВОДА/ps на диск или дисковое нашей Premium с вверх too5000 операции ввода-ВЫВОДА/ps на одном диске. В этой статье будет подробно не о том, как tooprovision и присоединения виртуальной машины Linux tooa данных дисков. См. в разделе статьи Microsoft Azure hello [подключить диск](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) подробные инструкции по как tooattach пустые данные на диске tooa Linux виртуальной машины в Azure.

## <a name="install-hello-lvm-utilities"></a>Установите служебные программы LVM hello
* **Ubuntu**

    ```bash  
    sudo apt-get update
    sudo apt-get install lvm2
    ```

* **RHEL, CentOS и Oracle Linux**

    ```bash   
    sudo yum install lvm2
    ```

* **SLES 12 и openSUSE**

    ```bash   
    sudo zypper install lvm2
    ```

* **SLES 11**

    ```bash   
    sudo zypper install lvm2
    ```

    На SLES11 необходимо также изменить `/etc/sysconfig/lvm` и задайте `LVM_ACTIVATED_ON_DISCOVERED` слишком «включить»:

    ```sh   
    LVM_ACTIVATED_ON_DISCOVERED="enable" 
    ```

## <a name="configure-lvm"></a>Настройка диспетчера логических томов
В этом руководстве предполагается, вы привязали три диски с данными, которые мы будем называть tooas `/dev/sdc`, `/dev/sdd` и `/dev/sde`. Обратите внимание, что они могут не всегда быть hello же пути на виртуальной машине. Можно запустить "`sudo fdisk -l`" или аналогичную команду toolist доступных дисков.

1. Подготовка физических томов hello.

    ```bash    
    sudo pvcreate /dev/sd[cde]
    Physical volume "/dev/sdc" successfully created
    Physical volume "/dev/sdd" successfully created
    Physical volume "/dev/sde" successfully created
    ```

2. Создайте группу томов. В этом примере мы вызов группы томов hello `data-vg01`:

    ```bash    
    sudo vgcreate data-vg01 /dev/sd[cde]
    Volume group "data-vg01" successfully created
    ```

3. Создание логических томов hello. Hello команда ниже мы создает один логический том вызове `data-lv01` toospan hello весь том группы, но Обратите внимание, что также нецелесообразно toocreate несколько логических томов в группы томов hello.

    ```bash   
    sudo lvcreate --extents 100%FREE --stripes 3 --name data-lv01 data-vg01
    Logical volume "data-lv01" created.
    ```

4. Логический том формате hello

    ```bash  
    sudo mkfs -t ext4 /dev/data-vg01/data-lv01
    ```
   
   > [!NOTE]
   > Для SLES11 замените ext4 на `-t ext3`. SLES11 поддерживает только файловые системы tooext4 доступ только для чтения.

## <a name="add-hello-new-file-system-tooetcfstab"></a>Добавить hello новый файл system слишком/и т. д/fstab
> [!IMPORTANT]
> Неправильное редактирование hello `/etc/fstab` файла может привести к невозможности загрузки системы. Если нет уверенности, см. документацию распространения toohello сведения о как tooproperly изменять этот файл. Также рекомендуется, чтобы резервная копия hello `/etc/fstab` создается файл, прежде чем изменять.

1. Создайте точку подключения hello требуемого для новой файловой системы, например:

    ```bash  
    sudo mkdir /data
    ```

2. Найти путь логический том hello

    ```bash    
    lvdisplay
    --- Logical volume ---
    LV Path                /dev/data-vg01/data-lv01
    ....
    ```

3. Откройте `/etc/fstab` в текстовом редакторе и добавьте запись для hello новой файловой системы, например:

    ```bash    
    /dev/data-vg01/data-lv01  /data  ext4  defaults  0  2
    ```   
    Затем сохраните и закройте `/etc/fstab`.

4. Тестирование этого hello `/etc/fstab` правильности введенных:

    ```bash    
    sudo mount -a
    ```

    Если эта команда приведет к сообщение об ошибке, Проверьте синтаксис hello в hello `/etc/fstab` файла.
   
    Далее выполните hello `mount` подключения команда tooensure hello файловой системы:

    ```bash    
    mount
    ......
    /dev/mapper/data--vg01-data--lv01 on /data type ext4 (rw)
    ```

5. (Необязательно) Параметры загрузки, предотвращающие сбой, в файле `/etc/fstab`
   
    Большинство установок включают либо hello `nobootwait` или `nofail` подключения параметры, которые могут быть добавлены toohello `/etc/fstab` файл. Эти параметры для сбоев при монтировании определенной файловой системы и выполнение tooboot toocontinue системы Linux hello даже если это не удается tooproperly подключения hello RAID файловой системы. Дополнительные сведения об этих параметрах см. документацию tooyour распространения.
   
    Пример (Ubuntu):

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,nobootwait  0  2
    ```

## <a name="trimunmap-support"></a>Поддержка операций TRIM и UNMAP
Некоторые версии Linux ядра поддержки TRIM и отмене СОПОСТАВЛЕНИЯ операций toodiscard неиспользуемые блоки на диске hello. Эти операции, в первую очередь используются в tooinform стандартное хранилище Azure, которая удалена страницы становятся недействительными и может быть удален. Удаление страниц позволит сократить затраты, если вы создаете большие файлы, а затем удаляете их.

Существует два способа tooenable TRIM поддержки в ВМ Linux. Как обычно см. на распределение hello рекомендованный подход:

- Используйте hello `discard` подключить параметр в `/etc/fstab`, например:

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,discard  0  2
    ```

- В некоторых случаях hello `discard` параметра может негативно сказаться на производительности. Кроме того, можно запустить hello `fstrim` вручную команды из командной строки hello, или добавьте его tooyour crontab toorun регулярно:

    **Ubuntu**

    ```bash 
    # sudo apt-get install util-linux
    # sudo fstrim /datadrive
    ```

    **RHEL или CentOS**

    ```bash 
    # sudo yum install util-linux
    # sudo fstrim /datadrive
    ```
