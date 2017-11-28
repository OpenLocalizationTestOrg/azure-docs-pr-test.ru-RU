---
title: "aaaHow tooresize виртуальная машина Linux с hello Azure CLI 1.0 | Документы Microsoft"
description: "Как tooscale вверх или масштаб работу виртуальной машины Linux, изменив hello размер виртуальной Машины."
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/16/2016
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 43dd955dc2f2dd9d1b2da07ecbfbf2459bcaa4d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-vm-with-azure-cli-10"></a><span data-ttu-id="effcc-103">Изменение размера виртуальной машины Linux с помощью Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="effcc-103">Resize a Linux VM with Azure CLI 1.0</span></span>

## <a name="overview"></a><span data-ttu-id="effcc-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="effcc-104">Overview</span></span>

<span data-ttu-id="effcc-105">После подготовки виртуальной машины (VM) можно масштабировать hello ВМ вверх или вниз, изменив hello [размер виртуальной Машины][vm-sizes].</span><span class="sxs-lookup"><span data-stu-id="effcc-105">After you provision a virtual machine (VM), you can scale hello VM up or down by changing hello [VM size][vm-sizes].</span></span> <span data-ttu-id="effcc-106">В некоторых случаях необходимо сначала отменить hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="effcc-106">In some cases, you must deallocate hello VM first.</span></span> <span data-ttu-id="effcc-107">Это может произойти, если новый размер hello не доступен на кластере hello оборудования, на котором размещается виртуальная машина hello.</span><span class="sxs-lookup"><span data-stu-id="effcc-107">This can happen if hello new size is not available on hello hardware cluster that is hosting hello VM.</span></span>

<span data-ttu-id="effcc-108">В этой статье показано, как tooresize в виртуальной Машине Linux с помощью hello [Azure CLI][azure-cli].</span><span class="sxs-lookup"><span data-stu-id="effcc-108">This article shows how tooresize a Linux VM using hello [Azure CLI][azure-cli].</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="effcc-109">Задача hello toocomplete версии CLI</span><span class="sxs-lookup"><span data-stu-id="effcc-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="effcc-110">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="effcc-110">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="effcc-111">[Azure CLI 1.0](#resize-a-linux-vm) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)</span><span class="sxs-lookup"><span data-stu-id="effcc-111">[Azure CLI 1.0](#resize-a-linux-vm) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="effcc-112">[Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -нашей нового поколения CLI для модели развертывания hello ресурсов управления</span><span class="sxs-lookup"><span data-stu-id="effcc-112">[Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="resize-a-linux-vm"></a><span data-ttu-id="effcc-113">Изменение размера виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="effcc-113">Resize a Linux VM</span></span>
<span data-ttu-id="effcc-114">tooresize виртуальную Машину, выполните hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="effcc-114">tooresize a VM, perform hello following steps.</span></span>

1. <span data-ttu-id="effcc-115">Выполните следующую команду CLI hello.</span><span class="sxs-lookup"><span data-stu-id="effcc-115">Run hello following CLI command.</span></span> <span data-ttu-id="effcc-116">Эта команда выводит список размеров виртуальных Машин hello, доступные на кластере оборудования hello hello ВМ размещения.</span><span class="sxs-lookup"><span data-stu-id="effcc-116">This command lists hello VM sizes that are available on hello hardware cluster where hello VM is hosted.</span></span>
   
    ```azurecli
    azure vm sizes -g myResourceGroup --vm-name myVM
    ```
2. <span data-ttu-id="effcc-117">При желании hello, указан размер запустите hello, следующая команда tooresize hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="effcc-117">If hello desired size is listed, run hello following command tooresize hello VM.</span></span>
   
    ```azurecli
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM  \
        --enable-boot-diagnostics
        --boot-diagnostics-storage-uri https://mystorageaccount.blob.core.windows.net/ 
    ```
   
    <span data-ttu-id="effcc-118">во время этого процесса будет перезапущена Hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="effcc-118">hello VM will restart during this process.</span></span> <span data-ttu-id="effcc-119">После перезапуска hello будут перераспределены существующей операционной системы и дисков данных.</span><span class="sxs-lookup"><span data-stu-id="effcc-119">After hello restart, your existing OS and data disks will be remapped.</span></span> <span data-ttu-id="effcc-120">Все устройства hello временного диска будут потеряны.</span><span class="sxs-lookup"><span data-stu-id="effcc-120">Anything on hello temporary disk will be lost.</span></span>
   
    <span data-ttu-id="effcc-121">Используйте hello `--enable-boot-diagnostics` позволяет [загрузки диагностики][boot-diagnostics], toolog связанные toostartup любые ошибки.</span><span class="sxs-lookup"><span data-stu-id="effcc-121">Use hello `--enable-boot-diagnostics` option enables [boot diagnostics][boot-diagnostics], toolog any errors related toostartup.</span></span>
3. <span data-ttu-id="effcc-122">В противном случае — если hello требуемого размера не указан, выполните следующие команды toodeallocate hello виртуальной Машины, ее размер, а затем перезапустите ВМ hello hello.</span><span class="sxs-lookup"><span data-stu-id="effcc-122">Otherwise, if hello desired size is not listed, run hello following commands toodeallocate hello VM, resize it, and then restart hello VM.</span></span>
   
    ```azurecli
    azure vm deallocate -g myResourceGroup myVM
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM \
        --enable-boot-diagnostics --boot-diagnostics-storage-uri \
        https://mystorageaccount.blob.core.windows.net/ 
    azure vm start -g myResourceGroup myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="effcc-123">Освобождение hello виртуальной Машины также освобождает любой динамических IP-адресов, назначенных toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="effcc-123">Deallocating hello VM also releases any dynamic IP addresses assigned toohello VM.</span></span> <span data-ttu-id="effcc-124">Hello ОС и диски с данными не затрагиваются.</span><span class="sxs-lookup"><span data-stu-id="effcc-124">hello OS and data disks are not affected.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="effcc-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="effcc-125">Next steps</span></span>
<span data-ttu-id="effcc-126">Для дополнительной масштабируемости запустите несколько экземпляров виртуальных машин и разверните их. Дополнительные сведения см. в статье [Автоматическое масштабирование машин Linux в наборе масштабирования виртуальных машин][scale-set].</span><span class="sxs-lookup"><span data-stu-id="effcc-126">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->

[azure-cli]:../../cli-install-nodejs.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
