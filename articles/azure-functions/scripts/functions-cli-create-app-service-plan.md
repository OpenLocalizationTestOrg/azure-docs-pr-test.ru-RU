---
title: "aaaAzure образец скрипта CLI - Создание функции приложения в плане обслуживания приложений | Документы Microsoft"
description: "Пример сценария Azure CLI для создания приложения-функции в плане службы приложений."
services: functions
documentationcenter: functions
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0e221db6-ee2d-4e16-9bf6-a456cd05b6e7
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 04/11/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: c0ffbbbf022e5680e5ae3141e784e7c7bced0bc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-in-an-app-service-plan"></a><span data-ttu-id="47a4d-103">Создание приложения-функции в плане службы приложений</span><span class="sxs-lookup"><span data-stu-id="47a4d-103">Create a Function App in an App Service plan</span></span>

<span data-ttu-id="47a4d-104">Этот пример сценария создает приложение-функцию Azure, которое является контейнером для ваших функций.</span><span class="sxs-lookup"><span data-stu-id="47a4d-104">This sample script creates an Azure Function App, which is a container for your functions.</span></span> <span data-ttu-id="47a4d-105">Функции приложения Hello создается с использованием выделенного план служб приложений, это означает, что ресурсы сервера всегда активны.</span><span class="sxs-lookup"><span data-stu-id="47a4d-105">hello Function App is created using a dedicated App Service plan, which means your server resources are always on.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="47a4d-106">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="47a4d-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="47a4d-107">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="47a4d-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="47a4d-108">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="47a4d-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="47a4d-109">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="47a4d-109">Sample script</span></span>

<span data-ttu-id="47a4d-110">Этот скрипт создает приложение-функцию Azure с помощью выделенного [плана службы приложений](../functions-scale.md#app-service-plan).</span><span class="sxs-lookup"><span data-stu-id="47a4d-110">This script creates an Azure Function app using a dedicated [App Service plan](../functions-scale.md#app-service-plan).</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-app-service-plan/create-function-app-app-service-plan.sh "Create an Azure Function on an App Service plan")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="47a4d-111">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="47a4d-111">Script explanation</span></span>

<span data-ttu-id="47a4d-112">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="47a4d-112">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="47a4d-113">Этот скрипт использует hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="47a4d-113">This script uses hello following commands:</span></span>

| <span data-ttu-id="47a4d-114">Команда</span><span class="sxs-lookup"><span data-stu-id="47a4d-114">Command</span></span> | <span data-ttu-id="47a4d-115">Примечания</span><span class="sxs-lookup"><span data-stu-id="47a4d-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="47a4d-116">az group create</span><span class="sxs-lookup"><span data-stu-id="47a4d-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="47a4d-117">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="47a4d-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="47a4d-118">az storage account create</span><span class="sxs-lookup"><span data-stu-id="47a4d-118">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="47a4d-119">Создает учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="47a4d-119">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="47a4d-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="47a4d-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appserviceplan#create) | <span data-ttu-id="47a4d-121">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="47a4d-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="47a4d-122">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="47a4d-122">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#delete) | <span data-ttu-id="47a4d-123">Создает приложение-функцию Azure.</span><span class="sxs-lookup"><span data-stu-id="47a4d-123">Creates an Azure Function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="47a4d-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="47a4d-124">Next steps</span></span>

<span data-ttu-id="47a4d-125">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="47a4d-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="47a4d-126">Дополнительные примеры сценариев, использующих функции Azure CLI можно найти в hello [документации Azure функции](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="47a4d-126">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
