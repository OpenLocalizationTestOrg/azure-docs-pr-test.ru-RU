---
title: "Пример сценария CLI - aaaAzure создавать кэш Redis Azure Premium с кластеризацией | Документы Microsoft"
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
ms.openlocfilehash: ca34d40059b282cb2abc7e3e2b8771226029744c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-premium-azure-redis-cache-with-clustering"></a><span data-ttu-id="4879a-103">Создание кэша Redis для Azure уровня Премиум с кластеризацией</span><span class="sxs-lookup"><span data-stu-id="4879a-103">Create a Premium Azure Redis Cache with clustering</span></span>

<span data-ttu-id="4879a-104">В этом сценарии вы узнаете, как toocreate уровня Premium 6 ГБ кэша Azure Redis с кластеризацией включен и двух сегментов.</span><span class="sxs-lookup"><span data-stu-id="4879a-104">In this scenario, you learn how toocreate a 6 GB Premium tier Azure Redis Cache with clustering enabled and two shards.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="4879a-105">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="4879a-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/create-premium-cache-cluster/create-premium-cache-cluster.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="4879a-106">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="4879a-106">Script explanation</span></span>

<span data-ttu-id="4879a-107">Этот скрипт использует следующие команды toocreate hello группу ресурсов и кэш redis уровня Premium с кластеризацией enable.</span><span class="sxs-lookup"><span data-stu-id="4879a-107">This script uses hello following commands toocreate a resource group and a Premium tier redis cache with clustering enable.</span></span> <span data-ttu-id="4879a-108">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="4879a-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4879a-109">Команда</span><span class="sxs-lookup"><span data-stu-id="4879a-109">Command</span></span> | <span data-ttu-id="4879a-110">Примечания</span><span class="sxs-lookup"><span data-stu-id="4879a-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4879a-111">az group create</span><span class="sxs-lookup"><span data-stu-id="4879a-111">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="4879a-112">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="4879a-112">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4879a-113">az redis create</span><span class="sxs-lookup"><span data-stu-id="4879a-113">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="4879a-114">Создает экземпляр кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="4879a-114">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="4879a-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4879a-115">Next steps</span></span>

<span data-ttu-id="4879a-116">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4879a-116">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="4879a-117">Дополнительные образцы сценариев CLI кэша Redis Azure можно найти в hello [документации кэш Azure Redis](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4879a-117">Additional Azure Redis Cache CLI script samples can be found in hello [Azure Redis Cache documentation](../cli-samples.md).</span></span>
