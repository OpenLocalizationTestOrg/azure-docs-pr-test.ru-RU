---
title: "Пример скрипта Azure CLI. Создание веб-приложения с развертыванием из GitHub | Документация Майкрософт"
description: "Пример скрипта Azure CLI. Создание веб-приложения с развертыванием из GitHub"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0205c991-0989-4ca3-bb41-237dcc964460
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: sample
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 61e9d65319cecf3ea4e9152ebdf1035566aad74c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-with-deployment-from-github"></a><span data-ttu-id="7af95-103">Создание веб-приложения с развертыванием из GitHub</span><span class="sxs-lookup"><span data-stu-id="7af95-103">Create a web app with deployment from GitHub</span></span>

<span data-ttu-id="7af95-104">Этот пример скрипта создает веб-приложение в службе приложений со связанными ресурсами, а затем развертывает код веб-приложения из открытого репозитория GitHub (без непрерывного развертывания).</span><span class="sxs-lookup"><span data-stu-id="7af95-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="7af95-105">Дополнительные сведения о непрерывном развертывании на GitHub см. в статье [Создание веб-приложения с непрерывным развертыванием из GitHub](app-service-cli-continuous-deployment-github.md).</span><span class="sxs-lookup"><span data-stu-id="7af95-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-cli-continuous-deployment-github.md).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7af95-106">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="7af95-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="7af95-107">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="7af95-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="7af95-108">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7af95-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="7af95-109">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="7af95-109">Sample script</span></span>

<span data-ttu-id="7af95-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github/deploy-github.sh?highlight=3 "Создание веб-приложения с развертыванием из GitHub")]</span><span class="sxs-lookup"><span data-stu-id="7af95-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github/deploy-github.sh?highlight=3 "Create a web app with deployment from GitHub")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="7af95-111">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="7af95-111">Script explanation</span></span> 

<span data-ttu-id="7af95-112">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="7af95-112">This script uses the following commands.</span></span> <span data-ttu-id="7af95-113">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="7af95-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="7af95-114">Команда</span><span class="sxs-lookup"><span data-stu-id="7af95-114">Command</span></span> | <span data-ttu-id="7af95-115">Примечания</span><span class="sxs-lookup"><span data-stu-id="7af95-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7af95-116">az group create</span><span class="sxs-lookup"><span data-stu-id="7af95-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="7af95-117">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="7af95-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7af95-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="7af95-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="7af95-119">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="7af95-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="7af95-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="7af95-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="7af95-121">Создает веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="7af95-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="7af95-122">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="7af95-122">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="7af95-123">Связывает веб-приложение Azure с репозиторием Git или Mercurial.</span><span class="sxs-lookup"><span data-stu-id="7af95-123">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="7af95-124">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="7af95-124">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="7af95-125">Открывает веб-приложение Azure в браузере.</span><span class="sxs-lookup"><span data-stu-id="7af95-125">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7af95-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7af95-126">Next steps</span></span>

<span data-ttu-id="7af95-127">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7af95-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7af95-128">Дополнительные примеры скриптов Azure CLI для службы приложений см. в [документации по службе приложений Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7af95-128">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
