---
title: "Создание функции Azure, которая подключается к Azure Cosmos DB | Документация Майкрософт"
description: "Пример скрипта Azure CLI для создания функции Azure, которая подключается к Azure Cosmos DB."
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
ms.openlocfilehash: ba7e934f71824493f29b001cea6dd1c567ef3414
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-that-connects-to-an-azure-cosmos-db"></a><span data-ttu-id="c1134-103">Создание функции Azure, которая подключается к Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c1134-103">Create an Azure Function that connects to an Azure Cosmos DB</span></span>

<span data-ttu-id="c1134-104">Этот пример сценария создает приложение-функцию Azure и подключается к Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c1134-104">This sample script creates an Azure Function App and connects to an Azure Cosmos DB database.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c1134-105">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="c1134-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="c1134-106">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="c1134-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="c1134-107">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c1134-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="c1134-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="c1134-108">Sample script</span></span>

<span data-ttu-id="c1134-109">Этот пример создает приложение-функцию Azure, а также добавляет конечную точку и ключ доступа Cosmos DB в параметры приложения.</span><span class="sxs-lookup"><span data-stu-id="c1134-109">This sample creates an Azure Function app and adds a Cosmos DB endpoint and access key to app settings.</span></span>

<span data-ttu-id="c1134-110">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-cosmos-db/create-function-app-connect-to-cosmos-db.sh "Создание функции Azure, которая подключается к Azure Cosmos DB")]</span><span class="sxs-lookup"><span data-stu-id="c1134-110">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-cosmos-db/create-function-app-connect-to-cosmos-db.sh "Create an Azure Function that connects to an Azure Cosmos DB")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="c1134-111">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="c1134-111">Clean up deployment</span></span>

<span data-ttu-id="c1134-112">После выполнения примера сценария можно удалить группу ресурсов и все связанные с ней ресурсы, использовав следующую команду.</span><span class="sxs-lookup"><span data-stu-id="c1134-112">After the script sample has been run, the follow command can be used to remove the resource group and all related resources.</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="c1134-113">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="c1134-113">Script explanation</span></span>

<span data-ttu-id="c1134-114">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="c1134-114">This script uses the following commands.</span></span> <span data-ttu-id="c1134-115">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="c1134-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c1134-116">Команда</span><span class="sxs-lookup"><span data-stu-id="c1134-116">Command</span></span> | <span data-ttu-id="c1134-117">Примечания</span><span class="sxs-lookup"><span data-stu-id="c1134-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c1134-118">az login</span><span class="sxs-lookup"><span data-stu-id="c1134-118">az login</span></span>](https://docs.microsoft.com/cli/azure/#login) | <span data-ttu-id="c1134-119">Вход в Azure.</span><span class="sxs-lookup"><span data-stu-id="c1134-119">Login to Azure.</span></span> |
| [<span data-ttu-id="c1134-120">az group create</span><span class="sxs-lookup"><span data-stu-id="c1134-120">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="c1134-121">Создайте группу ресурсов с расположением.</span><span class="sxs-lookup"><span data-stu-id="c1134-121">Create a resource group with location</span></span> |
| [<span data-ttu-id="c1134-122">az storage account create</span><span class="sxs-lookup"><span data-stu-id="c1134-122">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account) | <span data-ttu-id="c1134-123">Создайте учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="c1134-123">Create a storage account</span></span> |
| [<span data-ttu-id="c1134-124">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="c1134-124">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="c1134-125">Создайте приложение-функцию.</span><span class="sxs-lookup"><span data-stu-id="c1134-125">Create a new function app</span></span> |
| [<span data-ttu-id="c1134-126">az documentdb create</span><span class="sxs-lookup"><span data-stu-id="c1134-126">az documentdb create</span></span>](https://docs.microsoft.com/cli/azure/documentdb#create) | <span data-ttu-id="c1134-127">Создайте базу данных DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="c1134-127">Create documentdb database</span></span> |
| [<span data-ttu-id="c1134-128">az group delete</span><span class="sxs-lookup"><span data-stu-id="c1134-128">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="c1134-129">Очистка</span><span class="sxs-lookup"><span data-stu-id="c1134-129">Clean up</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c1134-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c1134-130">Next steps</span></span>

<span data-ttu-id="c1134-131">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c1134-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c1134-132">Дополнительные примеры сценариев Azure CLI для Функций Azure см. в [документации по Функциям Azure](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c1134-132">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>




