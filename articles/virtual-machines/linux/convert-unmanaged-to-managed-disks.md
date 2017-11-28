---
title: "aaaConvert виртуальной машины Linux в Azure из неуправляемого диски toomanaged - управляемых дисков Azure | Документы Microsoft"
description: "Как диски tooconvert из toomanaged неуправляемые дисков виртуальной Машины Linux с помощью Azure CLI 2.0 в модели развертывания диспетчера ресурсов hello"
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
ms.openlocfilehash: 1b94da11deab46f344e28ab4491cf220506b6347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-linux-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a><span data-ttu-id="7798e-103">Преобразовать виртуальную машину Linux с неуправляемой дисков toomanaged дисков</span><span class="sxs-lookup"><span data-stu-id="7798e-103">Convert a Linux virtual machine from unmanaged disks toomanaged disks</span></span>

<span data-ttu-id="7798e-104">При наличии существующих Linux виртуальных машин (ВМ), использующие неуправляемые диски можно преобразовать диски toouse управляемых виртуальных машин hello через hello [управляемых дисков Azure](../windows/managed-disks-overview.md) службы.</span><span class="sxs-lookup"><span data-stu-id="7798e-104">If you have existing Linux virtual machines (VMs) that use unmanaged disks, you can convert hello VMs toouse managed disks through hello [Azure Managed Disks](../windows/managed-disks-overview.md) service.</span></span> <span data-ttu-id="7798e-105">Этот процесс преобразует диска hello операционной системы и все подключенные диски данных.</span><span class="sxs-lookup"><span data-stu-id="7798e-105">This process converts both hello OS disk and any attached data disks.</span></span>

<span data-ttu-id="7798e-106">В этой статье показано, как tooconvert виртуальных машин с помощью hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="7798e-106">This article shows you how tooconvert VMs by using hello Azure CLI.</span></span> <span data-ttu-id="7798e-107">Если необходима tooinstall или обновить ее, см. раздел [установить CLI Azure 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7798e-107">If you need tooinstall or upgrade it, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="7798e-108">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="7798e-108">Before you begin</span></span>

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]


## <a name="convert-single-instance-vms"></a><span data-ttu-id="7798e-109">Преобразование одноэкземплярных виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="7798e-109">Convert single-instance VMs</span></span>
<span data-ttu-id="7798e-110">В этом разделе описывается, как диски toomanaged в tooconvert экземпляра ВМ Azure из неуправляемого.</span><span class="sxs-lookup"><span data-stu-id="7798e-110">This section covers how tooconvert single-instance Azure VMs from unmanaged disks toomanaged disks.</span></span> <span data-ttu-id="7798e-111">(Если виртуальные машины в наборе доступности, см. следующий раздел hello.) Можно использовать этот процесс tooconvert hello виртуальных машин из дисков toopremium управляемых дисков неуправляемого premium (SSD) или стандарт (HDD) неуправляемого дисков toostandard управляемых дисков.</span><span class="sxs-lookup"><span data-stu-id="7798e-111">(If your VMs are in an availability set, see hello next section.) You can use this process tooconvert hello VMs from premium (SSD) unmanaged disks toopremium managed disks, or from standard (HDD) unmanaged disks toostandard managed disks.</span></span>

