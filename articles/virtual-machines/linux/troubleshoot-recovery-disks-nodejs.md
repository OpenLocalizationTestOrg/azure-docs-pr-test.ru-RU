---
title: "Использование виртуальной машины Linux для устранения неполадок с помощью Azure CLI 1.0 | Документация Майкрософт"
description: "Узнайте, как устранять неполадки виртуальных машин Linux, подключив диск ОС к виртуальной машине восстановления с помощью Azure CLI 1.0."
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
ms.openlocfilehash: d817358211f123c96d899c5cff88cc47aeb5c9c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-the-os-disk-to-a-recovery-vm-using-the-azure-cli-10"></a><span data-ttu-id="9e16e-103">Устранение неполадок виртуальной машины Linux путем подключения диска ОС к виртуальной машине восстановления с помощью Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="9e16e-103">Troubleshoot a Linux VM by attaching the OS disk to a recovery VM using the Azure CLI 1.0</span></span>
<span data-ttu-id="9e16e-104">Если возникает проблема с загрузкой или диском на виртуальной машине Linux, возможно, вам нужно устранить неполадки, связанные с самим виртуальным жестким диском.</span><span class="sxs-lookup"><span data-stu-id="9e16e-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span></span> <span data-ttu-id="9e16e-105">Например, такая ситуация возникает из-за неправильной записи в `/etc/fstab`, которая мешает успешно загрузить виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="9e16e-105">A common example would be an invalid entry in `/etc/fstab` that prevents the VM from being able to boot successfully.</span></span> <span data-ttu-id="9e16e-106">В этой статье подробно описано, как с помощью Azure CLI 1.0 подключить виртуальный жесткий диск к другой виртуальной машине Linux для устранения ошибок, а затем воссоздать исходную виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="9e16e-106">This article details how to use the Azure CLI 1.0 to connect your virtual hard disk to another Linux VM to fix any errors, then re-create your original VM.</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="9e16e-107">Версии интерфейса командной строки для выполнения задачи</span><span class="sxs-lookup"><span data-stu-id="9e16e-107">CLI versions to complete the task</span></span>
<span data-ttu-id="9e16e-108">Вы можете выполнить задачу, используя одну из следующих версий интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="9e16e-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="9e16e-109">[Azure CLI 1.0](#recovery-process-overview) — интерфейс командной строки для классической модели развертывания и модели развертывания Resource Manager (в этой статье).</span><span class="sxs-lookup"><span data-stu-id="9e16e-109">[Azure CLI 1.0](#recovery-process-overview) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="9e16e-110">[Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) — интерфейс командной строки следующего поколения для модели развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9e16e-110">[Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="9e16e-111">Обзор процесса восстановления</span><span class="sxs-lookup"><span data-stu-id="9e16e-111">Recovery process overview</span></span>
<span data-ttu-id="9e16e-112">Процесс устранения неполадок выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="9e16e-112">The troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="9e16e-113">Удалите виртуальную машину, на которой возникли проблемы, сохранив ее виртуальные жесткие диски.</span><span class="sxs-lookup"><span data-stu-id="9e16e-113">Delete the VM encountering issues, keeping the virtual hard disks.</span></span>
2. <span data-ttu-id="9e16e-114">Присоедините и подключите виртуальный жесткий диск к другой виртуальной машине Linux для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="9e16e-114">Attach and mount the virtual hard disk to another Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="9e16e-115">Подключитесь к этой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="9e16e-115">Connect to the troubleshooting VM.</span></span> <span data-ttu-id="9e16e-116">Измените файлы или запустите средства, которые нужны для устранения неполадок на исходном виртуальном жестком диске.</span><span class="sxs-lookup"><span data-stu-id="9e16e-116">Edit files or run any tools to fix issues on the original virtual hard disk.</span></span>
4. <span data-ttu-id="9e16e-117">Отключите и отсоедините виртуальный жесткий диск от виртуальной машины, на которой выполняется устранение неполадок.</span><span class="sxs-lookup"><span data-stu-id="9e16e-117">Unmount and detach the virtual hard disk from the troubleshooting VM.</span></span>
5. <span data-ttu-id="9e16e-118">Создайте другую виртуальную машину, используя исходный виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="9e16e-118">Create a VM using the original virtual hard disk.</span></span>

<span data-ttu-id="9e16e-119">Убедитесь, что у вас установлена [последняя версия Azure CLI 1.0](../../cli-install-nodejs.md), выполнен вход в систему и используется режим Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9e16e-119">Make sure that you have [the latest Azure CLI 1.0](../../cli-install-nodejs.md) installed and logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="9e16e-120">В следующих примерах замените имена параметров собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="9e16e-120">In the following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="9e16e-121">Используемые имена параметров: `myResourceGroup`, `mystorageaccount` и `myVM`.</span><span class="sxs-lookup"><span data-stu-id="9e16e-121">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="9e16e-122">Выявление проблем при загрузке</span><span class="sxs-lookup"><span data-stu-id="9e16e-122">Determine boot issues</span></span>
<span data-ttu-id="9e16e-123">Изучите последовательные выходные данные, чтобы определить, почему виртуальная машина не может правильно загрузиться.</span><span class="sxs-lookup"><span data-stu-id="9e16e-123">Examine the serial output to determine why your VM is not able to boot correctly.</span></span> <span data-ttu-id="9e16e-124">Например, причиной может быть некорректная запись в `/etc/fstab`, удаление или перемещение базового виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="9e16e-124">A common example is an invalid entry in `/etc/fstab`, or the underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="9e16e-125">В следующем примере возвращаются последовательные выходные данные с виртуальной машины `myVM` в группе ресурсов `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="9e16e-125">The following example gets the serial output from the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm get-serial-output --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="9e16e-126">Просмотрите последовательные выходные данные, чтобы определить причину сбоя загрузки виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="9e16e-126">Review the serial output to determine why the VM is failing to boot.</span></span> <span data-ttu-id="9e16e-127">Если они не помогли определить причину сбоя, может потребоваться просмотреть файлы журналов в каталоге `/var/log` после подключения виртуального жесткого диска к виртуальной машине для устранению неполадок.</span><span class="sxs-lookup"><span data-stu-id="9e16e-127">If the serial output isn't providing any indication, you may need to review log files in `/var/log` once you have the virtual hard disk connected to a troubleshooting VM.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="9e16e-128">Просмотр сведений для существующего виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="9e16e-128">View existing virtual hard disk details</span></span>
<span data-ttu-id="9e16e-129">Прежде чем присоединить виртуальный жесткий диск к другой виртуальной машине, следует определить имя этого виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="9e16e-129">Before you can attach your virtual hard disk to another VM, you need to identify the name of the virtual hard disk (VHD).</span></span> 

<span data-ttu-id="9e16e-130">В следующем примере возвращаются сведения о виртуальной машине `myVM` в группе ресурсов `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="9e16e-130">The following example gets information for the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="9e16e-131">Найдите параметр `Vhd URI`, который содержится в выходных данных предыдущей команды.</span><span class="sxs-lookup"><span data-stu-id="9e16e-131">Look for `Vhd URI` in the output from the preceding command.</span></span> <span data-ttu-id="9e16e-132">В следующем сокращенном примере выходных данных `Vhd URI` находится в последней строке:</span><span class="sxs-lookup"><span data-stu-id="9e16e-132">The following truncated example output shows the `Vhd URI` on the last line:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up the VM "myVM"
+ Looking up the NIC "myNic"
+ Looking up the public ip "myPublicIP"
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


## <a name="delete-existing-vm"></a><span data-ttu-id="9e16e-133">Удаление существующей виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="9e16e-133">Delete existing VM</span></span>
<span data-ttu-id="9e16e-134">Виртуальные жесткие диски и виртуальные машины — это разные ресурсы в Azure.</span><span class="sxs-lookup"><span data-stu-id="9e16e-134">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="9e16e-135">Виртуальный жесткий диск является местом хранения операционной системы, приложений и конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9e16e-135">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="9e16e-136">Виртуальная машина — это просто метаданные, которые определяют размер или расположение объекта, а также ссылки на ресурсы, такие как виртуальные жесткие диски или виртуальные сетевые адаптеры.</span><span class="sxs-lookup"><span data-stu-id="9e16e-136">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="9e16e-137">При присоединении виртуального жесткого диска к виртуальной машине для него регистрируется аренда.</span><span class="sxs-lookup"><span data-stu-id="9e16e-137">Each virtual hard disk has a lease assigned when attached to a VM.</span></span> <span data-ttu-id="9e16e-138">Диски данных можно присоединять и отсоединять во время работы виртуальной машины, но диск операционной системы отсоединить невозможно, пока ресурс виртуальной машины не будет удален.</span><span class="sxs-lookup"><span data-stu-id="9e16e-138">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span></span> <span data-ttu-id="9e16e-139">Аренда сохраняет привязку диска операционной системы к виртуальной машине, даже когда эта виртуальная машина остановлена или отменено ее распределение.</span><span class="sxs-lookup"><span data-stu-id="9e16e-139">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="9e16e-140">Поэтому для восстановления виртуальной машины нужно прежде всего удалить ресурс виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="9e16e-140">The first step to recover your VM is to delete the VM resource itself.</span></span> <span data-ttu-id="9e16e-141">Удаление виртуальной машины не повлияет на виртуальные жесткие диски, размещенные в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="9e16e-141">Deleting the VM leaves the virtual hard disks in your storage account.</span></span> <span data-ttu-id="9e16e-142">После удаления виртуальной машины присоедините виртуальный жесткий диск к другой виртуальной машине, чтобы устранить неполадки.</span><span class="sxs-lookup"><span data-stu-id="9e16e-142">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span></span>

<span data-ttu-id="9e16e-143">В следующем примере виртуальная машина `myVM` удаляется из группы ресурсов `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="9e16e-143">The following example deletes the VM named `myVM` from the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm delete --resource-group myResourceGroup --name myVM 
```

<span data-ttu-id="9e16e-144">Дождитесь, пока удаление завершится, прежде чем присоединять виртуальный жесткий диск к другой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="9e16e-144">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span></span> <span data-ttu-id="9e16e-145">Чтобы присоединить виртуальный жесткий диск к другой виртуальной машине, необходимо снять аренду, которая привязывает диск к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="9e16e-145">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-to-another-vm"></a><span data-ttu-id="9e16e-146">Присоединение существующего виртуального жесткого диска к другой виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="9e16e-146">Attach existing virtual hard disk to another VM</span></span>
<span data-ttu-id="9e16e-147">В следующих нескольких шагах описывается использование другой виртуальной машины для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="9e16e-147">For the next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="9e16e-148">Присоедините существующий виртуальный жесткий диск к виртуальной машине для устранения неполадок, чтобы просматривать и изменять содержимое диска.</span><span class="sxs-lookup"><span data-stu-id="9e16e-148">You attach the existing virtual hard disk to this troubleshooting VM to browse and edit the disk's content.</span></span> <span data-ttu-id="9e16e-149">Этот процесс позволяет, например, исправить ошибки конфигурации или изучить дополнительные журналы протоколов или системы.</span><span class="sxs-lookup"><span data-stu-id="9e16e-149">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="9e16e-150">Выберите или создайте другую виртуальную машину, которая будет использоваться для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="9e16e-150">Choose or create another VM to use for troubleshooting purposes.</span></span>

<span data-ttu-id="9e16e-151">При присоединении существующего виртуального жесткого диска укажите URL-адрес диска, полученный в предыдущей команде `azure vm show`.</span><span class="sxs-lookup"><span data-stu-id="9e16e-151">When you attach the existing virtual hard disk, specify the URL to the disk obtained in the preceding `azure vm show` command.</span></span> <span data-ttu-id="9e16e-152">В следующем примере существующий виртуальный жесткий диск присоединяется к виртуальной машине для устранения неполадок `myVMRecovery` в группе ресурсов `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="9e16e-152">The following example attaches an existing virtual hard disk to the troubleshooting VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm disk attach --resource-group myResourceGroup --name myVMRecovery \
    --vhd-url https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-the-attached-data-disk"></a><span data-ttu-id="9e16e-153">Подключение присоединенного диска данных</span><span class="sxs-lookup"><span data-stu-id="9e16e-153">Mount the attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="9e16e-154">В следующих примерах описана процедура для виртуальной машины Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="9e16e-154">The following examples detail the steps required on an Ubuntu VM.</span></span> <span data-ttu-id="9e16e-155">Если вы используете другой дистрибутив Linux, например Red Hat Enterprise Linux или SUSE, команды `mount` и расположение файлов журнала могут немного отличаться.</span><span class="sxs-lookup"><span data-stu-id="9e16e-155">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, the log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="9e16e-156">Используйте документацию к своему дистрибутиву, чтобы скорректировать команды соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="9e16e-156">Refer to the documentation for your specific distro for the appropriate changes in commands.</span></span>

1. <span data-ttu-id="9e16e-157">Подключитесь к виртуальной машине для устранения неполадок по протоколу SSH, используя соответствующие учетные данные.</span><span class="sxs-lookup"><span data-stu-id="9e16e-157">SSH to your troubleshooting VM using the appropriate credentials.</span></span> <span data-ttu-id="9e16e-158">Если присоединенный диск является первым диском данных на этой виртуальной машине, он скорее всего подключен к `/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="9e16e-158">If this disk is the first data disk attached to your troubleshooting VM, the disk is likely connected to `/dev/sdc`.</span></span> <span data-ttu-id="9e16e-159">Запустите команду `dmseg`, чтобы просмотреть присоединенные диски:</span><span class="sxs-lookup"><span data-stu-id="9e16e-159">Use `dmseg` to view attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```

    <span data-ttu-id="9e16e-160">Вы должны увидеть результат, аналогичный приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="9e16e-160">The output is similar to the following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="9e16e-161">В предыдущем примере диск операционной системы расположен в `/dev/sda`, а временный диск, предоставляемый для каждой виртуальной машины, расположен в `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="9e16e-161">In the preceding example, the OS disk is at `/dev/sda` and the temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="9e16e-162">Если у вас несколько дисков данных, они будут присоединены как `/dev/sdd`, `/dev/sde` и т. д.</span><span class="sxs-lookup"><span data-stu-id="9e16e-162">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="9e16e-163">Создайте каталог для подключения существующего виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="9e16e-163">Create a directory to mount your existing virtual hard disk.</span></span> <span data-ttu-id="9e16e-164">Следующая команда создает каталог с именем `troubleshootingdisk`.</span><span class="sxs-lookup"><span data-stu-id="9e16e-164">The following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="9e16e-165">Если на существующем виртуальном жестком диске есть несколько разделов, подключите нужный.</span><span class="sxs-lookup"><span data-stu-id="9e16e-165">If you have multiple partitions on your existing virtual hard disk, mount the required partition.</span></span> <span data-ttu-id="9e16e-166">Следующая команда подключает первый основной разделу к каталогу `/dev/sdc1`.</span><span class="sxs-lookup"><span data-stu-id="9e16e-166">The following example mounts the first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="9e16e-167">Мы рекомендуем подключать диски данных к виртуальным машинам Azure с использованием глобального уникального идентификатора (UUID) виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="9e16e-167">Best practice is to mount data disks on VMs in Azure using the universally unique identifier (UUID) of the virtual hard disk.</span></span> <span data-ttu-id="9e16e-168">Для нашего упрощенного примера по устранению неполадок можно и не использовать UUID для подключения диска.</span><span class="sxs-lookup"><span data-stu-id="9e16e-168">For this short troubleshooting scenario, mounting the virtual hard disk using the UUID is not necessary.</span></span> <span data-ttu-id="9e16e-169">Но в обычной ситуации, если вы измените `/etc/fstab` так, чтобы виртуальные жесткие диски подключались по имени устройства вместо UUID, у виртуальной машины могут быть проблемы с загрузкой.</span><span class="sxs-lookup"><span data-stu-id="9e16e-169">However, under normal use, editing `/etc/fstab` to mount virtual hard disks using device name rather than UUID may cause the VM to fail to boot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="9e16e-170">Устранение неполадок на исходном виртуальном жестком диске</span><span class="sxs-lookup"><span data-stu-id="9e16e-170">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="9e16e-171">Теперь, когда существующий виртуальный жесткий диск подключен, вы можете выполнить любые необходимые действия по обслуживанию и (или) устранению неполадок.</span><span class="sxs-lookup"><span data-stu-id="9e16e-171">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="9e16e-172">После устранения проблем выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9e16e-172">Once you have addressed the issues, continue with the following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="9e16e-173">Отключение и отсоединение исходного виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="9e16e-173">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="9e16e-174">После устранения ошибок отключите и отсоедините существующий виртуальный жесткий диск от виртуальной машины, использованный для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="9e16e-174">Once your errors are resolved, you unmount and detach the existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="9e16e-175">Виртуальный жесткий диск нельзя использовать с другой виртуальной машиной, пока вы не отмените аренду, присоединяющую виртуальный жесткий диск к виртуальной машине для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="9e16e-175">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span></span>

1. <span data-ttu-id="9e16e-176">Используя открытый сеанс подключения по SSH к виртуальной машине для устранения неполадок, отключите существующий виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="9e16e-176">From the SSH session to your troubleshooting VM, unmount the existing virtual hard disk.</span></span> <span data-ttu-id="9e16e-177">Прежде всего выйдите из каталога, в котором создана точка подключения.</span><span class="sxs-lookup"><span data-stu-id="9e16e-177">Change out of the parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="9e16e-178">Теперь отключите существующий виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="9e16e-178">Now unmount the existing virtual hard disk.</span></span> <span data-ttu-id="9e16e-179">В следующем примере диск отключается от каталога `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="9e16e-179">The following example unmounts the device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="9e16e-180">Теперь отсоедините виртуальный жесткий диск от виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="9e16e-180">Now detach the virtual hard disk from the VM.</span></span> <span data-ttu-id="9e16e-181">Выйдите из сеанса SSH и вернитесь к виртуальной машине для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="9e16e-181">Exit the SSH session to your troubleshooting VM.</span></span> <span data-ttu-id="9e16e-182">В Azure CLI сначала укажите диски данных, подключенные к виртуальной машине для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="9e16e-182">In the Azure CLI, first list the attached data disks to your troubleshooting VM.</span></span> <span data-ttu-id="9e16e-183">В следующем примере указываются диски данных, подключенные к виртуальной машине `myVMRecovery` в группе ресурсов `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="9e16e-183">The following example lists the data disks attached to the VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    azure vm disk list --resource-group myResourceGroup --vm-name myVMRecovery
    ```

    <span data-ttu-id="9e16e-184">Обратите внимание на значение `Lun` для существующего виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="9e16e-184">Note the `Lun` value for your existing virtual hard disk.</span></span> <span data-ttu-id="9e16e-185">В следующем примере выходных данных команды показан существующий виртуальный диска, подключенный к логическому устройству с номером 0:</span><span class="sxs-lookup"><span data-stu-id="9e16e-185">The following example command output shows the existing virtual disk attached at LUN 0:</span></span>

    ```azurecli
    info:    Executing command vm disk list
    + Looking up the VM "myVMRecovery"
    data:    Name              Lun  DiskSizeGB  Caching  URI
    data:    ------            ---  ----------  -------  ------------------------------------------------------------------------
    data:    myVM              0                None     https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    info:    vm disk list command OK
    ```

    <span data-ttu-id="9e16e-186">Отсоедините диск данных от виртуальной машины, используя применимое значение `Lun`:</span><span class="sxs-lookup"><span data-stu-id="9e16e-186">Detach the data disk from your VM using the applicable `Lun` value:</span></span>

    ```azurecli
    azure vm disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --lun 0
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="9e16e-187">Создание виртуальной машины из исходного жесткого диска</span><span class="sxs-lookup"><span data-stu-id="9e16e-187">Create VM from original hard disk</span></span>
<span data-ttu-id="9e16e-188">Чтобы создать виртуальную машину из исходного виртуального жесткого диска, используйте [этот шаблон Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="9e16e-188">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span></span> <span data-ttu-id="9e16e-189">Фактический шаблон JSON доступен по следующей ссылке:</span><span class="sxs-lookup"><span data-stu-id="9e16e-189">The actual JSON template is at the following link:</span></span>

- <span data-ttu-id="9e16e-190">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="9e16e-190">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span></span>

<span data-ttu-id="9e16e-191">Этот шаблон развертывает виртуальную машину в существующую виртуальную сеть, используя URL-адрес виртуального жесткого диска из использованной выше команды.</span><span class="sxs-lookup"><span data-stu-id="9e16e-191">The template deploys a VM into an existing virtual network, using the VHD URL from the earlier command.</span></span> <span data-ttu-id="9e16e-192">В следующем примере шаблон развертывается в группе ресурсов `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="9e16e-192">The following example deploys the template to the resource group named `myResourceGroup`:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup --name myDeployment \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

<span data-ttu-id="9e16e-193">Укажите сведения на запросы шаблона, такие как имя виртуальной машины (`myDeployedVM` в приведенном ниже примере), тип операционной системы (`Linux`) и размер виртуальной машины (`Standard_DS1_v2`).</span><span class="sxs-lookup"><span data-stu-id="9e16e-193">Answer the prompts for the template such as VM name (`myDeployedVM` the following example), OS type (`Linux`), and VM size (`Standard_DS1_v2`).</span></span> <span data-ttu-id="9e16e-194">Используется то же значение `osDiskVhdUri`, что и при присоединении существующего виртуального жесткого диска к виртуальной машине для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="9e16e-194">The `osDiskVhdUri` is the same as previously used when attaching the existing virtual hard disk to the troubleshooting VM.</span></span> <span data-ttu-id="9e16e-195">Пример выходных данных команды и запросы выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9e16e-195">An example of the command output and prompts is as follows:</span></span>

```azurecli
info:    Executing command group deployment create
info:    Supply values for the following parameters
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
+ Waiting for deployment to complete
+
```


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="9e16e-196">Восстановление диагностики загрузки</span><span class="sxs-lookup"><span data-stu-id="9e16e-196">Re-enable boot diagnostics</span></span>

<span data-ttu-id="9e16e-197">При создании виртуальной машины на основе существующего виртуального жесткого диска диагностика загрузки не всегда автоматически включена.</span><span class="sxs-lookup"><span data-stu-id="9e16e-197">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="9e16e-198">В следующем примере на виртуальной машине `myDeployedVM` в группе ресурсов `myResourceGroup` включается расширение диагностики:</span><span class="sxs-lookup"><span data-stu-id="9e16e-198">The following example enables the diagnostic extension on the VM named `myDeployedVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm enable-diag --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a><span data-ttu-id="9e16e-199">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9e16e-199">Next steps</span></span>
<span data-ttu-id="9e16e-200">При возникновении проблем с подключением к виртуальной машине см. статью [Устранение неполадок с SSH-подключением к виртуальной машине Azure Linux: сбой, ошибка или отклонение](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9e16e-200">If you are having issues connecting to your VM, see [Troubleshoot SSH connections to an Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="9e16e-201">Для решения проблем с доступом к приложениям, выполняющимся на виртуальной машине, см. статью [Устранение проблем с подключением к приложениям на виртуальных машинах Linux в Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9e16e-201">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>