---
title: "базы данных Azure SQL в пример монитора шкалы одним aaaCLI | Документы Microsoft"
description: "Azure CLI пример сценария toomonitor и масштаб одной базы данных Azure SQL"
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
ms.openlocfilehash: 36031ddd46a947a80fe37884858a84eb66217270
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toomonitor-and-scale-a-single-sql-database"></a><span data-ttu-id="dc0cd-103">Используйте CLI toomonitor и масштабировать одной базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="dc0cd-103">Use CLI toomonitor and scale a single SQL database</span></span>

<span data-ttu-id="dc0cd-104">В этом примере сценария Azure CLI масштабирует один уровень производительности tooa базы данных Azure SQL после выполнения запроса к hello сведения о размере базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="dc0cd-104">This Azure CLI script example scales a single Azure SQL database tooa different performance level after querying hello size information of hello database.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="dc0cd-105">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="dc0cd-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="dc0cd-106">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="dc0cd-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="dc0cd-107">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="dc0cd-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="dc0cd-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="dc0cd-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.sh "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="dc0cd-109">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="dc0cd-109">Clean up deployment</span></span>

<span data-ttu-id="dc0cd-110">После выполнения сценария образец hello hello, следующая команда может быть группы ресурсов используется tooremove hello и все ресурсы, связанные с ним.</span><span class="sxs-lookup"><span data-stu-id="dc0cd-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="dc0cd-111">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="dc0cd-111">Script explanation</span></span>

<span data-ttu-id="dc0cd-112">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="dc0cd-112">This script uses hello following commands.</span></span> <span data-ttu-id="dc0cd-113">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="dc0cd-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="dc0cd-114">Команда</span><span class="sxs-lookup"><span data-stu-id="dc0cd-114">Command</span></span> | <span data-ttu-id="dc0cd-115">Примечания</span><span class="sxs-lookup"><span data-stu-id="dc0cd-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="dc0cd-116">az group create</span><span class="sxs-lookup"><span data-stu-id="dc0cd-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="dc0cd-117">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="dc0cd-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="dc0cd-118">az sql server create</span><span class="sxs-lookup"><span data-stu-id="dc0cd-118">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="dc0cd-119">Создает логический сервер, на котором размещена база данных.</span><span class="sxs-lookup"><span data-stu-id="dc0cd-119">Creates a logical server that hosts a database.</span></span> |
| [<span data-ttu-id="dc0cd-120">az sql db show-usage</span><span class="sxs-lookup"><span data-stu-id="dc0cd-120">az sql db show-usage</span></span>](https://docs.microsoft.com/cli/azure/sql/db#show-usage) | <span data-ttu-id="dc0cd-121">Показывает сведения об использовании hello размер для базы данных.</span><span class="sxs-lookup"><span data-stu-id="dc0cd-121">Shows hello size usage information for a database.</span></span> |
| [<span data-ttu-id="dc0cd-122">az sql db update</span><span class="sxs-lookup"><span data-stu-id="dc0cd-122">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="dc0cd-123">Обновляет свойства базы данных (например, «hello службы уровня или уровня производительности) или перемещает базу данных в, из или между эластичные пулы.</span><span class="sxs-lookup"><span data-stu-id="dc0cd-123">Updates database properties (such as hello service tier or performance level) or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="dc0cd-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="dc0cd-124">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="dc0cd-125">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="dc0cd-125">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="dc0cd-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dc0cd-126">Next steps</span></span>

<span data-ttu-id="dc0cd-127">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dc0cd-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="dc0cd-128">Дополнительные образцы сценариев CLI базы данных SQL можно найти в hello [документации по базе данных SQL Azure](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="dc0cd-128">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
