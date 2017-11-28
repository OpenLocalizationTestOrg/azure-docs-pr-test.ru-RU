---
title: "aaaAzure образец скрипта CLI - создания веб-приложения и развертывания кода tooa промежуточной среде | Документы Microsoft"
description: "Пример сценария Azure CLI - создания веб-приложения и развертывания кода tooa промежуточной среде"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 2b995dcd-e471-4355-9fda-00babcdb156e
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: cd07f5eda31041effd7b7334f5ecc04e6c1a0514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-tooa-staging-environment"></a><span data-ttu-id="5c783-103">Создание веб-приложения и развертывание кода tooa промежуточной среде</span><span class="sxs-lookup"><span data-stu-id="5c783-103">Create a web app and deploy code tooa staging environment</span></span>

<span data-ttu-id="5c783-104">Этот образец скрипта создает веб-приложения в службе приложений слотом развертывания называется «промежуточный», а затем развернет toohello образец приложения, «промежуточный» слоте.</span><span class="sxs-lookup"><span data-stu-id="5c783-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app toohello "staging" slot.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5c783-105">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="5c783-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="5c783-106">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="5c783-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="5c783-107">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5c783-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="5c783-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="5c783-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.sh "Create a web app and deploy code tooa staging environment")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="5c783-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="5c783-109">Script explanation</span></span>

<span data-ttu-id="5c783-110">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="5c783-110">This script uses hello following commands.</span></span> <span data-ttu-id="5c783-111">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="5c783-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="5c783-112">Команда</span><span class="sxs-lookup"><span data-stu-id="5c783-112">Command</span></span> | <span data-ttu-id="5c783-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="5c783-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5c783-114">az group create</span><span class="sxs-lookup"><span data-stu-id="5c783-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="5c783-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="5c783-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5c783-116">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="5c783-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="5c783-117">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="5c783-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="5c783-118">az webapp create</span><span class="sxs-lookup"><span data-stu-id="5c783-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="5c783-119">Создает веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="5c783-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="5c783-120">az webapp deployment slot create</span><span class="sxs-lookup"><span data-stu-id="5c783-120">az webapp deployment slot create</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#create) | <span data-ttu-id="5c783-121">Создает слот развертывания.</span><span class="sxs-lookup"><span data-stu-id="5c783-121">Create a deployment slot.</span></span> |
| [<span data-ttu-id="5c783-122">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="5c783-122">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="5c783-123">Связывает веб-приложение Azure с репозиторием Git или Mercurial.</span><span class="sxs-lookup"><span data-stu-id="5c783-123">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="5c783-124">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="5c783-124">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="5c783-125">Открывает веб-приложение Azure в браузере.</span><span class="sxs-lookup"><span data-stu-id="5c783-125">Open an Azure web app in a browser.</span></span> |
| [<span data-ttu-id="5c783-126">az webapp deployment slot swap</span><span class="sxs-lookup"><span data-stu-id="5c783-126">az webapp deployment slot swap</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#swap) | <span data-ttu-id="5c783-127">Переключает указанный слот развертывания в рабочую среду.</span><span class="sxs-lookup"><span data-stu-id="5c783-127">Swap a specified deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5c783-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5c783-128">Next steps</span></span>

<span data-ttu-id="5c783-129">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5c783-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5c783-130">Дополнительные образцы сценариев CLI приложения службы можно найти в hello [документации по службе приложений Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5c783-130">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
