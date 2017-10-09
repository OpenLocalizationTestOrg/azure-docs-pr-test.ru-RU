---
title: "Проектирование первой базы данных Azure для PostgreSQL с помощью Azure CLI | Документация Майкрософт"
description: "В этом учебнике показано, как tooDesign Azure первой базы данных для PostgreSQL с помощью Azure CLI."
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
ms.openlocfilehash: 7914925c090e0b6f3e7c8a999eedb0b2baf83d7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-azure-cli"></a><span data-ttu-id="1d139-103">Проектирование первой базы данных Azure для PostgreSQL с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1d139-103">Design your first Azure Database for PostgreSQL using Azure CLI</span></span> 
<span data-ttu-id="1d139-104">В этом учебнике используется Azure CLI (интерфейс командной строки) и другие служебные программы toolearn как для:</span><span class="sxs-lookup"><span data-stu-id="1d139-104">In this tutorial, you use Azure CLI (command-line interface) and other utilities toolearn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="1d139-105">Создание базы данных Azure для PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="1d139-105">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="1d139-106">Настройте брандмауэр сервера hello</span><span class="sxs-lookup"><span data-stu-id="1d139-106">Configure hello server firewall</span></span>
> * <span data-ttu-id="1d139-107">Используйте [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) toocreate программа базы данных</span><span class="sxs-lookup"><span data-stu-id="1d139-107">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility toocreate a database</span></span>
> * <span data-ttu-id="1d139-108">Загрузка примера данных</span><span class="sxs-lookup"><span data-stu-id="1d139-108">Load sample data</span></span>
> * <span data-ttu-id="1d139-109">Запрос данных</span><span class="sxs-lookup"><span data-stu-id="1d139-109">Query data</span></span>
> * <span data-ttu-id="1d139-110">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="1d139-110">Update data</span></span>
> * <span data-ttu-id="1d139-111">восстановление данных.</span><span class="sxs-lookup"><span data-stu-id="1d139-111">Restore data</span></span>

