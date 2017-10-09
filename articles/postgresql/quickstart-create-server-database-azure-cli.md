---
title: "Создание базы данных Azure для PostgreSQL, с помощью Azure CLI hello | Документы Microsoft"
description: "Быстрый запуск toocreate руководство по и управления базой данных Azure для сервера PostgreSQL, с помощью Azure CLI (интерфейс командной строки)."
services: postgresql
author: sanagama
ms.author: sanagama
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: quickstart
ms.date: 06/13/2017
ms.openlocfilehash: 946aa3cbf5ff9f5ac4e51248412d3da5d718141e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-postgresql-using-hello-azure-cli"></a><span data-ttu-id="e5147-103">Создание базы данных Azure для PostgreSQL, с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e5147-103">Create an Azure Database for PostgreSQL using hello Azure CLI</span></span>
<span data-ttu-id="e5147-104">База данных Azure для PostgreSQL является управляемой службы, которая позволяет toorun, управлять и масштабировать высокодоступных баз данных PostgreSQL в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="e5147-104">Azure Database for PostgreSQL is a managed service that enables you toorun, manage, and scale highly available PostgreSQL databases in hello cloud.</span></span> <span data-ttu-id="e5147-105">Hello Azure CLI — используется toocreate и управления ресурсами Azure hello командной строке или в сценариях.</span><span class="sxs-lookup"><span data-stu-id="e5147-105">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="e5147-106">Краткого руководства показано, как toocreate Azure базы данных для сервера PostgreSQL в [группы ресурсов Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) с помощью Azure CLI "hello".</span><span class="sxs-lookup"><span data-stu-id="e5147-106">This quickstart shows you how toocreate an Azure Database for PostgreSQL server in an [Azure resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) using hello Azure CLI.</span></span>

