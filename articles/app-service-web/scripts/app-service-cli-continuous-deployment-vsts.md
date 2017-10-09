---
title: "Пример сценария CLI - aaaAzure Создание веб-приложения с непрерывным развертыванием из Visual Studio Team Services | Документы Microsoft"
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
ms.openlocfilehash: f8d0c2645ec5311296ca9b2df20f97e77bab2283
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-visual-studio-team-services"></a><span data-ttu-id="cab3a-103">Создание веб-приложения с непрерывным развертыванием из Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="cab3a-103">Create a web app with continuous deployment from Visual Studio Team Services</span></span>

<span data-ttu-id="cab3a-104">Этот пример сценария создает веб-приложение в службе приложений со связанными ресурсами, а затем настраивает непрерывное развертывание из репозитория Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="cab3a-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a Visual Studio Team Services repository.</span></span> <span data-ttu-id="cab3a-105">Для этого примера потребуется:</span><span class="sxs-lookup"><span data-stu-id="cab3a-105">For this sample, you will need:</span></span>

* <span data-ttu-id="cab3a-106">Репозиторий Visual Studio Team Services с кодом приложения, для которого у вас есть права администратора.</span><span class="sxs-lookup"><span data-stu-id="cab3a-106">A Visual Studio Team Services repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="cab3a-107">[Личный маркер доступа](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) для учетной записи Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="cab3a-107">A [Personal Access Token (PAT)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) for your Visual Studio Team Services account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="cab3a-108">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="cab3a-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="cab3a-109">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="cab3a-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="cab3a-110">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="cab3a-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="cab3a-111">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="cab3a-111">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-vsts-continuous/deploy-vsts-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from Visual Studio Team Services")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="cab3a-112">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="cab3a-112">Script explanation</span></span>

<span data-ttu-id="cab3a-113">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="cab3a-113">This script uses hello following commands.</span></span> <span data-ttu-id="cab3a-114">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="cab3a-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="cab3a-115">Команда</span><span class="sxs-lookup"><span data-stu-id="cab3a-115">Command</span></span> | <span data-ttu-id="cab3a-116">Примечания</span><span class="sxs-lookup"><span data-stu-id="cab3a-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="cab3a-117">az group create</span><span class="sxs-lookup"><span data-stu-id="cab3a-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="cab3a-118">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="cab3a-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="cab3a-119">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="cab3a-119">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="cab3a-120">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="cab3a-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="cab3a-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="cab3a-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="cab3a-122">Создает веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="cab3a-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="cab3a-123">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="cab3a-123">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="cab3a-124">Связывает веб-приложение Azure с репозиторием Git или Mercurial.</span><span class="sxs-lookup"><span data-stu-id="cab3a-124">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="cab3a-125">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="cab3a-125">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="cab3a-126">Открывает веб-приложение Azure в браузере.</span><span class="sxs-lookup"><span data-stu-id="cab3a-126">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="cab3a-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cab3a-127">Next steps</span></span>

<span data-ttu-id="cab3a-128">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cab3a-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="cab3a-129">Дополнительные образцы сценариев CLI приложения службы можно найти в hello [документации по службе приложений Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="cab3a-129">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
