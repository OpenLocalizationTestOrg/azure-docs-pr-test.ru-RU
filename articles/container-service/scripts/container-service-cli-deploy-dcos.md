---
title: "Пример скрипта Azure CLI. Создание кластера DC/OS ACS | Документы Майкрософт"
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
ms.openlocfilehash: 4efd7dea04fd3486f875e57737e438c966872dd4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="5acf8-104">Создание кластера DC/OS службы контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="5acf8-104">Create an Azure Container Service DC/OS Cluster</span></span>

<span data-ttu-id="5acf8-105">В этом примере создается кластер службы контейнеров Azure для запуска DCOS.</span><span class="sxs-lookup"><span data-stu-id="5acf8-105">This sample creates an Azure Container Service cluster running DCOS.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5acf8-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="5acf8-106">Sample script</span></span>

```azurecli
az group create --name myResourceGroup --location eastus

az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

## <a name="clean-up-deployment"></a><span data-ttu-id="5acf8-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="5acf8-107">Clean up deployment</span></span> 

<span data-ttu-id="5acf8-108">Выполните следующую команду, чтобы удалить группу ресурсов, виртуальную машину и все связанные с ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="5acf8-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="5acf8-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="5acf8-109">Script explanation</span></span>

<span data-ttu-id="5acf8-110">Чтобы создать развертывание, скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="5acf8-110">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="5acf8-111">Для каждого элемента в таблице приведены ссылки на документацию по команде.</span><span class="sxs-lookup"><span data-stu-id="5acf8-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5acf8-112">Команда</span><span class="sxs-lookup"><span data-stu-id="5acf8-112">Command</span></span> | <span data-ttu-id="5acf8-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="5acf8-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5acf8-114">az group create</span><span class="sxs-lookup"><span data-stu-id="5acf8-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="5acf8-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="5acf8-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5acf8-116">az acs create</span><span class="sxs-lookup"><span data-stu-id="5acf8-116">az acs create</span></span>](https://docs.microsoft.com/cli/azure/acs#create) | <span data-ttu-id="5acf8-117">Создает кластер ACS.</span><span class="sxs-lookup"><span data-stu-id="5acf8-117">Creates and ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5acf8-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5acf8-118">Next steps</span></span>

<span data-ttu-id="5acf8-119">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5acf8-119">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5acf8-120">Дополнительные примеры скриптов CLI службы контейнеров Azure см. в [документации по службе контейнеров Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5acf8-120">Additional Azure Container Service CLI script samples can be found in the [Azure Container Service documentation](../cli-samples.md).</span></span>