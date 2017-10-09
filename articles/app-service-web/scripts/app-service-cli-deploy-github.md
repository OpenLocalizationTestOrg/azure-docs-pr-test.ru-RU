---
title: "Пример сценария CLI - aaaAzure создать веб-приложения при развертывании из GitHub | Документы Microsoft"
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
ms.openlocfilehash: eb7231aa5c6a7e23d76885107e733008382f7487
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-deployment-from-github"></a><span data-ttu-id="bb296-103">Создание веб-приложения с развертыванием из GitHub</span><span class="sxs-lookup"><span data-stu-id="bb296-103">Create a web app with deployment from GitHub</span></span>

<span data-ttu-id="bb296-104">Этот пример скрипта создает веб-приложение в службе приложений со связанными ресурсами, а затем развертывает код веб-приложения из открытого репозитория GitHub (без непрерывного развертывания).</span><span class="sxs-lookup"><span data-stu-id="bb296-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="bb296-105">Дополнительные сведения о непрерывном развертывании на GitHub см. в статье [Создание веб-приложения с непрерывным развертыванием из GitHub](app-service-cli-continuous-deployment-github.md).</span><span class="sxs-lookup"><span data-stu-id="bb296-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-cli-continuous-deployment-github.md).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="bb296-106">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="bb296-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="bb296-107">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="bb296-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="bb296-108">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="bb296-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="bb296-109">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="bb296-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github/deploy-github.sh?highlight=3 "Create a web app with deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="bb296-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="bb296-110">Script explanation</span></span> 

<span data-ttu-id="bb296-111">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="bb296-111">This script uses hello following commands.</span></span> <span data-ttu-id="bb296-112">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="bb296-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="bb296-113">Команда</span><span class="sxs-lookup"><span data-stu-id="bb296-113">Command</span></span> | <span data-ttu-id="bb296-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="bb296-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="bb296-115">az group create</span><span class="sxs-lookup"><span data-stu-id="bb296-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="bb296-116">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="bb296-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="bb296-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="bb296-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="bb296-118">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="bb296-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="bb296-119">az webapp create</span><span class="sxs-lookup"><span data-stu-id="bb296-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="bb296-120">Создает веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="bb296-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="bb296-121">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="bb296-121">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="bb296-122">Связывает веб-приложение Azure с репозиторием Git или Mercurial.</span><span class="sxs-lookup"><span data-stu-id="bb296-122">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="bb296-123">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="bb296-123">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="bb296-124">Открывает веб-приложение Azure в браузере.</span><span class="sxs-lookup"><span data-stu-id="bb296-124">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bb296-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bb296-125">Next steps</span></span>

<span data-ttu-id="bb296-126">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bb296-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="bb296-127">Дополнительные образцы сценариев CLI приложения службы можно найти в hello [документации по службе приложений Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="bb296-127">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
