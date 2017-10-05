---
title: "Пример сценария Azure CLI. Создание приложения-функции для выполнения без сервера | Документация Майкрософт"
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
ms.openlocfilehash: 37046967bd5ab0d797d1c66690db7200fb4805e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-function-app-for-serverless-execution"></a><span data-ttu-id="1a48c-103">Создание приложения-функции для выполнения без сервера</span><span class="sxs-lookup"><span data-stu-id="1a48c-103">Create a Function App for serverless execution</span></span>

<span data-ttu-id="1a48c-104">Этот пример сценария создает приложение-функцию Azure, которое является контейнером для ваших функций.</span><span class="sxs-lookup"><span data-stu-id="1a48c-104">This sample script creates an Azure Function App, which is a container for your functions.</span></span> <span data-ttu-id="1a48c-105">Приложение-функция создается с помощью [плана потребления](../functions-scale.md#consumption-plan), который идеально подходит для рабочих нагрузок, выполняемых на основе событий без использования сервера.</span><span class="sxs-lookup"><span data-stu-id="1a48c-105">The Function App is created using the [consumption plan](../functions-scale.md#consumption-plan), which is ideal for event-driven serverless workloads.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="1a48c-106">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="1a48c-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="1a48c-107">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="1a48c-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="1a48c-108">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1a48c-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="1a48c-109">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="1a48c-109">Sample script</span></span>

<span data-ttu-id="1a48c-110">Этот скрипт создает приложение-функцию Azure с помощью [плана потребления](../functions-scale.md#consumption-plan).</span><span class="sxs-lookup"><span data-stu-id="1a48c-110">This script creates an Azure Function app using the [consumption plan](../functions-scale.md#consumption-plan).</span></span>

<span data-ttu-id="1a48c-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-consumption/create-function-app-consumption.sh "Создание функции Azure на основе плана потребления")]</span><span class="sxs-lookup"><span data-stu-id="1a48c-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-consumption/create-function-app-consumption.sh "Create an Azure Function on a consumption plan")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="1a48c-112">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="1a48c-112">Script explanation</span></span>

<span data-ttu-id="1a48c-113">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="1a48c-113">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="1a48c-114">Этот сценарий использует следующие команды:</span><span class="sxs-lookup"><span data-stu-id="1a48c-114">This script uses the following commands:</span></span>

| <span data-ttu-id="1a48c-115">Команда</span><span class="sxs-lookup"><span data-stu-id="1a48c-115">Command</span></span> | <span data-ttu-id="1a48c-116">Примечания</span><span class="sxs-lookup"><span data-stu-id="1a48c-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1a48c-117">az group create</span><span class="sxs-lookup"><span data-stu-id="1a48c-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="1a48c-118">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="1a48c-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1a48c-119">az storage account create</span><span class="sxs-lookup"><span data-stu-id="1a48c-119">az storage account create</span></span>](/cli/azure/storage/account#create) | <span data-ttu-id="1a48c-120">Создает учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="1a48c-120">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="1a48c-121">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="1a48c-121">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="1a48c-122">Создает функцию Azure.</span><span class="sxs-lookup"><span data-stu-id="1a48c-122">Creates an Azure Function.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1a48c-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1a48c-123">Next steps</span></span>

<span data-ttu-id="1a48c-124">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1a48c-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="1a48c-125">Дополнительные примеры сценариев Azure CLI для Функций Azure см. в [документации по Функциям Azure](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1a48c-125">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
