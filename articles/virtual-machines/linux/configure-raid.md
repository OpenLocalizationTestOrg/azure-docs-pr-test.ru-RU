---
title: "Настройка программного RAID-массива на виртуальной машине под управлением Linux | Документация Майкрософт"
description: "Узнайте, как использовать mdadm для настройки RAID-массива на платформе Linux в Azure."
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
ms.openlocfilehash: 12f540a700fbf85e579e8aadc9f6def039299ff7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-software-raid-on-linux"></a><span data-ttu-id="4cc09-103">Настройка программного RAID-массива в Linux</span><span class="sxs-lookup"><span data-stu-id="4cc09-103">Configure Software RAID on Linux</span></span>
<span data-ttu-id="4cc09-104">Это обычный сценарий для использования программного RAID-массива на виртуальных машинах Linux в Azure, который позволяет представить множество дисков данных в виде одного RAID-устройства.</span><span class="sxs-lookup"><span data-stu-id="4cc09-104">It's a common scenario to use software RAID on Linux virtual machines in Azure to present multiple attached data disks as a single RAID device.</span></span> <span data-ttu-id="4cc09-105">Обычно это делается для повышения производительности и обеспечения возможности увеличения пропускной способности по сравнению с использованием только одного диска.</span><span class="sxs-lookup"><span data-stu-id="4cc09-105">Typically this can be used to improve performance and allow for improved throughput compared to using just a single disk.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="4cc09-106">Присоединение дисков данных</span><span class="sxs-lookup"><span data-stu-id="4cc09-106">Attaching data disks</span></span>
<span data-ttu-id="4cc09-107">Для настройки RAID-устройства требуется не менее двух пустых дисков данных.</span><span class="sxs-lookup"><span data-stu-id="4cc09-107">Two or more empty data disks are needed to configure a RAID device.</span></span>  <span data-ttu-id="4cc09-108">Основная причина создания устройства RAID — повышение производительности операций ввода-вывода дисков.</span><span class="sxs-lookup"><span data-stu-id="4cc09-108">The primary reason for creating a RAID device is to improve performance of your disk IO.</span></span>  <span data-ttu-id="4cc09-109">В зависимости от потребностей ввода-вывода, можно подключить диски, которые хранятся в хранилище уровня "Стандартный" и допускают до 500 операций ввода-вывода в секунду на диск, или диски из хранилища уровня "Премиум", поддерживающие до 5000 операций ввода-вывода в секунду.</span><span class="sxs-lookup"><span data-stu-id="4cc09-109">Based on your IO needs, you can choose to attach disks that are stored in our Standard Storage, with up to 500 IO/ps per disk or our Premium storage with up to 5000 IO/ps per disk.</span></span> <span data-ttu-id="4cc09-110">В этой статье мы не останавливаемся подробно на том, как подготовить и подключить диски данных к виртуальной машине Linux.</span><span class="sxs-lookup"><span data-stu-id="4cc09-110">This article does not go into detail on how to provision and attach data disks to a Linux virtual machine.</span></span>  <span data-ttu-id="4cc09-111">Подробные указания по подключению пустого диска данных к виртуальной машине Linux в Azure см. в разделе [Добавление диска](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) статьи Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="4cc09-111">See the Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how to attach an empty data disk to a Linux virtual machine on Azure.</span></span>

## <a name="install-the-mdadm-utility"></a><span data-ttu-id="4cc09-112">Установка служебной программы mdadm</span><span class="sxs-lookup"><span data-stu-id="4cc09-112">Install the mdadm utility</span></span>
* <span data-ttu-id="4cc09-113">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="4cc09-113">**Ubuntu**</span></span>
```bash
sudo apt-get update
sudo apt-get install mdadm
```

* <span data-ttu-id="4cc09-114">**CentOS и Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="4cc09-114">**CentOS & Oracle Linux**</span></span>
```bash
sudo yum install mdadm
```

