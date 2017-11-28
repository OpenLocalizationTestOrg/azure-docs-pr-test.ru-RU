---
title: "Пример сценария PowerShell - aaaAzure создания сетей многоуровневые приложения | Документы Microsoft"
description: "Пример скрипта Azure PowerShell для создания сети для многоуровневых приложений."
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 46d6d16dc5dbc8be467359f31346f017727b1abe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="c47a2-103">Создание сети для многоуровневых приложений</span><span class="sxs-lookup"><span data-stu-id="c47a2-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="c47a2-104">В этом примере скрипта создается виртуальная сеть с интерфейсной и внутренней подсетями.</span><span class="sxs-lookup"><span data-stu-id="c47a2-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="c47a2-105">Подсети интерфейса toohello трафика является ограниченной tooHTTP и SSH, при toohello трафика конечной подсети ограниченный tooMySQL, порт 3306.</span><span class="sxs-lookup"><span data-stu-id="c47a2-105">Traffic toohello front-end subnet is limited tooHTTP and SSH, while traffic toohello back-end subnet is limited tooMySQL, port 3306.</span></span> <span data-ttu-id="c47a2-106">После выполнения скрипта hello имеется две виртуальные машины, по одному в каждой подсети, можно развернуть веб-сервера и программное обеспечение MySQL.</span><span class="sxs-lookup"><span data-stu-id="c47a2-106">After running hello script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

<span data-ttu-id="c47a2-107">При необходимости установите Azure PowerShell с помощью инструкции hello, найденные в hello hello [руководство по Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), а затем запустите `Login-AzureRmAccount` toocreate соединения с Azure.</span><span class="sxs-lookup"><span data-stu-id="c47a2-107">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c47a2-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="c47a2-108">Sample script</span></span>


[!code-powershell[main](../../../powershell_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.ps1  "Virtual network for multi-tier application")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c47a2-109">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="c47a2-109">Clean up deployment</span></span> 

<span data-ttu-id="c47a2-110">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="c47a2-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="c47a2-111">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="c47a2-111">Script explanation</span></span>

<span data-ttu-id="c47a2-112">Этот скрипт использует следующие команды toocreate hello группы ресурсов, виртуальной сети и группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="c47a2-112">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="c47a2-113">Каждая команда в таблице hello связывает toocommand документации.</span><span class="sxs-lookup"><span data-stu-id="c47a2-113">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="c47a2-114">Команда</span><span class="sxs-lookup"><span data-stu-id="c47a2-114">Command</span></span> | <span data-ttu-id="c47a2-115">Примечания</span><span class="sxs-lookup"><span data-stu-id="c47a2-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c47a2-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c47a2-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="c47a2-117">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="c47a2-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c47a2-118">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="c47a2-118">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="c47a2-119">Создает виртуальную сеть Azure и интерфейсную подсеть.</span><span class="sxs-lookup"><span data-stu-id="c47a2-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="c47a2-120">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="c47a2-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="c47a2-121">Создает внутреннюю подсеть.</span><span class="sxs-lookup"><span data-stu-id="c47a2-121">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="c47a2-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="c47a2-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="c47a2-123">Создает открытый tooaccess hello IP адрес виртуальной Машины из Интернета hello.</span><span class="sxs-lookup"><span data-stu-id="c47a2-123">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="c47a2-124">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="c47a2-124">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="c47a2-125">Создает виртуальными сетевыми интерфейсами и вкладывает их подсети виртуальной сети toohello внешнего и внутреннего интерфейса.</span><span class="sxs-lookup"><span data-stu-id="c47a2-125">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="c47a2-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="c47a2-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="c47a2-127">Создание группы безопасности сети (NSG), которые будут связанного toohello внешнего и внутреннего интерфейса подсети.</span><span class="sxs-lookup"><span data-stu-id="c47a2-127">Creates network security groups (NSG) that are associated toohello front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="c47a2-128">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="c47a2-128">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) |<span data-ttu-id="c47a2-129">Создаются правила NSG, разрешать или запрещать определенные порты toospecific подсетей.</span><span class="sxs-lookup"><span data-stu-id="c47a2-129">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="c47a2-130">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="c47a2-130">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="c47a2-131">Создает виртуальные машины и присоединяет tooeach сетевого Адаптера виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="c47a2-131">Creates virtual machines and attaches a NIC tooeach VM.</span></span> <span data-ttu-id="c47a2-132">Эта команда также указывает toouse образ виртуальной машины hello и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="c47a2-132">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="c47a2-133">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c47a2-133">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="c47a2-134">Удаляет группу ресурсов и все содержащиеся в ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="c47a2-134">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c47a2-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c47a2-135">Next steps</span></span>

<span data-ttu-id="c47a2-136">Дополнительные сведения о hello Azure PowerShell см. в разделе [документация по Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c47a2-136">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="c47a2-137">Дополнительные сетевые образцы сценариев PowerShell можно найти в hello [документации Azure Общие сведения о сети](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c47a2-137">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
