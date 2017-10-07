---
title: "aaaAzure образец скрипта PowerShell - toosame диски или другой подписке управляемых копии (перемещения) | Документы Microsoft"
description: "Azure образец скрипта PowerShell - toosame дисков управляемых копии (перемещения) или другой подписке"
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
ms.openlocfilehash: 22e19a47228cbf628bebebd73012b8aa7baf073c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-in-hello-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="3a7f7-103">Копировать управляемых жестких дисков в hello таким же или разных подписка с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="3a7f7-103">Copy managed disks in hello same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="3a7f7-104">Этот скрипт создает копию существующего управляемого диска в hello одной подписке или другую подписку.</span><span class="sxs-lookup"><span data-stu-id="3a7f7-104">This script creates a copy of an existing managed disk in hello same subscription or different subscription.</span></span> <span data-ttu-id="3a7f7-105">Hello создается новый диск в hello же регионе, что и родительский hello управляемого диска.</span><span class="sxs-lookup"><span data-stu-id="3a7f7-105">hello new disk is created in hello same region as hello parent managed disk.</span></span>   

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="3a7f7-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="3a7f7-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.ps1 "Copy managed disk")]


## <a name="script-explanation"></a><span data-ttu-id="3a7f7-107">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="3a7f7-107">Script explanation</span></span>

<span data-ttu-id="3a7f7-108">Этот скрипт использует следующую команды toocreate нового управляемого диска в hello целевой подписки с помощью hello идентификатор источника hello управляемого диска.</span><span class="sxs-lookup"><span data-stu-id="3a7f7-108">This script uses following commands toocreate a new managed disk in hello target subscription using hello Id of hello source managed disk.</span></span> <span data-ttu-id="3a7f7-109">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="3a7f7-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3a7f7-110">Команда</span><span class="sxs-lookup"><span data-stu-id="3a7f7-110">Command</span></span> | <span data-ttu-id="3a7f7-111">Примечания</span><span class="sxs-lookup"><span data-stu-id="3a7f7-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3a7f7-112">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="3a7f7-112">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="3a7f7-113">Создает конфигурацию диска, которая используется для создания диска.</span><span class="sxs-lookup"><span data-stu-id="3a7f7-113">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="3a7f7-114">Он включает hello ресурсов идентификатор hello родительский диск и расположение, в то же, что расположение hello родительского диска.</span><span class="sxs-lookup"><span data-stu-id="3a7f7-114">It includes hello resource Id of hello parent disk and location that is same as hello location of parent disk.</span></span>  |
| [<span data-ttu-id="3a7f7-115">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="3a7f7-115">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="3a7f7-116">Создает диск с помощью конфигурации диска, имени диска и имени группы ресурсов, которые передаются в качестве параметров.</span><span class="sxs-lookup"><span data-stu-id="3a7f7-116">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="3a7f7-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3a7f7-117">Next steps</span></span>

[<span data-ttu-id="3a7f7-118">Создание виртуальной машины на основе управляемого диска</span><span class="sxs-lookup"><span data-stu-id="3a7f7-118">Create a virtual machine from a managed disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="3a7f7-119">Дополнительные сведения о hello модуля Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3a7f7-119">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="3a7f7-120">Примеры сценариев PowerShell дополнительную виртуальную машину можно найти в hello [документации виртуальной Машины Windows Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3a7f7-120">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
