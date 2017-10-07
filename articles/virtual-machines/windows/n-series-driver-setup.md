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
# <a name="set-up-gpu-drivers-for-n-series-vms-running-windows-server"></a>Установка драйверов GPU для виртуальных машин серии N под управлением Windows Server
преимущества tootake работы GPU hello Azure N-й серии виртуальных машин под управлением Windows Server 2016 или Windows Server 2012 R2, установите поддерживаемые NVIDIA графические драйверы. В этой статье приводятся действия по установке драйверов после развертывания виртуальных машин серии N. Сведения об установке драйверов также доступны для [виртуальных машин Linux](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Основные характеристики, сведения о дисках и объеме памяти см. в статье [Графический процессор](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 


[!INCLUDE [virtual-machines-n-series-windows-support](../../../includes/virtual-machines-n-series-windows-support.md)]



## <a name="driver-installation"></a>Установка драйвера

1. Подключение с удаленного рабочего стола tooeach N-й серии виртуальных Машин.

2. Загрузить, извлечь и установить драйвер hello поддерживается для операционной системы Windows.

После установки драйвера на виртуальных машинах Azure серии NV их требуется перезагрузить. На виртуальных машинах NC перезагрузка не требуется.

## <a name="verify-driver-installation"></a>Проверка установки драйверов

Установку драйвера можно проверить в диспетчере устройств. Hello пример настройки карты hello Tesla K80 на виртуальной Машине Azure NC.

![Свойства драйвера GPU](./media/n-series-driver-setup/GPU_driver_properties.png)

hello tooquery состояния устройств GPU, запустите hello [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) программа устанавливается вместе с драйвером hello.

1. Откройте командную строку и измените toohello **C:\Program Files\NVIDIA Corporation\NVSMI** каталога.

2. Запустите **nvidia-smi**. Если установлен драйвер hello вы увидите примерно toobelow выходных данных. Обратите внимание, что **GPU Util** показывает **0%** в настоящее время выполняется рабочая нагрузка GPU на hello виртуальной Машины.

![Состояние устройства NVIDIA](./media/n-series-driver-setup/smi.png)  

## <a name="rdma-network-for-nc24r-vms"></a>Сеть RDMA для виртуальных машин NC24r

Можно включить подключение к сети RDMA в NC24r виртуальных машин, развернутых в hello одной группе доступности. необходимо добавить tooinstall Windows драйверов сетевых устройств, позволяющие подключения RDMA Hello расширение HpcVmDrivers. использовать tooadd hello ВМ расширения tooan NC24r ВМ, [Azure PowerShell](/powershell/azure/overview) командлеты для диспетчера ресурсов Azure.

> [!NOTE]
> В настоящее время только Windows Server 2012 R2 поддерживает сети RDMA hello на виртуальных машинах NC24r.
> 

расширение HpcVMDrivers tooinstall hello последние версии 1.1 на поддержку функции RDMA существующей виртуальной Машины с именем myVM в hello Запад США:
  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  Дополнительные сведения см. в разделе [Обзор расширений и компонентов виртуальной машины под управлением Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

сеть RDMA Hello поддерживает трафик интерфейса передачи сообщений (MPI) для приложений, работающих с [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) или Intel MPI 5.x. 


## <a name="next-steps"></a>Дальнейшие действия

* Дополнительные сведения о графических процессоров NVIDIA hello hello N-й серии виртуальных машин см.:
    * [NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (для виртуальных машин Azure серии NC);
    * [NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (для виртуальных машин Azure серии NV).

* Разработчики приложений ускорением GPU для hello NVIDIA Tesla GPU также можно загрузить и установить hello 8 CUDA набора средств для [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) или [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe). Дополнительные сведения см. в разделе hello [руководство по установке CUDA](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).


