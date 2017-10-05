---
title: "Создание приложения-функции и развертывание кода функции из GitHub | Документация Майкрософт"
description: "Пример сценария Azure CLI для создания приложения-функции и развертывание кода функции из GitHub."
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: d67e85f91c80efe464fceb1105243bedfba83a0f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-function-app-and-deploy-function-code-from-github"></a><span data-ttu-id="91e61-103">Создание приложения-функции и развертывание кода функции из GitHub</span><span class="sxs-lookup"><span data-stu-id="91e61-103">Create a function app and deploy function code from GitHub</span></span>

<span data-ttu-id="91e61-104">Этот пример сценария создает приложение-функцию с помощью [плана потребления](../functions-scale.md#consumption-plan) со связанными ресурсами и развертывает код функции из открытого репозитория GitHub (без непрерывного развертывания).</span><span class="sxs-lookup"><span data-stu-id="91e61-104">This sample script creates a function app using the [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and deploys your function code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="91e61-105">Для непрерывной доставки кода функции из GitHub см. статью [Создание службы приложений](functions-cli-create-function-app-github-continuous.md).</span><span class="sxs-lookup"><span data-stu-id="91e61-105">For continuous delivery of function code from GitHub, read [Create a function app and continuously deploy from GitHub](functions-cli-create-function-app-github-continuous.md)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="91e61-106">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="91e61-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="91e61-107">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="91e61-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="91e61-108">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="91e61-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="91e61-109">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="91e61-109">Sample script</span></span>

<span data-ttu-id="91e61-110">Этот пример создает приложения-функцию Azure и развертывает код функции из GitHub.</span><span class="sxs-lookup"><span data-stu-id="91e61-110">This sample creates an Azure Function app and deploys function code from GitHub.</span></span>

<span data-ttu-id="91e61-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github/deploy-function-app-with-function-github.sh?highlight=3 "Создание приложения-функции с развертыванием из GitHub")]</span><span class="sxs-lookup"><span data-stu-id="91e61-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github/deploy-function-app-with-function-github.sh?highlight=3 "Create a function app with deployment from GitHub")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="91e61-112">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="91e61-112">Script explanation</span></span>

<span data-ttu-id="91e61-113">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="91e61-113">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="91e61-114">Этот сценарий использует следующие команды:</span><span class="sxs-lookup"><span data-stu-id="91e61-114">This script uses the following commands:</span></span>

| <span data-ttu-id="91e61-115">Команда</span><span class="sxs-lookup"><span data-stu-id="91e61-115">Command</span></span> | <span data-ttu-id="91e61-116">Примечания</span><span class="sxs-lookup"><span data-stu-id="91e61-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="91e61-117">az group create</span><span class="sxs-lookup"><span data-stu-id="91e61-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="91e61-118">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="91e61-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="91e61-119">az storage account create</span><span class="sxs-lookup"><span data-stu-id="91e61-119">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="91e61-120">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="91e61-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="91e61-121">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="91e61-121">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) | <span data-ttu-id="91e61-122">Создает приложение-функцию Azure.</span><span class="sxs-lookup"><span data-stu-id="91e61-122">Creates an Azure Function app.</span></span> |
| [<span data-ttu-id="91e61-123">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="91e61-123">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="91e61-124">Связывает приложение-функцию с репозиторием Git или Mercurial.</span><span class="sxs-lookup"><span data-stu-id="91e61-124">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="91e61-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="91e61-125">Next steps</span></span>

<span data-ttu-id="91e61-126">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="91e61-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="91e61-127">Дополнительные примеры сценариев Azure CLI для Функций Azure см. в [документации по Функциям Azure](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="91e61-127">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
