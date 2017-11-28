---
title: "Параметры кластера HPC Pack aaaLinux в облаке hello | Документы Microsoft"
description: "Дополнительные сведения о параметрах с помощью пакета Microsoft HPC toocreate и управления ими Linux представляющие высокопроизводительные вычислительные системы (HPC) кластера в облаке Azure hello"
services: virtual-machines-linux,cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: ac60624e-aefa-40c3-8bc1-ef6d5c0ef1a2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 02/06/2017
ms.author: danlep
ms.openlocfilehash: 60d093b466f44a0391815842c421c328e8c7a0d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="options-with-hpc-pack-toocreate-and-manage-an-hpc-cluster-in-azure-for-linux-workloads"></a><span data-ttu-id="608fc-103">Параметры с пакетом HPC toocreate и управления ими кластер HPC в Azure для рабочих нагрузок Linux</span><span class="sxs-lookup"><span data-stu-id="608fc-103">Options with HPC Pack toocreate and manage an HPC cluster in Azure for Linux workloads</span></span>
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

<span data-ttu-id="608fc-104">Эта статья посвящена рабочих нагрузок HPC Pack toorun параметры toouse Linux.</span><span class="sxs-lookup"><span data-stu-id="608fc-104">This article focuses on options toouse HPC Pack toorun Linux workloads.</span></span> <span data-ttu-id="608fc-105">Существуют также возможности запуска [рабочих нагрузок HPC Windows с помощью пакета HPC](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="608fc-105">There are also options for running [Windows HPC workloads with HPC Pack](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a><span data-ttu-id="608fc-106">Запуск кластера пакета HPC на виртуальных машинах Azure</span><span class="sxs-lookup"><span data-stu-id="608fc-106">Run an HPC Pack cluster in Azure VMs</span></span>
### <a name="azure-templates"></a><span data-ttu-id="608fc-107">Шаблоны Azure</span><span class="sxs-lookup"><span data-stu-id="608fc-107">Azure templates</span></span>
* <span data-ttu-id="608fc-108">(GitHub) [Шаблоны кластера пакета HPC 2016](https://github.com/MsHpcPack/HPCPack2016)</span><span class="sxs-lookup"><span data-stu-id="608fc-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span></span>
* <span data-ttu-id="608fc-109">(Marketplace) [Кластер пакета HPC для рабочих нагрузок Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)</span><span class="sxs-lookup"><span data-stu-id="608fc-109">(Marketplace) [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)</span></span>
* <span data-ttu-id="608fc-110">(Краткое руководство) [Создание кластера HPC с вычислительными узлами Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)</span><span class="sxs-lookup"><span data-stu-id="608fc-110">(Quickstart) [Create an HPC cluster with Linux compute nodes](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)</span></span>

### <a name="powershell-deployment-script"></a><span data-ttu-id="608fc-111">Сценарий развертывания PowerShell</span><span class="sxs-lookup"><span data-stu-id="608fc-111">PowerShell deployment script</span></span>
* [<span data-ttu-id="608fc-112">Создание кластера Linux HPC с hello скрипт развертывания IaaS пакета HPC</span><span class="sxs-lookup"><span data-stu-id="608fc-112">Create a Linux HPC cluster with hello HPC Pack IaaS deployment script</span></span>](../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="tutorials"></a><span data-ttu-id="608fc-113">Учебники</span><span class="sxs-lookup"><span data-stu-id="608fc-113">Tutorials</span></span>
* [<span data-ttu-id="608fc-114">Руководство. Начало работы с вычислительными узлами Linux в кластере пакета HPC в Azure</span><span class="sxs-lookup"><span data-stu-id="608fc-114">Tutorial: Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="608fc-115">Руководство. запуск NAMD с пакетом Microsoft HPC на вычислительных узлах Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="608fc-115">Tutorial: Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](classic/hpcpack-cluster-namd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="608fc-116">Руководство. выполнение заданий OpenFOAM с помощью пакета Microsoft HPC в кластере Linux RDMA в Azure</span><span class="sxs-lookup"><span data-stu-id="608fc-116">Tutorial: Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="608fc-117">Руководство. Выполнение заданий STAR-CCM+ в кластере Linux RDMA в Azure с помощью пакета Microsoft HPC</span><span class="sxs-lookup"><span data-stu-id="608fc-117">Tutorial: Run STAR-CCM+ with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-starccm.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="cluster-management"></a><span data-ttu-id="608fc-118">Управление кластерами</span><span class="sxs-lookup"><span data-stu-id="608fc-118">Cluster management</span></span>
* [<span data-ttu-id="608fc-119">Отправить кластера HPC Pack tooan заданий в Azure</span><span class="sxs-lookup"><span data-stu-id="608fc-119">Submit jobs tooan HPC Pack cluster in Azure</span></span>](../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="608fc-120">Управление заданиями в пакете HPC</span><span class="sxs-lookup"><span data-stu-id="608fc-120">Job management in HPC Pack</span></span>](https://technet.microsoft.com/library/jj899585.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a><span data-ttu-id="608fc-121">Создание кластеров RDMA для рабочих нагрузок MPI</span><span class="sxs-lookup"><span data-stu-id="608fc-121">Create RDMA clusters for MPI workloads</span></span>
* [<span data-ttu-id="608fc-122">Руководство. выполнение заданий OpenFOAM с помощью пакета Microsoft HPC в кластере Linux RDMA в Azure</span><span class="sxs-lookup"><span data-stu-id="608fc-122">Tutorial: Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="608fc-123">Настройка приложений MPI Linux RDMA toorun кластера</span><span class="sxs-lookup"><span data-stu-id="608fc-123">Set up a Linux RDMA cluster toorun MPI applications</span></span>](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

