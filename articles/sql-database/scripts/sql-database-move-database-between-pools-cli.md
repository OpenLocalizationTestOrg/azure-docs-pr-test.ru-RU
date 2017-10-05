---
title: "Пример для CLI. Перемещение базы данных SQL Azure в эластичный пул SQL | Документация Майкрософт"
description: "Пример сценария Azure CLI для перемещения базы данных SQL в эластичном пуле SQL."
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 07/05/2017
ms.author: janeng
ms.openlocfilehash: 1dc31a0b20f36e28a58896ed63a5e0395ae1d3af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-cli-to-move-an-azure-sql-database-in-a-sql-elastic-pool"></a><span data-ttu-id="fa43a-103">Перемещение базы данных Azure SQL в эластичном пуле SQL с помощью интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="fa43a-103">Use CLI to move an Azure SQL database in a SQL elastic pool</span></span>

<span data-ttu-id="fa43a-104">Этот пример сценария Azure CLI создает два эластичных пула и перемещает базу данных SQL Azure из одного пула в другой, а затем перемещает базу данных из этого эластичного пула на уровень производительности отдельной базы данных Azure.</span><span class="sxs-lookup"><span data-stu-id="fa43a-104">This Azure CLI script example creates two elastic pools and moves an Azure SQL database from one SQL elastic pool into another SQL elastic pool, and then moves the database out of elastic pool to a single Azure database performance level.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="fa43a-105">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="fa43a-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="fa43a-106">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="fa43a-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="fa43a-107">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fa43a-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="fa43a-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="fa43a-108">Sample script</span></span>

<span data-ttu-id="fa43a-109">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/move-database-between-pools/move-database-between-pools.sh "Перемещение базы данных между пулами")]</span><span class="sxs-lookup"><span data-stu-id="fa43a-109">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/move-database-between-pools/move-database-between-pools.sh "Move database between pools")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="fa43a-110">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="fa43a-110">Clean up deployment</span></span>

<span data-ttu-id="fa43a-111">После выполнения примера сценария можно удалить группу ресурсов и все связанные с ней ресурсы, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="fa43a-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="fa43a-112">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="fa43a-112">Script explanation</span></span>

<span data-ttu-id="fa43a-113">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="fa43a-113">This script uses the following commands.</span></span> <span data-ttu-id="fa43a-114">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="fa43a-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="fa43a-115">Команда</span><span class="sxs-lookup"><span data-stu-id="fa43a-115">Command</span></span> | <span data-ttu-id="fa43a-116">Примечания</span><span class="sxs-lookup"><span data-stu-id="fa43a-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fa43a-117">az group create</span><span class="sxs-lookup"><span data-stu-id="fa43a-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="fa43a-118">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="fa43a-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fa43a-119">az sql server create</span><span class="sxs-lookup"><span data-stu-id="fa43a-119">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="fa43a-120">Создает логический сервер, на котором размещена база данных или эластичный пул.</span><span class="sxs-lookup"><span data-stu-id="fa43a-120">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="fa43a-121">az sql elastic-pools create</span><span class="sxs-lookup"><span data-stu-id="fa43a-121">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="fa43a-122">Создает эластичный пул на логическом сервере.</span><span class="sxs-lookup"><span data-stu-id="fa43a-122">Creates an elastic pool within the logical server.</span></span> |
| [<span data-ttu-id="fa43a-123">az sql db create</span><span class="sxs-lookup"><span data-stu-id="fa43a-123">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="fa43a-124">Создает на логическом сервере отдельную базу данных или базу данных в составе пула.</span><span class="sxs-lookup"><span data-stu-id="fa43a-124">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="fa43a-125">az sql db update</span><span class="sxs-lookup"><span data-stu-id="fa43a-125">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="fa43a-126">Обновляет свойства базы данных или перемещает базу данных в эластичный пул, из него или между эластичными пулами.</span><span class="sxs-lookup"><span data-stu-id="fa43a-126">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="fa43a-127">az group delete</span><span class="sxs-lookup"><span data-stu-id="fa43a-127">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="fa43a-128">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="fa43a-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fa43a-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fa43a-129">Next steps</span></span>

<span data-ttu-id="fa43a-130">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fa43a-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fa43a-131">Дополнительные примеры сценариев интерфейса командной строки для Базы данных SQL Azure см. в [документации по Базе данных SQL](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="fa43a-131">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>


