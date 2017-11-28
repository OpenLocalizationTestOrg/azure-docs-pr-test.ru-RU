---
title: "Образец скрипта PowerShell - aaaAzure создать балансировки сетевой Нагрузки Windows VM | Документы Microsoft"
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
ms.openlocfilehash: 60a48c5f243c8ff3ab886437ae45b21ce069ea4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-traffic-between-highly-available-virtual-machines"></a><span data-ttu-id="ce388-103">Балансировка нагрузки для трафика между высокодоступными виртуальными машинами</span><span class="sxs-lookup"><span data-stu-id="ce388-103">Load balance traffic between highly available virtual machines</span></span>

<span data-ttu-id="ce388-104">В этом примере сценария создается все необходимое toorun несколько виртуальных машин Windows Server 2016, настроенных в высокой доступности и загрузить сбалансированной конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ce388-104">This script sample creates everything needed toorun several Windows Server 2016 virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="ce388-105">После выполнения скрипта hello, будет иметь три виртуальные машины присоединены к домену tooan группе доступности Azure и доступный с помощью подсистемы балансировки нагрузки Azure.</span><span class="sxs-lookup"><span data-stu-id="ce388-105">After running hello script, you will have three virtual machines, joined tooan Azure Availability Set, and accessible through an Azure Load Balancer.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ce388-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="ce388-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.ps1 "Create VM NLB")]

## <a name="clean-up-deployment"></a><span data-ttu-id="ce388-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="ce388-107">Clean up deployment</span></span> 

<span data-ttu-id="ce388-108">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="ce388-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ce388-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="ce388-109">Script explanation</span></span>

<span data-ttu-id="ce388-110">Этот скрипт использует следующие команды toocreate hello развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="ce388-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="ce388-111">Каждый элемент в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="ce388-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ce388-112">Команда</span><span class="sxs-lookup"><span data-stu-id="ce388-112">Command</span></span> | <span data-ttu-id="ce388-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="ce388-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ce388-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ce388-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="ce388-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="ce388-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ce388-116">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="ce388-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="ce388-117">Создает конфигурацию подсети.</span><span class="sxs-lookup"><span data-stu-id="ce388-117">Creates a subnet configuration.</span></span> <span data-ttu-id="ce388-118">Эта конфигурация используется с hello процесс создания виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="ce388-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="ce388-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="ce388-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="ce388-120">Создает виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="ce388-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="ce388-121">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="ce388-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="ce388-122">Создает общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="ce388-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="ce388-123">New-AzureRmLoadBalancerFrontendIpConfig</span><span class="sxs-lookup"><span data-stu-id="ce388-123">New-AzureRmLoadBalancerFrontendIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) | <span data-ttu-id="ce388-124">Создает конфигурацию внешних IP-адресов для балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="ce388-124">Creates a front-end IP configuration for a load balancer.</span></span> |
| [<span data-ttu-id="ce388-125">New-AzureRmLoadBalancerBackendAddressPoolConfig</span><span class="sxs-lookup"><span data-stu-id="ce388-125">New-AzureRmLoadBalancerBackendAddressPoolConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) | <span data-ttu-id="ce388-126">Создает конфигурацию внутреннего пула адресов для подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="ce388-126">Creates a backend address pool configuration for a load balancer.</span></span> |
| [<span data-ttu-id="ce388-127">New-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="ce388-127">New-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | <span data-ttu-id="ce388-128">Создает конфигурацию пробы для балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="ce388-128">Creates a probe configuration for a load balancer.</span></span> |
| [<span data-ttu-id="ce388-129">New-AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="ce388-129">New-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | <span data-ttu-id="ce388-130">Создает конфигурацию правил для балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="ce388-130">Creates a rule configuration for a load balancer.</span></span> |
| [<span data-ttu-id="ce388-131">New-AzureRmLoadBalancerInboundNatRuleConfig</span><span class="sxs-lookup"><span data-stu-id="ce388-131">New-AzureRmLoadBalancerInboundNatRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) | <span data-ttu-id="ce388-132">Создает конфигурацию правил NAT для балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="ce388-132">Creates an inbound NAT rule configuration for a load balancer.</span></span> |
| [<span data-ttu-id="ce388-133">New-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="ce388-133">New-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancer) | <span data-ttu-id="ce388-134">Создает балансировщик нагрузки.</span><span class="sxs-lookup"><span data-stu-id="ce388-134">Creates a load balancer.</span></span> |
| [<span data-ttu-id="ce388-135">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="ce388-135">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="ce388-136">Создает конфигурацию правил группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="ce388-136">Creates a network security group rule configuration.</span></span> <span data-ttu-id="ce388-137">Такая настройка является toocreate используется правило NSG при создании hello NSG.</span><span class="sxs-lookup"><span data-stu-id="ce388-137">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="ce388-138">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="ce388-138">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="ce388-139">Создает группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="ce388-139">Creates a network security group.</span></span> |
| [<span data-ttu-id="ce388-140">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="ce388-140">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="ce388-141">Возвращает сведения о подсети.</span><span class="sxs-lookup"><span data-stu-id="ce388-141">Gets subnet information.</span></span> <span data-ttu-id="ce388-142">Эта информация используется при создании сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="ce388-142">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="ce388-143">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="ce388-143">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="ce388-144">Создает сетевой интерфейс.</span><span class="sxs-lookup"><span data-stu-id="ce388-144">Creates a network interface.</span></span> |
| [<span data-ttu-id="ce388-145">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="ce388-145">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="ce388-146">Создает конфигурацию виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ce388-146">Creates a VM configuration.</span></span> <span data-ttu-id="ce388-147">Эта конфигурация включает в себя такие сведения, как имя виртуальной машины, операционную систему и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="ce388-147">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="ce388-148">Конфигурация Hello используется во время создания виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="ce388-148">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="ce388-149">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="ce388-149">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="ce388-150">Создайте виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="ce388-150">Create a virtual machine.</span></span> |
|[<span data-ttu-id="ce388-151">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ce388-151">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="ce388-152">Удаляет группу ресурсов и все ресурсы, содержащиеся в ней.</span><span class="sxs-lookup"><span data-stu-id="ce388-152">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ce388-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ce388-153">Next steps</span></span>

<span data-ttu-id="ce388-154">Дополнительные сведения о hello модуля Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ce388-154">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="ce388-155">Примеры сценариев PowerShell дополнительную виртуальную машину можно найти в hello [документации виртуальной Машины Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ce388-155">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
