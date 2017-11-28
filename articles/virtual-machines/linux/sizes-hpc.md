---
title: "Размеры виртуальных машин Linux в Azure, оптимизированных для HPC | Документация Майкрософт"
description: "Список различных размеров виртуальных машин Linux в Azure, оптимизированных для высокопроизводительных вычислений."
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: b7a3844ce86b4efac8a4fc3c2540e7b6460873a2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="high-performance-compute-linux-vm-sizes"></a><span data-ttu-id="b0b80-103">Размеры виртуальных машин Linux, оптимизированных для HPC</span><span class="sxs-lookup"><span data-stu-id="b0b80-103">High performance compute Linux VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a><span data-ttu-id="b0b80-104">Экземпляры с поддержкой RDMA</span><span class="sxs-lookup"><span data-stu-id="b0b80-104">RDMA-capable instances</span></span>
<span data-ttu-id="b0b80-105">Подмножество экземпляров для ресурсоемких вычислений (H16r, H16mr, A8 и A9) представляет собой сетевой интерфейс для подключения с удаленным доступом к памяти (RDMA).</span><span class="sxs-lookup"><span data-stu-id="b0b80-105">A subset of the compute-intensive instances (H16r, H16mr, A8, and A9) feature a network interface for remote direct memory access (RDMA) connectivity.</span></span> <span data-ttu-id="b0b80-106">Этот интерфейс является дополнением к стандартному сетевому интерфейсу Azure, который доступен для виртуальных машин других размеров.</span><span class="sxs-lookup"><span data-stu-id="b0b80-106">This interface is in addition to the standard Azure network interface available to other VM sizes.</span></span> 
  
<span data-ttu-id="b0b80-107">Этот интерфейс обеспечивает связь экземпляров с поддержкой RDMA при помощи сети InfiniBand, работающей на скорости FDR для виртуальных машин H16r и H16mr и на скорости QDR для виртуальных машин A8 и A9.</span><span class="sxs-lookup"><span data-stu-id="b0b80-107">This interface allows the RDMA-capable instances to communicate over an InfiniBand network, operating at FDR rates for H16r and H16mr virtual machines, and QDR rates for A8 and A9 virtual machines.</span></span> <span data-ttu-id="b0b80-108">Эти возможности RDMA позволяют увеличить масштабируемость и производительность приложений с интерфейсом MPI.</span><span class="sxs-lookup"><span data-stu-id="b0b80-108">These RDMA capabilities can boost the scalability and performance of Message Passing Interface (MPI) applications.</span></span>

<span data-ttu-id="b0b80-109">Ниже приведены требования к виртуальным машинам Linux с поддержкой RDMA для получения доступа к сети Azure RDMA.</span><span class="sxs-lookup"><span data-stu-id="b0b80-109">Following are requirements for RDMA-capable Linux VMs to access the Azure RDMA network:</span></span>
 
