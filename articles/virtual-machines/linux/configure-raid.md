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
# <a name="configure-software-raid-on-linux"></a><span data-ttu-id="7b05a-103">Настройка программного RAID-массива в Linux</span><span class="sxs-lookup"><span data-stu-id="7b05a-103">Configure Software RAID on Linux</span></span>
<span data-ttu-id="7b05a-104">Это общие сценарии toouse программного RAID на виртуальных машинах Linux в Azure toopresent несколько вложенных данных диски как одно устройство RAID.</span><span class="sxs-lookup"><span data-stu-id="7b05a-104">It's a common scenario toouse software RAID on Linux virtual machines in Azure toopresent multiple attached data disks as a single RAID device.</span></span> <span data-ttu-id="7b05a-105">Обычно это используется tooimprove производительность и разрешить для улучшения пропускной способности по сравнению toousing один диск.</span><span class="sxs-lookup"><span data-stu-id="7b05a-105">Typically this can be used tooimprove performance and allow for improved throughput compared toousing just a single disk.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="7b05a-106">Присоединение дисков данных</span><span class="sxs-lookup"><span data-stu-id="7b05a-106">Attaching data disks</span></span>
<span data-ttu-id="7b05a-107">Два или более пустые диски для данных, необходимые tooconfigure устройство RAID.</span><span class="sxs-lookup"><span data-stu-id="7b05a-107">Two or more empty data disks are needed tooconfigure a RAID device.</span></span>  <span data-ttu-id="7b05a-108">Hello основной причиной для создания устройства RAID является tooimprove производительности операций ввода-ВЫВОДА диска.</span><span class="sxs-lookup"><span data-stu-id="7b05a-108">hello primary reason for creating a RAID device is tooimprove performance of your disk IO.</span></span>  <span data-ttu-id="7b05a-109">Исходя из потребностей операции ввода-ВЫВОДА, вы можете tooattach дисков, которые хранятся в нашем стандартное хранилище с вверх too500 операции ввода-ВЫВОДА/ps на диск или дисковое нашей Premium с вверх too5000 операции ввода-ВЫВОДА/ps на одном диске.</span><span class="sxs-lookup"><span data-stu-id="7b05a-109">Based on your IO needs, you can choose tooattach disks that are stored in our Standard Storage, with up too500 IO/ps per disk or our Premium storage with up too5000 IO/ps per disk.</span></span> <span data-ttu-id="7b05a-110">В этой статье подробно не о том, как tooprovision и присоединения виртуальной машины Linux tooa данных дисков.</span><span class="sxs-lookup"><span data-stu-id="7b05a-110">This article does not go into detail on how tooprovision and attach data disks tooa Linux virtual machine.</span></span>  <span data-ttu-id="7b05a-111">См. статью Microsoft Azure hello [подключить диск](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) подробные инструкции по как tooattach пустые данные на диске tooa Linux виртуальной машины в Azure.</span><span class="sxs-lookup"><span data-stu-id="7b05a-111">See hello Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how tooattach an empty data disk tooa Linux virtual machine on Azure.</span></span>

## <a name="install-hello-mdadm-utility"></a><span data-ttu-id="7b05a-112">Установить программу mdadm hello</span><span class="sxs-lookup"><span data-stu-id="7b05a-112">Install hello mdadm utility</span></span>
* <span data-ttu-id="7b05a-113">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="7b05a-113">**Ubuntu**</span></span>
```bash
sudo apt-get update
sudo apt-get install mdadm
```

* <span data-ttu-id="7b05a-114">**CentOS и Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="7b05a-114">**CentOS & Oracle Linux**</span></span>
```bash
sudo yum install mdadm
```

* <span data-ttu-id="7b05a-115">**SLES и openSUSE**</span><span class="sxs-lookup"><span data-stu-id="7b05a-115">**SLES and openSUSE**</span></span>
```bash  
zypper install mdadm
```

## <a name="create-hello-disk-partitions"></a><span data-ttu-id="7b05a-116">Создание разделов диска hello</span><span class="sxs-lookup"><span data-stu-id="7b05a-116">Create hello disk partitions</span></span>
<span data-ttu-id="7b05a-117">В этом примере мы создаем один дисковый раздел в /dev/sdc.</span><span class="sxs-lookup"><span data-stu-id="7b05a-117">In this example, we create a single disk partition on /dev/sdc.</span></span> <span data-ttu-id="7b05a-118">будет вызван /dev/sdc1 Hello нового раздела.</span><span class="sxs-lookup"><span data-stu-id="7b05a-118">hello new disk partition will be called /dev/sdc1.</span></span>

