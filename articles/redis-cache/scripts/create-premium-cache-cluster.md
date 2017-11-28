---
title: "Пример скрипта Azure CLI. Создание кэша Redis для Azure уровня Премиум с кластеризацией | Документы Майкрософт"
description: "Пример скрипта Azure CLI. Создание кэша Redis для Azure уровня Премиум с кластеризацией"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 07bcceae-2521-4fe3-b88f-ed833104ddd2
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: 87d0fe4c3eaa8f7b75343a36a069ecdac8241d74
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-premium-azure-redis-cache-with-clustering"></a><span data-ttu-id="01540-103">Создание кэша Redis для Azure уровня Премиум с кластеризацией</span><span class="sxs-lookup"><span data-stu-id="01540-103">Create a Premium Azure Redis Cache with clustering</span></span>

<span data-ttu-id="01540-104">В этом сценарии вы узнаете, как создать кэш Redis для Azure уровня Премиум размером 6 ГБ с кластеризацией и двумя сегментами.</span><span class="sxs-lookup"><span data-stu-id="01540-104">In this scenario, you learn how to create a 6 GB Premium tier Azure Redis Cache with clustering enabled and two shards.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="01540-105">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="01540-105">Sample script</span></span>

<span data-ttu-id="01540-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/create-premium-cache-cluster/create-premium-cache-cluster.sh "Кэш Redis для Azure")]</span><span class="sxs-lookup"><span data-stu-id="01540-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/create-premium-cache-cluster/create-premium-cache-cluster.sh "Azure Redis Cache")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="01540-107">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="01540-107">Script explanation</span></span>

<span data-ttu-id="01540-108">Для создания группы ресурсов и кэша Redis для Azure уровня Премиум с кластеризацией в этом скрипте используются следующие команды.</span><span class="sxs-lookup"><span data-stu-id="01540-108">This script uses the following commands to create a resource group and a Premium tier redis cache with clustering enable.</span></span> <span data-ttu-id="01540-109">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="01540-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="01540-110">Команда</span><span class="sxs-lookup"><span data-stu-id="01540-110">Command</span></span> | <span data-ttu-id="01540-111">Примечания</span><span class="sxs-lookup"><span data-stu-id="01540-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="01540-112">az group create</span><span class="sxs-lookup"><span data-stu-id="01540-112">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="01540-113">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="01540-113">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="01540-114">az redis create</span><span class="sxs-lookup"><span data-stu-id="01540-114">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="01540-115">Создает экземпляр кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="01540-115">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="01540-116">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="01540-116">Next steps</span></span>

<span data-ttu-id="01540-117">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="01540-117">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="01540-118">Дополнительные примеры сценариев Azure CLI для кэша Redis для Azure см. в [документации по кэшу Redis для Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="01540-118">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>