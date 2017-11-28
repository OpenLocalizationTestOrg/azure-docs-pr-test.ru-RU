---
title: "Создание политики отработки отказа с помощью скрипта Azure CLI для обеспечения высокой доступности | Документация Майкрософт"
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
ms.openlocfilehash: 96083d66cc1a2ef179f9313c1b3ed04162c1c048
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-failover-policy-for-high-availability-using-the-azure-cli"></a><span data-ttu-id="4e1e6-103">Создание политики отработки отказа для обеспечения высокой доступности с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4e1e6-103">Create a failover policy for high availability using the Azure CLI</span></span>

<span data-ttu-id="4e1e6-104">Данный пример скрипта CLI создает учетную запись базы данных Azure Cosmos DB, а затем настраивает ее для обеспечения высокой доступности.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-104">This sample CLI script creates an Azure Cosmos DB account, and then configures it for high availability.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4e1e6-105">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="4e1e6-106">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="4e1e6-107">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4e1e6-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="4e1e6-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="4e1e6-108">Sample script</span></span>

<span data-ttu-id="4e1e6-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/high-availability-cosmosdb-configure-failover/high-availability-cosmosdb-configure-failover.sh?highlight=23-27 "Создание политики отработки отказа для базы данных Azure Cosmos DB")]</span><span class="sxs-lookup"><span data-stu-id="4e1e6-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/high-availability-cosmosdb-configure-failover/high-availability-cosmosdb-configure-failover.sh?highlight=23-27 "Create an Azure Cosmos DB failover policy")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="4e1e6-110">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="4e1e6-110">Clean up deployment</span></span>

<span data-ttu-id="4e1e6-111">После выполнения примера сценария можно удалить группу ресурсов и все связанные с ней ресурсы, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="4e1e6-112">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="4e1e6-112">Script explanation</span></span>

<span data-ttu-id="4e1e6-113">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-113">This script uses the following commands.</span></span> <span data-ttu-id="4e1e6-114">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="4e1e6-115">Команда</span><span class="sxs-lookup"><span data-stu-id="4e1e6-115">Command</span></span> | <span data-ttu-id="4e1e6-116">Примечания</span><span class="sxs-lookup"><span data-stu-id="4e1e6-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4e1e6-117">az group create</span><span class="sxs-lookup"><span data-stu-id="4e1e6-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="4e1e6-118">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4e1e6-119">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="4e1e6-119">az cosmosdb create</span></span>](/cli/azure/sql/server#create) | <span data-ttu-id="4e1e6-120">Создает учетную запись базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-120">Creates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="4e1e6-121">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="4e1e6-121">az cosmosdb update</span></span>](/cli/azure/cosmosdb#update) | <span data-ttu-id="4e1e6-122">Обновляет учетную запись базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-122">Updates Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="4e1e6-123">az group delete</span><span class="sxs-lookup"><span data-stu-id="4e1e6-123">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="4e1e6-124">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="4e1e6-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4e1e6-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4e1e6-125">Next steps</span></span>

<span data-ttu-id="4e1e6-126">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4e1e6-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="4e1e6-127">Дополнительные примеры скриптов CLI для базы данных Azure Cosmos DB см. в [документации по интерфейсу командной строки базы данных Azure Cosmos DB](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4e1e6-127">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
