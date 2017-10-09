---
title: "AAA» Azure CLI Script – создать базу данных Azure для MySQL | Документы Microsoft»"
description: "Этот пример скрипта CLI создает сервер базы данных Azure для MySQL и настраивает правило брандмауэра на уровне сервера."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.custom: mvc
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: 1d619ee0547efd8275eaf7c1347b6c3427025c3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-mysql-server-and-configure-a-firewall-rule-using-hello-azure-cli"></a><span data-ttu-id="0a7fc-103">Создать сервер MySQL и настройка правила брандмауэра с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0a7fc-103">Create a MySQL server and configure a firewall rule using hello Azure CLI</span></span>
<span data-ttu-id="0a7fc-104">Этот пример скрипта CLI создает сервер базы данных Azure для MySQL и настраивает правило брандмауэра на уровне сервера.</span><span class="sxs-lookup"><span data-stu-id="0a7fc-104">This sample CLI script creates an Azure Database for MySQL server and configures a server-level firewall rule.</span></span> <span data-ttu-id="0a7fc-105">После успешного выполнения сценария hello hello MySQL server доступен для всех служб Azure и IP-адрес настроен hello.</span><span class="sxs-lookup"><span data-stu-id="0a7fc-105">Once hello script runs successfully, hello MySQL server is accessible by all Azure services and hello configured IP address.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0a7fc-106">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="0a7fc-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="0a7fc-107">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="0a7fc-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="0a7fc-108">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0a7fc-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="0a7fc-109">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="0a7fc-109">Sample script</span></span>
<span data-ttu-id="0a7fc-110">В этот образец скрипта измените hello выделенной строки toocustomize hello имя и пароль администратора.</span><span class="sxs-lookup"><span data-stu-id="0a7fc-110">In this sample script, edit hello highlighted lines toocustomize hello admin username and password.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/create-mysql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for MySQL, and server-level firewall rule.")]

## <a name="clean-up-deployment"></a><span data-ttu-id="0a7fc-111">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="0a7fc-111">Clean up deployment</span></span>
<span data-ttu-id="0a7fc-112">После выполнения сценария образец hello hello, следующая команда может быть группы ресурсов используется tooremove hello и все ресурсы, связанные с ним.</span><span class="sxs-lookup"><span data-stu-id="0a7fc-112">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/delete-mysql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="0a7fc-113">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="0a7fc-113">Script explanation</span></span>
<span data-ttu-id="0a7fc-114">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="0a7fc-114">This script uses hello following commands.</span></span> <span data-ttu-id="0a7fc-115">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="0a7fc-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="0a7fc-116">**Команда**</span><span class="sxs-lookup"><span data-stu-id="0a7fc-116">**Command**</span></span> | <span data-ttu-id="0a7fc-117">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="0a7fc-117">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="0a7fc-118">az group create</span><span class="sxs-lookup"><span data-stu-id="0a7fc-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="0a7fc-119">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="0a7fc-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0a7fc-120">az mysql server create</span><span class="sxs-lookup"><span data-stu-id="0a7fc-120">az mysql server create</span></span>](/cli/azure/mysql/server#create) | <span data-ttu-id="0a7fc-121">Создает сервер MySQL, содержащий hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="0a7fc-121">Creates a MySQL server that hosts hello databases.</span></span> |
| [<span data-ttu-id="0a7fc-122">az mysql server firewall create</span><span class="sxs-lookup"><span data-stu-id="0a7fc-122">az mysql server firewall create</span></span>](/cli/azure/mysql/server/firewall-rule#create) | <span data-ttu-id="0a7fc-123">Создает сервер toohello доступа tooallow правило межсетевого экрана и базы данных, из hello ввести диапазон IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="0a7fc-123">Creates a firewall rule tooallow access toohello server and databases under it from hello entered IP address range.</span></span> |
| [<span data-ttu-id="0a7fc-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="0a7fc-124">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="0a7fc-125">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="0a7fc-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0a7fc-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0a7fc-126">Next steps</span></span>
- <span data-ttu-id="0a7fc-127">Дополнительные сведения о hello Azure CLI: [документации Azure CLI](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0a7fc-127">Read more information on hello Azure CLI: [Azure CLI documentation](/cli/azure/overview).</span></span>
- <span data-ttu-id="0a7fc-128">Попробуйте использовать другие скрипты на основе [примеров Azure CLI для базы данных Azure для MySQL](../sample-scripts-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="0a7fc-128">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
