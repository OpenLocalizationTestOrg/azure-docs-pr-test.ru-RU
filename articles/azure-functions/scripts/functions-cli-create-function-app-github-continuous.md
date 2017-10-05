---
title: "Создание приложения-функции и развертывание кода функции из GitHub | Документация Майкрософт"
description: "Создание приложения-функции и развертывание кода функции из GitHub."
services: functions
ms.service: functions
keywords: 
ms.devlang: azurecli
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.custom: mvc
ms.openlocfilehash: 67eb41d89328ab57741c419d8b718e19b947dab1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-app-service"></a><span data-ttu-id="f0abc-103">Создание службы приложений</span><span class="sxs-lookup"><span data-stu-id="f0abc-103">Create an App Service</span></span>

<span data-ttu-id="f0abc-104">Этот пример сценария создает приложение-функцию с помощью [плана потребления](../functions-scale.md#consumption-plan) со связанными ресурсами и непрерывно развертывает код функции из репозитория GitHub.</span><span class="sxs-lookup"><span data-stu-id="f0abc-104">This sample script creates a function app using the [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and continuously deploys your function code from a GitHub repository.</span></span> <span data-ttu-id="f0abc-105">Для этого примера вам потребуются следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="f0abc-105">In this sample, you need:</span></span>

* <span data-ttu-id="f0abc-106">Репозиторий GitHub с кодом функции, для которого у вас есть права администратора.</span><span class="sxs-lookup"><span data-stu-id="f0abc-106">A GitHub repository with functions code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="f0abc-107">[Личный маркер доступа](https://help.github.com/articles/creating-an-access-token-for-command-line-use) для учетной записи GitHub.</span><span class="sxs-lookup"><span data-stu-id="f0abc-107">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f0abc-108">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="f0abc-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f0abc-109">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="f0abc-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="f0abc-110">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f0abc-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="f0abc-111">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="f0abc-111">Sample script</span></span>

<span data-ttu-id="f0abc-112">Этот пример создает приложения-функцию Azure и развертывает код функции из GitHub.</span><span class="sxs-lookup"><span data-stu-id="f0abc-112">This sample creates an Azure Function app and deploys function code from GitHub.</span></span>

<span data-ttu-id="f0abc-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github-continuous/deploy-function-app-with-function-github-continuous.sh?highlight=3-4 "Служба Azure")]</span><span class="sxs-lookup"><span data-stu-id="f0abc-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github-continuous/deploy-function-app-with-function-github-continuous.sh?highlight=3-4 "Azure Service")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="f0abc-114">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="f0abc-114">Script explanation</span></span>

<span data-ttu-id="f0abc-115">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="f0abc-115">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="f0abc-116">Этот сценарий использует следующие команды:</span><span class="sxs-lookup"><span data-stu-id="f0abc-116">This script uses the following:</span></span>

| <span data-ttu-id="f0abc-117">Команда</span><span class="sxs-lookup"><span data-stu-id="f0abc-117">Command</span></span> | <span data-ttu-id="f0abc-118">Примечания</span><span class="sxs-lookup"><span data-stu-id="f0abc-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f0abc-119">az group create</span><span class="sxs-lookup"><span data-stu-id="f0abc-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f0abc-120">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="f0abc-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f0abc-121">az storage account create</span><span class="sxs-lookup"><span data-stu-id="f0abc-121">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="f0abc-122">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="f0abc-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="f0abc-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="f0abc-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) |
| [<span data-ttu-id="f0abc-124">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="f0abc-124">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="f0abc-125">Связывает приложение-функцию с репозиторием Git или Mercurial.</span><span class="sxs-lookup"><span data-stu-id="f0abc-125">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f0abc-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f0abc-126">Next steps</span></span>

<span data-ttu-id="f0abc-127">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f0abc-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f0abc-128">Дополнительные примеры сценариев Azure CLI для Функций Azure см. в [документации по Функциям Azure](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f0abc-128">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
