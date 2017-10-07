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
# <a name="options-with-hpc-pack-toocreate-and-manage-a-windows-hpc-cluster-in-azure"></a>Параметры с пакетом HPC toocreate и управлять кластером Windows HPC в Azure
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

Эта статья посвящена toocreate параметры пакета HPC рабочих нагрузок Windows toorun кластеров. Существуют также варианты для создания пакета HPC кластеры toorun [рабочих нагрузок Linux HPC](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a>Запуск кластера пакета HPC на виртуальных машинах Azure
### <a name="azure-templates"></a>Шаблоны Azure
* (GitHub) [Шаблоны кластера пакета HPC 2016](https://github.com/MsHpcPack/HPCPack2016)
* (Marketplace) [Кластер пакета HPC для рабочих нагрузок Windows](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)
* (Marketplace) [Кластер пакета HPC для рабочих нагрузок Excel](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)
* (Краткое руководство) [Создание кластера HPC](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)
* (Краткое руководство) [Создание кластера HPC с помощью пользовательского образа вычислительного узла](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)

### <a name="azure-vm-images"></a>Образы виртуальных машин Azure
* [Головной узел пакета HPC 2016 на Windows Server 2016](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2016?tab=Overview)
* [Вычислительный узел пакета HPC 2016 на Windows Server 2016](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2016?tab=Overview)
* [Головной узел пакета HPC 2016 на Windows Server 2012 R2](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2012R2?tab=Overview)
* [Вычислительный узел пакета HPC 2016 на Windows Server 2012 R2](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2012R2?tab=Overview)
* [Головной узел пакета HPC 2012 R2 на Windows Server 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)
* [Вычислительный узел пакета HPC 2012 R2 на Windows Server 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodeonwindowsserver2012r2/)
* [Вычислительный узел пакета HPC с Excel на Windows Server 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodewithexcelonwindowsserver2012r2/)

### <a name="powershell-deployment-script"></a>Сценарий развертывания PowerShell
* [Создание кластера HPC с hello скрипт развертывания IaaS пакета HPC](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="tutorials"></a>Учебники
* [Руководство: Развертывание кластера пакета HPC 2016 в Azure](hpcpack-2016-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Учебник: Приступая к работе с кластере HPC Pack в Azure toorun Excel и рабочими нагрузками SOA](excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="manual-deployment-with-hello-azure-portal"></a>Развертывание вручную с помощью портала Azure hello
* [Настройка hello головного узла кластера HPC Pack на ВМ Azure](hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="cluster-management"></a>Управление кластерами
* [Управление вычислительными кластерами пакета HPC в Azure](classic/hpcpack-cluster-node-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Автоматическое изменение размера ресурсов кластера пакета HPC в Azure в соответствии с рабочей нагрузкой кластера](classic/hpcpack-cluster-node-autogrowshrink.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Отправить кластера HPC Pack tooan заданий в Azure](hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Управление заданиями в пакете HPC](https://technet.microsoft.com/library/jj899585.aspx)
* [Управление кластером пакета HPC в Azure с помощью Azure Active Directory](hpcpack-cluster-active-directory.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="add-worker-role-nodes-tooan-hpc-pack-cluster"></a>Добавление рабочей роли узлы tooan HPC Pack кластера
* [Повышение tooAzure рабочих экземпляров с помощью пакета HPC](https://technet.microsoft.com/library/gg481749.aspx)
* [Учебник: настройка гибридного кластера с пакетом HPC в Azure](../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)
* [Добавление Azure «повышение» узлы tooan головной узел пакета HPC в Azure](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="integrate-with-azure-batch"></a>Интеграция с пакетной службой Azure
* [Повышение tooAzure пакета с помощью пакета HPC](https://technet.microsoft.com/library/mt612877.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a>Создание кластеров RDMA для рабочих нагрузок MPI
* [Настройка кластера Windows RDMA с помощью приложений MPI toorun пакета HPC](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

