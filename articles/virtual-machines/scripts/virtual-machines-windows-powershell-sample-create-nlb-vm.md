---
title: "Пример сценария Azure PowerShell. Создание виртуальной машины Windows с балансировкой нагрузки | Документация Майкрософт"
description: "Пример сценария Azure PowerShell для создания виртуальной машины Windows с балансировкой нагрузки."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/05/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 25bcbbcd1615e01a384825d7bd1582a528e91f71
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="load-balance-traffic-between-highly-available-virtual-machines"></a><span data-ttu-id="d6678-103">Балансировка нагрузки для трафика между высокодоступными виртуальными машинами</span><span class="sxs-lookup"><span data-stu-id="d6678-103">Load balance traffic between highly available virtual machines</span></span>

<span data-ttu-id="d6678-104">Этот пример скрипта позволяет создать все необходимые компоненты для запуска нескольких виртуальных машин Windows Server 2016, настроенных в высокодоступной конфигурации с балансировкой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="d6678-104">This script sample creates everything needed to run several Windows Server 2016 virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="d6678-105">После выполнения этого сценария будут созданы три виртуальные машины, которые будут добавлены в группу доступности Azure. Доступ к ним можно будет получить через Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="d6678-105">After running the script, you will have three virtual machines, joined to an Azure Availability Set, and accessible through an Azure Load Balancer.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d6678-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="d6678-106">Sample script</span></span>

<span data-ttu-id="d6678-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.ps1 "Создание виртуальной машины с балансировкой нагрузки")]</span><span class="sxs-lookup"><span data-stu-id="d6678-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.ps1 "Create VM NLB")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="d6678-108">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="d6678-108">Clean up deployment</span></span> 

<span data-ttu-id="d6678-109">Выполните следующую команду, чтобы удалить группу ресурсов, виртуальную машину и все связанные с ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d6678-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="d6678-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="d6678-110">Script explanation</span></span>

<span data-ttu-id="d6678-111">Чтобы создать развертывание, скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="d6678-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="d6678-112">Для каждого элемента в таблице приведены ссылки на документацию по команде.</span><span class="sxs-lookup"><span data-stu-id="d6678-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d6678-113">Команда</span><span class="sxs-lookup"><span data-stu-id="d6678-113">Command</span></span> | <span data-ttu-id="d6678-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="d6678-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d6678-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d6678-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="d6678-116">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d6678-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d6678-117">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="d6678-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="d6678-118">Создает конфигурацию подсети.</span><span class="sxs-lookup"><span data-stu-id="d6678-118">Creates a subnet configuration.</span></span> <span data-ttu-id="d6678-119">Эта конфигурация используется в процессе создания виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="d6678-119">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="d6678-120">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="d6678-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="d6678-121">Создает виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="d6678-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="d6678-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="d6678-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="d6678-123">Создает общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="d6678-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="d6678-124">New-AzureRmLoadBalancerFrontendIpConfig</span><span class="sxs-lookup"><span data-stu-id="d6678-124">New-AzureRmLoadBalancerFrontendIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) | <span data-ttu-id="d6678-125">Создает конфигурацию внешних IP-адресов для балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="d6678-125">Creates a front-end IP configuration for a load balancer.</span></span> |
| [<span data-ttu-id="d6678-126">New-AzureRmLoadBalancerBackendAddressPoolConfig</span><span class="sxs-lookup"><span data-stu-id="d6678-126">New-AzureRmLoadBalancerBackendAddressPoolConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) | <span data-ttu-id="d6678-127">Создает конфигурацию внутреннего пула адресов для подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="d6678-127">Creates a backend address pool configuration for a load balancer.</span></span> |
| [<span data-ttu-id="d6678-128">New-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="d6678-128">New-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | <span data-ttu-id="d6678-129">Создает конфигурацию пробы для балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="d6678-129">Creates a probe configuration for a load balancer.</span></span> |
| [<span data-ttu-id="d6678-130">New-AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="d6678-130">New-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | <span data-ttu-id="d6678-131">Создает конфигурацию правил для балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="d6678-131">Creates a rule configuration for a load balancer.</span></span> |
| [<span data-ttu-id="d6678-132">New-AzureRmLoadBalancerInboundNatRuleConfig</span><span class="sxs-lookup"><span data-stu-id="d6678-132">New-AzureRmLoadBalancerInboundNatRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) | <span data-ttu-id="d6678-133">Создает конфигурацию правил NAT для балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="d6678-133">Creates an inbound NAT rule configuration for a load balancer.</span></span> |
| [<span data-ttu-id="d6678-134">New-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="d6678-134">New-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancer) | <span data-ttu-id="d6678-135">Создает балансировщик нагрузки.</span><span class="sxs-lookup"><span data-stu-id="d6678-135">Creates a load balancer.</span></span> |
| [<span data-ttu-id="d6678-136">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="d6678-136">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="d6678-137">Создает конфигурацию правил группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="d6678-137">Creates a network security group rule configuration.</span></span> <span data-ttu-id="d6678-138">Эта конфигурация используется для создания правила NSG при создании этой NSG.</span><span class="sxs-lookup"><span data-stu-id="d6678-138">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="d6678-139">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="d6678-139">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="d6678-140">Создает группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="d6678-140">Creates a network security group.</span></span> |
| [<span data-ttu-id="d6678-141">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="d6678-141">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="d6678-142">Возвращает сведения о подсети.</span><span class="sxs-lookup"><span data-stu-id="d6678-142">Gets subnet information.</span></span> <span data-ttu-id="d6678-143">Эта информация используется при создании сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="d6678-143">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="d6678-144">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="d6678-144">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="d6678-145">Создает сетевой интерфейс.</span><span class="sxs-lookup"><span data-stu-id="d6678-145">Creates a network interface.</span></span> |
| [<span data-ttu-id="d6678-146">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="d6678-146">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="d6678-147">Создает конфигурацию виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d6678-147">Creates a VM configuration.</span></span> <span data-ttu-id="d6678-148">Эта конфигурация включает в себя такие сведения, как имя виртуальной машины, операционную систему и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="d6678-148">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="d6678-149">Данная конфигурации используется при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d6678-149">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="d6678-150">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="d6678-150">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="d6678-151">Создайте виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="d6678-151">Create a virtual machine.</span></span> |
|[<span data-ttu-id="d6678-152">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d6678-152">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="d6678-153">Удаляет группу ресурсов и все ресурсы, содержащиеся в ней.</span><span class="sxs-lookup"><span data-stu-id="d6678-153">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d6678-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d6678-154">Next steps</span></span>

<span data-ttu-id="d6678-155">Дополнительные сведения о модуле Azure PowerShell см. в [документации по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d6678-155">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="d6678-156">Дополнительные примеры сценариев PowerShell для виртуальных машин представлены в [документации по виртуальным машинам Azure под управлением Windows](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d6678-156">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
