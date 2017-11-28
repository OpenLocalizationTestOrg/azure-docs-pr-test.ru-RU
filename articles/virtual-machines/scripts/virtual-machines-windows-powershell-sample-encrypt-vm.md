---
title: "Пример сценария Azure PowerShell. Шифрование виртуальной машины Windows | Документация Майкрософт"
description: "Пример сценария Azure PowerShell для шифрования виртуальной машины Windows."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/02/2017
ms.author: iainfou
ms.openlocfilehash: 9279fea482fcd8716bcd996985e10f500a4775ce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="encrypt-a-windows-virtual-machine-with-azure-powershell"></a><span data-ttu-id="77a66-103">Шифрование виртуальной машины Windows с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="77a66-103">Encrypt a Windows virtual machine with Azure PowerShell</span></span>

<span data-ttu-id="77a66-104">Этот сценарий создает безопасное Azure Key Vault, ключи шифрования, субъект-службу Azure Active Directory и виртуальную машину Windows.</span><span class="sxs-lookup"><span data-stu-id="77a66-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Windows virtual machine (VM).</span></span> <span data-ttu-id="77a66-105">Затем эта виртуальная машина шифруется с помощью ключа шифрования из Key Vault и учетных данных субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="77a66-105">The VM is then encrypted using the encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="77a66-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="77a66-106">Sample script</span></span>

<span data-ttu-id="77a66-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/encrypt-vm/encrypt-windows-vm.ps1 "Шифрование дисков виртуальной машины")]</span><span class="sxs-lookup"><span data-stu-id="77a66-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/encrypt-vm/encrypt-windows-vm.ps1 "Encrypt VM disks")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="77a66-108">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="77a66-108">Clean up deployment</span></span> 

<span data-ttu-id="77a66-109">Выполните следующую команду, чтобы удалить группу ресурсов, виртуальную машину и все связанные с ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="77a66-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="77a66-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="77a66-110">Script explanation</span></span>

