---
title: "Пример скрипта Azure CLI. Создание веб-приложения с непрерывным развертыванием из GitHub | Документация Майкрософт"
description: "Пример скрипта Azure CLI. Создание веб-приложения с непрерывным развертыванием из GitHub"
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
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: a12085a7a8146c22d6b079381542d4fe3a8e6e87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="91051-103">Создание веб-приложения с непрерывным развертыванием из GitHub</span><span class="sxs-lookup"><span data-stu-id="91051-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="91051-104">Этот пример скрипта создает веб-приложение в службе приложений со связанными ресурсами, а затем настраивает непрерывное развертывание из репозитория GitHub.</span><span class="sxs-lookup"><span data-stu-id="91051-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="91051-105">Дополнительные сведения о развертывании GitHub без непрерывного развертывания см. в статье [Создание веб-приложения и развертывание кода из GitHub](app-service-cli-deploy-github.md).</span><span class="sxs-lookup"><span data-stu-id="91051-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-cli-deploy-github.md).</span></span> <span data-ttu-id="91051-106">Для этого примера потребуется:</span><span class="sxs-lookup"><span data-stu-id="91051-106">In this sample, you will need:</span></span>

* <span data-ttu-id="91051-107">Репозиторий GitHub с кодом приложения, для которого у вас есть права администратора.</span><span class="sxs-lookup"><span data-stu-id="91051-107">A GitHub repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="91051-108">[Личный маркер доступа](https://help.github.com/articles/creating-an-access-token-for-command-line-use) для учетной записи GitHub.</span><span class="sxs-lookup"><span data-stu-id="91051-108">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="91051-109">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="91051-109">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="91051-110">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="91051-110">Run `az --version` to find the version.</span></span> <span data-ttu-id="91051-111">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="91051-111">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="91051-112">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="91051-112">Sample script</span></span>

<span data-ttu-id="91051-113">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github-continuous/deploy-github-continuous.sh?highlight=3-4 "Создание веб-приложения с непрерывным развертыванием из GitHub")]</span><span class="sxs-lookup"><span data-stu-id="91051-113">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github-continuous/deploy-github-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from GitHub")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="91051-114">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="91051-114">Script explanation</span></span>

<span data-ttu-id="91051-115">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="91051-115">This script uses the following commands.</span></span> <span data-ttu-id="91051-116">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="91051-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="91051-117">Команда</span><span class="sxs-lookup"><span data-stu-id="91051-117">Command</span></span> | <span data-ttu-id="91051-118">Примечания</span><span class="sxs-lookup"><span data-stu-id="91051-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="91051-119">az group create</span><span class="sxs-lookup"><span data-stu-id="91051-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="91051-120">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="91051-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="91051-121">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="91051-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="91051-122">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="91051-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="91051-123">az webapp create</span><span class="sxs-lookup"><span data-stu-id="91051-123">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="91051-124">Создает веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="91051-124">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="91051-125">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="91051-125">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="91051-126">Связывает веб-приложение Azure с репозиторием Git или Mercurial.</span><span class="sxs-lookup"><span data-stu-id="91051-126">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="91051-127">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="91051-127">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="91051-128">Открывает веб-приложение Azure в браузере.</span><span class="sxs-lookup"><span data-stu-id="91051-128">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="91051-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="91051-129">Next steps</span></span>

<span data-ttu-id="91051-130">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="91051-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="91051-131">Дополнительные примеры скриптов Azure CLI для службы приложений см. в [документации по службе приложений Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="91051-131">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
