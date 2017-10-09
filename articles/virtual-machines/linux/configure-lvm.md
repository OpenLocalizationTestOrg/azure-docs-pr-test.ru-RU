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
# <a name="configure-lvm-on-a-linux-vm-in-azure"></a><span data-ttu-id="2f3c1-103">Настройка диспетчера логических томов на виртуальной машине Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="2f3c1-103">Configure LVM on a Linux VM in Azure</span></span>
<span data-ttu-id="2f3c1-104">В этом документе будут рассматриваться как tooconfigure диспетчер логических томов (LVM) на виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-104">This document will discuss how tooconfigure Logical Volume Manager (LVM) in your Azure virtual machine.</span></span> <span data-ttu-id="2f3c1-105">Хотя и существует нецелесообразно tooconfigure LVM на любом диске присоединенного toohello виртуальной машины, по умолчанию большинство облаку изображений не будет LVM настроен на hello диска ОС.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-105">While it is feasible tooconfigure LVM on any disk attached toohello virtual machine, by default most cloud images will not have LVM configured on hello OS disk.</span></span> <span data-ttu-id="2f3c1-106">Это tooprevent проблем с группами повторяющиеся тома, если диск ОС-нибудь hello присоединенного tooanother виртуальная машина hello одинаковое распределение и тип, т. е. во время восстановления.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-106">This is tooprevent problems with duplicate volume groups if hello OS disk is ever attached tooanother VM of hello same distribution and type, i.e. during a recovery scenario.</span></span> <span data-ttu-id="2f3c1-107">Поэтому рекомендуется только toouse LVM на дисках данных hello.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-107">Therefore it is recommended only toouse LVM on hello data disks.</span></span>

## <a name="linear-vs-striped-logical-volumes"></a><span data-ttu-id="2f3c1-108">Линейные и чередующиеся логические тома</span><span class="sxs-lookup"><span data-stu-id="2f3c1-108">Linear vs. striped logical volumes</span></span>
<span data-ttu-id="2f3c1-109">LVM может быть используется toocombine количество физических дисков в одному тому хранилища.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-109">LVM can be used toocombine a number of physical disks into a single storage volume.</span></span> <span data-ttu-id="2f3c1-110">По умолчанию LVM обычно создаст линейной логических томах, что означает физическое хранилище hello соединенных вместе.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-110">By default LVM will usually create linear logical volumes, which means that hello physical storage is concatenated together.</span></span> <span data-ttu-id="2f3c1-111">В этом случае операции чтения и записи будет обычно отправляться только одного диска tooa.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-111">In this case read/write operations will typically only be sent tooa single disk.</span></span> <span data-ttu-id="2f3c1-112">В отличие от этого, мы также чередующиеся тома могут создаваться логических операций чтения и записи в которых распределенных toomultiple дисков в группе томов hello (т. е. аналогично tooRAID0).</span><span class="sxs-lookup"><span data-stu-id="2f3c1-112">In contrast, we can also create striped logical volumes where reads and writes are distributed toomultiple disks contained in hello volume group (i.e. similar tooRAID0).</span></span> <span data-ttu-id="2f3c1-113">Для повышения производительности, скорее всего, вы будете toostripe логических томов, чтобы операции чтения и записи используют все диски данных.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-113">For performance reasons it is likely you will want toostripe your logical volumes so that reads and writes utilize all your attached data disks.</span></span>

