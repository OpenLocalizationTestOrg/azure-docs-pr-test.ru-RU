---
title: "aaaHow tooresize виртуальная машина Linux с hello Azure CLI 2.0 | Документы Microsoft"
description: "Как tooscale вверх или масштаб работу виртуальной машины Linux, изменив hello размер виртуальной Машины."
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: e163f878-b919-45c5-9f5a-75a64f3b14a0
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2017
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e8fba485b5bcc7824f546de5cf3df77624a28008
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-virtual-machine-using-cli-20"></a><span data-ttu-id="3ba2e-103">Изменение размера виртуальной машины Linux с помощью CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3ba2e-103">Resize a Linux virtual machine using CLI 2.0</span></span>

<span data-ttu-id="3ba2e-104">После подготовки виртуальной машины (VM) можно масштабировать hello ВМ вверх или вниз, изменив hello [размер виртуальной Машины][vm-sizes].</span><span class="sxs-lookup"><span data-stu-id="3ba2e-104">After you provision a virtual machine (VM), you can scale hello VM up or down by changing hello [VM size][vm-sizes].</span></span> <span data-ttu-id="3ba2e-105">В некоторых случаях необходимо сначала отменить hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="3ba2e-105">In some cases, you must deallocate hello VM first.</span></span> <span data-ttu-id="3ba2e-106">Требуется toodeallocate hello виртуальной Машины, если размер недоступен в кластере hello оборудования, на котором размещается виртуальная машина hello требуемого hello.</span><span class="sxs-lookup"><span data-stu-id="3ba2e-106">You need toodeallocate hello VM if hello desired size is not available on hello hardware cluster that is hosting hello VM.</span></span> <span data-ttu-id="3ba2e-107">В этой статье указаны как tooresize a виртуальная машина Linux с hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="3ba2e-107">This article details how tooresize a Linux VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="3ba2e-108">Можно также выполнить следующие действия с hello [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3ba2e-108">You can also perform these steps with hello [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="resize-a-vm"></a><span data-ttu-id="3ba2e-109">Изменение размера виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="3ba2e-109">Resize a VM</span></span>
<span data-ttu-id="3ba2e-110">tooresize виртуальной Машины необходимо hello последней [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="3ba2e-110">tooresize a VM, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

1. <span data-ttu-id="3ba2e-111">Изменяет размер hello просмотреть список доступных виртуальных Машин на кластере оборудования hello размещения hello виртуальной Машины с [az виртуальной машины-vm-resize параметры списка](/cli/azure/vm#list-vm-resize-options).</span><span class="sxs-lookup"><span data-stu-id="3ba2e-111">View hello list of available VM sizes on hello hardware cluster where hello VM is hosted with [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options).</span></span> <span data-ttu-id="3ba2e-112">Hello следующий пример отображает список размеров виртуальной Машины для виртуальной Машины с именем hello `myVM` в группе ресурсов hello `myResourceGroup` области:</span><span class="sxs-lookup"><span data-stu-id="3ba2e-112">hello following example lists VM sizes for hello VM named `myVM` in hello resource group `myResourceGroup` region:</span></span>
   
    ```azurecli
    az vm list-vm-resize-options --resource-group myResourceGroup --name myVM --output table
    ```

2. <span data-ttu-id="3ba2e-113">По желанию hello указан размер виртуальной Машины, изменение размера hello виртуальной Машины с [изменить размер виртуальной машины az](/cli/azure/vm#resize).</span><span class="sxs-lookup"><span data-stu-id="3ba2e-113">If hello desired VM size is listed, resize hello VM with [az vm resize](/cli/azure/vm#resize).</span></span> <span data-ttu-id="3ba2e-114">Следующий пример изменяет размер Hello hello виртуальной Машины с именем `myVM` toohello `Standard_DS3_v2` размер:</span><span class="sxs-lookup"><span data-stu-id="3ba2e-114">hello following example resizes hello VM named `myVM` toohello `Standard_DS3_v2` size:</span></span>
   
    ```azurecli
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    ```
   
    <span data-ttu-id="3ba2e-115">Hello ВМ перезапускается во время этого процесса.</span><span class="sxs-lookup"><span data-stu-id="3ba2e-115">hello VM restarts during this process.</span></span> <span data-ttu-id="3ba2e-116">После перезапуска hello сопоставляются существующей операционной системы и дисков данных.</span><span class="sxs-lookup"><span data-stu-id="3ba2e-116">After hello restart, your existing OS and data disks are remapped.</span></span> <span data-ttu-id="3ba2e-117">Все устройства hello временный диск будет потеряно.</span><span class="sxs-lookup"><span data-stu-id="3ba2e-117">Anything on hello temporary disk is lost.</span></span>

3. <span data-ttu-id="3ba2e-118">При желании hello не указан размер виртуальной Машины необходимо toofirst deallocate hello виртуальной Машины с [ВМ az deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="3ba2e-118">If hello desired VM size is not listed, you need toofirst deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="3ba2e-119">Этот процесс позволяет toothen ВМ hello использоваться размер tooany размер доступной, hello поддерживает области и их запуска.</span><span class="sxs-lookup"><span data-stu-id="3ba2e-119">This process allows hello VM toothen be resized tooany size available that hello region supports and then started.</span></span> <span data-ttu-id="3ba2e-120">Hello следующее deallocate, масштабировать и затем запустить Виртуальную машину с именем hello `myVM` в группе ресурсов hello с именем `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="3ba2e-120">hello following steps deallocate, resize, and then start hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>
   
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    az vm start --resource-group myResourceGroup --name myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="3ba2e-121">Освобождение hello виртуальной Машины также освобождает любой динамических IP-адресов, назначенных toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="3ba2e-121">Deallocating hello VM also releases any dynamic IP addresses assigned toohello VM.</span></span> <span data-ttu-id="3ba2e-122">Hello ОС и диски с данными не затрагиваются.</span><span class="sxs-lookup"><span data-stu-id="3ba2e-122">hello OS and data disks are not affected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ba2e-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3ba2e-123">Next steps</span></span>
<span data-ttu-id="3ba2e-124">Для дополнительной масштабируемости запустите несколько экземпляров виртуальных машин и разверните их. Дополнительные сведения см. в статье [Автоматическое масштабирование машин Linux в наборе масштабирования виртуальных машин][scale-set].</span><span class="sxs-lookup"><span data-stu-id="3ba2e-124">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
