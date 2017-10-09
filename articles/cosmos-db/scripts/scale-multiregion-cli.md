---
title: "aaaAzure сценарий CLI-Multiregion репликации для Azure Cosmos DB | Документы Microsoft"
description: "Пример скрипта Azure CLI. Репликация в нескольких регионах для базы данных Azure Cosmos DB"
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
ms.openlocfilehash: e3590303ed3bda9eca1046bf62fff6b61333156c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-an-azure-cosmos-db-database-account-in-multiple-regions-and-configure-failover-priorities-using-hello-azure-cli"></a><span data-ttu-id="6020d-103">Реплицировать базу данных Azure Cosmos учетную запись базы данных в нескольких регионах и настроить с помощью Azure CLI hello приоритетов отработки отказа</span><span class="sxs-lookup"><span data-stu-id="6020d-103">Replicate an Azure Cosmos DB database account in multiple regions and configure failover priorities using hello Azure CLI</span></span>

<span data-ttu-id="6020d-104">Этот пример реплицирует любые виды Azure Cosmos DB учетная запись базы данных в нескольких регионах и настраивает приоритетов отработки отказа с помощью Azure CLI hello.</span><span class="sxs-lookup"><span data-stu-id="6020d-104">This sample replicates any kind of Azure Cosmos DB database account in multiple regions and configures failover priorities using hello Azure CLI.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6020d-105">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="6020d-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6020d-106">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="6020d-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="6020d-107">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6020d-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="6020d-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="6020d-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/scale-cosmosdb-replicate-multiple-regions/scale-cosmosdb-replicate-multiple-regions.sh?highlight=21-31 "Scale Azure Cosmos DB into multiple regions")]

## <a name="clean-up-deployment"></a><span data-ttu-id="6020d-109">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="6020d-109">Clean up deployment</span></span>

<span data-ttu-id="6020d-110">После выполнения сценария образец hello hello, следующая команда может быть группы ресурсов используется tooremove hello и все ресурсы, связанные с ним.</span><span class="sxs-lookup"><span data-stu-id="6020d-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="6020d-111">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="6020d-111">Script explanation</span></span>

<span data-ttu-id="6020d-112">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="6020d-112">This script uses hello following commands.</span></span> <span data-ttu-id="6020d-113">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="6020d-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="6020d-114">Команда</span><span class="sxs-lookup"><span data-stu-id="6020d-114">Command</span></span> | <span data-ttu-id="6020d-115">Примечания</span><span class="sxs-lookup"><span data-stu-id="6020d-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6020d-116">az group create</span><span class="sxs-lookup"><span data-stu-id="6020d-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="6020d-117">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="6020d-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6020d-118">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="6020d-118">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="6020d-119">Обновляет учетную запись базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6020d-119">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="6020d-120">az group delete</span><span class="sxs-lookup"><span data-stu-id="6020d-120">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="6020d-121">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="6020d-121">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6020d-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6020d-122">Next steps</span></span>

<span data-ttu-id="6020d-123">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6020d-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6020d-124">Дополнительные примеры сценариев, использующих DB Cosmos Azure CLI можно найти в hello [документации Azure Cosmos DB CLI](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6020d-124">Additional Azure Cosmos DB CLI script samples can be found in hello [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