<span data-ttu-id="2f3c1-114">В этом документе описаны как toocombine данные за несколько дисков в одну группу томов и затем создать чередующийся том логического.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-114">This document will describe how toocombine several data disks into a single volume group, and then create a striped logical volume.</span></span> <span data-ttu-id="2f3c1-115">Hello шаги будут немного обобщенный toowork с большинством дистрибутивов.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-115">hello steps below are somewhat generalized toowork with most distributions.</span></span> <span data-ttu-id="2f3c1-116">В большинстве случаев hello служебные программы и рабочие процессы для управления LVM в Azure не отличаются фундаментально от других сред.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-116">In most cases hello utilities and workflows for managing LVM on Azure are not fundamentally different than other environments.</span></span> <span data-ttu-id="2f3c1-117">Для получения дополнительных сведений и рекомендаций по использованию диспетчера логических томов с вашим дистрибутивом обратитесь к поставщику Linux.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-117">As usual, please also consult your Linux vendor for documentation and best practices for using LVM with your particular distribution.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="2f3c1-118">Присоединение дисков данных</span><span class="sxs-lookup"><span data-stu-id="2f3c1-118">Attaching data disks</span></span>
<span data-ttu-id="2f3c1-119">Один часто будут toostart с двумя или более пустые диски для данных при использовании LVM.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-119">One will usually want toostart with two or more empty data disks when using LVM.</span></span> <span data-ttu-id="2f3c1-120">Исходя из потребностей операции ввода-ВЫВОДА, вы можете tooattach дисков, которые хранятся в нашем стандартное хранилище с вверх too500 операции ввода-ВЫВОДА/ps на диск или дисковое нашей Premium с вверх too5000 операции ввода-ВЫВОДА/ps на одном диске.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-120">Based on your IO needs, you can choose tooattach disks that are stored in our Standard Storage, with up too500 IO/ps per disk or our Premium storage with up too5000 IO/ps per disk.</span></span> <span data-ttu-id="2f3c1-121">В этой статье будет подробно не о том, как tooprovision и присоединения виртуальной машины Linux tooa данных дисков.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-121">This article will not go into detail on how tooprovision and attach data disks tooa Linux virtual machine.</span></span> <span data-ttu-id="2f3c1-122">См. в разделе статьи Microsoft Azure hello [подключить диск](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) подробные инструкции по как tooattach пустые данные на диске tooa Linux виртуальной машины в Azure.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-122">Please see hello Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how tooattach an empty data disk tooa Linux virtual machine on Azure.</span></span>

## <a name="install-hello-lvm-utilities"></a><span data-ttu-id="2f3c1-123">Установите служебные программы LVM hello</span><span class="sxs-lookup"><span data-stu-id="2f3c1-123">Install hello LVM utilities</span></span>
* <span data-ttu-id="2f3c1-124">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="2f3c1-124">**Ubuntu**</span></span>

    ```bash  
    sudo apt-get update
    sudo apt-get install lvm2
    ```

* <span data-ttu-id="2f3c1-125">**RHEL, CentOS и Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="2f3c1-125">**RHEL, CentOS & Oracle Linux**</span></span>

    ```bash   
    sudo yum install lvm2
    ```

* <span data-ttu-id="2f3c1-126">**SLES 12 и openSUSE**</span><span class="sxs-lookup"><span data-stu-id="2f3c1-126">**SLES 12 and openSUSE**</span></span>

    ```bash   
    sudo zypper install lvm2
    ```

* <span data-ttu-id="2f3c1-127">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="2f3c1-127">**SLES 11**</span></span>

    ```bash   
    sudo zypper install lvm2
    ```

    <span data-ttu-id="2f3c1-128">На SLES11 необходимо также изменить `/etc/sysconfig/lvm` и задайте `LVM_ACTIVATED_ON_DISCOVERED` слишком «включить»:</span><span class="sxs-lookup"><span data-stu-id="2f3c1-128">On SLES11 you must also edit `/etc/sysconfig/lvm` and set `LVM_ACTIVATED_ON_DISCOVERED` too"enable":</span></span>

    ```sh   
    LVM_ACTIVATED_ON_DISCOVERED="enable" 
    ```

## <a name="configure-lvm"></a><span data-ttu-id="2f3c1-129">Настройка диспетчера логических томов</span><span class="sxs-lookup"><span data-stu-id="2f3c1-129">Configure LVM</span></span>
<span data-ttu-id="2f3c1-130">В этом руководстве предполагается, вы привязали три диски с данными, которые мы будем называть tooas `/dev/sdc`, `/dev/sdd` и `/dev/sde`.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-130">In this guide we will assume you have attached three data disks, which we'll refer tooas `/dev/sdc`, `/dev/sdd` and `/dev/sde`.</span></span> <span data-ttu-id="2f3c1-131">Обратите внимание, что они могут не всегда быть hello же пути на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-131">Note that these may not always be hello same path names in your VM.</span></span> <span data-ttu-id="2f3c1-132">Можно запустить "`sudo fdisk -l`" или аналогичную команду toolist доступных дисков.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-132">You can run '`sudo fdisk -l`' or similar command toolist your available disks.</span></span>

1. <span data-ttu-id="2f3c1-133">Подготовка физических томов hello.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-133">Prepare hello physical volumes:</span></span>

    ```bash    
    sudo pvcreate /dev/sd[cde]
    Physical volume "/dev/sdc" successfully created
    Physical volume "/dev/sdd" successfully created
    Physical volume "/dev/sde" successfully created
    ```

