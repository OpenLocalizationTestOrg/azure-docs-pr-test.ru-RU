---
title: "Образец скрипта CLI - aaaAzure подключения tooa redis веб-приложения кэша | Документы Microsoft"
description: "Сценарий Azure CLI пример — подключить кэш redis tooa web app"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: bc8345b2-8487-40c6-a91f-77414e8688e6
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: b911e6643591b8f07aeb64d4d62876c0fa156a8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-redis-cache"></a><span data-ttu-id="dc672-103">Подключение веб-приложения tooa redis кэша</span><span class="sxs-lookup"><span data-stu-id="dc672-103">Connect a web app tooa redis cache</span></span>

<span data-ttu-id="dc672-104">В этом сценарии вы узнаете, как toocreate Azure redis кэша и Azure веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="dc672-104">In this scenario you will learn how toocreate an Azure redis cache and an Azure web app.</span></span> <span data-ttu-id="dc672-105">Затем будет связан hello redis кэша toohello веб-приложения с помощью параметров приложения.</span><span class="sxs-lookup"><span data-stu-id="dc672-105">Then you will link hello redis cache toohello web app using app settings.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="dc672-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="dc672-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-redis/connect-to-redis.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="dc672-107">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="dc672-107">Script explanation</span></span>

<span data-ttu-id="dc672-108">Этот скрипт использует hello, следующие команды redis toocreate группу ресурсов веб-приложения, кэш и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="dc672-108">This script uses hello following commands toocreate a resource group, web app, redis cache and all related resources.</span></span> <span data-ttu-id="dc672-109">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="dc672-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="dc672-110">Команда</span><span class="sxs-lookup"><span data-stu-id="dc672-110">Command</span></span> | <span data-ttu-id="dc672-111">Примечания</span><span class="sxs-lookup"><span data-stu-id="dc672-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="dc672-112">az group create</span><span class="sxs-lookup"><span data-stu-id="dc672-112">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="dc672-113">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="dc672-113">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="dc672-114">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="dc672-114">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="dc672-115">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="dc672-115">Creates an App Service plan.</span></span> <span data-ttu-id="dc672-116">Это как ферма сервера для веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="dc672-116">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="dc672-117">az webapp create</span><span class="sxs-lookup"><span data-stu-id="dc672-117">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="dc672-118">Создает веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="dc672-118">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="dc672-119">az redis create</span><span class="sxs-lookup"><span data-stu-id="dc672-119">az redis create</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#create) | <span data-ttu-id="dc672-120">Создает экземпляр кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="dc672-120">Create new Redis Cache instance.</span></span> <span data-ttu-id="dc672-121">Это происходит, где будут храниться данные hello.</span><span class="sxs-lookup"><span data-stu-id="dc672-121">This is where hello data will be stored.</span></span> |
| [<span data-ttu-id="dc672-122">az redis list-keys</span><span class="sxs-lookup"><span data-stu-id="dc672-122">az redis list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#list-keys) | <span data-ttu-id="dc672-123">Список ключей доступа hello для экземпляра кэша redis hello.</span><span class="sxs-lookup"><span data-stu-id="dc672-123">Lists hello access keys for hello redis cache instance.</span></span> |
| [<span data-ttu-id="dc672-124">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="dc672-124">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="dc672-125">Создает или обновляет параметр приложения для веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="dc672-125">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="dc672-126">Параметры приложения представляются в качестве переменных среды для приложения.</span><span class="sxs-lookup"><span data-stu-id="dc672-126">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dc672-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dc672-127">Next steps</span></span>

<span data-ttu-id="dc672-128">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dc672-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="dc672-129">Дополнительные образцы сценариев CLI приложения службы можно найти в hello [документации по службе приложений Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="dc672-129">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
