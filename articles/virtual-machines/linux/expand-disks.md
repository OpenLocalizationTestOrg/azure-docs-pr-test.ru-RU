---
title: "aaaExpand виртуальных жестких дисков на виртуальной Машине Linux в Azure | Документы Microsoft"
description: "Узнайте, как tooexpand виртуальных жестких дисков на виртуальной Машине Linux с hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: 7c09a682cb4322c027e57667640e8f1f8e6612f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooexpand-virtual-hard-disks-on-a-linux-vm-with-hello-azure-cli"></a><span data-ttu-id="e8df7-103">Как tooexpand виртуальных жестких дисков на виртуальной Машине Linux с hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e8df7-103">How tooexpand virtual hard disks on a Linux VM with hello Azure CLI</span></span>
<span data-ttu-id="e8df7-104">размер виртуального жесткого диска по умолчанию Hello hello операционной системы (ОС) обычно составляет 30 ГБ на виртуальной машине (VM) Linux в Azure.</span><span class="sxs-lookup"><span data-stu-id="e8df7-104">hello default virtual hard disk size for hello operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span></span> <span data-ttu-id="e8df7-105">Вы можете [добавить диски данных](add-disk.md) tooprovide для дополнительного пространства хранилища, но вы также можете tooexpand существующий диск данных.</span><span class="sxs-lookup"><span data-stu-id="e8df7-105">You can [add data disks](add-disk.md) tooprovide for additional storage space, but you may also wish tooexpand an existing data disk.</span></span> <span data-ttu-id="e8df7-106">В этой статье указаны как tooexpand управление диски для виртуальной Машины Linux с hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="e8df7-106">This article details how tooexpand managed disks for a Linux VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="e8df7-107">Можно также развернуть диск ОС hello неуправляемого с hello [Azure CLI 1.0](expand-disks-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="e8df7-107">You can also expand hello unmanaged OS disk with hello [Azure CLI 1.0](expand-disks-nodejs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="e8df7-108">Всегда проверяйте, созданы ли резервные копии данных, прежде чем выполнять операции по изменению размера диска.</span><span class="sxs-lookup"><span data-stu-id="e8df7-108">Always make sure that you back up your data before you perform disk resize operations.</span></span> <span data-ttu-id="e8df7-109">Дополнительные сведения см. в статье [Архивация виртуальных машин Linux в Azure](tutorial-backup-vms.md).</span><span class="sxs-lookup"><span data-stu-id="e8df7-109">For more information, see [Back up Linux VMs in Azure](tutorial-backup-vms.md).</span></span>

## <a name="expand-disk"></a><span data-ttu-id="e8df7-110">Расширение диска</span><span class="sxs-lookup"><span data-stu-id="e8df7-110">Expand disk</span></span>
<span data-ttu-id="e8df7-111">Убедитесь, что hello последней [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="e8df7-111">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="e8df7-112">Для этой статьи потребуется существующая виртуальная машина в Azure с хотя бы одним подключенным и подготовленным диском данных.</span><span class="sxs-lookup"><span data-stu-id="e8df7-112">This article requires an existing VM in Azure with at least one data disk attached and prepared.</span></span> <span data-ttu-id="e8df7-113">Если у вас нет виртуальной машины, которую можно использовать, см. раздел [о создании и подготовке виртуальной машины с дисками данных](tutorial-manage-disks.md#create-and-attach-disks).</span><span class="sxs-lookup"><span data-stu-id="e8df7-113">If you do not already have a VM that you can use, see [Create and prepare a VM with data disks](tutorial-manage-disks.md#create-and-attach-disks).</span></span>

<span data-ttu-id="e8df7-114">В hello следующим примерам, замените имена параметров примере собственные значения.</span><span class="sxs-lookup"><span data-stu-id="e8df7-114">In hello following samples, replace example parameter names with your own values.</span></span> <span data-ttu-id="e8df7-115">Примеры имен параметров: *myResourceGroup* и *myVM*.</span><span class="sxs-lookup"><span data-stu-id="e8df7-115">Example parameter names include *myResourceGroup* and *myVM*.</span></span>

1. <span data-ttu-id="e8df7-116">Невозможно выполнить операции для виртуальных жестких дисков с hello виртуальной Машины под управлением.</span><span class="sxs-lookup"><span data-stu-id="e8df7-116">Operations on virtual hard disks cannot be performed with hello VM running.</span></span> <span data-ttu-id="e8df7-117">Отмените подготовку виртуальной машины, выполнив команду [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="e8df7-117">Deallocate your VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="e8df7-118">Hello следующий пример отменяет выделение hello виртуальной Машины с именем *myVM* в группе ресурсов hello с именем *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="e8df7-118">hello following example deallocates hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > <span data-ttu-id="e8df7-119">`az vm stop`не освобождает hello вычислительных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e8df7-119">`az vm stop` does not release hello compute resources.</span></span> <span data-ttu-id="e8df7-120">toorelease вычислительных ресурсов, используйте `az vm deallocate`.</span><span class="sxs-lookup"><span data-stu-id="e8df7-120">toorelease compute resources, use `az vm deallocate`.</span></span> <span data-ttu-id="e8df7-121">Hello виртуальная машина должна быть освобождена tooexpand hello виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="e8df7-121">hello VM must be deallocated tooexpand hello virtual hard disk.</span></span>

2. <span data-ttu-id="e8df7-122">Просмотрите список управляемых дисков в группе ресурсов, выполнив команду [az disk list](/cli/azure/disk#list).</span><span class="sxs-lookup"><span data-stu-id="e8df7-122">View a list of managed disks in a resource group with [az disk list](/cli/azure/disk#list).</span></span> <span data-ttu-id="e8df7-123">Hello следующий пример отображает список управляемых дисков в группе ресурсов hello с именем *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="e8df7-123">hello following example displays a list of managed disks in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az disk list \
        --resource-group myResourceGroup \
        --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
        --output table
    ```

    <span data-ttu-id="e8df7-124">Разверните hello диска с [обновление диска az](/cli/azure/disk#update).</span><span class="sxs-lookup"><span data-stu-id="e8df7-124">Expand hello required disk with [az disk update](/cli/azure/disk#update).</span></span> <span data-ttu-id="e8df7-125">Hello следующий пример расширяет hello управляемого диска с именем *myDataDisk* toobe *200*ГБ:</span><span class="sxs-lookup"><span data-stu-id="e8df7-125">hello following example expands hello managed disk named *myDataDisk* toobe *200*Gb in size:</span></span>

    ```azurecli
    az disk update \
        --resource-group myResourceGroup \
        --name myDataDisk \
        --size-gb 200
    ```

    > [!NOTE]
    > <span data-ttu-id="e8df7-126">При развертывании управляемого диска hello обновить размер — сопоставленных toohello ближайший размер управляемого диска.</span><span class="sxs-lookup"><span data-stu-id="e8df7-126">When you expand a managed disk, hello updated size is mapped toohello nearest managed disk size.</span></span> <span data-ttu-id="e8df7-127">Таблицы размеров свободного управляемого hello и уровней, см. [Azure диски Обзор управляемых - цены и выставление счетов](../windows/managed-disks-overview.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="e8df7-127">For a table of hello available managed disk sizes and tiers, see [Azure Managed Disks Overview - Pricing and Billing](../windows/managed-disks-overview.md#pricing-and-billing).</span></span>

3. <span data-ttu-id="e8df7-128">Запустите виртуальную машину, выполнив команду [az vm start](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="e8df7-128">Start your VM with [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="e8df7-129">Следующий пример запускает Hello hello виртуальной Машины с именем *myVM* в группе ресурсов hello с именем *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="e8df7-129">hello following example starts hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="e8df7-130">Tooyour SSH виртуальных Машин с соответствующими учетными данными hello.</span><span class="sxs-lookup"><span data-stu-id="e8df7-130">SSH tooyour VM with hello appropriate credentials.</span></span> <span data-ttu-id="e8df7-131">Можно получить hello общедоступный IP-адрес виртуальной Машины с [Показать ВМ az](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="e8df7-131">You can obtain hello public IP address of your VM with [az vm show](/cli/azure/vm#show):</span></span>

    ```azurecli
    az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
    ```

5. <span data-ttu-id="e8df7-132">toouse hello развернуто диска, раздел hello tooexpand и файловой системы.</span><span class="sxs-lookup"><span data-stu-id="e8df7-132">toouse hello expanded disk, you need tooexpand hello underlying partition and filesystem.</span></span>

    <span data-ttu-id="e8df7-133">а.</span><span class="sxs-lookup"><span data-stu-id="e8df7-133">a.</span></span> <span data-ttu-id="e8df7-134">Если уже подключен, отключите hello диска:</span><span class="sxs-lookup"><span data-stu-id="e8df7-134">If already mounted, unmount hello disk:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

    <span data-ttu-id="e8df7-135">b.</span><span class="sxs-lookup"><span data-stu-id="e8df7-135">b.</span></span> <span data-ttu-id="e8df7-136">Используйте `parted` tooview сведения на диске и размер раздела hello:</span><span class="sxs-lookup"><span data-stu-id="e8df7-136">Use `parted` tooview disk information and resize hello partition:</span></span>

    ```bash
    sudo parted /dev/sdc
    ```

    <span data-ttu-id="e8df7-137">Просмотр сведений о hello существующего раздела макета с `print`.</span><span class="sxs-lookup"><span data-stu-id="e8df7-137">View information about hello existing partition layout with `print`.</span></span> <span data-ttu-id="e8df7-138">Hello выходных данных примерно toohello следующий пример, который показывает, что базовый диск hello имеет размер в ГБ 215:</span><span class="sxs-lookup"><span data-stu-id="e8df7-138">hello output is similar toohello following example, which shows hello underlying disk is 215Gb in size:</span></span>

    ```bash
    GNU Parted 3.2
    Using /dev/sdc1
    Welcome tooGNU Parted! Type 'help' tooview a list of commands.
    (parted) print
    Model: Unknown Msft Virtual Disk (scsi)
    Disk /dev/sdc1: 215GB
    Sector size (logical/physical): 512B/4096B
    Partition Table: loop
    Disk Flags:
    
    Number  Start  End    Size   File system  Flags
        1      0.00B  107GB  107GB  ext4
    ```

    <span data-ttu-id="e8df7-139">c.</span><span class="sxs-lookup"><span data-stu-id="e8df7-139">c.</span></span> <span data-ttu-id="e8df7-140">Разверните секцию hello с `resizepart`.</span><span class="sxs-lookup"><span data-stu-id="e8df7-140">Expand hello partition with `resizepart`.</span></span> <span data-ttu-id="e8df7-141">Введите номер секции hello, *1*и размер для новой секции hello:</span><span class="sxs-lookup"><span data-stu-id="e8df7-141">Enter hello partition number, *1*, and a size for hello new partition:</span></span>

    ```bash
    (parted) resizepart
    Partition number? 1
    End?  [107GB]? 215GB
    ```

    <span data-ttu-id="e8df7-142">d.</span><span class="sxs-lookup"><span data-stu-id="e8df7-142">d.</span></span> <span data-ttu-id="e8df7-143">tooexit, введите`quit`</span><span class="sxs-lookup"><span data-stu-id="e8df7-143">tooexit, enter `quit`</span></span>

5. <span data-ttu-id="e8df7-144">С секцией hello изменения размеров, проверки согласованности секции hello с `e2fsck`:</span><span class="sxs-lookup"><span data-stu-id="e8df7-144">With hello partition resized, verify hello partition consistency with `e2fsck`:</span></span>

    ```bash
    sudo e2fsck -f /dev/sdc1
    ```

6. <span data-ttu-id="e8df7-145">Теперь измените размер hello файловой системы с `resize2fs`:</span><span class="sxs-lookup"><span data-stu-id="e8df7-145">Now resize hello filesystem with `resize2fs`:</span></span>

    ```bash
    sudo resize2fs /dev/sdc1
    ```

7. <span data-ttu-id="e8df7-146">Подключения hello секции toohello требуемого расположения, такие как `/datadrive`:</span><span class="sxs-lookup"><span data-stu-id="e8df7-146">Mount hello partition toohello desired location, such as `/datadrive`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```

8. <span data-ttu-id="e8df7-147">диск ОС hello tooverify был изменен, используйте `df -h`.</span><span class="sxs-lookup"><span data-stu-id="e8df7-147">tooverify hello OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="e8df7-148">Следующий пример выходных данных Hello показывает hello диска с данными, */dev/sdc1*, теперь составляет 200 ГБ:</span><span class="sxs-lookup"><span data-stu-id="e8df7-148">hello following example output shows hello data drive, */dev/sdc1*, is now 200 GB:</span></span>

    ```bash
    Filesystem      Size   Used  Avail Use% Mounted on
    /dev/sdc1        197G   60M   187G   1% /datadrive
    ```

## <a name="next-steps"></a><span data-ttu-id="e8df7-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e8df7-149">Next steps</span></span>
<span data-ttu-id="e8df7-150">Если требуется дополнительное хранилище, вы также [добавить tooa дисков данных виртуальной Машины с Linux](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="e8df7-150">If you need additional storage, you also [add data disks tooa Linux VM](add-disk.md).</span></span> <span data-ttu-id="e8df7-151">Дополнительные сведения о шифровании диска см. в разделе [шифрование дисков на виртуальной Машине Linux с помощью hello Azure CLI](encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="e8df7-151">For more information about disk encryption, see [Encrypt disks on a Linux VM using hello Azure CLI](encrypt-disks.md).</span></span>