1. <span data-ttu-id="7b05a-119">Запуск `fdisk` toobegin Создание разделов</span><span class="sxs-lookup"><span data-stu-id="7b05a-119">Start `fdisk` toobegin creating partitions</span></span>

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

2. <span data-ttu-id="7b05a-120">Нажмите клавишу 'n' на hello prompt toocreate  **n** овый секции:</span><span class="sxs-lookup"><span data-stu-id="7b05a-120">Press 'n' at hello prompt toocreate a **n**ew partition:</span></span>

    ```bash
    Command (m for help): n
    ```

3. <span data-ttu-id="7b05a-121">Затем нажмите клавишу «p» toocreate **p**вичный секции:</span><span class="sxs-lookup"><span data-stu-id="7b05a-121">Next, press 'p' toocreate a **p**rimary partition:</span></span>

    ```bash 
    Command action
            e   extended
            p   primary partition (1-4)
    ```

4. <span data-ttu-id="7b05a-122">Нажмите клавишу "1" tooselect секция с номером 1:</span><span class="sxs-lookup"><span data-stu-id="7b05a-122">Press '1' tooselect partition number 1:</span></span>

    ```bash
    Partition number (1-4): 1
    ```

5. <span data-ttu-id="7b05a-123">Выберите hello начальную точку новой секции hello, или нажмите клавишу `<enter>` раздел tooaccept hello по умолчанию tooplace hello в начале hello hello свободного места на диске hello:</span><span class="sxs-lookup"><span data-stu-id="7b05a-123">Select hello starting point of hello new partition, or press `<enter>` tooaccept hello default tooplace hello partition at hello beginning of hello free space on hello drive:</span></span>

    ```bash   
    First cylinder (1-1305, default 1):
    Using default value 1
    ```

6. <span data-ttu-id="7b05a-124">Выберите размер hello hello секции, например 10 гигабайт секции toocreate типа «+10G».</span><span class="sxs-lookup"><span data-stu-id="7b05a-124">Select hello size of hello partition, for example type '+10G' toocreate a 10 gigabyte partition.</span></span> <span data-ttu-id="7b05a-125">Также можно нажать клавишу `<enter>` создать одну секцию, которая охватывает весь диск hello:</span><span class="sxs-lookup"><span data-stu-id="7b05a-125">Or, press `<enter>` create a single partition that spans hello entire drive:</span></span>

    ```bash   
    Last cylinder, +cylinders or +size{K,M,G} (1-1305, default 1305): 
    Using default value 1305
    ```

7. <span data-ttu-id="7b05a-126">Затем измените идентификатор hello и **t**ИП hello секцию по умолчанию hello идентификатор "83" (Linux) tooID «fd» (Linux raid автоматически):</span><span class="sxs-lookup"><span data-stu-id="7b05a-126">Next, change hello ID and **t**ype of hello partition from hello default ID '83' (Linux) tooID 'fd' (Linux raid auto):</span></span>

    ```bash  
    Command (m for help): t
    Selected partition 1
    Hex code (type L toolist codes): fd
    ```

8. <span data-ttu-id="7b05a-127">Наконец написание hello секции таблицы toohello диска и выйти из программы.</span><span class="sxs-lookup"><span data-stu-id="7b05a-127">Finally, write hello partition table toohello drive and exit fdisk:</span></span>

    ```bash   
    Command (m for help): w
    hello partition table has been altered!
    ```

## <a name="create-hello-raid-array"></a><span data-ttu-id="7b05a-128">Создать hello RAID-массив</span><span class="sxs-lookup"><span data-stu-id="7b05a-128">Create hello RAID array</span></span>
1. <span data-ttu-id="7b05a-129">Следующий пример будет «полосы» (уровень RAID 0) трех разделов, расположенных на трех отдельных дисках данных (sdc1, sdd1, sde1) Hello.</span><span class="sxs-lookup"><span data-stu-id="7b05a-129">hello following example will "stripe" (RAID level 0) three partitions located on three separate data disks (sdc1, sdd1, sde1).</span></span>  <span data-ttu-id="7b05a-130">После выполнения этой команды будет создано устройство RAID — **/dev/md127** .</span><span class="sxs-lookup"><span data-stu-id="7b05a-130">After running this command a new RAID device called **/dev/md127** is created.</span></span> <span data-ttu-id="7b05a-131">Также Обратите внимание, что если эти данные диски мы ранее частью другой уничтоженных RAID-массив может быть необходимые tooadd hello `--force` toohello параметр `mdadm` команды:</span><span class="sxs-lookup"><span data-stu-id="7b05a-131">Also note that if these data disks we previously part of another defunct RAID array it may be necessary tooadd hello `--force` parameter toohello `mdadm` command:</span></span>

    ```bash  
    sudo mdadm --create /dev/md127 --level 0 --raid-devices 3 \
        /dev/sdc1 /dev/sdd1 /dev/sde1
    ```

