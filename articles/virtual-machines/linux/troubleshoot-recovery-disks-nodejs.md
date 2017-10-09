---
title: "aaaUse a Linux, устранение неполадок виртуальной Машины с hello Azure CLI 1.0 | Документы Microsoft"
description: "Узнайте, как tootroubleshoot ВМ Linux проблемы при подключении hello ОС диска tooa восстановления виртуальной Машины с помощью hello Azure CLI 1.0"
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 398f681d1149299d444fcfdab20737315db02855
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-cli-10"></a><span data-ttu-id="28bfe-103">Устранение неполадок виртуальной Машины Linux путем присоединения восстановление tooa диска hello ОС виртуальной Машины с помощью hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="28bfe-103">Troubleshoot a Linux VM by attaching hello OS disk tooa recovery VM using hello Azure CLI 1.0</span></span>
<span data-ttu-id="28bfe-104">Если Linux виртуальной машины (VM), возникает ошибка загрузки или диск, может потребоваться tooperform действия на виртуальном жестком диске hello сам по устранению неполадок.</span><span class="sxs-lookup"><span data-stu-id="28bfe-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="28bfe-105">Распространенным примером будет недопустимую запись в `/etc/fstab` , предотвращает hello виртуальной Машины может tooboot успешно.</span><span class="sxs-lookup"><span data-stu-id="28bfe-105">A common example would be an invalid entry in `/etc/fstab` that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="28bfe-106">Этой статьи описаны как toouse hello Azure CLI 1.0 tooconnect вашего виртуального жесткого диска tooanother toofix ВМ Linux все ошибки, а затем повторного создания исходной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="28bfe-106">This article details how toouse hello Azure CLI 1.0 tooconnect your virtual hard disk tooanother Linux VM toofix any errors, then re-create your original VM.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="28bfe-107">Задача hello toocomplete версии CLI</span><span class="sxs-lookup"><span data-stu-id="28bfe-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="28bfe-108">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="28bfe-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="28bfe-109">[Azure CLI 1.0](#recovery-process-overview) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)</span><span class="sxs-lookup"><span data-stu-id="28bfe-109">[Azure CLI 1.0](#recovery-process-overview) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="28bfe-110">[Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -нашей нового поколения CLI для модели развертывания hello ресурсов управления</span><span class="sxs-lookup"><span data-stu-id="28bfe-110">[Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="28bfe-111">Обзор процесса восстановления</span><span class="sxs-lookup"><span data-stu-id="28bfe-111">Recovery process overview</span></span>
<span data-ttu-id="28bfe-112">Поиск и устранение неполадок Hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="28bfe-112">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="28bfe-113">Удалите hello ВМ возникновения проблемы, поддержание hello виртуальных жестких дисков.</span><span class="sxs-lookup"><span data-stu-id="28bfe-113">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="28bfe-114">Присоедините и подключите tooanother hello виртуальный жесткий диск виртуальной Машины с Linux для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="28bfe-114">Attach and mount hello virtual hard disk tooanother Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="28bfe-115">Подключите toohello Устранение неполадок виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="28bfe-115">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="28bfe-116">Изменение файлов или выполните любые средства toofix проблемы на hello исходный виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="28bfe-116">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="28bfe-117">Отключите образ и отсоединить виртуальный жесткий диск hello из hello, устранение неполадок виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="28bfe-117">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="28bfe-118">Создайте виртуальную Машину с помощью hello исходный виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="28bfe-118">Create a VM using hello original virtual hard disk.</span></span>

