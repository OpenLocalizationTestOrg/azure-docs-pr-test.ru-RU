---
title: "Пример сценария Azure CLI. Копирование (перемещение) управляемых дисков в ту же или другую подписку | Microsoft Docs"
description: "Пример сценария Azure CLI. Копирование (перемещение) управляемых дисков в ту же или другую подписку"
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
ms.openlocfilehash: 784ad81db2c83da14665fa926425928f12a15c27
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="copy-managed-disks-to-same-or-different-subscription-with-cli"></a><span data-ttu-id="0eae7-103">Копирование управляемых дисков в ту же или другую подписку с помощью интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="0eae7-103">Copy managed disks to same or different subscription with CLI</span></span>

<span data-ttu-id="0eae7-104">Этот сценарий копирует управляемый диск в ту же или другую подписку в одном регионе.</span><span class="sxs-lookup"><span data-stu-id="0eae7-104">This script copies a managed disk to same or different subscription but in the same region.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="0eae7-105">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="0eae7-105">Sample script</span></span>

<span data-ttu-id="0eae7-106">[!code-azurecli[main](../../../cli_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "Копирование управляемого диска")]</span><span class="sxs-lookup"><span data-stu-id="0eae7-106">[!code-azurecli[main](../../../cli_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "Copy managed disk")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="0eae7-107">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="0eae7-107">Script explanation</span></span>

<span data-ttu-id="0eae7-108">Этот сценарий использует приведенные ниже команды для создания управляемого диска в целевой подписке с помощью идентификатора исходного управляемого диска.</span><span class="sxs-lookup"><span data-stu-id="0eae7-108">This script uses following commands to create a new managed disk in the target subscription using the Id of the source managed disk.</span></span> <span data-ttu-id="0eae7-109">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="0eae7-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="0eae7-110">Команда</span><span class="sxs-lookup"><span data-stu-id="0eae7-110">Command</span></span> | <span data-ttu-id="0eae7-111">Примечания</span><span class="sxs-lookup"><span data-stu-id="0eae7-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0eae7-112">az disk show</span><span class="sxs-lookup"><span data-stu-id="0eae7-112">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="0eae7-113">Получает все свойства управляемого диска, используя имя и свойства группы ресурсов управляемого диска.</span><span class="sxs-lookup"><span data-stu-id="0eae7-113">Gets all the properties of a managed disk using the name and resource group properties of the managed disk.</span></span> <span data-ttu-id="0eae7-114">Свойство идентификатора используется для копирования управляемого диска в другую подписку.</span><span class="sxs-lookup"><span data-stu-id="0eae7-114">Id property is used to copy the managed disk to different subscription.</span></span>  |
| [<span data-ttu-id="0eae7-115">az disk create</span><span class="sxs-lookup"><span data-stu-id="0eae7-115">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="0eae7-116">Копирует управляемый диск путем создания нового управляемого диска в другой подписке, используя идентификатор и имя родительского управляемого диска.</span><span class="sxs-lookup"><span data-stu-id="0eae7-116">Copies a managed disk by creating a new managed disk in different subscription using Id and name the parent managed disk.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="0eae7-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0eae7-117">Next steps</span></span>

[<span data-ttu-id="0eae7-118">Создание виртуальной машины на основе управляемого диска</span><span class="sxs-lookup"><span data-stu-id="0eae7-118">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="0eae7-119">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0eae7-119">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="0eae7-120">Дополнительные примеры сценариев интерфейса командной строки для виртуальных машин и управляемых дисков см. в [документации по виртуальным машинам Azure под управлением Linux](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0eae7-120">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
