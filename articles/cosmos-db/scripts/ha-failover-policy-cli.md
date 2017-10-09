---
title: "CLI скрипт создания политики отработки отказа для обеспечения высокой доступности aaaAzure | Документы Microsoft"
description: "Пример скрипта Azure CLI. Создание политики отработки отказа для обеспечения высокой доступности"
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
ms.openlocfilehash: 9076f4ef23fceb4208c934c57ac6899f0b58ffd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-failover-policy-for-high-availability-using-hello-azure-cli"></a><span data-ttu-id="fad0c-103">Создание политики отработки отказа для обеспечения высокой доступности с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="fad0c-103">Create a failover policy for high availability using hello Azure CLI</span></span>

<span data-ttu-id="fad0c-104">Данный пример скрипта CLI создает учетную запись базы данных Azure Cosmos DB, а затем настраивает ее для обеспечения высокой доступности.</span><span class="sxs-lookup"><span data-stu-id="fad0c-104">This sample CLI script creates an Azure Cosmos DB account, and then configures it for high availability.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="fad0c-105">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="fad0c-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="fad0c-106">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="fad0c-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="fad0c-107">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fad0c-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="fad0c-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="fad0c-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/high-availability-cosmosdb-configure-failover/high-availability-cosmosdb-configure-failover.sh?highlight=23-27 "Create an Azure Cosmos DB failover policy")]

## <a name="clean-up-deployment"></a><span data-ttu-id="fad0c-109">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="fad0c-109">Clean up deployment</span></span>

<span data-ttu-id="fad0c-110">После выполнения сценария образец hello hello, следующая команда может быть группы ресурсов используется tooremove hello и все ресурсы, связанные с ним.</span><span class="sxs-lookup"><span data-stu-id="fad0c-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="fad0c-111">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="fad0c-111">Script explanation</span></span>

<span data-ttu-id="fad0c-112">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="fad0c-112">This script uses hello following commands.</span></span> <span data-ttu-id="fad0c-113">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="fad0c-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="fad0c-114">Команда</span><span class="sxs-lookup"><span data-stu-id="fad0c-114">Command</span></span> | <span data-ttu-id="fad0c-115">Примечания</span><span class="sxs-lookup"><span data-stu-id="fad0c-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fad0c-116">az group create</span><span class="sxs-lookup"><span data-stu-id="fad0c-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="fad0c-117">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="fad0c-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fad0c-118">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="fad0c-118">az cosmosdb create</span></span>](/cli/azure/sql/server#create) | <span data-ttu-id="fad0c-119">Создает учетную запись базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fad0c-119">Creates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="fad0c-120">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="fad0c-120">az cosmosdb update</span></span>](/cli/azure/cosmosdb#update) | <span data-ttu-id="fad0c-121">Обновляет учетную запись базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fad0c-121">Updates Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="fad0c-122">az group delete</span><span class="sxs-lookup"><span data-stu-id="fad0c-122">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="fad0c-123">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="fad0c-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fad0c-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fad0c-124">Next steps</span></span>

<span data-ttu-id="fad0c-125">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fad0c-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fad0c-126">Дополнительные примеры сценариев, использующих DB Cosmos Azure CLI можно найти в hello [документации Azure Cosmos DB CLI](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="fad0c-126">Additional Azure Cosmos DB CLI script samples can be found in hello [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