2. <span data-ttu-id="7b05a-132">Создайте hello файловой системы на новое устройство RAID hello</span><span class="sxs-lookup"><span data-stu-id="7b05a-132">Create hello file system on hello new RAID device</span></span>
   
    <span data-ttu-id="7b05a-133">а.</span><span class="sxs-lookup"><span data-stu-id="7b05a-133">a.</span></span> <span data-ttu-id="7b05a-134">**CentOS, Oracle Linux, SLES 12, openSUSE и Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="7b05a-134">**CentOS, Oracle Linux, SLES 12, openSUSE, and Ubuntu**</span></span>

    ```bash   
    sudo mkfs -t ext4 /dev/md127
    ```
   
    <span data-ttu-id="7b05a-135">b.</span><span class="sxs-lookup"><span data-stu-id="7b05a-135">b.</span></span> <span data-ttu-id="7b05a-136">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="7b05a-136">**SLES 11**</span></span>

    ```bash
    sudo mkfs -t ext3 /dev/md127
    ```
   
    <span data-ttu-id="7b05a-137">c.</span><span class="sxs-lookup"><span data-stu-id="7b05a-137">c.</span></span> <span data-ttu-id="7b05a-138">**SLES 11** — включите boot.md и создайте mdadm.conf.</span><span class="sxs-lookup"><span data-stu-id="7b05a-138">**SLES 11** - enable boot.md and create mdadm.conf</span></span>

    ```bash
    sudo -i chkconfig --add boot.md
    sudo echo 'DEVICE /dev/sd*[0-9]' >> /etc/mdadm.conf
    ```
   
   > [!NOTE]
   > <span data-ttu-id="7b05a-139">После внесения этих изменений в системах SUSE может потребоваться перезагрузка.</span><span class="sxs-lookup"><span data-stu-id="7b05a-139">A reboot may be required after making these changes on SUSE systems.</span></span> <span data-ttu-id="7b05a-140">Этот шаг *не* является обязательным для SLES 12.</span><span class="sxs-lookup"><span data-stu-id="7b05a-140">This step is *not* required on SLES 12.</span></span>
   > 
   > 

## <a name="add-hello-new-file-system-tooetcfstab"></a><span data-ttu-id="7b05a-141">Добавить hello новый файл system слишком/и т. д/fstab</span><span class="sxs-lookup"><span data-stu-id="7b05a-141">Add hello new file system too/etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7b05a-142">Неправильно редактировать файл/etc/fstab hello может привести к невозможности загрузки системы.</span><span class="sxs-lookup"><span data-stu-id="7b05a-142">Improperly editing hello /etc/fstab file could result in an unbootable system.</span></span> <span data-ttu-id="7b05a-143">Если нет уверенности, сведения о этот файл, как изменять tooproperly см toohello распространения документации.</span><span class="sxs-lookup"><span data-stu-id="7b05a-143">If unsure, refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="7b05a-144">Также рекомендуется, прежде чем изменять создается резервная копия файл/etc/fstab hello.</span><span class="sxs-lookup"><span data-stu-id="7b05a-144">It is also recommended that a backup of hello /etc/fstab file is created before editing.</span></span>

1. <span data-ttu-id="7b05a-145">Создайте точку подключения hello требуемого для новой файловой системы, например:</span><span class="sxs-lookup"><span data-stu-id="7b05a-145">Create hello desired mount point for your new file system, for example:</span></span>

    ```bash
    sudo mkdir /data
    ```
2. <span data-ttu-id="7b05a-146">При редактировании/etc/fstab, hello **UUID** должно быть используется tooreference hello системы, а не hello устройства имя файла.</span><span class="sxs-lookup"><span data-stu-id="7b05a-146">When editing /etc/fstab, hello **UUID** should be used tooreference hello file system rather than hello device name.</span></span>  <span data-ttu-id="7b05a-147">Используйте hello `blkid` toodetermine программа hello UUID для hello новая файловая система:</span><span class="sxs-lookup"><span data-stu-id="7b05a-147">Use hello `blkid` utility toodetermine hello UUID for hello new file system:</span></span>

    ```bash   
    sudo /sbin/blkid
    ...........
    /dev/md127: UUID="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee" TYPE="ext4"
    ```

