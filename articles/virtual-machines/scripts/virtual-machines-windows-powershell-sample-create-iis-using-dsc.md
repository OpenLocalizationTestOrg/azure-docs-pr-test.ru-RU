---
title: "Пример сценария Azure PowerShell для IIS с использованием DSC | Документация Майкрософт"
description: "Пример сценария Azure PowerShell для IIS с использованием DSC"
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
ms.date: 03/01/2017
ms.author: nepeters
ms.openlocfilehash: 38476119c88aa7d4f6578fc1e3756e11951e804a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-iis-vm-with-powershell"></a><span data-ttu-id="0b80e-103">Создание виртуальной машины IIS с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="0b80e-103">Create an IIS VM with PowerShell</span></span>

<span data-ttu-id="0b80e-104">Этот сценарий создает виртуальную машину Azure под управлением Windows Server 2016, а затем использует расширение DSC для виртуальных машин Azure, чтобы установить IIS.</span><span class="sxs-lookup"><span data-stu-id="0b80e-104">This script creates an Azure Virtual Machine running Windows Server 2016, and then uses the Azure Virtual Machine DSC Extension to install IIS.</span></span> <span data-ttu-id="0b80e-105">После выполнения сценария можно получить доступ к веб-сайту IIS по умолчанию по общедоступному IP-адресу виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0b80e-105">After running the script, you can access the default IIS website on the public IP address of the virtual machine.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="0b80e-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="0b80e-106">Sample script</span></span>

<span data-ttu-id="0b80e-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-dsc/create-windows-vm-iis-dsc.ps1 "Создание виртуальной машины IIS DSC")]</span><span class="sxs-lookup"><span data-stu-id="0b80e-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-dsc/create-windows-vm-iis-dsc.ps1 "Create VM IIS DSC")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="0b80e-108">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="0b80e-108">Clean up deployment</span></span> 

<span data-ttu-id="0b80e-109">Выполните следующую команду, чтобы удалить группу ресурсов, виртуальную машину и все связанные с ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="0b80e-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="0b80e-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="0b80e-110">Script explanation</span></span>

<span data-ttu-id="0b80e-111">Чтобы создать развертывание, скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="0b80e-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="0b80e-112">Для каждого элемента в таблице приведены ссылки на документацию по команде.</span><span class="sxs-lookup"><span data-stu-id="0b80e-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="0b80e-113">Команда</span><span class="sxs-lookup"><span data-stu-id="0b80e-113">Command</span></span> | <span data-ttu-id="0b80e-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="0b80e-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0b80e-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0b80e-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="0b80e-116">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="0b80e-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0b80e-117">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="0b80e-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="0b80e-118">Создает конфигурацию подсети.</span><span class="sxs-lookup"><span data-stu-id="0b80e-118">Creates a subnet configuration.</span></span> <span data-ttu-id="0b80e-119">Эта конфигурация используется в процессе создания виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="0b80e-119">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="0b80e-120">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="0b80e-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="0b80e-121">Создает виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="0b80e-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="0b80e-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="0b80e-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="0b80e-123">Создает общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="0b80e-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="0b80e-124">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="0b80e-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="0b80e-125">Создает конфигурацию правил группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="0b80e-125">Creates a network security group rule configuration.</span></span> <span data-ttu-id="0b80e-126">Эта конфигурация используется для создания правила NSG при создании этой NSG.</span><span class="sxs-lookup"><span data-stu-id="0b80e-126">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="0b80e-127">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="0b80e-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="0b80e-128">Создает группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="0b80e-128">Creates a network security group.</span></span> |
| [<span data-ttu-id="0b80e-129">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="0b80e-129">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="0b80e-130">Возвращает сведения о подсети.</span><span class="sxs-lookup"><span data-stu-id="0b80e-130">Gets subnet information.</span></span> <span data-ttu-id="0b80e-131">Эта информация используется при создании сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="0b80e-131">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="0b80e-132">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="0b80e-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="0b80e-133">Создает сетевой интерфейс.</span><span class="sxs-lookup"><span data-stu-id="0b80e-133">Creates a network interface.</span></span> |
| [<span data-ttu-id="0b80e-134">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="0b80e-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="0b80e-135">Создает конфигурацию виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0b80e-135">Creates a VM configuration.</span></span> <span data-ttu-id="0b80e-136">Эта конфигурация включает в себя такие сведения, как имя виртуальной машины, операционную систему и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="0b80e-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="0b80e-137">Данная конфигурации используется при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0b80e-137">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="0b80e-138">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="0b80e-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="0b80e-139">Создайте виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="0b80e-139">Create a virtual machine.</span></span> |
| [<span data-ttu-id="0b80e-140">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="0b80e-140">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="0b80e-141">Добавляет в виртуальную машину расширение виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0b80e-141">Add a VM extension to the virtual machine.</span></span> <span data-ttu-id="0b80e-142">В этом примере для установки IIS используется расширение пользовательских скриптов.</span><span class="sxs-lookup"><span data-stu-id="0b80e-142">In this sample, the custom script extension is used to install IIS.</span></span> |
|[<span data-ttu-id="0b80e-143">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0b80e-143">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="0b80e-144">Удаляет группу ресурсов и все ресурсы, содержащиеся в ней.</span><span class="sxs-lookup"><span data-stu-id="0b80e-144">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0b80e-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0b80e-145">Next steps</span></span>

<span data-ttu-id="0b80e-146">Дополнительные сведения о модуле Azure PowerShell см. в [документации по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0b80e-146">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="0b80e-147">Дополнительные примеры сценариев PowerShell для виртуальных машин представлены в [документации по виртуальным машинам Azure под управлением Windows](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0b80e-147">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
