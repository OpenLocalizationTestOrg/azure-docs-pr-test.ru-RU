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
ms.openlocfilehash: 0127e342bd0c3afbe9de775399f5510814bff499
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="copy-snapshot-of-a-managed-disk-to-same-or-different-subscription-with-cli"></a><span data-ttu-id="a84d3-103">Копирование моментального снимка управляемого диска в ту же или другую подписку с помощью интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="a84d3-103">Copy snapshot of a managed disk to same or different subscription with CLI</span></span>

<span data-ttu-id="a84d3-104">Этот сценарий копирует моментальный снимок управляемого диска в ту же или другую подписку.</span><span class="sxs-lookup"><span data-stu-id="a84d3-104">This script copies a snapshot of a managed disk to same or different subscription.</span></span> <span data-ttu-id="a84d3-105">Этот сценарий можно использовать для перемещения моментального снимка в другую подписку в том же регионе, что и родительский снимок.</span><span class="sxs-lookup"><span data-stu-id="a84d3-105">Use this script to move a snapshot to different subscription in the same region as the parent snapshot.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a84d3-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="a84d3-106">Sample script</span></span>

<span data-ttu-id="a84d3-107">[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Копирование моментального снимка")]</span><span class="sxs-lookup"><span data-stu-id="a84d3-107">[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="a84d3-108">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="a84d3-108">Script explanation</span></span>

<span data-ttu-id="a84d3-109">Этот сценарий использует приведенные ниже команды для создания моментального снимка в целевой подписке с помощью идентификатора исходного моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="a84d3-109">This script uses following commands to create a snapshot in the target subscription using the Id of the source snapshot.</span></span> <span data-ttu-id="a84d3-110">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="a84d3-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a84d3-111">Команда</span><span class="sxs-lookup"><span data-stu-id="a84d3-111">Command</span></span> | <span data-ttu-id="a84d3-112">Примечания</span><span class="sxs-lookup"><span data-stu-id="a84d3-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a84d3-113">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="a84d3-113">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="a84d3-114">Получает все свойства моментального снимка, используя имя и свойства группы ресурсов моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="a84d3-114">Gets all the properties of a snapshot using the name and resource group properties of the snapshot.</span></span> <span data-ttu-id="a84d3-115">Свойство идентификатора используется для копирования моментального снимка в другую подписку.</span><span class="sxs-lookup"><span data-stu-id="a84d3-115">Id property is used to copy the snapshot to different subscription.</span></span>  |
| [<span data-ttu-id="a84d3-116">az snapshot create</span><span class="sxs-lookup"><span data-stu-id="a84d3-116">az snapshot create</span></span>](https://docs.microsoft.com/cli/azure/snapshot#create) | <span data-ttu-id="a84d3-117">Копирует моментальный снимок путем создания моментального снимка в другой подписке с помощью идентификатора и имени родительского снимка.</span><span class="sxs-lookup"><span data-stu-id="a84d3-117">Copies a snapshot by creating a snapshot in different subscription using the Id and name of the parent snapshot.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="a84d3-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a84d3-118">Next steps</span></span>

[<span data-ttu-id="a84d3-119">Создание виртуальной машины на основе моментального снимка</span><span class="sxs-lookup"><span data-stu-id="a84d3-119">Create a virtual machine from a snapshot</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="a84d3-120">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a84d3-120">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a84d3-121">Дополнительные примеры сценариев интерфейса командной строки для виртуальных машин и управляемых дисков см. в [документации по виртуальным машинам Azure под управлением Linux](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a84d3-121">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
