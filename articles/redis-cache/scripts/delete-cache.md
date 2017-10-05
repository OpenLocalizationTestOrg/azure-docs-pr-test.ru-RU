---
title: "Пример скрипта Azure CLI. Удаление кэша Redis для Azure | Документы Майкрософт"
description: "Пример скрипта Azure CLI. Удаление кэша Redis для Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 7beded7a-d2c9-43a6-b3b4-b8079c11de4a
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: f959823b3a7c5b0262f693ecad1e6efc4eec4f35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="delete-an-azure-redis-cache"></a><span data-ttu-id="c3d97-103">Удаление кэша Redis для Azure</span><span class="sxs-lookup"><span data-stu-id="c3d97-103">Delete an Azure Redis Cache</span></span>

<span data-ttu-id="c3d97-104">В этом сценарии вы узнаете, как удалить кэш Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="c3d97-104">In this scenario, you learn how to delete an Azure Redis Cache.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="c3d97-105">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="c3d97-105">Sample script</span></span>

<span data-ttu-id="c3d97-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/delete-cache/delete-cache.sh "Кэш Redis для Azure")]</span><span class="sxs-lookup"><span data-stu-id="c3d97-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/delete-cache/delete-cache.sh "Azure Redis Cache")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="c3d97-107">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="c3d97-107">Script explanation</span></span>

<span data-ttu-id="c3d97-108">В этом сценарии используются следующие команды для удаления экземпляра кэша Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="c3d97-108">This script uses the following commands to delete an Azure Redis Cache instance.</span></span> <span data-ttu-id="c3d97-109">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="c3d97-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c3d97-110">Команда</span><span class="sxs-lookup"><span data-stu-id="c3d97-110">Command</span></span> | <span data-ttu-id="c3d97-111">Примечания</span><span class="sxs-lookup"><span data-stu-id="c3d97-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c3d97-112">az redis delete</span><span class="sxs-lookup"><span data-stu-id="c3d97-112">az redis delete</span></span>](https://docs.microsoft.com/cli/azure/redis#delete) | <span data-ttu-id="c3d97-113">Удаляет экземпляр кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="c3d97-113">Delete Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="c3d97-114">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c3d97-114">Next steps</span></span>

<span data-ttu-id="c3d97-115">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c3d97-115">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c3d97-116">Дополнительные примеры сценариев Azure CLI для кэша Redis для Azure см. в [документации по кэшу Redis для Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c3d97-116">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>