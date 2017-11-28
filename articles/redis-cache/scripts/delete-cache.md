---
title: "Пример сценария CLI - aaaAzure удалить кэш Azure Redis | Документы Microsoft"
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
ms.openlocfilehash: 788277f6464d40fedc597ce7f3041130312c07a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="delete-an-azure-redis-cache"></a><span data-ttu-id="28a3d-103">Удаление кэша Redis для Azure</span><span class="sxs-lookup"><span data-stu-id="28a3d-103">Delete an Azure Redis Cache</span></span>

<span data-ttu-id="28a3d-104">В этом сценарии вы узнаете, как toodelete Redis для Azure кэша.</span><span class="sxs-lookup"><span data-stu-id="28a3d-104">In this scenario, you learn how toodelete an Azure Redis Cache.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="28a3d-105">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="28a3d-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/delete-cache/delete-cache.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="28a3d-106">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="28a3d-106">Script explanation</span></span>

<span data-ttu-id="28a3d-107">Этот скрипт использует hello, следующие команды toodelete экземпляр кэша Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="28a3d-107">This script uses hello following commands toodelete an Azure Redis Cache instance.</span></span> <span data-ttu-id="28a3d-108">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="28a3d-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="28a3d-109">Команда</span><span class="sxs-lookup"><span data-stu-id="28a3d-109">Command</span></span> | <span data-ttu-id="28a3d-110">Примечания</span><span class="sxs-lookup"><span data-stu-id="28a3d-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="28a3d-111">az redis delete</span><span class="sxs-lookup"><span data-stu-id="28a3d-111">az redis delete</span></span>](https://docs.microsoft.com/cli/azure/redis#delete) | <span data-ttu-id="28a3d-112">Удаляет экземпляр кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="28a3d-112">Delete Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="28a3d-113">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="28a3d-113">Next steps</span></span>

<span data-ttu-id="28a3d-114">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="28a3d-114">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="28a3d-115">Дополнительные образцы сценариев CLI кэша Redis Azure можно найти в hello [документации кэш Azure Redis](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="28a3d-115">Additional Azure Redis Cache CLI script samples can be found in hello [Azure Redis Cache documentation](../cli-samples.md).</span></span>
