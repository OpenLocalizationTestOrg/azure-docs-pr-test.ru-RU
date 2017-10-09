---
title: "размеры виртуальных Машин Linux aaaAzure - HPC | Документы Microsoft"
description: "Список hello различные размеры, доступные для высокопроизводительных вычислительных систем виртуальных машин в Azure Linux."
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
ms.openlocfilehash: 0b02ee592902ff8097a71898faea1ac17a947d1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-compute-linux-vm-sizes"></a><span data-ttu-id="00999-103">Размеры виртуальных машин Linux, оптимизированных для HPC</span><span class="sxs-lookup"><span data-stu-id="00999-103">High performance compute Linux VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a><span data-ttu-id="00999-104">Экземпляры с поддержкой RDMA</span><span class="sxs-lookup"><span data-stu-id="00999-104">RDMA-capable instances</span></span>
<span data-ttu-id="00999-105">Подмножество hello экземпляров с большим объемом вычислений (H16r, H16mr, A8 и A9) возможностей сетевой интерфейс для подключения к удаленной памяти прямой доступ (RDMA).</span><span class="sxs-lookup"><span data-stu-id="00999-105">A subset of hello compute-intensive instances (H16r, H16mr, A8, and A9) feature a network interface for remote direct memory access (RDMA) connectivity.</span></span> <span data-ttu-id="00999-106">Этот интерфейс является Кроме размеры виртуальных Машин доступен tooother интерфейс стандартной сети Azure toohello.</span><span class="sxs-lookup"><span data-stu-id="00999-106">This interface is in addition toohello standard Azure network interface available tooother VM sizes.</span></span> 
  
<span data-ttu-id="00999-107">Этот интерфейс позволяет hello функцией RDMA экземпляры toocommunicate сети InfiniBand, работая на скорость FDR H16r и H16mr виртуальной машины и скорости QDR для виртуальных машин A8 и A9.</span><span class="sxs-lookup"><span data-stu-id="00999-107">This interface allows hello RDMA-capable instances toocommunicate over an InfiniBand network, operating at FDR rates for H16r and H16mr virtual machines, and QDR rates for A8 and A9 virtual machines.</span></span> <span data-ttu-id="00999-108">Эти возможности RDMA может значительно повысить hello масштабируемость и производительность приложений интерфейса передачи сообщений (MPI).</span><span class="sxs-lookup"><span data-stu-id="00999-108">These RDMA capabilities can boost hello scalability and performance of Message Passing Interface (MPI) applications.</span></span>

<span data-ttu-id="00999-109">Ниже приведены требования для сети Azure RDMA hello tooaccess функцией RDMA виртуальных машин Linux:</span><span class="sxs-lookup"><span data-stu-id="00999-109">Following are requirements for RDMA-capable Linux VMs tooaccess hello Azure RDMA network:</span></span>
 
