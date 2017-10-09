---
title: "aaaAzure образец скрипта PowerShell - создание моментального снимка из VHD toocreate несколько идентичных управляемых дисков в небольшой промежуток времени | Документы Microsoft"
description: "Сценарий Azure PowerShell пример — создание моментального снимка из VHD toocreate несколько идентичных управляемых дисков в небольшой промежуток времени"
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
ms.openlocfilehash: 5f11793b3669df099b6c31dfdbe906c96ba51786
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-snapshot-from-a-vhd-toocreate-multiple-identical-managed-disks-in-small-amount-of-time-with-powershell"></a><span data-ttu-id="8504b-103">Создание моментального снимка из VHD toocreate несколько идентичных управляемых дисков в небольшой промежуток времени с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="8504b-103">Create a snapshot from a VHD toocreate multiple identical managed disks in small amount of time with PowerShell</span></span>

<span data-ttu-id="8504b-104">Этот сценарий создает моментальный снимок из VHD-файла в учетной записи хранения в той же или другой подписке.</span><span class="sxs-lookup"><span data-stu-id="8504b-104">This script creates a snapshot from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="8504b-105">Использовать этот сценарий tooimport моментальный снимок специализированные tooa виртуальный жесткий ДИСК (не обобщенный или командой Sysprep), а затем использовать несколько идентичных дисков управляемого toocreate hello моментального снимка в небольшой промежуток времени.</span><span class="sxs-lookup"><span data-stu-id="8504b-105">Use this script tooimport a specialized (not generalized/sysprepped) VHD tooa snapshot and then use hello snapshot toocreate multiple identical managed disks in small amount of time.</span></span> <span data-ttu-id="8504b-106">Кроме того, используйте моментальный снимок данных виртуального жесткого диска tooa tooimport, а затем использовать несколько дисков, управляемых toocreate hello моментального снимка в небольшой промежуток времени.</span><span class="sxs-lookup"><span data-stu-id="8504b-106">Also, use it tooimport a data VHD tooa snapshot and then use hello snapshot toocreate multiple managed disks in small amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="8504b-107">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="8504b-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "Create snapshot from VHD")]


## <a name="script-explanation"></a><span data-ttu-id="8504b-108">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="8504b-108">Script explanation</span></span>

<span data-ttu-id="8504b-109">Этот скрипт использует следующие команды toocreate управляемого диска из VHD в другую подписку.</span><span class="sxs-lookup"><span data-stu-id="8504b-109">This script uses following commands toocreate a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="8504b-110">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="8504b-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="8504b-111">Команда</span><span class="sxs-lookup"><span data-stu-id="8504b-111">Command</span></span> | <span data-ttu-id="8504b-112">Примечания</span><span class="sxs-lookup"><span data-stu-id="8504b-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8504b-113">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="8504b-113">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="8504b-114">Создает конфигурацию диска, которая используется для создания диска.</span><span class="sxs-lookup"><span data-stu-id="8504b-114">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="8504b-115">Он включает тип хранилища, расположение, идентификатор учетной записи хранилища hello, где хранится hello родительского виртуального жесткого диска ресурса и URI VHD hello родительского виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="8504b-115">It includes storage type, location, resource Id of hello storage account where hello parent VHD is stored, and VHD URI of hello parent VHD.</span></span> |
| [<span data-ttu-id="8504b-116">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="8504b-116">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="8504b-117">Создает диск с помощью конфигурации диска, имени диска и имени группы ресурсов, которые передаются в качестве параметров.</span><span class="sxs-lookup"><span data-stu-id="8504b-117">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8504b-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8504b-118">Next steps</span></span>

[<span data-ttu-id="8504b-119">Создание управляемого диска из моментального снимка</span><span class="sxs-lookup"><span data-stu-id="8504b-119">Create a managed disk from snapshot</span></span>](virtual-machines-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)


[<span data-ttu-id="8504b-120">Создание виртуальной машины путем подключения управляемого диска как диска ОС</span><span class="sxs-lookup"><span data-stu-id="8504b-120">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="8504b-121">Дополнительные сведения о hello модуля Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8504b-121">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="8504b-122">Примеры сценариев PowerShell дополнительную виртуальную машину можно найти в hello [документации виртуальной Машины Windows Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8504b-122">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
