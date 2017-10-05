---
title: "Пример сценария Azure PowerShell. Копирование (перемещение) моментального снимка управляемого диска в ту же или другую подписку | Документация Майкрософт"
description: "Пример сценария Azure PowerShell для копирования (перемещения) моментального снимка управляемого диска в ту же или другую подписку."
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
ms.openlocfilehash: f7b4869669a2c5e840f9bd384dcd6d6096ba58e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="copy-snapshot-of-a-managed-disk-in-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="2e7c0-103">Копирование моментального снимка управляемого диска в ту же или другую подписку с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e7c0-103">Copy snapshot of a managed disk in same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="2e7c0-104">Этот сценарий создает копию моментального снимка в той же или в другой подписке.</span><span class="sxs-lookup"><span data-stu-id="2e7c0-104">This script creates a copy of a snapshot in the same same subscription or different subscription.</span></span> <span data-ttu-id="2e7c0-105">Используйте этот сценарий, чтобы переместить моментальный снимок в другую подписку для хранения данных.</span><span class="sxs-lookup"><span data-stu-id="2e7c0-105">Use this script to move a snapshot to different subscription for data retention.</span></span> <span data-ttu-id="2e7c0-106">Хранение моментальных снимков в другой подписке защитит вас от случайного удаления моментальных снимков в основной подписке.</span><span class="sxs-lookup"><span data-stu-id="2e7c0-106">Storing snapshots in different subscription protect you from accidental deletion of snapshots in your main subscription.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="2e7c0-107">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="2e7c0-107">Sample script</span></span>

<span data-ttu-id="2e7c0-108">[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "Копирование моментального снимка")]</span><span class="sxs-lookup"><span data-stu-id="2e7c0-108">[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="2e7c0-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="2e7c0-109">Script explanation</span></span>

<span data-ttu-id="2e7c0-110">Этот сценарий использует приведенные ниже команды для создания моментального снимка в целевой подписке с помощью идентификатора исходного моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="2e7c0-110">This script uses following commands to create a snapshot in the target subscription using the Id of the source snapshot.</span></span> <span data-ttu-id="2e7c0-111">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="2e7c0-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="2e7c0-112">Команда</span><span class="sxs-lookup"><span data-stu-id="2e7c0-112">Command</span></span> | <span data-ttu-id="2e7c0-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="2e7c0-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2e7c0-114">New-AzureRmSnapshotConfig</span><span class="sxs-lookup"><span data-stu-id="2e7c0-114">New-AzureRmSnapshotConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmSnapshotConfig) | <span data-ttu-id="2e7c0-115">Создает конфигурацию моментального снимка, используемую для создания моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="2e7c0-115">Creates snapshot configuration that is used for snapshot creation.</span></span> <span data-ttu-id="2e7c0-116">Она содержит идентификатор ресурса родительского моментального снимка и расположение, которое совпадает с расположением родительского моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="2e7c0-116">It includes the resource Id of the parent snapshot and location that is same as the parent snapshot.</span></span>  |
| [<span data-ttu-id="2e7c0-117">New-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="2e7c0-117">New-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="2e7c0-118">Создает моментальный снимок с помощью конфигурации моментального снимка, имени моментального снимка и имени группы ресурсов, которые передаются в качестве параметров.</span><span class="sxs-lookup"><span data-stu-id="2e7c0-118">Creates a snapshot using snapshot configuration, snapshot name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="2e7c0-119">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2e7c0-119">Next steps</span></span>

[<span data-ttu-id="2e7c0-120">Создание виртуальной машины на основе моментального снимка</span><span class="sxs-lookup"><span data-stu-id="2e7c0-120">Create a virtual machine from a snapshot</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="2e7c0-121">Дополнительные сведения о модуле Azure PowerShell см. в [документации по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2e7c0-121">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="2e7c0-122">Дополнительные примеры сценариев PowerShell для виртуальных машин представлены в [документации по виртуальным машинам Azure под управлением Windows](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2e7c0-122">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>