<span data-ttu-id="28bfe-119">Убедитесь, что [hello последнюю Azure CLI 1.0](../../cli-install-nodejs.md) установлены и зарегистрированы и использование режима диспетчера ресурсов:</span><span class="sxs-lookup"><span data-stu-id="28bfe-119">Make sure that you have [hello latest Azure CLI 1.0](../../cli-install-nodejs.md) installed and logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="28bfe-120">В hello следующих примерах замените имена параметров собственные значения.</span><span class="sxs-lookup"><span data-stu-id="28bfe-120">In hello following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="28bfe-121">Используемые имена параметров: `myResourceGroup`, `mystorageaccount` и `myVM`.</span><span class="sxs-lookup"><span data-stu-id="28bfe-121">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="28bfe-122">Выявление проблем при загрузке</span><span class="sxs-lookup"><span data-stu-id="28bfe-122">Determine boot issues</span></span>
<span data-ttu-id="28bfe-123">Изучите toodetermine последовательного вывода hello, почему ВМ не могут tooboot правильно.</span><span class="sxs-lookup"><span data-stu-id="28bfe-123">Examine hello serial output toodetermine why your VM is not able tooboot correctly.</span></span> <span data-ttu-id="28bfe-124">Распространенным примером является недопустимой записью в `/etc/fstab`, или hello базового виртуального жесткого диска, удален или перемещен.</span><span class="sxs-lookup"><span data-stu-id="28bfe-124">A common example is an invalid entry in `/etc/fstab`, or hello underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="28bfe-125">Hello следующий пример получает hello последовательного выходные данные из виртуальной Машины с именем hello `myVM` в группе ресурсов hello с именем `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="28bfe-125">hello following example gets hello serial output from hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm get-serial-output --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="28bfe-126">Просмотрите почему hello виртуальной Машины происходит сбой tooboot toodetermine последовательного вывода hello.</span><span class="sxs-lookup"><span data-stu-id="28bfe-126">Review hello serial output toodetermine why hello VM is failing tooboot.</span></span> <span data-ttu-id="28bfe-127">Если последовательного вывода hello не предоставляет сведения о том, может потребоваться tooreview файлы журналов в `/var/log` после hello виртуального жесткого диска, подключенного tooa Устранение неполадок виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="28bfe-127">If hello serial output isn't providing any indication, you may need tooreview log files in `/var/log` once you have hello virtual hard disk connected tooa troubleshooting VM.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="28bfe-128">Просмотр сведений для существующего виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="28bfe-128">View existing virtual hard disk details</span></span>
<span data-ttu-id="28bfe-129">Перед тем как присоединить tooanother вашего виртуального жесткого диска виртуальной Машины, необходимо имя hello tooidentify hello виртуального жесткого диска (VHD).</span><span class="sxs-lookup"><span data-stu-id="28bfe-129">Before you can attach your virtual hard disk tooanother VM, you need tooidentify hello name of hello virtual hard disk (VHD).</span></span> 

<span data-ttu-id="28bfe-130">Hello следующий пример получает сведения для виртуальной Машины с именем hello `myVM` в группе ресурсов hello с именем `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="28bfe-130">hello following example gets information for hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="28bfe-131">Найдите `Vhd URI` в выходных данных hello hello предшествующий команды.</span><span class="sxs-lookup"><span data-stu-id="28bfe-131">Look for `Vhd URI` in hello output from hello preceding command.</span></span> <span data-ttu-id="28bfe-132">Hello примере усеченные выходных данных ниже показаны hello `Vhd URI` на последнюю строку hello:</span><span class="sxs-lookup"><span data-stu-id="28bfe-132">hello following truncated example output shows hello `Vhd URI` on hello last line:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up hello VM "myVM"
+ Looking up hello NIC "myNic"
+ Looking up hello public ip "myPublicIP"
...
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :myVM
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
```


## <a name="delete-existing-vm"></a><span data-ttu-id="28bfe-133">Удаление существующей виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="28bfe-133">Delete existing VM</span></span>
<span data-ttu-id="28bfe-134">Виртуальные жесткие диски и виртуальные машины — это разные ресурсы в Azure.</span><span class="sxs-lookup"><span data-stu-id="28bfe-134">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="28bfe-135">Виртуальный жесткий диск является местом hello операционной системы, приложения и конфигурации.</span><span class="sxs-lookup"><span data-stu-id="28bfe-135">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="28bfe-136">Hello самой ВМ — точно так же метаданные, которые определяет hello размер или расположение и ссылки на ресурсы, такие как виртуальный жесткий диск или виртуальный сетевой адаптер (NIC).</span><span class="sxs-lookup"><span data-stu-id="28bfe-136">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="28bfe-137">Каждый виртуальный жесткий диск содержит аренды, назначенный при присоединении tooa виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="28bfe-137">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="28bfe-138">Несмотря на то, что диски с данными может быть присоединенные и отсоединенные даже в том случае, когда выполняется hello виртуальной Машины, диска ОС hello отключить невозможно, пока удаляется hello ресурса виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="28bfe-138">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="28bfe-139">Аренда Hello продолжается tooassociate hello ОС диска с виртуальной Машиной даже в том случае, если этой виртуальной Машины находится в состоянии остановки и освобождается.</span><span class="sxs-lookup"><span data-stu-id="28bfe-139">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="28bfe-140">Здравствуйте, первый шаг toorecover ВМ — toodelete hello ВМ сам ресурс.</span><span class="sxs-lookup"><span data-stu-id="28bfe-140">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="28bfe-141">Удаление hello ВМ оставляет hello виртуальных жестких дисков в вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="28bfe-141">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="28bfe-142">После hello удаления виртуальной Машины присоединения hello виртуальный жесткий диск tooanother ВМ tootroubleshoot и устранение ошибок hello.</span><span class="sxs-lookup"><span data-stu-id="28bfe-142">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="28bfe-143">Следующий пример удаляет Hello hello виртуальной Машины с именем `myVM` из группы ресурсов hello с именем `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="28bfe-143">hello following example deletes hello VM named `myVM` from hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm delete --resource-group myResourceGroup --name myVM 
```

<span data-ttu-id="28bfe-144">Подождите, пока hello ВМ закончит удаление перед присоединением tooanother hello виртуальный жесткий диск виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="28bfe-144">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="28bfe-145">Аренда Hello hello виртуальный жесткий диск, который связывает его с hello виртуальной Машины должен toobe выпуска перед тем как присоединить tooanother hello виртуальный жесткий диск виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="28bfe-145">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="28bfe-146">Подключить существующий виртуальный жесткий диск tooanother виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="28bfe-146">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="28bfe-147">Для Здравствуйте рядом шагах, для устранения неполадок используется другой виртуальной Машиной.</span><span class="sxs-lookup"><span data-stu-id="28bfe-147">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="28bfe-148">Подключить существующий виртуальный жесткий диск toothis hello Устранение неполадок виртуальной Машины toobrowse и изменить содержимое диска hello.</span><span class="sxs-lookup"><span data-stu-id="28bfe-148">You attach hello existing virtual hard disk toothis troubleshooting VM toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="28bfe-149">Этот процесс позволяет toocorrect все ошибки конфигурации или Просмотр дополнительных приложений или файлы журналов, например системы.</span><span class="sxs-lookup"><span data-stu-id="28bfe-149">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="28bfe-150">Выберите или создайте другой toouse виртуальной Машины для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="28bfe-150">Choose or create another VM toouse for troubleshooting purposes.</span></span>

<span data-ttu-id="28bfe-151">При присоединении hello существующий виртуальный жесткий диск, укажите диск toohello hello URL-адрес, полученный на предыдущем hello `azure vm show` команды.</span><span class="sxs-lookup"><span data-stu-id="28bfe-151">When you attach hello existing virtual hard disk, specify hello URL toohello disk obtained in hello preceding `azure vm show` command.</span></span> <span data-ttu-id="28bfe-152">Hello примере присоединяет существующий виртуальный жесткий диск toohello Устранение неполадок виртуальной Машины с именем `myVMRecovery` в группе ресурсов hello с именем `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="28bfe-152">hello following example attaches an existing virtual hard disk toohello troubleshooting VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm disk attach --resource-group myResourceGroup --name myVMRecovery \
    --vhd-url https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="28bfe-153">Подключить hello подключенный диск данных</span><span class="sxs-lookup"><span data-stu-id="28bfe-153">Mount hello attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="28bfe-154">Hello следующих примерах приведены шаги на Виртуальной машине Ubuntu hello.</span><span class="sxs-lookup"><span data-stu-id="28bfe-154">hello following examples detail hello steps required on an Ubuntu VM.</span></span> <span data-ttu-id="28bfe-155">Если вы используете другой дистрибутив Linux, например Red Hat Enterprise Linux или SUSE, hello расположения файлов журнала и `mount` команд может немного отличаться.</span><span class="sxs-lookup"><span data-stu-id="28bfe-155">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, hello log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="28bfe-156">См. в документации toohello для вашего конкретного дистрибутив для hello соответствующие изменения в командах.</span><span class="sxs-lookup"><span data-stu-id="28bfe-156">Refer toohello documentation for your specific distro for hello appropriate changes in commands.</span></span>

