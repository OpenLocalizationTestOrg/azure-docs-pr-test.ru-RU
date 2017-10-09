---
title: "Это функция Azure, которая подключается tooan Azure Cosmos DB aaaCreate | Документы Microsoft"
description: "Сценарий Azure CLI пример — создание это функция Azure, которая подключается tooan Azure Cosmos DB"
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
ms.openlocfilehash: 0fbc1ebec2dfd480e0cf3ca64f9febcec8af9a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-that-connects-tooan-azure-cosmos-db"></a><span data-ttu-id="2a26d-103">Создайте функцию Azure, которая подключается tooan Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2a26d-103">Create an Azure Function that connects tooan Azure Cosmos DB</span></span>

<span data-ttu-id="2a26d-104">Этот образец скрипта создает функции приложения Azure и подключении базы данных Azure Cosmos DB tooan.</span><span class="sxs-lookup"><span data-stu-id="2a26d-104">This sample script creates an Azure Function App and connects tooan Azure Cosmos DB database.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="2a26d-105">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="2a26d-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="2a26d-106">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="2a26d-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="2a26d-107">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2a26d-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="2a26d-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="2a26d-108">Sample script</span></span>

<span data-ttu-id="2a26d-109">Этот образец приложения Azure функция создает и добавляет Cosmos DB конечной точки и доступа ключа tooapp параметров.</span><span class="sxs-lookup"><span data-stu-id="2a26d-109">This sample creates an Azure Function app and adds a Cosmos DB endpoint and access key tooapp settings.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-cosmos-db/create-function-app-connect-to-cosmos-db.sh "Create an Azure Function that connects tooan Azure Cosmos DB")]

## <a name="clean-up-deployment"></a><span data-ttu-id="2a26d-110">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="2a26d-110">Clean up deployment</span></span>

<span data-ttu-id="2a26d-111">После выполнения сценария образец hello hello выполните команду может быть группа ресурсов используется tooremove hello и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="2a26d-111">After hello script sample has been run, hello follow command can be used tooremove hello resource group and all related resources.</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="2a26d-112">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="2a26d-112">Script explanation</span></span>

<span data-ttu-id="2a26d-113">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="2a26d-113">This script uses hello following commands.</span></span> <span data-ttu-id="2a26d-114">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="2a26d-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="2a26d-115">Команда</span><span class="sxs-lookup"><span data-stu-id="2a26d-115">Command</span></span> | <span data-ttu-id="2a26d-116">Примечания</span><span class="sxs-lookup"><span data-stu-id="2a26d-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2a26d-117">az login</span><span class="sxs-lookup"><span data-stu-id="2a26d-117">az login</span></span>](https://docs.microsoft.com/cli/azure/#login) | <span data-ttu-id="2a26d-118">TooAzure входа.</span><span class="sxs-lookup"><span data-stu-id="2a26d-118">Login tooAzure.</span></span> |
| [<span data-ttu-id="2a26d-119">az group create</span><span class="sxs-lookup"><span data-stu-id="2a26d-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="2a26d-120">Создайте группу ресурсов с расположением.</span><span class="sxs-lookup"><span data-stu-id="2a26d-120">Create a resource group with location</span></span> |
| [<span data-ttu-id="2a26d-121">az storage account create</span><span class="sxs-lookup"><span data-stu-id="2a26d-121">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account) | <span data-ttu-id="2a26d-122">Создайте учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="2a26d-122">Create a storage account</span></span> |
| [<span data-ttu-id="2a26d-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="2a26d-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="2a26d-124">Создайте приложение-функцию.</span><span class="sxs-lookup"><span data-stu-id="2a26d-124">Create a new function app</span></span> |
| [<span data-ttu-id="2a26d-125">az documentdb create</span><span class="sxs-lookup"><span data-stu-id="2a26d-125">az documentdb create</span></span>](https://docs.microsoft.com/cli/azure/documentdb#create) | <span data-ttu-id="2a26d-126">Создайте базу данных DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="2a26d-126">Create documentdb database</span></span> |
| [<span data-ttu-id="2a26d-127">az group delete</span><span class="sxs-lookup"><span data-stu-id="2a26d-127">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="2a26d-128">Очистка</span><span class="sxs-lookup"><span data-stu-id="2a26d-128">Clean up</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2a26d-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2a26d-129">Next steps</span></span>

<span data-ttu-id="2a26d-130">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2a26d-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2a26d-131">Дополнительные примеры сценариев, использующих функции Azure CLI можно найти в hello [документации Azure функции](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2a26d-131">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>




