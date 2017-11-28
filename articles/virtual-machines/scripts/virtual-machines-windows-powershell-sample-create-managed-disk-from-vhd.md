---
title: "aaaAzure образец скрипта PowerShell - Создание управляемого диска из VHD-файла в учетную запись хранилища в подписке на одном или разных | Документы Microsoft"
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
ms.openlocfilehash: 47acff274cdf79d6fc3cd685cda01cad3d14ca8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-same-or-different-subscription-with-powershell"></a><span data-ttu-id="80499-103">Создание управляемого диска из VHD-файла в учетной записи хранения в той же или другой подписке с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="80499-103">Create a managed disk from a VHD file in a storage account in same or different subscription with PowerShell</span></span>

<span data-ttu-id="80499-104">Этот сценарий создает управляемый диск на основе VHD-файла в учетной записи хранения в той же или другой подписке.</span><span class="sxs-lookup"><span data-stu-id="80499-104">This script creates a managed disk from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="80499-105">Используйте этот скрипт tooimport специальных (не обобщенный или командой Sysprep) виртуального жесткого диска toomanaged ОС диска toocreate виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="80499-105">Use this script tooimport a specialized (not generalized/sysprepped) VHD toomanaged OS disk toocreate a virtual machine.</span></span> <span data-ttu-id="80499-106">Кроме того используйте tooimport диск данных виртуального жесткого диска toomanaged данных.</span><span class="sxs-lookup"><span data-stu-id="80499-106">Also, use it tooimport a data VHD toomanaged data disk.</span></span> 

<span data-ttu-id="80499-107">Не создавайте несколько идентичных управляемых дисков из VHD-файла за небольшой промежуток времени.</span><span class="sxs-lookup"><span data-stu-id="80499-107">Don't create multiple identical managed disks from a VHD file in small amount of time.</span></span> <span data-ttu-id="80499-108">toocreate управляемых дисков из VHD-файл, создается моментальный снимок большого двоичного объекта hello VHD-файл и будет используется toocreate управляемых дисков.</span><span class="sxs-lookup"><span data-stu-id="80499-108">toocreate managed disks from a vhd file, blob snapshot of hello vhd file is created and then it is used toocreate managed disks.</span></span> <span data-ttu-id="80499-109">Только один большой двоичный объект может быть создано в минуту, которое вызывает сбои при создании диска из-за toothrottling.</span><span class="sxs-lookup"><span data-stu-id="80499-109">Only one blob snapshot can be created in a minute that causes disk creation failures due toothrottling.</span></span> <span data-ttu-id="80499-110">tooavoid повтор, создайте [управляемого моментального снимка из файла виртуального жесткого диска hello](virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) и затем используйте hello управляемых toocreate моментального снимка несколько дисков, управляемых за короткий промежуток времени.</span><span class="sxs-lookup"><span data-stu-id="80499-110">tooavoid this throttling, create a [managed snapshot from hello vhd file](virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) and then use hello managed snapshot toocreate multiple managed disks in short amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="80499-111">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="80499-111">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "Create managed disk from VHD")]


## <a name="script-explanation"></a><span data-ttu-id="80499-112">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="80499-112">Script explanation</span></span>

<span data-ttu-id="80499-113">Этот скрипт использует следующие команды toocreate управляемого диска из VHD в другую подписку.</span><span class="sxs-lookup"><span data-stu-id="80499-113">This script uses following commands toocreate a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="80499-114">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="80499-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="80499-115">Команда</span><span class="sxs-lookup"><span data-stu-id="80499-115">Command</span></span> | <span data-ttu-id="80499-116">Примечания</span><span class="sxs-lookup"><span data-stu-id="80499-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="80499-117">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="80499-117">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="80499-118">Создает конфигурацию диска, которая используется для создания диска.</span><span class="sxs-lookup"><span data-stu-id="80499-118">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="80499-119">Он включает тип хранилища, расположение, идентификатор hello учетной записи хранилища хранения hello родительского виртуального жесткого диска, hello родительского виртуального жесткого диска VHD URI ресурса.</span><span class="sxs-lookup"><span data-stu-id="80499-119">It includes storage type, location, resource Id of hello storage account where hello parent VHD is stored, VHD URI of hello parent VHD.</span></span> |
| [<span data-ttu-id="80499-120">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="80499-120">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="80499-121">Создает диск с помощью конфигурации диска, имени диска и имени группы ресурсов, которые передаются в качестве параметров.</span><span class="sxs-lookup"><span data-stu-id="80499-121">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="80499-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="80499-122">Next steps</span></span>

[<span data-ttu-id="80499-123">Создание виртуальной машины путем подключения управляемого диска как диска ОС</span><span class="sxs-lookup"><span data-stu-id="80499-123">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="80499-124">Дополнительные сведения о hello модуля Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="80499-124">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="80499-125">Примеры сценариев PowerShell дополнительную виртуальную машину можно найти в hello [документации виртуальной Машины Windows Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="80499-125">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