1. <span data-ttu-id="28bfe-157">Устранение неполадок виртуальной Машины, используя соответствующие учетные данные hello tooyour SSH.</span><span class="sxs-lookup"><span data-stu-id="28bfe-157">SSH tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="28bfe-158">Если этот диск является tooyour данных диске, подключенном hello для первого Устранение неполадок виртуальной Машины, hello подключен жесткий диск, скорее всего слишком`/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="28bfe-158">If this disk is hello first data disk attached tooyour troubleshooting VM, hello disk is likely connected too`/dev/sdc`.</span></span> <span data-ttu-id="28bfe-159">Используйте `dmseg` tooview присоединенных дисков:</span><span class="sxs-lookup"><span data-stu-id="28bfe-159">Use `dmseg` tooview attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```

    <span data-ttu-id="28bfe-160">Hello вывода будет примерно toohello следующий пример:</span><span class="sxs-lookup"><span data-stu-id="28bfe-160">hello output is similar toohello following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="28bfe-161">В предыдущих пример hello, диск hello ОС находится на `/dev/sda` и hello временного диска, указанное для каждой виртуальной Машины в `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="28bfe-161">In hello preceding example, hello OS disk is at `/dev/sda` and hello temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="28bfe-162">Если у вас несколько дисков данных, они будут присоединены как `/dev/sdd`, `/dev/sde` и т. д.</span><span class="sxs-lookup"><span data-stu-id="28bfe-162">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="28bfe-163">Создайте directory toomount существующий виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="28bfe-163">Create a directory toomount your existing virtual hard disk.</span></span> <span data-ttu-id="28bfe-164">Hello следующий пример создает каталог с именем `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="28bfe-164">hello following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="28bfe-165">При наличии нескольких секций на существующий виртуальный жесткий диск, подключите hello необходимые секции.</span><span class="sxs-lookup"><span data-stu-id="28bfe-165">If you have multiple partitions on your existing virtual hard disk, mount hello required partition.</span></span> <span data-ttu-id="28bfe-166">Hello следующий пример подключает первому основному разделу hello в `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="28bfe-166">hello following example mounts hello first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="28bfe-167">Лучший способ — что toomount диски с данными на виртуальных машинах в Azure с помощью hello универсальный уникальный идентификатор UUID hello виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="28bfe-167">Best practice is toomount data disks on VMs in Azure using hello universally unique identifier (UUID) of hello virtual hard disk.</span></span> <span data-ttu-id="28bfe-168">В этом сценарии короткий по устранению неполадок монтажного hello виртуального жесткого диска с помощью hello UUID не требуется.</span><span class="sxs-lookup"><span data-stu-id="28bfe-168">For this short troubleshooting scenario, mounting hello virtual hard disk using hello UUID is not necessary.</span></span> <span data-ttu-id="28bfe-169">Тем не менее, при обычных условиях использования редактирования `/etc/fstab` toomount виртуальных жестких дисков с помощью имени, а не может вызвать UUID hello tooboot toofail виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="28bfe-169">However, under normal use, editing `/etc/fstab` toomount virtual hard disks using device name rather than UUID may cause hello VM toofail tooboot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="28bfe-170">Устранение неполадок на исходном виртуальном жестком диске</span><span class="sxs-lookup"><span data-stu-id="28bfe-170">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="28bfe-171">С hello существующий виртуальный жесткий диск подключен теперь можно выполнять обслуживание и действия по устранению неполадок при необходимости.</span><span class="sxs-lookup"><span data-stu-id="28bfe-171">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="28bfe-172">После разрешения проблемы hello продолжите hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="28bfe-172">Once you have addressed hello issues, continue with hello following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="28bfe-173">Отключение и отсоединение исходного виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="28bfe-173">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="28bfe-174">После разрешения ошибки, можно отключить и отсоединение hello существующий виртуальный жесткий диск от виртуальной Машины по устранению неполадок.</span><span class="sxs-lookup"><span data-stu-id="28bfe-174">Once your errors are resolved, you unmount and detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="28bfe-175">Расположение виртуального жесткого диска нельзя использовать с любой другой ВМ до освобождения аренды hello присоединение toohello hello виртуального жесткого диска, устранение неполадок виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="28bfe-175">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="28bfe-176">Из сеанса SSH hello tooyour Устранение неполадок виртуальной Машины отключите hello существующий виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="28bfe-176">From hello SSH session tooyour troubleshooting VM, unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="28bfe-177">Сначала измените вне hello родительский каталог для точки подключения:</span><span class="sxs-lookup"><span data-stu-id="28bfe-177">Change out of hello parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="28bfe-178">Теперь отключите hello существующий виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="28bfe-178">Now unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="28bfe-179">Hello следующий пример отсоединяет диск hello устройство с `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="28bfe-179">hello following example unmounts hello device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="28bfe-180">Теперь отсоедините hello виртуальный жесткий диск из виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="28bfe-180">Now detach hello virtual hard disk from hello VM.</span></span> <span data-ttu-id="28bfe-181">Выйти из сеанса tooyour hello SSH, устранение неполадок виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="28bfe-181">Exit hello SSH session tooyour troubleshooting VM.</span></span> <span data-ttu-id="28bfe-182">В hello Azure CLI первый список hello подключен tooyour дисков данных, устранение неполадок виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="28bfe-182">In hello Azure CLI, first list hello attached data disks tooyour troubleshooting VM.</span></span> <span data-ttu-id="28bfe-183">Hello списки hello диски с данными в примере присоединенного toohello виртуальной Машины с именем `myVMRecovery` в группе ресурсов hello с именем `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="28bfe-183">hello following example lists hello data disks attached toohello VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    azure vm disk list --resource-group myResourceGroup --vm-name myVMRecovery
    ```

    <span data-ttu-id="28bfe-184">Примечание hello `Lun` значение для существующего виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="28bfe-184">Note hello `Lun` value for your existing virtual hard disk.</span></span> <span data-ttu-id="28bfe-185">Hello команду в следующем примере вывод содержит hello существующий виртуальный диск в LUN 0:</span><span class="sxs-lookup"><span data-stu-id="28bfe-185">hello following example command output shows hello existing virtual disk attached at LUN 0:</span></span>

    ```azurecli
    info:    Executing command vm disk list
    + Looking up hello VM "myVMRecovery"
    data:    Name              Lun  DiskSizeGB  Caching  URI
    data:    ------            ---  ----------  -------  ------------------------------------------------------------------------
    data:    myVM              0                None     https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    info:    vm disk list command OK
    ```

    <span data-ttu-id="28bfe-186">Отсоединить диск данных hello от виртуальной Машины с помощью hello применимо `Lun` значение:</span><span class="sxs-lookup"><span data-stu-id="28bfe-186">Detach hello data disk from your VM using hello applicable `Lun` value:</span></span>

    ```azurecli
    azure vm disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --lun 0
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="28bfe-187">Создание виртуальной машины из исходного жесткого диска</span><span class="sxs-lookup"><span data-stu-id="28bfe-187">Create VM from original hard disk</span></span>
<span data-ttu-id="28bfe-188">использовать ВМ с исходного виртуального жесткого диска, toocreate [этого шаблона Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="28bfe-188">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span></span> <span data-ttu-id="28bfe-189">шаблон фактического JSON Hello находится в hello по ссылке:</span><span class="sxs-lookup"><span data-stu-id="28bfe-189">hello actual JSON template is at hello following link:</span></span>

- <span data-ttu-id="28bfe-190">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="28bfe-190">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span></span>

<span data-ttu-id="28bfe-191">шаблон Hello развертывания ВМ в существующей виртуальной сети, с помощью hello URL-адрес VHD из hello ранее команд.</span><span class="sxs-lookup"><span data-stu-id="28bfe-191">hello template deploys a VM into an existing virtual network, using hello VHD URL from hello earlier command.</span></span> <span data-ttu-id="28bfe-192">Hello примере развертывает hello шаблона toohello ресурсов группы с именем `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="28bfe-192">hello following example deploys hello template toohello resource group named `myResourceGroup`:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup --name myDeployment \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

