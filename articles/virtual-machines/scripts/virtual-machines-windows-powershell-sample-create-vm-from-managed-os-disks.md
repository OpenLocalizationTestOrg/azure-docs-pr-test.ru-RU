---
title: "Пример скрипта Azure PowerShell. Создание виртуальной машины путем подключения управляемого диска в качестве диска ОС | Документация Майкрософт"
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
ms.openlocfilehash: ec532811e94647c8a04b9faf9474f6749969f83e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-powershell"></a><span data-ttu-id="a749a-103">Создание виртуальной машины с помощью существующего управляемого диска ОС с использованием PowerShell</span><span class="sxs-lookup"><span data-stu-id="a749a-103">Create a virtual machine using an existing managed OS disk with PowerShell</span></span>

<span data-ttu-id="a749a-104">Этот скрипт создает виртуальную машину путем подключения существующего управляемого диска как диска ОС.</span><span class="sxs-lookup"><span data-stu-id="a749a-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="a749a-105">Используйте этот скрипт в таких сценариях:</span><span class="sxs-lookup"><span data-stu-id="a749a-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="a749a-106">создание виртуальной машины из существующего управляемого диска ОС, скопированного из управляемого диска в другой подписке;</span><span class="sxs-lookup"><span data-stu-id="a749a-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="a749a-107">создание виртуальной машины из существующего управляемого диска, который был создан из специального файла VHD;</span><span class="sxs-lookup"><span data-stu-id="a749a-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="a749a-108">создание виртуальной машины из существующего управляемого диска ОС, который был создан из моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="a749a-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a749a-109">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="a749a-109">Sample script</span></span>

<span data-ttu-id="a749a-110">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Создание виртуальной машины из моментального снимка")]</span><span class="sxs-lookup"><span data-stu-id="a749a-110">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from snapshot")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="a749a-111">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="a749a-111">Clean up deployment</span></span> 

<span data-ttu-id="a749a-112">Выполните следующую команду, чтобы удалить группу ресурсов, виртуальную машину и все связанные с ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="a749a-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="a749a-113">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="a749a-113">Script explanation</span></span>

<span data-ttu-id="a749a-114">Этот скрипт использует следующие команды для получения свойств управляемого диска, его подключения к новой виртуальной машине и создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a749a-114">This script uses the following commands to get managed disk properties, attach a managed disk to a new VM and create a VM.</span></span> <span data-ttu-id="a749a-115">Для каждого элемента в таблице приведены ссылки на документацию по команде.</span><span class="sxs-lookup"><span data-stu-id="a749a-115">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a749a-116">Команда</span><span class="sxs-lookup"><span data-stu-id="a749a-116">Command</span></span> | <span data-ttu-id="a749a-117">Примечания</span><span class="sxs-lookup"><span data-stu-id="a749a-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a749a-118">Get-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="a749a-118">Get-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/Get-AzureRmDisk) | <span data-ttu-id="a749a-119">Возвращает объект диска на основе имени и группы ресурсов диска.</span><span class="sxs-lookup"><span data-stu-id="a749a-119">Gets disk object based on the name and the resource group of a disk.</span></span> <span data-ttu-id="a749a-120">Свойство идентификатора возвращенного объекта диска используется для подключения диска к новой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="a749a-120">Id property of the returned disk object is used to attach the disk to a new VM</span></span> |
| [<span data-ttu-id="a749a-121">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="a749a-121">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="a749a-122">Создает конфигурацию виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a749a-122">Creates a VM configuration.</span></span> <span data-ttu-id="a749a-123">Эта конфигурация включает в себя такие сведения, как имя виртуальной машины, операционную систему и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="a749a-123">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="a749a-124">Данная конфигурации используется при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a749a-124">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="a749a-125">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="a749a-125">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmosdisk) | <span data-ttu-id="a749a-126">Подключает управляемый диск, используя свойство идентификатора диска как диск ОС для новой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a749a-126">Attaches a managed disk using the Id property of the disk as OS disk to a new virtual machine</span></span> |
| [<span data-ttu-id="a749a-127">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="a749a-127">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="a749a-128">Создает общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="a749a-128">Creates a public IP address.</span></span> |
| [<span data-ttu-id="a749a-129">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="a749a-129">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="a749a-130">Создает сетевой интерфейс.</span><span class="sxs-lookup"><span data-stu-id="a749a-130">Creates a network interface.</span></span> |
| [<span data-ttu-id="a749a-131">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="a749a-131">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="a749a-132">Создайте виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="a749a-132">Create a virtual machine.</span></span> |
|[<span data-ttu-id="a749a-133">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a749a-133">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="a749a-134">Удаляет группу ресурсов и все ресурсы, содержащиеся в ней.</span><span class="sxs-lookup"><span data-stu-id="a749a-134">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a749a-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a749a-135">Next steps</span></span>

<span data-ttu-id="a749a-136">Дополнительные сведения о модуле Azure PowerShell см. в [документации по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a749a-136">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="a749a-137">Дополнительные примеры сценариев PowerShell для виртуальных машин представлены в [документации по виртуальным машинам Azure под управлением Windows](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a749a-137">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>