* <span data-ttu-id="00999-110">**Распределения** — необходимо развернуть виртуальные машины с поддержкой RDMA SUSE Linux Enterprise Server (SLES) или программного обеспечения Wave незаконных (прежнее название — OpenLogic) на основе CentOS HPC изображений в hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="00999-110">**Distributions** - You must deploy VMs from RDMA-capable SUSE Linux Enterprise Server (SLES) or Rogue Wave Software (formerly OpenLogic) CentOS-based HPC images in hello Azure Marketplace.</span></span> <span data-ttu-id="00999-111">Hello следующих Marketplace образов поддержки подключения RDMA:</span><span class="sxs-lookup"><span data-stu-id="00999-111">hello following Marketplace images support RDMA connectivity:</span></span>
  
    * <span data-ttu-id="00999-112">SLES 12 SP1 для HPC или SLES 12 SP1 для HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="00999-112">SLES 12 SP1 for HPC, or SLES 12 SP1 for HPC (Premium)</span></span>
    
    * <span data-ttu-id="00999-113">7.3 HPC на основе CentOS, 7.1 HPC на основе CentOS, 6.8 HPC на основе CentOS или 6.5 HPC на основе CentOS</span><span class="sxs-lookup"><span data-stu-id="00999-113">CentOS-based 7.3 HPC, CentOS-based 7.1 HPC, CentOS-based 6.8 HPC, or CentOS-based 6.5 HPC</span></span>  
 
        > [!NOTE]
        > <span data-ttu-id="00999-114">Для виртуальных машин серии H рекомендуем использовать образ SLES 12 SP1 для HPC или 7.1 (или более позднюю версию) HPC на основе CentOS.</span><span class="sxs-lookup"><span data-stu-id="00999-114">For H-series VMs, we recommend either a SLES 12 SP1 for HPC image or CentOS-based 7.1 or later HPC image.</span></span>
        >
        > <span data-ttu-id="00999-115">На изображениях HPC на основе CentOS hello, обновления ядра отключены в hello **yum** файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="00999-115">On hello CentOS-based HPC images, kernel updates are disabled in hello **yum** configuration file.</span></span> <span data-ttu-id="00999-116">Это происходит потому hello драйверы Linux RDMA распространяемых в виде пакета RPM и обновления драйверов может не работать, если обновляется hello ядра.</span><span class="sxs-lookup"><span data-stu-id="00999-116">This is because hello Linux RDMA drivers are distributed as an RPM package, and driver updates might not work if hello kernel is updated.</span></span>
        > 
        > 
