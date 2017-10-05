---
title: "Создание функции Azure, которая подключается к службе хранилища Azure | Документация Майкрософт"
description: "Пример скрипта Azure CLI для создания функции Azure, которая подключается к службе хранилища Azure."
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: functions
ms.assetid: 
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 04/20/2017
ms.author: rachelap
ms.custom: mvc
ms.openlocfilehash: 36dbc2c181c9991a27163e3194800f63c6c0e01e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-function-app-into-azure-storage-account"></a><span data-ttu-id="e4117-103">Интеграция приложения-функции в учетную запись хранения Azure</span><span class="sxs-lookup"><span data-stu-id="e4117-103">Integrate Function App into Azure Storage Account</span></span>

<span data-ttu-id="e4117-104">Этот пример скрипта создает приложение-функцию и учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="e4117-104">This sample script creates a Function App and Storage Account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e4117-105">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="e4117-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="e4117-106">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="e4117-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="e4117-107">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e4117-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="e4117-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="e4117-108">Sample script</span></span>

<span data-ttu-id="e4117-109">Этот пример создает приложение-функцию Azure и добавляет строку подключения хранилища в параметры приложения.</span><span class="sxs-lookup"><span data-stu-id="e4117-109">This sample creates an Azure Function app and adds the storage connection string to an app setting.</span></span>

<span data-ttu-id="e4117-110">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-storage/create-function-app-connect-to-storage-account.sh "Интеграция приложения-функции в учетную запись хранения Azure")]</span><span class="sxs-lookup"><span data-stu-id="e4117-110">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-storage/create-function-app-connect-to-storage-account.sh "Integrate Function App into Azure Storage Account")]</span></span>


## <a name="clean-up-deployment"></a><span data-ttu-id="e4117-111">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="e4117-111">Clean up deployment</span></span>

<span data-ttu-id="e4117-112">Выполнив пример сценария, вы можете удалить группу ресурсов, приложение службы приложений и все связанные ресурсы с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="e4117-112">After the script sample has been run, the following command can be used to remove the resource group, App Service app, and all related resources:</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="e4117-113">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="e4117-113">Script explanation</span></span>

<span data-ttu-id="e4117-114">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="e4117-114">This script uses the following commands.</span></span> <span data-ttu-id="e4117-115">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="e4117-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="e4117-116">Команда</span><span class="sxs-lookup"><span data-stu-id="e4117-116">Command</span></span> | <span data-ttu-id="e4117-117">Примечания</span><span class="sxs-lookup"><span data-stu-id="e4117-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e4117-118">az login</span><span class="sxs-lookup"><span data-stu-id="e4117-118">az login</span></span>](https://docs.microsoft.com/cli/azure/#login) | <span data-ttu-id="e4117-119">Вход в Azure.</span><span class="sxs-lookup"><span data-stu-id="e4117-119">Login to Azure.</span></span> |
| [<span data-ttu-id="e4117-120">az group create</span><span class="sxs-lookup"><span data-stu-id="e4117-120">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e4117-121">Создайте группу ресурсов с расположением.</span><span class="sxs-lookup"><span data-stu-id="e4117-121">Create a resource group with location</span></span> |
| [<span data-ttu-id="e4117-122">az storage account create</span><span class="sxs-lookup"><span data-stu-id="e4117-122">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account) | <span data-ttu-id="e4117-123">Создайте учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="e4117-123">Create a storage account</span></span> |
| [<span data-ttu-id="e4117-124">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="e4117-124">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="e4117-125">Создайте приложение-функцию.</span><span class="sxs-lookup"><span data-stu-id="e4117-125">Create a new function app</span></span> |
| [<span data-ttu-id="e4117-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="e4117-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="e4117-127">Очистка</span><span class="sxs-lookup"><span data-stu-id="e4117-127">Clean up</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e4117-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e4117-128">Next steps</span></span>

<span data-ttu-id="e4117-129">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e4117-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e4117-130">Дополнительные примеры сценариев Azure CLI для Функций Azure см. в [документации по Функциям Azure](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e4117-130">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
