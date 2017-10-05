---
title: "Проектирование первой базы данных Azure для PostgreSQL с помощью Azure CLI | Документация Майкрософт"
description: "Это руководство содержит сведения о проектировании первой базы данных Azure для PostgreSQL с помощью Azure CLI."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: azure-cli
ms.topic: tutorial
ms.date: 06/13/2017
ms.openlocfilehash: cf536fce8925f9173b541b845af25a8d8c38eabd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-azure-cli"></a><span data-ttu-id="4decc-103">Проектирование первой базы данных Azure для PostgreSQL с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4decc-103">Design your first Azure Database for PostgreSQL using Azure CLI</span></span> 
<span data-ttu-id="4decc-104">Из этого руководства вы узнаете, как с помощью Azure CLI (интерфейса командной строки) и других служебных программ выполнять следующие операции:</span><span class="sxs-lookup"><span data-stu-id="4decc-104">In this tutorial, you use Azure CLI (command-line interface) and other utilities to learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="4decc-105">создание базы данных Azure для PostgreSQL;</span><span class="sxs-lookup"><span data-stu-id="4decc-105">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="4decc-106">настройка брандмауэра сервера;</span><span class="sxs-lookup"><span data-stu-id="4decc-106">Configure the server firewall</span></span>
> * <span data-ttu-id="4decc-107">использование служебной программы [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) для создания базы данных;</span><span class="sxs-lookup"><span data-stu-id="4decc-107">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility to create a database</span></span>
> * <span data-ttu-id="4decc-108">Загрузка примера данных</span><span class="sxs-lookup"><span data-stu-id="4decc-108">Load sample data</span></span>
> * <span data-ttu-id="4decc-109">Запрос данных</span><span class="sxs-lookup"><span data-stu-id="4decc-109">Query data</span></span>
> * <span data-ttu-id="4decc-110">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="4decc-110">Update data</span></span>
> * <span data-ttu-id="4decc-111">восстановление данных.</span><span class="sxs-lookup"><span data-stu-id="4decc-111">Restore data</span></span>

