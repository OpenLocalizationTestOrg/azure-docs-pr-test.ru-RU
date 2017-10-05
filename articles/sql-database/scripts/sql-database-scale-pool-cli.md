---
title: "Пример для CLI. Масштабирование эластичного пула SQL в Базе данных SQL Azure | Документация Майкрософт"
description: "Пример сценария Azure CLI для масштабирования эластичного пула SQL в Базе данных SQL Azure."
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
ms.openlocfilehash: 888d2b7b7c118fede82d39881570a3b3d7b09961
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="use-cli-to-scale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="eab87-103">Масштабирование эластичного пула SQL в Базе данных SQL Azure с помощью интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="eab87-103">Use CLI to scale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="eab87-104">Этот пример сценария Azure CLI создает эластичные пулы SQL и перемещает базы данных в составе пулов, а также изменяет уровни производительности эластичных пулов.</span><span class="sxs-lookup"><span data-stu-id="eab87-104">This Azure CLI script example creates SQL elastic pools, moves pooled databases, and changes elastic pool performance levels.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="eab87-105">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="eab87-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="eab87-106">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="eab87-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="eab87-107">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="eab87-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="eab87-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="eab87-108">Sample script</span></span>

<span data-ttu-id="eab87-109">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "Перемещение базы данных между пулами")]</span><span class="sxs-lookup"><span data-stu-id="eab87-109">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "Move database between pools")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="eab87-110">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="eab87-110">Clean up deployment</span></span>

<span data-ttu-id="eab87-111">После выполнения примера сценария можно удалить группу ресурсов и все связанные с ней ресурсы, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="eab87-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="eab87-112">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="eab87-112">Script explanation</span></span>

<span data-ttu-id="eab87-113">Для создания группы ресурсов, логического сервера, базы данных SQL и правил брандмауэра этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="eab87-113">This script uses the following commands to create a resource group, logical server, SQL Database, and firewall rules.</span></span> <span data-ttu-id="eab87-114">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="eab87-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="eab87-115">Команда</span><span class="sxs-lookup"><span data-stu-id="eab87-115">Command</span></span> | <span data-ttu-id="eab87-116">Примечания</span><span class="sxs-lookup"><span data-stu-id="eab87-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="eab87-117">az group create</span><span class="sxs-lookup"><span data-stu-id="eab87-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="eab87-118">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="eab87-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="eab87-119">az sql server create</span><span class="sxs-lookup"><span data-stu-id="eab87-119">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="eab87-120">Создает логический сервер, на котором размещена база данных SQL.</span><span class="sxs-lookup"><span data-stu-id="eab87-120">Creates a logical server that hosts the SQL Database.</span></span> |
| [<span data-ttu-id="eab87-121">az sql elastic-pools create</span><span class="sxs-lookup"><span data-stu-id="eab87-121">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="eab87-122">Создает пул эластичных баз данных на логическом сервере.</span><span class="sxs-lookup"><span data-stu-id="eab87-122">Creates an elastic database pool within the logical server.</span></span> |
| [<span data-ttu-id="eab87-123">az sql db create</span><span class="sxs-lookup"><span data-stu-id="eab87-123">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="eab87-124">Создает базу данных SQL на логическом сервере.</span><span class="sxs-lookup"><span data-stu-id="eab87-124">Creates the SQL Database in the logical server.</span></span> |
| [<span data-ttu-id="eab87-125">az sql elastic-pools update</span><span class="sxs-lookup"><span data-stu-id="eab87-125">az sql elastic-pools update</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#update) | <span data-ttu-id="eab87-126">Обновляет пул эластичных баз данных. В этом примере также изменяется назначенная eDTU.</span><span class="sxs-lookup"><span data-stu-id="eab87-126">Updates an elastic database pool, in this example changes the assigned eDTU.</span></span> |
| [<span data-ttu-id="eab87-127">az group delete</span><span class="sxs-lookup"><span data-stu-id="eab87-127">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="eab87-128">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="eab87-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="eab87-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="eab87-129">Next steps</span></span>

<span data-ttu-id="eab87-130">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="eab87-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="eab87-131">Дополнительные примеры сценариев интерфейса командной строки для Базы данных SQL Azure см. в [документации по Базе данных SQL](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="eab87-131">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
