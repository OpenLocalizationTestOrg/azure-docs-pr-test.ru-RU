---
title: "Пример сценария CLI - aaaAzure Создание веб-приложения с непрерывным развертыванием из GitHub | Документы Microsoft"
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
ms.openlocfilehash: 6adb06a35ceea8ea64723c9887c25c50f046e280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="fc061-103">Создание веб-приложения с непрерывным развертыванием из GitHub</span><span class="sxs-lookup"><span data-stu-id="fc061-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="fc061-104">Этот пример скрипта создает веб-приложение в службе приложений со связанными ресурсами, а затем настраивает непрерывное развертывание из репозитория GitHub.</span><span class="sxs-lookup"><span data-stu-id="fc061-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="fc061-105">Дополнительные сведения о развертывании GitHub без непрерывного развертывания см. в статье [Создание веб-приложения и развертывание кода из GitHub](app-service-cli-deploy-github.md).</span><span class="sxs-lookup"><span data-stu-id="fc061-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-cli-deploy-github.md).</span></span> <span data-ttu-id="fc061-106">Для этого примера потребуется:</span><span class="sxs-lookup"><span data-stu-id="fc061-106">In this sample, you will need:</span></span>

* <span data-ttu-id="fc061-107">Репозиторий GitHub с кодом приложения, для которого у вас есть права администратора.</span><span class="sxs-lookup"><span data-stu-id="fc061-107">A GitHub repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="fc061-108">[Личный маркер доступа](https://help.github.com/articles/creating-an-access-token-for-command-line-use) для учетной записи GitHub.</span><span class="sxs-lookup"><span data-stu-id="fc061-108">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="fc061-109">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="fc061-109">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="fc061-110">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="fc061-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="fc061-111">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fc061-111">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="fc061-112">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="fc061-112">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github-continuous/deploy-github-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="fc061-113">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="fc061-113">Script explanation</span></span>

<span data-ttu-id="fc061-114">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="fc061-114">This script uses hello following commands.</span></span> <span data-ttu-id="fc061-115">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="fc061-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="fc061-116">Команда</span><span class="sxs-lookup"><span data-stu-id="fc061-116">Command</span></span> | <span data-ttu-id="fc061-117">Примечания</span><span class="sxs-lookup"><span data-stu-id="fc061-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fc061-118">az group create</span><span class="sxs-lookup"><span data-stu-id="fc061-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="fc061-119">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="fc061-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fc061-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="fc061-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="fc061-121">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="fc061-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="fc061-122">az webapp create</span><span class="sxs-lookup"><span data-stu-id="fc061-122">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="fc061-123">Создает веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="fc061-123">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="fc061-124">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="fc061-124">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="fc061-125">Связывает веб-приложение Azure с репозиторием Git или Mercurial.</span><span class="sxs-lookup"><span data-stu-id="fc061-125">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="fc061-126">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="fc061-126">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="fc061-127">Открывает веб-приложение Azure в браузере.</span><span class="sxs-lookup"><span data-stu-id="fc061-127">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fc061-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fc061-128">Next steps</span></span>

<span data-ttu-id="fc061-129">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fc061-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fc061-130">Дополнительные образцы сценариев CLI приложения службы можно найти в hello [документации по службе приложений Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="fc061-130">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
