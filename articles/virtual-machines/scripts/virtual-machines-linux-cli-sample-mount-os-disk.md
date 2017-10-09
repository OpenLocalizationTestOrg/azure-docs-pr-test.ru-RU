---
title: "aaaAzure образец скрипта CLI - монтирования диска операционной системы | Документы Microsoft"
description: "Пример скрипта Azure CLI. Подключение диска операционной системы"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5c614d09a64780575b70424d29052f1a6affec59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-vms-operating-system-disk"></a><span data-ttu-id="011b7-103">Устранение неполадок диска операционной системы виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="011b7-103">Troubleshoot a VMs operating system disk</span></span>

<span data-ttu-id="011b7-104">Этот сценарий подключает hello диск операционной системы виртуальной машины, сбоя или проблемный как данных диска tooa второй виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="011b7-104">This script mounts hello operating system disk of a failed or problematic virtual machine as a data disk tooa second virtual machine.</span></span> <span data-ttu-id="011b7-105">Это может быть полезно при устранении неполадок с дисками или восстановлении данных.</span><span class="sxs-lookup"><span data-stu-id="011b7-105">This can be useful when troubleshooting disk issues or recovering data.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="011b7-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="011b7-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/mount-os-disk/mount-os-disk.sh "Quick Create VM")]

## <a name="script-explanation"></a><span data-ttu-id="011b7-107">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="011b7-107">Script explanation</span></span>

<span data-ttu-id="011b7-108">Этот скрипт использует hello, следующие команды toocreate группу ресурсов виртуальной машины, и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="011b7-108">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="011b7-109">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="011b7-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="011b7-110">Команда</span><span class="sxs-lookup"><span data-stu-id="011b7-110">Command</span></span> | <span data-ttu-id="011b7-111">Примечания</span><span class="sxs-lookup"><span data-stu-id="011b7-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="011b7-112">az vm show</span><span class="sxs-lookup"><span data-stu-id="011b7-112">az vm show</span></span>](https://docs.microsoft.com/cli/azure/vm#show) | <span data-ttu-id="011b7-113">Возвращает список виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="011b7-113">Return a list of virtual machines.</span></span> <span data-ttu-id="011b7-114">В этом случае параметр запроса hello является диск операционной системы виртуальной машины используется tooreturn hello.</span><span class="sxs-lookup"><span data-stu-id="011b7-114">In this case, hello query option is used tooreturn hello virtual machine operating system disk.</span></span> <span data-ttu-id="011b7-115">Затем это значение добавляется имя переменной tooa «uri».</span><span class="sxs-lookup"><span data-stu-id="011b7-115">This value is then added tooa variable name ‘uri’.</span></span> |
| [<span data-ttu-id="011b7-116">az vm delete</span><span class="sxs-lookup"><span data-stu-id="011b7-116">az vm delete</span></span>](https://docs.microsoft.com/cli/azure/vm#delete) | <span data-ttu-id="011b7-117">Удаляет виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="011b7-117">Deletes a virtual machine.</span></span> |
| [<span data-ttu-id="011b7-118">az vm create</span><span class="sxs-lookup"><span data-stu-id="011b7-118">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="011b7-119">Создает виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="011b7-119">Creates a virtual machine.</span></span>  |
| [<span data-ttu-id="011b7-120">az vm disk attach</span><span class="sxs-lookup"><span data-stu-id="011b7-120">az vm disk attach</span></span>](https://docs.microsoft.com/cli/azure/vm/disk#attach) | <span data-ttu-id="011b7-121">Присоединяет диск tooa виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="011b7-121">Attaches a disk tooa virtual machine.</span></span> |
| [<span data-ttu-id="011b7-122">az vm list-ip-addresses</span><span class="sxs-lookup"><span data-stu-id="011b7-122">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="011b7-123">Возвращает hello IP-адреса виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="011b7-123">Returns hello IP addresses of a virtual machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="011b7-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="011b7-124">Next steps</span></span>

<span data-ttu-id="011b7-125">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="011b7-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="011b7-126">Примеры сценариев CLI дополнительную виртуальную машину можно найти в hello [документации виртуальной Машине Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="011b7-126">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
