---
title: "Создание приложения-функции и развертывание кода функции из Visual Studio Team Services | Документация Майкрософт"
description: "Создание приложения-функции и развертывание кода функции из Visual Studio Team Services."
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/28/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: 2ef177b55ad7ffd351156821f429e6ff8fbeccc7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-app-service"></a><span data-ttu-id="648cd-103">Создание службы приложений</span><span class="sxs-lookup"><span data-stu-id="648cd-103">Create an App Service</span></span>

<span data-ttu-id="648cd-104">Из этой статьи вы узнаете, как создать приложение-функцию с помощью [плана потребления](../functions-scale.md#consumption-plan) и связанных с ним ресурсов, а также как выполнить непрерывное развертывание кода функции из репозитория Visual Studio Team Services (VSTS).</span><span class="sxs-lookup"><span data-stu-id="648cd-104">In this scenario you will learn how to create a function app using the [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and continuously deploys your function code from a Visual Studio Team Services (VSTS) repository.</span></span> <span data-ttu-id="648cd-105">Для этого примера потребуется:</span><span class="sxs-lookup"><span data-stu-id="648cd-105">In this sample, you will need:</span></span>

* <span data-ttu-id="648cd-106">Репозиторий VSTS с кодом функции, для которого у вас есть права администратора.</span><span class="sxs-lookup"><span data-stu-id="648cd-106">A VSTS repository with functions code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="648cd-107">[Личный маркер доступа](https://help.github.com/articles/creating-an-access-token-for-command-line-use) для учетной записи GitHub.</span><span class="sxs-lookup"><span data-stu-id="648cd-107">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="648cd-108">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="648cd-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="648cd-109">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="648cd-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="648cd-110">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="648cd-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="648cd-111">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="648cd-111">Sample script</span></span>

<span data-ttu-id="648cd-112">Этот пример создает приложение-функцию Azure и развертывает код функции из Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="648cd-112">This sample creates an Azure Function app and deploys function code from Visual Studio Team Services.</span></span>

<span data-ttu-id="648cd-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-vsts/deploy-function-app-with-function-vsts.sh?highlight=3-4 "Служба Azure")]</span><span class="sxs-lookup"><span data-stu-id="648cd-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-vsts/deploy-function-app-with-function-vsts.sh?highlight=3-4 "Azure Service")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="648cd-114">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="648cd-114">Script explanation</span></span>

<span data-ttu-id="648cd-115">Для создания группы ресурсов, веб-приложений, DocumentDB и всех связанных ресурсов этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="648cd-115">This script uses the following commands to create a resource group, web app, documentdb and all related resources.</span></span> <span data-ttu-id="648cd-116">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="648cd-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="648cd-117">Команда</span><span class="sxs-lookup"><span data-stu-id="648cd-117">Command</span></span> | <span data-ttu-id="648cd-118">Примечания</span><span class="sxs-lookup"><span data-stu-id="648cd-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="648cd-119">az group create</span><span class="sxs-lookup"><span data-stu-id="648cd-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="648cd-120">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="648cd-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="648cd-121">az storage account create</span><span class="sxs-lookup"><span data-stu-id="648cd-121">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="648cd-122">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="648cd-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="648cd-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="648cd-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) |
| [<span data-ttu-id="648cd-124">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="648cd-124">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="648cd-125">Связывает приложение-функцию с репозиторием Git или Mercurial.</span><span class="sxs-lookup"><span data-stu-id="648cd-125">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="648cd-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="648cd-126">Next steps</span></span>

<span data-ttu-id="648cd-127">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="648cd-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="648cd-128">Дополнительные примеры сценариев Azure CLI для Функций Azure см. в [документации по Функциям Azure](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="648cd-128">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
