---
title: "aaaAzure образец скрипта CLI - toosame диски или другой подписке управляемых копии (перемещения) | Документы Microsoft"
description: "Azure CLI образец скрипта - toosame дисков управляемых копии (перемещения) или другой подписке"
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
ms.openlocfilehash: 8581169baa0fd0e0eec1c72eab77b657f48b1cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-toosame-or-different-subscription-with-cli"></a><span data-ttu-id="b3f4a-103">Скопируйте toosame управляемых дисков или другую подписку с CLI</span><span class="sxs-lookup"><span data-stu-id="b3f4a-103">Copy managed disks toosame or different subscription with CLI</span></span>

<span data-ttu-id="b3f4a-104">Этот скрипт копирует toosame управляемого диска или другую подписку, но в hello же области.</span><span class="sxs-lookup"><span data-stu-id="b3f4a-104">This script copies a managed disk toosame or different subscription but in hello same region.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="b3f4a-105">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="b3f4a-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "Copy managed disk")]


## <a name="script-explanation"></a><span data-ttu-id="b3f4a-106">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="b3f4a-106">Script explanation</span></span>

<span data-ttu-id="b3f4a-107">Этот скрипт использует следующую команды toocreate нового управляемого диска в hello целевой подписки с помощью hello идентификатор источника hello управляемого диска.</span><span class="sxs-lookup"><span data-stu-id="b3f4a-107">This script uses following commands toocreate a new managed disk in hello target subscription using hello Id of hello source managed disk.</span></span> <span data-ttu-id="b3f4a-108">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="b3f4a-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b3f4a-109">Команда</span><span class="sxs-lookup"><span data-stu-id="b3f4a-109">Command</span></span> | <span data-ttu-id="b3f4a-110">Примечания</span><span class="sxs-lookup"><span data-stu-id="b3f4a-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b3f4a-111">az disk show</span><span class="sxs-lookup"><span data-stu-id="b3f4a-111">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="b3f4a-112">Возвращает все свойства hello управляемого диска с помощью hello имя ресурса группы свойств и hello управляемого диска.</span><span class="sxs-lookup"><span data-stu-id="b3f4a-112">Gets all hello properties of a managed disk using hello name and resource group properties of hello managed disk.</span></span> <span data-ttu-id="b3f4a-113">Идентификатор свойства — используется toocopy hello управляемого диска toodifferent подписка.</span><span class="sxs-lookup"><span data-stu-id="b3f4a-113">Id property is used toocopy hello managed disk toodifferent subscription.</span></span>  |
| [<span data-ttu-id="b3f4a-114">az disk create</span><span class="sxs-lookup"><span data-stu-id="b3f4a-114">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="b3f4a-115">Копирует управляемого диска путем создания нового управляемого диска в другую подписку, используя идентификатор и имя родительского hello управляемого диска.</span><span class="sxs-lookup"><span data-stu-id="b3f4a-115">Copies a managed disk by creating a new managed disk in different subscription using Id and name hello parent managed disk.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="b3f4a-116">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b3f4a-116">Next steps</span></span>

[<span data-ttu-id="b3f4a-117">Создание виртуальной машины на основе управляемого диска</span><span class="sxs-lookup"><span data-stu-id="b3f4a-117">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="b3f4a-118">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b3f4a-118">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b3f4a-119">Установить дополнительную виртуальную машину и управляемых дисков CLI образцы скриптов можно найти в hello [документации виртуальной Машине Linux Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b3f4a-119">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
