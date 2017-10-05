---
title: "Создание учетной записи, базы данных и коллекции API MongoDB для Azure Cosmos DB с помощью сценария Azure CLI | Документация Майкрософт"
description: "Пример сценария Azure CLI для создания учетной записи, базы данных и коллекции API MongoDB в Azure Cosmos DB."
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 06/02/2017
ms.author: mimig
ms.openlocfilehash: b0bf637db90cfcb987ad43ed34cb8065d28b0fcf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-create-an-mongodb-api-account-using-the-azure-cli"></a><span data-ttu-id="d5e46-103">Azure Cosmos DB: создание учетной записи API MongoDB с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d5e46-103">Azure Cosmos DB: Create an MongoDB API account using the Azure CLI</span></span>

<span data-ttu-id="d5e46-104">Этот пример сценария интерфейса командной строки (CLI) создает учетную запись, базу данных и коллекцию API MongoDB в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d5e46-104">This sample CLI script creates an Azure Cosmos DB MongoDB API account, database, and collection.</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d5e46-105">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="d5e46-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="d5e46-106">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="d5e46-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="d5e46-107">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d5e46-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="d5e46-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="d5e46-108">Sample script</span></span>

<span data-ttu-id="d5e46-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/create-cosmosdb-mongodb-account/create-cosmosdb-mongodb-account.sh?highlight=15-35 "Создание учетной записи, базы данных и коллекции API MongoDB в Azure Cosmos DB")]</span><span class="sxs-lookup"><span data-stu-id="d5e46-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/create-cosmosdb-mongodb-account/create-cosmosdb-mongodb-account.sh?highlight=15-35 "Create an Azure Cosmos DB MongoDB API account, database, and collection")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="d5e46-110">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="d5e46-110">Clean up deployment</span></span>

<span data-ttu-id="d5e46-111">После выполнения примера сценария можно удалить группу ресурсов и все связанные с ней ресурсы, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="d5e46-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="d5e46-112">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="d5e46-112">Script explanation</span></span>

<span data-ttu-id="d5e46-113">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="d5e46-113">This script uses the following commands.</span></span> <span data-ttu-id="d5e46-114">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="d5e46-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d5e46-115">Команда</span><span class="sxs-lookup"><span data-stu-id="d5e46-115">Command</span></span> | <span data-ttu-id="d5e46-116">Примечания</span><span class="sxs-lookup"><span data-stu-id="d5e46-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d5e46-117">az group create</span><span class="sxs-lookup"><span data-stu-id="d5e46-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="d5e46-118">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d5e46-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d5e46-119">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="d5e46-119">az cosmosdb create</span></span>](/cli/azure/cosmosdb#create) | <span data-ttu-id="d5e46-120">Создает учетную запись Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d5e46-120">Creates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="d5e46-121">az group delete</span><span class="sxs-lookup"><span data-stu-id="d5e46-121">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="d5e46-122">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="d5e46-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d5e46-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d5e46-123">Next steps</span></span>

<span data-ttu-id="d5e46-124">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d5e46-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d5e46-125">Дополнительные примеры скриптов CLI для базы данных Azure Cosmos DB см. в [документации по интерфейсу командной строки базы данных Azure Cosmos DB](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d5e46-125">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
