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
# <a name="high-performance-compute-vm-sizes"></a><span data-ttu-id="2b0fa-103">Размеры виртуальных машин, оптимизированных для высокопроизводительных вычислений</span><span class="sxs-lookup"><span data-stu-id="2b0fa-103">High performance compute VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a><span data-ttu-id="2b0fa-104">Экземпляры с поддержкой RDMA</span><span class="sxs-lookup"><span data-stu-id="2b0fa-104">RDMA-capable instances</span></span>
<span data-ttu-id="2b0fa-105">Подмножество hello экземпляров с большим объемом вычислений (H16r, H16mr, A8 и A9) возможностей сетевой интерфейс для подключения к удаленной памяти прямой доступ (RDMA).</span><span class="sxs-lookup"><span data-stu-id="2b0fa-105">A subset of hello compute-intensive instances (H16r, H16mr, A8, and A9) feature a network interface for remote direct memory access (RDMA) connectivity.</span></span> <span data-ttu-id="2b0fa-106">Этот интерфейс является Кроме размеры виртуальных Машин доступен tooother интерфейс стандартной сети Azure toohello.</span><span class="sxs-lookup"><span data-stu-id="2b0fa-106">This interface is in addition toohello standard Azure network interface available tooother VM sizes.</span></span> 
  
<span data-ttu-id="2b0fa-107">Этот интерфейс позволяет hello функцией RDMA экземпляры toocommunicate сети InfiniBand, работая на скорость FDR H16r и H16mr виртуальной машины и скорости QDR для виртуальных машин A8 и A9.</span><span class="sxs-lookup"><span data-stu-id="2b0fa-107">This interface allows hello RDMA-capable instances toocommunicate over an InfiniBand network, operating at FDR rates for H16r and H16mr virtual machines, and QDR rates for A8 and A9 virtual machines.</span></span> <span data-ttu-id="2b0fa-108">Эти возможности RDMA может значительно повысить hello масштабируемость и производительность приложений интерфейса передачи сообщений (MPI).</span><span class="sxs-lookup"><span data-stu-id="2b0fa-108">These RDMA capabilities can boost hello scalability and performance of Message Passing Interface (MPI) applications.</span></span>

<span data-ttu-id="2b0fa-109">Ниже приведены требования для tooaccess функцией RDMA виртуальных машин Windows hello сети Azure RDMA:</span><span class="sxs-lookup"><span data-stu-id="2b0fa-109">Following are requirements for RDMA-capable Windows VMs tooaccess hello Azure RDMA network:</span></span> 

* <span data-ttu-id="2b0fa-110">**Операционная система**</span><span class="sxs-lookup"><span data-stu-id="2b0fa-110">**Operating system**</span></span>
  
  <span data-ttu-id="2b0fa-111">Windows Server 2012 R2, Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="2b0fa-111">Windows Server 2012 R2, Windows Server 2012</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="2b0fa-112">Сейчас соединение RDMA в Azure не поддерживается в Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="2b0fa-112">Currently, Windows Server 2016 does not support RDMA connectivity in Azure.</span></span>
  >

* <span data-ttu-id="2b0fa-113">**Группу доступности или облачная служба** — развертывание ВМ hello функцией RDMA в hello же доступности (при использовании модели развертывания диспетчера ресурсов Azure hello) или hello одной облачной службе (при использовании hello классической модели развертывания).</span><span class="sxs-lookup"><span data-stu-id="2b0fa-113">**Availability set or cloud service** – Deploy hello RDMA-capable VMs in hello same availability set (when you use hello Azure Resource Manager deployment model) or hello same cloud service (when you use hello classic deployment model).</span></span> <span data-ttu-id="2b0fa-114">При использовании пакета Azure hello функцией RDMA виртуальных машин должен быть в hello одного пула.</span><span class="sxs-lookup"><span data-stu-id="2b0fa-114">If you use Azure Batch, hello RDMA-capable VMs must be in hello same pool.</span></span>

* <span data-ttu-id="2b0fa-115">**MPI** — Microsoft MPI (MS-MPI) 2012 R2 и более поздних версий, библиотека Intel MPI 5.x.</span><span class="sxs-lookup"><span data-stu-id="2b0fa-115">**MPI** - Microsoft MPI (MS-MPI) 2012 R2 or later, Intel MPI Library 5.x</span></span>

  <span data-ttu-id="2b0fa-116">Поддерживаемые реализации MPI используйте Microsoft Network Direct toocommunicate интерфейс hello между экземплярами.</span><span class="sxs-lookup"><span data-stu-id="2b0fa-116">Supported MPI implementations use hello Microsoft Network Direct interface toocommunicate between instances.</span></span> 

* <span data-ttu-id="2b0fa-117">**Адресное пространство сети RDMA** -hello сети RDMA в Azure резервирует пространство 172.16.0.0/16 hello адрес.</span><span class="sxs-lookup"><span data-stu-id="2b0fa-117">**RDMA network address space** - hello RDMA network in Azure reserves hello address space 172.16.0.0/16.</span></span> <span data-ttu-id="2b0fa-118">toorun приложений MPI на экземплярах, развернутых в виртуальной сети Azure, убедитесь в том, что адресное пространство виртуальной сети hello не перекрывает сети RDMA hello.</span><span class="sxs-lookup"><span data-stu-id="2b0fa-118">toorun MPI applications on instances deployed in an Azure virtual network, make sure that hello virtual network address space does not overlap hello RDMA network.</span></span>

