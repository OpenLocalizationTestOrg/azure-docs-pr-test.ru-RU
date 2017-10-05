---
title: "Пример скрипта Azure CLI. Создание веб-приложения ASP.NET Core в контейнере Docker | Документация Майкрософт"
description: "Пример скрипта Azure CLI. Создание веб-приложения ASP.NET Core в контейнере Docker"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 3a2d1983-ff7b-476a-ac44-49ec2aabb31a
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 5d1e2c7d2815df5fb9c176ec290a18d330ea3f7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-aspnet-core-web-app-in-a-docker-container"></a><span data-ttu-id="ff248-103">Создание веб-приложения ASP.NET Core в контейнере Docker</span><span class="sxs-lookup"><span data-stu-id="ff248-103">Create an ASP.NET Core web app in a Docker container</span></span>

<span data-ttu-id="ff248-104">В этом сценарии вы узнаете, как создать группу ресурсов, план службы приложений Linux и веб-приложение, а также как развернуть приложение ASP.NET Core, используя контейнер Docker.</span><span class="sxs-lookup"><span data-stu-id="ff248-104">In this scenario you will learn how to create a resource group, Linux app service plan, and web app, and deploy an ASP.NET Core application using a Docker Container.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ff248-105">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="ff248-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ff248-106">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="ff248-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="ff248-107">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ff248-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="ff248-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="ff248-108">Sample script</span></span>

<span data-ttu-id="ff248-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-linux-docker/deploy-linux-docker.sh?highlight=6 "Docker в Linux")]</span><span class="sxs-lookup"><span data-stu-id="ff248-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-linux-docker/deploy-linux-docker.sh?highlight=6 "Linux Docker")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="ff248-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="ff248-110">Script explanation</span></span>

<span data-ttu-id="ff248-111">Для создания группы ресурсов, веб-приложений и всех связанных с ними ресурсов этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="ff248-111">This script uses the following commands to create a resource group, web app, and all related resources.</span></span> <span data-ttu-id="ff248-112">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="ff248-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ff248-113">Команда</span><span class="sxs-lookup"><span data-stu-id="ff248-113">Command</span></span> | <span data-ttu-id="ff248-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="ff248-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ff248-115">az group create</span><span class="sxs-lookup"><span data-stu-id="ff248-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ff248-116">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="ff248-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ff248-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="ff248-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="ff248-118">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="ff248-118">Creates an App Service plan.</span></span> <span data-ttu-id="ff248-119">Это как ферма сервера для веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="ff248-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="ff248-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="ff248-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="ff248-121">Создает веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="ff248-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="ff248-122">az webapp config container set</span><span class="sxs-lookup"><span data-stu-id="ff248-122">az webapp config container set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/container#set) | <span data-ttu-id="ff248-123">Настраивает контейнер Docker для веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="ff248-123">Sets the Docker container for the Azure web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ff248-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ff248-124">Next steps</span></span>

<span data-ttu-id="ff248-125">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ff248-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ff248-126">Дополнительные примеры скриптов Azure CLI для службы приложений см. в [документации по службе приложений Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ff248-126">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
