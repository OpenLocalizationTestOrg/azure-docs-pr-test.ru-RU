---
title: "Пример сценария Azure PowerShell. Создание виртуальной машины из моментального снимка | Документация Майкрософт"
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
ms.openlocfilehash: 63d108bbfd0f58f8a40bf1c7c8649e3a1f7ed288
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-powershell"></a><span data-ttu-id="4f467-103">Создание виртуальной машины из моментального снимка с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="4f467-103">Create a virtual machine from a snapshot with PowerShell</span></span>

<span data-ttu-id="4f467-104">Этот скрипт создает виртуальную машину из моментального снимка диска ОС.</span><span class="sxs-lookup"><span data-stu-id="4f467-104">This script creates a virtual machine from a snapshot of an OS disk.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="4f467-105">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="4f467-105">Sample script</span></span>

<span data-ttu-id="4f467-106">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Создание виртуальной машины с помощью управляемого диска ОС")]</span><span class="sxs-lookup"><span data-stu-id="4f467-106">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from managed os disk")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="4f467-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="4f467-107">Clean up deployment</span></span> 

<span data-ttu-id="4f467-108">Выполните следующую команду, чтобы удалить группу ресурсов, виртуальную машину и все связанные с ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="4f467-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="4f467-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="4f467-109">Script explanation</span></span>

<span data-ttu-id="4f467-110">Для получения свойств моментального снимка, создания управляемого диска из моментального снимка и создания виртуальной машины этот сценарий использует указанные ниже команды.</span><span class="sxs-lookup"><span data-stu-id="4f467-110">This script uses the following commands to get snapshot properties, create a managed disk from snapshot and create a VM.</span></span> <span data-ttu-id="4f467-111">Для каждого элемента в таблице приведены ссылки на документацию по команде.</span><span class="sxs-lookup"><span data-stu-id="4f467-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="4f467-112">Команда</span><span class="sxs-lookup"><span data-stu-id="4f467-112">Command</span></span> | <span data-ttu-id="4f467-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="4f467-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4f467-114">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="4f467-114">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/get-azurermsnapshot) | <span data-ttu-id="4f467-115">Возвращает моментальный снимок на основе его имени.</span><span class="sxs-lookup"><span data-stu-id="4f467-115">Gets a snapshot using snapshot name.</span></span> |
| [<span data-ttu-id="4f467-116">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="4f467-116">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/new-azurermdiskconfig) | <span data-ttu-id="4f467-117">Создает конфигурацию диска.</span><span class="sxs-lookup"><span data-stu-id="4f467-117">Creates a disk configuration.</span></span> <span data-ttu-id="4f467-118">Эта конфигурация используется при создании диска.</span><span class="sxs-lookup"><span data-stu-id="4f467-118">This configuration is used with the disk creation process.</span></span> |
| [<span data-ttu-id="4f467-119">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="4f467-119">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/new-azurermdisk) | <span data-ttu-id="4f467-120">Создает управляемый диск.</span><span class="sxs-lookup"><span data-stu-id="4f467-120">Creates a managed disk.</span></span> |
| [<span data-ttu-id="4f467-121">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="4f467-121">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="4f467-122">Создает конфигурацию виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="4f467-122">Creates a VM configuration.</span></span> <span data-ttu-id="4f467-123">Эта конфигурация включает в себя такие сведения, как имя виртуальной машины, операционную систему и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="4f467-123">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="4f467-124">Данная конфигурации используется при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="4f467-124">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="4f467-125">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="4f467-125">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmosdisk) | <span data-ttu-id="4f467-126">Присоединяет управляемый диск в качестве диска ОС к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="4f467-126">Attaches the managed disk as OS disk to the virtual machine</span></span> |
| [<span data-ttu-id="4f467-127">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="4f467-127">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="4f467-128">Создает общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="4f467-128">Creates a public IP address.</span></span> |
| [<span data-ttu-id="4f467-129">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="4f467-129">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="4f467-130">Создает сетевой интерфейс.</span><span class="sxs-lookup"><span data-stu-id="4f467-130">Creates a network interface.</span></span> |
| [<span data-ttu-id="4f467-131">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="4f467-131">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="4f467-132">Создает виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="4f467-132">Creates a virtual machine.</span></span> |
|[<span data-ttu-id="4f467-133">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4f467-133">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="4f467-134">Удаляет группу ресурсов и все ресурсы, содержащиеся в ней.</span><span class="sxs-lookup"><span data-stu-id="4f467-134">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4f467-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4f467-135">Next steps</span></span>

<span data-ttu-id="4f467-136">Дополнительные сведения о модуле Azure PowerShell см. в [документации по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4f467-136">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="4f467-137">Дополнительные примеры сценариев PowerShell для виртуальных машин представлены в [документации по виртуальным машинам Azure под управлением Windows](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4f467-137">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>