* <span data-ttu-id="2b0fa-119">**Расширение HpcVmDrivers ВМ** -на ВМ с поддержкой RDMA, необходимо добавить hello HpcVmDrivers расширения tooinstall Windows драйверов сетевых устройств для подключения RDMA.</span><span class="sxs-lookup"><span data-stu-id="2b0fa-119">**HpcVmDrivers VM extension** - On RDMA-capable VMs, you must add hello HpcVmDrivers extension tooinstall Windows network device drivers for RDMA connectivity.</span></span> <span data-ttu-id="2b0fa-120">(В некоторых развертываниях экземпляров A8 и A9 hello расширение HpcVmDrivers добавляется автоматически.) tooa расширение ВМ hello tooadd виртуальной Машины, можно использовать [Azure PowerShell](/powershell/azure/overview) командлетов.</span><span class="sxs-lookup"><span data-stu-id="2b0fa-120">(In certain deployments of A8 and A9 instances, hello HpcVmDrivers extension is added automatically.) tooadd hello VM extension tooa VM, you can use [Azure PowerShell](/powershell/azure/overview) cmdlets.</span></span> 

  
  <span data-ttu-id="2b0fa-121">Здравствуйте, следующая команда устанавливает hello последнее расширение HpcVMDrivers версии 1.1 на существующей виртуальной Машине функцией RDMA с именем *myVM* развернут в группе ресурсов hello с именем *myResourceGroup* в hello  *Западная часть США* области:</span><span class="sxs-lookup"><span data-stu-id="2b0fa-121">hello following command installs hello latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named *myVM* deployed in hello resource group named *myResourceGroup* in hello *West US* region:</span></span>

  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  
  <span data-ttu-id="2b0fa-122">Дополнительные сведения см. в статье [Обзор расширений и компонентов виртуальной машины под управлением Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2b0fa-122">For more information, see [Virtual machine extensions and features](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="2b0fa-123">Вы также можете работать с расширениями для виртуальных машин, развернутых в hello [классической модели развертывания](classic/manage-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="2b0fa-123">You can also work with extensions for VMs deployed in hello [classic deployment model](classic/manage-extensions.md).</span></span>


## <a name="using-hpc-pack"></a><span data-ttu-id="2b0fa-124">Использование пакета HPC</span><span class="sxs-lookup"><span data-stu-id="2b0fa-124">Using HPC Pack</span></span>

<span data-ttu-id="2b0fa-125">[Пакет Microsoft HPC](https://technet.microsoft.com/library/jj899572.aspx), корпорации Майкрософт свободного HPC заданиями и кластером решение по управлению, один из вариантов toocreate вычислительного кластера в Azure toorun приложений MPI на основе Windows и других рабочих нагрузок HPC.</span><span class="sxs-lookup"><span data-stu-id="2b0fa-125">[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is one option for you toocreate a compute cluster in Azure toorun Windows-based MPI applications and other HPC workloads.</span></span> <span data-ttu-id="2b0fa-126">HPC Pack 2012 R2 и более поздних версиях включают среду выполнения для MS-MPI, использующий сеть Azure RDMA hello при развертывании на виртуальных машинах функцией RDMA.</span><span class="sxs-lookup"><span data-stu-id="2b0fa-126">HPC Pack 2012 R2 and later versions include a runtime environment for MS-MPI that uses hello Azure RDMA network when deployed on RDMA-capable VMs.</span></span>




## <a name="other-sizes"></a><span data-ttu-id="2b0fa-127">Остальные размеры</span><span class="sxs-lookup"><span data-stu-id="2b0fa-127">Other sizes</span></span>
- [<span data-ttu-id="2b0fa-128">Универсальные</span><span class="sxs-lookup"><span data-stu-id="2b0fa-128">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="2b0fa-129">Оптимизированные для вычислений</span><span class="sxs-lookup"><span data-stu-id="2b0fa-129">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="2b0fa-130">Оптимизированные для памяти</span><span class="sxs-lookup"><span data-stu-id="2b0fa-130">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)
- [<span data-ttu-id="2b0fa-131">Оптимизированные для хранилища</span><span class="sxs-lookup"><span data-stu-id="2b0fa-131">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)
- [<span data-ttu-id="2b0fa-132">Оптимизированные для GPU</span><span class="sxs-lookup"><span data-stu-id="2b0fa-132">GPU optimized</span></span>](sizes-gpu.md)

## <a name="next-steps"></a><span data-ttu-id="2b0fa-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2b0fa-133">Next steps</span></span>

- <span data-ttu-id="2b0fa-134">Контрольные списки toouse hello экземпляров вычислений с помощью пакета HPC в Windows Server, в разделе [настроить кластер Windows RDMA с пакетом HPC приложений MPI toorun](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2b0fa-134">For checklists toouse hello compute-intensive instances with HPC Pack on Windows Server, see [Set up a Windows RDMA cluster with HPC Pack toorun MPI applications](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

- <span data-ttu-id="2b0fa-135">toouse экземпляров с большим объемом вычислений при выполнении приложений MPI с пакетом Azure в разделе [несколькими экземплярами использования задачи toorun приложений интерфейса передачи сообщений (MPI) в пакете Azure](../../batch/batch-mpi.md).</span><span class="sxs-lookup"><span data-stu-id="2b0fa-135">toouse compute-intensive instances when running MPI applications with Azure Batch, see [Use multi-instance tasks toorun Message Passing Interface (MPI) applications in Azure Batch](../../batch/batch-mpi.md).</span></span>

- <span data-ttu-id="2b0fa-136">Узнайте больше о том, как с помощью [единиц вычислений Azure (ACU)](acu.md) сравнить производительность вычислений для различных номеров SKU Azure.</span><span class="sxs-lookup"><span data-stu-id="2b0fa-136">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>




