---
title: "aaaAzure образец скрипта PowerShell - OMS | Документы Microsoft"
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
ms.openlocfilehash: 75bfa42b538d8f5f01bb24d507797470b9491602
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-operations-management-suite-monitored-vm-with-powershell"></a><span data-ttu-id="d14f9-103">Создание виртуальной машины, отслеживаемой Operations Management Suite, с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="d14f9-103">Create an Operations Management Suite monitored VM with PowerShell</span></span>

<span data-ttu-id="d14f9-104">Этот скрипт создает виртуальную машину Azure, устанавливает агент Operations Management Suite (OMS) hello и регистрирует hello системы с помощью рабочей области OMS.</span><span class="sxs-lookup"><span data-stu-id="d14f9-104">This script creates an Azure Virtual Machine, installs hello Operations Management Suite (OMS) agent, and enrolls hello system with an OMS workspace.</span></span> <span data-ttu-id="d14f9-105">После выполнения сценария hello, будут отображаться в консоли OMS hello hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d14f9-105">Once hello script has run, hello virtual machine will be visible in hello OMS console.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d14f9-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="d14f9-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-monitor-oms/create-vm-monitor-oms.ps1 "Create VM OMS")]

## <a name="clean-up-deployment"></a><span data-ttu-id="d14f9-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="d14f9-107">Clean up deployment</span></span> 

<span data-ttu-id="d14f9-108">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="d14f9-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="d14f9-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="d14f9-109">Script explanation</span></span>

<span data-ttu-id="d14f9-110">Этот скрипт использует следующие команды toocreate hello развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="d14f9-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="d14f9-111">Каждый элемент в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="d14f9-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d14f9-112">Команда</span><span class="sxs-lookup"><span data-stu-id="d14f9-112">Command</span></span> | <span data-ttu-id="d14f9-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="d14f9-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d14f9-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d14f9-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="d14f9-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d14f9-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d14f9-116">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="d14f9-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="d14f9-117">Создает конфигурацию подсети.</span><span class="sxs-lookup"><span data-stu-id="d14f9-117">Creates a subnet configuration.</span></span> <span data-ttu-id="d14f9-118">Эта конфигурация используется с hello процесс создания виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="d14f9-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="d14f9-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="d14f9-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="d14f9-120">Создает виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="d14f9-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="d14f9-121">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="d14f9-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="d14f9-122">Создает общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="d14f9-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="d14f9-123">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="d14f9-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="d14f9-124">Создает конфигурацию правил группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="d14f9-124">Creates a network security group rule configuration.</span></span> <span data-ttu-id="d14f9-125">Такая настройка является toocreate используется правило NSG при создании hello NSG.</span><span class="sxs-lookup"><span data-stu-id="d14f9-125">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="d14f9-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="d14f9-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="d14f9-127">Создает группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="d14f9-127">Creates a network security group.</span></span> |
| [<span data-ttu-id="d14f9-128">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="d14f9-128">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="d14f9-129">Возвращает сведения о подсети.</span><span class="sxs-lookup"><span data-stu-id="d14f9-129">Gets subnet information.</span></span> <span data-ttu-id="d14f9-130">Эта информация используется при создании сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="d14f9-130">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="d14f9-131">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="d14f9-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="d14f9-132">Создает сетевой интерфейс.</span><span class="sxs-lookup"><span data-stu-id="d14f9-132">Creates a network interface.</span></span> |
| [<span data-ttu-id="d14f9-133">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="d14f9-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="d14f9-134">Создает конфигурацию виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d14f9-134">Creates a VM configuration.</span></span> <span data-ttu-id="d14f9-135">Эта конфигурация включает в себя такие сведения, как имя виртуальной машины, операционную систему и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="d14f9-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="d14f9-136">Конфигурация Hello используется во время создания виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d14f9-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="d14f9-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="d14f9-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="d14f9-138">Создайте виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="d14f9-138">Create a virtual machine.</span></span> |
| [<span data-ttu-id="d14f9-139">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="d14f9-139">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="d14f9-140">Добавьте виртуальную машину toohello расширения виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d14f9-140">Add a VM extension toohello virtual machine.</span></span> <span data-ttu-id="d14f9-141">В этом случае hello расширение Operations Management Suite agent — агент OMS используется tooinstall hello и зарегистрировать hello виртуальной Машины в рабочей области OMS.</span><span class="sxs-lookup"><span data-stu-id="d14f9-141">In this case, hello Operations Management Suite agent extension is used tooinstall hello OMS agent and enroll hello VM in an OMS workspace.</span></span> |
|[<span data-ttu-id="d14f9-142">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d14f9-142">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="d14f9-143">Удаляет группу ресурсов и все ресурсы, содержащиеся в ней.</span><span class="sxs-lookup"><span data-stu-id="d14f9-143">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d14f9-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d14f9-144">Next steps</span></span>

<span data-ttu-id="d14f9-145">Дополнительные сведения о hello модуля Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d14f9-145">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="d14f9-146">Примеры сценариев PowerShell дополнительную виртуальную машину можно найти в hello [документации виртуальной Машине Linux Azure](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d14f9-146">Additional virtual machine PowerShell script samples can be found in hello [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
