---
title: "Управляемые диски Azure. Преобразование виртуальной машины Linux с неуправляемыми дисками в Azure для использования управляемых дисков | Документация Майкрософт"
description: "Переключение виртуальной машины Linux, развернутой в рамках модели Resource Manager, с неуправляемых дисков на управляемые диски с помощью Azure CLI 2.0."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 94f8e3330fb2d6547811315fcfdb8ced338e0247
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="convert-a-linux-virtual-machine-from-unmanaged-disks-to-managed-disks"></a><span data-ttu-id="bfe5c-103">Переключение виртуальной машины Linux с неуправляемых дисков на управляемые диски</span><span class="sxs-lookup"><span data-stu-id="bfe5c-103">Convert a Linux virtual machine from unmanaged disks to managed disks</span></span>

<span data-ttu-id="bfe5c-104">При наличии виртуальных машин Linux, использующих неуправляемые диски, их можно преобразовать для использования управляемых дисков с помощью службы [Управляемые диски Azure](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bfe5c-104">If you have existing Linux virtual machines (VMs) that use unmanaged disks, you can convert the VMs to use managed disks through the [Azure Managed Disks](../windows/managed-disks-overview.md) service.</span></span> <span data-ttu-id="bfe5c-105">При этом преобразуются диск операционной системы и все подключенные диски данных.</span><span class="sxs-lookup"><span data-stu-id="bfe5c-105">This process converts both the OS disk and any attached data disks.</span></span>

<span data-ttu-id="bfe5c-106">В этой статье показано, как преобразовать виртуальные машины с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="bfe5c-106">This article shows you how to convert VMs by using the Azure CLI.</span></span> <span data-ttu-id="bfe5c-107">Если вам установить или обновить Azure CLI, ознакомьтесь со статьей [Установка Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="bfe5c-107">If you need to install or upgrade it, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="bfe5c-108">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="bfe5c-108">Before you begin</span></span>

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]


## <a name="convert-single-instance-vms"></a><span data-ttu-id="bfe5c-109">Преобразование одноэкземплярных виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="bfe5c-109">Convert single-instance VMs</span></span>
<span data-ttu-id="bfe5c-110">В этом разделе описывается, как преобразовать одноэкземплярные виртуальные машины Azure с неуправляемыми дисками, чтобы они могли использовать Управляемые диски.</span><span class="sxs-lookup"><span data-stu-id="bfe5c-110">This section covers how to convert single-instance Azure VMs from unmanaged disks to managed disks.</span></span> <span data-ttu-id="bfe5c-111">(Если виртуальные машины находятся в группе доступности, ознакомьтесь со следующим разделом.) Этот процесс позволяет переключить виртуальные машины с неуправляемых дисков уровня "Премиум" (SSD) на управляемые диски уровня "Премиум" или с неуправляемых дисков уровня "Стандартный" (жесткие диски) на управляемые диски уровня "Стандартный".</span><span class="sxs-lookup"><span data-stu-id="bfe5c-111">(If your VMs are in an availability set, see the next section.) You can use this process to convert the VMs from premium (SSD) unmanaged disks to premium managed disks, or from standard (HDD) unmanaged disks to standard managed disks.</span></span>

1. <span data-ttu-id="bfe5c-112">Отмените выделение виртуальной машины с помощью команды [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="bfe5c-112">Deallocate the VM by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="bfe5c-113">В следующем примере освобождается виртуальная машина `myVM`, входящая в группу ресурсов `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="bfe5c-113">The following example deallocates the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

2. <span data-ttu-id="bfe5c-114">Преобразуйте виртуальную машину для использования управляемых дисков, выполнив команду [az vm convert](/cli/azure/vm#convert).</span><span class="sxs-lookup"><span data-stu-id="bfe5c-114">Convert the VM to managed disks by using [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="bfe5c-115">Приведенный ниже процесс преобразовывает виртуальную машину `myVM`, включая ее диск ОС и все диски данных.</span><span class="sxs-lookup"><span data-stu-id="bfe5c-115">The following process converts the VM named `myVM`, including the OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="bfe5c-116">После преобразования запустите виртуальную машину командой [az vm start](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="bfe5c-116">Start the VM after the conversion to managed disks by using [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="bfe5c-117">В следующем примере запускается виртуальная машина `myVM` в группе ресурсов `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="bfe5c-117">The following example starts the VM named `myVM` in the resource group named `myResourceGroup`.</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="convert-vms-in-an-availability-set"></a><span data-ttu-id="bfe5c-118">Преобразование виртуальных машин в группе доступности</span><span class="sxs-lookup"><span data-stu-id="bfe5c-118">Convert VMs in an availability set</span></span>

<span data-ttu-id="bfe5c-119">Если виртуальные машины, которые вы хотите преобразовать для использования управляемых дисков, входят в группу доступности, то необходимо сначала преобразовать эту группу доступности в управляемую группу доступности.</span><span class="sxs-lookup"><span data-stu-id="bfe5c-119">If the VMs that you want to convert to managed disks are in an availability set, you first need to convert the availability set to a managed availability set.</span></span>

<span data-ttu-id="bfe5c-120">Перед преобразованием группы доступности нужно освободить все виртуальные машины в этой группе.</span><span class="sxs-lookup"><span data-stu-id="bfe5c-120">All VMs in the availability set must be deallocated before you convert the availability set.</span></span> <span data-ttu-id="bfe5c-121">Запланируйте преобразование всех виртуальных машин для использования управляемых дисков после того, как содержащая их группа доступности будет преобразована в управляемую группу доступности.</span><span class="sxs-lookup"><span data-stu-id="bfe5c-121">Plan to convert all VMs to managed disks after the availability set itself has been converted to a managed availability set.</span></span> <span data-ttu-id="bfe5c-122">Затем можно будет запустить все виртуальные машины и продолжить работу в обычном режиме.</span><span class="sxs-lookup"><span data-stu-id="bfe5c-122">Then, start all the VMs and continue operating as normal.</span></span>

1. <span data-ttu-id="bfe5c-123">Выведите список всех виртуальных машин в группе доступности, выполнив команду [az vm availability-set list](/cli/azure/vm/availability-set#list).</span><span class="sxs-lookup"><span data-stu-id="bfe5c-123">List all VMs in an availability set by using [az vm availability-set list](/cli/azure/vm/availability-set#list).</span></span> <span data-ttu-id="bfe5c-124">В следующем примере выводится список виртуальных машин в группе доступности `myAvailabilitySet` в группе ресурсов `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="bfe5c-124">The following example lists all VMs in the availability set named `myAvailabilitySet` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set show \
        --resource-group myResourceGroup \
        --name myAvailabilitySet \
        --query [virtualMachines[*].id] \
        --output table
    ```

2. <span data-ttu-id="bfe5c-125">Отмените выделение всех виртуальных машин командой [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="bfe5c-125">Deallocate all the VMs by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="bfe5c-126">В следующем примере освобождается виртуальная машина `myVM`, входящая в группу ресурсов `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="bfe5c-126">The following example deallocates the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="bfe5c-127">Преобразуйте группу доступности с помощью команды [az vm availability-set convert](/cli/azure/vm/availability-set#convert).</span><span class="sxs-lookup"><span data-stu-id="bfe5c-127">Convert the availability set by using [az vm availability-set convert](/cli/azure/vm/availability-set#convert).</span></span> <span data-ttu-id="bfe5c-128">В следующем примере преобразовывается группа доступности `myAvailabilitySet` в группе ресурсов `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="bfe5c-128">The following example converts the availability set named `myAvailabilitySet` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set convert \
        --resource-group myResourceGroup \
        --name myAvailabilitySet
    ```

4. <span data-ttu-id="bfe5c-129">Преобразуйте все виртуальные машины для использования управляемых дисков с помощью команды [az vm convert](/cli/azure/vm#convert).</span><span class="sxs-lookup"><span data-stu-id="bfe5c-129">Convert all the VMs to managed disks by using [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="bfe5c-130">Приведенный ниже процесс преобразовывает виртуальную машину `myVM`, включая ее диск ОС и все диски данных.</span><span class="sxs-lookup"><span data-stu-id="bfe5c-130">The following process converts the VM named `myVM`, including the OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

5. <span data-ttu-id="bfe5c-131">После преобразования запустите все виртуальные машины с помощью команды [az vm start](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="bfe5c-131">Start all the VMs after the conversion to managed disks by using [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="bfe5c-132">В следующем примере запускается виртуальная машина `myVM` в группе ресурсов `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="bfe5c-132">The following example starts the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="next-steps"></a><span data-ttu-id="bfe5c-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bfe5c-133">Next steps</span></span>
<span data-ttu-id="bfe5c-134">Дополнительные сведения о возможностях хранения данных доступны в [обзоре Управляемых дисков Azure](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bfe5c-134">For more information about storage options, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>
