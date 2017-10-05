---
title: "Пример для CLI. Создание базы данных SQL Azure | Документация Майкрософт"
description: "Пример сценария Azure CLI для создания базы данных SQL."
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
ms.openlocfilehash: 908898ca691d2b53b9f54afa60c41e091163bd50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-cli-to-create-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="5b56c-103">Создание отдельной базы данных SQL и настройка правила брандмауэра с помощью интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="5b56c-103">Use CLI to create a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="5b56c-104">Этот пример сценария Azure CLI создает базу данных SQL Azure и настраивает правило брандмауэра уровня сервера.</span><span class="sxs-lookup"><span data-stu-id="5b56c-104">This Azure CLI script example creates an Azure SQL database and configure a server-level firewall rule.</span></span> <span data-ttu-id="5b56c-105">После успешного выполнения скрипта доступ к базе данных SQL можно получить из всех служб Azure, а также по настроенному IP-адресу.</span><span class="sxs-lookup"><span data-stu-id="5b56c-105">Once the script has been successfully run, the SQL Database can be accessed from all Azure services and the configured IP address.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5b56c-106">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="5b56c-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="5b56c-107">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="5b56c-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="5b56c-108">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5b56c-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="5b56c-109">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="5b56c-109">Sample script</span></span>

<span data-ttu-id="5b56c-110">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/create-and-configure-database/create-and-configure-database.sh?highlight=9-10 "Создание базы данных SQL")]</span><span class="sxs-lookup"><span data-stu-id="5b56c-110">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/create-and-configure-database/create-and-configure-database.sh?highlight=9-10 "Create SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="5b56c-111">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="5b56c-111">Clean up deployment</span></span>

<span data-ttu-id="5b56c-112">После выполнения примера сценария можно удалить группу ресурсов и все связанные с ней ресурсы, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="5b56c-112">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="5b56c-113">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="5b56c-113">Script explanation</span></span>

<span data-ttu-id="5b56c-114">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="5b56c-114">This script uses the following commands.</span></span> <span data-ttu-id="5b56c-115">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="5b56c-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5b56c-116">Команда</span><span class="sxs-lookup"><span data-stu-id="5b56c-116">Command</span></span> | <span data-ttu-id="5b56c-117">Примечания</span><span class="sxs-lookup"><span data-stu-id="5b56c-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5b56c-118">az group create</span><span class="sxs-lookup"><span data-stu-id="5b56c-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="5b56c-119">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="5b56c-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5b56c-120">az sql server create</span><span class="sxs-lookup"><span data-stu-id="5b56c-120">az sql server create</span></span>](/cli/azure/sql/server#create) | <span data-ttu-id="5b56c-121">Создает логический сервер, на котором размещена база данных SQL.</span><span class="sxs-lookup"><span data-stu-id="5b56c-121">Creates a logical server that hosts the SQL Database.</span></span> |
| [<span data-ttu-id="5b56c-122">az sql server firewall create</span><span class="sxs-lookup"><span data-stu-id="5b56c-122">az sql server firewall create</span></span>](/cli/azure/sql/server/firewall-rule#create) | <span data-ttu-id="5b56c-123">Создает правило брандмауэра, чтобы разрешить доступ ко всем базам данных SQL на сервере по введенному диапазону IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="5b56c-123">Creates a firewall rule to allow access to all SQL Databases on the server from the entered IP address range.</span></span> |
| [<span data-ttu-id="5b56c-124">az sql db create</span><span class="sxs-lookup"><span data-stu-id="5b56c-124">az sql db create</span></span>](/cli/azure/sql/db#create) | <span data-ttu-id="5b56c-125">Создает базу данных SQL на логическом сервере.</span><span class="sxs-lookup"><span data-stu-id="5b56c-125">Creates the SQL Database in the logical server.</span></span> |
| [<span data-ttu-id="5b56c-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="5b56c-126">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="5b56c-127">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="5b56c-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5b56c-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5b56c-128">Next steps</span></span>

<span data-ttu-id="5b56c-129">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5b56c-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5b56c-130">Дополнительные примеры сценариев интерфейса командной строки для Базы данных SQL Azure см. в [документации по Базе данных SQL](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5b56c-130">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>

