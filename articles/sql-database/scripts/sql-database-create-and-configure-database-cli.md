---
title: "aaaCLI пример создания базы данных Azure SQL | Документы Microsoft"
description: "Azure CLI пример сценария toocreate базы данных SQL"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 0d54e284e19f16387813e24d7beb7ab048a39263
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toocreate-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="53f36-103">Используйте toocreate CLI одной базы данных Azure SQL и настройте правила брандмауэра</span><span class="sxs-lookup"><span data-stu-id="53f36-103">Use CLI toocreate a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="53f36-104">Этот пример сценария Azure CLI создает базу данных SQL Azure и настраивает правило брандмауэра уровня сервера.</span><span class="sxs-lookup"><span data-stu-id="53f36-104">This Azure CLI script example creates an Azure SQL database and configure a server-level firewall rule.</span></span> <span data-ttu-id="53f36-105">После успешного выполнения сценария hello приветствия базы данных SQL может осуществляться из всех служб Azure и hello настроить IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="53f36-105">Once hello script has been successfully run, hello SQL Database can be accessed from all Azure services and hello configured IP address.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="53f36-106">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="53f36-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="53f36-107">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="53f36-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="53f36-108">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="53f36-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="53f36-109">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="53f36-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/create-and-configure-database/create-and-configure-database.sh?highlight=9-10 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="53f36-110">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="53f36-110">Clean up deployment</span></span>

<span data-ttu-id="53f36-111">После выполнения сценария образец hello hello, следующая команда может быть группы ресурсов используется tooremove hello и все ресурсы, связанные с ним.</span><span class="sxs-lookup"><span data-stu-id="53f36-111">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="53f36-112">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="53f36-112">Script explanation</span></span>

<span data-ttu-id="53f36-113">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="53f36-113">This script uses hello following commands.</span></span> <span data-ttu-id="53f36-114">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="53f36-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="53f36-115">Команда</span><span class="sxs-lookup"><span data-stu-id="53f36-115">Command</span></span> | <span data-ttu-id="53f36-116">Примечания</span><span class="sxs-lookup"><span data-stu-id="53f36-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="53f36-117">az group create</span><span class="sxs-lookup"><span data-stu-id="53f36-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="53f36-118">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="53f36-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="53f36-119">az sql server create</span><span class="sxs-lookup"><span data-stu-id="53f36-119">az sql server create</span></span>](/cli/azure/sql/server#create) | <span data-ttu-id="53f36-120">Создает логический сервер, что узлы hello базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="53f36-120">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="53f36-121">az sql server firewall create</span><span class="sxs-lookup"><span data-stu-id="53f36-121">az sql server firewall create</span></span>](/cli/azure/sql/server/firewall-rule#create) | <span data-ttu-id="53f36-122">Создает брандмауэра правило tooallow доступа tooall баз данных SQL на сервере hello из hello ввести диапазон IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="53f36-122">Creates a firewall rule tooallow access tooall SQL Databases on hello server from hello entered IP address range.</span></span> |
| [<span data-ttu-id="53f36-123">az sql db create</span><span class="sxs-lookup"><span data-stu-id="53f36-123">az sql db create</span></span>](/cli/azure/sql/db#create) | <span data-ttu-id="53f36-124">Создает hello базы данных SQL в логическом сервере hello.</span><span class="sxs-lookup"><span data-stu-id="53f36-124">Creates hello SQL Database in hello logical server.</span></span> |
| [<span data-ttu-id="53f36-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="53f36-125">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="53f36-126">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="53f36-126">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="53f36-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="53f36-127">Next steps</span></span>

<span data-ttu-id="53f36-128">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="53f36-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="53f36-129">Дополнительные образцы сценариев CLI базы данных SQL можно найти в hello [документации по базе данных SQL Azure](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="53f36-129">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>

