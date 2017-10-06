---
title: "Пример сценария CLI - aaaAzure масштабировать веб-приложения по всему миру с архитектурой высокой доступности | Документы Microsoft"
description: "Пример скрипта Azure CLI. Глобальное масштабирование веб-приложения с помощью высокодоступной архитектуры"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: e4033a50-0e05-4505-8ce8-c876204b2acc
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: b72fbccd7f2aaab58e4b4721e14dca14146c7c72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="e538d-103">Глобальное масштабирование веб-приложения с помощью высокодоступной архитектуры</span><span class="sxs-lookup"><span data-stu-id="e538d-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="e538d-104">В этом сценарии вы создадите группу ресурсов, два плана службы приложений, два веб-приложения, профиль и две конечные точки диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="e538d-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="e538d-105">После завершения hello упражнении будет высокой, доступных архитектуру, позволяющую предоставляет общедоступный веб-приложения на основе минимальной задержки сети hello.</span><span class="sxs-lookup"><span data-stu-id="e538d-105">Once hello exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on hello lowest network latency.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e538d-106">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="e538d-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="e538d-107">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="e538d-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="e538d-108">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e538d-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="e538d-109">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="e538d-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-geographic/scale-geographic.sh "Geographic Scale")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="e538d-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="e538d-110">Script explanation</span></span>

<span data-ttu-id="e538d-111">Этот скрипт использует следующие команды toocreate группы ресурсов, веб-приложения, профиль диспетчера трафика hello и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="e538d-111">This script uses hello following commands toocreate a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="e538d-112">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="e538d-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e538d-113">Команда</span><span class="sxs-lookup"><span data-stu-id="e538d-113">Command</span></span> | <span data-ttu-id="e538d-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="e538d-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e538d-115">az group create</span><span class="sxs-lookup"><span data-stu-id="e538d-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e538d-116">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="e538d-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e538d-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="e538d-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="e538d-118">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="e538d-118">Creates an App Service plan.</span></span> <span data-ttu-id="e538d-119">Это как ферма сервера для веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="e538d-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="e538d-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="e538d-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="e538d-121">Создает веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="e538d-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="e538d-122">az network traffic-manager profile create</span><span class="sxs-lookup"><span data-stu-id="e538d-122">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="e538d-123">Создает профиль диспетчера трафика Azure.</span><span class="sxs-lookup"><span data-stu-id="e538d-123">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="e538d-124">az network traffic-manager endpoint create</span><span class="sxs-lookup"><span data-stu-id="e538d-124">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="e538d-125">Добавляет конечную точку tooan профиль диспетчера трафика Azure.</span><span class="sxs-lookup"><span data-stu-id="e538d-125">Adds a endpoint tooan Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e538d-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e538d-126">Next steps</span></span>

<span data-ttu-id="e538d-127">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e538d-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e538d-128">Дополнительные образцы сценариев CLI приложения службы можно найти в hello [документации по службе приложений Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e538d-128">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
