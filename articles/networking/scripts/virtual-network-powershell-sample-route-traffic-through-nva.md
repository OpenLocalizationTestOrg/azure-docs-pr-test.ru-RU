---
title: "Пример скрипта Azure PowerShell. Маршрутизация трафика через виртуальный сетевой модуль | Документация Майкрософт"
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
ms.openlocfilehash: 883d28dac72a66c2186d222f72b04d68e532cead
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="d43ff-103">Маршрутизация трафика через виртуальный сетевой модуль</span><span class="sxs-lookup"><span data-stu-id="d43ff-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="d43ff-104">В этом примере скрипта создается виртуальная сеть с интерфейсной и внутренней подсетями.</span><span class="sxs-lookup"><span data-stu-id="d43ff-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="d43ff-105">Скрипт также создает виртуальную машину с IP-пересылкой, которая позволяет маршрутизировать трафик между двумя подсетями.</span><span class="sxs-lookup"><span data-stu-id="d43ff-105">It also creates a VM with IP forwarding enabled to route traffic between the two subnets.</span></span> <span data-ttu-id="d43ff-106">После выполнения скрипта вы можете развернуть на виртуальной машине программное обеспечение сети, например брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="d43ff-106">After running the script you can deploy network software, such as a firewall application, to the VM.</span></span>

<span data-ttu-id="d43ff-107">При необходимости установите Azure PowerShell с помощью инструкции, приведенной в [руководстве Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), а затем выполните команду `Login-AzureRmAccount`, чтобы создать подключение к Azure.</span><span class="sxs-lookup"><span data-stu-id="d43ff-107">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d43ff-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="d43ff-108">Sample script</span></span>


<span data-ttu-id="d43ff-109">[!code-powershell[main](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "Маршрутизация трафика через виртуальный сетевой модуль")]</span><span class="sxs-lookup"><span data-stu-id="d43ff-109">[!code-powershell[main](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "Route traffic through a network virtual appliance")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="d43ff-110">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="d43ff-110">Clean up deployment</span></span> 

<span data-ttu-id="d43ff-111">Выполните следующую команду, чтобы удалить группу ресурсов, виртуальную машину и все связанные с ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d43ff-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```
## <a name="script-explanation"></a><span data-ttu-id="d43ff-112">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="d43ff-112">Script explanation</span></span>

<span data-ttu-id="d43ff-113">Для создания группы ресурсов, виртуальной сети и групп безопасности сети этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="d43ff-113">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="d43ff-114">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="d43ff-114">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="d43ff-115">Команда</span><span class="sxs-lookup"><span data-stu-id="d43ff-115">Command</span></span> | <span data-ttu-id="d43ff-116">Примечания</span><span class="sxs-lookup"><span data-stu-id="d43ff-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d43ff-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d43ff-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="d43ff-118">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d43ff-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d43ff-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="d43ff-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="d43ff-120">Создает виртуальную сеть Azure и интерфейсную подсеть.</span><span class="sxs-lookup"><span data-stu-id="d43ff-120">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="d43ff-121">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="d43ff-121">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="d43ff-122">Создает внутреннюю подсеть и подсеть DMZ.</span><span class="sxs-lookup"><span data-stu-id="d43ff-122">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="d43ff-123">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="d43ff-123">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="d43ff-124">Создает общедоступный IP-адрес для доступа к виртуальной машине из Интернета.</span><span class="sxs-lookup"><span data-stu-id="d43ff-124">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="d43ff-125">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="d43ff-125">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="d43ff-126">Создает виртуальный сетевой интерфейс и включает IP-пересылку для него.</span><span class="sxs-lookup"><span data-stu-id="d43ff-126">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="d43ff-127">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="d43ff-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="d43ff-128">Создает группу безопасности сети (NSG).</span><span class="sxs-lookup"><span data-stu-id="d43ff-128">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="d43ff-129">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="d43ff-129">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="d43ff-130">Создает правила группы безопасности сети, которые разрешают входящий трафик по портам HTTP и HTTPS к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="d43ff-130">Creates NSG rules that allow HTTP and HTTPS ports inbound to the VM.</span></span> |
| [<span data-ttu-id="d43ff-131">Set-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="d43ff-131">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig)| <span data-ttu-id="d43ff-132">Связывает группы безопасности сети и таблицы маршрутов с подсетями.</span><span class="sxs-lookup"><span data-stu-id="d43ff-132">Associates the NSGs and route tables to subnets.</span></span> |
| [<span data-ttu-id="d43ff-133">New-AzureRmRouteTable</span><span class="sxs-lookup"><span data-stu-id="d43ff-133">New-AzureRmRouteTable</span></span>](/powershell/module/azurerm.network/new-azurermroutetable)| <span data-ttu-id="d43ff-134">Создает таблицу маршрутов для всех маршрутов.</span><span class="sxs-lookup"><span data-stu-id="d43ff-134">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="d43ff-135">New-AzureRMRouteConfig</span><span class="sxs-lookup"><span data-stu-id="d43ff-135">New-AzureRMRouteConfig</span></span>](/powershell/module/azurerm.network/new-azurermrouteconfig)| <span data-ttu-id="d43ff-136">Создает маршруты для маршрутизации трафика между подсетями и Интернетом через виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="d43ff-136">Creates routes to route traffic between subnets and the Internet through the VM.</span></span> |
| [<span data-ttu-id="d43ff-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="d43ff-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="d43ff-138">Создает виртуальную машину и присоединяет к ней сетевой адаптер.</span><span class="sxs-lookup"><span data-stu-id="d43ff-138">Creates a virtual machine and attaches the NIC to it.</span></span> <span data-ttu-id="d43ff-139">Эта команда также указывает образ виртуальной машины и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="d43ff-139">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="d43ff-140">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d43ff-140">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)  | <span data-ttu-id="d43ff-141">Удаляет группу ресурсов и все содержащиеся в ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d43ff-141">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d43ff-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d43ff-142">Next steps</span></span>

<span data-ttu-id="d43ff-143">Дополнительные сведения о Azure PowerShell см. в [документации по Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d43ff-143">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="d43ff-144">Дополнительные примеры скриптов PowerShell для сетей см. в [обзорной документации по сетям Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d43ff-144">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>