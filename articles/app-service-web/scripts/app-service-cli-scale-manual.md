---
title: "Пример скрипта Azure CLI. Масштабирование веб-приложения вручную с помощью Azure CLI 2.0 | Документация Майкрософт"
description: "Пример скрипта Azure CLI. Масштабирование веб-приложения вручную с помощью Azure CLI 2.0"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 251d9074-8fff-4121-ad16-9eca9556ac96
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: fe05661eb4e2d5c37aebdbfde002b34588db69e7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="d3dee-103">Масштабирование веб-приложения вручную</span><span class="sxs-lookup"><span data-stu-id="d3dee-103">Scale a web app manually</span></span>

<span data-ttu-id="d3dee-104">В этой статье вы узнаете, как создать группу ресурсов, план службы приложений и веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="d3dee-104">In this scenario you will learn to create a resource group, app service plan and web app.</span></span> <span data-ttu-id="d3dee-105">Затем вы выполните масштабирование плана службы приложений от одного экземпляра до нескольких.</span><span class="sxs-lookup"><span data-stu-id="d3dee-105">You will then scale the App Service Plan from a single instance to multiple instances.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d3dee-106">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="d3dee-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="d3dee-107">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="d3dee-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="d3dee-108">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d3dee-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="d3dee-109">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="d3dee-109">Sample script</span></span>

<span data-ttu-id="d3dee-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-manual/scale-manual.sh "Масштабирование вручную")]</span><span class="sxs-lookup"><span data-stu-id="d3dee-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-manual/scale-manual.sh "Manual Scale")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="d3dee-111">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="d3dee-111">Script explanation</span></span>

<span data-ttu-id="d3dee-112">Для создания группы ресурсов, веб-приложений и всех связанных с ними ресурсов этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="d3dee-112">This script uses the following commands to create a resource group, web app, and all related resources.</span></span> <span data-ttu-id="d3dee-113">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="d3dee-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d3dee-114">Команда</span><span class="sxs-lookup"><span data-stu-id="d3dee-114">Command</span></span> | <span data-ttu-id="d3dee-115">Примечания</span><span class="sxs-lookup"><span data-stu-id="d3dee-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d3dee-116">az group create</span><span class="sxs-lookup"><span data-stu-id="d3dee-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="d3dee-117">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d3dee-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d3dee-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="d3dee-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="d3dee-119">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="d3dee-119">Creates an App Service plan.</span></span> <span data-ttu-id="d3dee-120">Это как ферма сервера для веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="d3dee-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="d3dee-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="d3dee-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="d3dee-122">Создает веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="d3dee-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="d3dee-123">az appservice plan update</span><span class="sxs-lookup"><span data-stu-id="d3dee-123">az appservice plan update</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#update) | <span data-ttu-id="d3dee-124">Обновляет свойства плана службы приложений.</span><span class="sxs-lookup"><span data-stu-id="d3dee-124">Updates properties of the App Service plan.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d3dee-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d3dee-125">Next steps</span></span>

<span data-ttu-id="d3dee-126">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d3dee-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d3dee-127">Дополнительные примеры скриптов Azure CLI для службы приложений см. в [документации по службе приложений Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d3dee-127">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
