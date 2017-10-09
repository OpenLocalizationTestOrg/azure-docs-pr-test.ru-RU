---
title: "Пример aaaCLI масштабируется SQL базы данных SQL эластичный пул Azure | Документы Microsoft"
description: "Azure CLI пример сценария tooscale гибкий пул SQL в базе данных SQL Azure"
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
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 436128b8183213f78b9abc2ec46efe2a3ed3c37c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-tooscale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="79ae1-103">Использовать tooscale CLI гибкий пул SQL в базе данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="79ae1-103">Use CLI tooscale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="79ae1-104">Этот пример сценария Azure CLI создает эластичные пулы SQL и перемещает базы данных в составе пулов, а также изменяет уровни производительности эластичных пулов.</span><span class="sxs-lookup"><span data-stu-id="79ae1-104">This Azure CLI script example creates SQL elastic pools, moves pooled databases, and changes elastic pool performance levels.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="79ae1-105">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="79ae1-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="79ae1-106">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="79ae1-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="79ae1-107">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="79ae1-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="79ae1-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="79ae1-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "Move database between pools")]

## <a name="clean-up-deployment"></a><span data-ttu-id="79ae1-109">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="79ae1-109">Clean up deployment</span></span>

<span data-ttu-id="79ae1-110">После выполнения сценария образец hello hello, следующая команда может быть группы ресурсов используется tooremove hello и все ресурсы, связанные с ним.</span><span class="sxs-lookup"><span data-stu-id="79ae1-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="79ae1-111">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="79ae1-111">Script explanation</span></span>

<span data-ttu-id="79ae1-112">Этот скрипт использует hello следующие команды toocreate группы ресурсов, логического сервера, базы данных SQL и правила брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="79ae1-112">This script uses hello following commands toocreate a resource group, logical server, SQL Database, and firewall rules.</span></span> <span data-ttu-id="79ae1-113">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="79ae1-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="79ae1-114">Команда</span><span class="sxs-lookup"><span data-stu-id="79ae1-114">Command</span></span> | <span data-ttu-id="79ae1-115">Примечания</span><span class="sxs-lookup"><span data-stu-id="79ae1-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="79ae1-116">az group create</span><span class="sxs-lookup"><span data-stu-id="79ae1-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="79ae1-117">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="79ae1-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="79ae1-118">az sql server create</span><span class="sxs-lookup"><span data-stu-id="79ae1-118">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="79ae1-119">Создает логический сервер, что узлы hello базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="79ae1-119">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="79ae1-120">az sql elastic-pools create</span><span class="sxs-lookup"><span data-stu-id="79ae1-120">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="79ae1-121">Создает пул эластичных баз данных в логическом сервере hello.</span><span class="sxs-lookup"><span data-stu-id="79ae1-121">Creates an elastic database pool within hello logical server.</span></span> |
| [<span data-ttu-id="79ae1-122">az sql db create</span><span class="sxs-lookup"><span data-stu-id="79ae1-122">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="79ae1-123">Создает hello базы данных SQL в логическом сервере hello.</span><span class="sxs-lookup"><span data-stu-id="79ae1-123">Creates hello SQL Database in hello logical server.</span></span> |
| [<span data-ttu-id="79ae1-124">az sql elastic-pools update</span><span class="sxs-lookup"><span data-stu-id="79ae1-124">az sql elastic-pools update</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#update) | <span data-ttu-id="79ae1-125">Обновляет пул эластичных баз данных в этот пример hello изменений, назначенный eDTU.</span><span class="sxs-lookup"><span data-stu-id="79ae1-125">Updates an elastic database pool, in this example changes hello assigned eDTU.</span></span> |
| [<span data-ttu-id="79ae1-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="79ae1-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="79ae1-127">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="79ae1-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="79ae1-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="79ae1-128">Next steps</span></span>

<span data-ttu-id="79ae1-129">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="79ae1-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="79ae1-130">Дополнительные образцы сценариев CLI базы данных SQL можно найти в hello [документации по базе данных SQL Azure](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="79ae1-130">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
