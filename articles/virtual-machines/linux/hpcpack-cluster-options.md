---
title: "Варианты кластеров пакета HPC на основе Linux в облаке | Документация Майкрософт"
description: "Узнайте о вариантах создания кластера высокопроизводительных вычислительных систем (HPC) на основе Linux и управления им в облаке Azure с помощью пакета Microsoft HPC."
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
ms.openlocfilehash: 616006d29149f7f47b03bd127cf3c83ad63a5c39
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="options-with-hpc-pack-to-create-and-manage-an-hpc-cluster-in-azure-for-linux-workloads"></a><span data-ttu-id="02974-103">Варианты создания кластера HPC в Azure для рабочих нагрузок Linux и управления им с помощью пакета HPC</span><span class="sxs-lookup"><span data-stu-id="02974-103">Options with HPC Pack to create and manage an HPC cluster in Azure for Linux workloads</span></span>
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

<span data-ttu-id="02974-104">Эта статья посвящена вариантам использования пакета HPC для запуска рабочих нагрузок Linux.</span><span class="sxs-lookup"><span data-stu-id="02974-104">This article focuses on options to use HPC Pack to run Linux workloads.</span></span> <span data-ttu-id="02974-105">Существуют также возможности запуска [рабочих нагрузок HPC Windows с помощью пакета HPC](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="02974-105">There are also options for running [Windows HPC workloads with HPC Pack](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a><span data-ttu-id="02974-106">Запуск кластера пакета HPC на виртуальных машинах Azure</span><span class="sxs-lookup"><span data-stu-id="02974-106">Run an HPC Pack cluster in Azure VMs</span></span>
### <a name="azure-templates"></a><span data-ttu-id="02974-107">Шаблоны Azure</span><span class="sxs-lookup"><span data-stu-id="02974-107">Azure templates</span></span>
* <span data-ttu-id="02974-108">(GitHub) [Шаблоны кластера пакета HPC 2016](https://github.com/MsHpcPack/HPCPack2016)</span><span class="sxs-lookup"><span data-stu-id="02974-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span></span>
* <span data-ttu-id="02974-109">(Marketplace) [Кластер пакета HPC для рабочих нагрузок Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)</span><span class="sxs-lookup"><span data-stu-id="02974-109">(Marketplace) [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)</span></span>
* <span data-ttu-id="02974-110">(Краткое руководство) [Создание кластера HPC с вычислительными узлами Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)</span><span class="sxs-lookup"><span data-stu-id="02974-110">(Quickstart) [Create an HPC cluster with Linux compute nodes](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)</span></span>

### <a name="powershell-deployment-script"></a><span data-ttu-id="02974-111">Сценарий развертывания PowerShell</span><span class="sxs-lookup"><span data-stu-id="02974-111">PowerShell deployment script</span></span>
* [<span data-ttu-id="02974-112">Создание кластера HPC Linux с помощью сценария развертывания IaaS пакета HPC</span><span class="sxs-lookup"><span data-stu-id="02974-112">Create a Linux HPC cluster with the HPC Pack IaaS deployment script</span></span>](../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="tutorials"></a><span data-ttu-id="02974-113">Учебники</span><span class="sxs-lookup"><span data-stu-id="02974-113">Tutorials</span></span>
* [<span data-ttu-id="02974-114">Руководство. Начало работы с вычислительными узлами Linux в кластере пакета HPC в Azure</span><span class="sxs-lookup"><span data-stu-id="02974-114">Tutorial: Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="02974-115">Руководство. запуск NAMD с пакетом Microsoft HPC на вычислительных узлах Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="02974-115">Tutorial: Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](classic/hpcpack-cluster-namd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="02974-116">Руководство. выполнение заданий OpenFOAM с помощью пакета Microsoft HPC в кластере Linux RDMA в Azure</span><span class="sxs-lookup"><span data-stu-id="02974-116">Tutorial: Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="02974-117">Руководство. Выполнение заданий STAR-CCM+ в кластере Linux RDMA в Azure с помощью пакета Microsoft HPC</span><span class="sxs-lookup"><span data-stu-id="02974-117">Tutorial: Run STAR-CCM+ with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-starccm.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="cluster-management"></a><span data-ttu-id="02974-118">Управление кластерами</span><span class="sxs-lookup"><span data-stu-id="02974-118">Cluster management</span></span>
* [<span data-ttu-id="02974-119">Отправка заданий в кластер пакета HPC в Azure</span><span class="sxs-lookup"><span data-stu-id="02974-119">Submit jobs to an HPC Pack cluster in Azure</span></span>](../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="02974-120">Управление заданиями в пакете HPC</span><span class="sxs-lookup"><span data-stu-id="02974-120">Job management in HPC Pack</span></span>](https://technet.microsoft.com/library/jj899585.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a><span data-ttu-id="02974-121">Создание кластеров RDMA для рабочих нагрузок MPI</span><span class="sxs-lookup"><span data-stu-id="02974-121">Create RDMA clusters for MPI workloads</span></span>
* [<span data-ttu-id="02974-122">Руководство. выполнение заданий OpenFOAM с помощью пакета Microsoft HPC в кластере Linux RDMA в Azure</span><span class="sxs-lookup"><span data-stu-id="02974-122">Tutorial: Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="02974-123">Настройка кластера Linux RDMA для выполнения приложений MPI</span><span class="sxs-lookup"><span data-stu-id="02974-123">Set up a Linux RDMA cluster to run MPI applications</span></span>](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

