---
title: "Использование виртуальной машины Linux для устранения неполадок с помощью Azure CLI 2.0 | Документация Майкрософт"
description: "Узнайте, как устранять неполадки виртуальных машин Linux, подключив диск ОС к виртуальной машине восстановления с помощью Azure CLI 2.0."
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
ms.openlocfilehash: 7a28accce1bd328b2b486b588c44d91b03e42122
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-the-os-disk-to-a-recovery-vm-with-the-azure-cli-20"></a><span data-ttu-id="c5777-103">Устранение неполадок виртуальной машины Linux путем подключения диска ОС к виртуальной машине восстановления с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c5777-103">Troubleshoot a Linux VM by attaching the OS disk to a recovery VM with the Azure CLI 2.0</span></span>
<span data-ttu-id="c5777-104">Если возникает проблема с загрузкой или диском на виртуальной машине Linux, возможно, вам нужно устранить неполадки, связанные с самим виртуальным жестким диском.</span><span class="sxs-lookup"><span data-stu-id="c5777-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span></span> <span data-ttu-id="c5777-105">Например, такая ситуация возникает из-за неправильной записи в `/etc/fstab`, которая мешает успешно загрузить виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="c5777-105">A common example would be an invalid entry in `/etc/fstab` that prevents the VM from being able to boot successfully.</span></span> <span data-ttu-id="c5777-106">В этой статье подробно описано, как с помощью Azure CLI 2.0 подключить виртуальный жесткий диск к другой виртуальной машине Linux для устранения ошибок, а затем воссоздать исходную виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="c5777-106">This article details how to use the Azure CLI 2.0 to connect your virtual hard disk to another Linux VM to fix any errors, then re-create your original VM.</span></span> <span data-ttu-id="c5777-107">Эти действия можно также выполнить с помощью [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c5777-107">You can also perform these steps with the [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="c5777-108">Обзор процесса восстановления</span><span class="sxs-lookup"><span data-stu-id="c5777-108">Recovery process overview</span></span>
<span data-ttu-id="c5777-109">Процесс устранения неполадок выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="c5777-109">The troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="c5777-110">Удалите виртуальную машину, на которой возникли проблемы, сохранив ее виртуальные жесткие диски.</span><span class="sxs-lookup"><span data-stu-id="c5777-110">Delete the VM encountering issues, keeping the virtual hard disks.</span></span>
2. <span data-ttu-id="c5777-111">Присоедините и подключите виртуальный жесткий диск к другой виртуальной машине Linux для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="c5777-111">Attach and mount the virtual hard disk to another Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="c5777-112">Подключитесь к этой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="c5777-112">Connect to the troubleshooting VM.</span></span> <span data-ttu-id="c5777-113">Измените файлы или запустите средства, которые нужны для устранения неполадок на исходном виртуальном жестком диске.</span><span class="sxs-lookup"><span data-stu-id="c5777-113">Edit files or run any tools to fix issues on the original virtual hard disk.</span></span>
4. <span data-ttu-id="c5777-114">Отключите и отсоедините виртуальный жесткий диск от виртуальной машины, на которой выполняется устранение неполадок.</span><span class="sxs-lookup"><span data-stu-id="c5777-114">Unmount and detach the virtual hard disk from the troubleshooting VM.</span></span>
5. <span data-ttu-id="c5777-115">Создайте другую виртуальную машину, используя исходный виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="c5777-115">Create a VM using the original virtual hard disk.</span></span>

<span data-ttu-id="c5777-116">Чтобы выполнить эти действия по устранению неполадок, нужно установить последнюю версию [Azure CLI 2.0](/cli/azure/install-az-cli2) и войти в учетную запись Azure с помощью команды [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="c5777-116">To perform these troubleshooting steps, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="c5777-117">В следующих примерах замените имена параметров собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="c5777-117">In the following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="c5777-118">Используемые имена параметров: `myResourceGroup`, `mystorageaccount` и `myVM`.</span><span class="sxs-lookup"><span data-stu-id="c5777-118">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="c5777-119">Выявление проблем при загрузке</span><span class="sxs-lookup"><span data-stu-id="c5777-119">Determine boot issues</span></span>
<span data-ttu-id="c5777-120">Изучите последовательные выходные данные, чтобы определить, почему виртуальная машина не может правильно загрузиться.</span><span class="sxs-lookup"><span data-stu-id="c5777-120">Examine the serial output to determine why your VM is not able to boot correctly.</span></span> <span data-ttu-id="c5777-121">Например, причиной может быть некорректная запись в `/etc/fstab`, удаление или перемещение базового виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="c5777-121">A common example is an invalid entry in `/etc/fstab`, or the underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="c5777-122">Получите журналы загрузки с помощью команды [az vm boot-diagnostics get-boot-log](/cli/azure/vm/boot-diagnostics#get-boot-log).</span><span class="sxs-lookup"><span data-stu-id="c5777-122">Get the boot logs with [az vm boot-diagnostics get-boot-log](/cli/azure/vm/boot-diagnostics#get-boot-log).</span></span> <span data-ttu-id="c5777-123">В следующем примере возвращаются последовательные выходные данные с виртуальной машины `myVM` в группе ресурсов `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="c5777-123">The following example gets the serial output from the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm boot-diagnostics get-boot-log --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="c5777-124">Просмотрите последовательные выходные данные, чтобы определить причину сбоя загрузки виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c5777-124">Review the serial output to determine why the VM is failing to boot.</span></span> <span data-ttu-id="c5777-125">Если они не помогли определить причину сбоя, может потребоваться просмотреть файлы журналов в каталоге `/var/log` после подключения виртуального жесткого диска к виртуальной машине для устранению неполадок.</span><span class="sxs-lookup"><span data-stu-id="c5777-125">If the serial output isn't providing any indication, you may need to review log files in `/var/log` once you have the virtual hard disk connected to a troubleshooting VM.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="c5777-126">Просмотр сведений для существующего виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="c5777-126">View existing virtual hard disk details</span></span>
<span data-ttu-id="c5777-127">Прежде чем подключить виртуальный жесткий диск к другой виртуальной машине, следует определить универсальный код ресурса (URI) диска ОС.</span><span class="sxs-lookup"><span data-stu-id="c5777-127">Before you can attach your virtual hard disk (VHD) to another VM, you need to identify the URI of the OS disk.</span></span> 

<span data-ttu-id="c5777-128">Просмотрите сведения о виртуальной машине с помощью команды [az vm show](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="c5777-128">View information about your VM with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="c5777-129">Используйте флаг `--query` для извлечения универсального кода ресурса (URI) диска ОС.</span><span class="sxs-lookup"><span data-stu-id="c5777-129">Use the `--query` flag to extract the URI to the OS disk.</span></span> <span data-ttu-id="c5777-130">В следующем примере возвращаются сведения о дисках виртуальной машины `myVM` в группе ресурсов `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="c5777-130">The following example gets disk information for the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm show --resource-group myResourceGroup --name myVM \
    --query [storageProfile.osDisk.vhd.uri] --output tsv
```

<span data-ttu-id="c5777-131">Универсальный код ресурса (URI) имеет вид **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.</span><span class="sxs-lookup"><span data-stu-id="c5777-131">The URI is similar to **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.</span></span>

## <a name="delete-existing-vm"></a><span data-ttu-id="c5777-132">Удаление существующей виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c5777-132">Delete existing VM</span></span>
<span data-ttu-id="c5777-133">Виртуальные жесткие диски и виртуальные машины — это разные ресурсы в Azure.</span><span class="sxs-lookup"><span data-stu-id="c5777-133">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="c5777-134">Виртуальный жесткий диск является местом хранения операционной системы, приложений и конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c5777-134">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="c5777-135">Виртуальная машина — это просто метаданные, которые определяют размер или расположение объекта, а также ссылки на ресурсы, такие как виртуальные жесткие диски или виртуальные сетевые адаптеры.</span><span class="sxs-lookup"><span data-stu-id="c5777-135">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="c5777-136">При присоединении виртуального жесткого диска к виртуальной машине для него регистрируется аренда.</span><span class="sxs-lookup"><span data-stu-id="c5777-136">Each virtual hard disk has a lease assigned when attached to a VM.</span></span> <span data-ttu-id="c5777-137">Диски данных можно присоединять и отсоединять во время работы виртуальной машины, но диск операционной системы отсоединить невозможно, пока ресурс виртуальной машины не будет удален.</span><span class="sxs-lookup"><span data-stu-id="c5777-137">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span></span> <span data-ttu-id="c5777-138">Аренда сохраняет привязку диска операционной системы к виртуальной машине, даже когда эта виртуальная машина остановлена или отменено ее распределение.</span><span class="sxs-lookup"><span data-stu-id="c5777-138">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="c5777-139">Поэтому для восстановления виртуальной машины нужно прежде всего удалить ресурс виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c5777-139">The first step to recover your VM is to delete the VM resource itself.</span></span> <span data-ttu-id="c5777-140">Удаление виртуальной машины не повлияет на виртуальные жесткие диски, размещенные в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="c5777-140">Deleting the VM leaves the virtual hard disks in your storage account.</span></span> <span data-ttu-id="c5777-141">После удаления виртуальной машины присоедините виртуальный жесткий диск к другой виртуальной машине, чтобы устранить неполадки.</span><span class="sxs-lookup"><span data-stu-id="c5777-141">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span></span>

<span data-ttu-id="c5777-142">Удалите виртуальную машину с помощью команды [az vm delete](/cli/azure/vm#delete).</span><span class="sxs-lookup"><span data-stu-id="c5777-142">Delete the VM with [az vm delete](/cli/azure/vm#delete).</span></span> <span data-ttu-id="c5777-143">В следующем примере виртуальная машина `myVM` удаляется из группы ресурсов `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="c5777-143">The following example deletes the VM named `myVM` from the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm delete --resource-group myResourceGroup --name myVM 
```

<span data-ttu-id="c5777-144">Дождитесь, пока удаление завершится, прежде чем присоединять виртуальный жесткий диск к другой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="c5777-144">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span></span> <span data-ttu-id="c5777-145">Чтобы присоединить виртуальный жесткий диск к другой виртуальной машине, необходимо снять аренду, которая привязывает диск к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="c5777-145">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-to-another-vm"></a><span data-ttu-id="c5777-146">Присоединение существующего виртуального жесткого диска к другой виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="c5777-146">Attach existing virtual hard disk to another VM</span></span>
<span data-ttu-id="c5777-147">В следующих нескольких шагах описывается использование другой виртуальной машины для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="c5777-147">For the next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="c5777-148">Присоедините существующий виртуальный жесткий диск к виртуальной машине для устранения неполадок, чтобы просматривать и изменять содержимое диска.</span><span class="sxs-lookup"><span data-stu-id="c5777-148">You attach the existing virtual hard disk to this troubleshooting VM to browse and edit the disk's content.</span></span> <span data-ttu-id="c5777-149">Этот процесс позволяет, например, исправить ошибки конфигурации или изучить дополнительные журналы протоколов или системы.</span><span class="sxs-lookup"><span data-stu-id="c5777-149">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="c5777-150">Выберите или создайте другую виртуальную машину, которая будет использоваться для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="c5777-150">Choose or create another VM to use for troubleshooting purposes.</span></span>

<span data-ttu-id="c5777-151">Подключите существующий виртуальный жесткий диск с помощью команды [az vm unmanaged-disk attach](/cli/azure/vm/unmanaged-disk#attach).</span><span class="sxs-lookup"><span data-stu-id="c5777-151">Attach the existing virtual hard disk with [az vm unmanaged-disk attach](/cli/azure/vm/unmanaged-disk#attach).</span></span> <span data-ttu-id="c5777-152">При присоединении существующего виртуального жесткого диска укажите универсальный код ресурса (URI) адрес диска, полученный в предыдущей команде `az vm show`.</span><span class="sxs-lookup"><span data-stu-id="c5777-152">When you attach the existing virtual hard disk, specify the URI to the disk obtained in the preceding `az vm show` command.</span></span> <span data-ttu-id="c5777-153">В следующем примере существующий виртуальный жесткий диск присоединяется к виртуальной машине для устранения неполадок `myVMRecovery` в группе ресурсов `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="c5777-153">The following example attaches an existing virtual hard disk to the troubleshooting VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm unmanaged-disk attach --resource-group myResourceGroup --vm-name myVMRecovery \
    --vhd-uri https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-the-attached-data-disk"></a><span data-ttu-id="c5777-154">Подключение присоединенного диска данных</span><span class="sxs-lookup"><span data-stu-id="c5777-154">Mount the attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="c5777-155">В следующих примерах описана процедура для виртуальной машины Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c5777-155">The following examples detail the steps required on an Ubuntu VM.</span></span> <span data-ttu-id="c5777-156">Если вы используете другой дистрибутив Linux, например Red Hat Enterprise Linux или SUSE, команды `mount` и расположение файлов журнала могут немного отличаться.</span><span class="sxs-lookup"><span data-stu-id="c5777-156">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, the log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="c5777-157">Используйте документацию к своему дистрибутиву, чтобы скорректировать команды соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="c5777-157">Refer to the documentation for your specific distro for the appropriate changes in commands.</span></span>

1. <span data-ttu-id="c5777-158">Подключитесь к виртуальной машине для устранения неполадок по протоколу SSH, используя соответствующие учетные данные.</span><span class="sxs-lookup"><span data-stu-id="c5777-158">SSH to your troubleshooting VM using the appropriate credentials.</span></span> <span data-ttu-id="c5777-159">Если присоединенный диск является первым диском данных на этой виртуальной машине, он скорее всего подключен к `/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="c5777-159">If this disk is the first data disk attached to your troubleshooting VM, the disk is likely connected to `/dev/sdc`.</span></span> <span data-ttu-id="c5777-160">Запустите команду `dmseg`, чтобы просмотреть присоединенные диски:</span><span class="sxs-lookup"><span data-stu-id="c5777-160">Use `dmseg` to view attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```

    <span data-ttu-id="c5777-161">Вы должны увидеть результат, аналогичный приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="c5777-161">The output is similar to the following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="c5777-162">В предыдущем примере диск операционной системы расположен в `/dev/sda`, а временный диск, предоставляемый для каждой виртуальной машины, расположен в `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="c5777-162">In the preceding example, the OS disk is at `/dev/sda` and the temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="c5777-163">Если у вас несколько дисков данных, они будут присоединены как `/dev/sdd`, `/dev/sde` и т. д.</span><span class="sxs-lookup"><span data-stu-id="c5777-163">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="c5777-164">Создайте каталог для подключения существующего виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="c5777-164">Create a directory to mount your existing virtual hard disk.</span></span> <span data-ttu-id="c5777-165">Следующая команда создает каталог с именем `troubleshootingdisk`.</span><span class="sxs-lookup"><span data-stu-id="c5777-165">The following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="c5777-166">Если на существующем виртуальном жестком диске есть несколько разделов, подключите нужный.</span><span class="sxs-lookup"><span data-stu-id="c5777-166">If you have multiple partitions on your existing virtual hard disk, mount the required partition.</span></span> <span data-ttu-id="c5777-167">Следующая команда подключает первый основной разделу к каталогу `/dev/sdc1`.</span><span class="sxs-lookup"><span data-stu-id="c5777-167">The following example mounts the first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="c5777-168">Мы рекомендуем подключать диски данных к виртуальным машинам Azure с использованием глобального уникального идентификатора (UUID) виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="c5777-168">Best practice is to mount data disks on VMs in Azure using the universally unique identifier (UUID) of the virtual hard disk.</span></span> <span data-ttu-id="c5777-169">Для нашего упрощенного примера по устранению неполадок можно и не использовать UUID для подключения диска.</span><span class="sxs-lookup"><span data-stu-id="c5777-169">For this short troubleshooting scenario, mounting the virtual hard disk using the UUID is not necessary.</span></span> <span data-ttu-id="c5777-170">Но в обычной ситуации, если вы измените `/etc/fstab` так, чтобы виртуальные жесткие диски подключались по имени устройства вместо UUID, у виртуальной машины могут быть проблемы с загрузкой.</span><span class="sxs-lookup"><span data-stu-id="c5777-170">However, under normal use, editing `/etc/fstab` to mount virtual hard disks using device name rather than UUID may cause the VM to fail to boot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="c5777-171">Устранение неполадок на исходном виртуальном жестком диске</span><span class="sxs-lookup"><span data-stu-id="c5777-171">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="c5777-172">Теперь, когда существующий виртуальный жесткий диск подключен, вы можете выполнить любые необходимые действия по обслуживанию и (или) устранению неполадок.</span><span class="sxs-lookup"><span data-stu-id="c5777-172">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="c5777-173">После устранения проблем выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c5777-173">Once you have addressed the issues, continue with the following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="c5777-174">Отключение и отсоединение исходного виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="c5777-174">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="c5777-175">После устранения ошибок отключите и отсоедините существующий виртуальный жесткий диск от виртуальной машины, использованный для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="c5777-175">Once your errors are resolved, you unmount and detach the existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="c5777-176">Виртуальный жесткий диск нельзя использовать с другой виртуальной машиной, пока вы не отмените аренду, присоединяющую виртуальный жесткий диск к виртуальной машине для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="c5777-176">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span></span>

1. <span data-ttu-id="c5777-177">Используя открытый сеанс подключения по SSH к виртуальной машине для устранения неполадок, отключите существующий виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="c5777-177">From the SSH session to your troubleshooting VM, unmount the existing virtual hard disk.</span></span> <span data-ttu-id="c5777-178">Прежде всего выйдите из каталога, в котором создана точка подключения.</span><span class="sxs-lookup"><span data-stu-id="c5777-178">Change out of the parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="c5777-179">Теперь отключите существующий виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="c5777-179">Now unmount the existing virtual hard disk.</span></span> <span data-ttu-id="c5777-180">В следующем примере диск отключается от каталога `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="c5777-180">The following example unmounts the device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="c5777-181">Теперь отсоедините виртуальный жесткий диск от виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c5777-181">Now detach the virtual hard disk from the VM.</span></span> <span data-ttu-id="c5777-182">Выйдите из сеанса SSH и вернитесь к виртуальной машине для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="c5777-182">Exit the SSH session to your troubleshooting VM.</span></span> <span data-ttu-id="c5777-183">Выведите список дисков данных, подключенные к виртуальной машине для устранения неполадок, выполнив команду [az vm unmanaged-disk list](/cli/azure/vm/unmanaged-disk#list).</span><span class="sxs-lookup"><span data-stu-id="c5777-183">List the attached data disks to your troubleshooting VM with [az vm unmanaged-disk list](/cli/azure/vm/unmanaged-disk#list).</span></span> <span data-ttu-id="c5777-184">В следующем примере указываются диски данных, подключенные к виртуальной машине `myVMRecovery` в группе ресурсов `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="c5777-184">The following example lists the data disks attached to the VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    azure vm unmanaged-disk list --resource-group myResourceGroup --vm-name myVMRecovery \
        --query '[].{Disk:vhd.uri}' --output table
    ```

    <span data-ttu-id="c5777-185">Обратите внимание на имя существующего виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="c5777-185">Note the name for your existing virtual hard disk.</span></span> <span data-ttu-id="c5777-186">Например, имя диска с универсальным кодом ресурса (URI) **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** — **myVHD**.</span><span class="sxs-lookup"><span data-stu-id="c5777-186">For example, the name of a disk with the URI of **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** is **myVHD**.</span></span> 

    <span data-ttu-id="c5777-187">Отключите диск данных от виртуальной машины командой [az vm unmanaged-disk detach](/cli/azure/vm/unmanaged-disk#detach).</span><span class="sxs-lookup"><span data-stu-id="c5777-187">Detach the data disk from your VM [az vm unmanaged-disk detach](/cli/azure/vm/unmanaged-disk#detach).</span></span> <span data-ttu-id="c5777-188">В следующем примере диск `myVHD` отключается от виртуальной машины `myVMRecovery` в группе ресурсов `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="c5777-188">The following example detaches the disk named `myVHD` from the VM named `myVMRecovery` in the `myResourceGroup` resource group:</span></span>

    ```azurecli
    az vm unmanaged-disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --name myVHD
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="c5777-189">Создание виртуальной машины из исходного жесткого диска</span><span class="sxs-lookup"><span data-stu-id="c5777-189">Create VM from original hard disk</span></span>
<span data-ttu-id="c5777-190">Чтобы создать виртуальную машину из исходного виртуального жесткого диска, используйте [этот шаблон Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="c5777-190">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span></span> <span data-ttu-id="c5777-191">Фактический шаблон JSON доступен по следующей ссылке:</span><span class="sxs-lookup"><span data-stu-id="c5777-191">The actual JSON template is at the following link:</span></span>

- <span data-ttu-id="c5777-192">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="c5777-192">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span></span>

<span data-ttu-id="c5777-193">Шаблон развертывает виртуальную машину с помощью универсального кода ресурса (URI) виртуального жесткого диска из предыдущей команды.</span><span class="sxs-lookup"><span data-stu-id="c5777-193">The template deploys a VM using the VHD URI from the earlier command.</span></span> <span data-ttu-id="c5777-194">Разверните шаблон с помощью команды [az group deployment create](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="c5777-194">Deploy the template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="c5777-195">Введите универсальный код ресурса (URI) для исходного виртуального жесткого диска, а затем укажите тип ОС, размер и имя виртуальной машины, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="c5777-195">Provide the URI to your original VHD and then specify the OS type, VM size, and VM name as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeployment \
  --parameters '{"osDiskVhdUri": {"value": "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"},
    "osType": {"value": "Linux"},
    "vmSize": {"value": "Standard_DS1_v2"},
    "vmName": {"value": "myDeployedVM"}}' \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="c5777-196">Восстановление диагностики загрузки</span><span class="sxs-lookup"><span data-stu-id="c5777-196">Re-enable boot diagnostics</span></span>
<span data-ttu-id="c5777-197">При создании виртуальной машины на основе существующего виртуального жесткого диска диагностика загрузки не всегда автоматически включена.</span><span class="sxs-lookup"><span data-stu-id="c5777-197">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="c5777-198">Включите диагностику загрузки с помощью команды [az vm boot-diagnostics enable](/cli/azure/vm/boot-diagnostics#enable).</span><span class="sxs-lookup"><span data-stu-id="c5777-198">Enable boot diagnostics with [az vm boot-diagnostics enable](/cli/azure/vm/boot-diagnostics#enable).</span></span> <span data-ttu-id="c5777-199">В следующем примере на виртуальной машине `myDeployedVM` в группе ресурсов `myResourceGroup` включается расширение диагностики:</span><span class="sxs-lookup"><span data-stu-id="c5777-199">The following example enables the diagnostic extension on the VM named `myDeployedVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm boot-diagnostics enable --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a><span data-ttu-id="c5777-200">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c5777-200">Next steps</span></span>
<span data-ttu-id="c5777-201">При возникновении проблем с подключением к виртуальной машине см. статью [Устранение неполадок с SSH-подключением к виртуальной машине Azure Linux: сбой, ошибка или отклонение](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c5777-201">If you are having issues connecting to your VM, see [Troubleshoot SSH connections to an Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="c5777-202">Для решения проблем с доступом к приложениям, выполняющимся на виртуальной машине, см. статью [Устранение проблем с подключением к приложениям на виртуальных машинах Linux в Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c5777-202">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>