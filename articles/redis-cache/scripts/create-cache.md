---
title: "Пример сценария CLI - aaaAzure создать кэш Azure Redis | Документы Microsoft"
description: "Пример сценария Azure CLI. Создание кэша Redis для Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: afd7f6e0-9297-4c98-a95e-597be939cef7
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: 85b007a426fbd4752034ec8663835963d140dd75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-redis-cache"></a><span data-ttu-id="a3482-103">Создание кэша Redis для Azure</span><span class="sxs-lookup"><span data-stu-id="a3482-103">Create an Azure Redis Cache</span></span>

<span data-ttu-id="a3482-104">В этом сценарии вы узнаете, как toocreate Redis для Azure кэша.</span><span class="sxs-lookup"><span data-stu-id="a3482-104">In this scenario, you learn how toocreate an Azure Redis Cache.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="a3482-105">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="a3482-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/create-cache/create-cache.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="a3482-106">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="a3482-106">Script explanation</span></span>

<span data-ttu-id="a3482-107">Этот скрипт использует следующие команды toocreate hello, группу ресурсов и кэш redis.</span><span class="sxs-lookup"><span data-stu-id="a3482-107">This script uses hello following commands toocreate a resource group and a redis cache.</span></span> <span data-ttu-id="a3482-108">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="a3482-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a3482-109">Команда</span><span class="sxs-lookup"><span data-stu-id="a3482-109">Command</span></span> | <span data-ttu-id="a3482-110">Примечания</span><span class="sxs-lookup"><span data-stu-id="a3482-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a3482-111">az group create</span><span class="sxs-lookup"><span data-stu-id="a3482-111">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="a3482-112">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="a3482-112">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a3482-113">az redis create</span><span class="sxs-lookup"><span data-stu-id="a3482-113">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="a3482-114">Создает экземпляр кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="a3482-114">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="a3482-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a3482-115">Next steps</span></span>

<span data-ttu-id="a3482-116">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a3482-116">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a3482-117">Дополнительные образцы сценариев CLI кэша Redis Azure можно найти в hello [документации кэш Azure Redis](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a3482-117">Additional Azure Redis Cache CLI script samples can be found in hello [Azure Redis Cache documentation](../cli-samples.md).</span></span>
