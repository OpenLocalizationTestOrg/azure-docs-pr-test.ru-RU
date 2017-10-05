---
title: "Расширение виртуальных жестких дисков виртуальной машины Linux в Azure | Документация Майкрософт"
description: "Узнайте, как расширить виртуальные жесткие диски на виртуальной машине Linux с помощью Azure CLI 2.0"
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
ms.openlocfilehash: b82cc0473c003da767ee230ab485c69b233977d1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-expand-virtual-hard-disks-on-a-linux-vm-with-the-azure-cli"></a><span data-ttu-id="fce9f-103">Расширение виртуальных жестких дисков на виртуальной машине Linux с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="fce9f-103">How to expand virtual hard disks on a Linux VM with the Azure CLI</span></span>
<span data-ttu-id="fce9f-104">Как правило, размер виртуального жесткого диска по умолчанию для операционной системы на виртуальной машине Linux в Azure составляет 30 ГБ.</span><span class="sxs-lookup"><span data-stu-id="fce9f-104">The default virtual hard disk size for the operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span></span> <span data-ttu-id="fce9f-105">Вы можете [добавить диски данных](add-disk.md), чтобы предоставить дополнительное место для хранения, а также расширить существующий диск данных.</span><span class="sxs-lookup"><span data-stu-id="fce9f-105">You can [add data disks](add-disk.md) to provide for additional storage space, but you may also wish to expand an existing data disk.</span></span> <span data-ttu-id="fce9f-106">В этой статье подробно описано, как расширить управляемые диски для виртуальной машины Linux с помощью Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="fce9f-106">This article details how to expand managed disks for a Linux VM with the Azure CLI 2.0.</span></span> <span data-ttu-id="fce9f-107">С помощью [Azure CLI 1.0](expand-disks-nodejs.md) можно также расширить неуправляемые диски операционной системы.</span><span class="sxs-lookup"><span data-stu-id="fce9f-107">You can also expand the unmanaged OS disk with the [Azure CLI 1.0](expand-disks-nodejs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="fce9f-108">Всегда проверяйте, созданы ли резервные копии данных, прежде чем выполнять операции по изменению размера диска.</span><span class="sxs-lookup"><span data-stu-id="fce9f-108">Always make sure that you back up your data before you perform disk resize operations.</span></span> <span data-ttu-id="fce9f-109">Дополнительные сведения см. в статье [Архивация виртуальных машин Linux в Azure](tutorial-backup-vms.md).</span><span class="sxs-lookup"><span data-stu-id="fce9f-109">For more information, see [Back up Linux VMs in Azure](tutorial-backup-vms.md).</span></span>

## <a name="expand-disk"></a><span data-ttu-id="fce9f-110">Расширение диска</span><span class="sxs-lookup"><span data-stu-id="fce9f-110">Expand disk</span></span>
<span data-ttu-id="fce9f-111">Обязательно установите последнюю версию [Azure CLI 2.0](/cli/azure/install-az-cli2) и войдите в учетную запись Azure с помощью команды [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="fce9f-111">Make sure that you have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="fce9f-112">Для этой статьи потребуется существующая виртуальная машина в Azure с хотя бы одним подключенным и подготовленным диском данных.</span><span class="sxs-lookup"><span data-stu-id="fce9f-112">This article requires an existing VM in Azure with at least one data disk attached and prepared.</span></span> <span data-ttu-id="fce9f-113">Если у вас нет виртуальной машины, которую можно использовать, см. раздел [о создании и подготовке виртуальной машины с дисками данных](tutorial-manage-disks.md#create-and-attach-disks).</span><span class="sxs-lookup"><span data-stu-id="fce9f-113">If you do not already have a VM that you can use, see [Create and prepare a VM with data disks](tutorial-manage-disks.md#create-and-attach-disks).</span></span>

<span data-ttu-id="fce9f-114">В следующих примерах замените имена параметров собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="fce9f-114">In the following samples, replace example parameter names with your own values.</span></span> <span data-ttu-id="fce9f-115">Примеры имен параметров: *myResourceGroup* и *myVM*.</span><span class="sxs-lookup"><span data-stu-id="fce9f-115">Example parameter names include *myResourceGroup* and *myVM*.</span></span>

1. <span data-ttu-id="fce9f-116">Нельзя выполнять операции с виртуальными жесткими дисками на работающей виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="fce9f-116">Operations on virtual hard disks cannot be performed with the VM running.</span></span> <span data-ttu-id="fce9f-117">Отмените подготовку виртуальной машины, выполнив команду [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="fce9f-117">Deallocate your VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="fce9f-118">В следующем примере отменяется распределение виртуальной машины *myVM*, входящей в группу ресурсов с именем *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="fce9f-118">The following example deallocates the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > <span data-ttu-id="fce9f-119">Операция `az vm stop` не освобождает вычислительные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="fce9f-119">`az vm stop` does not release the compute resources.</span></span> <span data-ttu-id="fce9f-120">Чтобы освободить вычислительные ресурсы, используйте `az vm deallocate`.</span><span class="sxs-lookup"><span data-stu-id="fce9f-120">To release compute resources, use `az vm deallocate`.</span></span> <span data-ttu-id="fce9f-121">Для расширения виртуального жесткого диска следует отменить распределение виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="fce9f-121">The VM must be deallocated to expand the virtual hard disk.</span></span>

2. <span data-ttu-id="fce9f-122">Просмотрите список управляемых дисков в группе ресурсов, выполнив команду [az disk list](/cli/azure/disk#list).</span><span class="sxs-lookup"><span data-stu-id="fce9f-122">View a list of managed disks in a resource group with [az disk list](/cli/azure/disk#list).</span></span> <span data-ttu-id="fce9f-123">В следующем примере выводится список управляемых дисков, входящих в группу ресурсов с именем *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="fce9f-123">The following example displays a list of managed disks in the resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az disk list \
        --resource-group myResourceGroup \
        --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
        --output table
    ```

    <span data-ttu-id="fce9f-124">Расширьте диск, выполнив команду [az disk update](/cli/azure/disk#update).</span><span class="sxs-lookup"><span data-stu-id="fce9f-124">Expand the required disk with [az disk update](/cli/azure/disk#update).</span></span> <span data-ttu-id="fce9f-125">В следующем примере размер управляемого диска *myDataDisk* увеличивается до *200* ГБ:</span><span class="sxs-lookup"><span data-stu-id="fce9f-125">The following example expands the managed disk named *myDataDisk* to be *200*Gb in size:</span></span>

    ```azurecli
    az disk update \
        --resource-group myResourceGroup \
        --name myDataDisk \
        --size-gb 200
    ```

    > [!NOTE]
    > <span data-ttu-id="fce9f-126">При расширении управляемого диска его новый размер сопоставляется с размером ближайшего управляемого диска.</span><span class="sxs-lookup"><span data-stu-id="fce9f-126">When you expand a managed disk, the updated size is mapped to the nearest managed disk size.</span></span> <span data-ttu-id="fce9f-127">Таблица с размерами и ценовыми категориями доступных управляемых дисков доступна в разделе [Цены и выставление счетов](../windows/managed-disks-overview.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="fce9f-127">For a table of the available managed disk sizes and tiers, see [Azure Managed Disks Overview - Pricing and Billing](../windows/managed-disks-overview.md#pricing-and-billing).</span></span>

3. <span data-ttu-id="fce9f-128">Запустите виртуальную машину, выполнив команду [az vm start](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="fce9f-128">Start your VM with [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="fce9f-129">В следующем примере запускается виртуальная машина *myVM*, входящая в группу ресурсов с именем *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="fce9f-129">The following example starts the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="fce9f-130">Подключитесь к виртуальной машине по протоколу SSH, используя соответствующие учетные данные.</span><span class="sxs-lookup"><span data-stu-id="fce9f-130">SSH to your VM with the appropriate credentials.</span></span> <span data-ttu-id="fce9f-131">Вы можете получить общедоступный IP-адрес виртуальной машины с помощью команды [az vm show](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="fce9f-131">You can obtain the public IP address of your VM with [az vm show](/cli/azure/vm#show):</span></span>

    ```azurecli
    az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
    ```

5. <span data-ttu-id="fce9f-132">Чтобы использовать развернутый диск, необходимо развернуть основной раздел и файловую систему.</span><span class="sxs-lookup"><span data-stu-id="fce9f-132">To use the expanded disk, you need to expand the underlying partition and filesystem.</span></span>

    <span data-ttu-id="fce9f-133">а.</span><span class="sxs-lookup"><span data-stu-id="fce9f-133">a.</span></span> <span data-ttu-id="fce9f-134">Если диск подключен, отключите его.</span><span class="sxs-lookup"><span data-stu-id="fce9f-134">If already mounted, unmount the disk:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

    <span data-ttu-id="fce9f-135">b.</span><span class="sxs-lookup"><span data-stu-id="fce9f-135">b.</span></span> <span data-ttu-id="fce9f-136">Чтобы просмотреть сведения о диске и изменить размер раздела, используйте команду `parted`.</span><span class="sxs-lookup"><span data-stu-id="fce9f-136">Use `parted` to view disk information and resize the partition:</span></span>

    ```bash
    sudo parted /dev/sdc
    ```

    <span data-ttu-id="fce9f-137">Просмотрите сведения о структуре существующего раздела с помощью команды `print`.</span><span class="sxs-lookup"><span data-stu-id="fce9f-137">View information about the existing partition layout with `print`.</span></span> <span data-ttu-id="fce9f-138">В результате будут выведены выходные данные, как в примере ниже, указывающие, что размер основного диска составляет 215 ГБ.</span><span class="sxs-lookup"><span data-stu-id="fce9f-138">The output is similar to the following example, which shows the underlying disk is 215Gb in size:</span></span>

    ```bash
    GNU Parted 3.2
    Using /dev/sdc1
    Welcome to GNU Parted! Type 'help' to view a list of commands.
    (parted) print
    Model: Unknown Msft Virtual Disk (scsi)
    Disk /dev/sdc1: 215GB
    Sector size (logical/physical): 512B/4096B
    Partition Table: loop
    Disk Flags:
    
    Number  Start  End    Size   File system  Flags
        1      0.00B  107GB  107GB  ext4
    ```

    <span data-ttu-id="fce9f-139">c.</span><span class="sxs-lookup"><span data-stu-id="fce9f-139">c.</span></span> <span data-ttu-id="fce9f-140">Разверните раздел с помощью команды `resizepart`.</span><span class="sxs-lookup"><span data-stu-id="fce9f-140">Expand the partition with `resizepart`.</span></span> <span data-ttu-id="fce9f-141">Введите номер (*1*) и размер для нового раздела.</span><span class="sxs-lookup"><span data-stu-id="fce9f-141">Enter the partition number, *1*, and a size for the new partition:</span></span>

    ```bash
    (parted) resizepart
    Partition number? 1
    End?  [107GB]? 215GB
    ```

    <span data-ttu-id="fce9f-142">d.</span><span class="sxs-lookup"><span data-stu-id="fce9f-142">d.</span></span> <span data-ttu-id="fce9f-143">Чтобы закрыть командную строку, введите `quit`.</span><span class="sxs-lookup"><span data-stu-id="fce9f-143">To exit, enter `quit`</span></span>

5. <span data-ttu-id="fce9f-144">Изменив размер раздела, проверьте его целостность с помощью команды `e2fsck`.</span><span class="sxs-lookup"><span data-stu-id="fce9f-144">With the partition resized, verify the partition consistency with `e2fsck`:</span></span>

    ```bash
    sudo e2fsck -f /dev/sdc1
    ```

6. <span data-ttu-id="fce9f-145">Теперь измените размер файловой системы, выполнив команду `resize2fs`.</span><span class="sxs-lookup"><span data-stu-id="fce9f-145">Now resize the filesystem with `resize2fs`:</span></span>

    ```bash
    sudo resize2fs /dev/sdc1
    ```

7. <span data-ttu-id="fce9f-146">Подключите раздел к необходимому расположению, например `/datadrive`.</span><span class="sxs-lookup"><span data-stu-id="fce9f-146">Mount the partition to the desired location, such as `/datadrive`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```

8. <span data-ttu-id="fce9f-147">Чтобы проверить, изменился ли размер диска операционной системы, используйте `df -h`.</span><span class="sxs-lookup"><span data-stu-id="fce9f-147">To verify the OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="fce9f-148">В следующем примере выходных данных показано, что теперь размер основного раздела (*/dev/sdc1*) составляет 200 ГБ:</span><span class="sxs-lookup"><span data-stu-id="fce9f-148">The following example output shows the data drive, */dev/sdc1*, is now 200 GB:</span></span>

    ```bash
    Filesystem      Size   Used  Avail Use% Mounted on
    /dev/sdc1        197G   60M   187G   1% /datadrive
    ```

## <a name="next-steps"></a><span data-ttu-id="fce9f-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fce9f-149">Next steps</span></span>
<span data-ttu-id="fce9f-150">Если вам требуется дополнительное место для хранения, можно также [добавить диски данных в виртуальную машину Linux](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="fce9f-150">If you need additional storage, you also [add data disks to a Linux VM](add-disk.md).</span></span> <span data-ttu-id="fce9f-151">Дополнительные сведения о шифровании диска см. в статье [Encrypt disks on a Linux VM using the Azure CLI](encrypt-disks.md) (Шифрование дисков на виртуальной машине Linux с помощью Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="fce9f-151">For more information about disk encryption, see [Encrypt disks on a Linux VM using the Azure CLI](encrypt-disks.md).</span></span>