* <span data-ttu-id="b0b80-110">**Дистрибутивы** — разверните виртуальные машины из образов SUSE Linux Enterprise Server (SLES) или Rogue Wave Software (ранее OpenLogic) CentOS HPC с поддержкой RDMA, доступных в Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b0b80-110">**Distributions** - You must deploy VMs from RDMA-capable SUSE Linux Enterprise Server (SLES) or Rogue Wave Software (formerly OpenLogic) CentOS-based HPC images in the Azure Marketplace.</span></span> <span data-ttu-id="b0b80-111">Соединение RDMA поддерживается в следующих образах Marketplace:</span><span class="sxs-lookup"><span data-stu-id="b0b80-111">The following Marketplace images support RDMA connectivity:</span></span>
  
    * <span data-ttu-id="b0b80-112">SLES 12 SP1 для HPC или SLES 12 SP1 для HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="b0b80-112">SLES 12 SP1 for HPC, or SLES 12 SP1 for HPC (Premium)</span></span>
    
    * <span data-ttu-id="b0b80-113">7.3 HPC на основе CentOS, 7.1 HPC на основе CentOS, 6.8 HPC на основе CentOS или 6.5 HPC на основе CentOS</span><span class="sxs-lookup"><span data-stu-id="b0b80-113">CentOS-based 7.3 HPC, CentOS-based 7.1 HPC, CentOS-based 6.8 HPC, or CentOS-based 6.5 HPC</span></span>  
 
        > [!NOTE]
        > <span data-ttu-id="b0b80-114">Для виртуальных машин серии H рекомендуем использовать образ SLES 12 SP1 для HPC или 7.1 (или более позднюю версию) HPC на основе CentOS.</span><span class="sxs-lookup"><span data-stu-id="b0b80-114">For H-series VMs, we recommend either a SLES 12 SP1 for HPC image or CentOS-based 7.1 or later HPC image.</span></span>
        >
        > <span data-ttu-id="b0b80-115">В образах HPC на основе CentOS обновления ядра отключены в файле конфигурации **yum** .</span><span class="sxs-lookup"><span data-stu-id="b0b80-115">On the CentOS-based HPC images, kernel updates are disabled in the **yum** configuration file.</span></span> <span data-ttu-id="b0b80-116">Это связано с тем, что драйверы Linux RDMA распространяются в виде пакета RPM и обновления драйверов могут не сработать в случае обновления ядра.</span><span class="sxs-lookup"><span data-stu-id="b0b80-116">This is because the Linux RDMA drivers are distributed as an RPM package, and driver updates might not work if the kernel is updated.</span></span>
        > 
        > 