2. <span data-ttu-id="2f3c1-134">Создайте группу томов.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-134">Create a volume group.</span></span> <span data-ttu-id="2f3c1-135">В этом примере мы вызов группы томов hello `data-vg01`:</span><span class="sxs-lookup"><span data-stu-id="2f3c1-135">In this example we are calling hello volume group `data-vg01`:</span></span>

    ```bash    
    sudo vgcreate data-vg01 /dev/sd[cde]
    Volume group "data-vg01" successfully created
    ```

3. <span data-ttu-id="2f3c1-136">Создание логических томов hello.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-136">Create hello logical volume(s).</span></span> <span data-ttu-id="2f3c1-137">Hello команда ниже мы создает один логический том вызове `data-lv01` toospan hello весь том группы, но Обратите внимание, что также нецелесообразно toocreate несколько логических томов в группы томов hello.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-137">hello command below we will create a single logical volume called `data-lv01` toospan hello entire volume group, but note that it is also feasible toocreate multiple logical volumes in hello volume group.</span></span>

    ```bash   
    sudo lvcreate --extents 100%FREE --stripes 3 --name data-lv01 data-vg01
    Logical volume "data-lv01" created.
    ```

4. <span data-ttu-id="2f3c1-138">Логический том формате hello</span><span class="sxs-lookup"><span data-stu-id="2f3c1-138">Format hello logical volume</span></span>

    ```bash  
    sudo mkfs -t ext4 /dev/data-vg01/data-lv01
    ```
   
   > [!NOTE]
   > <span data-ttu-id="2f3c1-139">Для SLES11 замените ext4 на `-t ext3`.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-139">With SLES11 use `-t ext3` instead of ext4.</span></span> <span data-ttu-id="2f3c1-140">SLES11 поддерживает только файловые системы tooext4 доступ только для чтения.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-140">SLES11 only supports read-only access tooext4 filesystems.</span></span>

## <a name="add-hello-new-file-system-tooetcfstab"></a><span data-ttu-id="2f3c1-141">Добавить hello новый файл system слишком/и т. д/fstab</span><span class="sxs-lookup"><span data-stu-id="2f3c1-141">Add hello new file system too/etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2f3c1-142">Неправильное редактирование hello `/etc/fstab` файла может привести к невозможности загрузки системы.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-142">Improperly editing hello `/etc/fstab` file could result in an unbootable system.</span></span> <span data-ttu-id="2f3c1-143">Если нет уверенности, см. документацию распространения toohello сведения о как tooproperly изменять этот файл.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-143">If unsure, please refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="2f3c1-144">Также рекомендуется, чтобы резервная копия hello `/etc/fstab` создается файл, прежде чем изменять.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-144">It is also recommended that a backup of hello `/etc/fstab` file is created before editing.</span></span>

1. <span data-ttu-id="2f3c1-145">Создайте точку подключения hello требуемого для новой файловой системы, например:</span><span class="sxs-lookup"><span data-stu-id="2f3c1-145">Create hello desired mount point for your new file system, for example:</span></span>

    ```bash  
    sudo mkdir /data
    ```

2. <span data-ttu-id="2f3c1-146">Найти путь логический том hello</span><span class="sxs-lookup"><span data-stu-id="2f3c1-146">Locate hello logical volume path</span></span>

    ```bash    
    lvdisplay
    --- Logical volume ---
    LV Path                /dev/data-vg01/data-lv01
    ....
    ```

