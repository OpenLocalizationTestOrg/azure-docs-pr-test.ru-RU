---
title: "Пример сценария PowerShell - aaaAzure шифрования ВМ Windows | Документы Microsoft"
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
ms.openlocfilehash: 80c52a0b734a52a051ed30026b294840fd521143
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-a-windows-virtual-machine-with-azure-powershell"></a><span data-ttu-id="d6480-103">Шифрование виртуальной машины Windows с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d6480-103">Encrypt a Windows virtual machine with Azure PowerShell</span></span>

<span data-ttu-id="d6480-104">Этот сценарий создает безопасное Azure Key Vault, ключи шифрования, субъект-службу Azure Active Directory и виртуальную машину Windows.</span><span class="sxs-lookup"><span data-stu-id="d6480-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Windows virtual machine (VM).</span></span> <span data-ttu-id="d6480-105">Hello ВМ шифруется с помощью ключа шифрования hello из хранилища ключей и учетных данных участника службы.</span><span class="sxs-lookup"><span data-stu-id="d6480-105">hello VM is then encrypted using hello encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d6480-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="d6480-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/encrypt-vm/encrypt-windows-vm.ps1 "Encrypt VM disks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="d6480-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="d6480-107">Clean up deployment</span></span> 

<span data-ttu-id="d6480-108">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="d6480-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="d6480-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="d6480-109">Script explanation</span></span>

<span data-ttu-id="d6480-110">Этот скрипт использует следующие команды toocreate hello развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="d6480-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="d6480-111">Каждый элемент в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="d6480-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d6480-112">Команда</span><span class="sxs-lookup"><span data-stu-id="d6480-112">Command</span></span> | <span data-ttu-id="d6480-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="d6480-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d6480-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d6480-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="d6480-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d6480-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d6480-116">New-AzureRmKeyVault</span><span class="sxs-lookup"><span data-stu-id="d6480-116">New-AzureRmKeyVault</span></span>](/powershell/module/azurerm.keyvault/new-azurermkeyvault) | <span data-ttu-id="d6480-117">Создает хранилище ключей Azure toostore безопасности данных, например ключи шифрования.</span><span class="sxs-lookup"><span data-stu-id="d6480-117">Creates an Azure Key Vault toostore secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="d6480-118">Add-AzureKeyVaultKey</span><span class="sxs-lookup"><span data-stu-id="d6480-118">Add-AzureKeyVaultKey</span></span>](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) | <span data-ttu-id="d6480-119">Создает ключ шифрования в Key Vault.</span><span class="sxs-lookup"><span data-stu-id="d6480-119">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="d6480-120">New-AzureRmADServicePrincipal</span><span class="sxs-lookup"><span data-stu-id="d6480-120">New-AzureRmADServicePrincipal</span></span>](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | <span data-ttu-id="d6480-121">Создает службу Azure Active Directory toosecurely основной проверки подлинности и управления ключами tooencryption доступа.</span><span class="sxs-lookup"><span data-stu-id="d6480-121">Creates an Azure Active Directory service principal toosecurely authenticate and control access tooencryption keys.</span></span> |
| [<span data-ttu-id="d6480-122">Set-AzureRmKeyVaultAccessPolicy</span><span class="sxs-lookup"><span data-stu-id="d6480-122">Set-AzureRmKeyVaultAccessPolicy</span></span>](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) | <span data-ttu-id="d6480-123">Задает разрешения на хранилище ключей toogrant hello разделы tooencryption участнику доступ к службе hello.</span><span class="sxs-lookup"><span data-stu-id="d6480-123">Sets permissions on hello Key Vault toogrant hello service principal access tooencryption keys.</span></span> |
| [<span data-ttu-id="d6480-124">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="d6480-124">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="d6480-125">Создает конфигурацию подсети.</span><span class="sxs-lookup"><span data-stu-id="d6480-125">Creates a subnet configuration.</span></span> <span data-ttu-id="d6480-126">Эта конфигурация используется с hello процесс создания виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="d6480-126">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="d6480-127">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="d6480-127">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="d6480-128">Создает виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="d6480-128">Creates a virtual network.</span></span> |
| [<span data-ttu-id="d6480-129">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="d6480-129">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="d6480-130">Создает общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="d6480-130">Creates a public IP address.</span></span> |
| [<span data-ttu-id="d6480-131">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="d6480-131">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="d6480-132">Создает конфигурацию правил группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="d6480-132">Creates a network security group rule configuration.</span></span> <span data-ttu-id="d6480-133">Такая настройка является toocreate используется правило NSG при создании hello NSG.</span><span class="sxs-lookup"><span data-stu-id="d6480-133">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="d6480-134">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="d6480-134">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="d6480-135">Создает группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="d6480-135">Creates a network security group.</span></span> |
| [<span data-ttu-id="d6480-136">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="d6480-136">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="d6480-137">Возвращает сведения о подсети.</span><span class="sxs-lookup"><span data-stu-id="d6480-137">Gets subnet information.</span></span> <span data-ttu-id="d6480-138">Эта информация используется при создании сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="d6480-138">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="d6480-139">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="d6480-139">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="d6480-140">Создает сетевой интерфейс.</span><span class="sxs-lookup"><span data-stu-id="d6480-140">Creates a network interface.</span></span> |
| [<span data-ttu-id="d6480-141">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="d6480-141">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="d6480-142">Создает конфигурацию виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d6480-142">Creates a VM configuration.</span></span> <span data-ttu-id="d6480-143">Эта конфигурация включает в себя такие сведения, как имя виртуальной машины, операционную систему и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="d6480-143">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="d6480-144">Конфигурация Hello используется во время создания виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d6480-144">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="d6480-145">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="d6480-145">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="d6480-146">Создайте виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="d6480-146">Create a virtual machine.</span></span> |
| [<span data-ttu-id="d6480-147">Get-AzureRmKeyVault</span><span class="sxs-lookup"><span data-stu-id="d6480-147">Get-AzureRmKeyVault</span></span>](/powershell/module/azurerm.keyvault/get-azurermkeyvault) | <span data-ttu-id="d6480-148">Получает необходимые сведения о хранилище ключей hello</span><span class="sxs-lookup"><span data-stu-id="d6480-148">Gets required information on hello Key Vault</span></span> |
| [<span data-ttu-id="d6480-149">Set-AzureRmVMDiskEncryptionExtension</span><span class="sxs-lookup"><span data-stu-id="d6480-149">Set-AzureRmVMDiskEncryptionExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) | <span data-ttu-id="d6480-150">Включает шифрование на ВМ с помощью учетных данных участника службы hello и ключ шифрования.</span><span class="sxs-lookup"><span data-stu-id="d6480-150">Enables encryption on a VM using hello service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="d6480-151">Get-AzureRmVmDiskEncryptionStatus</span><span class="sxs-lookup"><span data-stu-id="d6480-151">Get-AzureRmVmDiskEncryptionStatus</span></span>](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus) | <span data-ttu-id="d6480-152">Показывает состояние hello hello процесс шифрования виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d6480-152">Shows hello status of hello VM encryption process.</span></span> |
| [<span data-ttu-id="d6480-153">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d6480-153">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="d6480-154">Удаляет группу ресурсов и все ресурсы, содержащиеся в ней.</span><span class="sxs-lookup"><span data-stu-id="d6480-154">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d6480-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d6480-155">Next steps</span></span>

<span data-ttu-id="d6480-156">Дополнительные сведения о hello модуля Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d6480-156">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="d6480-157">Примеры сценариев PowerShell дополнительную виртуальную машину можно найти в hello [документации виртуальной Машины Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d6480-157">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
