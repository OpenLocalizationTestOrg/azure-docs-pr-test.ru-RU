---
title: "Пример сценария PowerShell - aaaAzure создания виртуальной Машины Windows | Документы Microsoft"
description: "Пример сценария Azure PowerShell для создания виртуальной машины Windows."
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
ms.date: 03/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 81f04ed88a968cb7ac540b0b4b874dcf230a8e1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-configured-virtual-machine-with-powershell"></a><span data-ttu-id="f4c85-103">Создание полностью настроенной виртуальной машины с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4c85-103">Create a fully configured virtual machine with PowerShell</span></span>

<span data-ttu-id="f4c85-104">Этот сценарий создает виртуальную машину Azure под управлением Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="f4c85-104">This script creates an Azure Virtual Machine running Windows Server 2016.</span></span> <span data-ttu-id="f4c85-105">После выполнения сценария hello, для доступа к RDP hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="f4c85-105">After running hello script, you can access hello virtual machine over RDP.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="f4c85-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="f4c85-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-detailed/create-windows-vm-detailed.ps1 "Create VM detailed")]

## <a name="clean-up-deployment"></a><span data-ttu-id="f4c85-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="f4c85-107">Clean up deployment</span></span> 

<span data-ttu-id="f4c85-108">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="f4c85-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="f4c85-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="f4c85-109">Script explanation</span></span>

<span data-ttu-id="f4c85-110">Этот скрипт использует следующие команды toocreate hello развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="f4c85-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="f4c85-111">Каждый элемент в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="f4c85-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f4c85-112">Команда</span><span class="sxs-lookup"><span data-stu-id="f4c85-112">Command</span></span> | <span data-ttu-id="f4c85-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="f4c85-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f4c85-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f4c85-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="f4c85-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="f4c85-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f4c85-116">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="f4c85-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="f4c85-117">Создает конфигурацию подсети.</span><span class="sxs-lookup"><span data-stu-id="f4c85-117">Creates a subnet configuration.</span></span> <span data-ttu-id="f4c85-118">Эта конфигурация используется с hello процесс создания виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="f4c85-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="f4c85-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="f4c85-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="f4c85-120">Создает виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="f4c85-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="f4c85-121">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="f4c85-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="f4c85-122">Создает общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="f4c85-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="f4c85-123">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="f4c85-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="f4c85-124">Создает конфигурацию правил группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="f4c85-124">Creates a network security group rule configuration.</span></span> <span data-ttu-id="f4c85-125">Такая настройка является toocreate используется правило NSG при создании hello NSG.</span><span class="sxs-lookup"><span data-stu-id="f4c85-125">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="f4c85-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="f4c85-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="f4c85-127">Создает группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="f4c85-127">Creates a network security group.</span></span> |
| [<span data-ttu-id="f4c85-128">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="f4c85-128">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="f4c85-129">Возвращает сведения о подсети.</span><span class="sxs-lookup"><span data-stu-id="f4c85-129">Gets subnet information.</span></span> <span data-ttu-id="f4c85-130">Эта информация используется при создании сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="f4c85-130">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="f4c85-131">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="f4c85-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="f4c85-132">Создает сетевой интерфейс.</span><span class="sxs-lookup"><span data-stu-id="f4c85-132">Creates a network interface.</span></span> |
| [<span data-ttu-id="f4c85-133">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="f4c85-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="f4c85-134">Создает конфигурацию виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="f4c85-134">Creates a VM configuration.</span></span> <span data-ttu-id="f4c85-135">Эта конфигурация включает в себя такие сведения, как имя виртуальной машины, операционную систему и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="f4c85-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="f4c85-136">Конфигурация Hello используется во время создания виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="f4c85-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="f4c85-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="f4c85-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="f4c85-138">Создайте виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="f4c85-138">Create a virtual machine.</span></span> |
|[<span data-ttu-id="f4c85-139">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f4c85-139">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="f4c85-140">Удаляет группу ресурсов и все ресурсы, содержащиеся в ней.</span><span class="sxs-lookup"><span data-stu-id="f4c85-140">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f4c85-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f4c85-141">Next steps</span></span>

<span data-ttu-id="f4c85-142">Дополнительные сведения о hello модуля Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f4c85-142">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f4c85-143">Примеры сценариев PowerShell дополнительную виртуальную машину можно найти в hello [документации виртуальной Машины Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f4c85-143">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