3. <span data-ttu-id="2f3c1-147">Откройте `/etc/fstab` в текстовом редакторе и добавьте запись для hello новой файловой системы, например:</span><span class="sxs-lookup"><span data-stu-id="2f3c1-147">Open `/etc/fstab` in a text editor and add an entry for hello new file system, for example:</span></span>

    ```bash    
    /dev/data-vg01/data-lv01  /data  ext4  defaults  0  2
    ```   
    <span data-ttu-id="2f3c1-148">Затем сохраните и закройте `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-148">Then, save and close `/etc/fstab`.</span></span>

4. <span data-ttu-id="2f3c1-149">Тестирование этого hello `/etc/fstab` правильности введенных:</span><span class="sxs-lookup"><span data-stu-id="2f3c1-149">Test that hello `/etc/fstab` entry is correct:</span></span>

    ```bash    
    sudo mount -a
    ```

    <span data-ttu-id="2f3c1-150">Если эта команда приведет к сообщение об ошибке, Проверьте синтаксис hello в hello `/etc/fstab` файла.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-150">If this command results in an error message please check hello syntax in hello `/etc/fstab` file.</span></span>
   
    <span data-ttu-id="2f3c1-151">Далее выполните hello `mount` подключения команда tooensure hello файловой системы:</span><span class="sxs-lookup"><span data-stu-id="2f3c1-151">Next run hello `mount` command tooensure hello file system is mounted:</span></span>

    ```bash    
    mount
    ......
    /dev/mapper/data--vg01-data--lv01 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="2f3c1-152">(Необязательно) Параметры загрузки, предотвращающие сбой, в файле `/etc/fstab`</span><span class="sxs-lookup"><span data-stu-id="2f3c1-152">(Optional) Failsafe boot parameters in `/etc/fstab`</span></span>
   
    <span data-ttu-id="2f3c1-153">Большинство установок включают либо hello `nobootwait` или `nofail` подключения параметры, которые могут быть добавлены toohello `/etc/fstab` файл.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-153">Many distributions include either hello `nobootwait` or `nofail` mount parameters that may be added toohello `/etc/fstab` file.</span></span> <span data-ttu-id="2f3c1-154">Эти параметры для сбоев при монтировании определенной файловой системы и выполнение tooboot toocontinue системы Linux hello даже если это не удается tooproperly подключения hello RAID файловой системы.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-154">These parameters allow for failures when mounting a particular file system and allow hello Linux system toocontinue tooboot even if it is unable tooproperly mount hello RAID file system.</span></span> <span data-ttu-id="2f3c1-155">Дополнительные сведения об этих параметрах см. документацию tooyour распространения.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-155">Please refer tooyour distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="2f3c1-156">Пример (Ubuntu):</span><span class="sxs-lookup"><span data-stu-id="2f3c1-156">Example (Ubuntu):</span></span>

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,nobootwait  0  2
    ```

## <a name="trimunmap-support"></a><span data-ttu-id="2f3c1-157">Поддержка операций TRIM и UNMAP</span><span class="sxs-lookup"><span data-stu-id="2f3c1-157">TRIM/UNMAP support</span></span>
<span data-ttu-id="2f3c1-158">Некоторые версии Linux ядра поддержки TRIM и отмене СОПОСТАВЛЕНИЯ операций toodiscard неиспользуемые блоки на диске hello.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-158">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="2f3c1-159">Эти операции, в первую очередь используются в tooinform стандартное хранилище Azure, которая удалена страницы становятся недействительными и может быть удален.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-159">These operations are primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="2f3c1-160">Удаление страниц позволит сократить затраты, если вы создаете большие файлы, а затем удаляете их.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-160">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="2f3c1-161">Существует два способа tooenable TRIM поддержки в ВМ Linux.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-161">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="2f3c1-162">Как обычно см. на распределение hello рекомендованный подход:</span><span class="sxs-lookup"><span data-stu-id="2f3c1-162">As usual, consult your distribution for hello recommended approach:</span></span>

- <span data-ttu-id="2f3c1-163">Используйте hello `discard` подключить параметр в `/etc/fstab`, например:</span><span class="sxs-lookup"><span data-stu-id="2f3c1-163">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="2f3c1-164">В некоторых случаях hello `discard` параметра может негативно сказаться на производительности.</span><span class="sxs-lookup"><span data-stu-id="2f3c1-164">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="2f3c1-165">Кроме того, можно запустить hello `fstrim` вручную команды из командной строки hello, или добавьте его tooyour crontab toorun регулярно:</span><span class="sxs-lookup"><span data-stu-id="2f3c1-165">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>

    <span data-ttu-id="2f3c1-166">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="2f3c1-166">**Ubuntu**</span></span>

    ```bash 
    # sudo apt-get install util-linux
    # sudo fstrim /datadrive
    ```

    <span data-ttu-id="2f3c1-167">**RHEL или CentOS**</span><span class="sxs-lookup"><span data-stu-id="2f3c1-167">**RHEL/CentOS**</span></span>

    ```bash 
    # sudo yum install util-linux
    # sudo fstrim /datadrive
    ```