<span data-ttu-id="e5147-107">Если у вас еще нет подписки Azure, создайте [бесплатную](https://azure.microsoft.com/free/) учетную запись Azure, прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="e5147-107">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e5147-108">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="e5147-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="e5147-109">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="e5147-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="e5147-110">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e5147-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="e5147-111">Если у вас несколько подписок, выберите нужную подписку hello, в котором будет выставлен счет hello ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e5147-111">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource will be billed.</span></span> <span data-ttu-id="e5147-112">Выберите конкретный идентификатор подписки вашей учетной записи, выполнив команду [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="e5147-112">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="e5147-113">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="e5147-113">Create a resource group</span></span>

<span data-ttu-id="e5147-114">Создание [группы ресурсов Azure](../azure-resource-manager/resource-group-overview.md) с помощью hello [Создание группы az](/cli/azure/group#create) команды.</span><span class="sxs-lookup"><span data-stu-id="e5147-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="e5147-115">Группа ресурсов — это логический контейнер, в котором ресурсы Azure развертываются и администрируются как группа.</span><span class="sxs-lookup"><span data-stu-id="e5147-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="e5147-116">Hello следующий пример создает группу ресурсов с именем `myresourcegroup` в hello `westus` расположение.</span><span class="sxs-lookup"><span data-stu-id="e5147-116">hello following example creates a resource group named `myresourcegroup` in hello `westus` location.</span></span>
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="e5147-117">Создание сервера базы данных Azure для PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="e5147-117">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="e5147-118">Создание [базы данных Azure для сервера PostgreSQL](overview.md) с помощью hello [az postgres server создать](/cli/azure/postgres/server#create) команды.</span><span class="sxs-lookup"><span data-stu-id="e5147-118">Create an [Azure Database for PostgreSQL server](overview.md) using hello [az postgres server create](/cli/azure/postgres/server#create) command.</span></span> <span data-ttu-id="e5147-119">Сервер содержит группу баз данных, которыми можно управлять как группой.</span><span class="sxs-lookup"><span data-stu-id="e5147-119">A server contains a group of databases managed as a group.</span></span> 

<span data-ttu-id="e5147-120">Hello следующий пример создает сервер с именем `mypgserver-20170401` в группе ресурсов `myresourcegroup` с именем входа администратора сервера `mylogin`.</span><span class="sxs-lookup"><span data-stu-id="e5147-120">hello following example creates a server named `mypgserver-20170401` in your resource group `myresourcegroup` with server admin login `mylogin`.</span></span> <span data-ttu-id="e5147-121">Имя сервера Hello сопоставляет имя tooDNS и, таким образом необходимые toobe глобально уникальным в Azure.</span><span class="sxs-lookup"><span data-stu-id="e5147-121">hello name of a server maps tooDNS name and is thus required toobe globally unique in Azure.</span></span> <span data-ttu-id="e5147-122">Замена hello `<server_admin_password>` с собственное значение.</span><span class="sxs-lookup"><span data-stu-id="e5147-122">Substitute hello `<server_admin_password>` with your own value.</span></span>
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401  --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> <span data-ttu-id="e5147-123">Имя входа администратора сервера Hello и пароль, указанные здесь являются необходимые toolog в toohello сервера и баз данных далее в этом кратком руководстве.</span><span class="sxs-lookup"><span data-stu-id="e5147-123">hello server admin login and password that you specify here are required toolog in toohello server and its databases later in this quick start.</span></span> <span data-ttu-id="e5147-124">Запомните или запишите эту информацию для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="e5147-124">Remember or record this information for later use.</span></span>

<span data-ttu-id="e5147-125">По умолчанию на сервере создается база данных **postgres**.</span><span class="sxs-lookup"><span data-stu-id="e5147-125">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="e5147-126">Hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) база данных является базой данных по умолчанию, предназначены для использования пользователями, служебные программы и сторонние приложения.</span><span class="sxs-lookup"><span data-stu-id="e5147-126">hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 


## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="e5147-127">Настройка правила брандмауэра на уровне сервера</span><span class="sxs-lookup"><span data-stu-id="e5147-127">Configure a server-level firewall rule</span></span>

<span data-ttu-id="e5147-128">Создайте правило брандмауэра уровня сервера Azure PostgreSQL с hello [az postgres правила брандмауэра для сервера — создание](/cli/azure/postgres/server/firewall-rule#create) команды.</span><span class="sxs-lookup"><span data-stu-id="e5147-128">Create an Azure PostgreSQL server-level firewall rule with hello [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> <span data-ttu-id="e5147-129">Правила брандмауэра уровня сервера позволяет внешнего приложения, такие как [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) или [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour server через брандмауэр службы Azure PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="e5147-129">A server-level firewall rule allows an external application, such as [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) or [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour server through hello Azure PostgreSQL service firewall.</span></span> 

<span data-ttu-id="e5147-130">Можно задать правило брандмауэра, которое охватывает IP диапазон toobe может tooconnect из сети.</span><span class="sxs-lookup"><span data-stu-id="e5147-130">You can set a firewall rule that covers an IP range toobe able tooconnect from your network.</span></span> <span data-ttu-id="e5147-131">Hello следующий пример использует [az postgres правила брандмауэра для сервера — создание](/cli/azure/postgres/server/firewall-rule#create) toocreate правило брандмауэра `AllowAllIps` IP-адрес диапазона адресов.</span><span class="sxs-lookup"><span data-stu-id="e5147-131">hello following example uses [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) toocreate a firewall rule `AllowAllIps` for an IP address range.</span></span> <span data-ttu-id="e5147-132">tooopen всех IP-адресов, использовать в качестве hello, начальный IP-адрес и 255.255.255.255 как hello конечный адрес 0.0.0.0.</span><span class="sxs-lookup"><span data-stu-id="e5147-132">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="e5147-133">Сервер PostgreSQL Azure обменивается данными через порт 5432.</span><span class="sxs-lookup"><span data-stu-id="e5147-133">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="e5147-134">При попытках подключения из корпоративной сети может оказаться, что исходящий трафик через порт 5432 запрещен сетевым брандмауэром.</span><span class="sxs-lookup"><span data-stu-id="e5147-134">When connecting from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="e5147-135">Есть открыть порт сервера базы данных SQL Azure на 5432 tooconnect tooyour ИТ-отдела.</span><span class="sxs-lookup"><span data-stu-id="e5147-135">Have your IT department open port 5432 tooconnect tooyour Azure SQL Database server.</span></span>

## <a name="get-hello-connection-information"></a><span data-ttu-id="e5147-136">Получить сведения о соединении hello</span><span class="sxs-lookup"><span data-stu-id="e5147-136">Get hello connection information</span></span>

<span data-ttu-id="e5147-137">tooconnect tooyour сервера, необходимо иметь учетные данные сведения и доступа узла tooprovide.</span><span class="sxs-lookup"><span data-stu-id="e5147-137">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

<span data-ttu-id="e5147-138">Hello получается в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="e5147-138">hello result is in JSON format.</span></span> <span data-ttu-id="e5147-139">Запишите hello **Имя_входа_администратора** и **fullyQualifiedDomainName**.</span><span class="sxs-lookup"><span data-stu-id="e5147-139">Make a note of hello **administratorLogin** and **fullyQualifiedDomainName**.</span></span>
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

## <a name="connect-toopostgresql-database-using-psql"></a><span data-ttu-id="e5147-140">Подключитесь с помощью psql базу данных tooPostgreSQL</span><span class="sxs-lookup"><span data-stu-id="e5147-140">Connect tooPostgreSQL database using psql</span></span>

<span data-ttu-id="e5147-141">Если клиентский компьютер имеет PostgreSQL установлен, можно использовать локальный экземпляр [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooconnect tooan Azure PostgreSQL сервера.</span><span class="sxs-lookup"><span data-stu-id="e5147-141">If your client computer has PostgreSQL installed, you can use a local instance of [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooconnect tooan Azure PostgreSQL server.</span></span> <span data-ttu-id="e5147-142">Теперь воспользуемся hello psql программы командной строки tooconnect toohello Azure PostgreSQL сервера.</span><span class="sxs-lookup"><span data-stu-id="e5147-142">Let's now use hello psql command-line utility tooconnect toohello Azure PostgreSQL server.</span></span>

1. <span data-ttu-id="e5147-143">Запустите следующие команды psql tooconnect tooan базы данных Azure для сервера PostgreSQL hello</span><span class="sxs-lookup"><span data-stu-id="e5147-143">Run hello following psql command tooconnect tooan Azure Database for PostgreSQL server</span></span>
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  <span data-ttu-id="e5147-144">Например, следующую команду hello подключается toohello по умолчанию база данных с именем **postgres** на сервере PostgreSQL **mypgserver 20170401.postgres.database.azure.com** с использованием учетных данных.</span><span class="sxs-lookup"><span data-stu-id="e5147-144">For example, hello following command connects toohello default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="e5147-145">Введите hello `<server_admin_password>` вы выбрали при запросе пароля.</span><span class="sxs-lookup"><span data-stu-id="e5147-145">Enter hello `<server_admin_password>` you chose when prompted for password.</span></span>
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
```

2.  <span data-ttu-id="e5147-146">После toohello подключенного сервера, создайте пустую базу данных в строке приветствия.</span><span class="sxs-lookup"><span data-stu-id="e5147-146">Once you are connected toohello server, create a blank database at hello prompt.</span></span>
```sql
CREATE DATABASE mypgsqldb;
```

3.  <span data-ttu-id="e5147-147">Выполните следующие tooswitch для команды подключение к базе данных только что созданный toohello hello строке hello **mypgsqldb**:</span><span class="sxs-lookup"><span data-stu-id="e5147-147">At hello prompt, execute hello following command tooswitch connection toohello newly created database **mypgsqldb**:</span></span>
```sql
\c mypgsqldb
```

## <a name="connect-toopostgresql-database-using-pgadmin"></a><span data-ttu-id="e5147-148">Подключитесь с помощью pgAdmin базу данных tooPostgreSQL</span><span class="sxs-lookup"><span data-stu-id="e5147-148">Connect tooPostgreSQL database using pgAdmin</span></span>

<span data-ttu-id="e5147-149">с помощью средства hello графического интерфейса пользователя PostgreSQL сервера с tooAzure tooconnect _pgAdmin_</span><span class="sxs-lookup"><span data-stu-id="e5147-149">tooconnect tooAzure PostgreSQL server using hello GUI tool _pgAdmin_</span></span>
1.  <span data-ttu-id="e5147-150">Запустите hello _pgAdmin_ приложения на клиентском компьютере.</span><span class="sxs-lookup"><span data-stu-id="e5147-150">Launch hello _pgAdmin_ application on your client computer.</span></span> <span data-ttu-id="e5147-151">Вы можете установить _pgAdmin_ с помощью http://www.pgadmin.org/.</span><span class="sxs-lookup"><span data-stu-id="e5147-151">You can install _pgAdmin_ from http://www.pgadmin.org/.</span></span>
2.  <span data-ttu-id="e5147-152">Выберите **добавить новый сервер** из hello **быстрые ссылки** меню.</span><span class="sxs-lookup"><span data-stu-id="e5147-152">Choose **Add New Server** from hello **Quick Links** menu.</span></span>
3.  <span data-ttu-id="e5147-153">В hello **создание - сервера** диалоговое окно **Общие** введите уникальное понятное имя для сервера hello.</span><span class="sxs-lookup"><span data-stu-id="e5147-153">In hello **Create - Server** dialog box **General** tab, enter a unique friendly Name for hello server.</span></span> <span data-ttu-id="e5147-154">Например, **Azure PostgreSQL Server**.</span><span class="sxs-lookup"><span data-stu-id="e5147-154">Say **Azure PostgreSQL Server**.</span></span>
 <span data-ttu-id="e5147-155">![Средство pgAdmin. Создание сервера](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)</span><span class="sxs-lookup"><span data-stu-id="e5147-155">![pgAdmin tool - create - server](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)</span></span>
4.  <span data-ttu-id="e5147-156">В hello **создание - сервера** диалоговом **подключения** вкладки:</span><span class="sxs-lookup"><span data-stu-id="e5147-156">In hello **Create - Server** dialog box, **Connection** tab:</span></span>
    - <span data-ttu-id="e5147-157">Введите hello полное имя сервера (например, **mypgserver 20170401.postgres.database.azure.com**) в hello **имя узла / адрес** поле.</span><span class="sxs-lookup"><span data-stu-id="e5147-157">Enter hello fully qualified server name (for example, **mypgserver-20170401.postgres.database.azure.com**) in hello **Host Name/ Address** box.</span></span> 
    - <span data-ttu-id="e5147-158">Введите порт 5432 в hello **порт** поле.</span><span class="sxs-lookup"><span data-stu-id="e5147-158">Enter port 5432 into hello **Port** box.</span></span> 
    - <span data-ttu-id="e5147-159">Введите hello **имя входа администратора сервера (user@mypgserver)** полученные ранее в данном краткое руководство и пароль, введенный при создании сервера hello в hello **Username** и **пароля** соответственно.</span><span class="sxs-lookup"><span data-stu-id="e5147-159">Enter hello **Server admin login (user@mypgserver)** obtained earlier in this quickstart and password you entered when you created hello server into hello **Username** and **Password** boxes, respectively.</span></span>
    - <span data-ttu-id="e5147-160">Выберите для **режима SSL** значение **Запросить**.</span><span class="sxs-lookup"><span data-stu-id="e5147-160">Select **SSL Mode** as **Require**.</span></span> <span data-ttu-id="e5147-161">По умолчанию все серверы PostgreSQL Azure создаются с включенным применением SSL.</span><span class="sxs-lookup"><span data-stu-id="e5147-161">By default, all Azure PostgreSQL servers are created with SSL enforcing turned ON.</span></span> <span data-ttu-id="e5147-162">tooturn OFF применяют SSL, см. Подробности в [применения SSL](./concepts-ssl-connection-security.md).</span><span class="sxs-lookup"><span data-stu-id="e5147-162">tooturn OFF SSL enforcing, see details in [Enforcing SSL](./concepts-ssl-connection-security.md).</span></span>

    ![pgAdmin. Создание сервера](./media/quickstart-create-server-database-azure-cli/2-pgadmin-create-server.png)
5.  <span data-ttu-id="e5147-164">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e5147-164">Click **Save**.</span></span>
6.  <span data-ttu-id="e5147-165">В левой области обозревателя hello разверните hello **групп серверов**.</span><span class="sxs-lookup"><span data-stu-id="e5147-165">In hello Browser left pane, expand hello **Server Groups**.</span></span> <span data-ttu-id="e5147-166">Выберите свой сервер **Azure PostgreSQL Server**.</span><span class="sxs-lookup"><span data-stu-id="e5147-166">Choose your server **Azure PostgreSQL Server**.</span></span>
7.  <span data-ttu-id="e5147-167">Выберите hello **сервера** подключены, а затем выберите **баз данных** под ним.</span><span class="sxs-lookup"><span data-stu-id="e5147-167">Choose hello **Server** you connected to, and then choose **Databases** under it.</span></span> 
8.  <span data-ttu-id="e5147-168">Щелкните правой кнопкой мыши **баз данных** tooCreate базы данных.</span><span class="sxs-lookup"><span data-stu-id="e5147-168">Right-click on **Databases** tooCreate a Database.</span></span>
9.  <span data-ttu-id="e5147-169">Выберите имя базы данных **mypgsqldb** и hello владельца для него, что имя входа администратора сервера **пользователь**.</span><span class="sxs-lookup"><span data-stu-id="e5147-169">Choose a database name **mypgsqldb** and hello owner for it as server admin login **mylogin**.</span></span>
10. <span data-ttu-id="e5147-170">Нажмите кнопку **Сохранить** toocreate пустую базу данных.</span><span class="sxs-lookup"><span data-stu-id="e5147-170">Click **Save** toocreate a blank database.</span></span>
11. <span data-ttu-id="e5147-171">В hello **браузера**, разверните hello **серверы** группы.</span><span class="sxs-lookup"><span data-stu-id="e5147-171">In hello **Browser**, expand hello **Servers** group.</span></span> <span data-ttu-id="e5147-172">Разверните сервер hello, вы создали и см. база данных hello **mypgsqldb** под ним.</span><span class="sxs-lookup"><span data-stu-id="e5147-172">Expand hello server you created, and see hello database **mypgsqldb** under it.</span></span>
 <span data-ttu-id="e5147-173">![pgAdmin. Создание базы данных](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)</span><span class="sxs-lookup"><span data-stu-id="e5147-173">![pgAdmin - Create - Database](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)</span></span>


## <a name="clean-up-resources"></a><span data-ttu-id="e5147-174">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="e5147-174">Clean up resources</span></span>

<span data-ttu-id="e5147-175">Очистить все ресурсы, созданные в кратком руководстве hello, удалив hello [группы ресурсов Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e5147-175">Clean up all resources you created in hello quickstart by deleting hello [Azure resource group](../azure-resource-manager/resource-group-overview.md).</span></span>

> [!TIP]
> <span data-ttu-id="e5147-176">Другие краткие руководства в этой коллекции созданы на основе этого документа.</span><span class="sxs-lookup"><span data-stu-id="e5147-176">Other quickstarts in this collection build upon this quick start.</span></span> <span data-ttu-id="e5147-177">Если вы планируете toowork с последующей toocontinue краткие руководства, выполните очистку не hello ресурсы, созданные в этом кратком руководстве.</span><span class="sxs-lookup"><span data-stu-id="e5147-177">If you plan toocontinue on toowork with subsequent quickstarts, do not clean up hello resources created in this quickstart.</span></span> <span data-ttu-id="e5147-178">Если вы не планируете toocontinue, используйте следующие шаги toodelete hello все ресурсы, созданные в этом кратком руководстве в hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e5147-178">If you do not plan toocontinue, use hello following steps toodelete all resources created by this quickstart in hello Azure CLI.</span></span>

```azurecli-interactive
az group delete --name myresourcegroup
```

<span data-ttu-id="e5147-179">Если вы просто хотите toodelete hello один только что созданный сервер, можно запустить [удаления сервера postgres az](/cli/azure/postgres/server#delete) команды.</span><span class="sxs-lookup"><span data-stu-id="e5147-179">If you just would like toodelete hello one newly created server, you can run [az postgres server delete](/cli/azure/postgres/server#delete) command.</span></span>
```azurecli-interactive
az postgres server delete --resource-group myresourcegroup --name mypgserver-20170401
```

## <a name="next-steps"></a><span data-ttu-id="e5147-180">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e5147-180">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="e5147-181">Перенос базы данных с помощью экспорта и импорта</span><span class="sxs-lookup"><span data-stu-id="e5147-181">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
