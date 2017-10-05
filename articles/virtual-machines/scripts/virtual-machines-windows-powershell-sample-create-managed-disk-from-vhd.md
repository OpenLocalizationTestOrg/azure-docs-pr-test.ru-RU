---
title: "Пример сценария Azure PowerShell. Создание управляемого диска из VHD-файла в учетной записи хранения в той же или другой подписке | Документация Майкрософт"
description: "Пример сценария Azure PowerShell для создания управляемого диска из VHD-файла в учетной записи хранения в той же или другой подписке."
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
ms.openlocfilehash: 728def40a3eb132537decbd099fa71f4544c6b87
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-same-or-different-subscription-with-powershell"></a><span data-ttu-id="05c92-103">Создание управляемого диска из VHD-файла в учетной записи хранения в той же или другой подписке с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="05c92-103">Create a managed disk from a VHD file in a storage account in same or different subscription with PowerShell</span></span>

<span data-ttu-id="05c92-104">Этот сценарий создает управляемый диск на основе VHD-файла в учетной записи хранения в той же или другой подписке.</span><span class="sxs-lookup"><span data-stu-id="05c92-104">This script creates a managed disk from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="05c92-105">Этот сценарий можно использовать, чтобы импортировать специализированный (не универсальный и не подготовленный командой Sysprep) VHD в управляемый диск ОС для создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="05c92-105">Use this script to import a specialized (not generalized/sysprepped) VHD to managed OS disk to create a virtual machine.</span></span> <span data-ttu-id="05c92-106">Кроме того, с его помощью можно импортировать VHD данных в управляемый диск данных.</span><span class="sxs-lookup"><span data-stu-id="05c92-106">Also, use it to import a data VHD to managed data disk.</span></span> 

<span data-ttu-id="05c92-107">Не создавайте несколько идентичных управляемых дисков из VHD-файла за небольшой промежуток времени.</span><span class="sxs-lookup"><span data-stu-id="05c92-107">Don't create multiple identical managed disks from a VHD file in small amount of time.</span></span> <span data-ttu-id="05c92-108">При создании управляемых дисков из VHD-файла создается моментальный снимок большого двоичного объекта VHD-файла, который затем используется для этой операции.</span><span class="sxs-lookup"><span data-stu-id="05c92-108">To create managed disks from a vhd file, blob snapshot of the vhd file is created and then it is used to create managed disks.</span></span> <span data-ttu-id="05c92-109">За минуту может быть создан только один большой двоичный объект, что приводит к сбоям при создании дисков из-за регулирования.</span><span class="sxs-lookup"><span data-stu-id="05c92-109">Only one blob snapshot can be created in a minute that causes disk creation failures due to throttling.</span></span> <span data-ttu-id="05c92-110">Во избежание этого регулирования создайте [управляемый моментальный снимок из VHD-файла](virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json), а затем используйте его для создания нескольких управляемых дисков за короткий промежуток времени.</span><span class="sxs-lookup"><span data-stu-id="05c92-110">To avoid this throttling, create a [managed snapshot from the vhd file](virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) and then use the managed snapshot to create multiple managed disks in short amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="05c92-111">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="05c92-111">Sample script</span></span>

<span data-ttu-id="05c92-112">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "Создание управляемого диска на основе VHD")]</span><span class="sxs-lookup"><span data-stu-id="05c92-112">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "Create managed disk from VHD")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="05c92-113">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="05c92-113">Script explanation</span></span>

<span data-ttu-id="05c92-114">Этот сценарий использует приведенные ниже команды для создания управляемого диска на основе VHD.</span><span class="sxs-lookup"><span data-stu-id="05c92-114">This script uses following commands to create a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="05c92-115">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="05c92-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="05c92-116">Команда</span><span class="sxs-lookup"><span data-stu-id="05c92-116">Command</span></span> | <span data-ttu-id="05c92-117">Примечания</span><span class="sxs-lookup"><span data-stu-id="05c92-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="05c92-118">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="05c92-118">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="05c92-119">Создает конфигурацию диска, которая используется для создания диска.</span><span class="sxs-lookup"><span data-stu-id="05c92-119">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="05c92-120">Она содержит тип хранилища, расположение, идентификатор ресурса учетной записи хранения, в которой хранится родительский VHD, и универсальный код ресурса (URI) родительского VHD.</span><span class="sxs-lookup"><span data-stu-id="05c92-120">It includes storage type, location, resource Id of the storage account where the parent VHD is stored, VHD URI of the parent VHD.</span></span> |
| [<span data-ttu-id="05c92-121">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="05c92-121">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="05c92-122">Создает диск с помощью конфигурации диска, имени диска и имени группы ресурсов, которые передаются в качестве параметров.</span><span class="sxs-lookup"><span data-stu-id="05c92-122">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="05c92-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="05c92-123">Next steps</span></span>

[<span data-ttu-id="05c92-124">Создание виртуальной машины путем подключения управляемого диска как диска ОС</span><span class="sxs-lookup"><span data-stu-id="05c92-124">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="05c92-125">Дополнительные сведения о модуле Azure PowerShell см. в [документации по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="05c92-125">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="05c92-126">Дополнительные примеры сценариев PowerShell для виртуальных машин представлены в [документации по виртуальным машинам Azure под управлением Windows](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="05c92-126">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>