---
title: "Размеры виртуальных машин Windows в Azure, оптимизированных для рабочих нагрузок HPC | Документация Майкрософт"
description: "Список различных размеров виртуальных машин Windows в Azure, оптимизированных для высокопроизводительных вычислений."
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
ms.openlocfilehash: a0596d134e9c26877848f93d72f35bfd2c957570
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="high-performance-compute-vm-sizes"></a><span data-ttu-id="50863-103">Размеры виртуальных машин, оптимизированных для высокопроизводительных вычислений</span><span class="sxs-lookup"><span data-stu-id="50863-103">High performance compute VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a><span data-ttu-id="50863-104">Экземпляры с поддержкой RDMA</span><span class="sxs-lookup"><span data-stu-id="50863-104">RDMA-capable instances</span></span>
<span data-ttu-id="50863-105">Подмножество экземпляров для ресурсоемких вычислений (H16r, H16mr, A8 и A9) представляет собой сетевой интерфейс для подключения с удаленным доступом к памяти (RDMA).</span><span class="sxs-lookup"><span data-stu-id="50863-105">A subset of the compute-intensive instances (H16r, H16mr, A8, and A9) feature a network interface for remote direct memory access (RDMA) connectivity.</span></span> <span data-ttu-id="50863-106">Этот интерфейс является дополнением к стандартному сетевому интерфейсу Azure, который доступен для виртуальных машин других размеров.</span><span class="sxs-lookup"><span data-stu-id="50863-106">This interface is in addition to the standard Azure network interface available to other VM sizes.</span></span> 
  
<span data-ttu-id="50863-107">Этот интерфейс обеспечивает связь экземпляров с поддержкой RDMA при помощи сети InfiniBand, работающей на скорости FDR для виртуальных машин H16r и H16mr и на скорости QDR для виртуальных машин A8 и A9.</span><span class="sxs-lookup"><span data-stu-id="50863-107">This interface allows the RDMA-capable instances to communicate over an InfiniBand network, operating at FDR rates for H16r and H16mr virtual machines, and QDR rates for A8 and A9 virtual machines.</span></span> <span data-ttu-id="50863-108">Эти возможности RDMA позволяют увеличить масштабируемость и производительность приложений с интерфейсом MPI.</span><span class="sxs-lookup"><span data-stu-id="50863-108">These RDMA capabilities can boost the scalability and performance of Message Passing Interface (MPI) applications.</span></span>

<span data-ttu-id="50863-109">Ниже приведены требования к виртуальным машинам Windows с поддержкой RDMA для получения доступа к сети Azure RDMA.</span><span class="sxs-lookup"><span data-stu-id="50863-109">Following are requirements for RDMA-capable Windows VMs to access the Azure RDMA network:</span></span> 

* <span data-ttu-id="50863-110">**Операционная система**</span><span class="sxs-lookup"><span data-stu-id="50863-110">**Operating system**</span></span>
  
  <span data-ttu-id="50863-111">Windows Server 2012 R2, Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="50863-111">Windows Server 2012 R2, Windows Server 2012</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="50863-112">Сейчас соединение RDMA в Azure не поддерживается в Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="50863-112">Currently, Windows Server 2016 does not support RDMA connectivity in Azure.</span></span>
  >

* <span data-ttu-id="50863-113">**Группа доступности или облачная служба**. Виртуальные машины с поддержкой RDMA следует развертывать в одной и той же группе доступности (при использовании модели развертывания с помощью Azure Resource Manager) или в одной и той же облачной службе (при использовании классической модели развертывания).</span><span class="sxs-lookup"><span data-stu-id="50863-113">**Availability set or cloud service** – Deploy the RDMA-capable VMs in the same availability set (when you use the Azure Resource Manager deployment model) or the same cloud service (when you use the classic deployment model).</span></span> <span data-ttu-id="50863-114">При использовании пакетной службы Azure виртуальные машины с поддержкой RDMA должны находиться в одном пуле.</span><span class="sxs-lookup"><span data-stu-id="50863-114">If you use Azure Batch, the RDMA-capable VMs must be in the same pool.</span></span>

* <span data-ttu-id="50863-115">**MPI** — Microsoft MPI (MS-MPI) 2012 R2 и более поздних версий, библиотека Intel MPI 5.x.</span><span class="sxs-lookup"><span data-stu-id="50863-115">**MPI** - Microsoft MPI (MS-MPI) 2012 R2 or later, Intel MPI Library 5.x</span></span>

  <span data-ttu-id="50863-116">Для взаимодействия между экземплярами поддерживаемые реализации MPI используют интерфейс Microsoft Network Direct.</span><span class="sxs-lookup"><span data-stu-id="50863-116">Supported MPI implementations use the Microsoft Network Direct interface to communicate between instances.</span></span> 

* <span data-ttu-id="50863-117">**Адресное пространство сети RDMA.** Сеть RDMA в Azure резервирует адресное пространство 172.16.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="50863-117">**RDMA network address space** - The RDMA network in Azure reserves the address space 172.16.0.0/16.</span></span> <span data-ttu-id="50863-118">Чтобы выполнять приложения MPI в экземплярах, развернутых в виртуальной сети Azure, убедитесь, что адресное пространство виртуальной сети не пересекается с сетью RDMA.</span><span class="sxs-lookup"><span data-stu-id="50863-118">To run MPI applications on instances deployed in an Azure virtual network, make sure that the virtual network address space does not overlap the RDMA network.</span></span>