* <span data-ttu-id="4cc09-115">**SLES и openSUSE**</span><span class="sxs-lookup"><span data-stu-id="4cc09-115">**SLES and openSUSE**</span></span>
```bash  
zypper install mdadm
```

## <a name="create-the-disk-partitions"></a><span data-ttu-id="4cc09-116">Создание дисковых разделов</span><span class="sxs-lookup"><span data-stu-id="4cc09-116">Create the disk partitions</span></span>
<span data-ttu-id="4cc09-117">В этом примере мы создаем один дисковый раздел в /dev/sdc.</span><span class="sxs-lookup"><span data-stu-id="4cc09-117">In this example, we create a single disk partition on /dev/sdc.</span></span> <span data-ttu-id="4cc09-118">Новый дисковый раздел будет назван /dev/sdc1.</span><span class="sxs-lookup"><span data-stu-id="4cc09-118">The new disk partition will be called /dev/sdc1.</span></span>

1. <span data-ttu-id="4cc09-119">Запустите `fdisk`, чтобы начать создание разделов:</span><span class="sxs-lookup"><span data-stu-id="4cc09-119">Start `fdisk` to begin creating partitions</span></span>

    ```bash
    sudo fdisk /dev/sdc
    Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
    Building a new DOS disklabel with disk identifier 0xa34cb70c.
    Changes will remain in memory only, until you decide to write them.
    After that, of course, the previous content won't be recoverable.

    WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
                    switch off the mode (command 'c') and change display units to
                    sectors (command 'u').
    ```

2. <span data-ttu-id="4cc09-120">Нажмите клавишу 'n' в командной строке для создания  **n** овый секции:</span><span class="sxs-lookup"><span data-stu-id="4cc09-120">Press 'n' at the prompt to create a **n**ew partition:</span></span>

    ```bash
    Command (m for help): n
    ```

3. <span data-ttu-id="4cc09-121">Далее нажмите «p», чтобы создать основной ( **p**rimary) раздел:</span><span class="sxs-lookup"><span data-stu-id="4cc09-121">Next, press 'p' to create a **p**rimary partition:</span></span>

    ```bash 
    Command action
            e   extended
            p   primary partition (1-4)
    ```

4. <span data-ttu-id="4cc09-122">Нажмите «1», чтобы выбрать номер раздела 1.</span><span class="sxs-lookup"><span data-stu-id="4cc09-122">Press '1' to select partition number 1:</span></span>

    ```bash
    Partition number (1-4): 1
    ```

5. <span data-ttu-id="4cc09-123">Выберите начальную точку нового раздела или нажмите клавишу `<enter>` , чтобы принять значения по умолчанию и поместить раздел в начале свободного пространства на диске:</span><span class="sxs-lookup"><span data-stu-id="4cc09-123">Select the starting point of the new partition, or press `<enter>` to accept the default to place the partition at the beginning of the free space on the drive:</span></span>

    ```bash   
    First cylinder (1-1305, default 1):
    Using default value 1
    ```

6. <span data-ttu-id="4cc09-124">Выберите размер раздела, например, введите «+10G», чтобы создать раздел размером 10 гигабайт.</span><span class="sxs-lookup"><span data-stu-id="4cc09-124">Select the size of the partition, for example type '+10G' to create a 10 gigabyte partition.</span></span> <span data-ttu-id="4cc09-125">Или нажмите клавишу `<enter>` , чтобы создать один раздел, охватывающий весь диск:</span><span class="sxs-lookup"><span data-stu-id="4cc09-125">Or, press `<enter>` create a single partition that spans the entire drive:</span></span>

    ```bash   
    Last cylinder, +cylinders or +size{K,M,G} (1-1305, default 1305): 
    Using default value 1305
    ```

