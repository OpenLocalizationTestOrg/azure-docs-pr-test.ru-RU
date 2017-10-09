---
title: "aaaAbout вычислений виртуальных машин с Linux | Документы Microsoft"
description: "Справочные сведения и рекомендации по использованию hello H-series и A8, A9, A10 и A11 вычислений размеры виртуальных машин Linux"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 16cf6e2d-f401-4b22-af8c-9a337179f5f6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 37636840a3f809ac19354a5a7993257216f675f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="about-h-series-and-compute-intensive-a-series-vms-for-linux"></a><span data-ttu-id="72631-103">Сведения об экземплярах серии H и серии A для ресурсоемких вычислений для Linux</span><span class="sxs-lookup"><span data-stu-id="72631-103">About H-series and compute-intensive A-series VMs for Linux</span></span>
<span data-ttu-id="72631-104">Вот основные сведения и некоторые рекомендации по использованию hello Azure H ряд новых и hello предыдущих размеров A8, A9, A10 и A11, также известный как *вычислений* экземпляров.</span><span class="sxs-lookup"><span data-stu-id="72631-104">Here is background information and some considerations for using hello newer Azure H-series and hello earlier A8, A9, A10, and A11 sizes, also known as *compute-intensive* instances.</span></span> <span data-ttu-id="72631-105">Эта статья посвящена применению этих размеров на виртуальных машинах Linux.</span><span class="sxs-lookup"><span data-stu-id="72631-105">This article focuses on using these sizes for Linux VMs.</span></span> <span data-ttu-id="72631-106">Сведения в этой статье можно также использовать для [виртуальных машин Windows](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="72631-106">You can also use them for [Windows VMs](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="72631-107">Основные характеристики, сведения о дисках и объеме памяти см. в статье [Размеры виртуальных машин в Azure](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="72631-107">For basic specs, storage capacities, and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="access-toohello-rdma-network"></a><span data-ttu-id="72631-108">Доступа к сети RDMA toohello</span><span class="sxs-lookup"><span data-stu-id="72631-108">Access toohello RDMA network</span></span>
<span data-ttu-id="72631-109">Можно создать кластеры с поддержкой RDMA виртуальных машин Linux, выполните одну из следующих поддерживаемых дистрибутивах Linux HPC и поддерживаемых преимущества tootake реализации MPI сети Azure RDMA hello hello.</span><span class="sxs-lookup"><span data-stu-id="72631-109">You can create clusters of RDMA-capable Linux VMs that run one of hello following supported Linux HPC distributions and a supported MPI implementation tootake advantage of hello Azure RDMA network.</span></span> <span data-ttu-id="72631-110">В разделе [настройки приложений MPI toorun кластеров Linux RDMA](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) для параметров развертывания и шаги настройки образца.</span><span class="sxs-lookup"><span data-stu-id="72631-110">See [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) for deployment options and sample configuration steps.</span></span>

* <span data-ttu-id="72631-111">**Распределения** — необходимо развернуть виртуальные машины с поддержкой RDMA SUSE Linux Enterprise Server (SLES) или программного обеспечения Wave незаконных (прежнее название — OpenLogic) на основе CentOS HPC изображений в hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="72631-111">**Distributions** - You must deploy VMs from RDMA-capable SUSE Linux Enterprise Server (SLES) or Rogue Wave Software (formerly OpenLogic) CentOS-based HPC images in hello Azure Marketplace.</span></span> <span data-ttu-id="72631-112">Hello следующих Marketplace образов поддержки подключения RDMA:</span><span class="sxs-lookup"><span data-stu-id="72631-112">hello following Marketplace images support RDMA connectivity:</span></span>
  
    * <span data-ttu-id="72631-113">SLES 12 SP1 для HPC, SLES 12 SP1 для HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="72631-113">SLES 12 SP1 for HPC, SLES 12 SP1 for HPC (Premium)</span></span>
    
    * <span data-ttu-id="72631-114">7.1 HPC на основе CentOS, 6.5 HPC на основе CentOS.</span><span class="sxs-lookup"><span data-stu-id="72631-114">CentOS-based 7.1 HPC, CentOS-based 6.5 HPC</span></span>  
 
        > [!NOTE]
        > <span data-ttu-id="72631-115">Для виртуальных машин серии H рекомендуем использовать образ SLES 12 SP1 для HPC или 7.1 HPC на основе CentOS.</span><span class="sxs-lookup"><span data-stu-id="72631-115">For H-series VMs, we recommend either a SLES 12 SP1 for HPC image or CentOS-based 7.1 HPC image.</span></span>
        >
        > <span data-ttu-id="72631-116">На изображениях HPC на основе CentOS hello, обновления ядра отключены в hello **yum** файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="72631-116">On hello CentOS-based HPC images, kernel updates are disabled in hello **yum** configuration file.</span></span> <span data-ttu-id="72631-117">Это происходит потому hello драйверы Linux RDMA распространяемых в виде пакета RPM и обновления драйверов может не работать, если обновляется hello ядра.</span><span class="sxs-lookup"><span data-stu-id="72631-117">This is because hello Linux RDMA drivers are distributed as an RPM package, and driver updates might not work if hello kernel is updated.</span></span>
        > 
        > 
* <span data-ttu-id="72631-118">**MPI** : Intel MPI Library 5.x</span><span class="sxs-lookup"><span data-stu-id="72631-118">**MPI** - Intel MPI Library 5.x</span></span>
  
    <span data-ttu-id="72631-119">В зависимости от образа Marketplace hello выбирать, отдельные лицензирования, установки, или настройки Intel MPI будет требоваться, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="72631-119">Depending on hello Marketplace image you choose, separate licensing, installation, or configuration of Intel MPI may be needed, as follows:</span></span> 
  
  * <span data-ttu-id="72631-120">**SP1 SLES 12 для образа HPC** -пакеты Intel MPI распространяется на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="72631-120">**SLES 12 SP1 for HPC image** - Intel MPI packages are distributed on hello VM.</span></span> <span data-ttu-id="72631-121">Установите, запустив hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="72631-121">Install by running hello following command:</span></span>

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * <span data-ttu-id="72631-122">**Образы HPC на основе CentOS** — здесь уже установлена библиотека Intel MPI 5.1.</span><span class="sxs-lookup"><span data-stu-id="72631-122">**CentOS-based HPC images**  - Intel MPI 5.1 is already installed.</span></span>  
    
    <span data-ttu-id="72631-123">Дополнительные системные конфигурации — необходимые toorun заданий MPI в кластеризованных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="72631-123">Additional system configuration is needed toorun MPI jobs on clustered VMs.</span></span> <span data-ttu-id="72631-124">Например, в кластере виртуальных машин, необходимо tooestablish доверия между hello вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="72631-124">For example, on a cluster of VMs, you need tooestablish trust among hello compute nodes.</span></span> <span data-ttu-id="72631-125">Типичные параметры в разделе [настройки приложений MPI toorun кластеров Linux RDMA](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="72631-125">For typical settings, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="considerations-for-hpc-pack-and-linux"></a><span data-ttu-id="72631-126">Рекомендации по использованию пакета HPC и Linux</span><span class="sxs-lookup"><span data-stu-id="72631-126">Considerations for HPC Pack and Linux</span></span>
<span data-ttu-id="72631-127">[Пакет HPC](https://technet.microsoft.com/library/jj899572.aspx), свободного HPC заданиями и кластером решении для управления Майкрософт, предоставляет один вариант toouse hello вычислений экземпляры с Linux.</span><span class="sxs-lookup"><span data-stu-id="72631-127">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, provides one option for you toouse hello compute-intensive instances with Linux.</span></span> <span data-ttu-id="72631-128">последние версии Hello HPC Pack поддерживает несколько дистрибутивов Linux, toorun на вычислительных узлов, развернутые в виртуальных машинах Azure, под управлением Windows Server головного узла.</span><span class="sxs-lookup"><span data-stu-id="72631-128">hello latest releases of HPC Pack support several Linux distributions toorun on compute nodes deployed in Azure VMs, managed by a Windows Server head node.</span></span> <span data-ttu-id="72631-129">С поддержкой RDMA Linux вычислительных узлов под управлением Intel MPI пакет HPC можно планирование и запуск приложений Linux MPI доступа к сети RDMA hello.</span><span class="sxs-lookup"><span data-stu-id="72631-129">With RDMA-capable Linux compute nodes running Intel MPI, HPC Pack can schedule and run Linux MPI applications that access hello RDMA network.</span></span> <span data-ttu-id="72631-130">tooget работы см. в разделе [Приступая к работе с Linux вычислительных узлов в кластере HPC Pack в Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="72631-130">tooget started, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="network-topology-considerations"></a><span data-ttu-id="72631-131">Аспекты топологии сети</span><span class="sxs-lookup"><span data-stu-id="72631-131">Network topology considerations</span></span>
* <span data-ttu-id="72631-132">На виртуальных машинах Linux с поддержкой RDMA интерфейс Eth1 зарезервирован для сетевого трафика RDMA.</span><span class="sxs-lookup"><span data-stu-id="72631-132">On RDMA-enabled Linux VMs in Azure, Eth1 is reserved for RDMA network traffic.</span></span> <span data-ttu-id="72631-133">Не изменяйте параметры Eth1 или любые сведения в файле конфигурации hello ссылается toothis сети.</span><span class="sxs-lookup"><span data-stu-id="72631-133">Do not change any Eth1 settings or any information in hello configuration file referring toothis network.</span></span> <span data-ttu-id="72631-134">Eth0 зарезервирован для обычного сетевого трафика Azure.</span><span class="sxs-lookup"><span data-stu-id="72631-134">Eth0 is reserved for regular Azure network traffic.</span></span>
* <span data-ttu-id="72631-135">В Azure не поддерживается IP через InfiniBand (IB).</span><span class="sxs-lookup"><span data-stu-id="72631-135">In Azure, IP over InfiniBand (IB) is not supported.</span></span> <span data-ttu-id="72631-136">Поддерживается только RDMA через IB.</span><span class="sxs-lookup"><span data-stu-id="72631-136">Only RDMA over IB is supported.</span></span>



## <a name="next-steps"></a><span data-ttu-id="72631-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="72631-137">Next steps</span></span>
* <span data-ttu-id="72631-138">Дополнительные сведения о доступности и расценках размеров hello большим объемом вычислений см [ценах — виртуальные машины](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span><span class="sxs-lookup"><span data-stu-id="72631-138">For details about availability and pricing of hello compute-intensive sizes, see [Virtual Machines pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span></span>
* <span data-ttu-id="72631-139">Сведения о дисках и объеме памяти см. в статье [Размеры виртуальных машин в Azure](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="72631-139">For storage capacities and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="72631-140">tooget запущена, развертывание и использование размера большим объемом вычислений с RDMA в Linux, см. [настройки приложений MPI toorun кластеров Linux RDMA](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="72631-140">tooget started deploying and using compute-intensive sizes with RDMA on Linux, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