<span data-ttu-id="28bfe-193">Hello ответов запрашивает hello шаблона, например имя виртуальной Машины (`myDeployedVM` hello в следующем примере), тип операционной системы (`Linux`) и размер виртуальной Машины (`Standard_DS1_v2`).</span><span class="sxs-lookup"><span data-stu-id="28bfe-193">Answer hello prompts for hello template such as VM name (`myDeployedVM` hello following example), OS type (`Linux`), and VM size (`Standard_DS1_v2`).</span></span> <span data-ttu-id="28bfe-194">Hello `osDiskVhdUri` Здравствуйте, же, как уже используется при присоединении hello существующий виртуальный жесткий диск toohello Устранение неполадок виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="28bfe-194">hello `osDiskVhdUri` is hello same as previously used when attaching hello existing virtual hard disk toohello troubleshooting VM.</span></span> <span data-ttu-id="28bfe-195">Пример выходных данных команды hello и запрос выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="28bfe-195">An example of hello command output and prompts is as follows:</span></span>

```azurecli
info:    Executing command group deployment create
info:    Supply values for hello following parameters
vmName:  myDeployedVM
osType:  Linux
osDiskVhdUri:  https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
vmSize:  Standard_DS1_v2
existingVirtualNetworkName:  myVnet
existingVirtualNetworkResourceGroup:  myResourceGroup
subnetName:  mySubnet
dnsNameForPublicIP:  mypublicipdeployed
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "mydeployment"
+ Waiting for deployment toocomplete
+
```


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="28bfe-196">Восстановление диагностики загрузки</span><span class="sxs-lookup"><span data-stu-id="28bfe-196">Re-enable boot diagnostics</span></span>

<span data-ttu-id="28bfe-197">При создании ВМ из hello существующий виртуальный жесткий диск, диагностика загрузки может не быть доступной.</span><span class="sxs-lookup"><span data-stu-id="28bfe-197">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="28bfe-198">Hello следующий пример включает hello диагностического расширения для виртуальной Машины с именем hello `myDeployedVM` в группе ресурсов hello с именем `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="28bfe-198">hello following example enables hello diagnostic extension on hello VM named `myDeployedVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm enable-diag --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a><span data-ttu-id="28bfe-199">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="28bfe-199">Next steps</span></span>
<span data-ttu-id="28bfe-200">Если возникают проблемы с подключением tooyour виртуальной Машины, см. раздел [Устранение SSH подключений tooan виртуальной Машины Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="28bfe-200">If you are having issues connecting tooyour VM, see [Troubleshoot SSH connections tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="28bfe-201">Для решения проблем с доступом к приложениям, выполняющимся на виртуальной машине, см. статью [Устранение проблем с подключением к приложениям на виртуальных машинах Linux в Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="28bfe-201">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
