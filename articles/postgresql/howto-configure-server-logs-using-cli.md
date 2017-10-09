---
title: "aaaConfigure и доступа в журналах сервера с помощью Azure CLI PostgreSQL | Документы Microsoft"
description: "В этой статье описывается, как tooconfigure и доступа hello в журналах сервера в базе данных Azure PostgreSQL, с помощью командной строки Azure CLI."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 924d4e7634cc48405bcb0f813cf61d8b72ad8aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-access-server-logs-using-azure-cli"></a><span data-ttu-id="84764-103">Настройка журналов сервера и получение к ним доступа с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="84764-103">Configure and access server logs using Azure CLI</span></span>
<span data-ttu-id="84764-104">Можно загрузить с помощью командной строки (CLI Azure) hello ошибки журналы hello PostgreSQL сервера.</span><span class="sxs-lookup"><span data-stu-id="84764-104">You can download hello PostgreSQL server error logs using hello Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="84764-105">Тем не менее журналы tootransaction доступа не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="84764-105">However, access tootransaction logs is not supported.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="84764-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="84764-106">Prerequisites</span></span>
<span data-ttu-id="84764-107">toostep через этот как tooguide необходимо:</span><span class="sxs-lookup"><span data-stu-id="84764-107">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="84764-108">[сервер базы данных Azure для PostgreSQL](quickstart-create-server-database-azure-cli.md);</span><span class="sxs-lookup"><span data-stu-id="84764-108">An [Azure Database for PostgreSQL server](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="84764-109">Установка [Azure CLI 2.0](/cli/azure/install-azure-cli) командной строки программы или используйте hello оболочки облако Azure в обозревателе hello.</span><span class="sxs-lookup"><span data-stu-id="84764-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command-line utility or use hello Azure Cloud Shell in hello browser.</span></span>

## <a name="configure-logging-for-azure-database-for-postgresql"></a><span data-ttu-id="84764-110">Настройка ведения журнала для базы данных Azure для PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="84764-110">Configure logging for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="84764-111">Можно настроить hello server tooaccess запроса журналы и журналы ошибок.</span><span class="sxs-lookup"><span data-stu-id="84764-111">You can configure hello server tooaccess query logs and error logs.</span></span> <span data-ttu-id="84764-112">Журналы ошибок могут содержать сведения об автоматической очистке, подключениях и контрольных точках.</span><span class="sxs-lookup"><span data-stu-id="84764-112">Error logs can contain auto-vacuum, connection, and checkpoints information.</span></span>
1. <span data-ttu-id="84764-113">Включите ведение журнала.</span><span class="sxs-lookup"><span data-stu-id="84764-113">Turn on logging</span></span>
2. <span data-ttu-id="84764-114">Журнал обновления\_инструкции и журнала\_min\_длительность\_ведение журнала запросов tooenable инструкции</span><span class="sxs-lookup"><span data-stu-id="84764-114">Update log\_statement and log\_min\_duration\_statement tooenable query logging</span></span>
3. <span data-ttu-id="84764-115">Измените срок хранения.</span><span class="sxs-lookup"><span data-stu-id="84764-115">Update retention period</span></span>

<span data-ttu-id="84764-116">Дополнительные сведения см. в статье [Настройка параметров конфигурации сервера с помощью Azure CLI](howto-configure-server-parameters-using-cli.md).</span><span class="sxs-lookup"><span data-stu-id="84764-116">For more information, see [customizing server configuration parameters](howto-configure-server-parameters-using-cli.md).</span></span>

## <a name="list-logs-for-azure-database-for-postgresql-server"></a><span data-ttu-id="84764-117">Получение списка журналов для базы данных Azure для сервера PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="84764-117">List logs for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="84764-118">toolist hello доступные файлы журнала для сервера, запустите hello [az postgres журналы сервера список](/cli/azure/postgres/server-logs#list) команды.</span><span class="sxs-lookup"><span data-stu-id="84764-118">toolist hello available log files for your server, run hello [az postgres server-logs list](/cli/azure/postgres/server-logs#list) command.</span></span>

<span data-ttu-id="84764-119">Можно получить список файлов журнала hello для сервера **mypgserver 20170401.postgres.database.azure.com** группе ресурсов **myresourcegroup**и направить его tooa текстовый файл с именем **журнала\_файлы\_list.txt.**</span><span class="sxs-lookup"><span data-stu-id="84764-119">You can list hello log files for server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup**, and direct it tooa text file called **log\_files\_list.txt.**</span></span>
```azurecli-interactive
az postgres server-logs list --resource-group myresourcegroup --server mypgserver-20170401 > log_files_list.txt
```
## <a name="download-logs-locally-from-hello-server"></a><span data-ttu-id="84764-120">Локально загружать журналы с сервера hello</span><span class="sxs-lookup"><span data-stu-id="84764-120">Download logs locally from hello server</span></span>
<span data-ttu-id="84764-121">Hello [загрузить журналы сервера в postgres az](/cli/azure/postgres/server-logs#download) позволяет вам toodownload отдельные файлы журналов для вашего сервера.</span><span class="sxs-lookup"><span data-stu-id="84764-121">hello [az postgres server-logs download](/cli/azure/postgres/server-logs#download) command allows you toodownload individual log files for your server.</span></span> 

<span data-ttu-id="84764-122">В этом примере загрузки hello файла журнала конкретного сервера hello **mypgserver 20170401.postgres.database.azure.com** группе ресурсов **myresourcegroup** tooyour локальной среде.</span><span class="sxs-lookup"><span data-stu-id="84764-122">This example downloads hello specific log file for hello server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup** tooyour local environment.</span></span>
```azurecli-interactive
az postgres server-logs download --name 20170414-mypgserver-20170401-postgresql.log --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="next-steps"></a><span data-ttu-id="84764-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="84764-123">Next steps</span></span>
- <span data-ttu-id="84764-124">toolearn Дополнительные сведения о журналах сервера. в разделе [журналы сервера в базе данных Azure для PostgreSQL](concepts-server-logs.md)</span><span class="sxs-lookup"><span data-stu-id="84764-124">toolearn more about server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
- <span data-ttu-id="84764-125">Дополнительные сведения о параметрах сервера см. в статье [Настройка параметров конфигурации сервера с помощью Azure CLI](howto-configure-server-parameters-using-cli.md).</span><span class="sxs-lookup"><span data-stu-id="84764-125">For more information on server parameters, see [Customize server configuration parameters using Azure CLI](howto-configure-server-parameters-using-cli.md)</span></span>
