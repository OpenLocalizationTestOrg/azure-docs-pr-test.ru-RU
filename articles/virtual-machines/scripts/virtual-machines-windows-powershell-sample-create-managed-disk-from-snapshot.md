---
title: "Пример сценария PowerShell - aaaAzure создания управляемой дисковой из моментального снимка | Документы Microsoft"
description: "Пример сценария Azure PowerShell для создания управляемого диска из моментального снимка."
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
ms.openlocfilehash: b99413b4c3e9a662a5fef74b7e4aeb5ecbb26af4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-powershell"></a><span data-ttu-id="a39fb-103">Создание управляемого диска из моментального снимка с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="a39fb-103">Create a managed disk from a snapshot with PowerShell</span></span>

<span data-ttu-id="a39fb-104">Этот сценарий создает управляемый диск на основе моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="a39fb-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="a39fb-105">Используйте toorestore виртуальную машину из моментальных снимков дисков операционной системы и данных.</span><span class="sxs-lookup"><span data-stu-id="a39fb-105">Use it toorestore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="a39fb-106">Можно создать управляемые диски данных и ОС на основе соответствующих моментальных снимков, а затем создать виртуальную машину, подключив эти управляемые диски.</span><span class="sxs-lookup"><span data-stu-id="a39fb-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="a39fb-107">Кроме того, вы можете восстановить диски данных существующей виртуальной машины, подключив диски данных, созданные из моментальных снимков.</span><span class="sxs-lookup"><span data-stu-id="a39fb-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a39fb-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="a39fb-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-managed-disk-from-snapshot/create-managed-disk-from-snapshot.ps1 "Create managed disk from snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="a39fb-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="a39fb-109">Script explanation</span></span>

<span data-ttu-id="a39fb-110">Этот скрипт использует следующие команды toocreate управляемого диска из моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="a39fb-110">This script uses following commands toocreate a managed disk from a snapshot.</span></span> <span data-ttu-id="a39fb-111">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="a39fb-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a39fb-112">Команда</span><span class="sxs-lookup"><span data-stu-id="a39fb-112">Command</span></span> | <span data-ttu-id="a39fb-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="a39fb-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a39fb-114">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="a39fb-114">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/Get-AzureRmSnapshot) | <span data-ttu-id="a39fb-115">Возвращает свойства моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="a39fb-115">Gets snapshot properties.</span></span>  |
| [<span data-ttu-id="a39fb-116">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="a39fb-116">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="a39fb-117">Создает конфигурацию диска, которая используется для создания диска.</span><span class="sxs-lookup"><span data-stu-id="a39fb-117">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="a39fb-118">Он содержит идентификатор родительского снимка hello, расположение, то же, что расположение hello родительский тип хранилища моментальных снимков и hello hello ресурса.</span><span class="sxs-lookup"><span data-stu-id="a39fb-118">It includes hello resource Id of hello parent snapshot, location that is same as hello location of parent snapshot and hello storage type.</span></span>  |
| [<span data-ttu-id="a39fb-119">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="a39fb-119">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="a39fb-120">Создает диск с помощью конфигурации диска, имени диска и имени группы ресурсов, которые передаются в качестве параметров.</span><span class="sxs-lookup"><span data-stu-id="a39fb-120">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="a39fb-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a39fb-121">Next steps</span></span>

[<span data-ttu-id="a39fb-122">Создание виртуальной машины на основе управляемого диска</span><span class="sxs-lookup"><span data-stu-id="a39fb-122">Create a virtual machine from a managed disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="a39fb-123">Дополнительные сведения о hello модуля Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a39fb-123">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="a39fb-124">Примеры сценариев PowerShell дополнительную виртуальную машину можно найти в hello [документации виртуальной Машины Windows Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a39fb-124">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