3. <span data-ttu-id="7b05a-148">Откройте/etc/fstab в текстовом редакторе и добавьте запись для hello новой файловой системы, например:</span><span class="sxs-lookup"><span data-stu-id="7b05a-148">Open /etc/fstab in a text editor and add an entry for hello new file system, for example:</span></span>

    ```bash   
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults  0  2
    ```
   
    <span data-ttu-id="7b05a-149">**SLES 11**:</span><span class="sxs-lookup"><span data-stu-id="7b05a-149">Or on **SLES 11**:</span></span>

    ```bash
    /dev/disk/by-uuid/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext3  defaults  0  2
    ```
   
    <span data-ttu-id="7b05a-150">Затем сохраните и закройте /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="7b05a-150">Then, save and close /etc/fstab.</span></span>

4. <span data-ttu-id="7b05a-151">Проверьте правильность hello/etc/fstab записи:</span><span class="sxs-lookup"><span data-stu-id="7b05a-151">Test that hello /etc/fstab entry is correct:</span></span>

    ```bash  
    sudo mount -a
    ```

    <span data-ttu-id="7b05a-152">Если эта команда приведет к сообщение об ошибке, Проверьте синтаксис hello в файле/etc/fstab hello.</span><span class="sxs-lookup"><span data-stu-id="7b05a-152">If this command results in an error message, please check hello syntax in hello /etc/fstab file.</span></span>
   
    <span data-ttu-id="7b05a-153">Далее выполните hello `mount` подключения команда tooensure hello файловой системы:</span><span class="sxs-lookup"><span data-stu-id="7b05a-153">Next run hello `mount` command tooensure hello file system is mounted:</span></span>

    ```bash   
    mount
    .................
    /dev/md127 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="7b05a-154">(Необязательно) Параметры загрузки в безопасном режиме</span><span class="sxs-lookup"><span data-stu-id="7b05a-154">(Optional) Failsafe Boot Parameters</span></span>
   
    <span data-ttu-id="7b05a-155">**Конфигурация fstab**</span><span class="sxs-lookup"><span data-stu-id="7b05a-155">**fstab configuration**</span></span>
   
    <span data-ttu-id="7b05a-156">Большинство установок включают либо hello `nobootwait` или `nofail` подключения параметры, которые могут быть добавлены toohello/etc/fstab файла.</span><span class="sxs-lookup"><span data-stu-id="7b05a-156">Many distributions include either hello `nobootwait` or `nofail` mount parameters that may be added toohello /etc/fstab file.</span></span> <span data-ttu-id="7b05a-157">Эти параметры для сбоев при монтировании определенной файловой системы и выполнение tooboot toocontinue системы Linux hello даже если это не удается tooproperly подключения hello RAID файловой системы.</span><span class="sxs-lookup"><span data-stu-id="7b05a-157">These parameters allow for failures when mounting a particular file system and allow hello Linux system toocontinue tooboot even if it is unable tooproperly mount hello RAID file system.</span></span> <span data-ttu-id="7b05a-158">Дополнительные сведения об этих параметрах см. в документации tooyour распространения.</span><span class="sxs-lookup"><span data-stu-id="7b05a-158">Refer tooyour distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="7b05a-159">Пример (Ubuntu):</span><span class="sxs-lookup"><span data-stu-id="7b05a-159">Example (Ubuntu):</span></span>

    ```bash  
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,nobootwait  0  2
    ```   

    <span data-ttu-id="7b05a-160">**Параметры загрузки Linux**</span><span class="sxs-lookup"><span data-stu-id="7b05a-160">**Linux boot parameters**</span></span>
   
    <span data-ttu-id="7b05a-161">В дополнение toohello выше параметров, hello параметр ядра "`bootdegraded=true`" можно разрешить tooboot системы hello, даже в том случае, если hello RAID воспринимается как поврежден или сниженной активности, например, если диск с данными случайно удален из виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="7b05a-161">In addition toohello above parameters, hello kernel parameter "`bootdegraded=true`" can allow hello system tooboot even if hello RAID is perceived as damaged or degraded, for example if a data drive is inadvertently removed from hello virtual machine.</span></span> <span data-ttu-id="7b05a-162">По умолчанию это может также привести к невозможности загрузки системы.</span><span class="sxs-lookup"><span data-stu-id="7b05a-162">By default this could also result in a non-bootable system.</span></span>
   
    <span data-ttu-id="7b05a-163">См. документации tooyour распространения на как tooproperly изменить параметры ядра.</span><span class="sxs-lookup"><span data-stu-id="7b05a-163">Please refer tooyour distribution's documentation on how tooproperly edit kernel parameters.</span></span> <span data-ttu-id="7b05a-164">Например, в большинство установок (CentOS, Oracle Linux SLES 11) эти параметры могут быть добавлены вручную toohello "`/boot/grub/menu.lst`" файла.</span><span class="sxs-lookup"><span data-stu-id="7b05a-164">For example, in many distributions (CentOS, Oracle Linux, SLES 11) these parameters may be added manually toohello "`/boot/grub/menu.lst`" file.</span></span>  <span data-ttu-id="7b05a-165">В Ubuntu этот параметр можно добавить toohello `GRUB_CMDLINE_LINUX_DEFAULT` переменной на «/ и т. д, по умолчанию или grub».</span><span class="sxs-lookup"><span data-stu-id="7b05a-165">On Ubuntu this parameter can be added toohello `GRUB_CMDLINE_LINUX_DEFAULT` variable on "/etc/default/grub".</span></span>


## <a name="trimunmap-support"></a><span data-ttu-id="7b05a-166">Поддержка операций TRIM и UNMAP</span><span class="sxs-lookup"><span data-stu-id="7b05a-166">TRIM/UNMAP support</span></span>
<span data-ttu-id="7b05a-167">Некоторые версии Linux ядра поддержки TRIM и отмене СОПОСТАВЛЕНИЯ операций toodiscard неиспользуемые блоки на диске hello.</span><span class="sxs-lookup"><span data-stu-id="7b05a-167">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="7b05a-168">Эти операции, в первую очередь используются в tooinform стандартное хранилище Azure, которая удалена страницы становятся недействительными и может быть удален.</span><span class="sxs-lookup"><span data-stu-id="7b05a-168">These operations are primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="7b05a-169">Удаление страниц позволит сократить затраты, если вы создаете большие файлы, а затем удаляете их.</span><span class="sxs-lookup"><span data-stu-id="7b05a-169">Discarding pages can save cost if you create large files and then delete them.</span></span>

> [!NOTE]
> <span data-ttu-id="7b05a-170">RAID может выполнять команды отклонения не в том случае, если размер фрагмента данных hello для hello массива задается сборки, чем по умолчанию hello (512 КБ).</span><span class="sxs-lookup"><span data-stu-id="7b05a-170">RAID may not issue discard commands if hello chunk size for hello array is set tooless than hello default (512KB).</span></span> <span data-ttu-id="7b05a-171">Это так, как отменить сопоставление hello степенью гранулярности hello узла также равен 512 КБ.</span><span class="sxs-lookup"><span data-stu-id="7b05a-171">This is because hello unmap granularity on hello Host is also 512KB.</span></span> <span data-ttu-id="7b05a-172">Если вы изменили размер фрагмента массива hello через его mdadm `--chunk=` ядре hello может быть пропущен параметр, а затем TRIM или отменить сопоставление запросов.</span><span class="sxs-lookup"><span data-stu-id="7b05a-172">If you modified hello array's chunk size via mdadm's `--chunk=` parameter, then TRIM/unmap requests may be ignored by hello kernel.</span></span>

<span data-ttu-id="7b05a-173">Существует два способа tooenable TRIM поддержки в ВМ Linux.</span><span class="sxs-lookup"><span data-stu-id="7b05a-173">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="7b05a-174">Как обычно см. на распределение hello рекомендованный подход:</span><span class="sxs-lookup"><span data-stu-id="7b05a-174">As usual, consult your distribution for hello recommended approach:</span></span>

- <span data-ttu-id="7b05a-175">Используйте hello `discard` подключить параметр в `/etc/fstab`, например:</span><span class="sxs-lookup"><span data-stu-id="7b05a-175">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="7b05a-176">В некоторых случаях hello `discard` параметра может негативно сказаться на производительности.</span><span class="sxs-lookup"><span data-stu-id="7b05a-176">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="7b05a-177">Кроме того, можно запустить hello `fstrim` вручную команды из командной строки hello, или добавьте его tooyour crontab toorun регулярно:</span><span class="sxs-lookup"><span data-stu-id="7b05a-177">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>

    <span data-ttu-id="7b05a-178">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="7b05a-178">**Ubuntu**</span></span>

    ```bash
    # sudo apt-get install util-linux
    # sudo fstrim /data
    ```

    <span data-ttu-id="7b05a-179">**RHEL или CentOS**</span><span class="sxs-lookup"><span data-stu-id="7b05a-179">**RHEL/CentOS**</span></span>
    ```bash
    # sudo yum install util-linux
    # sudo fstrim /data
    ```
