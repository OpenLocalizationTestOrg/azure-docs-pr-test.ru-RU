---
title: "Пример сценария PowerShell - Экспорт копирования моментальных снимков с учетной записью хранения tooa VHD в другом регионе aaaAzure | Документы Microsoft"
description: "Azure образец скрипта PowerShell - Экспорт копирования моментальных снимков с учетной записью хранения tooa VHD в одном другом регионе"
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
ms.openlocfilehash: 3b3e38c6b06bfa1e117f4e913dfc09443a795196
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-powershell"></a><span data-ttu-id="e5d82-103">Экспорт» или «копировать управляемый снимки с учетной записью хранения tooa VHD в другом регионе с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="e5d82-103">Export/Copy managed snapshots as VHD tooa storage account in different region with PowerShell</span></span>

<span data-ttu-id="e5d82-104">Этот сценарий экспортирует учетную запись хранения tooa управляемого моментального снимка в другом регионе.</span><span class="sxs-lookup"><span data-stu-id="e5d82-104">This script exports a managed snapshot tooa storage account in different region.</span></span> <span data-ttu-id="e5d82-105">Сначала генерации hello универсальный код Ресурса SAS hello моментальных снимков и использует его toocopy его tooa учетной записи хранилища в другом регионе.</span><span class="sxs-lookup"><span data-stu-id="e5d82-105">It first generates hello SAS URI of hello snapshot and then uses it toocopy it tooa storage account in different region.</span></span> <span data-ttu-id="e5d82-106">Используйте эту резервную копию toomaintain сценария управляемого диски в другом регионе для аварийного восстановления.</span><span class="sxs-lookup"><span data-stu-id="e5d82-106">Use this script toomaintain backup of your managed disks in different region for disaster recovery.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e5d82-107">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="e5d82-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/copy-snapshot-to-storage-account/copy-snapshot-to-storage-account.ps1 "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="e5d82-108">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="e5d82-108">Script explanation</span></span>

<span data-ttu-id="e5d82-109">Этот скрипт использует следующую toogenerate команды универсальный код Ресурса SAS для управляемых hello моментального снимка и копий моментальных снимков tooa учетной записи хранилища с помощью универсального кода Ресурса SAS.</span><span class="sxs-lookup"><span data-stu-id="e5d82-109">This script uses following commands toogenerate SAS URI for a managed snapshot and copies hello snapshot tooa storage account using SAS URI.</span></span> <span data-ttu-id="e5d82-110">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="e5d82-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e5d82-111">Команда</span><span class="sxs-lookup"><span data-stu-id="e5d82-111">Command</span></span> | <span data-ttu-id="e5d82-112">Примечания</span><span class="sxs-lookup"><span data-stu-id="e5d82-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e5d82-113">Grant-AzureRmSnapshotAccess</span><span class="sxs-lookup"><span data-stu-id="e5d82-113">Grant-AzureRmSnapshotAccess</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="e5d82-114">Создает универсальный код Ресурса SAS для снимок, который используется toocopy его tooa учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="e5d82-114">Generates SAS URI for a snapshot that is used toocopy it tooa storage account.</span></span> |
| [<span data-ttu-id="e5d82-115">New-AzureStorageContext</span><span class="sxs-lookup"><span data-stu-id="e5d82-115">New-AzureStorageContext</span></span>](/powershell/module/azure.storage/New-AzureStorageContext) | <span data-ttu-id="e5d82-116">Создает контекст учетной записи хранилища с помощью hello имя учетной записи и ключа.</span><span class="sxs-lookup"><span data-stu-id="e5d82-116">Creates a storage account context using hello account name and key.</span></span> <span data-ttu-id="e5d82-117">Этот контекст может быть используется tooperform операций чтения и записи на учетную запись хранения hello.</span><span class="sxs-lookup"><span data-stu-id="e5d82-117">This context can be used tooperform read/write operations on hello storage account.</span></span> |
| [<span data-ttu-id="e5d82-118">Start-AzureStorageBlobCopy</span><span class="sxs-lookup"><span data-stu-id="e5d82-118">Start-AzureStorageBlobCopy</span></span>](/powershell/module/azure.storage/Start-AzureStorageBlobCopy) | <span data-ttu-id="e5d82-119">Здравствуйте, копии базового VHD учетной записи хранения tooa моментальных снимков</span><span class="sxs-lookup"><span data-stu-id="e5d82-119">Copies hello underlying VHD of a snapshot tooa storage account</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e5d82-120">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e5d82-120">Next steps</span></span>

[<span data-ttu-id="e5d82-121">Создание управляемого диска на основе VHD</span><span class="sxs-lookup"><span data-stu-id="e5d82-121">Create a managed disk from a VHD</span></span>](./../scripts/storage-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json)

[<span data-ttu-id="e5d82-122">Создание виртуальной машины на основе управляемого диска</span><span class="sxs-lookup"><span data-stu-id="e5d82-122">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="e5d82-123">Дополнительные сведения о hello модуля Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e5d82-123">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="e5d82-124">Примеры сценариев PowerShell дополнительную виртуальную машину можно найти в hello [документации виртуальной Машины Windows Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e5d82-124">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
