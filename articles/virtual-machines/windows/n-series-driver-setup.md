---
title: "Установка драйвера серии N для Windows | Документация Майкрософт"
description: "Как установить драйверы NVIDIA GPU для виртуальных машин серии N под управлением Windows в Azure"
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
ms.openlocfilehash: b480d10df777a2757c073ff77e1845d33d63163a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="set-up-gpu-drivers-for-n-series-vms-running-windows-server"></a><span data-ttu-id="f7bc5-103">Установка драйверов GPU для виртуальных машин серии N под управлением Windows Server</span><span class="sxs-lookup"><span data-stu-id="f7bc5-103">Set up GPU drivers for N-series VMs running Windows Server</span></span>
<span data-ttu-id="f7bc5-104">Чтобы воспользоваться преимуществами возможностей GPU виртуальных машин Azure серии N под управлением Windows Server 2016 или Windows Server 2012 R2, необходимо установить графические драйверы NVIDIA.</span><span class="sxs-lookup"><span data-stu-id="f7bc5-104">To take advantage of the GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, install supported NVIDIA graphics drivers.</span></span> <span data-ttu-id="f7bc5-105">В этой статье приводятся действия по установке драйверов после развертывания виртуальных машин серии N.</span><span class="sxs-lookup"><span data-stu-id="f7bc5-105">This article provides driver setup steps after you deploy an N-series VM.</span></span> <span data-ttu-id="f7bc5-106">Сведения об установке драйверов также доступны для [виртуальных машин Linux](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f7bc5-106">Driver setup information is also available for [Linux VMs](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="f7bc5-107">Основные характеристики, сведения о дисках и объеме памяти см. в статье [Графический процессор](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f7bc5-107">For basic specs, storage capacities, and disk details, see [GPU Windows VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 


[!INCLUDE [virtual-machines-n-series-windows-support](../../../includes/virtual-machines-n-series-windows-support.md)]



## <a name="driver-installation"></a><span data-ttu-id="f7bc5-108">Установка драйвера</span><span class="sxs-lookup"><span data-stu-id="f7bc5-108">Driver installation</span></span>

1. <span data-ttu-id="f7bc5-109">Подключитесь к каждой виртуальной машине серии N с помощью удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="f7bc5-109">Connect by Remote Desktop to each N-series VM.</span></span>

2. <span data-ttu-id="f7bc5-110">Скачайте, извлеките и установите поддерживаемый драйвер для своей операционной системы Windows.</span><span class="sxs-lookup"><span data-stu-id="f7bc5-110">Download, extract, and install the supported driver for your Windows operating system.</span></span>

<span data-ttu-id="f7bc5-111">После установки драйвера на виртуальных машинах Azure серии NV их требуется перезагрузить.</span><span class="sxs-lookup"><span data-stu-id="f7bc5-111">On Azure NV VMs, a restart is required after driver installation.</span></span> <span data-ttu-id="f7bc5-112">На виртуальных машинах NC перезагрузка не требуется.</span><span class="sxs-lookup"><span data-stu-id="f7bc5-112">On NC VMs, a restart is not required.</span></span>

## <a name="verify-driver-installation"></a><span data-ttu-id="f7bc5-113">Проверка установки драйверов</span><span class="sxs-lookup"><span data-stu-id="f7bc5-113">Verify driver installation</span></span>

<span data-ttu-id="f7bc5-114">Установку драйвера можно проверить в диспетчере устройств.</span><span class="sxs-lookup"><span data-stu-id="f7bc5-114">You can verify driver installation in Device Manager.</span></span> <span data-ttu-id="f7bc5-115">В следующем примере показана успешная конфигурация карты Tesla K80 на виртуальной машине Azure серии NC.</span><span class="sxs-lookup"><span data-stu-id="f7bc5-115">The following example shows successful configuration of the Tesla K80 card on an Azure NC VM.</span></span>

![Свойства драйвера GPU](./media/n-series-driver-setup/GPU_driver_properties.png)

<span data-ttu-id="f7bc5-117">Чтобы запросить состояние устройства GPU, выполните служебную программу командной строки [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface), установленную вместе с драйвером.</span><span class="sxs-lookup"><span data-stu-id="f7bc5-117">To query the GPU device state, run the [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with the driver.</span></span>

1. <span data-ttu-id="f7bc5-118">Откройте командную строку и измените каталог на **:\Program Files\NVIDIA Corporation\NVSMI**.</span><span class="sxs-lookup"><span data-stu-id="f7bc5-118">Open a command prompt and change to the **C:\Program Files\NVIDIA Corporation\NVSMI** directory.</span></span>

2. <span data-ttu-id="f7bc5-119">Запустите **nvidia-smi**.</span><span class="sxs-lookup"><span data-stu-id="f7bc5-119">Run **nvidia-smi**.</span></span> <span data-ttu-id="f7bc5-120">Если драйвер установлен, то отобразятся выходные данные, аналогичные приведенным ниже.</span><span class="sxs-lookup"><span data-stu-id="f7bc5-120">If the driver is installed you will see output similar to below.</span></span> <span data-ttu-id="f7bc5-121">Обратите внимание, что **GPU-Util** отобразит **0 %**, если в данный момент графический процессор не выполняет рабочую нагрузку на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="f7bc5-121">Note that **GPU-Util** shows **0%** unless you are currently running a GPU workload on the VM.</span></span>

![Состояние устройства NVIDIA](./media/n-series-driver-setup/smi.png)  

## <a name="rdma-network-for-nc24r-vms"></a><span data-ttu-id="f7bc5-123">Сеть RDMA для виртуальных машин NC24r</span><span class="sxs-lookup"><span data-stu-id="f7bc5-123">RDMA network for NC24r VMs</span></span>

<span data-ttu-id="f7bc5-124">Можно включить сетевое подключение RDMA на виртуальных машинах NC24r, развернутых в одной группе доступности.</span><span class="sxs-lookup"><span data-stu-id="f7bc5-124">RDMA network connectivity can be enabled on NC24r VMs deployed in the same availability set.</span></span> <span data-ttu-id="f7bc5-125">Необходимо добавить расширение HpcVmDrivers для установки драйверов сетевых устройств Windows, обеспечивающих подключения RDMA.</span><span class="sxs-lookup"><span data-stu-id="f7bc5-125">The HpcVmDrivers extension must be added to install Windows network device drivers that enable RDMA connectivity.</span></span> <span data-ttu-id="f7bc5-126">Чтобы в виртуальную машину NC24r добавить расширение виртуальной машины, используйте командлеты [Azure PowerShell](/powershell/azure/overview) для Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f7bc5-126">To add the VM extension to an NC24r VM, use [Azure PowerShell](/powershell/azure/overview) cmdlets for Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="f7bc5-127">В настоящее время только Windows Server 2012 R2 поддерживает сеть RDMA на виртуальных машинах NC24r.</span><span class="sxs-lookup"><span data-stu-id="f7bc5-127">Currently, only Windows Server 2012 R2 supports the RDMA network on NC24r VMs.</span></span>
> 

<span data-ttu-id="f7bc5-128">Чтобы установить последнюю версию расширения HpcVMDrivers 1.1 на существующую виртуальную машину myVM с поддержкой RDMA, размещенную в регионе "Западная часть США", выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="f7bc5-128">To install the latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named myVM in the West US region:</span></span>
  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  <span data-ttu-id="f7bc5-129">Дополнительные сведения см. в разделе [Обзор расширений и компонентов виртуальной машины под управлением Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f7bc5-129">For more information, see [Virtual machine extensions and features for Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="f7bc5-130">Сеть RDMA поддерживает трафик MPI (Message Passing Interface) для приложений, использующих [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) или Intel MPI 5.x.</span><span class="sxs-lookup"><span data-stu-id="f7bc5-130">The RDMA network supports Message Passing Interface (MPI) traffic for applications running with [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) or Intel MPI 5.x.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="f7bc5-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f7bc5-131">Next steps</span></span>

* <span data-ttu-id="f7bc5-132">Дополнительные сведения о графических процессорах NVIDIA в виртуальных машинах серии N см. в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="f7bc5-132">For more information about the NVIDIA GPUs on the N-series VMs, see:</span></span>
    * <span data-ttu-id="f7bc5-133">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (для виртуальных машин Azure серии NC);</span><span class="sxs-lookup"><span data-stu-id="f7bc5-133">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="f7bc5-134">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (для виртуальных машин Azure серии NV).</span><span class="sxs-lookup"><span data-stu-id="f7bc5-134">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>

* <span data-ttu-id="f7bc5-135">Разработчики приложений, использующих ускорение на GPU, которые предназначены для графических процессоров NVIDIA Tesla, могут также скачать и установить набор средств CUDA Toolkit 8 для [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) или [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe).</span><span class="sxs-lookup"><span data-stu-id="f7bc5-135">Developers building GPU-accelerated applications for the NVIDIA Tesla GPUs can also download and install the CUDA Toolkit 8 for [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) or [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe).</span></span> <span data-ttu-id="f7bc5-136">Дополнительные сведения см. в [руководстве по установке CUDA](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).</span><span class="sxs-lookup"><span data-stu-id="f7bc5-136">For more information, see the [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).</span></span>


