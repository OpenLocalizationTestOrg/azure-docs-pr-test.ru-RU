---
title: "Пример сценария CLI - aaaAzure создания управляемой дисковой из моментального снимка | Документы Microsoft"
description: "Пример сценария Azure CLI. Создание управляемого диска на основе моментального снимка"
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
ms.openlocfilehash: 549692f5027b3f50b0dd89fe701ebbf0f51d6031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-cli"></a><span data-ttu-id="60e5a-103">Создание управляемого диска на основе моментального снимка с помощью интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="60e5a-103">Create a managed disk from a snapshot with CLI</span></span>

<span data-ttu-id="60e5a-104">Этот сценарий создает управляемый диск на основе моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="60e5a-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="60e5a-105">Используйте toorestore виртуальную машину из моментальных снимков дисков операционной системы и данных.</span><span class="sxs-lookup"><span data-stu-id="60e5a-105">Use it toorestore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="60e5a-106">Можно создать управляемые диски данных и ОС на основе соответствующих моментальных снимков, а затем создать виртуальную машину, подключив эти управляемые диски.</span><span class="sxs-lookup"><span data-stu-id="60e5a-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="60e5a-107">Кроме того, вы можете восстановить диски данных существующей виртуальной машины, подключив диски данных, созданные из моментальных снимков.</span><span class="sxs-lookup"><span data-stu-id="60e5a-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="60e5a-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="60e5a-108">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-disks-from-snapshot/create-managed-disks-from-snapshot.sh "Create managed disk from snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="60e5a-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="60e5a-109">Script explanation</span></span>

<span data-ttu-id="60e5a-110">Этот скрипт использует следующие команды toocreate управляемого диска из моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="60e5a-110">This script uses following commands toocreate a managed disk from a snapshot.</span></span> <span data-ttu-id="60e5a-111">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="60e5a-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="60e5a-112">Команда</span><span class="sxs-lookup"><span data-stu-id="60e5a-112">Command</span></span> | <span data-ttu-id="60e5a-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="60e5a-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="60e5a-114">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="60e5a-114">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="60e5a-115">Возвращает все свойства hello моментального снимка с использованием имени hello и свойства группы ресурсов hello моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="60e5a-115">Gets all hello properties of a snapshot using hello name and resource group properties of hello snapshot.</span></span> <span data-ttu-id="60e5a-116">Идентификатор свойства — используется toocreate управляемого диска.</span><span class="sxs-lookup"><span data-stu-id="60e5a-116">Id property is used toocreate managed disk.</span></span>  |
| [<span data-ttu-id="60e5a-117">az disk create</span><span class="sxs-lookup"><span data-stu-id="60e5a-117">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="60e5a-118">Создает управляемый диск с помощью идентификатора управляемого моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="60e5a-118">Creates a managed disk using snapshot Id of a managed snapshot</span></span> |

## <a name="next-steps"></a><span data-ttu-id="60e5a-119">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="60e5a-119">Next steps</span></span>

[<span data-ttu-id="60e5a-120">Создание виртуальной машины путем подключения управляемого диска как диска ОС</span><span class="sxs-lookup"><span data-stu-id="60e5a-120">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="60e5a-121">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="60e5a-121">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="60e5a-122">Установить дополнительную виртуальную машину и управляемых дисков CLI образцы скриптов можно найти в hello [документации виртуальной Машине Linux Azure](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="60e5a-122">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