7. <span data-ttu-id="4cc09-126">Далее измените идентификатор и тип ( **t**ype) раздела со значения по умолчанию «83» (Linux) на fd (автоматическое RAID-устройство Linux):</span><span class="sxs-lookup"><span data-stu-id="4cc09-126">Next, change the ID and **t**ype of the partition from the default ID '83' (Linux) to ID 'fd' (Linux raid auto):</span></span>

    ```bash  
    Command (m for help): t
    Selected partition 1
    Hex code (type L to list codes): fd
    ```

8. <span data-ttu-id="4cc09-127">Наконец, запишите таблицу разделов на диск и выйдите из программы fdisk:</span><span class="sxs-lookup"><span data-stu-id="4cc09-127">Finally, write the partition table to the drive and exit fdisk:</span></span>

    ```bash   
    Command (m for help): w
    The partition table has been altered!
    ```

## <a name="create-the-raid-array"></a><span data-ttu-id="4cc09-128">Создание RAID-массива</span><span class="sxs-lookup"><span data-stu-id="4cc09-128">Create the RAID array</span></span>
1. <span data-ttu-id="4cc09-129">В приведенном ниже примере "чередуются" (RAID уровня 0) три раздела, расположенные на трех отдельных дисках данных (sdc1, sdd1, sde1).</span><span class="sxs-lookup"><span data-stu-id="4cc09-129">The following example will "stripe" (RAID level 0) three partitions located on three separate data disks (sdc1, sdd1, sde1).</span></span>  <span data-ttu-id="4cc09-130">После выполнения этой команды будет создано устройство RAID — **/dev/md127** .</span><span class="sxs-lookup"><span data-stu-id="4cc09-130">After running this command a new RAID device called **/dev/md127** is created.</span></span> <span data-ttu-id="4cc09-131">Заметьте также, что если эти диски данных были ранее частью другого RAID-массива, который больше не существует, может потребоваться добавить параметр `--force` в команду `mdadm`.</span><span class="sxs-lookup"><span data-stu-id="4cc09-131">Also note that if these data disks we previously part of another defunct RAID array it may be necessary to add the `--force` parameter to the `mdadm` command:</span></span>

    ```bash  
    sudo mdadm --create /dev/md127 --level 0 --raid-devices 3 \
        /dev/sdc1 /dev/sdd1 /dev/sde1
    ```

2. <span data-ttu-id="4cc09-132">Создайте файловую систему на новом RAID-устройстве.</span><span class="sxs-lookup"><span data-stu-id="4cc09-132">Create the file system on the new RAID device</span></span>
   
    <span data-ttu-id="4cc09-133">а.</span><span class="sxs-lookup"><span data-stu-id="4cc09-133">a.</span></span> <span data-ttu-id="4cc09-134">**CentOS, Oracle Linux, SLES 12, openSUSE и Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="4cc09-134">**CentOS, Oracle Linux, SLES 12, openSUSE, and Ubuntu**</span></span>

    ```bash   
    sudo mkfs -t ext4 /dev/md127
    ```
   
    <span data-ttu-id="4cc09-135">b.</span><span class="sxs-lookup"><span data-stu-id="4cc09-135">b.</span></span> <span data-ttu-id="4cc09-136">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="4cc09-136">**SLES 11**</span></span>

    ```bash
    sudo mkfs -t ext3 /dev/md127
    ```
   
    <span data-ttu-id="4cc09-137">c.</span><span class="sxs-lookup"><span data-stu-id="4cc09-137">c.</span></span> <span data-ttu-id="4cc09-138">**SLES 11** — включите boot.md и создайте mdadm.conf.</span><span class="sxs-lookup"><span data-stu-id="4cc09-138">**SLES 11** - enable boot.md and create mdadm.conf</span></span>

    ```bash
    sudo -i chkconfig --add boot.md
    sudo echo 'DEVICE /dev/sd*[0-9]' >> /etc/mdadm.conf
    ```
   
   > [!NOTE]
   > <span data-ttu-id="4cc09-139">После внесения этих изменений в системах SUSE может потребоваться перезагрузка.</span><span class="sxs-lookup"><span data-stu-id="4cc09-139">A reboot may be required after making these changes on SUSE systems.</span></span> <span data-ttu-id="4cc09-140">Этот шаг *не* является обязательным для SLES 12.</span><span class="sxs-lookup"><span data-stu-id="4cc09-140">This step is *not* required on SLES 12.</span></span>
   > 
   > 

