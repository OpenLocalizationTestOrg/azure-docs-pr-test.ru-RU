---
title: "Пример скрипта Azure CLI. Масштабирование кластера ACS | Документы Майкрософт"
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
ms.openlocfilehash: 0ea2c73436e650fdb37535538baccc565369fa9d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="scale-an-azure-container-service-cluster"></a><span data-ttu-id="87ca4-104">Масштабирование кластера службы контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="87ca4-104">Scale an Azure Container Service Cluster</span></span>

<span data-ttu-id="87ca4-105">В этом примере выполняется масштабирование в службе контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="87ca4-105">This sample scales and Azure Container Service.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="87ca4-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="87ca4-106">Sample script</span></span>

```azurecli
az acs scale --resource-group myResourceGroup --name myK8SCluster --new-agent-count 5
```

## <a name="clean-up-deployment"></a><span data-ttu-id="87ca4-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="87ca4-107">Clean up deployment</span></span> 

<span data-ttu-id="87ca4-108">Выполните следующую команду, чтобы удалить группу ресурсов, виртуальную машину и все связанные с ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="87ca4-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="87ca4-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="87ca4-109">Script explanation</span></span>

<span data-ttu-id="87ca4-110">Чтобы создать развертывание, скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="87ca4-110">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="87ca4-111">Для каждого элемента в таблице приведены ссылки на документацию по команде.</span><span class="sxs-lookup"><span data-stu-id="87ca4-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="87ca4-112">Команда</span><span class="sxs-lookup"><span data-stu-id="87ca4-112">Command</span></span> | <span data-ttu-id="87ca4-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="87ca4-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="87ca4-114">az acs scale</span><span class="sxs-lookup"><span data-stu-id="87ca4-114">az acs scale</span></span>](/cli/azure/acs#scale) | <span data-ttu-id="87ca4-115">Масштабирование кластера ACS.</span><span class="sxs-lookup"><span data-stu-id="87ca4-115">Scale an ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="87ca4-116">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="87ca4-116">Next steps</span></span>

<span data-ttu-id="87ca4-117">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="87ca4-117">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="87ca4-118">Дополнительные примеры скриптов CLI службы контейнеров Azure см. в [документации по службе контейнеров Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="87ca4-118">Additional Azure Container Service CLI script samples can be found in the [Azure Container Service documentation](../cli-samples.md).</span></span>