1. <span data-ttu-id="7798e-112">Освободить hello виртуальной Машины с помощью [ВМ az deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="7798e-112">Deallocate hello VM by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="7798e-113">Hello следующий пример отменяет выделение hello виртуальной Машины с именем `myVM` в группе ресурсов hello с именем `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="7798e-113">hello following example deallocates hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

2. <span data-ttu-id="7798e-114">Преобразовать диски toomanaged hello ВМ с помощью [преобразование виртуальной машины az](/cli/azure/vm#convert).</span><span class="sxs-lookup"><span data-stu-id="7798e-114">Convert hello VM toomanaged disks by using [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="7798e-115">После процесса преобразует Hello hello виртуальной Машины с именем `myVM`, включая диск hello ОС и дисков данных:</span><span class="sxs-lookup"><span data-stu-id="7798e-115">hello following process converts hello VM named `myVM`, including hello OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="7798e-116">Запустите hello виртуальной Машины после hello преобразования toomanaged диски с помощью [запуска виртуальной машины az](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="7798e-116">Start hello VM after hello conversion toomanaged disks by using [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="7798e-117">Следующий пример запускает Hello hello виртуальной Машины с именем `myVM` в группе ресурсов hello с именем `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="7798e-117">hello following example starts hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="convert-vms-in-an-availability-set"></a><span data-ttu-id="7798e-118">Преобразование виртуальных машин в группе доступности</span><span class="sxs-lookup"><span data-stu-id="7798e-118">Convert VMs in an availability set</span></span>

<span data-ttu-id="7798e-119">Если hello ВМ, которые вы хотите tooconvert toomanaged диски находятся в наборе доступности, необходимо сначала управляемый набор tooa tooconvert hello доступности группы доступности.</span><span class="sxs-lookup"><span data-stu-id="7798e-119">If hello VMs that you want tooconvert toomanaged disks are in an availability set, you first need tooconvert hello availability set tooa managed availability set.</span></span>

<span data-ttu-id="7798e-120">Все виртуальные машины в наборе доступности hello должна освобождаться перед преобразованием набора доступности hello.</span><span class="sxs-lookup"><span data-stu-id="7798e-120">All VMs in hello availability set must be deallocated before you convert hello availability set.</span></span> <span data-ttu-id="7798e-121">Все диски виртуальных машин toomanaged после доступности hello назначила себя tooconvert план был преобразованный tooa управляемые группы доступности.</span><span class="sxs-lookup"><span data-stu-id="7798e-121">Plan tooconvert all VMs toomanaged disks after hello availability set itself has been converted tooa managed availability set.</span></span> <span data-ttu-id="7798e-122">Затем запустите все виртуальные машины hello и продолжить работу в обычном режиме.</span><span class="sxs-lookup"><span data-stu-id="7798e-122">Then, start all hello VMs and continue operating as normal.</span></span>

1. <span data-ttu-id="7798e-123">Выведите список всех виртуальных машин в группе доступности, выполнив команду [az vm availability-set list](/cli/azure/vm/availability-set#list).</span><span class="sxs-lookup"><span data-stu-id="7798e-123">List all VMs in an availability set by using [az vm availability-set list](/cli/azure/vm/availability-set#list).</span></span> <span data-ttu-id="7798e-124">Hello следующий пример отображает список всех виртуальных машин в набор доступности hello `myAvailabilitySet` в группе ресурсов hello с именем `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="7798e-124">hello following example lists all VMs in hello availability set named `myAvailabilitySet` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set show \
        --resource-group myResourceGroup \
        --name myAvailabilitySet \
        --query [virtualMachines[*].id] \
        --output table
    ```

2. <span data-ttu-id="7798e-125">Освободить все hello виртуальные машины с помощью [ВМ az deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="7798e-125">Deallocate all hello VMs by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="7798e-126">Hello следующий пример отменяет выделение hello виртуальной Машины с именем `myVM` в группе ресурсов hello с именем `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="7798e-126">hello following example deallocates hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="7798e-127">Преобразовать hello доступности с помощью [преобразовать группу доступности виртуальной машины az](/cli/azure/vm/availability-set#convert).</span><span class="sxs-lookup"><span data-stu-id="7798e-127">Convert hello availability set by using [az vm availability-set convert](/cli/azure/vm/availability-set#convert).</span></span> <span data-ttu-id="7798e-128">Hello следующий пример преобразует набор именованных доступности hello `myAvailabilitySet` в группе ресурсов hello с именем `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="7798e-128">hello following example converts hello availability set named `myAvailabilitySet` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set convert \
        --resource-group myResourceGroup \
        --name myAvailabilitySet
    ```

4. <span data-ttu-id="7798e-129">Преобразовать все диски toomanaged ВМ hello, используя [преобразование виртуальной машины az](/cli/azure/vm#convert).</span><span class="sxs-lookup"><span data-stu-id="7798e-129">Convert all hello VMs toomanaged disks by using [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="7798e-130">После процесса преобразует Hello hello виртуальной Машины с именем `myVM`, включая диск hello ОС и дисков данных:</span><span class="sxs-lookup"><span data-stu-id="7798e-130">hello following process converts hello VM named `myVM`, including hello OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

5. <span data-ttu-id="7798e-131">Запустить все виртуальные машины hello после hello преобразования toomanaged диски с помощью [запуска виртуальной машины az](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="7798e-131">Start all hello VMs after hello conversion toomanaged disks by using [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="7798e-132">Следующий пример запускает Hello hello виртуальной Машины с именем `myVM` в группе ресурсов hello с именем `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="7798e-132">hello following example starts hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="next-steps"></a><span data-ttu-id="7798e-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7798e-133">Next steps</span></span>
<span data-ttu-id="7798e-134">Дополнительные сведения о возможностях хранения данных доступны в [обзоре Управляемых дисков Azure](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7798e-134">For more information about storage options, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>
