---
title: "Пример сценария Azure CLI. Создание управляемого диска на основе VHD-файла в учетной записи хранения в той же подписке | Документы Майкрософт"
description: "Пример сценария Azure CLI. Создание управляемого диска на основе VHD-файла в учетной записи хранения в той же подписке"
services: virtual-machines-linux
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: ramankum
ms.openlocfilehash: 448636e87db126defc804a613bb61ff19a086ad9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-the-same-subscription-with-cli"></a><span data-ttu-id="fa099-103">Создание управляемого диска на основе VHD-файла в учетной записи хранения в той же подписке с помощью интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="fa099-103">Create a managed disk from a VHD file in a storage account in the same subscription with CLI</span></span>

<span data-ttu-id="fa099-104">Этот сценарий создает управляемый диск на основе VHD-файла в учетной записи хранения в той же подписке.</span><span class="sxs-lookup"><span data-stu-id="fa099-104">This script creates a managed disk from a VHD file in a storage account in the same subscription.</span></span> <span data-ttu-id="fa099-105">Этот сценарий можно использовать для импорта специализированного (не универсального и не обработанного командой Sysprep) виртуального жесткого диска в управляемый диск операционной системы для создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="fa099-105">Use this script to import a specialized (not generalized/sysprepped) VHD to managed OS disk to create a virtual machine.</span></span> <span data-ttu-id="fa099-106">Кроме того, с его помощью можно импортировать виртуальный жесткий диск данных в управляемый диск данных.</span><span class="sxs-lookup"><span data-stu-id="fa099-106">Or, use it to import a data VHD to managed data disk.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="fa099-107">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="fa099-107">Sample script</span></span>

<span data-ttu-id="fa099-108">[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "Создание управляемого диска на основе VHD")]</span><span class="sxs-lookup"><span data-stu-id="fa099-108">[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "Create managed disk from VHD")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="fa099-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="fa099-109">Script explanation</span></span>

<span data-ttu-id="fa099-110">Этот сценарий использует следующие команды для создания управляемого диска на основе VHD-файла.</span><span class="sxs-lookup"><span data-stu-id="fa099-110">This script uses following commands to create a managed disk from a VHD.</span></span> <span data-ttu-id="fa099-111">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="fa099-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="fa099-112">Команда</span><span class="sxs-lookup"><span data-stu-id="fa099-112">Command</span></span> | <span data-ttu-id="fa099-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="fa099-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fa099-114">az disk create</span><span class="sxs-lookup"><span data-stu-id="fa099-114">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="fa099-115">Создает управляемый диск на основе URI виртуального жесткого диска в учетной записи хранения в той же подписке.</span><span class="sxs-lookup"><span data-stu-id="fa099-115">Creates a managed disk using URI of a VHD in a storage account in the same subscription</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fa099-116">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fa099-116">Next steps</span></span>

[<span data-ttu-id="fa099-117">Создание виртуальной машины путем подключения управляемого диска как диска операционной системы</span><span class="sxs-lookup"><span data-stu-id="fa099-117">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="fa099-118">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fa099-118">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fa099-119">Дополнительные примеры сценариев интерфейса командной строки для виртуальных машин и управляемых дисков см. в [документации по виртуальным машинам Azure под управлением Linux](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fa099-119">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
