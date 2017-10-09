---
title: "aaaCreate приложения функции и развертывать код функции из GitHub | Документы Microsoft"
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
ms.openlocfilehash: 4d44204b899b32af464260db51ed98bcf00eb2bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-app-service"></a><span data-ttu-id="8431e-103">Создание службы приложений</span><span class="sxs-lookup"><span data-stu-id="8431e-103">Create an App Service</span></span>

<span data-ttu-id="8431e-104">Этот образец скрипта создает приложение функции с помощью hello [плана потребления](../functions-scale.md#consumption-plan) и его связанные ресурсы и постоянно развертывает функция кода из репозитория GitHub.</span><span class="sxs-lookup"><span data-stu-id="8431e-104">This sample script creates a function app using hello [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and continuously deploys your function code from a GitHub repository.</span></span> <span data-ttu-id="8431e-105">Для этого примера вам потребуются следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="8431e-105">In this sample, you need:</span></span>

* <span data-ttu-id="8431e-106">Репозиторий GitHub с кодом функции, для которого у вас есть права администратора.</span><span class="sxs-lookup"><span data-stu-id="8431e-106">A GitHub repository with functions code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="8431e-107">[Личный маркер доступа](https://help.github.com/articles/creating-an-access-token-for-command-line-use) для учетной записи GitHub.</span><span class="sxs-lookup"><span data-stu-id="8431e-107">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="8431e-108">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="8431e-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="8431e-109">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="8431e-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="8431e-110">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8431e-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="8431e-111">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="8431e-111">Sample script</span></span>

<span data-ttu-id="8431e-112">Этот пример создает приложения-функцию Azure и развертывает код функции из GitHub.</span><span class="sxs-lookup"><span data-stu-id="8431e-112">This sample creates an Azure Function app and deploys function code from GitHub.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github-continuous/deploy-function-app-with-function-github-continuous.sh?highlight=3-4 "Azure Service")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="8431e-113">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="8431e-113">Script explanation</span></span>

<span data-ttu-id="8431e-114">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="8431e-114">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="8431e-115">Этот скрипт использует hello следующее:</span><span class="sxs-lookup"><span data-stu-id="8431e-115">This script uses hello following:</span></span>

| <span data-ttu-id="8431e-116">Команда</span><span class="sxs-lookup"><span data-stu-id="8431e-116">Command</span></span> | <span data-ttu-id="8431e-117">Примечания</span><span class="sxs-lookup"><span data-stu-id="8431e-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8431e-118">az group create</span><span class="sxs-lookup"><span data-stu-id="8431e-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="8431e-119">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="8431e-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8431e-120">az storage account create</span><span class="sxs-lookup"><span data-stu-id="8431e-120">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="8431e-121">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="8431e-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="8431e-122">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="8431e-122">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) |
| [<span data-ttu-id="8431e-123">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="8431e-123">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="8431e-124">Связывает приложение-функцию с репозиторием Git или Mercurial.</span><span class="sxs-lookup"><span data-stu-id="8431e-124">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8431e-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8431e-125">Next steps</span></span>

<span data-ttu-id="8431e-126">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8431e-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="8431e-127">Дополнительные примеры сценариев, использующих функции Azure CLI можно найти в hello [документации Azure функции](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8431e-127">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
