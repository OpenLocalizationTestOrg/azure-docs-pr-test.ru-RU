---
title: "Пример сценария CLI - aaaAzure масштабировать кластер ACS | Документы Microsoft"
description: "Пример скрипта Azure CLI. Масштабирование кластера ACS"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, контейнеры, микрослужбы, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: nepeters
ms.openlocfilehash: b1c214d7cca615257ec8cd6e9993cd15f694289b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scale-an-azure-container-service-cluster"></a><span data-ttu-id="c028e-104">Масштабирование кластера службы контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="c028e-104">Scale an Azure Container Service Cluster</span></span>

<span data-ttu-id="c028e-105">В этом примере выполняется масштабирование в службе контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="c028e-105">This sample scales and Azure Container Service.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c028e-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="c028e-106">Sample script</span></span>

```azurecli
az acs scale --resource-group myResourceGroup --name myK8SCluster --new-agent-count 5
```

## <a name="clean-up-deployment"></a><span data-ttu-id="c028e-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="c028e-107">Clean up deployment</span></span> 

<span data-ttu-id="c028e-108">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="c028e-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="c028e-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="c028e-109">Script explanation</span></span>

<span data-ttu-id="c028e-110">Этот скрипт использует следующие команды toocreate hello развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="c028e-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="c028e-111">Каждый элемент в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="c028e-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c028e-112">Команда</span><span class="sxs-lookup"><span data-stu-id="c028e-112">Command</span></span> | <span data-ttu-id="c028e-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="c028e-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c028e-114">az acs scale</span><span class="sxs-lookup"><span data-stu-id="c028e-114">az acs scale</span></span>](/cli/azure/acs#scale) | <span data-ttu-id="c028e-115">Масштабирование кластера ACS.</span><span class="sxs-lookup"><span data-stu-id="c028e-115">Scale an ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c028e-116">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c028e-116">Next steps</span></span>

<span data-ttu-id="c028e-117">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c028e-117">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c028e-118">Дополнительные образцы сценариев службы контейнера Azure CLI можно найти в hello [документации по службе Azure контейнер](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c028e-118">Additional Azure Container Service CLI script samples can be found in hello [Azure Container Service documentation](../cli-samples.md).</span></span>

