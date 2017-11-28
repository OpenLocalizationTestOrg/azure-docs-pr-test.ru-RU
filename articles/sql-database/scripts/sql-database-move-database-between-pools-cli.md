---
title: "гибкий пул Azure SQL пример перемещения базы данных SQL aaaCLI | Документы Microsoft"
description: "Azure CLI пример сценария toomove базы данных SQL в пуле эластичных БД SQL"
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
ms.openlocfilehash: 841eb57d2d49612c3fadd3a6424a2b0309c69719
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toomove-an-azure-sql-database-in-a-sql-elastic-pool"></a><span data-ttu-id="661bb-103">Использовать toomove CLI из базы данных Azure SQL в пуле эластичных БД SQL</span><span class="sxs-lookup"><span data-stu-id="661bb-103">Use CLI toomove an Azure SQL database in a SQL elastic pool</span></span>

<span data-ttu-id="661bb-104">В этом примере сценария Azure CLI создает два пула эластичных и перемещает базу данных Azure SQL из одного гибкий пул SQL в другой гибкий пул SQL и затем перемещает hello базы данных вне уровня производительности для одной базы данных Azure tooa эластичного пула.</span><span class="sxs-lookup"><span data-stu-id="661bb-104">This Azure CLI script example creates two elastic pools and moves an Azure SQL database from one SQL elastic pool into another SQL elastic pool, and then moves hello database out of elastic pool tooa single Azure database performance level.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="661bb-105">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="661bb-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="661bb-106">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="661bb-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="661bb-107">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="661bb-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="661bb-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="661bb-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/move-database-between-pools/move-database-between-pools.sh "Move database between pools")]

## <a name="clean-up-deployment"></a><span data-ttu-id="661bb-109">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="661bb-109">Clean up deployment</span></span>

<span data-ttu-id="661bb-110">После выполнения сценария образец hello hello, следующая команда может быть группы ресурсов используется tooremove hello и все ресурсы, связанные с ним.</span><span class="sxs-lookup"><span data-stu-id="661bb-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="661bb-111">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="661bb-111">Script explanation</span></span>

<span data-ttu-id="661bb-112">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="661bb-112">This script uses hello following commands.</span></span> <span data-ttu-id="661bb-113">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="661bb-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="661bb-114">Команда</span><span class="sxs-lookup"><span data-stu-id="661bb-114">Command</span></span> | <span data-ttu-id="661bb-115">Примечания</span><span class="sxs-lookup"><span data-stu-id="661bb-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="661bb-116">az group create</span><span class="sxs-lookup"><span data-stu-id="661bb-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="661bb-117">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="661bb-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="661bb-118">az sql server create</span><span class="sxs-lookup"><span data-stu-id="661bb-118">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="661bb-119">Создает логический сервер, на котором размещена база данных или эластичный пул.</span><span class="sxs-lookup"><span data-stu-id="661bb-119">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="661bb-120">az sql elastic-pools create</span><span class="sxs-lookup"><span data-stu-id="661bb-120">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="661bb-121">Создает пул эластичных БД в логическом сервере hello.</span><span class="sxs-lookup"><span data-stu-id="661bb-121">Creates an elastic pool within hello logical server.</span></span> |
| [<span data-ttu-id="661bb-122">az sql db create</span><span class="sxs-lookup"><span data-stu-id="661bb-122">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="661bb-123">Создает на логическом сервере отдельную базу данных или базу данных в составе пула.</span><span class="sxs-lookup"><span data-stu-id="661bb-123">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="661bb-124">az sql db update</span><span class="sxs-lookup"><span data-stu-id="661bb-124">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="661bb-125">Обновляет свойства базы данных или перемещает базу данных в эластичный пул, из него или между эластичными пулами.</span><span class="sxs-lookup"><span data-stu-id="661bb-125">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="661bb-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="661bb-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="661bb-127">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="661bb-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="661bb-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="661bb-128">Next steps</span></span>

<span data-ttu-id="661bb-129">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="661bb-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="661bb-130">Дополнительные образцы сценариев CLI базы данных SQL можно найти в hello [документации по базе данных SQL Azure](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="661bb-130">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>


