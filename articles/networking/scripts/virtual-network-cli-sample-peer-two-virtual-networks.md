---
title: "Пример сценария CLI - aaaAzure одноранговых две виртуальные сети | Документы Microsoft"
description: "Пример скрипта Azure CLI. Пиринг между двумя виртуальными сетями"
services: virtual-network
documentationcenter: virtual-network
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 54dabb2b9e05951d10f1b6b4f61ca592ce11d364
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="a566e-103">Пиринг между двумя виртуальными сетями</span><span class="sxs-lookup"><span data-stu-id="a566e-103">Peer two virtual networks</span></span>

<span data-ttu-id="a566e-104">Этот скрипт создается и выполняется подключение двух виртуальных сетей в hello hello trhough того же региона сети Azure.</span><span class="sxs-lookup"><span data-stu-id="a566e-104">This script creates and connects two virtual networks in hello same region trhough hello Azure network.</span></span> <span data-ttu-id="a566e-105">После выполнения сценария hello, вы создадите пиринг между двумя виртуальными сетями.</span><span class="sxs-lookup"><span data-stu-id="a566e-105">After running hello script, you will create a peering between two virtual networks.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="a566e-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="a566e-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.sh "Peer two networks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="a566e-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="a566e-107">Clean up deployment</span></span> 

<span data-ttu-id="a566e-108">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="a566e-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="a566e-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="a566e-109">Script explanation</span></span>

<span data-ttu-id="a566e-110">Этот скрипт использует hello, следующие команды toocreate группу ресурсов виртуальной машины, и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="a566e-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="a566e-111">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="a566e-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a566e-112">Команда</span><span class="sxs-lookup"><span data-stu-id="a566e-112">Command</span></span> | <span data-ttu-id="a566e-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="a566e-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a566e-114">az group create</span><span class="sxs-lookup"><span data-stu-id="a566e-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="a566e-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="a566e-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a566e-116">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="a566e-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="a566e-117">Создает виртуальную сеть и подсеть Azure.</span><span class="sxs-lookup"><span data-stu-id="a566e-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="a566e-118">az network vnet peering create</span><span class="sxs-lookup"><span data-stu-id="a566e-118">az network vnet peering create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/peering#create) | <span data-ttu-id="a566e-119">Создает пиринг между двумя виртуальными сетями.</span><span class="sxs-lookup"><span data-stu-id="a566e-119">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="a566e-120">az group delete</span><span class="sxs-lookup"><span data-stu-id="a566e-120">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="a566e-121">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="a566e-121">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a566e-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a566e-122">Next steps</span></span>

<span data-ttu-id="a566e-123">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a566e-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a566e-124">Дополнительные сетевые образцы сценариев CLI можно найти в hello [документации Azure Общие сведения о сети](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a566e-124">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md).</span></span>