* <span data-ttu-id="00999-117">**MPI** : Intel MPI Library 5.x</span><span class="sxs-lookup"><span data-stu-id="00999-117">**MPI** - Intel MPI Library 5.x</span></span>
  
    <span data-ttu-id="00999-118">В зависимости от образа Marketplace hello выбирать, отдельные лицензирования, установки, или настройки Intel MPI будет требоваться, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="00999-118">Depending on hello Marketplace image you choose, separate licensing, installation, or configuration of Intel MPI may be needed, as follows:</span></span> 
  
  * <span data-ttu-id="00999-119">**SP1 SLES 12 для образа HPC** -пакеты Intel MPI распространяется на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="00999-119">**SLES 12 SP1 for HPC image** - Intel MPI packages are distributed on hello VM.</span></span> <span data-ttu-id="00999-120">Установите, запустив hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="00999-120">Install by running hello following command:</span></span>

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * <span data-ttu-id="00999-121">**Образы HPC на основе CentOS** — здесь уже установлена библиотека Intel MPI 5.1.</span><span class="sxs-lookup"><span data-stu-id="00999-121">**CentOS-based HPC images**  - Intel MPI 5.1 is already installed.</span></span>  
    
    <span data-ttu-id="00999-122">Дополнительные системные конфигурации — необходимые toorun заданий MPI в кластеризованных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="00999-122">Additional system configuration is needed toorun MPI jobs on clustered VMs.</span></span> <span data-ttu-id="00999-123">Например, в кластере виртуальных машин, необходимо tooestablish доверия между hello вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="00999-123">For example, on a cluster of VMs, you need tooestablish trust among hello compute nodes.</span></span> <span data-ttu-id="00999-124">Типичные параметры в разделе [настройки приложений MPI Linux RDMA toorun кластера](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="00999-124">For typical settings, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

### <a name="network-topology-considerations"></a><span data-ttu-id="00999-125">Аспекты топологии сети</span><span class="sxs-lookup"><span data-stu-id="00999-125">Network topology considerations</span></span>
* <span data-ttu-id="00999-126">На виртуальных машинах Linux с поддержкой RDMA интерфейс Eth1 зарезервирован для сетевого трафика RDMA.</span><span class="sxs-lookup"><span data-stu-id="00999-126">On RDMA-enabled Linux VMs in Azure, Eth1 is reserved for RDMA network traffic.</span></span> <span data-ttu-id="00999-127">Не изменяйте параметры Eth1 или любые сведения в файле конфигурации hello ссылается toothis сети.</span><span class="sxs-lookup"><span data-stu-id="00999-127">Do not change any Eth1 settings or any information in hello configuration file referring toothis network.</span></span> <span data-ttu-id="00999-128">Eth0 зарезервирован для обычного сетевого трафика Azure.</span><span class="sxs-lookup"><span data-stu-id="00999-128">Eth0 is reserved for regular Azure network traffic.</span></span>

* <span data-ttu-id="00999-129">В Azure не поддерживается IP через InfiniBand (IB).</span><span class="sxs-lookup"><span data-stu-id="00999-129">In Azure, IP over InfiniBand (IB) is not supported.</span></span> <span data-ttu-id="00999-130">Поддерживается только RDMA через IB.</span><span class="sxs-lookup"><span data-stu-id="00999-130">Only RDMA over IB is supported.</span></span>

## <a name="using-hpc-pack"></a><span data-ttu-id="00999-131">Использование пакета HPC</span><span class="sxs-lookup"><span data-stu-id="00999-131">Using HPC Pack</span></span>
<span data-ttu-id="00999-132">[Пакет HPC](https://technet.microsoft.com/library/jj899572.aspx), корпорации Майкрософт свободного HPC заданиями и кластером решение по управлению, один из вариантов для вас экземпляров вычислений hello toouse с Linux.</span><span class="sxs-lookup"><span data-stu-id="00999-132">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is one option for you toouse hello compute-intensive instances with Linux.</span></span> <span data-ttu-id="00999-133">последние версии Hello HPC Pack поддерживает несколько дистрибутивов Linux, toorun на вычислительных узлов, развернутые в виртуальных машинах Azure, под управлением Windows Server головного узла.</span><span class="sxs-lookup"><span data-stu-id="00999-133">hello latest releases of HPC Pack support several Linux distributions toorun on compute nodes deployed in Azure VMs, managed by a Windows Server head node.</span></span> <span data-ttu-id="00999-134">С поддержкой RDMA Linux вычислительных узлов под управлением Intel MPI пакет HPC можно планирование и запуск приложений Linux MPI доступа к сети RDMA hello.</span><span class="sxs-lookup"><span data-stu-id="00999-134">With RDMA-capable Linux compute nodes running Intel MPI, HPC Pack can schedule and run Linux MPI applications that access hello RDMA network.</span></span> <span data-ttu-id="00999-135">Ознакомьтесь со статьей [Начало работы с вычислительными узлами Linux в кластере пакета HPC в Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="00999-135">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="other-sizes"></a><span data-ttu-id="00999-136">Остальные размеры</span><span class="sxs-lookup"><span data-stu-id="00999-136">Other sizes</span></span>
- [<span data-ttu-id="00999-137">Универсальные</span><span class="sxs-lookup"><span data-stu-id="00999-137">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="00999-138">Оптимизированные для вычислений</span><span class="sxs-lookup"><span data-stu-id="00999-138">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="00999-139">Оптимизированные для памяти</span><span class="sxs-lookup"><span data-stu-id="00999-139">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="00999-140">Оптимизированные для хранилища</span><span class="sxs-lookup"><span data-stu-id="00999-140">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="00999-141">GPU</span><span class="sxs-lookup"><span data-stu-id="00999-141">GPU</span></span>](../windows/sizes-gpu.md)


## <a name="next-steps"></a><span data-ttu-id="00999-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="00999-142">Next steps</span></span>

- <span data-ttu-id="00999-143">tooget запущена, развертывание и использование размера большим объемом вычислений с RDMA в Linux, см. [настройки приложений MPI toorun кластеров Linux RDMA](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="00999-143">tooget started deploying and using compute-intensive sizes with RDMA on Linux, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

- <span data-ttu-id="00999-144">Узнайте больше о том, как с помощью [единиц вычислений Azure (ACU)](acu.md) сравнить производительность вычислений для различных номеров SKU Azure.</span><span class="sxs-lookup"><span data-stu-id="00999-144">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>