* <span data-ttu-id="b0b80-117">**MPI** : Intel MPI Library 5.x</span><span class="sxs-lookup"><span data-stu-id="b0b80-117">**MPI** - Intel MPI Library 5.x</span></span>
  
    <span data-ttu-id="b0b80-118">В зависимости от того, какой образ вы выберете на Marketplace, может потребоваться лицензирование, установка или настройка Intel MPI, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="b0b80-118">Depending on the Marketplace image you choose, separate licensing, installation, or configuration of Intel MPI may be needed, as follows:</span></span> 
  
  * <span data-ttu-id="b0b80-119">**Образ SLES 12 SP1 для HPC** — пакеты Intel MPI, размещенные на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="b0b80-119">**SLES 12 SP1 for HPC image** - Intel MPI packages are distributed on the VM.</span></span> <span data-ttu-id="b0b80-120">Установите , выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b0b80-120">Install by running the following command:</span></span>

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * <span data-ttu-id="b0b80-121">**Образы HPC на основе CentOS** — здесь уже установлена библиотека Intel MPI 5.1.</span><span class="sxs-lookup"><span data-stu-id="b0b80-121">**CentOS-based HPC images**  - Intel MPI 5.1 is already installed.</span></span>  
    
    <span data-ttu-id="b0b80-122">Потребуется дополнительная настройка системы для выполнения заданий MPI на кластеризованных виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="b0b80-122">Additional system configuration is needed to run MPI jobs on clustered VMs.</span></span> <span data-ttu-id="b0b80-123">Например, следует установить доверительные отношения между вычислительными узлами в кластере виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="b0b80-123">For example, on a cluster of VMs, you need to establish trust among the compute nodes.</span></span> <span data-ttu-id="b0b80-124">Типичные примеры настройки можно найти в статье [Настройка кластера Linux RDMA для выполнения приложений MPI](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b0b80-124">For typical settings, see [Set up a Linux RDMA cluster to run MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

### <a name="network-topology-considerations"></a><span data-ttu-id="b0b80-125">Аспекты топологии сети</span><span class="sxs-lookup"><span data-stu-id="b0b80-125">Network topology considerations</span></span>
* <span data-ttu-id="b0b80-126">На виртуальных машинах Linux с поддержкой RDMA интерфейс Eth1 зарезервирован для сетевого трафика RDMA.</span><span class="sxs-lookup"><span data-stu-id="b0b80-126">On RDMA-enabled Linux VMs in Azure, Eth1 is reserved for RDMA network traffic.</span></span> <span data-ttu-id="b0b80-127">Не изменяйте параметры Eth1 и любые данные в файле конфигурации при обращении к этой сети.</span><span class="sxs-lookup"><span data-stu-id="b0b80-127">Do not change any Eth1 settings or any information in the configuration file referring to this network.</span></span> <span data-ttu-id="b0b80-128">Eth0 зарезервирован для обычного сетевого трафика Azure.</span><span class="sxs-lookup"><span data-stu-id="b0b80-128">Eth0 is reserved for regular Azure network traffic.</span></span>

* <span data-ttu-id="b0b80-129">В Azure не поддерживается IP через InfiniBand (IB).</span><span class="sxs-lookup"><span data-stu-id="b0b80-129">In Azure, IP over InfiniBand (IB) is not supported.</span></span> <span data-ttu-id="b0b80-130">Поддерживается только RDMA через IB.</span><span class="sxs-lookup"><span data-stu-id="b0b80-130">Only RDMA over IB is supported.</span></span>

## <a name="using-hpc-pack"></a><span data-ttu-id="b0b80-131">Использование пакета HPC</span><span class="sxs-lookup"><span data-stu-id="b0b80-131">Using HPC Pack</span></span>
<span data-ttu-id="b0b80-132">Для использования экземпляров для ресурсоемких вычислений в Linux можно применить [пакет Microsoft HPC](https://technet.microsoft.com/library/jj899572.aspx) (бесплатное решение по управлению кластерами и заданиями HPC).</span><span class="sxs-lookup"><span data-stu-id="b0b80-132">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is one option for you to use the compute-intensive instances with Linux.</span></span> <span data-ttu-id="b0b80-133">Последние выпуски пакета HPC поддерживают несколько дистрибутивов Linux, выполняемых на вычислительных узлах, развернутых в виртуальных машинах Azure, под управлением головного узла Windows Server.</span><span class="sxs-lookup"><span data-stu-id="b0b80-133">The latest releases of HPC Pack support several Linux distributions to run on compute nodes deployed in Azure VMs, managed by a Windows Server head node.</span></span> <span data-ttu-id="b0b80-134">Используя вычислительные узлы Linux с поддержкой RDMA и Intel MPI, пакет HPC может планировать и выполнять приложения Linux MPI, которые обращаются к сети RDMA.</span><span class="sxs-lookup"><span data-stu-id="b0b80-134">With RDMA-capable Linux compute nodes running Intel MPI, HPC Pack can schedule and run Linux MPI applications that access the RDMA network.</span></span> <span data-ttu-id="b0b80-135">Ознакомьтесь со статьей [Начало работы с вычислительными узлами Linux в кластере пакета HPC в Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b0b80-135">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="other-sizes"></a><span data-ttu-id="b0b80-136">Остальные размеры</span><span class="sxs-lookup"><span data-stu-id="b0b80-136">Other sizes</span></span>
- [<span data-ttu-id="b0b80-137">Универсальные</span><span class="sxs-lookup"><span data-stu-id="b0b80-137">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="b0b80-138">Оптимизированные для вычислений</span><span class="sxs-lookup"><span data-stu-id="b0b80-138">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="b0b80-139">Оптимизированные для памяти</span><span class="sxs-lookup"><span data-stu-id="b0b80-139">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="b0b80-140">Оптимизированные для хранилища</span><span class="sxs-lookup"><span data-stu-id="b0b80-140">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="b0b80-141">GPU</span><span class="sxs-lookup"><span data-stu-id="b0b80-141">GPU</span></span>](../windows/sizes-gpu.md)


## <a name="next-steps"></a><span data-ttu-id="b0b80-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b0b80-142">Next steps</span></span>

- <span data-ttu-id="b0b80-143">Чтобы приступить к развертыванию и использованию виртуальных машин Linux для ресурсоемких вычислений с поддержкой RDMA, изучите статью [Настройка кластера Linux RDMA для выполнения приложений MPI](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b0b80-143">To get started deploying and using compute-intensive sizes with RDMA on Linux, see [Set up a Linux RDMA cluster to run MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

- <span data-ttu-id="b0b80-144">Узнайте больше о том, как с помощью [единиц вычислений Azure (ACU)](acu.md) сравнить производительность вычислений для различных номеров SKU Azure.</span><span class="sxs-lookup"><span data-stu-id="b0b80-144">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>




