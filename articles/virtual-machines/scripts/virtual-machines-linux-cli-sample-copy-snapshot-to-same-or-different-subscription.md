---
title: "Пример сценария CLI - копии (перемещения) снимок toosame управляемого диска или другой подписке с CLI aaaAzure | Документы Microsoft"
description: "Пример сценария Azure CLI - копии (перемещения) снимок toosame управляемого диска или другой подписке с CLI"
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
ms.openlocfilehash: f214ab1fc1cb2cb42479d82e455f20a8cc55c83d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-toosame-or-different-subscription-with-cli"></a><span data-ttu-id="a9002-103">Скопировать моментальный снимок toosame управляемого диска или другой подписке с CLI</span><span class="sxs-lookup"><span data-stu-id="a9002-103">Copy snapshot of a managed disk toosame or different subscription with CLI</span></span>

<span data-ttu-id="a9002-104">Этот скрипт копирует моментальный снимок toosame управляемого диска или другую подписку.</span><span class="sxs-lookup"><span data-stu-id="a9002-104">This script copies a snapshot of a managed disk toosame or different subscription.</span></span> <span data-ttu-id="a9002-105">Используйте этот скрипт toomove toodifferent подписки на моментальные снимки в hello же регионе, что hello родительского снимка.</span><span class="sxs-lookup"><span data-stu-id="a9002-105">Use this script toomove a snapshot toodifferent subscription in hello same region as hello parent snapshot.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a9002-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="a9002-106">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="a9002-107">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="a9002-107">Script explanation</span></span>

<span data-ttu-id="a9002-108">Этот скрипт использует следующую toocreate команд моментального снимка в hello целевой подписки с помощью hello идентификатор моментального снимка источника hello.</span><span class="sxs-lookup"><span data-stu-id="a9002-108">This script uses following commands toocreate a snapshot in hello target subscription using hello Id of hello source snapshot.</span></span> <span data-ttu-id="a9002-109">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="a9002-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a9002-110">Команда</span><span class="sxs-lookup"><span data-stu-id="a9002-110">Command</span></span> | <span data-ttu-id="a9002-111">Примечания</span><span class="sxs-lookup"><span data-stu-id="a9002-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a9002-112">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="a9002-112">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="a9002-113">Возвращает все свойства hello моментального снимка с использованием имени hello и свойства группы ресурсов hello моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="a9002-113">Gets all hello properties of a snapshot using hello name and resource group properties of hello snapshot.</span></span> <span data-ttu-id="a9002-114">Идентификатор свойства — это используемые toocopy hello моментального снимка toodifferent подписка.</span><span class="sxs-lookup"><span data-stu-id="a9002-114">Id property is used toocopy hello snapshot toodifferent subscription.</span></span>  |
| [<span data-ttu-id="a9002-115">az snapshot create</span><span class="sxs-lookup"><span data-stu-id="a9002-115">az snapshot create</span></span>](https://docs.microsoft.com/cli/azure/snapshot#create) | <span data-ttu-id="a9002-116">Здравствуйте моментального снимка путем создания моментального снимка в другую подписку, используя идентификатор и имя копии hello родительского снимка.</span><span class="sxs-lookup"><span data-stu-id="a9002-116">Copies a snapshot by creating a snapshot in different subscription using hello Id and name of hello parent snapshot.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="a9002-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a9002-117">Next steps</span></span>

[<span data-ttu-id="a9002-118">Создание виртуальной машины на основе моментального снимка</span><span class="sxs-lookup"><span data-stu-id="a9002-118">Create a virtual machine from a snapshot</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="a9002-119">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a9002-119">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a9002-120">Установить дополнительную виртуальную машину и управляемых дисков CLI образцы скриптов можно найти в hello [документации виртуальной Машине Linux Azure](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a9002-120">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
