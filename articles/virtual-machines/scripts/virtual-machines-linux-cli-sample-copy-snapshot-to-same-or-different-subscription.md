---
title: "Пример сценария Azure CLI. Копирование (перемещение) моментального снимка управляемого диска в ту же или другую подписку с помощью CLI | Документы Майкрософт"
description: "Пример сценария Azure CLI. Копирование (перемещение) моментального снимка управляемого диска в ту же или другую подписку с помощью CLI"
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
ms.openlocfilehash: 6cc0125c08ccb77d014b4642d702c556fffdc8bf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="copy-snapshot-of-a-managed-disk-to-same-or-different-subscription-with-cli"></a><span data-ttu-id="6a037-103">Копирование моментального снимка управляемого диска в ту же или другую подписку с помощью интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="6a037-103">Copy snapshot of a managed disk to same or different subscription with CLI</span></span>

<span data-ttu-id="6a037-104">Этот сценарий копирует моментальный снимок управляемого диска в ту же или другую подписку.</span><span class="sxs-lookup"><span data-stu-id="6a037-104">This script copies a snapshot of a managed disk to same or different subscription.</span></span> <span data-ttu-id="6a037-105">Этот сценарий можно использовать для перемещения моментального снимка в другую подписку в том же регионе, что и родительский снимок.</span><span class="sxs-lookup"><span data-stu-id="6a037-105">Use this script to move a snapshot to different subscription in the same region as the parent snapshot.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="6a037-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="6a037-106">Sample script</span></span>

<span data-ttu-id="6a037-107">[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Копирование моментального снимка")]</span><span class="sxs-lookup"><span data-stu-id="6a037-107">[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="6a037-108">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="6a037-108">Script explanation</span></span>

<span data-ttu-id="6a037-109">Этот сценарий использует приведенные ниже команды для создания моментального снимка в целевой подписке с помощью идентификатора исходного моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="6a037-109">This script uses following commands to create a snapshot in the target subscription using the Id of the source snapshot.</span></span> <span data-ttu-id="6a037-110">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="6a037-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6a037-111">Команда</span><span class="sxs-lookup"><span data-stu-id="6a037-111">Command</span></span> | <span data-ttu-id="6a037-112">Примечания</span><span class="sxs-lookup"><span data-stu-id="6a037-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6a037-113">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="6a037-113">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="6a037-114">Получает все свойства моментального снимка, используя имя и свойства группы ресурсов моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="6a037-114">Gets all the properties of a snapshot using the name and resource group properties of the snapshot.</span></span> <span data-ttu-id="6a037-115">Свойство идентификатора используется для копирования моментального снимка в другую подписку.</span><span class="sxs-lookup"><span data-stu-id="6a037-115">Id property is used to copy the snapshot to different subscription.</span></span>  |
| [<span data-ttu-id="6a037-116">az snapshot create</span><span class="sxs-lookup"><span data-stu-id="6a037-116">az snapshot create</span></span>](https://docs.microsoft.com/cli/azure/snapshot#create) | <span data-ttu-id="6a037-117">Копирует моментальный снимок путем создания моментального снимка в другой подписке с помощью идентификатора и имени родительского снимка.</span><span class="sxs-lookup"><span data-stu-id="6a037-117">Copies a snapshot by creating a snapshot in different subscription using the Id and name of the parent snapshot.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="6a037-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6a037-118">Next steps</span></span>

[<span data-ttu-id="6a037-119">Создание виртуальной машины на основе моментального снимка</span><span class="sxs-lookup"><span data-stu-id="6a037-119">Create a virtual machine from a snapshot</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="6a037-120">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6a037-120">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6a037-121">Дополнительные примеры сценариев интерфейса командной строки для виртуальных машин и управляемых дисков см. в [документации по виртуальным машинам Azure под управлением Linux](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6a037-121">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
