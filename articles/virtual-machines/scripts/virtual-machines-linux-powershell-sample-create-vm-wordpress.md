---
title: "Пример сценария Azure PowerShell для WordPress | Документация Майкрософт"
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
ms.openlocfilehash: 778a6d5cfc63f80aa66654d682fedb178cfd67a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-wordpress-vm-with-powershell"></a><span data-ttu-id="1f2df-103">Создание виртуальной машины WordPress с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="1f2df-103">Create a WordPress VM with PowerShell</span></span>

<span data-ttu-id="1f2df-104">Этот сценарий создает виртуальную машину и устанавливает WordPress с использованием расширения пользовательских сценариев виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="1f2df-104">This script creates a virtual machine and uses the Azure Virtual Machine custom script extension to install WordPress.</span></span> <span data-ttu-id="1f2df-105">После выполнения сценария можно получить доступ к сайту конфигурации WordPress по адресу `http://<public IP of VM>/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="1f2df-105">After running the script, you can access the WordPress configuration site at  `http://<public IP of VM>/wordpress`.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="1f2df-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="1f2df-106">Sample script</span></span>

<span data-ttu-id="1f2df-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.ps1 "Создание виртуальной машины WordPress")]</span><span class="sxs-lookup"><span data-stu-id="1f2df-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.ps1 "Create VM WordPress")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="1f2df-108">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="1f2df-108">Clean up deployment</span></span> 

<span data-ttu-id="1f2df-109">Выполните следующую команду, чтобы удалить группу ресурсов, виртуальную машину и все связанные с ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="1f2df-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="1f2df-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="1f2df-110">Script explanation</span></span>

<span data-ttu-id="1f2df-111">Чтобы создать развертывание, скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="1f2df-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="1f2df-112">Для каждого элемента в таблице приведены ссылки на документацию по команде.</span><span class="sxs-lookup"><span data-stu-id="1f2df-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="1f2df-113">Команда</span><span class="sxs-lookup"><span data-stu-id="1f2df-113">Command</span></span> | <span data-ttu-id="1f2df-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="1f2df-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1f2df-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1f2df-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="1f2df-116">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="1f2df-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1f2df-117">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="1f2df-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="1f2df-118">Создает конфигурацию подсети.</span><span class="sxs-lookup"><span data-stu-id="1f2df-118">Creates a subnet configuration.</span></span> <span data-ttu-id="1f2df-119">Эта конфигурация используется в процессе создания виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="1f2df-119">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="1f2df-120">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="1f2df-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="1f2df-121">Создает виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="1f2df-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="1f2df-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="1f2df-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="1f2df-123">Создает общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="1f2df-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="1f2df-124">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="1f2df-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="1f2df-125">Создает конфигурацию правил группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="1f2df-125">Creates a network security group rule configuration.</span></span> <span data-ttu-id="1f2df-126">Эта конфигурация используется для создания правила NSG при создании этой NSG.</span><span class="sxs-lookup"><span data-stu-id="1f2df-126">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="1f2df-127">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="1f2df-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="1f2df-128">Создает группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="1f2df-128">Creates a network security group.</span></span> |
| [<span data-ttu-id="1f2df-129">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="1f2df-129">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="1f2df-130">Возвращает сведения о подсети.</span><span class="sxs-lookup"><span data-stu-id="1f2df-130">Gets subnet information.</span></span> <span data-ttu-id="1f2df-131">Эта информация используется при создании сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="1f2df-131">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="1f2df-132">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="1f2df-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="1f2df-133">Создает сетевой интерфейс.</span><span class="sxs-lookup"><span data-stu-id="1f2df-133">Creates a network interface.</span></span> |
| [<span data-ttu-id="1f2df-134">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="1f2df-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="1f2df-135">Создает конфигурацию виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="1f2df-135">Creates a VM configuration.</span></span> <span data-ttu-id="1f2df-136">Эта конфигурация включает в себя такие сведения, как имя виртуальной машины, операционную систему и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="1f2df-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="1f2df-137">Данная конфигурации используется при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="1f2df-137">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="1f2df-138">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="1f2df-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="1f2df-139">Создайте виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="1f2df-139">Create a virtual machine.</span></span> |
| [<span data-ttu-id="1f2df-140">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="1f2df-140">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="1f2df-141">Добавляет расширение пользовательских скриптов на виртуальную машину, вызывающее скрипт для установки WordPress.</span><span class="sxs-lookup"><span data-stu-id="1f2df-141">Add the Custom Script Extension to the virtual machine, which invokes a script to install WordPress.</span></span> |
|[<span data-ttu-id="1f2df-142">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1f2df-142">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="1f2df-143">Удаляет группу ресурсов и все ресурсы, содержащиеся в ней.</span><span class="sxs-lookup"><span data-stu-id="1f2df-143">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1f2df-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1f2df-144">Next steps</span></span>

<span data-ttu-id="1f2df-145">Дополнительные сведения о модуле Azure PowerShell см. в [документации по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1f2df-145">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="1f2df-146">Дополнительные примеры сценариев PowerShell для виртуальных машин представлены в [документации по виртуальным машинам Azure под управлением Linux](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1f2df-146">Additional virtual machine PowerShell script samples can be found in the [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
