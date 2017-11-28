---
title: "Пример сценария CLI - aaaAzure масштабировать веб-приложения вручную с помощью Azure CLI 2.0 | Документы Microsoft"
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
ms.openlocfilehash: 64464c8a44522fdc2c8f3d0192388302a1d12667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="40fb2-103">Масштабирование веб-приложения вручную</span><span class="sxs-lookup"><span data-stu-id="40fb2-103">Scale a web app manually</span></span>

<span data-ttu-id="40fb2-104">В этом сценарии вы узнаете toocreate группу ресурсов, приложение службы плана и веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="40fb2-104">In this scenario you will learn toocreate a resource group, app service plan and web app.</span></span> <span data-ttu-id="40fb2-105">Затем будет масштабироваться hello план служб приложений из toomultiple единственных экземпляров.</span><span class="sxs-lookup"><span data-stu-id="40fb2-105">You will then scale hello App Service Plan from a single instance toomultiple instances.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="40fb2-106">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="40fb2-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="40fb2-107">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="40fb2-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="40fb2-108">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="40fb2-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="40fb2-109">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="40fb2-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-manual/scale-manual.sh "Manual Scale")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="40fb2-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="40fb2-110">Script explanation</span></span>

<span data-ttu-id="40fb2-111">Этот скрипт использует hello следующие команды toocreate группы ресурсов, веб-приложения и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="40fb2-111">This script uses hello following commands toocreate a resource group, web app, and all related resources.</span></span> <span data-ttu-id="40fb2-112">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="40fb2-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="40fb2-113">Команда</span><span class="sxs-lookup"><span data-stu-id="40fb2-113">Command</span></span> | <span data-ttu-id="40fb2-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="40fb2-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="40fb2-115">az group create</span><span class="sxs-lookup"><span data-stu-id="40fb2-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="40fb2-116">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="40fb2-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="40fb2-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="40fb2-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="40fb2-118">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="40fb2-118">Creates an App Service plan.</span></span> <span data-ttu-id="40fb2-119">Это как ферма сервера для веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="40fb2-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="40fb2-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="40fb2-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="40fb2-121">Создает веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="40fb2-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="40fb2-122">az appservice plan update</span><span class="sxs-lookup"><span data-stu-id="40fb2-122">az appservice plan update</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#update) | <span data-ttu-id="40fb2-123">Обновляет свойства hello план служб приложений.</span><span class="sxs-lookup"><span data-stu-id="40fb2-123">Updates properties of hello App Service plan.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="40fb2-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="40fb2-124">Next steps</span></span>

<span data-ttu-id="40fb2-125">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="40fb2-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="40fb2-126">Дополнительные образцы сценариев CLI приложения службы можно найти в hello [документации по службе приложений Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="40fb2-126">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
