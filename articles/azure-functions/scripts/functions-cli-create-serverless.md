---
title: "aaaAzure образец скрипта CLI - создать приложение функции для выполнения без сервера | Документы Microsoft"
description: "Пример сценария Azure CLI для создания приложения-функции для выполнения без сервера."
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
ms.openlocfilehash: 7ec872b642e50827896a73a9e43bcc87233e15c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-for-serverless-execution"></a><span data-ttu-id="76720-103">Создание приложения-функции для выполнения без сервера</span><span class="sxs-lookup"><span data-stu-id="76720-103">Create a Function App for serverless execution</span></span>

<span data-ttu-id="76720-104">Этот пример сценария создает приложение-функцию Azure, которое является контейнером для ваших функций.</span><span class="sxs-lookup"><span data-stu-id="76720-104">This sample script creates an Azure Function App, which is a container for your functions.</span></span> <span data-ttu-id="76720-105">Hello функции создания приложения с помощью hello [плана потребления](../functions-scale.md#consumption-plan), которые идеально подходят для рабочих нагрузок без сервера с событиями.</span><span class="sxs-lookup"><span data-stu-id="76720-105">hello Function App is created using hello [consumption plan](../functions-scale.md#consumption-plan), which is ideal for event-driven serverless workloads.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="76720-106">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="76720-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="76720-107">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="76720-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="76720-108">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="76720-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="76720-109">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="76720-109">Sample script</span></span>

<span data-ttu-id="76720-110">Этот скрипт создает функцию Azure приложения с помощью hello [плана потребления](../functions-scale.md#consumption-plan).</span><span class="sxs-lookup"><span data-stu-id="76720-110">This script creates an Azure Function app using hello [consumption plan](../functions-scale.md#consumption-plan).</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-consumption/create-function-app-consumption.sh "Create an Azure Function on a consumption plan")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="76720-111">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="76720-111">Script explanation</span></span>

<span data-ttu-id="76720-112">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="76720-112">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="76720-113">Этот скрипт использует hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="76720-113">This script uses hello following commands:</span></span>

| <span data-ttu-id="76720-114">Команда</span><span class="sxs-lookup"><span data-stu-id="76720-114">Command</span></span> | <span data-ttu-id="76720-115">Примечания</span><span class="sxs-lookup"><span data-stu-id="76720-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="76720-116">az group create</span><span class="sxs-lookup"><span data-stu-id="76720-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="76720-117">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="76720-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="76720-118">az storage account create</span><span class="sxs-lookup"><span data-stu-id="76720-118">az storage account create</span></span>](/cli/azure/storage/account#create) | <span data-ttu-id="76720-119">Создает учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="76720-119">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="76720-120">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="76720-120">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="76720-121">Создает функцию Azure.</span><span class="sxs-lookup"><span data-stu-id="76720-121">Creates an Azure Function.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="76720-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="76720-122">Next steps</span></span>

<span data-ttu-id="76720-123">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="76720-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="76720-124">Дополнительные примеры сценариев, использующих функции Azure CLI можно найти в hello [документации Azure функции](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="76720-124">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
