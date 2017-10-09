---
title: "AAA» Azure CLI Script – создать базу данных Azure для PostgreSQL | Документы Microsoft»"
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
ms.openlocfilehash: bbe31f77283aa4a3bb36d1fd9171c280594a8267
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-postgresql-server-and-configure-a-firewall-rule-using-hello-azure-cli"></a><span data-ttu-id="68803-103">Создание базы данных Azure для сервера PostgreSQL и настройка правила брандмауэра с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="68803-103">Create an Azure Database for PostgreSQL server and configure a firewall rule using hello Azure CLI</span></span>
<span data-ttu-id="68803-104">Этот пример скрипта CLI создает сервер базы данных Azure для PostgreSQL и настраивает правило брандмауэра на уровне сервера.</span><span class="sxs-lookup"><span data-stu-id="68803-104">This sample CLI script creates an Azure Database for PostgreSQL server and configures a server-level firewall rule.</span></span> <span data-ttu-id="68803-105">После успешного выполнения сценария hello hello PostgreSQL сервера может осуществляться из всех служб Azure и IP-адрес настроен hello.</span><span class="sxs-lookup"><span data-stu-id="68803-105">Once hello script has been successfully run, hello PostgreSQL server can be accessed from all Azure services and hello configured IP address.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="68803-106">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="68803-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="68803-107">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="68803-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="68803-108">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="68803-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="68803-109">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="68803-109">Sample script</span></span>
<span data-ttu-id="68803-110">В этот образец скрипта измените hello выделенной строки toocustomize hello имя и пароль администратора.</span><span class="sxs-lookup"><span data-stu-id="68803-110">In this sample script, edit hello highlighted lines toocustomize hello admin username and password.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/create-postgresql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for PostgreSQL, and server-level firewall rule.")]

## <a name="clean-up-deployment"></a><span data-ttu-id="68803-111">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="68803-111">Clean up deployment</span></span>
<span data-ttu-id="68803-112">После выполнения сценария образец hello hello, следующая команда может быть группы ресурсов используется tooremove hello и все ресурсы, связанные с ним.</span><span class="sxs-lookup"><span data-stu-id="68803-112">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/delete-postgresql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="68803-113">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="68803-113">Script explanation</span></span>
<span data-ttu-id="68803-114">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="68803-114">This script uses hello following commands.</span></span> <span data-ttu-id="68803-115">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="68803-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="68803-116">**Команда**</span><span class="sxs-lookup"><span data-stu-id="68803-116">**Command**</span></span> | <span data-ttu-id="68803-117">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="68803-117">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="68803-118">az group create</span><span class="sxs-lookup"><span data-stu-id="68803-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="68803-119">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="68803-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="68803-120">az postgres server create</span><span class="sxs-lookup"><span data-stu-id="68803-120">az postgres server create</span></span>](/cli/azure/postgres/server#create) | <span data-ttu-id="68803-121">Создает сервер PostgreSQL, на котором размещены базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="68803-121">Creates a PostgreSQL server that hosts hello databases.</span></span> |
| [<span data-ttu-id="68803-122">az postgres server firewall create</span><span class="sxs-lookup"><span data-stu-id="68803-122">az postgres server firewall create</span></span>](/cli/azure/postgres/server/firewall-rule#create) | <span data-ttu-id="68803-123">Создает сервер toohello доступа tooallow правило межсетевого экрана и базы данных, из hello ввести диапазон IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="68803-123">Creates a firewall rule tooallow access toohello server and databases under it from hello entered IP address range.</span></span> |
| [<span data-ttu-id="68803-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="68803-124">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="68803-125">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="68803-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="68803-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="68803-126">Next steps</span></span>
- <span data-ttu-id="68803-127">Дополнительные сведения о hello Azure CLI: [документации Azure CLI](/cli/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="68803-127">Read more information on hello Azure CLI: [Azure CLI documentation](/cli/azure/overview)</span></span>
- <span data-ttu-id="68803-128">Попробуйте использовать другие скрипты на основе [примеров Azure CLI для базы данных Azure для PostgreSQL](../sample-scripts-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="68803-128">Try additional scripts: [Azure CLI samples for Azure Database for PostgreSQL](../sample-scripts-azure-cli.md)</span></span>
