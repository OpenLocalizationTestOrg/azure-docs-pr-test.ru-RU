---
title: "Скрипт Azure CLI. Создание базы данных Azure для PostgreSQL | Документация Майкрософт"
description: "Здесь приведен пример скрипта Azure CLI, который создает сервер базы данных Azure для PostgreSQL и настраивает правило брандмауэра на уровне сервера."
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: azure-cli
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: e545b568cd57fdcf28ab33a5ebfa34a495111c7f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-azure-database-for-postgresql-server-and-configure-a-firewall-rule-using-the-azure-cli"></a><span data-ttu-id="eb8d5-103">Создание сервера базы данных Azure для PostgreSQL и настройка правила брандмауэра с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="eb8d5-103">Create an Azure Database for PostgreSQL server and configure a firewall rule using the Azure CLI</span></span>
<span data-ttu-id="eb8d5-104">Этот пример скрипта CLI создает сервер базы данных Azure для PostgreSQL и настраивает правило брандмауэра на уровне сервера.</span><span class="sxs-lookup"><span data-stu-id="eb8d5-104">This sample CLI script creates an Azure Database for PostgreSQL server and configures a server-level firewall rule.</span></span> <span data-ttu-id="eb8d5-105">После успешного выполнения скрипта доступ к серверу PostgreSQL можно получить из всех служб Azure, а также по настроенному IP-адресу.</span><span class="sxs-lookup"><span data-stu-id="eb8d5-105">Once the script has been successfully run, the PostgreSQL server can be accessed from all Azure services and the configured IP address.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="eb8d5-106">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="eb8d5-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="eb8d5-107">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="eb8d5-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="eb8d5-108">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="eb8d5-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="eb8d5-109">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="eb8d5-109">Sample script</span></span>
<span data-ttu-id="eb8d5-110">В этом примере скрипта измените выделенные строки, чтобы настроить имя и пароль администратора.</span><span class="sxs-lookup"><span data-stu-id="eb8d5-110">In this sample script, edit the highlighted lines to customize the admin username and password.</span></span>
<span data-ttu-id="eb8d5-111">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/create-postgresql-server-and-firewall-rule.sh?highlight=15-16 "Создание базы данных Azure для PostgreSQL и правила брандмауэра на уровне сервера.")]</span><span class="sxs-lookup"><span data-stu-id="eb8d5-111">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/create-postgresql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for PostgreSQL, and server-level firewall rule.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="eb8d5-112">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="eb8d5-112">Clean up deployment</span></span>
<span data-ttu-id="eb8d5-113">После выполнения примера сценария можно удалить группу ресурсов и все связанные с ней ресурсы, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="eb8d5-113">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>
<span data-ttu-id="eb8d5-114">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/delete-postgresql.sh "Удаление группы ресурсов.")]</span><span class="sxs-lookup"><span data-stu-id="eb8d5-114">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/delete-postgresql.sh "Delete the resource group.")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="eb8d5-115">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="eb8d5-115">Script explanation</span></span>
<span data-ttu-id="eb8d5-116">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="eb8d5-116">This script uses the following commands.</span></span> <span data-ttu-id="eb8d5-117">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="eb8d5-117">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="eb8d5-118">**Команда**</span><span class="sxs-lookup"><span data-stu-id="eb8d5-118">**Command**</span></span> | <span data-ttu-id="eb8d5-119">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="eb8d5-119">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="eb8d5-120">az group create</span><span class="sxs-lookup"><span data-stu-id="eb8d5-120">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="eb8d5-121">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="eb8d5-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="eb8d5-122">az postgres server create</span><span class="sxs-lookup"><span data-stu-id="eb8d5-122">az postgres server create</span></span>](/cli/azure/postgres/server#create) | <span data-ttu-id="eb8d5-123">Создает сервер PostgreSQL, на котором размещены базы данных.</span><span class="sxs-lookup"><span data-stu-id="eb8d5-123">Creates a PostgreSQL server that hosts the databases.</span></span> |
| [<span data-ttu-id="eb8d5-124">az postgres server firewall create</span><span class="sxs-lookup"><span data-stu-id="eb8d5-124">az postgres server firewall create</span></span>](/cli/azure/postgres/server/firewall-rule#create) | <span data-ttu-id="eb8d5-125">Создает правило брандмауэра, чтобы разрешить доступ к серверу и размещенным на нем базам данных по введенному диапазону IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="eb8d5-125">Creates a firewall rule to allow access to the server and databases under it from the entered IP address range.</span></span> |
| [<span data-ttu-id="eb8d5-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="eb8d5-126">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="eb8d5-127">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="eb8d5-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="eb8d5-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="eb8d5-128">Next steps</span></span>
- <span data-ttu-id="eb8d5-129">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="eb8d5-129">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure/overview)</span></span>
- <span data-ttu-id="eb8d5-130">Попробуйте использовать другие скрипты на основе [примеров Azure CLI для базы данных Azure для PostgreSQL](../sample-scripts-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="eb8d5-130">Try additional scripts: [Azure CLI samples for Azure Database for PostgreSQL](../sample-scripts-azure-cli.md)</span></span>
