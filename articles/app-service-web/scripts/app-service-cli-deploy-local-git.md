---
title: "Пример скрипта Azure CLI. Создание веб-приложения и развертывание кода из локального репозитория Git | Документация Майкрософт"
description: "Пример скрипта Azure CLI. Создание веб-приложения и развертывание кода из локального репозитория Git"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 048f98aa-f708-44cb-9b9e-953f67dc6da8
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 50d69ac48438920ce59808ee79809235d8330b14
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="522a9-103">Создание веб-приложения и развертывание кода из локального репозитория Git</span><span class="sxs-lookup"><span data-stu-id="522a9-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="522a9-104">Этот пример скрипта создает веб-приложение со связанными ресурсами в службе приложений, а затем развертывает код веб-приложения в локальном репозитории Git.</span><span class="sxs-lookup"><span data-stu-id="522a9-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="522a9-105">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="522a9-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="522a9-106">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="522a9-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="522a9-107">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="522a9-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="522a9-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="522a9-108">Sample script</span></span>

<span data-ttu-id="522a9-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-local-git/deploy-local-git.sh?highlight=3-5 "Создание веб-приложения и развертывание кода из локального репозитория Git")]</span><span class="sxs-lookup"><span data-stu-id="522a9-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-local-git/deploy-local-git.sh?highlight=3-5 "Create a web app and deploy code from a local Git repository")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="522a9-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="522a9-110">Script explanation</span></span>

<span data-ttu-id="522a9-111">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="522a9-111">This script uses the following commands.</span></span> <span data-ttu-id="522a9-112">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="522a9-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="522a9-113">Команда</span><span class="sxs-lookup"><span data-stu-id="522a9-113">Command</span></span> | <span data-ttu-id="522a9-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="522a9-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="522a9-115">az group create</span><span class="sxs-lookup"><span data-stu-id="522a9-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="522a9-116">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="522a9-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="522a9-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="522a9-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="522a9-118">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="522a9-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="522a9-119">az webapp create</span><span class="sxs-lookup"><span data-stu-id="522a9-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="522a9-120">Создает веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="522a9-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="522a9-121">az webapp deployment user set</span><span class="sxs-lookup"><span data-stu-id="522a9-121">az webapp deployment user set</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/user#set) | <span data-ttu-id="522a9-122">Настраивает учетные данные развертывания на уровне учетной записи для службы приложений.</span><span class="sxs-lookup"><span data-stu-id="522a9-122">Sets the account-level deployment credentials for App Service.</span></span> |
| [<span data-ttu-id="522a9-123">az webapp deployment source config-local-git</span><span class="sxs-lookup"><span data-stu-id="522a9-123">az webapp deployment source config-local-git</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/source#config-local-git) | <span data-ttu-id="522a9-124">Создает конфигурацию системы управления версиями для локального репозитория Git.</span><span class="sxs-lookup"><span data-stu-id="522a9-124">Creates a source control configuration for a local Git repository.</span></span> |
| [<span data-ttu-id="522a9-125">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="522a9-125">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="522a9-126">Открывает веб-приложение Azure в браузере.</span><span class="sxs-lookup"><span data-stu-id="522a9-126">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="522a9-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="522a9-127">Next steps</span></span>

<span data-ttu-id="522a9-128">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="522a9-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="522a9-129">Дополнительные примеры скриптов Azure CLI для службы приложений см. в [документации по службе приложений Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="522a9-129">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
