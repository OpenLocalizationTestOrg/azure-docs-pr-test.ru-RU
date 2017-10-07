---
title: "Пример сценария PowerShell - aaaAzure создания виртуальной Машины путем присоединения управляемого диск как диск ОС | Документы Microsoft"
description: "Пример скрипта Azure PowerShell. Создание виртуальной машины путем подключения управляемого диска в качестве диска ОС"
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
ms.openlocfilehash: 8ae5b14df3977a4af91b92692cb925199cfb8058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-powershell"></a><span data-ttu-id="4436e-103">Создание виртуальной машины с помощью существующего управляемого диска ОС с использованием PowerShell</span><span class="sxs-lookup"><span data-stu-id="4436e-103">Create a virtual machine using an existing managed OS disk with PowerShell</span></span>

<span data-ttu-id="4436e-104">Этот скрипт создает виртуальную машину путем подключения существующего управляемого диска как диска ОС.</span><span class="sxs-lookup"><span data-stu-id="4436e-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="4436e-105">Используйте этот скрипт в таких сценариях:</span><span class="sxs-lookup"><span data-stu-id="4436e-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="4436e-106">создание виртуальной машины из существующего управляемого диска ОС, скопированного из управляемого диска в другой подписке;</span><span class="sxs-lookup"><span data-stu-id="4436e-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="4436e-107">создание виртуальной машины из существующего управляемого диска, который был создан из специального файла VHD;</span><span class="sxs-lookup"><span data-stu-id="4436e-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="4436e-108">создание виртуальной машины из существующего управляемого диска ОС, который был создан из моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="4436e-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="4436e-109">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="4436e-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from snapshot")]

## <a name="clean-up-deployment"></a><span data-ttu-id="4436e-110">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="4436e-110">Clean up deployment</span></span> 

<span data-ttu-id="4436e-111">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="4436e-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="4436e-112">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="4436e-112">Script explanation</span></span>

<span data-ttu-id="4436e-113">Этот скрипт использует следующие свойства диска tooget управляемых команды hello, присоединить tooa управляемого диска новой виртуальной Машины и создание виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="4436e-113">This script uses hello following commands tooget managed disk properties, attach a managed disk tooa new VM and create a VM.</span></span> <span data-ttu-id="4436e-114">Каждый элемент в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="4436e-114">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4436e-115">Команда</span><span class="sxs-lookup"><span data-stu-id="4436e-115">Command</span></span> | <span data-ttu-id="4436e-116">Примечания</span><span class="sxs-lookup"><span data-stu-id="4436e-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4436e-117">Get-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="4436e-117">Get-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/Get-AzureRmDisk) | <span data-ttu-id="4436e-118">Возвращает объект диска, на основе имени hello и группы ресурсов hello диска.</span><span class="sxs-lookup"><span data-stu-id="4436e-118">Gets disk object based on hello name and hello resource group of a disk.</span></span> <span data-ttu-id="4436e-119">Свойство идентификатора hello возвращается объект диска используется tooattach hello диск tooa новой виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="4436e-119">Id property of hello returned disk object is used tooattach hello disk tooa new VM</span></span> |
| [<span data-ttu-id="4436e-120">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="4436e-120">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="4436e-121">Создает конфигурацию виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="4436e-121">Creates a VM configuration.</span></span> <span data-ttu-id="4436e-122">Эта конфигурация включает в себя такие сведения, как имя виртуальной машины, операционную систему и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="4436e-122">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="4436e-123">Конфигурация Hello используется во время создания виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="4436e-123">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="4436e-124">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="4436e-124">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmosdisk) | <span data-ttu-id="4436e-125">Присоединяет управляемого диска с помощью свойства Id hello hello диск как ОС диска tooa новой виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="4436e-125">Attaches a managed disk using hello Id property of hello disk as OS disk tooa new virtual machine</span></span> |
| [<span data-ttu-id="4436e-126">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="4436e-126">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="4436e-127">Создает общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="4436e-127">Creates a public IP address.</span></span> |
| [<span data-ttu-id="4436e-128">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="4436e-128">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="4436e-129">Создает сетевой интерфейс.</span><span class="sxs-lookup"><span data-stu-id="4436e-129">Creates a network interface.</span></span> |
| [<span data-ttu-id="4436e-130">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="4436e-130">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="4436e-131">Создайте виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="4436e-131">Create a virtual machine.</span></span> |
|[<span data-ttu-id="4436e-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4436e-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="4436e-133">Удаляет группу ресурсов и все ресурсы, содержащиеся в ней.</span><span class="sxs-lookup"><span data-stu-id="4436e-133">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4436e-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4436e-134">Next steps</span></span>

<span data-ttu-id="4436e-135">Дополнительные сведения о hello модуля Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4436e-135">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="4436e-136">Примеры сценариев PowerShell дополнительную виртуальную машину можно найти в hello [документации виртуальной Машины Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4436e-136">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
