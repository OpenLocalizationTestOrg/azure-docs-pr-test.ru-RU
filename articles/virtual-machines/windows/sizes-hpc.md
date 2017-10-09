---
title: "размеры виртуальной Машины Windows aaaAzure - HPC | Документы Microsoft"
description: "Список hello различные размеры, доступные для Windows высокопроизводительные вычислительные системы виртуальных машин в Azure."
services: virtual-machines-windows
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 092bc32cfe048f439ad833911bef4ed17eda7977
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-compute-vm-sizes"></a>Размеры виртуальных машин, оптимизированных для высокопроизводительных вычислений

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a>Экземпляры с поддержкой RDMA
Подмножество hello экземпляров с большим объемом вычислений (H16r, H16mr, A8 и A9) возможностей сетевой интерфейс для подключения к удаленной памяти прямой доступ (RDMA). Этот интерфейс является Кроме размеры виртуальных Машин доступен tooother интерфейс стандартной сети Azure toohello. 
  
Этот интерфейс позволяет hello функцией RDMA экземпляры toocommunicate сети InfiniBand, работая на скорость FDR H16r и H16mr виртуальной машины и скорости QDR для виртуальных машин A8 и A9. Эти возможности RDMA может значительно повысить hello масштабируемость и производительность приложений интерфейса передачи сообщений (MPI).

Ниже приведены требования для tooaccess функцией RDMA виртуальных машин Windows hello сети Azure RDMA: 

* **Операционная система**
  
  Windows Server 2012 R2, Windows Server 2012
  
  > [!NOTE]
  > Сейчас соединение RDMA в Azure не поддерживается в Windows Server 2016.
  >

* **Группу доступности или облачная служба** — развертывание ВМ hello функцией RDMA в hello же доступности (при использовании модели развертывания диспетчера ресурсов Azure hello) или hello одной облачной службе (при использовании hello классической модели развертывания). При использовании пакета Azure hello функцией RDMA виртуальных машин должен быть в hello одного пула.

* **MPI** — Microsoft MPI (MS-MPI) 2012 R2 и более поздних версий, библиотека Intel MPI 5.x.

  Поддерживаемые реализации MPI используйте Microsoft Network Direct toocommunicate интерфейс hello между экземплярами. 

* **Адресное пространство сети RDMA** -hello сети RDMA в Azure резервирует пространство 172.16.0.0/16 hello адрес. toorun приложений MPI на экземплярах, развернутых в виртуальной сети Azure, убедитесь в том, что адресное пространство виртуальной сети hello не перекрывает сети RDMA hello.

* **Расширение HpcVmDrivers ВМ** -на ВМ с поддержкой RDMA, необходимо добавить hello HpcVmDrivers расширения tooinstall Windows драйверов сетевых устройств для подключения RDMA. (В некоторых развертываниях экземпляров A8 и A9 hello расширение HpcVmDrivers добавляется автоматически.) tooa расширение ВМ hello tooadd виртуальной Машины, можно использовать [Azure PowerShell](/powershell/azure/overview) командлетов. 

  
  Здравствуйте, следующая команда устанавливает hello последнее расширение HpcVMDrivers версии 1.1 на существующей виртуальной Машине функцией RDMA с именем *myVM* развернут в группе ресурсов hello с именем *myResourceGroup* в hello  *Западная часть США* области:

  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  
  Дополнительные сведения см. в статье [Обзор расширений и компонентов виртуальной машины под управлением Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Вы также можете работать с расширениями для виртуальных машин, развернутых в hello [классической модели развертывания](classic/manage-extensions.md).


## <a name="using-hpc-pack"></a>Использование пакета HPC

[Пакет Microsoft HPC](https://technet.microsoft.com/library/jj899572.aspx), корпорации Майкрософт свободного HPC заданиями и кластером решение по управлению, один из вариантов toocreate вычислительного кластера в Azure toorun приложений MPI на основе Windows и других рабочих нагрузок HPC. HPC Pack 2012 R2 и более поздних версиях включают среду выполнения для MS-MPI, использующий сеть Azure RDMA hello при развертывании на виртуальных машинах функцией RDMA.




## <a name="other-sizes"></a>Остальные размеры
- [Универсальные](sizes-general.md)
- [Оптимизированные для вычислений](sizes-compute.md)
- [Оптимизированные для памяти](../virtual-machines-windows-sizes-memory.md)
- [Оптимизированные для хранилища](../virtual-machines-windows-sizes-storage.md)
- [Оптимизированные для GPU](sizes-gpu.md)

## <a name="next-steps"></a>Дальнейшие действия

- Контрольные списки toouse hello экземпляров вычислений с помощью пакета HPC в Windows Server, в разделе [настроить кластер Windows RDMA с пакетом HPC приложений MPI toorun](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

- toouse экземпляров с большим объемом вычислений при выполнении приложений MPI с пакетом Azure в разделе [несколькими экземплярами использования задачи toorun приложений интерфейса передачи сообщений (MPI) в пакете Azure](../../batch/batch-mpi.md).

- Узнайте больше о том, как с помощью [единиц вычислений Azure (ACU)](acu.md) сравнить производительность вычислений для различных номеров SKU Azure.




