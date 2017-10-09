---
title: "aaaConfigure программного RAID на виртуальной машине под управлением Linux | Документы Microsoft"
description: "Узнайте, как RAID toouse mdadm tooconfigure в Linux в Azure."
services: virtual-machines-linux
documentationcenter: na
author: rickstercdn
manager: timlt
editor: tysonn
tag: azure-service-management,azure-resource-manager
ms.assetid: f3cb2786-bda6-4d2c-9aaf-2db80f490feb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: rclaus
ms.openlocfilehash: f06e2679d953faf88ffee9991226cdb3cc1cbdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-software-raid-on-linux"></a>Настройка программного RAID-массива в Linux
Это общие сценарии toouse программного RAID на виртуальных машинах Linux в Azure toopresent несколько вложенных данных диски как одно устройство RAID. Обычно это используется tooimprove производительность и разрешить для улучшения пропускной способности по сравнению toousing один диск.

## <a name="attaching-data-disks"></a>Присоединение дисков данных
Два или более пустые диски для данных, необходимые tooconfigure устройство RAID.  Hello основной причиной для создания устройства RAID является tooimprove производительности операций ввода-ВЫВОДА диска.  Исходя из потребностей операции ввода-ВЫВОДА, вы можете tooattach дисков, которые хранятся в нашем стандартное хранилище с вверх too500 операции ввода-ВЫВОДА/ps на диск или дисковое нашей Premium с вверх too5000 операции ввода-ВЫВОДА/ps на одном диске. В этой статье подробно не о том, как tooprovision и присоединения виртуальной машины Linux tooa данных дисков.  См. статью Microsoft Azure hello [подключить диск](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) подробные инструкции по как tooattach пустые данные на диске tooa Linux виртуальной машины в Azure.

## <a name="install-hello-mdadm-utility"></a>Установить программу mdadm hello
* **Ubuntu**
```bash
sudo apt-get update
sudo apt-get install mdadm
```

* **CentOS и Oracle Linux**
```bash
sudo yum install mdadm
```

* **SLES и openSUSE**
```bash  
zypper install mdadm
```

## <a name="create-hello-disk-partitions"></a>Создание разделов диска hello
В этом примере мы создаем один дисковый раздел в /dev/sdc. будет вызван /dev/sdc1 Hello нового раздела.

1. Запуск `fdisk` toobegin Создание разделов

    ```bash
    sudo fdisk /dev/sdc
    Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
    Building a new DOS disklabel with disk identifier 0xa34cb70c.
    Changes will remain in memory only, until you decide toowrite them.
    After that, of course, hello previous content won't be recoverable.

    WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
                    switch off hello mode (command 'c') and change display units to
                    sectors (command 'u').
    ```

2. Нажмите клавишу 'n' на hello prompt toocreate  **n** овый секции:

    ```bash
    Command (m for help): n
    ```

3. Затем нажмите клавишу «p» toocreate **p**вичный секции:

    ```bash 
    Command action
            e   extended
            p   primary partition (1-4)
    ```

4. Нажмите клавишу "1" tooselect секция с номером 1:

    ```bash
    Partition number (1-4): 1
    ```

5. Выберите hello начальную точку новой секции hello, или нажмите клавишу `<enter>` раздел tooaccept hello по умолчанию tooplace hello в начале hello hello свободного места на диске hello:

    ```bash   
    First cylinder (1-1305, default 1):
    Using default value 1
    ```

6. Выберите размер hello hello секции, например 10 гигабайт секции toocreate типа «+10G». Также можно нажать клавишу `<enter>` создать одну секцию, которая охватывает весь диск hello:

    ```bash   
    Last cylinder, +cylinders or +size{K,M,G} (1-1305, default 1305): 
    Using default value 1305
    ```

7. Затем измените идентификатор hello и **t**ИП hello секцию по умолчанию hello идентификатор "83" (Linux) tooID «fd» (Linux raid автоматически):

    ```bash  
    Command (m for help): t
    Selected partition 1
    Hex code (type L toolist codes): fd
    ```

8. Наконец написание hello секции таблицы toohello диска и выйти из программы.

    ```bash   
    Command (m for help): w
    hello partition table has been altered!
    ```

## <a name="create-hello-raid-array"></a>Создать hello RAID-массив
1. Следующий пример будет «полосы» (уровень RAID 0) трех разделов, расположенных на трех отдельных дисках данных (sdc1, sdd1, sde1) Hello.  После выполнения этой команды будет создано устройство RAID — **/dev/md127** . Также Обратите внимание, что если эти данные диски мы ранее частью другой уничтоженных RAID-массив может быть необходимые tooadd hello `--force` toohello параметр `mdadm` команды:

    ```bash  
    sudo mdadm --create /dev/md127 --level 0 --raid-devices 3 \
        /dev/sdc1 /dev/sdd1 /dev/sde1
    ```