## <a name="add-the-new-file-system-to-etcfstab"></a><span data-ttu-id="4cc09-141">Добавление новой файловой системы в /etc/fstab</span><span class="sxs-lookup"><span data-stu-id="4cc09-141">Add the new file system to /etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4cc09-142">Некорректное изменение файла /etc/fstab может привести к невозможности загрузить систему.</span><span class="sxs-lookup"><span data-stu-id="4cc09-142">Improperly editing the /etc/fstab file could result in an unbootable system.</span></span> <span data-ttu-id="4cc09-143">Если у вас есть сомнения, см. инструкции по правильному изменению этого файла в документации дистрибутива.</span><span class="sxs-lookup"><span data-stu-id="4cc09-143">If unsure, refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="4cc09-144">Также рекомендуется перед внесением изменений создать резервную копию файла /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="4cc09-144">It is also recommended that a backup of the /etc/fstab file is created before editing.</span></span>

1. <span data-ttu-id="4cc09-145">Создайте нужную точку монтирования для новой файловой системы, например:</span><span class="sxs-lookup"><span data-stu-id="4cc09-145">Create the desired mount point for your new file system, for example:</span></span>

    ```bash
    sudo mkdir /data
    ```
2. <span data-ttu-id="4cc09-146">При изменении файла /etc/fstab следует использовать **UUID** для ссылки на файловую систему, а не имя устройства.</span><span class="sxs-lookup"><span data-stu-id="4cc09-146">When editing /etc/fstab, the **UUID** should be used to reference the file system rather than the device name.</span></span>  <span data-ttu-id="4cc09-147">Чтобы определить UUID для новой файловой системы, используйте служебную программу `blkid` .</span><span class="sxs-lookup"><span data-stu-id="4cc09-147">Use the `blkid` utility to determine the UUID for the new file system:</span></span>

    ```bash   
    sudo /sbin/blkid
    ...........
    /dev/md127: UUID="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee" TYPE="ext4"
    ```

3. <span data-ttu-id="4cc09-148">Откройте файл /etc/fstab в текстовом редакторе и добавьте запись для новой файловой системы, например:</span><span class="sxs-lookup"><span data-stu-id="4cc09-148">Open /etc/fstab in a text editor and add an entry for the new file system, for example:</span></span>

    ```bash   
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults  0  2
    ```
   
    <span data-ttu-id="4cc09-149">**SLES 11**:</span><span class="sxs-lookup"><span data-stu-id="4cc09-149">Or on **SLES 11**:</span></span>

    ```bash
    /dev/disk/by-uuid/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext3  defaults  0  2
    ```
   
    <span data-ttu-id="4cc09-150">Затем сохраните и закройте /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="4cc09-150">Then, save and close /etc/fstab.</span></span>

