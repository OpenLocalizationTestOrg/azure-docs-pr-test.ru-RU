---
title: "параметры в облаке hello кластера HPC Pack aaaWindows | Документы Microsoft"
description: "Дополнительные сведения о параметрах с помощью пакета Microsoft HPC toocreate и управление Windows представляющие высокопроизводительные вычислительные системы (HPC) кластера в облаке Azure hello"
services: virtual-machines-windows,cloud-services,batch
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 02c5566d-2129-483c-9ecf-0d61030442d7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/06/2017
ms.author: danlep
ms.openlocfilehash: 6158d9dd0cecda38b14f85a2b2080163f18e8cf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="options-with-hpc-pack-toocreate-and-manage-a-windows-hpc-cluster-in-azure"></a><span data-ttu-id="324d2-103">Параметры с пакетом HPC toocreate и управлять кластером Windows HPC в Azure</span><span class="sxs-lookup"><span data-stu-id="324d2-103">Options with HPC Pack toocreate and manage a Windows HPC cluster in Azure</span></span>
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

<span data-ttu-id="324d2-104">Эта статья посвящена toocreate параметры пакета HPC рабочих нагрузок Windows toorun кластеров.</span><span class="sxs-lookup"><span data-stu-id="324d2-104">This article focuses on options toocreate HPC Pack clusters toorun Windows workloads.</span></span> <span data-ttu-id="324d2-105">Существуют также варианты для создания пакета HPC кластеры toorun [рабочих нагрузок Linux HPC](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="324d2-105">There are also options for creating HPC Pack clusters toorun [Linux HPC workloads](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a><span data-ttu-id="324d2-106">Запуск кластера пакета HPC на виртуальных машинах Azure</span><span class="sxs-lookup"><span data-stu-id="324d2-106">Run an HPC Pack cluster in Azure VMs</span></span>
### <a name="azure-templates"></a><span data-ttu-id="324d2-107">Шаблоны Azure</span><span class="sxs-lookup"><span data-stu-id="324d2-107">Azure templates</span></span>
* <span data-ttu-id="324d2-108">(GitHub) [Шаблоны кластера пакета HPC 2016](https://github.com/MsHpcPack/HPCPack2016)</span><span class="sxs-lookup"><span data-stu-id="324d2-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span></span>
* <span data-ttu-id="324d2-109">(Marketplace) [Кластер пакета HPC для рабочих нагрузок Windows](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)</span><span class="sxs-lookup"><span data-stu-id="324d2-109">(Marketplace) [HPC Pack cluster for Windows workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)</span></span>
* <span data-ttu-id="324d2-110">(Marketplace) [Кластер пакета HPC для рабочих нагрузок Excel](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)</span><span class="sxs-lookup"><span data-stu-id="324d2-110">(Marketplace) [HPC Pack cluster for Excel workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)</span></span>
* <span data-ttu-id="324d2-111">(Краткое руководство) [Создание кластера HPC](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)</span><span class="sxs-lookup"><span data-stu-id="324d2-111">(Quickstart) [Create an HPC cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)</span></span>
* <span data-ttu-id="324d2-112">(Краткое руководство) [Создание кластера HPC с помощью пользовательского образа вычислительного узла](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)</span><span class="sxs-lookup"><span data-stu-id="324d2-112">(Quickstart) [Create an HPC cluster with custom compute node image](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)</span></span>

### <a name="azure-vm-images"></a><span data-ttu-id="324d2-113">Образы виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="324d2-113">Azure VM images</span></span>
* [<span data-ttu-id="324d2-114">Головной узел пакета HPC 2016 на Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="324d2-114">HPC Pack 2016 head node on Windows Server 2016</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2016?tab=Overview)
* [<span data-ttu-id="324d2-115">Вычислительный узел пакета HPC 2016 на Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="324d2-115">HPC Pack 2016 compute node on Windows Server 2016</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2016?tab=Overview)
* [<span data-ttu-id="324d2-116">Головной узел пакета HPC 2016 на Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="324d2-116">HPC Pack 2016 head node on Windows Server 2012 R2</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2012R2?tab=Overview)
* [<span data-ttu-id="324d2-117">Вычислительный узел пакета HPC 2016 на Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="324d2-117">HPC Pack 2016 compute node on Windows Server 2012 R2</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2012R2?tab=Overview)
* [<span data-ttu-id="324d2-118">Головной узел пакета HPC 2012 R2 на Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="324d2-118">HPC Pack 2012 R2 head node on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)
* [<span data-ttu-id="324d2-119">Вычислительный узел пакета HPC 2012 R2 на Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="324d2-119">HPC Pack 2012 R2 compute node on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodeonwindowsserver2012r2/)
* [<span data-ttu-id="324d2-120">Вычислительный узел пакета HPC с Excel на Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="324d2-120">HPC Pack compute node with Excel on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodewithexcelonwindowsserver2012r2/)

### <a name="powershell-deployment-script"></a><span data-ttu-id="324d2-121">Сценарий развертывания PowerShell</span><span class="sxs-lookup"><span data-stu-id="324d2-121">PowerShell deployment script</span></span>
* [<span data-ttu-id="324d2-122">Создание кластера HPC с hello скрипт развертывания IaaS пакета HPC</span><span class="sxs-lookup"><span data-stu-id="324d2-122">Create an HPC cluster with hello HPC Pack IaaS deployment script</span></span>](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="tutorials"></a><span data-ttu-id="324d2-123">Учебники</span><span class="sxs-lookup"><span data-stu-id="324d2-123">Tutorials</span></span>
* [<span data-ttu-id="324d2-124">Руководство: Развертывание кластера пакета HPC 2016 в Azure</span><span class="sxs-lookup"><span data-stu-id="324d2-124">Tutorial: Deploy an HPC Pack 2016 cluster in Azure</span></span>](hpcpack-2016-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="324d2-125">Учебник: Приступая к работе с кластере HPC Pack в Azure toorun Excel и рабочими нагрузками SOA</span><span class="sxs-lookup"><span data-stu-id="324d2-125">Tutorial: Get started with an HPC Pack cluster in Azure toorun Excel and SOA workloads</span></span>](excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="manual-deployment-with-hello-azure-portal"></a><span data-ttu-id="324d2-126">Развертывание вручную с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="324d2-126">Manual deployment with hello Azure portal</span></span>
* [<span data-ttu-id="324d2-127">Настройка hello головного узла кластера HPC Pack на ВМ Azure</span><span class="sxs-lookup"><span data-stu-id="324d2-127">Set up hello head node of an HPC Pack cluster in an Azure VM</span></span>](hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="cluster-management"></a><span data-ttu-id="324d2-128">Управление кластерами</span><span class="sxs-lookup"><span data-stu-id="324d2-128">Cluster management</span></span>
* [<span data-ttu-id="324d2-129">Управление вычислительными кластерами пакета HPC в Azure</span><span class="sxs-lookup"><span data-stu-id="324d2-129">Manage compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster-node-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="324d2-130">Автоматическое изменение размера ресурсов кластера пакета HPC в Azure в соответствии с рабочей нагрузкой кластера</span><span class="sxs-lookup"><span data-stu-id="324d2-130">Grow and shrink Azure compute resources in an HPC Pack cluster</span></span>](classic/hpcpack-cluster-node-autogrowshrink.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="324d2-131">Отправить кластера HPC Pack tooan заданий в Azure</span><span class="sxs-lookup"><span data-stu-id="324d2-131">Submit jobs tooan HPC Pack cluster in Azure</span></span>](hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="324d2-132">Управление заданиями в пакете HPC</span><span class="sxs-lookup"><span data-stu-id="324d2-132">Job management in HPC Pack</span></span>](https://technet.microsoft.com/library/jj899585.aspx)
* [<span data-ttu-id="324d2-133">Управление кластером пакета HPC в Azure с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="324d2-133">Manage an HPC Pack cluster in Azure with Azure Active Directory</span></span>](hpcpack-cluster-active-directory.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="add-worker-role-nodes-tooan-hpc-pack-cluster"></a><span data-ttu-id="324d2-134">Добавление рабочей роли узлы tooan HPC Pack кластера</span><span class="sxs-lookup"><span data-stu-id="324d2-134">Add worker role nodes tooan HPC Pack cluster</span></span>
* [<span data-ttu-id="324d2-135">Повышение tooAzure рабочих экземпляров с помощью пакета HPC</span><span class="sxs-lookup"><span data-stu-id="324d2-135">Burst tooAzure worker instances with HPC Pack</span></span>](https://technet.microsoft.com/library/gg481749.aspx)
* [<span data-ttu-id="324d2-136">Учебник: настройка гибридного кластера с пакетом HPC в Azure</span><span class="sxs-lookup"><span data-stu-id="324d2-136">Tutorial: Set up a hybrid cluster with HPC Pack in Azure</span></span>](../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)
* [<span data-ttu-id="324d2-137">Добавление Azure «повышение» узлы tooan головной узел пакета HPC в Azure</span><span class="sxs-lookup"><span data-stu-id="324d2-137">Add Azure "burst" nodes tooan HPC Pack head node in Azure</span></span>](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="integrate-with-azure-batch"></a><span data-ttu-id="324d2-138">Интеграция с пакетной службой Azure</span><span class="sxs-lookup"><span data-stu-id="324d2-138">Integrate with Azure Batch</span></span>
* [<span data-ttu-id="324d2-139">Повышение tooAzure пакета с помощью пакета HPC</span><span class="sxs-lookup"><span data-stu-id="324d2-139">Burst tooAzure Batch with HPC Pack</span></span>](https://technet.microsoft.com/library/mt612877.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a><span data-ttu-id="324d2-140">Создание кластеров RDMA для рабочих нагрузок MPI</span><span class="sxs-lookup"><span data-stu-id="324d2-140">Create RDMA clusters for MPI workloads</span></span>
* [<span data-ttu-id="324d2-141">Настройка кластера Windows RDMA с помощью приложений MPI toorun пакета HPC</span><span class="sxs-lookup"><span data-stu-id="324d2-141">Set up a Windows RDMA cluster with HPC Pack toorun MPI applications</span></span>](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

