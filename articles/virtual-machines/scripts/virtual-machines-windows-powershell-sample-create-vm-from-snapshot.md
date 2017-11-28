---
title: "Пример сценария PowerShell - aaaAzure создания виртуальной Машины из моментального снимка | Документы Microsoft"
description: "Создание виртуальной машины из моментального снимка с помощью сценария Azure PowerShell."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: 89c65171b55bff0582c4a26df0b0f29f556845fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-powershell"></a><span data-ttu-id="24316-103">Создание виртуальной машины из моментального снимка с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="24316-103">Create a virtual machine from a snapshot with PowerShell</span></span>

<span data-ttu-id="24316-104">Этот скрипт создает виртуальную машину из моментального снимка диска ОС.</span><span class="sxs-lookup"><span data-stu-id="24316-104">This script creates a virtual machine from a snapshot of an OS disk.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="24316-105">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="24316-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from managed os disk")]

## <a name="clean-up-deployment"></a><span data-ttu-id="24316-106">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="24316-106">Clean up deployment</span></span> 

<span data-ttu-id="24316-107">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="24316-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="24316-108">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="24316-108">Script explanation</span></span>

<span data-ttu-id="24316-109">Этот скрипт использует hello, следующие команды tooget свойства моментального снимка, создание управляемого диска из моментального снимка и создания виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="24316-109">This script uses hello following commands tooget snapshot properties, create a managed disk from snapshot and create a VM.</span></span> <span data-ttu-id="24316-110">Каждый элемент в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="24316-110">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="24316-111">Команда</span><span class="sxs-lookup"><span data-stu-id="24316-111">Command</span></span> | <span data-ttu-id="24316-112">Примечания</span><span class="sxs-lookup"><span data-stu-id="24316-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="24316-113">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="24316-113">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/get-azurermsnapshot) | <span data-ttu-id="24316-114">Возвращает моментальный снимок на основе его имени.</span><span class="sxs-lookup"><span data-stu-id="24316-114">Gets a snapshot using snapshot name.</span></span> |
| [<span data-ttu-id="24316-115">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="24316-115">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/new-azurermdiskconfig) | <span data-ttu-id="24316-116">Создает конфигурацию диска.</span><span class="sxs-lookup"><span data-stu-id="24316-116">Creates a disk configuration.</span></span> <span data-ttu-id="24316-117">Эта конфигурация используется с процессом создания диска hello.</span><span class="sxs-lookup"><span data-stu-id="24316-117">This configuration is used with hello disk creation process.</span></span> |
| [<span data-ttu-id="24316-118">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="24316-118">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/new-azurermdisk) | <span data-ttu-id="24316-119">Создает управляемый диск.</span><span class="sxs-lookup"><span data-stu-id="24316-119">Creates a managed disk.</span></span> |
| [<span data-ttu-id="24316-120">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="24316-120">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="24316-121">Создает конфигурацию виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="24316-121">Creates a VM configuration.</span></span> <span data-ttu-id="24316-122">Эта конфигурация включает в себя такие сведения, как имя виртуальной машины, операционную систему и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="24316-122">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="24316-123">Конфигурация Hello используется во время создания виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="24316-123">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="24316-124">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="24316-124">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmosdisk) | <span data-ttu-id="24316-125">Присоединяет hello управляемого диска операционной системы диска toohello виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="24316-125">Attaches hello managed disk as OS disk toohello virtual machine</span></span> |
| [<span data-ttu-id="24316-126">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="24316-126">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="24316-127">Создает общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="24316-127">Creates a public IP address.</span></span> |
| [<span data-ttu-id="24316-128">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="24316-128">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="24316-129">Создает сетевой интерфейс.</span><span class="sxs-lookup"><span data-stu-id="24316-129">Creates a network interface.</span></span> |
| [<span data-ttu-id="24316-130">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="24316-130">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="24316-131">Создает виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="24316-131">Creates a virtual machine.</span></span> |
|[<span data-ttu-id="24316-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="24316-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="24316-133">Удаляет группу ресурсов и все ресурсы, содержащиеся в ней.</span><span class="sxs-lookup"><span data-stu-id="24316-133">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="24316-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="24316-134">Next steps</span></span>

<span data-ttu-id="24316-135">Дополнительные сведения о hello модуля Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="24316-135">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="24316-136">Примеры сценариев PowerShell дополнительную виртуальную машину можно найти в hello [документации виртуальной Машины Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="24316-136">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