<span data-ttu-id="77a66-111">Чтобы создать развертывание, скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="77a66-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="77a66-112">Для каждого элемента в таблице приведены ссылки на документацию по команде.</span><span class="sxs-lookup"><span data-stu-id="77a66-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="77a66-113">Команда</span><span class="sxs-lookup"><span data-stu-id="77a66-113">Command</span></span> | <span data-ttu-id="77a66-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="77a66-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="77a66-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="77a66-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="77a66-116">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="77a66-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="77a66-117">New-AzureRmKeyVault</span><span class="sxs-lookup"><span data-stu-id="77a66-117">New-AzureRmKeyVault</span></span>](/powershell/module/azurerm.keyvault/new-azurermkeyvault) | <span data-ttu-id="77a66-118">Создает Azure Key Vault для хранения защищенных данных, таких как ключи шифрования.</span><span class="sxs-lookup"><span data-stu-id="77a66-118">Creates an Azure Key Vault to store secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="77a66-119">Add-AzureKeyVaultKey</span><span class="sxs-lookup"><span data-stu-id="77a66-119">Add-AzureKeyVaultKey</span></span>](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) | <span data-ttu-id="77a66-120">Создает ключ шифрования в Key Vault.</span><span class="sxs-lookup"><span data-stu-id="77a66-120">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="77a66-121">New-AzureRmADServicePrincipal</span><span class="sxs-lookup"><span data-stu-id="77a66-121">New-AzureRmADServicePrincipal</span></span>](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | <span data-ttu-id="77a66-122">Создает субъект-службу Azure Active Directory для безопасной аутентификации и контроля доступа к ключам шифрования.</span><span class="sxs-lookup"><span data-stu-id="77a66-122">Creates an Azure Active Directory service principal to securely authenticate and control access to encryption keys.</span></span> |
| [<span data-ttu-id="77a66-123">Set-AzureRmKeyVaultAccessPolicy</span><span class="sxs-lookup"><span data-stu-id="77a66-123">Set-AzureRmKeyVaultAccessPolicy</span></span>](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) | <span data-ttu-id="77a66-124">Задает разрешения для Key Vault, предоставляя субъекту-службе доступ к ключам шифрования.</span><span class="sxs-lookup"><span data-stu-id="77a66-124">Sets permissions on the Key Vault to grant the service principal access to encryption keys.</span></span> |
| [<span data-ttu-id="77a66-125">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="77a66-125">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="77a66-126">Создает конфигурацию подсети.</span><span class="sxs-lookup"><span data-stu-id="77a66-126">Creates a subnet configuration.</span></span> <span data-ttu-id="77a66-127">Эта конфигурация используется в процессе создания виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="77a66-127">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="77a66-128">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="77a66-128">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="77a66-129">Создает виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="77a66-129">Creates a virtual network.</span></span> |
| [<span data-ttu-id="77a66-130">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="77a66-130">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="77a66-131">Создает общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="77a66-131">Creates a public IP address.</span></span> |
| [<span data-ttu-id="77a66-132">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="77a66-132">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="77a66-133">Создает конфигурацию правил группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="77a66-133">Creates a network security group rule configuration.</span></span> <span data-ttu-id="77a66-134">Эта конфигурация используется для создания правила NSG при создании этой NSG.</span><span class="sxs-lookup"><span data-stu-id="77a66-134">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="77a66-135">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="77a66-135">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="77a66-136">Создает группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="77a66-136">Creates a network security group.</span></span> |
| [<span data-ttu-id="77a66-137">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="77a66-137">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="77a66-138">Возвращает сведения о подсети.</span><span class="sxs-lookup"><span data-stu-id="77a66-138">Gets subnet information.</span></span> <span data-ttu-id="77a66-139">Эта информация используется при создании сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="77a66-139">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="77a66-140">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="77a66-140">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="77a66-141">Создает сетевой интерфейс.</span><span class="sxs-lookup"><span data-stu-id="77a66-141">Creates a network interface.</span></span> |
| [<span data-ttu-id="77a66-142">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="77a66-142">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="77a66-143">Создает конфигурацию виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="77a66-143">Creates a VM configuration.</span></span> <span data-ttu-id="77a66-144">Эта конфигурация включает в себя такие сведения, как имя виртуальной машины, операционную систему и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="77a66-144">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="77a66-145">Данная конфигурации используется при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="77a66-145">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="77a66-146">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="77a66-146">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="77a66-147">Создайте виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="77a66-147">Create a virtual machine.</span></span> |
| [<span data-ttu-id="77a66-148">Get-AzureRmKeyVault</span><span class="sxs-lookup"><span data-stu-id="77a66-148">Get-AzureRmKeyVault</span></span>](/powershell/module/azurerm.keyvault/get-azurermkeyvault) | <span data-ttu-id="77a66-149">Получает необходимые сведения о Key Vault.</span><span class="sxs-lookup"><span data-stu-id="77a66-149">Gets required information on the Key Vault</span></span> |
| [<span data-ttu-id="77a66-150">Set-AzureRmVMDiskEncryptionExtension</span><span class="sxs-lookup"><span data-stu-id="77a66-150">Set-AzureRmVMDiskEncryptionExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) | <span data-ttu-id="77a66-151">Включает шифрование на виртуальной машине с помощью учетных данных субъекта-службы и ключа шифрования.</span><span class="sxs-lookup"><span data-stu-id="77a66-151">Enables encryption on a VM using the service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="77a66-152">Get-AzureRmVmDiskEncryptionStatus</span><span class="sxs-lookup"><span data-stu-id="77a66-152">Get-AzureRmVmDiskEncryptionStatus</span></span>](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus) | <span data-ttu-id="77a66-153">Отображает состояние шифрования виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="77a66-153">Shows the status of the VM encryption process.</span></span> |
| [<span data-ttu-id="77a66-154">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="77a66-154">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="77a66-155">Удаляет группу ресурсов и все ресурсы, содержащиеся в ней.</span><span class="sxs-lookup"><span data-stu-id="77a66-155">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="77a66-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="77a66-156">Next steps</span></span>

<span data-ttu-id="77a66-157">Дополнительные сведения о модуле Azure PowerShell см. в [документации по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="77a66-157">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="77a66-158">Дополнительные примеры сценариев PowerShell для виртуальных машин представлены в [документации по виртуальным машинам Azure под управлением Windows](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="77a66-158">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