* <span data-ttu-id="50863-119">**Расширение виртуальных машин HpcVmDrivers**. На виртуальных машинах с поддержкой RDMA необходимо добавить расширение HpcVmDrivers для установки драйверов сетевых устройств Windows, обеспечивающих подключение RDMA.</span><span class="sxs-lookup"><span data-stu-id="50863-119">**HpcVmDrivers VM extension** - On RDMA-capable VMs, you must add the HpcVmDrivers extension to install Windows network device drivers for RDMA connectivity.</span></span> <span data-ttu-id="50863-120">(В некоторых развертываниях экземпляров A8 и A9 расширение HpcVmDrivers добавляется автоматически.) Чтобы добавить в виртуальную машину расширение виртуальной машины, можно использовать командлеты [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="50863-120">(In certain deployments of A8 and A9 instances, the HpcVmDrivers extension is added automatically.) To add the VM extension to a VM, you can use [Azure PowerShell](/powershell/azure/overview) cmdlets.</span></span> 

  
  <span data-ttu-id="50863-121">Следующая команда устанавливает последнюю версию (1.1) расширения HpcVMDrivers на существующую виртуальную машину с поддержкой RDMA, которая носит имя *myVM*. Эта машина развернута в группе ресурсов с именем *myResourceGroup* в регионе *Западная часть США*:</span><span class="sxs-lookup"><span data-stu-id="50863-121">The following command installs the latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named *myVM* deployed in the resource group named *myResourceGroup* in the *West US* region:</span></span>

  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  
  <span data-ttu-id="50863-122">Дополнительные сведения см. в статье [Обзор расширений и компонентов виртуальной машины под управлением Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="50863-122">For more information, see [Virtual machine extensions and features](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="50863-123">Вы также можете работать с расширениями для виртуальных машин, развернутых в рамках [классической модели развертывания](classic/manage-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="50863-123">You can also work with extensions for VMs deployed in the [classic deployment model](classic/manage-extensions.md).</span></span>


## <a name="using-hpc-pack"></a><span data-ttu-id="50863-124">Использование пакета HPC</span><span class="sxs-lookup"><span data-stu-id="50863-124">Using HPC Pack</span></span>

<span data-ttu-id="50863-125">[Пакет Microsoft HPC](https://technet.microsoft.com/library/jj899572.aspx). Бесплатный кластер высокопроизводительных вычислений Майкрософт и решение для управления заданиями — это один из вариантов создания вычислительного кластера в Azure для выполнения приложений MPI под управлением Windows и других рабочих нагрузок HPC.</span><span class="sxs-lookup"><span data-stu-id="50863-125">[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is one option for you to create a compute cluster in Azure to run Windows-based MPI applications and other HPC workloads.</span></span> <span data-ttu-id="50863-126">Пакет HPC 2012 R2 и более поздних версий включает среду выполнения для MS-MPI, которая использует сеть Azure RDMA при развертывании на виртуальных машинах с поддержкой RDMA.</span><span class="sxs-lookup"><span data-stu-id="50863-126">HPC Pack 2012 R2 and later versions include a runtime environment for MS-MPI that uses the Azure RDMA network when deployed on RDMA-capable VMs.</span></span>




## <a name="other-sizes"></a><span data-ttu-id="50863-127">Остальные размеры</span><span class="sxs-lookup"><span data-stu-id="50863-127">Other sizes</span></span>
- [<span data-ttu-id="50863-128">Универсальные</span><span class="sxs-lookup"><span data-stu-id="50863-128">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="50863-129">Оптимизированные для вычислений</span><span class="sxs-lookup"><span data-stu-id="50863-129">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="50863-130">Оптимизированные для памяти</span><span class="sxs-lookup"><span data-stu-id="50863-130">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)
- [<span data-ttu-id="50863-131">Оптимизированные для хранилища</span><span class="sxs-lookup"><span data-stu-id="50863-131">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)
- [<span data-ttu-id="50863-132">Оптимизированные для GPU</span><span class="sxs-lookup"><span data-stu-id="50863-132">GPU optimized</span></span>](sizes-gpu.md)

## <a name="next-steps"></a><span data-ttu-id="50863-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="50863-133">Next steps</span></span>

- <span data-ttu-id="50863-134">Контрольные списки для использования экземпляров с большим объемом вычислений с пакетом HPC на Windows Server см. в статье [Настройка кластера RDMA в Windows с помощью пакета HPC для запуска приложений MPI](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="50863-134">For checklists to use the compute-intensive instances with HPC Pack on Windows Server, see [Set up a Windows RDMA cluster with HPC Pack to run MPI applications](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

- <span data-ttu-id="50863-135">Сведения об использовании экземпляров для ресурсоемких вычислений при запуске приложений MPI с использованием пакетной службы Azure см. в статье [Использование задач с несколькими экземплярами для запуска приложений с интерфейсом передачи сообщений в пакетной службе](../../batch/batch-mpi.md).</span><span class="sxs-lookup"><span data-stu-id="50863-135">To use compute-intensive instances when running MPI applications with Azure Batch, see [Use multi-instance tasks to run Message Passing Interface (MPI) applications in Azure Batch](../../batch/batch-mpi.md).</span></span>

- <span data-ttu-id="50863-136">Узнайте больше о том, как с помощью [единиц вычислений Azure (ACU)](acu.md) сравнить производительность вычислений для различных номеров SKU Azure.</span><span class="sxs-lookup"><span data-stu-id="50863-136">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>




