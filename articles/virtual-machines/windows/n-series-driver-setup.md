---
title: "Настройка драйвера aaaAzure N-й серии для Windows | Документы Microsoft"
description: "Как tooset драйверы GPU, NVIDIA для N-й серии виртуальных машин под управлением Windows в Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f3950c34-9406-48ae-bcd9-c0418607b37d
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/07/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2acce57d4f9eb1d02bf3bc0303bcb9690475698c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-gpu-drivers-for-n-series-vms-running-windows-server"></a><span data-ttu-id="990ef-103">Установка драйверов GPU для виртуальных машин серии N под управлением Windows Server</span><span class="sxs-lookup"><span data-stu-id="990ef-103">Set up GPU drivers for N-series VMs running Windows Server</span></span>
<span data-ttu-id="990ef-104">преимущества tootake работы GPU hello Azure N-й серии виртуальных машин под управлением Windows Server 2016 или Windows Server 2012 R2, установите поддерживаемые NVIDIA графические драйверы.</span><span class="sxs-lookup"><span data-stu-id="990ef-104">tootake advantage of hello GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, install supported NVIDIA graphics drivers.</span></span> <span data-ttu-id="990ef-105">В этой статье приводятся действия по установке драйверов после развертывания виртуальных машин серии N.</span><span class="sxs-lookup"><span data-stu-id="990ef-105">This article provides driver setup steps after you deploy an N-series VM.</span></span> <span data-ttu-id="990ef-106">Сведения об установке драйверов также доступны для [виртуальных машин Linux](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="990ef-106">Driver setup information is also available for [Linux VMs](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="990ef-107">Основные характеристики, сведения о дисках и объеме памяти см. в статье [Графический процессор](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="990ef-107">For basic specs, storage capacities, and disk details, see [GPU Windows VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 


[!INCLUDE [virtual-machines-n-series-windows-support](../../../includes/virtual-machines-n-series-windows-support.md)]



## <a name="driver-installation"></a><span data-ttu-id="990ef-108">Установка драйвера</span><span class="sxs-lookup"><span data-stu-id="990ef-108">Driver installation</span></span>

1. <span data-ttu-id="990ef-109">Подключение с удаленного рабочего стола tooeach N-й серии виртуальных Машин.</span><span class="sxs-lookup"><span data-stu-id="990ef-109">Connect by Remote Desktop tooeach N-series VM.</span></span>

2. <span data-ttu-id="990ef-110">Загрузить, извлечь и установить драйвер hello поддерживается для операционной системы Windows.</span><span class="sxs-lookup"><span data-stu-id="990ef-110">Download, extract, and install hello supported driver for your Windows operating system.</span></span>

<span data-ttu-id="990ef-111">После установки драйвера на виртуальных машинах Azure серии NV их требуется перезагрузить.</span><span class="sxs-lookup"><span data-stu-id="990ef-111">On Azure NV VMs, a restart is required after driver installation.</span></span> <span data-ttu-id="990ef-112">На виртуальных машинах NC перезагрузка не требуется.</span><span class="sxs-lookup"><span data-stu-id="990ef-112">On NC VMs, a restart is not required.</span></span>

## <a name="verify-driver-installation"></a><span data-ttu-id="990ef-113">Проверка установки драйверов</span><span class="sxs-lookup"><span data-stu-id="990ef-113">Verify driver installation</span></span>

<span data-ttu-id="990ef-114">Установку драйвера можно проверить в диспетчере устройств.</span><span class="sxs-lookup"><span data-stu-id="990ef-114">You can verify driver installation in Device Manager.</span></span> <span data-ttu-id="990ef-115">Hello пример настройки карты hello Tesla K80 на виртуальной Машине Azure NC.</span><span class="sxs-lookup"><span data-stu-id="990ef-115">hello following example shows successful configuration of hello Tesla K80 card on an Azure NC VM.</span></span>

![Свойства драйвера GPU](./media/n-series-driver-setup/GPU_driver_properties.png)

<span data-ttu-id="990ef-117">hello tooquery состояния устройств GPU, запустите hello [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) программа устанавливается вместе с драйвером hello.</span><span class="sxs-lookup"><span data-stu-id="990ef-117">tooquery hello GPU device state, run hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with hello driver.</span></span>

1. <span data-ttu-id="990ef-118">Откройте командную строку и измените toohello **C:\Program Files\NVIDIA Corporation\NVSMI** каталога.</span><span class="sxs-lookup"><span data-stu-id="990ef-118">Open a command prompt and change toohello **C:\Program Files\NVIDIA Corporation\NVSMI** directory.</span></span>

2. <span data-ttu-id="990ef-119">Запустите **nvidia-smi**.</span><span class="sxs-lookup"><span data-stu-id="990ef-119">Run **nvidia-smi**.</span></span> <span data-ttu-id="990ef-120">Если установлен драйвер hello вы увидите примерно toobelow выходных данных.</span><span class="sxs-lookup"><span data-stu-id="990ef-120">If hello driver is installed you will see output similar toobelow.</span></span> <span data-ttu-id="990ef-121">Обратите внимание, что **GPU Util** показывает **0%** в настоящее время выполняется рабочая нагрузка GPU на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="990ef-121">Note that **GPU-Util** shows **0%** unless you are currently running a GPU workload on hello VM.</span></span>

![Состояние устройства NVIDIA](./media/n-series-driver-setup/smi.png)  

## <a name="rdma-network-for-nc24r-vms"></a><span data-ttu-id="990ef-123">Сеть RDMA для виртуальных машин NC24r</span><span class="sxs-lookup"><span data-stu-id="990ef-123">RDMA network for NC24r VMs</span></span>

<span data-ttu-id="990ef-124">Можно включить подключение к сети RDMA в NC24r виртуальных машин, развернутых в hello одной группе доступности.</span><span class="sxs-lookup"><span data-stu-id="990ef-124">RDMA network connectivity can be enabled on NC24r VMs deployed in hello same availability set.</span></span> <span data-ttu-id="990ef-125">необходимо добавить tooinstall Windows драйверов сетевых устройств, позволяющие подключения RDMA Hello расширение HpcVmDrivers.</span><span class="sxs-lookup"><span data-stu-id="990ef-125">hello HpcVmDrivers extension must be added tooinstall Windows network device drivers that enable RDMA connectivity.</span></span> <span data-ttu-id="990ef-126">использовать tooadd hello ВМ расширения tooan NC24r ВМ, [Azure PowerShell](/powershell/azure/overview) командлеты для диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="990ef-126">tooadd hello VM extension tooan NC24r VM, use [Azure PowerShell](/powershell/azure/overview) cmdlets for Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="990ef-127">В настоящее время только Windows Server 2012 R2 поддерживает сети RDMA hello на виртуальных машинах NC24r.</span><span class="sxs-lookup"><span data-stu-id="990ef-127">Currently, only Windows Server 2012 R2 supports hello RDMA network on NC24r VMs.</span></span>
> 

<span data-ttu-id="990ef-128">расширение HpcVMDrivers tooinstall hello последние версии 1.1 на поддержку функции RDMA существующей виртуальной Машины с именем myVM в hello Запад США:</span><span class="sxs-lookup"><span data-stu-id="990ef-128">tooinstall hello latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named myVM in hello West US region:</span></span>
  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  <span data-ttu-id="990ef-129">Дополнительные сведения см. в разделе [Обзор расширений и компонентов виртуальной машины под управлением Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="990ef-129">For more information, see [Virtual machine extensions and features for Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="990ef-130">сеть RDMA Hello поддерживает трафик интерфейса передачи сообщений (MPI) для приложений, работающих с [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) или Intel MPI 5.x.</span><span class="sxs-lookup"><span data-stu-id="990ef-130">hello RDMA network supports Message Passing Interface (MPI) traffic for applications running with [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) or Intel MPI 5.x.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="990ef-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="990ef-131">Next steps</span></span>

* <span data-ttu-id="990ef-132">Дополнительные сведения о графических процессоров NVIDIA hello hello N-й серии виртуальных машин см.:</span><span class="sxs-lookup"><span data-stu-id="990ef-132">For more information about hello NVIDIA GPUs on hello N-series VMs, see:</span></span>
    * <span data-ttu-id="990ef-133">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (для виртуальных машин Azure серии NC);</span><span class="sxs-lookup"><span data-stu-id="990ef-133">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="990ef-134">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (для виртуальных машин Azure серии NV).</span><span class="sxs-lookup"><span data-stu-id="990ef-134">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>

* <span data-ttu-id="990ef-135">Разработчики приложений ускорением GPU для hello NVIDIA Tesla GPU также можно загрузить и установить hello 8 CUDA набора средств для [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) или [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe).</span><span class="sxs-lookup"><span data-stu-id="990ef-135">Developers building GPU-accelerated applications for hello NVIDIA Tesla GPUs can also download and install hello CUDA Toolkit 8 for [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) or [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe).</span></span> <span data-ttu-id="990ef-136">Дополнительные сведения см. в разделе hello [руководство по установке CUDA](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).</span><span class="sxs-lookup"><span data-stu-id="990ef-136">For more information, see hello [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).</span></span>


