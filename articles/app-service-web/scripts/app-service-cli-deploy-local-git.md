---
title: "Образец скрипта CLI - aaaAzure создания веб-приложения и развертывания кода из локального репозитория Git | Документы Microsoft"
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
ms.openlocfilehash: 5ad75394c40025d8941282eabeaf34c19c72ee1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="101d8-103">Создание веб-приложения и развертывание кода из локального репозитория Git</span><span class="sxs-lookup"><span data-stu-id="101d8-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="101d8-104">Этот пример скрипта создает веб-приложение со связанными ресурсами в службе приложений, а затем развертывает код веб-приложения в локальном репозитории Git.</span><span class="sxs-lookup"><span data-stu-id="101d8-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="101d8-105">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="101d8-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="101d8-106">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="101d8-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="101d8-107">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="101d8-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="101d8-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="101d8-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-local-git/deploy-local-git.sh?highlight=3-5 "Create a web app and deploy code from a local Git repository")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="101d8-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="101d8-109">Script explanation</span></span>

<span data-ttu-id="101d8-110">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="101d8-110">This script uses hello following commands.</span></span> <span data-ttu-id="101d8-111">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="101d8-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="101d8-112">Команда</span><span class="sxs-lookup"><span data-stu-id="101d8-112">Command</span></span> | <span data-ttu-id="101d8-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="101d8-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="101d8-114">az group create</span><span class="sxs-lookup"><span data-stu-id="101d8-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="101d8-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="101d8-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="101d8-116">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="101d8-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="101d8-117">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="101d8-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="101d8-118">az webapp create</span><span class="sxs-lookup"><span data-stu-id="101d8-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="101d8-119">Создает веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="101d8-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="101d8-120">az webapp deployment user set</span><span class="sxs-lookup"><span data-stu-id="101d8-120">az webapp deployment user set</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/user#set) | <span data-ttu-id="101d8-121">Задает учетные данные развертывания на уровне учетной записи hello для приложения службы.</span><span class="sxs-lookup"><span data-stu-id="101d8-121">Sets hello account-level deployment credentials for App Service.</span></span> |
| [<span data-ttu-id="101d8-122">az webapp deployment source config-local-git</span><span class="sxs-lookup"><span data-stu-id="101d8-122">az webapp deployment source config-local-git</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/source#config-local-git) | <span data-ttu-id="101d8-123">Создает конфигурацию системы управления версиями для локального репозитория Git.</span><span class="sxs-lookup"><span data-stu-id="101d8-123">Creates a source control configuration for a local Git repository.</span></span> |
| [<span data-ttu-id="101d8-124">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="101d8-124">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="101d8-125">Открывает веб-приложение Azure в браузере.</span><span class="sxs-lookup"><span data-stu-id="101d8-125">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="101d8-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="101d8-126">Next steps</span></span>

<span data-ttu-id="101d8-127">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="101d8-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="101d8-128">Дополнительные образцы сценариев CLI приложения службы можно найти в hello [документации по службе приложений Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="101d8-128">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