<span data-ttu-id="4decc-112">Вы можете использовать Azure Cloud Shell в браузере или [установить Azure CLI 2.0]( /cli/azure/install-azure-cli) на компьютере, чтобы запустить блоки кода в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="4decc-112">You may use the Azure Cloud Shell in the browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer to run the code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4decc-113">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="4decc-113">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="4decc-114">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="4decc-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="4decc-115">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4decc-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="4decc-116">Если вы используете несколько подписок, выберите соответствующую подписку, в которой находится ресурс либо в которой за него взимается плата.</span><span class="sxs-lookup"><span data-stu-id="4decc-116">If you have multiple subscriptions, choose the appropriate subscription in which the resource exists or is billed for.</span></span> <span data-ttu-id="4decc-117">Выберите конкретный идентификатор подписки вашей учетной записи, выполнив команду [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="4decc-117">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="4decc-118">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="4decc-118">Create a resource group</span></span>
<span data-ttu-id="4decc-119">Создайте [группу ресурсов Azure](../azure-resource-manager/resource-group-overview.md) с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="4decc-119">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="4decc-120">Группа ресурсов — это логический контейнер, в котором ресурсы Azure развертываются и администрируются как группа.</span><span class="sxs-lookup"><span data-stu-id="4decc-120">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="4decc-121">В следующем примере создается группа ресурсов с именем `myresourcegroup` в расположении `westus`.</span><span class="sxs-lookup"><span data-stu-id="4decc-121">The following example creates a resource group named `myresourcegroup` in the `westus` location.</span></span>
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="4decc-122">Создание сервера базы данных Azure для PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="4decc-122">Create an Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="4decc-123">Создайте [сервер базы данных Azure для PostgreSQL](overview.md), выполнив команду [az postgres server create](/cli/azure/postgres/server#create).</span><span class="sxs-lookup"><span data-stu-id="4decc-123">Create an [Azure Database for PostgreSQL server](overview.md) using the [az postgres server create](/cli/azure/postgres/server#create) command.</span></span> <span data-ttu-id="4decc-124">Сервер содержит группу баз данных, которыми можно управлять как группой.</span><span class="sxs-lookup"><span data-stu-id="4decc-124">A server contains a group of databases managed as a group.</span></span> 

<span data-ttu-id="4decc-125">В указанном ниже примере в группе ресурсов `myresourcegroup` создается сервер `mypgserver-20170401` с именем для входа администратора сервера `mylogin`.</span><span class="sxs-lookup"><span data-stu-id="4decc-125">The following example creates a server called `mypgserver-20170401` in your resource group `myresourcegroup` with server admin login `mylogin`.</span></span> <span data-ttu-id="4decc-126">Имя сервера сопоставляется с DNS-именем, и поэтому оно должно быть глобально уникальным в рамках Azure.</span><span class="sxs-lookup"><span data-stu-id="4decc-126">Name of a server maps to DNS name and is thus required to be globally unique in Azure.</span></span> <span data-ttu-id="4decc-127">Замените `<server_admin_password>` собственным значением.</span><span class="sxs-lookup"><span data-stu-id="4decc-127">Substitute the `<server_admin_password>` with your own value.</span></span>
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401 --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> <span data-ttu-id="4decc-128">Указанные здесь учетные данные и пароль администратора сервера понадобятся позже в этом руководстве, чтобы войти на сервер и в его базу данных.</span><span class="sxs-lookup"><span data-stu-id="4decc-128">The server admin login and password that you specify here are required to log in to the server and its databases later in this quick start.</span></span> <span data-ttu-id="4decc-129">Запомните или запишите эту информацию для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="4decc-129">Remember or record this information for later use.</span></span>

<span data-ttu-id="4decc-130">По умолчанию на сервере создается база данных **postgres**.</span><span class="sxs-lookup"><span data-stu-id="4decc-130">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="4decc-131">База данных [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) — это база данных по умолчанию, предназначенная для использования пользователями, служебными программами и сторонними приложениями.</span><span class="sxs-lookup"><span data-stu-id="4decc-131">The [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 


## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="4decc-132">Настройка правила брандмауэра на уровне сервера</span><span class="sxs-lookup"><span data-stu-id="4decc-132">Configure a server-level firewall rule</span></span>

<span data-ttu-id="4decc-133">Создайте правило брандмауэра на уровне сервера Azure PostgreSQL, выполнив команду [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create).</span><span class="sxs-lookup"><span data-stu-id="4decc-133">Create an Azure PostgreSQL server-level firewall rule with the [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> <span data-ttu-id="4decc-134">Правило брандмауэра на уровне сервера позволяет внешним приложениям, таким как [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) или [PgAdmin](https://www.pgadmin.org/), подключаться к серверу через брандмауэр службы Azure PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="4decc-134">A server-level firewall rule allows an external application, such as [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) or [PgAdmin](https://www.pgadmin.org/) to connect to your server through the Azure PostgreSQL service firewall.</span></span> 

<span data-ttu-id="4decc-135">Вы можете задать правило брандмауэра, охватывающее диапазон IP-адресов, которые могут подключаться из сети.</span><span class="sxs-lookup"><span data-stu-id="4decc-135">You can set a firewall rule that covers an IP range to be able to connect from your network.</span></span> <span data-ttu-id="4decc-136">В указанном ниже примере для создания правила брандмауэра `AllowAllIps` для диапазона IP-адресов используется команда [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create).</span><span class="sxs-lookup"><span data-stu-id="4decc-136">The following example uses [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) to create a firewall rule `AllowAllIps` for an IP address range.</span></span> <span data-ttu-id="4decc-137">Чтобы открыть все IP-адреса, используйте 0.0.0.0 как начальный IP-адрес, а 255.255.255.255 — как конечный.</span><span class="sxs-lookup"><span data-stu-id="4decc-137">To open all IP addresses, use 0.0.0.0 as the starting IP address and 255.255.255.255 as the ending address.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="4decc-138">Сервер PostgreSQL Azure обменивается данными через порт 5432.</span><span class="sxs-lookup"><span data-stu-id="4decc-138">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="4decc-139">При попытках подключения из корпоративной сети может оказаться, что исходящий трафик через порт 5432 запрещен сетевым брандмауэром.</span><span class="sxs-lookup"><span data-stu-id="4decc-139">When connecting from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="4decc-140">Чтобы вы могли подключиться к серверу базы данных SQL Azure, ваш ИТ-отдел должен открыть порт 5432.</span><span class="sxs-lookup"><span data-stu-id="4decc-140">Have your IT department open port 5432 to connect to your Azure SQL Database server.</span></span>
>

## <a name="get-the-connection-information"></a><span data-ttu-id="4decc-141">Получение сведений о подключении</span><span class="sxs-lookup"><span data-stu-id="4decc-141">Get the connection information</span></span>

<span data-ttu-id="4decc-142">Чтобы подключиться к серверу, необходимо указать сведения об узле и учетные данные для доступа.</span><span class="sxs-lookup"><span data-stu-id="4decc-142">To connect to your server, you need to provide host information and access credentials.</span></span>
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

<span data-ttu-id="4decc-143">Результаты выводятся в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="4decc-143">The result is in JSON format.</span></span> <span data-ttu-id="4decc-144">Запишите **administratorLogin** и **fullyQualifiedDomainName**.</span><span class="sxs-lookup"><span data-stu-id="4decc-144">Make a note of the **administratorLogin** and **fullyQualifiedDomainName**.</span></span>
```json
{
  "administratorLogin": "mylogin",
  "fullyQualifiedDomainName": "mypgserver-20170401.postgres.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforPostgreSQL/servers/mypgserver-20170401",
  "location": "westus",
  "name": "mypgserver-20170401",
  "resourceGroup": "myresourcegroup",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "PGSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "sslEnforcement": null,
  "storageMb": 51200,
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": "9.6"
}
```

## <a name="connect-to-azure-database-for-postgresql-database-using-psql"></a><span data-ttu-id="4decc-145">Подключение к базе данных Azure для PostgreSQL с помощью psql</span><span class="sxs-lookup"><span data-stu-id="4decc-145">Connect to Azure Database for PostgreSQL database using psql</span></span>
<span data-ttu-id="4decc-146">Если на клиентском компьютере установлено PostgreSQL, вы можете использовать локальный экземпляр [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) или консоль облачной службы Azure, чтобы подключиться к серверу Azure PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="4decc-146">If your client computer has PostgreSQL installed, you can use a local instance of [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), or the Azure Cloud Console to connect to an Azure PostgreSQL server.</span></span> <span data-ttu-id="4decc-147">Теперь подключимся к серверу базы данных Azure для PostgreSQL с помощью служебной программы командной строки psql.</span><span class="sxs-lookup"><span data-stu-id="4decc-147">Let's now use the psql command-line utility to connect to the Azure Database for PostgreSQL server.</span></span>

1. <span data-ttu-id="4decc-148">Чтобы подключиться к серверу базы данных Azure для PostgreSQL, выполните следующую команду psql:</span><span class="sxs-lookup"><span data-stu-id="4decc-148">Run the following psql command to connect to an Azure Database for PostgreSQL server</span></span>
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  <span data-ttu-id="4decc-149">Например, следующая команда устанавливает подключение к базе данных по умолчанию **postgres** на сервере PostgreSQL **mypgserver-20170401.postgres.database.azure.com**, используя учетные данные для доступа.</span><span class="sxs-lookup"><span data-stu-id="4decc-149">For example, the following command connects to the default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="4decc-150">Введите `<server_admin_password>`, указанный при появлении запроса на ввод пароля.</span><span class="sxs-lookup"><span data-stu-id="4decc-150">Enter the `<server_admin_password>` you chose when prompted for password.</span></span>
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 ---dbname=postgres
```

2.  <span data-ttu-id="4decc-151">Подключившись к серверу, создайте пустую базу данных с помощью командной строки.</span><span class="sxs-lookup"><span data-stu-id="4decc-151">Once you are connected to the server, create a blank database at the prompt.</span></span>
```sql
CREATE DATABASE mypgsqldb;
```

3.  <span data-ttu-id="4decc-152">Чтобы подключиться к созданной базе данных **mypgsqldb**, выполните следующую команду в командной строке:</span><span class="sxs-lookup"><span data-stu-id="4decc-152">At the prompt, execute the following command to switch connection to the newly created database **mypgsqldb**:</span></span>
```sql
\c mypgsqldb
```

## <a name="create-tables-in-the-database"></a><span data-ttu-id="4decc-153">Создание таблиц в базе данных</span><span class="sxs-lookup"><span data-stu-id="4decc-153">Create tables in the database</span></span>
<span data-ttu-id="4decc-154">Теперь, когда вы знаете, как подключиться к базе данных Azure для PostgreSQL, рассмотрим, как выполнить некоторые основные задачи.</span><span class="sxs-lookup"><span data-stu-id="4decc-154">Now that you know how to connect to the Azure Database for PostgreSQL, we can go over how to complete some basic tasks.</span></span>

<span data-ttu-id="4decc-155">Сначала можно создать таблицу и заполнить ее некоторыми данными.</span><span class="sxs-lookup"><span data-stu-id="4decc-155">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="4decc-156">Давайте создадим таблицу, с помощью которой можно отслеживать данные инвентаризации.</span><span class="sxs-lookup"><span data-stu-id="4decc-156">Let's create a table that tracks inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

<span data-ttu-id="4decc-157">Вы можете просмотреть созданную таблицу в списке таблиц, введя:</span><span class="sxs-lookup"><span data-stu-id="4decc-157">You can see the newly created table in the list of tables now by typing:</span></span>
```sql
\dt
```

## <a name="load-data-into-the-tables"></a><span data-ttu-id="4decc-158">Загрузка данных в таблицу</span><span class="sxs-lookup"><span data-stu-id="4decc-158">Load data into the tables</span></span>
<span data-ttu-id="4decc-159">Теперь, когда таблица создана, мы можем вставить в нее данные.</span><span class="sxs-lookup"><span data-stu-id="4decc-159">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="4decc-160">Чтобы вставить некоторые строки данных, в открытом окне командной строки выполните следующий запрос:</span><span class="sxs-lookup"><span data-stu-id="4decc-160">At the open command prompt window, run the following query to insert some rows of data</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="4decc-161">Итак, в созданной ранее таблице содержится две строки данных.</span><span class="sxs-lookup"><span data-stu-id="4decc-161">You have now two rows of sample data into the table you created earlier.</span></span>

## <a name="query-and-update-the-data-in-the-tables"></a><span data-ttu-id="4decc-162">Запрос и обновление данных в таблицах</span><span class="sxs-lookup"><span data-stu-id="4decc-162">Query and update the data in the tables</span></span>
<span data-ttu-id="4decc-163">Чтобы извлечь сведения из таблицы базы данных, выполните приведенный ниже запрос.</span><span class="sxs-lookup"><span data-stu-id="4decc-163">Execute the following query to retrieve information from the database table.</span></span> 
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="4decc-164">Вы можете также обновить данные в таблицах, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4decc-164">You can also update the data in the tables</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="4decc-165">При извлечении данных строка будет обновляться соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="4decc-165">The row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-to-a-previous-point-in-time"></a><span data-ttu-id="4decc-166">Восстановление базы данных до предыдущей точки во времени</span><span class="sxs-lookup"><span data-stu-id="4decc-166">Restore a database to a previous point in time</span></span>
<span data-ttu-id="4decc-167">Представьте, что вы случайно удалили таблицу.</span><span class="sxs-lookup"><span data-stu-id="4decc-167">Imagine you have accidentally deleted a table.</span></span> <span data-ttu-id="4decc-168">Восстановить ее будет не просто.</span><span class="sxs-lookup"><span data-stu-id="4decc-168">This is something you cannot easily recover from.</span></span> <span data-ttu-id="4decc-169">База данных Azure для PostgreSQL позволяет вернуться в любой момент времени (в течение последних 7 дней (для уровня "Базовый") и 35 дней (для уровня "Стандартный")) и восстановить данные на определенный момент времени на новом сервере.</span><span class="sxs-lookup"><span data-stu-id="4decc-169">Azure Database for PostgreSQL allows you to go back to any point-in-time (in the last up to 7 days (Basic) and 35 days (Standard)) and restore this point-in-time to a new server.</span></span> <span data-ttu-id="4decc-170">Вы можете восстановить удаленные данные с помощью нового сервера.</span><span class="sxs-lookup"><span data-stu-id="4decc-170">You can use this new server to recover your deleted data.</span></span> <span data-ttu-id="4decc-171">Указанные ниже шаги позволяют восстановить сервер до точки во времени, когда была создана таблица.</span><span class="sxs-lookup"><span data-stu-id="4decc-171">The following steps restore the sample server to a point before the table was added.</span></span>

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

<span data-ttu-id="4decc-172">Для команды `az postgres server restore` необходимо настроить следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="4decc-172">The `az postgres server restore` command needs the following parameters:</span></span>
| <span data-ttu-id="4decc-173">Настройка</span><span class="sxs-lookup"><span data-stu-id="4decc-173">Setting</span></span> | <span data-ttu-id="4decc-174">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="4decc-174">Suggested value</span></span> | <span data-ttu-id="4decc-175">Описание</span><span class="sxs-lookup"><span data-stu-id="4decc-175">Description</span></span>  |
| --- | --- | --- |
| <span data-ttu-id="4decc-176">--resource-group</span><span class="sxs-lookup"><span data-stu-id="4decc-176">--resource-group</span></span> |  <span data-ttu-id="4decc-177">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4decc-177">myResourceGroup</span></span> |  <span data-ttu-id="4decc-178">Группа ресурсов, в которой находится исходный сервер.</span><span class="sxs-lookup"><span data-stu-id="4decc-178">The resource group in which the source server exists.</span></span>  |
| <span data-ttu-id="4decc-179">--name</span><span class="sxs-lookup"><span data-stu-id="4decc-179">--name</span></span> | <span data-ttu-id="4decc-180">mypgserver-restored</span><span class="sxs-lookup"><span data-stu-id="4decc-180">mypgserver-restored</span></span> | <span data-ttu-id="4decc-181">Имя нового сервера, созданного командой restore.</span><span class="sxs-lookup"><span data-stu-id="4decc-181">The name of the new server that is created by the restore command.</span></span> |
| <span data-ttu-id="4decc-182">restore-point-in-time</span><span class="sxs-lookup"><span data-stu-id="4decc-182">restore-point-in-time</span></span> | <span data-ttu-id="4decc-183">2017-04-13T13:59:00Z</span><span class="sxs-lookup"><span data-stu-id="4decc-183">2017-04-13T13:59:00Z</span></span> | <span data-ttu-id="4decc-184">Выберите точку во времени, до которой необходимо выполнить восстановление.</span><span class="sxs-lookup"><span data-stu-id="4decc-184">Select a point-in-time to restore to.</span></span> <span data-ttu-id="4decc-185">Значения даты и времени должны находиться в пределах срока хранения резервной копии исходного сервера.</span><span class="sxs-lookup"><span data-stu-id="4decc-185">This date and time must be within the source server's backup retention period.</span></span> <span data-ttu-id="4decc-186">Используйте формат даты и времени ISO8601.</span><span class="sxs-lookup"><span data-stu-id="4decc-186">Use ISO8601 date and time format.</span></span> <span data-ttu-id="4decc-187">Например, вы можете использовать свой местный часовой пояс, например `2017-04-13T05:59:00-08:00`, или использовать формат UTC Zulu `2017-04-13T13:59:00Z`.</span><span class="sxs-lookup"><span data-stu-id="4decc-187">For example, you may use your own local timezone, such as `2017-04-13T05:59:00-08:00`, or use UTC Zulu format `2017-04-13T13:59:00Z`.</span></span> |
| <span data-ttu-id="4decc-188">--source-server</span><span class="sxs-lookup"><span data-stu-id="4decc-188">--source-server</span></span> | <span data-ttu-id="4decc-189">mypgserver-20170401</span><span class="sxs-lookup"><span data-stu-id="4decc-189">mypgserver-20170401</span></span> | <span data-ttu-id="4decc-190">Имя или идентификатор исходного сервера, с которого необходимо выполнить восстановление.</span><span class="sxs-lookup"><span data-stu-id="4decc-190">The name or ID of the source server to restore from.</span></span> |

<span data-ttu-id="4decc-191">При восстановлении сервера до определенной точки во времени создается сервер путем копирования исходного сервера на заданный момент времени.</span><span class="sxs-lookup"><span data-stu-id="4decc-191">Restoring a server to a point-in-time creates a new server, copying as the original server as of the point in time you specify.</span></span> <span data-ttu-id="4decc-192">Значения расположения и ценовой категории для восстановленного сервера совпадают со значениями исходного сервера.</span><span class="sxs-lookup"><span data-stu-id="4decc-192">The location and pricing tier values for the restored server are the same as the source server.</span></span>

<span data-ttu-id="4decc-193">Команда выполняется в синхронном режиме и будет возвращена после восстановления сервера.</span><span class="sxs-lookup"><span data-stu-id="4decc-193">The command is synchronous, and will return after the server is restored.</span></span> <span data-ttu-id="4decc-194">После завершения восстановления найдите созданный сервер.</span><span class="sxs-lookup"><span data-stu-id="4decc-194">Once the restore finishes, locate the new server that was created.</span></span> <span data-ttu-id="4decc-195">Убедитесь, что данные восстановлены надлежащим образом.</span><span class="sxs-lookup"><span data-stu-id="4decc-195">Verify the data was restored as expected.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4decc-196">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4decc-196">Next steps</span></span>
<span data-ttu-id="4decc-197">Из этого руководства вы узнали, как с помощью Azure CLI (интерфейса командной строки) и других служебных программ выполнить следующие операции:</span><span class="sxs-lookup"><span data-stu-id="4decc-197">In this tutorial, you learned how to use Azure CLI (command-line interface) and other utilities to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="4decc-198">создание базы данных Azure для PostgreSQL;</span><span class="sxs-lookup"><span data-stu-id="4decc-198">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="4decc-199">настройка брандмауэра сервера;</span><span class="sxs-lookup"><span data-stu-id="4decc-199">Configure the server firewall</span></span>
> * <span data-ttu-id="4decc-200">использование служебной программы [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) для создания базы данных;</span><span class="sxs-lookup"><span data-stu-id="4decc-200">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility to create a database</span></span>
> * <span data-ttu-id="4decc-201">Загрузка примера данных</span><span class="sxs-lookup"><span data-stu-id="4decc-201">Load sample data</span></span>
> * <span data-ttu-id="4decc-202">Запрос данных</span><span class="sxs-lookup"><span data-stu-id="4decc-202">Query data</span></span>
> * <span data-ttu-id="4decc-203">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="4decc-203">Update data</span></span>
> * <span data-ttu-id="4decc-204">восстановление данных.</span><span class="sxs-lookup"><span data-stu-id="4decc-204">Restore data</span></span>

<span data-ttu-id="4decc-205">Чтобы узнать, как выполнять похожие задачи с помощью портала Azure, см. сведения в руководстве [Проектирование первой базы данных Azure для PostgreSQL с помощью портала Azure](tutorial-design-database-using-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4decc-205">Next, learn how to use the Azure portal to do similar tasks, review this tutorial: [Design your first Azure Database for PostgreSQL using the Azure portal](tutorial-design-database-using-azure-portal.md)</span></span>
