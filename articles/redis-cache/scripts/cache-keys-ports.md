---
title: "Пример сценария CLI - hello hostname Get, порты и ключи для кэша Azure Redis aaaAzure | Документы Microsoft"
description: "Azure CLI образец скрипта - Get hello hostname, порты и ключи для экземпляра кэша Redis для Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 761eb24e-2ba7-418d-8fc3-431153e69a90
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: e6e794558087d6568438c439e2bf99fc46eeb8bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-hostname-ports-and-keys-for-azure-redis-cache"></a><span data-ttu-id="0af87-103">Получить имя узла hello, порты и ключи для кэша Redis для Azure</span><span class="sxs-lookup"><span data-stu-id="0af87-103">Get hello hostname, ports, and keys for Azure Redis Cache</span></span>

<span data-ttu-id="0af87-104">В этом сценарии вы узнаете, способ использования экземпляра кэша Azure Redis tooan tooconnect tooretrieve hello hostname, порты и ключей.</span><span class="sxs-lookup"><span data-stu-id="0af87-104">In this scenario, you learn how tooretrieve hello hostname, ports, and keys used tooconnect tooan Azure Redis Cache instance.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="0af87-105">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="0af87-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/cache-keys-ports/cache-keys-ports.sh "Azure Redis Cache")]


## <a name="script-explanation"></a><span data-ttu-id="0af87-106">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="0af87-106">Script explanation</span></span>

<span data-ttu-id="0af87-107">Этот скрипт использует следующие команды tooretrieve hello hostname, ключи и порты для экземпляра кэша Redis для Azure hello.</span><span class="sxs-lookup"><span data-stu-id="0af87-107">This script uses hello following commands tooretrieve hello hostname, keys, and ports of an Azure Redis Cache instance.</span></span> <span data-ttu-id="0af87-108">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="0af87-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="0af87-109">Команда</span><span class="sxs-lookup"><span data-stu-id="0af87-109">Command</span></span> | <span data-ttu-id="0af87-110">Примечания</span><span class="sxs-lookup"><span data-stu-id="0af87-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0af87-111">az redis show</span><span class="sxs-lookup"><span data-stu-id="0af87-111">az redis show</span></span>](https://docs.microsoft.com/cli/azure/redis#show) | <span data-ttu-id="0af87-112">Извлекает сведения об экземпляре кэша Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="0af87-112">Retrieve details of an Azure Redis Cache instance.</span></span> |
| [<span data-ttu-id="0af87-113">az redis list-keys</span><span class="sxs-lookup"><span data-stu-id="0af87-113">az redis list-keys</span></span>](https://docs.microsoft.com/cli/azure/redis#list-keys) | <span data-ttu-id="0af87-114">Извлекает ключи доступа для экземпляра кэша Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="0af87-114">Retrieve access keys for an Azure Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="0af87-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0af87-115">Next steps</span></span>

<span data-ttu-id="0af87-116">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0af87-116">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="0af87-117">Дополнительные образцы сценариев CLI кэша Redis Azure можно найти в hello [документации кэш Azure Redis](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="0af87-117">Additional Azure Redis Cache CLI script samples can be found in hello [Azure Redis Cache documentation](../cli-samples.md).</span></span>
