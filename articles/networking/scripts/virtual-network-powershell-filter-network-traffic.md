---
title: "Пример сценария PowerShell aaaAzure - сетевого трафика виртуальных Машин фильтр | Документы Microsoft"
description: "Пример скрипта Azure PowerShell для фильтрации входящего и исходящего сетевого трафика виртуальной машины."
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
ms.openlocfilehash: 39eae6a43a8dc7f9fc616ef3ec50f95443fd3547
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="646b9-103">Фильтрация входящего и исходящего сетевого трафика виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="646b9-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="646b9-104">В этом примере скрипта создается виртуальная сеть с интерфейсной и внутренней подсетями.</span><span class="sxs-lookup"><span data-stu-id="646b9-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="646b9-105">Входящий сетевой трафик интерфейса подсеть toohello является ограниченной tooHTTP и HTTPS, а исходящий трафик toohello Интернет из внутренней подсети hello не допускается.</span><span class="sxs-lookup"><span data-stu-id="646b9-105">Inbound network traffic toohello front-end subnet is limited tooHTTP, and HTTPS, while outbound traffic toohello Internet from hello back-end subnet is not permitted.</span></span> <span data-ttu-id="646b9-106">После выполнения сценария hello, имеется одна виртуальная машина с двумя сетевыми адаптерами.</span><span class="sxs-lookup"><span data-stu-id="646b9-106">After running hello script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="646b9-107">Каждый сетевой Адаптер имеет подключенного tooa другой подсети.</span><span class="sxs-lookup"><span data-stu-id="646b9-107">Each NIC is connected tooa different subnet.</span></span>

<span data-ttu-id="646b9-108">При необходимости установите Azure PowerShell с помощью инструкции hello, найденные в hello hello [руководство по Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), а затем запустите `Login-AzureRmAccount` toocreate соединения с Azure.</span><span class="sxs-lookup"><span data-stu-id="646b9-108">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="646b9-109">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="646b9-109">Sample script</span></span>


[!code-powershell[main](../../../powershell_scripts/virtual-network/filter-network-traffic/filter-network-traffic.ps1  "Filter VM network traffic")]

## <a name="clean-up-deployment"></a><span data-ttu-id="646b9-110">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="646b9-110">Clean up deployment</span></span> 

<span data-ttu-id="646b9-111">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="646b9-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="646b9-112">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="646b9-112">Script explanation</span></span>

<span data-ttu-id="646b9-113">Этот скрипт использует следующие команды toocreate hello группы ресурсов, виртуальной сети и группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="646b9-113">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="646b9-114">Каждая команда в таблице hello связывает toocommand документации.</span><span class="sxs-lookup"><span data-stu-id="646b9-114">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="646b9-115">Команда</span><span class="sxs-lookup"><span data-stu-id="646b9-115">Command</span></span> | <span data-ttu-id="646b9-116">Примечания</span><span class="sxs-lookup"><span data-stu-id="646b9-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="646b9-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="646b9-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="646b9-118">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="646b9-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="646b9-119">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="646b9-119">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="646b9-120">Создает объект конфигурации подсети.</span><span class="sxs-lookup"><span data-stu-id="646b9-120">Creates a subnet configuration object</span></span> |
| [<span data-ttu-id="646b9-121">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="646b9-121">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="646b9-122">Создает виртуальную сеть Azure и интерфейсную подсеть.</span><span class="sxs-lookup"><span data-stu-id="646b9-122">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="646b9-123">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="646b9-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="646b9-124">Создает группу безопасности сети tooa toobe правила безопасности.</span><span class="sxs-lookup"><span data-stu-id="646b9-124">Creates security rules toobe assigned tooa network security group.</span></span> |
| [<span data-ttu-id="646b9-125">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="646b9-125">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) |<span data-ttu-id="646b9-126">Создаются правила NSG, разрешать или запрещать определенные порты toospecific подсетей.</span><span class="sxs-lookup"><span data-stu-id="646b9-126">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="646b9-127">Set-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="646b9-127">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="646b9-128">Связывает toosubnets Nsg.</span><span class="sxs-lookup"><span data-stu-id="646b9-128">Associates NSGs toosubnets.</span></span> |
| [<span data-ttu-id="646b9-129">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="646b9-129">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="646b9-130">Создает открытый tooaccess hello IP адрес виртуальной Машины из Интернета hello.</span><span class="sxs-lookup"><span data-stu-id="646b9-130">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="646b9-131">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="646b9-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="646b9-132">Создает виртуальными сетевыми интерфейсами и вкладывает их подсети виртуальной сети toohello внешнего и внутреннего интерфейса.</span><span class="sxs-lookup"><span data-stu-id="646b9-132">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="646b9-133">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="646b9-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="646b9-134">Создает конфигурацию виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="646b9-134">Creates a VM configuration.</span></span> <span data-ttu-id="646b9-135">Эта конфигурация включает в себя такие сведения, как имя виртуальной машины, операционную систему и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="646b9-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="646b9-136">Конфигурация Hello используется во время создания виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="646b9-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="646b9-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="646b9-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="646b9-138">Создайте виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="646b9-138">Create a virtual machine.</span></span> |
|[<span data-ttu-id="646b9-139">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="646b9-139">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="646b9-140">Удаляет группу ресурсов и все ресурсы, содержащиеся в ней.</span><span class="sxs-lookup"><span data-stu-id="646b9-140">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="646b9-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="646b9-141">Next steps</span></span>

<span data-ttu-id="646b9-142">Дополнительные сведения о hello Azure PowerShell см. в разделе [документация по Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="646b9-142">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="646b9-143">Дополнительные сетевые образцы сценариев PowerShell можно найти в hello [документации Azure Общие сведения о сети](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="646b9-143">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
