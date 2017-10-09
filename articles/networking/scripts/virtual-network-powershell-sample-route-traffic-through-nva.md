---
title: "Пример сценария PowerShell aaaAzure - трафик через сеть виртуального устройства | Документы Microsoft"
description: "Пример скрипта Azure PowerShell для маршрутизации трафика через виртуальный сетевой модуль брандмауэра."
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
ms.openlocfilehash: 3b999f3289d654c00d5becb973e2883896457d52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="ae293-103">Маршрутизация трафика через виртуальный сетевой модуль</span><span class="sxs-lookup"><span data-stu-id="ae293-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="ae293-104">В этом примере скрипта создается виртуальная сеть с интерфейсной и внутренней подсетями.</span><span class="sxs-lookup"><span data-stu-id="ae293-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="ae293-105">Он также создает виртуальную Машину с IP-пересылка включена tooroute трафик между двумя подсетями hello.</span><span class="sxs-lookup"><span data-stu-id="ae293-105">It also creates a VM with IP forwarding enabled tooroute traffic between hello two subnets.</span></span> <span data-ttu-id="ae293-106">После выполнения сценария hello можно развернуть сетевое программное обеспечение, таких как брандмауэр toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="ae293-106">After running hello script you can deploy network software, such as a firewall application, toohello VM.</span></span>

<span data-ttu-id="ae293-107">При необходимости установите Azure PowerShell с помощью инструкции hello, найденные в hello hello [руководство по Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), а затем запустите `Login-AzureRmAccount` toocreate соединения с Azure.</span><span class="sxs-lookup"><span data-stu-id="ae293-107">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ae293-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="ae293-108">Sample script</span></span>


[!code-powershell[main](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "Route traffic through a network virtual appliance")]

## <a name="clean-up-deployment"></a><span data-ttu-id="ae293-109">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="ae293-109">Clean up deployment</span></span> 

<span data-ttu-id="ae293-110">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="ae293-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```
## <a name="script-explanation"></a><span data-ttu-id="ae293-111">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="ae293-111">Script explanation</span></span>

<span data-ttu-id="ae293-112">Этот скрипт использует следующие команды toocreate hello группы ресурсов, виртуальной сети и группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="ae293-112">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="ae293-113">Каждая команда в таблице hello связывает toocommand документации.</span><span class="sxs-lookup"><span data-stu-id="ae293-113">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="ae293-114">Команда</span><span class="sxs-lookup"><span data-stu-id="ae293-114">Command</span></span> | <span data-ttu-id="ae293-115">Примечания</span><span class="sxs-lookup"><span data-stu-id="ae293-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ae293-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ae293-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="ae293-117">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="ae293-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ae293-118">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="ae293-118">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="ae293-119">Создает виртуальную сеть Azure и интерфейсную подсеть.</span><span class="sxs-lookup"><span data-stu-id="ae293-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="ae293-120">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="ae293-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="ae293-121">Создает внутреннюю подсеть и подсеть DMZ.</span><span class="sxs-lookup"><span data-stu-id="ae293-121">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="ae293-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="ae293-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="ae293-123">Создает открытый tooaccess hello IP адрес виртуальной Машины из Интернета hello.</span><span class="sxs-lookup"><span data-stu-id="ae293-123">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="ae293-124">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="ae293-124">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="ae293-125">Создает виртуальный сетевой интерфейс и включает IP-пересылку для него.</span><span class="sxs-lookup"><span data-stu-id="ae293-125">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="ae293-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="ae293-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="ae293-127">Создает группу безопасности сети (NSG).</span><span class="sxs-lookup"><span data-stu-id="ae293-127">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="ae293-128">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="ae293-128">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="ae293-129">Создает правила NSG, позволяющими toohello ВМ входящие порты HTTP и HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ae293-129">Creates NSG rules that allow HTTP and HTTPS ports inbound toohello VM.</span></span> |
| [<span data-ttu-id="ae293-130">Set-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="ae293-130">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig)| <span data-ttu-id="ae293-131">Связывает hello Nsg и toosubnets таблицы маршрутов.</span><span class="sxs-lookup"><span data-stu-id="ae293-131">Associates hello NSGs and route tables toosubnets.</span></span> |
| [<span data-ttu-id="ae293-132">New-AzureRmRouteTable</span><span class="sxs-lookup"><span data-stu-id="ae293-132">New-AzureRmRouteTable</span></span>](/powershell/module/azurerm.network/new-azurermroutetable)| <span data-ttu-id="ae293-133">Создает таблицу маршрутов для всех маршрутов.</span><span class="sxs-lookup"><span data-stu-id="ae293-133">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="ae293-134">New-AzureRMRouteConfig</span><span class="sxs-lookup"><span data-stu-id="ae293-134">New-AzureRMRouteConfig</span></span>](/powershell/module/azurerm.network/new-azurermrouteconfig)| <span data-ttu-id="ae293-135">Создает маршруты tooroute трафика между подсетями и hello Интернета через hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="ae293-135">Creates routes tooroute traffic between subnets and hello Internet through hello VM.</span></span> |
| [<span data-ttu-id="ae293-136">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="ae293-136">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="ae293-137">Создает виртуальную машину и присоединяет hello tooit сетевого Адаптера.</span><span class="sxs-lookup"><span data-stu-id="ae293-137">Creates a virtual machine and attaches hello NIC tooit.</span></span> <span data-ttu-id="ae293-138">Эта команда также указывает toouse образ виртуальной машины hello и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="ae293-138">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="ae293-139">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ae293-139">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)  | <span data-ttu-id="ae293-140">Удаляет группу ресурсов и все содержащиеся в ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="ae293-140">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ae293-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ae293-141">Next steps</span></span>

<span data-ttu-id="ae293-142">Дополнительные сведения о hello Azure PowerShell см. в разделе [документация по Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ae293-142">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="ae293-143">Дополнительные сетевые образцы сценариев PowerShell можно найти в hello [документации Azure Общие сведения о сети](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ae293-143">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
