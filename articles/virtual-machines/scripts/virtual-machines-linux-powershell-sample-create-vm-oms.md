---
title: "Пример сценария Azure PowerShell для OMS | Документация Майкрософт"
description: "Пример сценария Azure PowerShell для OMS."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/01/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: cd23f71221efb62d2547b2b683ca8e2218403a2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-operations-management-suite-monitored-vm-with-powershell"></a><span data-ttu-id="347d6-103">Создание виртуальной машины, отслеживаемой Operations Management Suite, с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="347d6-103">Create an Operations Management Suite monitored VM with PowerShell</span></span>

<span data-ttu-id="347d6-104">Этот скрипт создает виртуальную машину Azure, устанавливает агент Operations Management Suite и регистрирует систему в рабочей области OMS.</span><span class="sxs-lookup"><span data-stu-id="347d6-104">This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace.</span></span> <span data-ttu-id="347d6-105">После выполнения скрипта виртуальная машина отобразится в консоли OMS.</span><span class="sxs-lookup"><span data-stu-id="347d6-105">Once the script has run, the virtual machine will be visible in the OMS console.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="347d6-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="347d6-106">Sample script</span></span>

<span data-ttu-id="347d6-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-monitor-oms/create-vm-monitor-oms.ps1 "Создание виртуальной машины OMS")]</span><span class="sxs-lookup"><span data-stu-id="347d6-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-monitor-oms/create-vm-monitor-oms.ps1 "Create VM OMS")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="347d6-108">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="347d6-108">Clean up deployment</span></span> 

<span data-ttu-id="347d6-109">Выполните следующую команду, чтобы удалить группу ресурсов, виртуальную машину и все связанные с ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="347d6-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="347d6-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="347d6-110">Script explanation</span></span>

<span data-ttu-id="347d6-111">Чтобы создать развертывание, скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="347d6-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="347d6-112">Для каждого элемента в таблице приведены ссылки на документацию по команде.</span><span class="sxs-lookup"><span data-stu-id="347d6-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="347d6-113">Команда</span><span class="sxs-lookup"><span data-stu-id="347d6-113">Command</span></span> | <span data-ttu-id="347d6-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="347d6-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="347d6-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="347d6-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="347d6-116">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="347d6-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="347d6-117">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="347d6-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="347d6-118">Создает конфигурацию подсети.</span><span class="sxs-lookup"><span data-stu-id="347d6-118">Creates a subnet configuration.</span></span> <span data-ttu-id="347d6-119">Эта конфигурация используется в процессе создания виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="347d6-119">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="347d6-120">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="347d6-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="347d6-121">Создает виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="347d6-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="347d6-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="347d6-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="347d6-123">Создает общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="347d6-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="347d6-124">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="347d6-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="347d6-125">Создает конфигурацию правил группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="347d6-125">Creates a network security group rule configuration.</span></span> <span data-ttu-id="347d6-126">Эта конфигурация используется для создания правила NSG при создании этой NSG.</span><span class="sxs-lookup"><span data-stu-id="347d6-126">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="347d6-127">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="347d6-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="347d6-128">Создает группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="347d6-128">Creates a network security group.</span></span> |
| [<span data-ttu-id="347d6-129">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="347d6-129">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="347d6-130">Возвращает сведения о подсети.</span><span class="sxs-lookup"><span data-stu-id="347d6-130">Gets subnet information.</span></span> <span data-ttu-id="347d6-131">Эта информация используется при создании сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="347d6-131">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="347d6-132">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="347d6-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="347d6-133">Создает сетевой интерфейс.</span><span class="sxs-lookup"><span data-stu-id="347d6-133">Creates a network interface.</span></span> |
| [<span data-ttu-id="347d6-134">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="347d6-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="347d6-135">Создает конфигурацию виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="347d6-135">Creates a VM configuration.</span></span> <span data-ttu-id="347d6-136">Эта конфигурация включает в себя такие сведения, как имя виртуальной машины, операционную систему и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="347d6-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="347d6-137">Данная конфигурации используется при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="347d6-137">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="347d6-138">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="347d6-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="347d6-139">Создайте виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="347d6-139">Create a virtual machine.</span></span> |
| [<span data-ttu-id="347d6-140">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="347d6-140">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="347d6-141">Добавляет в виртуальную машину расширение виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="347d6-141">Add a VM extension to the virtual machine.</span></span> <span data-ttu-id="347d6-142">В этом случае расширение агента Operations Management Suite используется для установки агента OMS и регистрации виртуальной машины в рабочей области OMS.</span><span class="sxs-lookup"><span data-stu-id="347d6-142">In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace.</span></span> |
|[<span data-ttu-id="347d6-143">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="347d6-143">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="347d6-144">Удаляет группу ресурсов и все ресурсы, содержащиеся в ней.</span><span class="sxs-lookup"><span data-stu-id="347d6-144">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="347d6-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="347d6-145">Next steps</span></span>

<span data-ttu-id="347d6-146">Дополнительные сведения о модуле Azure PowerShell см. в [документации по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="347d6-146">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="347d6-147">Дополнительные примеры сценариев PowerShell для виртуальных машин представлены в [документации по виртуальным машинам Azure под управлением Linux](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="347d6-147">Additional virtual machine PowerShell script samples can be found in the [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
