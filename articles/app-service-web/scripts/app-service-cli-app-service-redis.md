---
title: "Пример скрипта Azure CLI. Подключение веб-приложения к кэшу Redis | Документация Майкрософт"
description: "Пример скрипта Azure CLI. Подключение веб-приложения к кэшу Redis"
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
ms.openlocfilehash: b697c8508a6c3422b6b0d0ca36843a9c884b505f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-web-app-to-a-redis-cache"></a><span data-ttu-id="6820d-103">Подключение веб-приложения к кэшу Redis</span><span class="sxs-lookup"><span data-stu-id="6820d-103">Connect a web app to a redis cache</span></span>

<span data-ttu-id="6820d-104">Из этой статьи вы узнаете, как создать кэш Redis для Azure и веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="6820d-104">In this scenario you will learn how to create an Azure redis cache and an Azure web app.</span></span> <span data-ttu-id="6820d-105">Затем вы свяжете базу кэш Redis с веб-приложением, используя параметры приложения.</span><span class="sxs-lookup"><span data-stu-id="6820d-105">Then you will link the redis cache to the web app using app settings.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="6820d-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="6820d-106">Sample script</span></span>

<span data-ttu-id="6820d-107">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-redis/connect-to-redis.sh "Кэш Redis для Azure")]</span><span class="sxs-lookup"><span data-stu-id="6820d-107">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-redis/connect-to-redis.sh "Azure Redis Cache")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="6820d-108">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="6820d-108">Script explanation</span></span>

<span data-ttu-id="6820d-109">Для создания группы ресурсов, веб-приложения, кэша Redis и всех связанных ресурсов этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="6820d-109">This script uses the following commands to create a resource group, web app, redis cache and all related resources.</span></span> <span data-ttu-id="6820d-110">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="6820d-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6820d-111">Команда</span><span class="sxs-lookup"><span data-stu-id="6820d-111">Command</span></span> | <span data-ttu-id="6820d-112">Примечания</span><span class="sxs-lookup"><span data-stu-id="6820d-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6820d-113">az group create</span><span class="sxs-lookup"><span data-stu-id="6820d-113">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6820d-114">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="6820d-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6820d-115">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="6820d-115">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="6820d-116">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="6820d-116">Creates an App Service plan.</span></span> <span data-ttu-id="6820d-117">Это как ферма сервера для веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="6820d-117">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="6820d-118">az webapp create</span><span class="sxs-lookup"><span data-stu-id="6820d-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="6820d-119">Создает веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="6820d-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="6820d-120">az redis create</span><span class="sxs-lookup"><span data-stu-id="6820d-120">az redis create</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#create) | <span data-ttu-id="6820d-121">Создает экземпляр кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="6820d-121">Create new Redis Cache instance.</span></span> <span data-ttu-id="6820d-122">Здесь будут храниться данные.</span><span class="sxs-lookup"><span data-stu-id="6820d-122">This is where the data will be stored.</span></span> |
| [<span data-ttu-id="6820d-123">az redis list-keys</span><span class="sxs-lookup"><span data-stu-id="6820d-123">az redis list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#list-keys) | <span data-ttu-id="6820d-124">Создает список ключей доступа для экземпляра кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="6820d-124">Lists the access keys for the redis cache instance.</span></span> |
| [<span data-ttu-id="6820d-125">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="6820d-125">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="6820d-126">Создает или обновляет параметр приложения для веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="6820d-126">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="6820d-127">Параметры приложения представляются в качестве переменных среды для приложения.</span><span class="sxs-lookup"><span data-stu-id="6820d-127">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6820d-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6820d-128">Next steps</span></span>

<span data-ttu-id="6820d-129">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6820d-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6820d-130">Дополнительные примеры скриптов Azure CLI для службы приложений см. в [документации по службе приложений Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6820d-130">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
