---
title: "Создание брандмауэра для Azure Cosmos DB с помощью сценария Azure CLI | Документация Майкрософт"
description: "Пример сценария Azure CLI для создания брандмауэра для Azure Cosmos DB."
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: sammvcple
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 06/02/2017
ms.author: mimig
ms.openlocfilehash: 51f61901e1b1615e48582690dea701a01a56ebca
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-create-a-firewall-using-the-azure-cli"></a><span data-ttu-id="52304-103">Azure Cosmos DB: создание брандмауэра с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="52304-103">Azure Cosmos DB: Create a firewall using the Azure CLI</span></span>

<span data-ttu-id="52304-104">Этот пример сценария интерфейса командной строки создает политику брандмауэра для любой учетной записи Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="52304-104">This sample CLI script creates a firewall policy for any kind of Azure Cosmos DB account.</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="52304-105">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="52304-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="52304-106">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="52304-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="52304-107">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="52304-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="52304-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="52304-108">Sample script</span></span>

<span data-ttu-id="52304-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/secure-cosmosdb-create-firewall/secure-cosmosdb-create-firewall.sh?highlight=38-42 "Создание брандмауэра для Azure Cosmos DB")]</span><span class="sxs-lookup"><span data-stu-id="52304-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/secure-cosmosdb-create-firewall/secure-cosmosdb-create-firewall.sh?highlight=38-42 "Create an Azure Cosmos DB firewall")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="52304-110">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="52304-110">Clean up deployment</span></span>

<span data-ttu-id="52304-111">После выполнения примера сценария можно удалить группу ресурсов и все связанные с ней ресурсы, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="52304-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="52304-112">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="52304-112">Script explanation</span></span>

<span data-ttu-id="52304-113">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="52304-113">This script uses the following commands.</span></span> <span data-ttu-id="52304-114">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="52304-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="52304-115">Команда</span><span class="sxs-lookup"><span data-stu-id="52304-115">Command</span></span> | <span data-ttu-id="52304-116">Примечания</span><span class="sxs-lookup"><span data-stu-id="52304-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="52304-117">az group create</span><span class="sxs-lookup"><span data-stu-id="52304-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="52304-118">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="52304-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="52304-119">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="52304-119">az cosmosdb create</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#create) | <span data-ttu-id="52304-120">Создает учетную запись Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="52304-120">Creates an Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="52304-121">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="52304-121">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="52304-122">Обновляет учетную запись Azure Cosmos DB для включения параметров брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="52304-122">Updates an Azure CosmosDB account to include firewall settings.</span></span> |
| [<span data-ttu-id="52304-123">az group delete</span><span class="sxs-lookup"><span data-stu-id="52304-123">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="52304-124">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="52304-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="52304-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="52304-125">Next steps</span></span>

<span data-ttu-id="52304-126">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="52304-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="52304-127">Дополнительные примеры скриптов CLI для базы данных Azure Cosmos DB см. в [документации по интерфейсу командной строки базы данных Azure Cosmos DB](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="52304-127">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