2. Создайте hello файловой системы на новое устройство RAID hello
   
    а. **CentOS, Oracle Linux, SLES 12, openSUSE и Ubuntu**

    ```bash   
    sudo mkfs -t ext4 /dev/md127
    ```
   
    b. **SLES 11**

    ```bash
    sudo mkfs -t ext3 /dev/md127
    ```
   
    c. **SLES 11** — включите boot.md и создайте mdadm.conf.

    ```bash
    sudo -i chkconfig --add boot.md
    sudo echo 'DEVICE /dev/sd*[0-9]' >> /etc/mdadm.conf
    ```
   
   > [!NOTE]
   > После внесения этих изменений в системах SUSE может потребоваться перезагрузка. Этот шаг *не* является обязательным для SLES 12.
   > 
   > 

## <a name="add-hello-new-file-system-tooetcfstab"></a>Добавить hello новый файл system слишком/и т. д/fstab
> [!IMPORTANT]
> Неправильно редактировать файл/etc/fstab hello может привести к невозможности загрузки системы. Если нет уверенности, сведения о этот файл, как изменять tooproperly см toohello распространения документации. Также рекомендуется, прежде чем изменять создается резервная копия файл/etc/fstab hello.

1. Создайте точку подключения hello требуемого для новой файловой системы, например:

    ```bash
    sudo mkdir /data
    ```
2. При редактировании/etc/fstab, hello **UUID** должно быть используется tooreference hello системы, а не hello устройства имя файла.  Используйте hello `blkid` toodetermine программа hello UUID для hello новая файловая система:

    ```bash   
    sudo /sbin/blkid
    ...........
    /dev/md127: UUID="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee" TYPE="ext4"
    ```

3. Откройте/etc/fstab в текстовом редакторе и добавьте запись для hello новой файловой системы, например:

    ```bash   
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults  0  2
    ```
   
    **SLES 11**:

    ```bash
    /dev/disk/by-uuid/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext3  defaults  0  2
    ```
   
    Затем сохраните и закройте /etc/fstab.

4. Проверьте правильность hello/etc/fstab записи:

    ```bash  
    sudo mount -a
    ```

    Если эта команда приведет к сообщение об ошибке, Проверьте синтаксис hello в файле/etc/fstab hello.
   
    Далее выполните hello `mount` подключения команда tooensure hello файловой системы:

    ```bash   
    mount
    .................
    /dev/md127 on /data type ext4 (rw)
    ```

5. (Необязательно) Параметры загрузки в безопасном режиме
   
    **Конфигурация fstab**
   
    Большинство установок включают либо hello `nobootwait` или `nofail` подключения параметры, которые могут быть добавлены toohello/etc/fstab файла. Эти параметры для сбоев при монтировании определенной файловой системы и выполнение tooboot toocontinue системы Linux hello даже если это не удается tooproperly подключения hello RAID файловой системы. Дополнительные сведения об этих параметрах см. в документации tooyour распространения.
   
    Пример (Ubuntu):

    ```bash  
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,nobootwait  0  2
    ```   

    **Параметры загрузки Linux**
   
    В дополнение toohello выше параметров, hello параметр ядра "`bootdegraded=true`" можно разрешить tooboot системы hello, даже в том случае, если hello RAID воспринимается как поврежден или сниженной активности, например, если диск с данными случайно удален из виртуальной машины hello. По умолчанию это может также привести к невозможности загрузки системы.
   
    См. документации tooyour распространения на как tooproperly изменить параметры ядра. Например, в большинство установок (CentOS, Oracle Linux SLES 11) эти параметры могут быть добавлены вручную toohello "`/boot/grub/menu.lst`" файла.  В Ubuntu этот параметр можно добавить toohello `GRUB_CMDLINE_LINUX_DEFAULT` переменной на «/ и т. д, по умолчанию или grub».


## <a name="trimunmap-support"></a>Поддержка операций TRIM и UNMAP
Некоторые версии Linux ядра поддержки TRIM и отмене СОПОСТАВЛЕНИЯ операций toodiscard неиспользуемые блоки на диске hello. Эти операции, в первую очередь используются в tooinform стандартное хранилище Azure, которая удалена страницы становятся недействительными и может быть удален. Удаление страниц позволит сократить затраты, если вы создаете большие файлы, а затем удаляете их.

> [!NOTE]
> RAID может выполнять команды отклонения не в том случае, если размер фрагмента данных hello для hello массива задается сборки, чем по умолчанию hello (512 КБ). Это так, как отменить сопоставление hello степенью гранулярности hello узла также равен 512 КБ. Если вы изменили размер фрагмента массива hello через его mdadm `--chunk=` ядре hello может быть пропущен параметр, а затем TRIM или отменить сопоставление запросов.

Существует два способа tooenable TRIM поддержки в ВМ Linux. Как обычно см. на распределение hello рекомендованный подход:

- Используйте hello `discard` подключить параметр в `/etc/fstab`, например:

    ```bash
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,discard  0  2
    ```

- В некоторых случаях hello `discard` параметра может негативно сказаться на производительности. Кроме того, можно запустить hello `fstrim` вручную команды из командной строки hello, или добавьте его tooyour crontab toorun регулярно:

    **Ubuntu**

    ```bash
    # sudo apt-get install util-linux
    # sudo fstrim /data
    ```

    **RHEL или CentOS**
    ```bash
    # sudo yum install util-linux
    # sudo fstrim /data
    ```
