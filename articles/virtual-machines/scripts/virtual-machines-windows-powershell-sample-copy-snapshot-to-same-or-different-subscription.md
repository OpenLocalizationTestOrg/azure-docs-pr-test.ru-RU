---
title: "Пример сценария PowerShell - копии (перемещения) снимок toosame управляемого диска или другой подписке aaaAzure | Документы Microsoft"
description: "Azure образец скрипта PowerShell - копии (перемещения) снимок toosame управляемого диска или другой подписке"
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
ms.date: 06/06/2017
ms.author: ramankum
ms.openlocfilehash: d7b8a71cc09d1950271f472e89b95bb551323be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-in-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="556af-103">Копирование моментального снимка управляемого диска в ту же или другую подписку с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="556af-103">Copy snapshot of a managed disk in same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="556af-104">Этот скрипт создает копию этого моментального снимка в hello же одной подписке или другую подписку.</span><span class="sxs-lookup"><span data-stu-id="556af-104">This script creates a copy of a snapshot in hello same same subscription or different subscription.</span></span> <span data-ttu-id="556af-105">Используйте этот скрипт toomove toodifferent подписки на моментальные снимки для хранения данных.</span><span class="sxs-lookup"><span data-stu-id="556af-105">Use this script toomove a snapshot toodifferent subscription for data retention.</span></span> <span data-ttu-id="556af-106">Хранение моментальных снимков в другой подписке защитит вас от случайного удаления моментальных снимков в основной подписке.</span><span class="sxs-lookup"><span data-stu-id="556af-106">Storing snapshots in different subscription protect you from accidental deletion of snapshots in your main subscription.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="556af-107">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="556af-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="556af-108">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="556af-108">Script explanation</span></span>

<span data-ttu-id="556af-109">Этот скрипт использует следующую toocreate команд моментального снимка в hello целевой подписки с помощью hello идентификатор моментального снимка источника hello.</span><span class="sxs-lookup"><span data-stu-id="556af-109">This script uses following commands toocreate a snapshot in hello target subscription using hello Id of hello source snapshot.</span></span> <span data-ttu-id="556af-110">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="556af-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="556af-111">Команда</span><span class="sxs-lookup"><span data-stu-id="556af-111">Command</span></span> | <span data-ttu-id="556af-112">Примечания</span><span class="sxs-lookup"><span data-stu-id="556af-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="556af-113">New-AzureRmSnapshotConfig</span><span class="sxs-lookup"><span data-stu-id="556af-113">New-AzureRmSnapshotConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmSnapshotConfig) | <span data-ttu-id="556af-114">Создает конфигурацию моментального снимка, используемую для создания моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="556af-114">Creates snapshot configuration that is used for snapshot creation.</span></span> <span data-ttu-id="556af-115">Он содержит идентификатор родительского снимка hello и расположение, которое совпадает с родительского снимка hello hello ресурса.</span><span class="sxs-lookup"><span data-stu-id="556af-115">It includes hello resource Id of hello parent snapshot and location that is same as hello parent snapshot.</span></span>  |
| [<span data-ttu-id="556af-116">New-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="556af-116">New-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="556af-117">Создает моментальный снимок с помощью конфигурации моментального снимка, имени моментального снимка и имени группы ресурсов, которые передаются в качестве параметров.</span><span class="sxs-lookup"><span data-stu-id="556af-117">Creates a snapshot using snapshot configuration, snapshot name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="556af-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="556af-118">Next steps</span></span>

[<span data-ttu-id="556af-119">Создание виртуальной машины на основе моментального снимка</span><span class="sxs-lookup"><span data-stu-id="556af-119">Create a virtual machine from a snapshot</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="556af-120">Дополнительные сведения о hello модуля Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="556af-120">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="556af-121">Примеры сценариев PowerShell дополнительную виртуальную машину можно найти в hello [документации виртуальной Машины Windows Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="556af-121">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