4. <span data-ttu-id="4cc09-151">Проверьте правильность записи в /etc/fstab:</span><span class="sxs-lookup"><span data-stu-id="4cc09-151">Test that the /etc/fstab entry is correct:</span></span>

    ```bash  
    sudo mount -a
    ```

    <span data-ttu-id="4cc09-152">Если в результате выполнения команды появляется сообщение об ошибке, проверьте синтаксис в файле /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="4cc09-152">If this command results in an error message, please check the syntax in the /etc/fstab file.</span></span>
   
    <span data-ttu-id="4cc09-153">Теперь выполните команду `mount` для подключения файловой системы:</span><span class="sxs-lookup"><span data-stu-id="4cc09-153">Next run the `mount` command to ensure the file system is mounted:</span></span>

    ```bash   
    mount
    .................
    /dev/md127 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="4cc09-154">(Необязательно) Параметры загрузки в безопасном режиме</span><span class="sxs-lookup"><span data-stu-id="4cc09-154">(Optional) Failsafe Boot Parameters</span></span>
   
    <span data-ttu-id="4cc09-155">**Конфигурация fstab**</span><span class="sxs-lookup"><span data-stu-id="4cc09-155">**fstab configuration**</span></span>
   
    <span data-ttu-id="4cc09-156">Многие дистрибутивы включают в себя параметры подключения `nobootwait` или `nofail`, которые можно добавить в файл /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="4cc09-156">Many distributions include either the `nobootwait` or `nofail` mount parameters that may be added to the /etc/fstab file.</span></span> <span data-ttu-id="4cc09-157">Эти параметры в случае сбоя при монтировании конкретной файловой системы позволяют системе Linux продолжить загрузку, даже если ей не удается надлежащим образом смонтировать файловую систему RAID.</span><span class="sxs-lookup"><span data-stu-id="4cc09-157">These parameters allow for failures when mounting a particular file system and allow the Linux system to continue to boot even if it is unable to properly mount the RAID file system.</span></span> <span data-ttu-id="4cc09-158">Дополнительные сведения об этих параметрах см. в документации по вашему дистрибутиву.</span><span class="sxs-lookup"><span data-stu-id="4cc09-158">Refer to your distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="4cc09-159">Пример (Ubuntu):</span><span class="sxs-lookup"><span data-stu-id="4cc09-159">Example (Ubuntu):</span></span>

    ```bash  
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,nobootwait  0  2
    ```   

    <span data-ttu-id="4cc09-160">**Параметры загрузки Linux**</span><span class="sxs-lookup"><span data-stu-id="4cc09-160">**Linux boot parameters**</span></span>
   
    <span data-ttu-id="4cc09-161">Помимо приведенных выше параметров, параметр ядра`bootdegraded=true`позволяет системе загружаться, даже если RAID-устройство воспринимается как поврежденное или с пониженной производительностью (например, если диск данных случайно удален с виртуальной машины).</span><span class="sxs-lookup"><span data-stu-id="4cc09-161">In addition to the above parameters, the kernel parameter "`bootdegraded=true`" can allow the system to boot even if the RAID is perceived as damaged or degraded, for example if a data drive is inadvertently removed from the virtual machine.</span></span> <span data-ttu-id="4cc09-162">По умолчанию это может также привести к невозможности загрузки системы.</span><span class="sxs-lookup"><span data-stu-id="4cc09-162">By default this could also result in a non-bootable system.</span></span>
   
    <span data-ttu-id="4cc09-163">Сведения о том, как правильно изменять параметры ядра, см. в документации по вашему дистрибутиву.</span><span class="sxs-lookup"><span data-stu-id="4cc09-163">Please refer to your distribution's documentation on how to properly edit kernel parameters.</span></span> <span data-ttu-id="4cc09-164">Например, во многих дистрибутивах (CentOS, Oracle Linux, SLES 11) эти параметры можно вручную добавить в файл `/boot/grub/menu.lst`.</span><span class="sxs-lookup"><span data-stu-id="4cc09-164">For example, in many distributions (CentOS, Oracle Linux, SLES 11) these parameters may be added manually to the "`/boot/grub/menu.lst`" file.</span></span>  <span data-ttu-id="4cc09-165">В Ubuntu этот параметр можно добавить в переменную `GRUB_CMDLINE_LINUX_DEFAULT` в файле /etc/default/grub.</span><span class="sxs-lookup"><span data-stu-id="4cc09-165">On Ubuntu this parameter can be added to the `GRUB_CMDLINE_LINUX_DEFAULT` variable on "/etc/default/grub".</span></span>


## <a name="trimunmap-support"></a><span data-ttu-id="4cc09-166">Поддержка операций TRIM и UNMAP</span><span class="sxs-lookup"><span data-stu-id="4cc09-166">TRIM/UNMAP support</span></span>
<span data-ttu-id="4cc09-167">Некоторые ядра Linux поддерживают операции TRIM и UNMAP для отмены неиспользуемых блоков на диске.</span><span class="sxs-lookup"><span data-stu-id="4cc09-167">Some Linux kernels support TRIM/UNMAP operations to discard unused blocks on the disk.</span></span> <span data-ttu-id="4cc09-168">Эти операции особенно удобно использовать в хранилище уровня "Стандартный", чтобы сообщать Azure о том, что удаленные страницы больше не действительны и могут быть удалены.</span><span class="sxs-lookup"><span data-stu-id="4cc09-168">These operations are primarily useful in standard storage to inform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="4cc09-169">Удаление страниц позволит сократить затраты, если вы создаете большие файлы, а затем удаляете их.</span><span class="sxs-lookup"><span data-stu-id="4cc09-169">Discarding pages can save cost if you create large files and then delete them.</span></span>

> [!NOTE]
> <span data-ttu-id="4cc09-170">RAID может не выполнять команды отклонения, если значения размера блока для массива меньше заданного значения по умолчанию (512 КБ).</span><span class="sxs-lookup"><span data-stu-id="4cc09-170">RAID may not issue discard commands if the chunk size for the array is set to less than the default (512KB).</span></span> <span data-ttu-id="4cc09-171">Причина в том, что степень детализации программы UNMAP на узле также составляет 512 КБ.</span><span class="sxs-lookup"><span data-stu-id="4cc09-171">This is because the unmap granularity on the Host is also 512KB.</span></span> <span data-ttu-id="4cc09-172">Если вы изменили размер блока массива с помощью параметра mdadm `--chunk=`, то ядро может игнорировать запросы операций TRIM и UNMAP.</span><span class="sxs-lookup"><span data-stu-id="4cc09-172">If you modified the array's chunk size via mdadm's `--chunk=` parameter, then TRIM/unmap requests may be ignored by the kernel.</span></span>

<span data-ttu-id="4cc09-173">Существует два способа включить поддержку операций TRIM в виртуальной машине Linux.</span><span class="sxs-lookup"><span data-stu-id="4cc09-173">There are two ways to enable TRIM support in your Linux VM.</span></span> <span data-ttu-id="4cc09-174">Как обычно, обратитесь к документации дистрибутива, чтобы выбрать рекомендуемый метод.</span><span class="sxs-lookup"><span data-stu-id="4cc09-174">As usual, consult your distribution for the recommended approach:</span></span>

- <span data-ttu-id="4cc09-175">Используйте параметр подключения `discard` в `/etc/fstab`. Ниже приведен пример.</span><span class="sxs-lookup"><span data-stu-id="4cc09-175">Use the `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="4cc09-176">В некоторых случаях параметр `discard` может негативно влиять на производительность.</span><span class="sxs-lookup"><span data-stu-id="4cc09-176">In some cases the `discard` option may have performance implications.</span></span> <span data-ttu-id="4cc09-177">Кроме того, вы можете вручную выполнить команду `fstrim` из командной строки или добавить ее в crontab для регулярного выполнения.</span><span class="sxs-lookup"><span data-stu-id="4cc09-177">Alternatively, you can run the `fstrim` command manually from the command line, or add it to your crontab to run regularly:</span></span>

    <span data-ttu-id="4cc09-178">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="4cc09-178">**Ubuntu**</span></span>

    ```bash
    # sudo apt-get install util-linux
    # sudo fstrim /data
    ```

    <span data-ttu-id="4cc09-179">**RHEL или CentOS**</span><span class="sxs-lookup"><span data-stu-id="4cc09-179">**RHEL/CentOS**</span></span>
    ```bash
    # sudo yum install util-linux
    # sudo fstrim /data
    ```
