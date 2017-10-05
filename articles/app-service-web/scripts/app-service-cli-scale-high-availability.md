---
title: "Пример скрипта Azure CLI. Глобальное масштабирование веб-приложения с помощью высокодоступной архитектуры | Документация Майкрософт"
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
ms.openlocfilehash: c368bdc48f197ff5b491d1796d85abfd339051a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="eb41e-103">Глобальное масштабирование веб-приложения с помощью высокодоступной архитектуры</span><span class="sxs-lookup"><span data-stu-id="eb41e-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="eb41e-104">В этом сценарии вы создадите группу ресурсов, два плана службы приложений, два веб-приложения, профиль и две конечные точки диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="eb41e-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="eb41e-105">Завершив его, вы получите высокодоступную архитектуру, обеспечивающую глобальную доступность веб-приложения на основе минимальной задержки сети.</span><span class="sxs-lookup"><span data-stu-id="eb41e-105">Once the exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on the lowest network latency.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="eb41e-106">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="eb41e-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="eb41e-107">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="eb41e-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="eb41e-108">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="eb41e-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="eb41e-109">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="eb41e-109">Sample script</span></span>

<span data-ttu-id="eb41e-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-geographic/scale-geographic.sh "Географическое масштабирование")]</span><span class="sxs-lookup"><span data-stu-id="eb41e-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-geographic/scale-geographic.sh "Geographic Scale")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="eb41e-111">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="eb41e-111">Script explanation</span></span>

<span data-ttu-id="eb41e-112">Для создания группы ресурсов, веб-приложения, профиля диспетчера трафика и всех связанных ресурсов этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="eb41e-112">This script uses the following commands to create a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="eb41e-113">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="eb41e-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="eb41e-114">Команда</span><span class="sxs-lookup"><span data-stu-id="eb41e-114">Command</span></span> | <span data-ttu-id="eb41e-115">Примечания</span><span class="sxs-lookup"><span data-stu-id="eb41e-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="eb41e-116">az group create</span><span class="sxs-lookup"><span data-stu-id="eb41e-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="eb41e-117">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="eb41e-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="eb41e-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="eb41e-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="eb41e-119">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="eb41e-119">Creates an App Service plan.</span></span> <span data-ttu-id="eb41e-120">Это как ферма сервера для веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="eb41e-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="eb41e-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="eb41e-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="eb41e-122">Создает веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="eb41e-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="eb41e-123">az network traffic-manager profile create</span><span class="sxs-lookup"><span data-stu-id="eb41e-123">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="eb41e-124">Создает профиль диспетчера трафика Azure.</span><span class="sxs-lookup"><span data-stu-id="eb41e-124">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="eb41e-125">az network traffic-manager endpoint create</span><span class="sxs-lookup"><span data-stu-id="eb41e-125">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="eb41e-126">Добавляет конечную точку в профиль диспетчера трафика Azure.</span><span class="sxs-lookup"><span data-stu-id="eb41e-126">Adds a endpoint to an Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="eb41e-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="eb41e-127">Next steps</span></span>

<span data-ttu-id="eb41e-128">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="eb41e-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="eb41e-129">Дополнительные примеры скриптов Azure CLI для службы приложений см. в [документации по службе приложений Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="eb41e-129">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
