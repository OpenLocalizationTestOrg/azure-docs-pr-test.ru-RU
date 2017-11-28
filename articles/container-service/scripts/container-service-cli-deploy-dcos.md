---
title: "aaaAzure образец скрипта CLI - создать кластер ACS DC/OS | Документы Microsoft"
description: "Пример скрипта Azure CLI. Создание кластера DC/OS ACS"
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
ms.openlocfilehash: 35213fd615b2145642add908dfc48516c33ff332
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="0f6f4-104">Создание кластера DC/OS службы контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="0f6f4-104">Create an Azure Container Service DC/OS Cluster</span></span>

<span data-ttu-id="0f6f4-105">В этом примере создается кластер службы контейнеров Azure для запуска DCOS.</span><span class="sxs-lookup"><span data-stu-id="0f6f4-105">This sample creates an Azure Container Service cluster running DCOS.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="0f6f4-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="0f6f4-106">Sample script</span></span>

```azurecli
az group create --name myResourceGroup --location eastus

az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

## <a name="clean-up-deployment"></a><span data-ttu-id="0f6f4-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="0f6f4-107">Clean up deployment</span></span> 

<span data-ttu-id="0f6f4-108">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="0f6f4-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="0f6f4-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="0f6f4-109">Script explanation</span></span>

<span data-ttu-id="0f6f4-110">Этот скрипт использует следующие команды toocreate hello развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="0f6f4-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="0f6f4-111">Каждый элемент в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="0f6f4-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="0f6f4-112">Команда</span><span class="sxs-lookup"><span data-stu-id="0f6f4-112">Command</span></span> | <span data-ttu-id="0f6f4-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="0f6f4-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0f6f4-114">az group create</span><span class="sxs-lookup"><span data-stu-id="0f6f4-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="0f6f4-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="0f6f4-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0f6f4-116">az acs create</span><span class="sxs-lookup"><span data-stu-id="0f6f4-116">az acs create</span></span>](https://docs.microsoft.com/cli/azure/acs#create) | <span data-ttu-id="0f6f4-117">Создает кластер ACS.</span><span class="sxs-lookup"><span data-stu-id="0f6f4-117">Creates and ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0f6f4-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0f6f4-118">Next steps</span></span>

<span data-ttu-id="0f6f4-119">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0f6f4-119">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="0f6f4-120">Дополнительные образцы сценариев службы контейнера Azure CLI можно найти в hello [документации по службе Azure контейнер](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="0f6f4-120">Additional Azure Container Service CLI script samples can be found in hello [Azure Container Service documentation](../cli-samples.md).</span></span>
