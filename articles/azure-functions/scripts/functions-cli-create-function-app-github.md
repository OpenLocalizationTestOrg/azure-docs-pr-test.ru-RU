---
title: "aaaCreate приложения функции и развертывать код функции из GitHub | Документы Microsoft"
description: "Пример сценария Azure CLI для создания приложения-функции и развертывание кода функции из GitHub."
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: 026886f11909149db695d9a52d0aa37f109f64e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-and-deploy-function-code-from-github"></a><span data-ttu-id="3db16-103">Создание приложения-функции и развертывание кода функции из GitHub</span><span class="sxs-lookup"><span data-stu-id="3db16-103">Create a function app and deploy function code from GitHub</span></span>

<span data-ttu-id="3db16-104">Этот образец скрипта создает приложение функции с помощью hello [плана потребления](../functions-scale.md#consumption-plan) и его связанные ресурсы и развертывает код функции из открытого репозитория GitHub (без непрерывного развертывания).</span><span class="sxs-lookup"><span data-stu-id="3db16-104">This sample script creates a function app using hello [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and deploys your function code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="3db16-105">Для непрерывной доставки кода функции из GitHub см. статью [Создание службы приложений](functions-cli-create-function-app-github-continuous.md).</span><span class="sxs-lookup"><span data-stu-id="3db16-105">For continuous delivery of function code from GitHub, read [Create a function app and continuously deploy from GitHub](functions-cli-create-function-app-github-continuous.md)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="3db16-106">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="3db16-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="3db16-107">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="3db16-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="3db16-108">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3db16-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="3db16-109">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="3db16-109">Sample script</span></span>

<span data-ttu-id="3db16-110">Этот пример создает приложения-функцию Azure и развертывает код функции из GitHub.</span><span class="sxs-lookup"><span data-stu-id="3db16-110">This sample creates an Azure Function app and deploys function code from GitHub.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github/deploy-function-app-with-function-github.sh?highlight=3 "Create a function app with deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="3db16-111">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="3db16-111">Script explanation</span></span>

<span data-ttu-id="3db16-112">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="3db16-112">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="3db16-113">Этот скрипт использует hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="3db16-113">This script uses hello following commands:</span></span>

| <span data-ttu-id="3db16-114">Команда</span><span class="sxs-lookup"><span data-stu-id="3db16-114">Command</span></span> | <span data-ttu-id="3db16-115">Примечания</span><span class="sxs-lookup"><span data-stu-id="3db16-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3db16-116">az group create</span><span class="sxs-lookup"><span data-stu-id="3db16-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="3db16-117">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="3db16-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3db16-118">az storage account create</span><span class="sxs-lookup"><span data-stu-id="3db16-118">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="3db16-119">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="3db16-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="3db16-120">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="3db16-120">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) | <span data-ttu-id="3db16-121">Создает приложение-функцию Azure.</span><span class="sxs-lookup"><span data-stu-id="3db16-121">Creates an Azure Function app.</span></span> |
| [<span data-ttu-id="3db16-122">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="3db16-122">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="3db16-123">Связывает приложение-функцию с репозиторием Git или Mercurial.</span><span class="sxs-lookup"><span data-stu-id="3db16-123">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3db16-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3db16-124">Next steps</span></span>

<span data-ttu-id="3db16-125">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3db16-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="3db16-126">Дополнительные примеры сценариев, использующих функции Azure CLI можно найти в hello [документации Azure функции](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3db16-126">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
