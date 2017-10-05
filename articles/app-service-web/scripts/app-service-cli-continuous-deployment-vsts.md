---
title: "Пример скрипта Azure CLI. Создание веб-приложения с непрерывным развертыванием из Visual Studio Team Services | Документация Майкрософт"
description: "Пример скрипта Azure CLI. Создание веб-приложения с непрерывным развертыванием из Visual Studio Team Services"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 389d3bd3-cd8e-4715-a3a1-031ec061d385
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 2b983616757ca3c4226c12876f5fd4c285067318
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-visual-studio-team-services"></a><span data-ttu-id="dcb70-103">Создание веб-приложения с непрерывным развертыванием из Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="dcb70-103">Create a web app with continuous deployment from Visual Studio Team Services</span></span>

<span data-ttu-id="dcb70-104">Этот пример сценария создает веб-приложение в службе приложений со связанными ресурсами, а затем настраивает непрерывное развертывание из репозитория Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="dcb70-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a Visual Studio Team Services repository.</span></span> <span data-ttu-id="dcb70-105">Для этого примера потребуется:</span><span class="sxs-lookup"><span data-stu-id="dcb70-105">For this sample, you will need:</span></span>

* <span data-ttu-id="dcb70-106">Репозиторий Visual Studio Team Services с кодом приложения, для которого у вас есть права администратора.</span><span class="sxs-lookup"><span data-stu-id="dcb70-106">A Visual Studio Team Services repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="dcb70-107">[Личный маркер доступа](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) для учетной записи Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="dcb70-107">A [Personal Access Token (PAT)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) for your Visual Studio Team Services account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="dcb70-108">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="dcb70-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="dcb70-109">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="dcb70-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="dcb70-110">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="dcb70-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="dcb70-111">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="dcb70-111">Sample script</span></span>

<span data-ttu-id="dcb70-112">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-vsts-continuous/deploy-vsts-continuous.sh?highlight=3-4 "Создание веб-приложения с непрерывным развертыванием из Visual Studio Team Services")]</span><span class="sxs-lookup"><span data-stu-id="dcb70-112">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-vsts-continuous/deploy-vsts-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from Visual Studio Team Services")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="dcb70-113">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="dcb70-113">Script explanation</span></span>

<span data-ttu-id="dcb70-114">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="dcb70-114">This script uses the following commands.</span></span> <span data-ttu-id="dcb70-115">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="dcb70-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="dcb70-116">Команда</span><span class="sxs-lookup"><span data-stu-id="dcb70-116">Command</span></span> | <span data-ttu-id="dcb70-117">Примечания</span><span class="sxs-lookup"><span data-stu-id="dcb70-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="dcb70-118">az group create</span><span class="sxs-lookup"><span data-stu-id="dcb70-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="dcb70-119">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="dcb70-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="dcb70-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="dcb70-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="dcb70-121">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="dcb70-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="dcb70-122">az webapp create</span><span class="sxs-lookup"><span data-stu-id="dcb70-122">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="dcb70-123">Создает веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="dcb70-123">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="dcb70-124">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="dcb70-124">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="dcb70-125">Связывает веб-приложение Azure с репозиторием Git или Mercurial.</span><span class="sxs-lookup"><span data-stu-id="dcb70-125">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="dcb70-126">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="dcb70-126">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="dcb70-127">Открывает веб-приложение Azure в браузере.</span><span class="sxs-lookup"><span data-stu-id="dcb70-127">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dcb70-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dcb70-128">Next steps</span></span>

<span data-ttu-id="dcb70-129">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dcb70-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="dcb70-130">Дополнительные примеры скриптов Azure CLI для службы приложений см. в [документации по службе приложений Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="dcb70-130">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
