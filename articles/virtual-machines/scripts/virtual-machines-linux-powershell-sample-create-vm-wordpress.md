---
title: "aaaAzure образец скрипта PowerShell - WordPress | Документы Microsoft"
description: "Пример сценария Azure PowerShell для WordPress."
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
ms.openlocfilehash: b011726a772bb4d13fcfcba088eac4d0305967c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-wordpress-vm-with-powershell"></a><span data-ttu-id="fdcfd-103">Создание виртуальной машины WordPress с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="fdcfd-103">Create a WordPress VM with PowerShell</span></span>

<span data-ttu-id="fdcfd-104">Этот скрипт создает виртуальную машину и использует расширение пользовательского скрипта tooinstall WordPress для hello виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="fdcfd-104">This script creates a virtual machine and uses hello Azure Virtual Machine custom script extension tooinstall WordPress.</span></span> <span data-ttu-id="fdcfd-105">После выполнения скрипта hello, можно получить доступ к hello WordPress веб-сайт конфигурации на `http://<public IP of VM>/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="fdcfd-105">After running hello script, you can access hello WordPress configuration site at  `http://<public IP of VM>/wordpress`.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="fdcfd-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="fdcfd-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.ps1 "Create VM WordPress")]

## <a name="clean-up-deployment"></a><span data-ttu-id="fdcfd-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="fdcfd-107">Clean up deployment</span></span> 

<span data-ttu-id="fdcfd-108">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="fdcfd-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="fdcfd-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="fdcfd-109">Script explanation</span></span>

<span data-ttu-id="fdcfd-110">Этот скрипт использует следующие команды toocreate hello развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="fdcfd-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="fdcfd-111">Каждый элемент в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="fdcfd-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="fdcfd-112">Команда</span><span class="sxs-lookup"><span data-stu-id="fdcfd-112">Command</span></span> | <span data-ttu-id="fdcfd-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="fdcfd-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fdcfd-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="fdcfd-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="fdcfd-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="fdcfd-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fdcfd-116">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="fdcfd-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="fdcfd-117">Создает конфигурацию подсети.</span><span class="sxs-lookup"><span data-stu-id="fdcfd-117">Creates a subnet configuration.</span></span> <span data-ttu-id="fdcfd-118">Эта конфигурация используется с hello процесс создания виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="fdcfd-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="fdcfd-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="fdcfd-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="fdcfd-120">Создает виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="fdcfd-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="fdcfd-121">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="fdcfd-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="fdcfd-122">Создает общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="fdcfd-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="fdcfd-123">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="fdcfd-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="fdcfd-124">Создает конфигурацию правил группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="fdcfd-124">Creates a network security group rule configuration.</span></span> <span data-ttu-id="fdcfd-125">Такая настройка является toocreate используется правило NSG при создании hello NSG.</span><span class="sxs-lookup"><span data-stu-id="fdcfd-125">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="fdcfd-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="fdcfd-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="fdcfd-127">Создает группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="fdcfd-127">Creates a network security group.</span></span> |
| [<span data-ttu-id="fdcfd-128">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="fdcfd-128">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="fdcfd-129">Возвращает сведения о подсети.</span><span class="sxs-lookup"><span data-stu-id="fdcfd-129">Gets subnet information.</span></span> <span data-ttu-id="fdcfd-130">Эта информация используется при создании сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="fdcfd-130">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="fdcfd-131">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="fdcfd-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="fdcfd-132">Создает сетевой интерфейс.</span><span class="sxs-lookup"><span data-stu-id="fdcfd-132">Creates a network interface.</span></span> |
| [<span data-ttu-id="fdcfd-133">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="fdcfd-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="fdcfd-134">Создает конфигурацию виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="fdcfd-134">Creates a VM configuration.</span></span> <span data-ttu-id="fdcfd-135">Эта конфигурация включает в себя такие сведения, как имя виртуальной машины, операционную систему и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="fdcfd-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="fdcfd-136">Конфигурация Hello используется во время создания виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="fdcfd-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="fdcfd-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="fdcfd-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="fdcfd-138">Создайте виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="fdcfd-138">Create a virtual machine.</span></span> |
| [<span data-ttu-id="fdcfd-139">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="fdcfd-139">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="fdcfd-140">Добавьте hello настраиваемое расширение скриптов toohello виртуального компьютера, который вызывает сценарий tooinstall WordPress.</span><span class="sxs-lookup"><span data-stu-id="fdcfd-140">Add hello Custom Script Extension toohello virtual machine, which invokes a script tooinstall WordPress.</span></span> |
|[<span data-ttu-id="fdcfd-141">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="fdcfd-141">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="fdcfd-142">Удаляет группу ресурсов и все ресурсы, содержащиеся в ней.</span><span class="sxs-lookup"><span data-stu-id="fdcfd-142">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fdcfd-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fdcfd-143">Next steps</span></span>

<span data-ttu-id="fdcfd-144">Дополнительные сведения о hello модуля Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fdcfd-144">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="fdcfd-145">Примеры сценариев PowerShell дополнительную виртуальную машину можно найти в hello [документации виртуальной Машине Linux Azure](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fdcfd-145">Additional virtual machine PowerShell script samples can be found in hello [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