<span data-ttu-id="1d139-112">Вы можете использовать hello оболочки облако Azure в обозревателе hello, или [установить CLI Azure 2.0]( /cli/azure/install-azure-cli) на блоки собственного компьютера toorun hello в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="1d139-112">You may use hello Azure Cloud Shell in hello browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer toorun hello code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="1d139-113">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="1d139-113">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="1d139-114">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="1d139-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="1d139-115">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1d139-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="1d139-116">Если у вас несколько подписок, выберите нужную подписку hello, в котором hello ресурсов существует, или плата за.</span><span class="sxs-lookup"><span data-stu-id="1d139-116">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span> <span data-ttu-id="1d139-117">Выберите конкретный идентификатор подписки вашей учетной записи, выполнив команду [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="1d139-117">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="1d139-118">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="1d139-118">Create a resource group</span></span>
<span data-ttu-id="1d139-119">Создание [группы ресурсов Azure](../azure-resource-manager/resource-group-overview.md) с помощью hello [Создание группы az](/cli/azure/group#create) команды.</span><span class="sxs-lookup"><span data-stu-id="1d139-119">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="1d139-120">Группа ресурсов — это логический контейнер, в котором ресурсы Azure развертываются и администрируются как группа.</span><span class="sxs-lookup"><span data-stu-id="1d139-120">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="1d139-121">Hello следующий пример создает группу ресурсов с именем `myresourcegroup` в hello `westus` расположение.</span><span class="sxs-lookup"><span data-stu-id="1d139-121">hello following example creates a resource group named `myresourcegroup` in hello `westus` location.</span></span>
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="1d139-122">Создание сервера базы данных Azure для PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="1d139-122">Create an Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="1d139-123">Создание [базы данных Azure для сервера PostgreSQL](overview.md) с помощью hello [az postgres server создать](/cli/azure/postgres/server#create) команды.</span><span class="sxs-lookup"><span data-stu-id="1d139-123">Create an [Azure Database for PostgreSQL server](overview.md) using hello [az postgres server create](/cli/azure/postgres/server#create) command.</span></span> <span data-ttu-id="1d139-124">Сервер содержит группу баз данных, которыми можно управлять как группой.</span><span class="sxs-lookup"><span data-stu-id="1d139-124">A server contains a group of databases managed as a group.</span></span> 

<span data-ttu-id="1d139-125">Hello следующий пример создает сервер называется `mypgserver-20170401` в группе ресурсов `myresourcegroup` с именем входа администратора сервера `mylogin`.</span><span class="sxs-lookup"><span data-stu-id="1d139-125">hello following example creates a server called `mypgserver-20170401` in your resource group `myresourcegroup` with server admin login `mylogin`.</span></span> <span data-ttu-id="1d139-126">Имя учетной записи для сопоставления имени tooDNS и, таким образом необходимые toobe глобально уникальным в Azure.</span><span class="sxs-lookup"><span data-stu-id="1d139-126">Name of a server maps tooDNS name and is thus required toobe globally unique in Azure.</span></span> <span data-ttu-id="1d139-127">Замена hello `<server_admin_password>` с собственное значение.</span><span class="sxs-lookup"><span data-stu-id="1d139-127">Substitute hello `<server_admin_password>` with your own value.</span></span>
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401 --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> <span data-ttu-id="1d139-128">Имя входа администратора сервера Hello и пароль, указанные здесь являются необходимые toolog в toohello сервера и баз данных далее в этом кратком руководстве.</span><span class="sxs-lookup"><span data-stu-id="1d139-128">hello server admin login and password that you specify here are required toolog in toohello server and its databases later in this quick start.</span></span> <span data-ttu-id="1d139-129">Запомните или запишите эту информацию для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="1d139-129">Remember or record this information for later use.</span></span>

<span data-ttu-id="1d139-130">По умолчанию на сервере создается база данных **postgres**.</span><span class="sxs-lookup"><span data-stu-id="1d139-130">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="1d139-131">Hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) база данных является базой данных по умолчанию, предназначены для использования пользователями, служебные программы и сторонние приложения.</span><span class="sxs-lookup"><span data-stu-id="1d139-131">hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 


## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="1d139-132">Настройка правила брандмауэра на уровне сервера</span><span class="sxs-lookup"><span data-stu-id="1d139-132">Configure a server-level firewall rule</span></span>

<span data-ttu-id="1d139-133">Создайте правило брандмауэра уровня сервера Azure PostgreSQL с hello [az postgres правила брандмауэра для сервера — создание](/cli/azure/postgres/server/firewall-rule#create) команды.</span><span class="sxs-lookup"><span data-stu-id="1d139-133">Create an Azure PostgreSQL server-level firewall rule with hello [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> <span data-ttu-id="1d139-134">Правила брандмауэра уровня сервера позволяет внешнего приложения, такие как [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) или [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour server через брандмауэр службы Azure PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="1d139-134">A server-level firewall rule allows an external application, such as [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) or [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour server through hello Azure PostgreSQL service firewall.</span></span> 

<span data-ttu-id="1d139-135">Можно задать правило брандмауэра, которое охватывает IP диапазон toobe может tooconnect из сети.</span><span class="sxs-lookup"><span data-stu-id="1d139-135">You can set a firewall rule that covers an IP range toobe able tooconnect from your network.</span></span> <span data-ttu-id="1d139-136">Hello следующий пример использует [az postgres правила брандмауэра для сервера — создание](/cli/azure/postgres/server/firewall-rule#create) toocreate правило брандмауэра `AllowAllIps` IP-адрес диапазона адресов.</span><span class="sxs-lookup"><span data-stu-id="1d139-136">hello following example uses [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) toocreate a firewall rule `AllowAllIps` for an IP address range.</span></span> <span data-ttu-id="1d139-137">tooopen всех IP-адресов, использовать в качестве hello, начальный IP-адрес и 255.255.255.255 как hello конечный адрес 0.0.0.0.</span><span class="sxs-lookup"><span data-stu-id="1d139-137">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="1d139-138">Сервер PostgreSQL Azure обменивается данными через порт 5432.</span><span class="sxs-lookup"><span data-stu-id="1d139-138">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="1d139-139">При попытках подключения из корпоративной сети может оказаться, что исходящий трафик через порт 5432 запрещен сетевым брандмауэром.</span><span class="sxs-lookup"><span data-stu-id="1d139-139">When connecting from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="1d139-140">Есть открыть порт сервера базы данных SQL Azure на 5432 tooconnect tooyour ИТ-отдела.</span><span class="sxs-lookup"><span data-stu-id="1d139-140">Have your IT department open port 5432 tooconnect tooyour Azure SQL Database server.</span></span>
>

## <a name="get-hello-connection-information"></a><span data-ttu-id="1d139-141">Получить сведения о соединении hello</span><span class="sxs-lookup"><span data-stu-id="1d139-141">Get hello connection information</span></span>

<span data-ttu-id="1d139-142">tooconnect tooyour сервера, необходимо иметь учетные данные сведения и доступа узла tooprovide.</span><span class="sxs-lookup"><span data-stu-id="1d139-142">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

<span data-ttu-id="1d139-143">Hello получается в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="1d139-143">hello result is in JSON format.</span></span> <span data-ttu-id="1d139-144">Запишите hello **Имя_входа_администратора** и **fullyQualifiedDomainName**.</span><span class="sxs-lookup"><span data-stu-id="1d139-144">Make a note of hello **administratorLogin** and **fullyQualifiedDomainName**.</span></span>
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

## <a name="connect-tooazure-database-for-postgresql-database-using-psql"></a><span data-ttu-id="1d139-145">Подключение tooAzure базы данных для базы данных PostgreSQL, с помощью psql</span><span class="sxs-lookup"><span data-stu-id="1d139-145">Connect tooAzure Database for PostgreSQL database using psql</span></span>
<span data-ttu-id="1d139-146">Если клиентский компьютер имеет PostgreSQL установлен, можно использовать локальный экземпляр [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), или hello Azure облачной tooconnect tooan Azure PostgreSQL сервера консоли.</span><span class="sxs-lookup"><span data-stu-id="1d139-146">If your client computer has PostgreSQL installed, you can use a local instance of [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), or hello Azure Cloud Console tooconnect tooan Azure PostgreSQL server.</span></span> <span data-ttu-id="1d139-147">Теперь воспользуемся hello psql программы командной строки tooconnect toohello базы данных Azure для сервера PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="1d139-147">Let's now use hello psql command-line utility tooconnect toohello Azure Database for PostgreSQL server.</span></span>

1. <span data-ttu-id="1d139-148">Запустите следующие команды psql tooconnect tooan базы данных Azure для сервера PostgreSQL hello</span><span class="sxs-lookup"><span data-stu-id="1d139-148">Run hello following psql command tooconnect tooan Azure Database for PostgreSQL server</span></span>
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  <span data-ttu-id="1d139-149">Например, следующую команду hello подключается toohello по умолчанию база данных с именем **postgres** на сервере PostgreSQL **mypgserver 20170401.postgres.database.azure.com** с использованием учетных данных.</span><span class="sxs-lookup"><span data-stu-id="1d139-149">For example, hello following command connects toohello default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="1d139-150">Введите hello `<server_admin_password>` вы выбрали при запросе пароля.</span><span class="sxs-lookup"><span data-stu-id="1d139-150">Enter hello `<server_admin_password>` you chose when prompted for password.</span></span>
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 ---dbname=postgres
```

2.  <span data-ttu-id="1d139-151">После toohello подключенного сервера, создайте пустую базу данных в строке приветствия.</span><span class="sxs-lookup"><span data-stu-id="1d139-151">Once you are connected toohello server, create a blank database at hello prompt.</span></span>
```sql
CREATE DATABASE mypgsqldb;
```

3.  <span data-ttu-id="1d139-152">Выполните следующие tooswitch для команды подключение к базе данных только что созданный toohello hello строке hello **mypgsqldb**:</span><span class="sxs-lookup"><span data-stu-id="1d139-152">At hello prompt, execute hello following command tooswitch connection toohello newly created database **mypgsqldb**:</span></span>
```sql
\c mypgsqldb
```

## <a name="create-tables-in-hello-database"></a><span data-ttu-id="1d139-153">Создание таблиц в базе данных hello</span><span class="sxs-lookup"><span data-stu-id="1d139-153">Create tables in hello database</span></span>
<span data-ttu-id="1d139-154">Теперь, когда вы знаете, как toohello tooconnect базы данных Azure для PostgreSQL, мы можем открыть как toocomplete некоторых базовых задач.</span><span class="sxs-lookup"><span data-stu-id="1d139-154">Now that you know how tooconnect toohello Azure Database for PostgreSQL, we can go over how toocomplete some basic tasks.</span></span>

<span data-ttu-id="1d139-155">Сначала можно создать таблицу и заполнить ее некоторыми данными.</span><span class="sxs-lookup"><span data-stu-id="1d139-155">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="1d139-156">Давайте создадим таблицу, с помощью которой можно отслеживать данные инвентаризации.</span><span class="sxs-lookup"><span data-stu-id="1d139-156">Let's create a table that tracks inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

<span data-ttu-id="1d139-157">Вы можете увидеть hello вновь созданные таблицы в списке hello таблиц теперь, введя:</span><span class="sxs-lookup"><span data-stu-id="1d139-157">You can see hello newly created table in hello list of tables now by typing:</span></span>
```sql
\dt
```

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="1d139-158">Загрузка данных в таблицы hello</span><span class="sxs-lookup"><span data-stu-id="1d139-158">Load data into hello tables</span></span>
<span data-ttu-id="1d139-159">Теперь, когда таблица создана, мы можем вставить в нее данные.</span><span class="sxs-lookup"><span data-stu-id="1d139-159">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="1d139-160">Привет открыть окно командной строки запустите следующий запрос tooinsert hello некоторых строк данных</span><span class="sxs-lookup"><span data-stu-id="1d139-160">At hello open command prompt window, run hello following query tooinsert some rows of data</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="1d139-161">У вас теперь две строки образца данных в таблицу hello, созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="1d139-161">You have now two rows of sample data into hello table you created earlier.</span></span>

## <a name="query-and-update-hello-data-in-hello-tables"></a><span data-ttu-id="1d139-162">Запрашивать и обновлять данные hello в таблицах hello</span><span class="sxs-lookup"><span data-stu-id="1d139-162">Query and update hello data in hello tables</span></span>
<span data-ttu-id="1d139-163">Выполните следующую информацию tooretrieve запроса из таблицы базы данных hello hello.</span><span class="sxs-lookup"><span data-stu-id="1d139-163">Execute hello following query tooretrieve information from hello database table.</span></span> 
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="1d139-164">Можно также обновить данные hello в таблицах hello</span><span class="sxs-lookup"><span data-stu-id="1d139-164">You can also update hello data in hello tables</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="1d139-165">Строка Hello обновляется соответствующим образом при извлечении данных.</span><span class="sxs-lookup"><span data-stu-id="1d139-165">hello row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a><span data-ttu-id="1d139-166">Восстановление предыдущей точки tooa базы данных времени</span><span class="sxs-lookup"><span data-stu-id="1d139-166">Restore a database tooa previous point in time</span></span>
<span data-ttu-id="1d139-167">Представьте, что вы случайно удалили таблицу.</span><span class="sxs-lookup"><span data-stu-id="1d139-167">Imagine you have accidentally deleted a table.</span></span> <span data-ttu-id="1d139-168">Восстановить ее будет не просто.</span><span class="sxs-lookup"><span data-stu-id="1d139-168">This is something you cannot easily recover from.</span></span> <span data-ttu-id="1d139-169">База данных Azure для PostgreSQL позволяет toogo tooany назад в определенный момент (в hello последней копии too7 дней (Basic) и на 35 дней (стандартный)) и восстановления на момент tooa созданный сервер.</span><span class="sxs-lookup"><span data-stu-id="1d139-169">Azure Database for PostgreSQL allows you toogo back tooany point-in-time (in hello last up too7 days (Basic) and 35 days (Standard)) and restore this point-in-time tooa new server.</span></span> <span data-ttu-id="1d139-170">Можно использовать этот новый сервер toorecover удаленные данные.</span><span class="sxs-lookup"><span data-stu-id="1d139-170">You can use this new server toorecover your deleted data.</span></span> <span data-ttu-id="1d139-171">Здравствуйте, следующая точка tooa сервера образец hello действия восстановления перед hello таблица была добавлена.</span><span class="sxs-lookup"><span data-stu-id="1d139-171">hello following steps restore hello sample server tooa point before hello table was added.</span></span>

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

<span data-ttu-id="1d139-172">Hello `az postgres server restore` команда должна hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="1d139-172">hello `az postgres server restore` command needs hello following parameters:</span></span>
| <span data-ttu-id="1d139-173">Настройка</span><span class="sxs-lookup"><span data-stu-id="1d139-173">Setting</span></span> | <span data-ttu-id="1d139-174">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="1d139-174">Suggested value</span></span> | <span data-ttu-id="1d139-175">Описание</span><span class="sxs-lookup"><span data-stu-id="1d139-175">Description</span></span>  |
| --- | --- | --- |
| <span data-ttu-id="1d139-176">--resource-group</span><span class="sxs-lookup"><span data-stu-id="1d139-176">--resource-group</span></span> |  <span data-ttu-id="1d139-177">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1d139-177">myResourceGroup</span></span> |  <span data-ttu-id="1d139-178">Группа ресурсов, в которых hello исходный сервер существует.</span><span class="sxs-lookup"><span data-stu-id="1d139-178">The resource group in which hello source server exists.</span></span>  |
| <span data-ttu-id="1d139-179">--name</span><span class="sxs-lookup"><span data-stu-id="1d139-179">--name</span></span> | <span data-ttu-id="1d139-180">mypgserver-restored</span><span class="sxs-lookup"><span data-stu-id="1d139-180">mypgserver-restored</span></span> | <span data-ttu-id="1d139-181">Имя Hello hello новый сервер, созданный команды restore hello.</span><span class="sxs-lookup"><span data-stu-id="1d139-181">hello name of hello new server that is created by hello restore command.</span></span> |
| <span data-ttu-id="1d139-182">restore-point-in-time</span><span class="sxs-lookup"><span data-stu-id="1d139-182">restore-point-in-time</span></span> | <span data-ttu-id="1d139-183">2017-04-13T13:59:00Z</span><span class="sxs-lookup"><span data-stu-id="1d139-183">2017-04-13T13:59:00Z</span></span> | <span data-ttu-id="1d139-184">Выберите на момент toorestore для.</span><span class="sxs-lookup"><span data-stu-id="1d139-184">Select a point-in-time toorestore to.</span></span> <span data-ttu-id="1d139-185">Дата и время должны находиться в пределах срока хранения резервной копии hello исходного сервера.</span><span class="sxs-lookup"><span data-stu-id="1d139-185">This date and time must be within hello source server's backup retention period.</span></span> <span data-ttu-id="1d139-186">Используйте формат даты и времени ISO8601.</span><span class="sxs-lookup"><span data-stu-id="1d139-186">Use ISO8601 date and time format.</span></span> <span data-ttu-id="1d139-187">Например, вы можете использовать свой местный часовой пояс, например `2017-04-13T05:59:00-08:00`, или использовать формат UTC Zulu `2017-04-13T13:59:00Z`.</span><span class="sxs-lookup"><span data-stu-id="1d139-187">For example, you may use your own local timezone, such as `2017-04-13T05:59:00-08:00`, or use UTC Zulu format `2017-04-13T13:59:00Z`.</span></span> |
| <span data-ttu-id="1d139-188">--source-server</span><span class="sxs-lookup"><span data-stu-id="1d139-188">--source-server</span></span> | <span data-ttu-id="1d139-189">mypgserver-20170401</span><span class="sxs-lookup"><span data-stu-id="1d139-189">mypgserver-20170401</span></span> | <span data-ttu-id="1d139-190">Hello имя или идентификатор hello исходного сервера toorestore из.</span><span class="sxs-lookup"><span data-stu-id="1d139-190">hello name or ID of hello source server toorestore from.</span></span> |

<span data-ttu-id="1d139-191">Восстановление сервера tooa в момент создает новый сервер, копирование как hello исходного сервера hello на момент времени, указываемые.</span><span class="sxs-lookup"><span data-stu-id="1d139-191">Restoring a server tooa point-in-time creates a new server, copying as hello original server as of hello point in time you specify.</span></span> <span data-ttu-id="1d139-192">расположение Hello и ценах уровня значения для сервера восстановления hello hello аналогично hello исходного сервера.</span><span class="sxs-lookup"><span data-stu-id="1d139-192">hello location and pricing tier values for hello restored server are hello same as hello source server.</span></span>

<span data-ttu-id="1d139-193">Hello команда выполняется в синхронном режиме и вернет после восстановления сервера hello.</span><span class="sxs-lookup"><span data-stu-id="1d139-193">hello command is synchronous, and will return after hello server is restored.</span></span> <span data-ttu-id="1d139-194">После завершения выполнения hello восстановления, найдите hello новый сервер, который был создан.</span><span class="sxs-lookup"><span data-stu-id="1d139-194">Once hello restore finishes, locate hello new server that was created.</span></span> <span data-ttu-id="1d139-195">Проверьте приветствия восстановления данных должным образом.</span><span class="sxs-lookup"><span data-stu-id="1d139-195">Verify hello data was restored as expected.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1d139-196">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1d139-196">Next steps</span></span>
<span data-ttu-id="1d139-197">В этом учебнике вы узнали, каким образом toouse Azure CLI (интерфейс командной строки) и других служебных программ для:</span><span class="sxs-lookup"><span data-stu-id="1d139-197">In this tutorial, you learned how toouse Azure CLI (command-line interface) and other utilities to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="1d139-198">Создание базы данных Azure для PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="1d139-198">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="1d139-199">Настройте брандмауэр сервера hello</span><span class="sxs-lookup"><span data-stu-id="1d139-199">Configure hello server firewall</span></span>
> * <span data-ttu-id="1d139-200">Используйте [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) toocreate программа базы данных</span><span class="sxs-lookup"><span data-stu-id="1d139-200">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility toocreate a database</span></span>
> * <span data-ttu-id="1d139-201">Загрузка примера данных</span><span class="sxs-lookup"><span data-stu-id="1d139-201">Load sample data</span></span>
> * <span data-ttu-id="1d139-202">Запрос данных</span><span class="sxs-lookup"><span data-stu-id="1d139-202">Query data</span></span>
> * <span data-ttu-id="1d139-203">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="1d139-203">Update data</span></span>
> * <span data-ttu-id="1d139-204">восстановление данных.</span><span class="sxs-lookup"><span data-stu-id="1d139-204">Restore data</span></span>

<span data-ttu-id="1d139-205">Далее, узнайте, как toouse hello Azure портала toodo других подобных задач, просмотрите этот учебник: [конструкцию первой базы данных Azure с помощью PostgreSQL hello портал Azure](tutorial-design-database-using-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="1d139-205">Next, learn how toouse hello Azure portal toodo similar tasks, review this tutorial: [Design your first Azure Database for PostgreSQL using hello Azure portal](tutorial-design-database-using-azure-portal.md)</span></span>
