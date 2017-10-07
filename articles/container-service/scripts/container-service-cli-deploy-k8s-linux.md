---
title: "aaaAzure образец скрипта CLI - создать кластер ACS Linux Kubernetes | Документы Microsoft"
description: "Пример скрипта Azure CLI. Создание кластера Kubernetes Linux ACS"
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
ms.openlocfilehash: 811929eea4fdf62d8c3de54e81cbc7f6cda858c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-container-service-kubernetes-linux-cluster"></a><span data-ttu-id="b0a01-104">Создание кластера Kubernetes Linux службы контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="b0a01-104">Create an Azure Container Service Kubernetes Linux Cluster</span></span>

<span data-ttu-id="b0a01-105">В этом примере создается кластер службы контейнеров Azure для запуска Kubernetes для контейнеров на основе Linux.</span><span class="sxs-lookup"><span data-stu-id="b0a01-105">This sample creates an Azure Container Service cluster running Kubernetes for Linux based containers.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="b0a01-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="b0a01-106">Sample script</span></span>

```azurecli
az group create --name myResourceGroup --location eastus

az acs create \
  --orchestrator-type kubernetes \
  --resource-group myResourceGroup \
  --name myK8SCluster \
  --generate-ssh-keys
```

## <a name="clean-up-deployment"></a><span data-ttu-id="b0a01-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="b0a01-107">Clean up deployment</span></span> 

<span data-ttu-id="b0a01-108">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="b0a01-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="b0a01-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="b0a01-109">Script explanation</span></span>

<span data-ttu-id="b0a01-110">Этот скрипт использует следующие команды toocreate hello развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="b0a01-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="b0a01-111">Каждый элемент в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="b0a01-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b0a01-112">Команда</span><span class="sxs-lookup"><span data-stu-id="b0a01-112">Command</span></span> | <span data-ttu-id="b0a01-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="b0a01-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b0a01-114">az group create</span><span class="sxs-lookup"><span data-stu-id="b0a01-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="b0a01-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="b0a01-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b0a01-116">az acs create</span><span class="sxs-lookup"><span data-stu-id="b0a01-116">az acs create</span></span>](https://docs.microsoft.com/cli/azure/acs#create) | <span data-ttu-id="b0a01-117">Создает кластер ACS.</span><span class="sxs-lookup"><span data-stu-id="b0a01-117">Creates and ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b0a01-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b0a01-118">Next steps</span></span>

<span data-ttu-id="b0a01-119">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b0a01-119">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b0a01-120">Дополнительные образцы сценариев службы контейнера Azure CLI можно найти в hello [документации по службе Azure контейнер](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b0a01-120">Additional Azure Container Service CLI script samples can be found in hello [Azure Container Service documentation](../cli-samples.md).</span></span>

