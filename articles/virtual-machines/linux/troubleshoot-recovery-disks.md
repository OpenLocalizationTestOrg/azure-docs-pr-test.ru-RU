---
title: "aaaUse a Linux, устранение неполадок виртуальной Машины с hello Azure CLI 2.0 | Документы Microsoft"
description: "Узнайте, как tootroubleshoot ВМ Linux проблемы при подключении hello ОС диска tooa восстановления виртуальной Машины с помощью hello Azure CLI 2.0"
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/16/2017
ms.author: iainfou
ms.openlocfilehash: 776d61b61280f46e3699157addcdb1e7dfb6818e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-with-hello-azure-cli-20"></a><span data-ttu-id="5bd59-103">Устранение неполадок виртуальной Машины Linux путем присоединения диска hello ОС tooa восстановления виртуальной Машины с hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5bd59-103">Troubleshoot a Linux VM by attaching hello OS disk tooa recovery VM with hello Azure CLI 2.0</span></span>
<span data-ttu-id="5bd59-104">Если Linux виртуальной машины (VM), возникает ошибка загрузки или диск, может потребоваться tooperform действия на виртуальном жестком диске hello сам по устранению неполадок.</span><span class="sxs-lookup"><span data-stu-id="5bd59-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="5bd59-105">Распространенным примером будет недопустимую запись в `/etc/fstab` , предотвращает hello виртуальной Машины может tooboot успешно.</span><span class="sxs-lookup"><span data-stu-id="5bd59-105">A common example would be an invalid entry in `/etc/fstab` that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="5bd59-106">Этой статьи описаны как toouse hello Azure CLI 2.0 tooconnect вашего виртуального жесткого диска tooanother toofix ВМ Linux все ошибки, а затем повторного создания исходной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5bd59-106">This article details how toouse hello Azure CLI 2.0 tooconnect your virtual hard disk tooanother Linux VM toofix any errors, then re-create your original VM.</span></span> <span data-ttu-id="5bd59-107">Можно также выполнить следующие действия с hello [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5bd59-107">You can also perform these steps with hello [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="5bd59-108">Обзор процесса восстановления</span><span class="sxs-lookup"><span data-stu-id="5bd59-108">Recovery process overview</span></span>
<span data-ttu-id="5bd59-109">Поиск и устранение неполадок Hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5bd59-109">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="5bd59-110">Удалите hello ВМ возникновения проблемы, поддержание hello виртуальных жестких дисков.</span><span class="sxs-lookup"><span data-stu-id="5bd59-110">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="5bd59-111">Присоедините и подключите tooanother hello виртуальный жесткий диск виртуальной Машины с Linux для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="5bd59-111">Attach and mount hello virtual hard disk tooanother Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="5bd59-112">Подключите toohello Устранение неполадок виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5bd59-112">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="5bd59-113">Изменение файлов или выполните любые средства toofix проблемы на hello исходный виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="5bd59-113">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="5bd59-114">Отключите образ и отсоединить виртуальный жесткий диск hello из hello, устранение неполадок виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5bd59-114">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="5bd59-115">Создайте виртуальную Машину с помощью hello исходный виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="5bd59-115">Create a VM using hello original virtual hard disk.</span></span>

<span data-ttu-id="5bd59-116">tooperform следующие шаги, hello требуется последняя версия [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="5bd59-116">tooperform these troubleshooting steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="5bd59-117">В hello следующих примерах замените имена параметров собственные значения.</span><span class="sxs-lookup"><span data-stu-id="5bd59-117">In hello following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="5bd59-118">Используемые имена параметров: `myResourceGroup`, `mystorageaccount` и `myVM`.</span><span class="sxs-lookup"><span data-stu-id="5bd59-118">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="5bd59-119">Выявление проблем при загрузке</span><span class="sxs-lookup"><span data-stu-id="5bd59-119">Determine boot issues</span></span>
<span data-ttu-id="5bd59-120">Изучите toodetermine последовательного вывода hello, почему ВМ не могут tooboot правильно.</span><span class="sxs-lookup"><span data-stu-id="5bd59-120">Examine hello serial output toodetermine why your VM is not able tooboot correctly.</span></span> <span data-ttu-id="5bd59-121">Распространенным примером является недопустимой записью в `/etc/fstab`, или hello базового виртуального жесткого диска, удален или перемещен.</span><span class="sxs-lookup"><span data-stu-id="5bd59-121">A common example is an invalid entry in `/etc/fstab`, or hello underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="5bd59-122">Получить журналы загрузки hello с [az ВМ Диагностика загрузки get загрузки журнал-](/cli/azure/vm/boot-diagnostics#get-boot-log).</span><span class="sxs-lookup"><span data-stu-id="5bd59-122">Get hello boot logs with [az vm boot-diagnostics get-boot-log](/cli/azure/vm/boot-diagnostics#get-boot-log).</span></span> <span data-ttu-id="5bd59-123">Hello следующий пример получает hello последовательного выходные данные из виртуальной Машины с именем hello `myVM` в группе ресурсов hello с именем `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="5bd59-123">hello following example gets hello serial output from hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm boot-diagnostics get-boot-log --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="5bd59-124">Просмотрите почему hello виртуальной Машины происходит сбой tooboot toodetermine последовательного вывода hello.</span><span class="sxs-lookup"><span data-stu-id="5bd59-124">Review hello serial output toodetermine why hello VM is failing tooboot.</span></span> <span data-ttu-id="5bd59-125">Если последовательного вывода hello не предоставляет сведения о том, может потребоваться tooreview файлы журналов в `/var/log` после hello виртуального жесткого диска, подключенного tooa Устранение неполадок виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5bd59-125">If hello serial output isn't providing any indication, you may need tooreview log files in `/var/log` once you have hello virtual hard disk connected tooa troubleshooting VM.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="5bd59-126">Просмотр сведений для существующего виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="5bd59-126">View existing virtual hard disk details</span></span>
<span data-ttu-id="5bd59-127">Перед тем как присоединить tooanother вашего виртуального жесткого диска (VHD) виртуальной Машины, необходимо tooidentify hello URI hello диска операционной системы.</span><span class="sxs-lookup"><span data-stu-id="5bd59-127">Before you can attach your virtual hard disk (VHD) tooanother VM, you need tooidentify hello URI of hello OS disk.</span></span> 

<span data-ttu-id="5bd59-128">Просмотрите сведения о виртуальной машине с помощью команды [az vm show](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="5bd59-128">View information about your VM with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="5bd59-129">Используйте hello `--query` флаг tooextract hello URI toohello ОС диска.</span><span class="sxs-lookup"><span data-stu-id="5bd59-129">Use hello `--query` flag tooextract hello URI toohello OS disk.</span></span> <span data-ttu-id="5bd59-130">Hello следующий пример возвращает сведения о диске для виртуальной Машины с именем hello `myVM` в группе ресурсов hello с именем `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="5bd59-130">hello following example gets disk information for hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm show --resource-group myResourceGroup --name myVM \
    --query [storageProfile.osDisk.vhd.uri] --output tsv
```

<span data-ttu-id="5bd59-131">Hello URI аналогичен слишком**https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.</span><span class="sxs-lookup"><span data-stu-id="5bd59-131">hello URI is similar too**https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.</span></span>

## <a name="delete-existing-vm"></a><span data-ttu-id="5bd59-132">Удаление существующей виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="5bd59-132">Delete existing VM</span></span>
<span data-ttu-id="5bd59-133">Виртуальные жесткие диски и виртуальные машины — это разные ресурсы в Azure.</span><span class="sxs-lookup"><span data-stu-id="5bd59-133">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="5bd59-134">Виртуальный жесткий диск является местом hello операционной системы, приложения и конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5bd59-134">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="5bd59-135">Hello самой ВМ — точно так же метаданные, которые определяет hello размер или расположение и ссылки на ресурсы, такие как виртуальный жесткий диск или виртуальный сетевой адаптер (NIC).</span><span class="sxs-lookup"><span data-stu-id="5bd59-135">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="5bd59-136">Каждый виртуальный жесткий диск содержит аренды, назначенный при присоединении tooa виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5bd59-136">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="5bd59-137">Несмотря на то, что диски с данными может быть присоединенные и отсоединенные даже в том случае, когда выполняется hello виртуальной Машины, диска ОС hello отключить невозможно, пока удаляется hello ресурса виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5bd59-137">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="5bd59-138">Аренда Hello продолжается tooassociate hello ОС диска с виртуальной Машиной даже в том случае, если этой виртуальной Машины находится в состоянии остановки и освобождается.</span><span class="sxs-lookup"><span data-stu-id="5bd59-138">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="5bd59-139">Здравствуйте, первый шаг toorecover ВМ — toodelete hello ВМ сам ресурс.</span><span class="sxs-lookup"><span data-stu-id="5bd59-139">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="5bd59-140">Удаление hello ВМ оставляет hello виртуальных жестких дисков в вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="5bd59-140">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="5bd59-141">После hello удаления виртуальной Машины присоединения hello виртуальный жесткий диск tooanother ВМ tootroubleshoot и устранение ошибок hello.</span><span class="sxs-lookup"><span data-stu-id="5bd59-141">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="5bd59-142">Удалить hello виртуальной Машины с [удаление виртуальной машины az](/cli/azure/vm#delete).</span><span class="sxs-lookup"><span data-stu-id="5bd59-142">Delete hello VM with [az vm delete](/cli/azure/vm#delete).</span></span> <span data-ttu-id="5bd59-143">Следующий пример удаляет Hello hello виртуальной Машины с именем `myVM` из группы ресурсов hello с именем `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="5bd59-143">hello following example deletes hello VM named `myVM` from hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm delete --resource-group myResourceGroup --name myVM 
```

<span data-ttu-id="5bd59-144">Подождите, пока hello ВМ закончит удаление перед присоединением tooanother hello виртуальный жесткий диск виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5bd59-144">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="5bd59-145">Аренда Hello hello виртуальный жесткий диск, который связывает его с hello виртуальной Машины должен toobe выпуска перед тем как присоединить tooanother hello виртуальный жесткий диск виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5bd59-145">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="5bd59-146">Подключить существующий виртуальный жесткий диск tooanother виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="5bd59-146">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="5bd59-147">Для Здравствуйте рядом шагах, для устранения неполадок используется другой виртуальной Машиной.</span><span class="sxs-lookup"><span data-stu-id="5bd59-147">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="5bd59-148">Подключить существующий виртуальный жесткий диск toothis hello Устранение неполадок виртуальной Машины toobrowse и изменить содержимое диска hello.</span><span class="sxs-lookup"><span data-stu-id="5bd59-148">You attach hello existing virtual hard disk toothis troubleshooting VM toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="5bd59-149">Этот процесс позволяет toocorrect все ошибки конфигурации или Просмотр дополнительных приложений или файлы журналов, например системы.</span><span class="sxs-lookup"><span data-stu-id="5bd59-149">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="5bd59-150">Выберите или создайте другой toouse виртуальной Машины для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="5bd59-150">Choose or create another VM toouse for troubleshooting purposes.</span></span>

<span data-ttu-id="5bd59-151">Подключить hello существующий виртуальный жесткий диск с [присоединения az диск виртуальной машины неуправляемого-](/cli/azure/vm/unmanaged-disk#attach).</span><span class="sxs-lookup"><span data-stu-id="5bd59-151">Attach hello existing virtual hard disk with [az vm unmanaged-disk attach](/cli/azure/vm/unmanaged-disk#attach).</span></span> <span data-ttu-id="5bd59-152">При присоединении hello существующий виртуальный жесткий диск, укажите диск toohello hello URI, полученный на предыдущем hello `az vm show` команды.</span><span class="sxs-lookup"><span data-stu-id="5bd59-152">When you attach hello existing virtual hard disk, specify hello URI toohello disk obtained in hello preceding `az vm show` command.</span></span> <span data-ttu-id="5bd59-153">Hello примере присоединяет существующий виртуальный жесткий диск toohello Устранение неполадок виртуальной Машины с именем `myVMRecovery` в группе ресурсов hello с именем `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="5bd59-153">hello following example attaches an existing virtual hard disk toohello troubleshooting VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm unmanaged-disk attach --resource-group myResourceGroup --vm-name myVMRecovery \
    --vhd-uri https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="5bd59-154">Подключить hello подключенный диск данных</span><span class="sxs-lookup"><span data-stu-id="5bd59-154">Mount hello attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="5bd59-155">Hello следующих примерах приведены шаги на Виртуальной машине Ubuntu hello.</span><span class="sxs-lookup"><span data-stu-id="5bd59-155">hello following examples detail hello steps required on an Ubuntu VM.</span></span> <span data-ttu-id="5bd59-156">Если вы используете другой дистрибутив Linux, например Red Hat Enterprise Linux или SUSE, hello расположения файлов журнала и `mount` команд может немного отличаться.</span><span class="sxs-lookup"><span data-stu-id="5bd59-156">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, hello log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="5bd59-157">См. в документации toohello для вашего конкретного дистрибутив для hello соответствующие изменения в командах.</span><span class="sxs-lookup"><span data-stu-id="5bd59-157">Refer toohello documentation for your specific distro for hello appropriate changes in commands.</span></span>

1. <span data-ttu-id="5bd59-158">Устранение неполадок виртуальной Машины, используя соответствующие учетные данные hello tooyour SSH.</span><span class="sxs-lookup"><span data-stu-id="5bd59-158">SSH tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="5bd59-159">Если этот диск является tooyour данных диске, подключенном hello для первого Устранение неполадок виртуальной Машины, hello подключен жесткий диск, скорее всего слишком`/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="5bd59-159">If this disk is hello first data disk attached tooyour troubleshooting VM, hello disk is likely connected too`/dev/sdc`.</span></span> <span data-ttu-id="5bd59-160">Используйте `dmseg` tooview присоединенных дисков:</span><span class="sxs-lookup"><span data-stu-id="5bd59-160">Use `dmseg` tooview attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```

    <span data-ttu-id="5bd59-161">Hello вывода будет примерно toohello следующий пример:</span><span class="sxs-lookup"><span data-stu-id="5bd59-161">hello output is similar toohello following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="5bd59-162">В предыдущих пример hello, диск hello ОС находится на `/dev/sda` и hello временного диска, указанное для каждой виртуальной Машины в `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="5bd59-162">In hello preceding example, hello OS disk is at `/dev/sda` and hello temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="5bd59-163">Если у вас несколько дисков данных, они будут присоединены как `/dev/sdd`, `/dev/sde` и т. д.</span><span class="sxs-lookup"><span data-stu-id="5bd59-163">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="5bd59-164">Создайте directory toomount существующий виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="5bd59-164">Create a directory toomount your existing virtual hard disk.</span></span> <span data-ttu-id="5bd59-165">Hello следующий пример создает каталог с именем `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="5bd59-165">hello following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="5bd59-166">При наличии нескольких секций на существующий виртуальный жесткий диск, подключите hello необходимые секции.</span><span class="sxs-lookup"><span data-stu-id="5bd59-166">If you have multiple partitions on your existing virtual hard disk, mount hello required partition.</span></span> <span data-ttu-id="5bd59-167">Hello следующий пример подключает первому основному разделу hello в `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="5bd59-167">hello following example mounts hello first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="5bd59-168">Лучший способ — что toomount диски с данными на виртуальных машинах в Azure с помощью hello универсальный уникальный идентификатор UUID hello виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="5bd59-168">Best practice is toomount data disks on VMs in Azure using hello universally unique identifier (UUID) of hello virtual hard disk.</span></span> <span data-ttu-id="5bd59-169">В этом сценарии короткий по устранению неполадок монтажного hello виртуального жесткого диска с помощью hello UUID не требуется.</span><span class="sxs-lookup"><span data-stu-id="5bd59-169">For this short troubleshooting scenario, mounting hello virtual hard disk using hello UUID is not necessary.</span></span> <span data-ttu-id="5bd59-170">Тем не менее, при обычных условиях использования редактирования `/etc/fstab` toomount виртуальных жестких дисков с помощью имени, а не может вызвать UUID hello tooboot toofail виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5bd59-170">However, under normal use, editing `/etc/fstab` toomount virtual hard disks using device name rather than UUID may cause hello VM toofail tooboot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="5bd59-171">Устранение неполадок на исходном виртуальном жестком диске</span><span class="sxs-lookup"><span data-stu-id="5bd59-171">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="5bd59-172">С hello существующий виртуальный жесткий диск подключен теперь можно выполнять обслуживание и действия по устранению неполадок при необходимости.</span><span class="sxs-lookup"><span data-stu-id="5bd59-172">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="5bd59-173">После разрешения проблемы hello продолжите hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="5bd59-173">Once you have addressed hello issues, continue with hello following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="5bd59-174">Отключение и отсоединение исходного виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="5bd59-174">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="5bd59-175">После разрешения ошибки, можно отключить и отсоединение hello существующий виртуальный жесткий диск от виртуальной Машины по устранению неполадок.</span><span class="sxs-lookup"><span data-stu-id="5bd59-175">Once your errors are resolved, you unmount and detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="5bd59-176">Расположение виртуального жесткого диска нельзя использовать с любой другой ВМ до освобождения аренды hello присоединение toohello hello виртуального жесткого диска, устранение неполадок виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5bd59-176">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="5bd59-177">Из сеанса SSH hello tooyour Устранение неполадок виртуальной Машины отключите hello существующий виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="5bd59-177">From hello SSH session tooyour troubleshooting VM, unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="5bd59-178">Сначала измените вне hello родительский каталог для точки подключения:</span><span class="sxs-lookup"><span data-stu-id="5bd59-178">Change out of hello parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="5bd59-179">Теперь отключите hello существующий виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="5bd59-179">Now unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="5bd59-180">Hello следующий пример отсоединяет диск hello устройство с `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="5bd59-180">hello following example unmounts hello device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="5bd59-181">Теперь отсоедините hello виртуальный жесткий диск из виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="5bd59-181">Now detach hello virtual hard disk from hello VM.</span></span> <span data-ttu-id="5bd59-182">Выйти из сеанса tooyour hello SSH, устранение неполадок виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5bd59-182">Exit hello SSH session tooyour troubleshooting VM.</span></span> <span data-ttu-id="5bd59-183">Список hello присоединенного tooyour дисков данных, устранение неполадок виртуальной Машины с [списка неуправляемого дисков виртуальной машины az](/cli/azure/vm/unmanaged-disk#list).</span><span class="sxs-lookup"><span data-stu-id="5bd59-183">List hello attached data disks tooyour troubleshooting VM with [az vm unmanaged-disk list](/cli/azure/vm/unmanaged-disk#list).</span></span> <span data-ttu-id="5bd59-184">Hello списки hello диски с данными в примере присоединенного toohello виртуальной Машины с именем `myVMRecovery` в группе ресурсов hello с именем `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="5bd59-184">hello following example lists hello data disks attached toohello VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    azure vm unmanaged-disk list --resource-group myResourceGroup --vm-name myVMRecovery \
        --query '[].{Disk:vhd.uri}' --output table
    ```

    <span data-ttu-id="5bd59-185">Запишите имя hello для существующего виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="5bd59-185">Note hello name for your existing virtual hard disk.</span></span> <span data-ttu-id="5bd59-186">Например, диск с именем hello hello URI **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** — **myVHD**.</span><span class="sxs-lookup"><span data-stu-id="5bd59-186">For example, hello name of a disk with hello URI of **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** is **myVHD**.</span></span> 

    <span data-ttu-id="5bd59-187">Отсоединить диск данных hello от ВМ [отсоединения az диск виртуальной машины неуправляемого-](/cli/azure/vm/unmanaged-disk#detach).</span><span class="sxs-lookup"><span data-stu-id="5bd59-187">Detach hello data disk from your VM [az vm unmanaged-disk detach](/cli/azure/vm/unmanaged-disk#detach).</span></span> <span data-ttu-id="5bd59-188">Hello следующий пример отсоединяет hello диск с именем `myVHD` из виртуальной Машины с именем hello `myVMRecovery` в hello `myResourceGroup` группа ресурсов:</span><span class="sxs-lookup"><span data-stu-id="5bd59-188">hello following example detaches hello disk named `myVHD` from hello VM named `myVMRecovery` in hello `myResourceGroup` resource group:</span></span>

    ```azurecli
    az vm unmanaged-disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --name myVHD
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="5bd59-189">Создание виртуальной машины из исходного жесткого диска</span><span class="sxs-lookup"><span data-stu-id="5bd59-189">Create VM from original hard disk</span></span>
<span data-ttu-id="5bd59-190">использовать ВМ с исходного виртуального жесткого диска, toocreate [этого шаблона Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="5bd59-190">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span></span> <span data-ttu-id="5bd59-191">шаблон фактического JSON Hello находится в hello по ссылке:</span><span class="sxs-lookup"><span data-stu-id="5bd59-191">hello actual JSON template is at hello following link:</span></span>

- <span data-ttu-id="5bd59-192">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="5bd59-192">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span></span>

<span data-ttu-id="5bd59-193">Hello шаблон развертывания ВМ с помощью hello URI VHD-файла из hello ранее команд.</span><span class="sxs-lookup"><span data-stu-id="5bd59-193">hello template deploys a VM using hello VHD URI from hello earlier command.</span></span> <span data-ttu-id="5bd59-194">Развертывание шаблона hello с [создания развертывания группы az](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="5bd59-194">Deploy hello template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="5bd59-195">Укажите hello URI tooyour исходный виртуальный жесткий ДИСК и затем укажите тип hello ОС, размер виртуальной Машины и имя виртуальной Машины следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5bd59-195">Provide hello URI tooyour original VHD and then specify hello OS type, VM size, and VM name as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeployment \
  --parameters '{"osDiskVhdUri": {"value": "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"},
    "osType": {"value": "Linux"},
    "vmSize": {"value": "Standard_DS1_v2"},
    "vmName": {"value": "myDeployedVM"}}' \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="5bd59-196">Восстановление диагностики загрузки</span><span class="sxs-lookup"><span data-stu-id="5bd59-196">Re-enable boot diagnostics</span></span>
<span data-ttu-id="5bd59-197">При создании ВМ из hello существующий виртуальный жесткий диск, диагностика загрузки может не быть доступной.</span><span class="sxs-lookup"><span data-stu-id="5bd59-197">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="5bd59-198">Включите диагностику загрузки с помощью команды [az vm boot-diagnostics enable](/cli/azure/vm/boot-diagnostics#enable).</span><span class="sxs-lookup"><span data-stu-id="5bd59-198">Enable boot diagnostics with [az vm boot-diagnostics enable](/cli/azure/vm/boot-diagnostics#enable).</span></span> <span data-ttu-id="5bd59-199">Hello следующий пример включает hello диагностического расширения для виртуальной Машины с именем hello `myDeployedVM` в группе ресурсов hello с именем `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="5bd59-199">hello following example enables hello diagnostic extension on hello VM named `myDeployedVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm boot-diagnostics enable --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a><span data-ttu-id="5bd59-200">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5bd59-200">Next steps</span></span>
<span data-ttu-id="5bd59-201">Если возникают проблемы с подключением tooyour виртуальной Машины, см. раздел [Устранение SSH подключений tooan виртуальной Машины Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5bd59-201">If you are having issues connecting tooyour VM, see [Troubleshoot SSH connections tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="5bd59-202">Для решения проблем с доступом к приложениям, выполняющимся на виртуальной машине, см. статью [Устранение проблем с подключением к приложениям на виртуальных машинах Linux в Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5bd59-202">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
