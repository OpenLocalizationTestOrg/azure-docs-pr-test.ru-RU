---
title: "Пример сценария Azure PowerShell. Создание моментального снимка из VHD для быстрого создания нескольких идентичных управляемых дисков | Документация Майкрософт"
description: "Пример сценария Azure PowerShell для создания моментального снимка из VHD для быстрого создания нескольких идентичных управляемых дисков."
services: virtual-machines-windows
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/05/2017
ms.author: ramankum
ms.openlocfilehash: 02a69abd6c17ce765996379309e22afad82c4e10
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-snapshot-from-a-vhd-to-create-multiple-identical-managed-disks-in-small-amount-of-time-with-powershell"></a><span data-ttu-id="2fca6-103">Создание моментального снимка из VHD для быстрого создания нескольких идентичных управляемых дисков с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="2fca6-103">Create a snapshot from a VHD to create multiple identical managed disks in small amount of time with PowerShell</span></span>

<span data-ttu-id="2fca6-104">Этот сценарий создает моментальный снимок из VHD-файла в учетной записи хранения в той же или другой подписке.</span><span class="sxs-lookup"><span data-stu-id="2fca6-104">This script creates a snapshot from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="2fca6-105">Этот сценарий можно использовать, чтобы импортировать специализированный (не универсальный и не подготовленный командой Sysprep) VHD в моментальный снимок, затем с помощью этого моментального снимка создать несколько идентичных управляемых дисков за короткий промежуток времени.</span><span class="sxs-lookup"><span data-stu-id="2fca6-105">Use this script to import a specialized (not generalized/sysprepped) VHD to a snapshot and then use the snapshot to create multiple identical managed disks in small amount of time.</span></span> <span data-ttu-id="2fca6-106">Кроме того, с его помощью можно импортировать VHD данных в моментальный снимок, а затем использовать этот моментальный снимок для быстрого создания нескольких управляемых дисков.</span><span class="sxs-lookup"><span data-stu-id="2fca6-106">Also, use it to import a data VHD to a snapshot and then use the snapshot to create multiple managed disks in small amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="2fca6-107">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="2fca6-107">Sample script</span></span>

<span data-ttu-id="2fca6-108">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "Создание моментального снимка из VHD")]</span><span class="sxs-lookup"><span data-stu-id="2fca6-108">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "Create snapshot from VHD")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="2fca6-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="2fca6-109">Script explanation</span></span>

<span data-ttu-id="2fca6-110">Этот сценарий использует приведенные ниже команды для создания управляемого диска на основе VHD.</span><span class="sxs-lookup"><span data-stu-id="2fca6-110">This script uses following commands to create a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="2fca6-111">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="2fca6-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="2fca6-112">Команда</span><span class="sxs-lookup"><span data-stu-id="2fca6-112">Command</span></span> | <span data-ttu-id="2fca6-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="2fca6-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2fca6-114">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="2fca6-114">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="2fca6-115">Создает конфигурацию диска, которая используется для создания диска.</span><span class="sxs-lookup"><span data-stu-id="2fca6-115">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="2fca6-116">Она содержит тип хранилища, расположение, идентификатор ресурса учетной записи хранения, в которой хранится родительский VHD, и универсальный код ресурса (URI) родительского VHD.</span><span class="sxs-lookup"><span data-stu-id="2fca6-116">It includes storage type, location, resource Id of the storage account where the parent VHD is stored, and VHD URI of the parent VHD.</span></span> |
| [<span data-ttu-id="2fca6-117">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="2fca6-117">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="2fca6-118">Создает диск с помощью конфигурации диска, имени диска и имени группы ресурсов, которые передаются в качестве параметров.</span><span class="sxs-lookup"><span data-stu-id="2fca6-118">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2fca6-119">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2fca6-119">Next steps</span></span>

[<span data-ttu-id="2fca6-120">Создание управляемого диска из моментального снимка</span><span class="sxs-lookup"><span data-stu-id="2fca6-120">Create a managed disk from snapshot</span></span>](virtual-machines-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)


[<span data-ttu-id="2fca6-121">Создание виртуальной машины путем подключения управляемого диска как диска ОС</span><span class="sxs-lookup"><span data-stu-id="2fca6-121">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="2fca6-122">Дополнительные сведения о модуле Azure PowerShell см. в [документации по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2fca6-122">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="2fca6-123">Дополнительные примеры сценариев PowerShell для виртуальных машин представлены в [документации по виртуальным машинам Azure под управлением Windows](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2fca6-123">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>