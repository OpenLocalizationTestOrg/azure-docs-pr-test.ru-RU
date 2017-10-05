---
title: "Получение строки подключения базы данных Azure Cosmos DB для приложений MongoDB с помощью скрипта Azure CLI | Документация Майкрософт"
description: "Получение строки подключения базы данных Azure Cosmos DB для приложений MongoDB с помощью скрипта Azure CLI"
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
ms.openlocfilehash: 916c92cab39306352fdf9dff0e0685fd61832d16
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="get-an-azure-cosmos-db-connection-string-for-mongodb-apps-using-the-azure-cli"></a><span data-ttu-id="f448e-103">Получение строки подключения базы данных Azure Cosmos DB для приложений MongoDB с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f448e-103">Get an Azure Cosmos DB connection string for MongoDB apps using the Azure CLI</span></span>

<span data-ttu-id="f448e-104">Этот пример получает строку подключения базы данных Azure Cosmos DB для приложений MongoDB с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f448e-104">This sample gets an Azure Cosmos DB connection string for MongoDB apps using the Azure CLI.</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f448e-105">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="f448e-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f448e-106">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="f448e-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="f448e-107">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f448e-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="f448e-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="f448e-108">Sample script</span></span>

<span data-ttu-id="f448e-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/secure-cosmosdb-get-mongodb-connection-string/secure-cosmosdb-get-mongodb-connection-string.sh?highlight=36-39 "Получение строки подключения базы данных Azure Cosmos DB для приложений MongoDB")]</span><span class="sxs-lookup"><span data-stu-id="f448e-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/secure-cosmosdb-get-mongodb-connection-string/secure-cosmosdb-get-mongodb-connection-string.sh?highlight=36-39 "Get Azure Cosmos DB connection string for MongoDB apps")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="f448e-110">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="f448e-110">Clean up deployment</span></span>

<span data-ttu-id="f448e-111">После выполнения примера сценария можно удалить группу ресурсов и все связанные с ней ресурсы, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="f448e-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="f448e-112">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="f448e-112">Script explanation</span></span>

<span data-ttu-id="f448e-113">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="f448e-113">This script uses the following commands.</span></span> <span data-ttu-id="f448e-114">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="f448e-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f448e-115">Команда</span><span class="sxs-lookup"><span data-stu-id="f448e-115">Command</span></span> | <span data-ttu-id="f448e-116">Примечания</span><span class="sxs-lookup"><span data-stu-id="f448e-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f448e-117">az group create</span><span class="sxs-lookup"><span data-stu-id="f448e-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f448e-118">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="f448e-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f448e-119">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="f448e-119">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="f448e-120">Обновляет учетную запись базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f448e-120">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="f448e-121">az cosmosdb list-connection-strings</span><span class="sxs-lookup"><span data-stu-id="f448e-121">az cosmosdb list-connection-strings</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#list-connection-strings) | <span data-ttu-id="f448e-122">Получает строку подключения для учетной записи.</span><span class="sxs-lookup"><span data-stu-id="f448e-122">Gets the connection string for the account.</span></span>|
| [<span data-ttu-id="f448e-123">az group delete</span><span class="sxs-lookup"><span data-stu-id="f448e-123">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="f448e-124">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="f448e-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f448e-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f448e-125">Next steps</span></span>

<span data-ttu-id="f448e-126">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f448e-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f448e-127">Дополнительные примеры скриптов CLI для базы данных Azure Cosmos DB см. в [документации по интерфейсу командной строки базы данных Azure Cosmos DB](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f448e-127">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
