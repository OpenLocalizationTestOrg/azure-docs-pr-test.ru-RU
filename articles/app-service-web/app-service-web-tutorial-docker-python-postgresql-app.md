---
title: "Создание в Azure веб-приложения Docker Python с подключением к базе данных PostgreSQL | Документация Майкрософт"
description: "Узнайте, как создать приложение Docker Python в Azure с подключением к базе данных PostgreSQL."
services: app-service\web
documentationcenter: python
author: berndverst
manager: erikre
editor: 
ms.assetid: 2bada123-ef18-44e5-be71-e16323b20466
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: tutorial
ms.date: 05/03/2017
ms.author: beverst
ms.custom: mvc
ms.openlocfilehash: e70f85a1eb4a6e1a81e0ca4fae228ca97deca6fe
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-docker-python-and-postgresql-web-app-in-azure"></a><span data-ttu-id="f109e-103">Создание в Azure веб-приложения Docker Python с подключением к базе данных PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="f109e-103">Build a Docker Python and PostgreSQL web app in Azure</span></span>

<span data-ttu-id="f109e-104">Веб-приложения Azure — это служба веб-размещения с самостоятельной установкой исправлений и высоким уровнем масштабируемости.</span><span class="sxs-lookup"><span data-stu-id="f109e-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="f109e-105">В этом руководстве показано, как создать базовое веб-приложение Docker Python в Azure.</span><span class="sxs-lookup"><span data-stu-id="f109e-105">This tutorial shows how to create a basic Docker Python web app in Azure.</span></span> <span data-ttu-id="f109e-106">Вы также подключите это приложение к базе данных PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="f109e-106">You'll connect this app to a PostgreSQL database.</span></span> <span data-ttu-id="f109e-107">После выполнения всех действий у вас будет приложение Python Flask, работающее в контейнере Docker в [веб-приложениях службы приложений Azure](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f109e-107">When you're done, you'll have a Python Flask application running within a Docker container on [Azure App Service Web Apps](app-service-web-overview.md).</span></span>

![Приложение Docker Python Flask в службе приложений Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

<span data-ttu-id="f109e-109">Выполните приведенные ниже действия в macOS.</span><span class="sxs-lookup"><span data-stu-id="f109e-109">You can follow the steps below on macOS.</span></span> <span data-ttu-id="f109e-110">Инструкции для Linux и Windows в большей степени совпадают, но различия не описаны в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="f109e-110">Linux and Windows instructions are the same in most cases, but the differences are not detailed in this tutorial.</span></span>
 
## <a name="prerequisites"></a><span data-ttu-id="f109e-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f109e-111">Prerequisites</span></span>

<span data-ttu-id="f109e-112">Для работы с этим руководством:</span><span class="sxs-lookup"><span data-stu-id="f109e-112">To complete this tutorial:</span></span>

1. <span data-ttu-id="f109e-113">[установите Git](https://git-scm.com/);</span><span class="sxs-lookup"><span data-stu-id="f109e-113">[Install Git](https://git-scm.com/)</span></span>
1. <span data-ttu-id="f109e-114">[установите Python](https://www.python.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="f109e-114">[Install Python](https://www.python.org/downloads/)</span></span>
1. <span data-ttu-id="f109e-115">[установите и запустите PostgreSQL](https://www.postgresql.org/download/);</span><span class="sxs-lookup"><span data-stu-id="f109e-115">[Install and run PostgreSQL](https://www.postgresql.org/download/)</span></span>
1. <span data-ttu-id="f109e-116">[установите Docker Community Edition](https://www.docker.com/community-edition).</span><span class="sxs-lookup"><span data-stu-id="f109e-116">[Install Docker Community Edition](https://www.docker.com/community-edition)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f109e-117">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="f109e-117">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f109e-118">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="f109e-118">Run `az --version` to find the version.</span></span> <span data-ttu-id="f109e-119">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f109e-119">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-postgresql-installation-and-create-a-database"></a><span data-ttu-id="f109e-120">Проверка локальной установки PostgreSQL и создание базы данных</span><span class="sxs-lookup"><span data-stu-id="f109e-120">Test local PostgreSQL installation and create a database</span></span>

<span data-ttu-id="f109e-121">Откройте окно терминала и выполните команду `psql postgres` для подключения к локальному серверу PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="f109e-121">Open the terminal window and run `psql postgres` to connect to your local PostgreSQL server.</span></span>

```bash
psql postgres
```

<span data-ttu-id="f109e-122">Если подключение успешно установлено, это означает, что база данных PostgreSQL запущена.</span><span class="sxs-lookup"><span data-stu-id="f109e-122">If your connection is successful, your PostgreSQL database is running.</span></span> <span data-ttu-id="f109e-123">В противном случае запустите локальную базу данных PostgreSQL, выполнив инструкции по [скачиванию ядра PostgreSQL](https://www.postgresql.org/download/).</span><span class="sxs-lookup"><span data-stu-id="f109e-123">If not, make sure that your local PostgresQL database is started by following the steps at [Downloads - PostgreSQL Core Distribution](https://www.postgresql.org/download/).</span></span>

<span data-ttu-id="f109e-124">Создайте базу данных *eventregistration* и настройте отдельного пользователя базы данных пользователя *manager* с паролем *supersecretpass*.</span><span class="sxs-lookup"><span data-stu-id="f109e-124">Create a database called *eventregistration* and set up a separate database user named *manager* with password *supersecretpass*.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration TO manager;
```
<span data-ttu-id="f109e-125">Введите *\q*, чтобы выйти из клиента PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="f109e-125">Type *\q* to exit the PostgreSQL client.</span></span> 

<a name="step2"></a>

## <a name="create-local-python-flask-application"></a><span data-ttu-id="f109e-126">Создание локального приложения Python Flask</span><span class="sxs-lookup"><span data-stu-id="f109e-126">Create local Python Flask application</span></span>

<span data-ttu-id="f109e-127">На этом шаге вы настроите локальный проект Python Flask.</span><span class="sxs-lookup"><span data-stu-id="f109e-127">In this step, you set up the local Python Flask project.</span></span>

### <a name="clone-the-sample-application"></a><span data-ttu-id="f109e-128">Клонирование примера приложения</span><span class="sxs-lookup"><span data-stu-id="f109e-128">Clone the sample application</span></span>

<span data-ttu-id="f109e-129">Откройте окно терминала и c помощью команды `CD` перейдите в рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="f109e-129">Open the terminal window, and `CD` to a working directory.</span></span>  

<span data-ttu-id="f109e-130">Выполните следующие команды, чтобы клонировать пример репозитория и перейти к выпуску *0.1-initialapp*.</span><span class="sxs-lookup"><span data-stu-id="f109e-130">Run the following commands to clone the sample repository and go to the *0.1-initialapp* release.</span></span>

```bash
git clone https://github.com/Azure-Samples/docker-flask-postgres.git
cd docker-flask-postgres
git checkout tags/0.1-initialapp
```

<span data-ttu-id="f109e-131">Этот пример репозитория содержит приложение [Flask](http://flask.pocoo.org/).</span><span class="sxs-lookup"><span data-stu-id="f109e-131">This sample repository contains a [Flask](http://flask.pocoo.org/) application.</span></span> 

### <a name="run-the-application"></a><span data-ttu-id="f109e-132">Выполнение приложения</span><span class="sxs-lookup"><span data-stu-id="f109e-132">Run the application</span></span>

> [!NOTE] 
> <span data-ttu-id="f109e-133">На последующем шаге вы упростите этот процесс, создав контейнер Docker для рабочей базы данных.</span><span class="sxs-lookup"><span data-stu-id="f109e-133">In a later step you simplify this process by building a Docker container to use with the production database.</span></span>

<span data-ttu-id="f109e-134">Установите необходимые пакеты и запустите приложение.</span><span class="sxs-lookup"><span data-stu-id="f109e-134">Install the required packages and start the application.</span></span>

```bash
pip install virtualenv
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="f109e-135">После полной загрузки приложения вы увидите следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="f109e-135">When the app is fully loaded, you see something similar to the following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

<span data-ttu-id="f109e-136">Перейдите по адресу http://127.0.0.1:5000 в браузере.</span><span class="sxs-lookup"><span data-stu-id="f109e-136">Navigate to http://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="f109e-137">Щелкните **Зарегистрировать**</span><span class="sxs-lookup"><span data-stu-id="f109e-137">Click **Register!**</span></span> <span data-ttu-id="f109e-138">и создайте тестового пользователя.</span><span class="sxs-lookup"><span data-stu-id="f109e-138">and create a test user.</span></span>

![Приложение Python Flask, выполняемое в локальной среде](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

<span data-ttu-id="f109e-140">Пример приложения Flask хранит данные пользователей в базе данных.</span><span class="sxs-lookup"><span data-stu-id="f109e-140">The Flask sample application stores user data in the database.</span></span> <span data-ttu-id="f109e-141">Если вам удалось зарегистрировать пользователя, значит, ваше приложение записывает данные в локальную базу данных PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="f109e-141">If you are successful at registering a user, your app is writing data to the local PostgreSQL database.</span></span>

<span data-ttu-id="f109e-142">Чтобы остановить Flask в любое время, введите Ctrl+C в окне терминала.</span><span class="sxs-lookup"><span data-stu-id="f109e-142">To stop the Flask server at anytime, type Ctrl+C in the terminal.</span></span> 

## <a name="create-a-production-postgresql-database"></a><span data-ttu-id="f109e-143">Создание рабочей базы данных PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="f109e-143">Create a production PostgreSQL database</span></span>

<span data-ttu-id="f109e-144">На этом шаге вы создадите базу данных PostgreSQL в Azure.</span><span class="sxs-lookup"><span data-stu-id="f109e-144">In this step, you create a PostgreSQL database in Azure.</span></span> <span data-ttu-id="f109e-145">При развертывании приложения в Azure используется эта облачная база данных.</span><span class="sxs-lookup"><span data-stu-id="f109e-145">When your app is deployed to Azure, it will use this cloud database.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="f109e-146">Вход в Azure</span><span class="sxs-lookup"><span data-stu-id="f109e-146">Log in to Azure</span></span>

<span data-ttu-id="f109e-147">Теперь создадим ресурсы, необходимые для размещения приложения Python в службе приложений Azure, с помощью Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="f109e-147">You are now going to use the Azure CLI 2.0 to create the resources needed to host your Python application in Azure App Service.</span></span>  <span data-ttu-id="f109e-148">Войдите в подписку Azure с помощью команды [az login](/cli/azure/#login) и следуйте инструкциям на экране.</span><span class="sxs-lookup"><span data-stu-id="f109e-148">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span> 

```azurecli
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="f109e-149">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="f109e-149">Create a resource group</span></span>

<span data-ttu-id="f109e-150">Создайте [группу ресурсов](../azure-resource-manager/resource-group-overview.md) с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="f109e-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with the [az group create](/cli/azure/group#create).</span></span> 

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="f109e-151">В следующем примере создается группа ресурсов в регионе "Западная часть США".</span><span class="sxs-lookup"><span data-stu-id="f109e-151">The following example creates a resource group in the West US region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West US"
```

<span data-ttu-id="f109e-152">Чтобы вывести список доступных расположений, используйте команду Azure CLI [az appservice list-locations](/cli/azure/appservice#list-locations).</span><span class="sxs-lookup"><span data-stu-id="f109e-152">Use the [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command to list available locations.</span></span>

### <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="f109e-153">Создание сервера базы данных Azure для PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="f109e-153">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="f109e-154">Создайте сервер PostgreSQL с помощью команды [az postgres server create](/cli/azure/documentdb#create).</span><span class="sxs-lookup"><span data-stu-id="f109e-154">Create a PostgreSQL server with the [az postgres server create](/cli/azure/documentdb#create) command.</span></span>

<span data-ttu-id="f109e-155">В следующей команде замените заполнитель *\<postgresql_name>* уникальным именем сервера, а заполнитель *\<admin_username>* — именем пользователя.</span><span class="sxs-lookup"><span data-stu-id="f109e-155">In the following command, substitute a unique server name for the *\<postgresql_name>* placeholder and a user name for the *\<admin_username>* placeholder.</span></span> <span data-ttu-id="f109e-156">Это имя используется как часть конечной точки PostgreSQL (`https://<postgresql_name>.postgres.database.azure.com`), поэтому оно должно быть уникальным на всех серверах в Azure.</span><span class="sxs-lookup"><span data-stu-id="f109e-156">The server name is used as part of your PostgreSQL endpoint (`https://<postgresql_name>.postgres.database.azure.com`), so the name needs to be unique across all servers in Azure.</span></span> <span data-ttu-id="f109e-157">Имя пользователя необходимо для создания учетной записи администратора исходной базы данных.</span><span class="sxs-lookup"><span data-stu-id="f109e-157">The user name is for the initial database admin user account.</span></span> <span data-ttu-id="f109e-158">Вам будет предложено выбрать пароль для этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="f109e-158">You are prompted to pick a password for this user.</span></span>

```azurecli-interactive
az postgres server create --resource-group myResourceGroup --name <postgresql_name> --admin-user <admin_username>
```

<span data-ttu-id="f109e-159">После создания сервера базы данных Azure для PostgreSQL в Azure CLI отображаются следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="f109e-159">When the Azure Database for PostgreSQL server is created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "administratorLogin": "<my_admin_username>",
  "fullyQualifiedDomainName": "<postgresql_name>.postgres.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforPostgreSQL/servers/<postgresql_name>",
  "location": "westus",
  "name": "<postgresql_name>",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capacity": 100,
    "family": null,
    "name": "PGSQLS3M100",
    "size": null,
    "tier": "Basic"
  },
  "sslEnforcement": null,
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

### <a name="create-a-firewall-rule-for-the-azure-database-for-postgresql-server"></a><span data-ttu-id="f109e-160">Создание правила брандмауэра для сервера базы данных Azure для PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="f109e-160">Create a firewall rule for the Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="f109e-161">Чтобы разрешить доступ к базе данных со всех IP-адресов, выполните следующую команду Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f109e-161">Run the following Azure CLI command to allow access to the database from all IP addresses.</span></span>

```azurecli-interactive
az postgres server firewall-rule create --resource-group myResourceGroup --server-name <postgresql_name> --start-ip-address=0.0.0.0 --end-ip-address=255.255.255.255 --name AllowAllIPs
```

<span data-ttu-id="f109e-162">Azure CLI подтверждает создание правила брандмауэра, выводя результат, аналогичный следующему:</span><span class="sxs-lookup"><span data-stu-id="f109e-162">The Azure CLI confirms the firewall rule creation with output similar to the following example:</span></span>

```json
{
  "endIpAddress": "255.255.255.255",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforPostgreSQL/servers/<postgresql_name>/firewallRules/AllowAllIPs",
  "name": "AllowAllIPs",
  "resourceGroup": "myResourceGroup",
  "startIpAddress": "0.0.0.0",
  "type": "Microsoft.DBforPostgreSQL/servers/firewallRules"
}
```

## <a name="connect-your-python-flask-application-to-the-database"></a><span data-ttu-id="f109e-163">Подключение приложения Python Flask к базе данных</span><span class="sxs-lookup"><span data-stu-id="f109e-163">Connect your Python Flask application to the database</span></span>

<span data-ttu-id="f109e-164">На этом шаге вы подключаете пример приложения Python Flask к серверу базы данных Azure для PostgreSQL, который вы создали.</span><span class="sxs-lookup"><span data-stu-id="f109e-164">In this step, you connect your Python Flask sample application to the Azure Database for PostgreSQL server you created.</span></span>

### <a name="create-an-empty-database-and-set-up-a-new-database-application-user"></a><span data-ttu-id="f109e-165">Создание пустой базы данных и настройка нового пользователя приложения базы данных</span><span class="sxs-lookup"><span data-stu-id="f109e-165">Create an empty database and set up a new database application user</span></span>

<span data-ttu-id="f109e-166">Создайте пользователя базы данных с доступом только к отдельной базе данных.</span><span class="sxs-lookup"><span data-stu-id="f109e-166">Create a database user with access to a single database only.</span></span> <span data-ttu-id="f109e-167">Эти учетные данные позволяют избежать предоставления приложению полного доступа к серверу.</span><span class="sxs-lookup"><span data-stu-id="f109e-167">You'll use these credentials to avoid giving the application full access to the server.</span></span>

<span data-ttu-id="f109e-168">Подключитесь к базе данных (вам будет предложено ввести пароль администратора).</span><span class="sxs-lookup"><span data-stu-id="f109e-168">Connect to the database (you're prompted for your admin password).</span></span>

```bash
psql -h <postgresql_name>.postgres.database.azure.com -U <my_admin_username>@<postgresql_name> postgres
```

<span data-ttu-id="f109e-169">Создайте базу данных и пользователя с помощью интерфейса командной строки PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="f109e-169">Create the database and user from the PostgreSQL CLI.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration TO manager;
```

<span data-ttu-id="f109e-170">Введите *\q*, чтобы выйти из клиента PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="f109e-170">Type *\q* to exit the PostgreSQL client.</span></span>

### <a name="test-the-application-locally-against-the-azure-postgresql-database"></a><span data-ttu-id="f109e-171">Тестирование приложения локально с базой данных Azure для PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="f109e-171">Test the application locally against the Azure PostgreSQL database</span></span> 

<span data-ttu-id="f109e-172">Теперь вернемся в папку *app* клонированного репозитория GitHub. Вы можете запустить приложение Python Flask, обновив переменные среды базы данных.</span><span class="sxs-lookup"><span data-stu-id="f109e-172">Going back now to the *app* folder of the cloned Github repository, you can run the Python Flask application by updating the database environment variables.</span></span>

```bash
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="f109e-173">После полной загрузки приложения вы увидите следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="f109e-173">When the app is fully loaded, you see something similar to the following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

<span data-ttu-id="f109e-174">Перейдите по адресу http://127.0.0.1:5000 в браузере.</span><span class="sxs-lookup"><span data-stu-id="f109e-174">Navigate to http://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="f109e-175">Щелкните **Зарегистрировать**</span><span class="sxs-lookup"><span data-stu-id="f109e-175">Click **Register!**</span></span> <span data-ttu-id="f109e-176">и создайте тестовую регистрацию.</span><span class="sxs-lookup"><span data-stu-id="f109e-176">and create a test registration.</span></span> <span data-ttu-id="f109e-177">Теперь приложение записывает данные в базу данных Azure.</span><span class="sxs-lookup"><span data-stu-id="f109e-177">You are now writing data to the database in Azure.</span></span>

![Приложение Python Flask, выполняемое в локальной среде](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

### <a name="running-the-application-from-a-docker-container"></a><span data-ttu-id="f109e-179">Запуск приложения из контейнера Docker</span><span class="sxs-lookup"><span data-stu-id="f109e-179">Running the application from a Docker Container</span></span>

<span data-ttu-id="f109e-180">Создайте образ контейнера Docker.</span><span class="sxs-lookup"><span data-stu-id="f109e-180">Build the Docker container image.</span></span>

```bash
cd ..
docker build -t flask-postgresql-sample .
```

<span data-ttu-id="f109e-181">Docker отображает подтверждение успешного создания контейнера.</span><span class="sxs-lookup"><span data-stu-id="f109e-181">Docker displays a confirmation that it successfully created the container.</span></span>

```bash
Successfully built 7548f983a36b
```

<span data-ttu-id="f109e-182">Добавьте переменные среды базы данных в файл переменных среды *db.env*.</span><span class="sxs-lookup"><span data-stu-id="f109e-182">Add database environment variables to an environment variable file *db.env*.</span></span> <span data-ttu-id="f109e-183">Приложение подключиться к рабочей базе данных PostgreSQL в Azure.</span><span class="sxs-lookup"><span data-stu-id="f109e-183">The app will connect to the PostgreSQL production database in Azure.</span></span>

```text
DBHOST="<postgresql_name>.postgres.database.azure.com"
DBUSER="manager@<postgresql_name>"
DBNAME="eventregistration"
DBPASS="supersecretpass"
```

<span data-ttu-id="f109e-184">Запустите приложение из контейнера Docker.</span><span class="sxs-lookup"><span data-stu-id="f109e-184">Run the app from within the Docker container.</span></span> <span data-ttu-id="f109e-185">Следующая команда указывает файл переменных среды и сопоставляет порт Flask по умолчанию 5000 с локальным портом 5000.</span><span class="sxs-lookup"><span data-stu-id="f109e-185">The following command specifies the environment variable file and maps the default Flask port 5000 to local port 5000.</span></span>

```bash
docker run -it --env-file db.env -p 5000:5000 flask-postgresql-sample
```

<span data-ttu-id="f109e-186">Выходные данные аналогичны показанным ранее.</span><span class="sxs-lookup"><span data-stu-id="f109e-186">The output is similar to what you saw earlier.</span></span> <span data-ttu-id="f109e-187">Тем не менее перенос исходной базы данных больше не требуется. Поэтому он пропускается.</span><span class="sxs-lookup"><span data-stu-id="f109e-187">However, the initial database migration no longer needs to be performed and therefore is skipped.</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
 * Serving Flask app "app"
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```

<span data-ttu-id="f109e-188">База данных уже содержит регистрацию, созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="f109e-188">The database already contains the registration you created previously.</span></span>

![Приложение Python Flask из контейнера Docker, выполняемое в локальной среде](./media/app-service-web-tutorial-docker-python-postgresql-app/local-docker.png)

## <a name="upload-the-docker-container-to-a-container-registry"></a><span data-ttu-id="f109e-190">Передача контейнера Docker в реестр контейнеров</span><span class="sxs-lookup"><span data-stu-id="f109e-190">Upload the Docker container to a container registry</span></span>

<span data-ttu-id="f109e-191">На этом шаге вы передадите контейнер Docker в реестр контейнеров.</span><span class="sxs-lookup"><span data-stu-id="f109e-191">In this step, you upload the Docker container to a container registry.</span></span> <span data-ttu-id="f109e-192">Вы будете использовать реестр контейнеров Azure, однако можно также использовать другие популярные реестры контейнеров, например Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="f109e-192">You'll use Azure Container Registry, but you could also use other popular ones such as Docker Hub.</span></span>

### <a name="create-an-azure-container-registry"></a><span data-ttu-id="f109e-193">Создание реестра контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="f109e-193">Create an Azure Container Registry</span></span>

<span data-ttu-id="f109e-194">В приведенной команде замените заполнитель *\<registry_name>* уникальным именем реестра контейнеров Azure по своему усмотрению, чтобы создать реестр контейнеров.</span><span class="sxs-lookup"><span data-stu-id="f109e-194">In the following command to create a container registry replace *\<registry_name>* with a unique Azure container registry name of your choice.</span></span>

```azurecli-interactive
az acr create --name <registry_name> --resource-group myResourceGroup --location "West US" --sku Basic
```

<span data-ttu-id="f109e-195">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="f109e-195">Output</span></span>
```json
{
  "adminUserEnabled": false,
  "creationDate": "2017-05-04T08:50:55.635688+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/<registry_name>",
  "location": "westus",
  "loginServer": "<registry_name>.azurecr.io",
  "name": "<registry_name>",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "<registry_name>01234"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

### <a name="retrieve-the-registry-credentials-for-pushing-and-pulling-docker-images"></a><span data-ttu-id="f109e-196">Получение учетных данных реестра для передачи и извлечения образов Docker</span><span class="sxs-lookup"><span data-stu-id="f109e-196">Retrieve the registry credentials for pushing and pulling Docker images</span></span>

<span data-ttu-id="f109e-197">Чтобы отобразить учетные данные реестра, сначала необходимо включить режим администратора.</span><span class="sxs-lookup"><span data-stu-id="f109e-197">To show registry credentials, enable admin mode first.</span></span>

```azurecli-interactive
az acr update --name <registry_name> --admin-enabled true
az acr credential show -n <registry_name>
```

<span data-ttu-id="f109e-198">Вы увидите два пароля.</span><span class="sxs-lookup"><span data-stu-id="f109e-198">You see two passwords.</span></span> <span data-ttu-id="f109e-199">Запишите имя пользователя и первый пароль.</span><span class="sxs-lookup"><span data-stu-id="f109e-199">Make note of the user name and the first password.</span></span>

```json
{
  "passwords": [
    {
      "name": "password",
      "value": "<registry_password>"
    },
    {
      "name": "password2",
      "value": "<registry_password2>"
    }
  ],
  "username": "<registry_name>"
}
```

### <a name="upload-your-docker-container-to-azure-container-registry"></a><span data-ttu-id="f109e-200">Передача контейнера Docker в реестр контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="f109e-200">Upload your Docker container to Azure Container Registry</span></span>

```bash
docker login <registry_name>.azurecr.io -u <registry_name> -p "<registry_password>"
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
```

## <a name="deploy-the-docker-python-flask-application-to-azure"></a><span data-ttu-id="f109e-201">Развертывание приложения Docker Python Flask в Azure</span><span class="sxs-lookup"><span data-stu-id="f109e-201">Deploy the Docker Python Flask application to Azure</span></span>

<span data-ttu-id="f109e-202">На этом шаге вы развернете приложение Docker Python Flask из контейнера Docker в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="f109e-202">In this step, you deploy your Docker container-based Python Flask application to Azure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="f109e-203">Создание плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="f109e-203">Create an App Service plan</span></span>

<span data-ttu-id="f109e-204">Создайте план службы приложений, выполнив команду [az appservice plan create](/cli/azure/appservice/plan#create).</span><span class="sxs-lookup"><span data-stu-id="f109e-204">Create an App Service plan with the [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="f109e-205">В следующем примере создается план службы приложений на основе Linux *myAppServicePlan* в ценовой категории S1:</span><span class="sxs-lookup"><span data-stu-id="f109e-205">The following example creates a Linux-based App Service plan named *myAppServicePlan* using the S1 pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku S1 --is-linux
```

<span data-ttu-id="f109e-206">После создания плана службы приложений в Azure CLI отображаются следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="f109e-206">When the App Service plan is created, the Azure CLI shows information similar to the following example:</span></span>

```json 
{
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "West US",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
  "kind": "linux",
  "location": "West US",
  "maximumNumberOfWorkers": 10,
  "name": "myAppServicePlan",
  "numberOfSites": 0,
  "perSiteScaling": false,
  "provisioningState": "Succeeded",
  "reserved": true,
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capabilities": null,
    "capacity": 1,
    "family": "S",
    "locations": null,
    "name": "S1",
    "size": "S1",
    "skuCapacity": null,
    "tier": "Standard"
  },
  "status": "Ready",
  "subscription": "00000000-0000-0000-0000-000000000000",
  "tags": null,
  "targetWorkerCount": 0,
  "targetWorkerSizeId": 0,
  "type": "Microsoft.Web/serverfarms",
  "workerTierName": null
}
``` 

### <a name="create-a-web-app"></a><span data-ttu-id="f109e-207">Создание веб-приложения</span><span class="sxs-lookup"><span data-stu-id="f109e-207">Create a web app</span></span>

<span data-ttu-id="f109e-208">Создайте веб-приложение в рамках плана *myAppServicePlan* службы приложений с помощью команды [az webapp create](/cli/azure/webapp#create).</span><span class="sxs-lookup"><span data-stu-id="f109e-208">Create a web app in the *myAppServicePlan* App Service plan with the [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="f109e-209">Веб-приложение предоставляет место для размещения и развертывания кода, а также URL-адрес для просмотра развернутого приложения.</span><span class="sxs-lookup"><span data-stu-id="f109e-209">The web app gives you a hosting space to deploy your code and provides a URL for you to view the deployed application.</span></span> <span data-ttu-id="f109e-210">Создайте веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="f109e-210">Use  to create the web app.</span></span> 

<span data-ttu-id="f109e-211">В следующей команде замените заполнитель *\<app_name>* уникальным именем приложения.</span><span class="sxs-lookup"><span data-stu-id="f109e-211">In the following command, replace the *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="f109e-212">Это имя используется в URL-адресе по умолчанию для веб-приложения, поэтому оно должно быть уникальным для всех приложений в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="f109e-212">This name is part of the default URL for the web app, so the name needs to be unique across all apps in Azure App Service.</span></span> 

```azurecli
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="f109e-213">После создания веб-приложения в Azure CLI отображаются следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="f109e-213">When the web app has been created, the Azure CLI shows information similar to the following example:</span></span> 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-the-database-environment-variables"></a><span data-ttu-id="f109e-214">Настройка переменных среды базы данных</span><span class="sxs-lookup"><span data-stu-id="f109e-214">Configure the database environment variables</span></span>

<span data-ttu-id="f109e-215">Ранее в этом руководстве вы определили переменные среды для подключения к базе данных PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="f109e-215">Earlier in the tutorial, you defined environment variables to connect to your PostgreSQL database.</span></span>

<span data-ttu-id="f109e-216">В службе приложений переменные среды устанавливаются как _параметры приложения_ с помощью команды [az webapp config appsettings set](/cli/azure/webapp/config#set).</span><span class="sxs-lookup"><span data-stu-id="f109e-216">In App Service, you set environment variables as _app settings_ by using the [az webapp config appsettings set](/cli/azure/webapp/config#set) command.</span></span> 

<span data-ttu-id="f109e-217">Код ниже указывает сведения о подключении к базе данных как параметры приложения.</span><span class="sxs-lookup"><span data-stu-id="f109e-217">The following example specifies the database connection details as app settings.</span></span> <span data-ttu-id="f109e-218">Кроме того, в нем определена переменная *PORT*, которая сопоставляет порт 5000 из контейнера Docker для получения трафика HTTP через порт 80.</span><span class="sxs-lookup"><span data-stu-id="f109e-218">It also uses the *PORT* variable to map PORT 5000 from your Docker Container to receive HTTP traffic on PORT 80.</span></span>

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBPASS="supersecretpass" DBNAME="eventregistration" PORT=5000
```

### <a name="configure-docker-container-deployment"></a><span data-ttu-id="f109e-219">Настройка развертывания контейнера Docker</span><span class="sxs-lookup"><span data-stu-id="f109e-219">Configure Docker container deployment</span></span> 

<span data-ttu-id="f109e-220">Служба приложений может автоматически скачать и запустить контейнер Docker.</span><span class="sxs-lookup"><span data-stu-id="f109e-220">AppService can automatically download and run a Docker container.</span></span>

```azurecli
az webapp config container set --resource-group myResourceGroup --name <app_name> --docker-registry-server-user "<registry_name>" --docker-registry-server-password "<registry_password>" --docker-custom-image-name "<registry_name>.azurecr.io/flask-postgresql-sample" --docker-registry-server-url "https://<registry_name>.azurecr.io"
```

<span data-ttu-id="f109e-221">При обновлении контейнера Docker или изменении параметров следует перезапустить приложение.</span><span class="sxs-lookup"><span data-stu-id="f109e-221">Whenever you update the Docker container or change the settings, restart the app.</span></span> <span data-ttu-id="f109e-222">Это позволяет применить все параметры и извлечь из реестра последний контейнер.</span><span class="sxs-lookup"><span data-stu-id="f109e-222">Restarting ensures that all settings are applied and the latest container is pulled from the registry.</span></span>

```azurecli-interactive
az webapp restart --resource-group myResourceGroup --name <app_name>
```

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="f109e-223">Переход к веб-приложению Azure</span><span class="sxs-lookup"><span data-stu-id="f109e-223">Browse to the Azure web app</span></span> 

<span data-ttu-id="f109e-224">Откройте развертываемое веб-приложение в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="f109e-224">Browse to the deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
```
> [!NOTE]
> <span data-ttu-id="f109e-225">Веб-приложению после внесения изменений в конфигурацию контейнера может потребоваться дополнительное время для скачивания и запуска контейнера.</span><span class="sxs-lookup"><span data-stu-id="f109e-225">The web app takes longer to load because the container has to be downloaded and started after the container configuration is changed.</span></span>

<span data-ttu-id="f109e-226">Вы увидите зарегистрированных ранее гостей, которые были сохранены в рабочей базе данных Azure на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="f109e-226">You see previously registered guests that were saved to the Azure production database in the previous step.</span></span>

![Приложение Python Flask из контейнера Docker, выполняемое в локальной среде](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-app-deployed.png)

<span data-ttu-id="f109e-228">**Поздравляем!**</span><span class="sxs-lookup"><span data-stu-id="f109e-228">**Congratulations!**</span></span> <span data-ttu-id="f109e-229">Вы запустили приложение Python Flask из контейнера Docker в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="f109e-229">You're running a Docker container-based Python Flask app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="f109e-230">Обновление модели данных и повторное развертывание</span><span class="sxs-lookup"><span data-stu-id="f109e-230">Update data model and redeploy</span></span>

<span data-ttu-id="f109e-231">На этом шаге вы добавите несколько участников для каждой регистрации событий, обновив модель гостя.</span><span class="sxs-lookup"><span data-stu-id="f109e-231">In this step, you add the number of attendees to each event registration by updating the Guest model.</span></span>

<span data-ttu-id="f109e-232">Получите для изменения выпуск *0.2-migration* с помощью следующей команды Git:</span><span class="sxs-lookup"><span data-stu-id="f109e-232">Check out the *0.2-migration* release with the following git command:</span></span>

```bash
git checkout tags/0.2-migration
```

<span data-ttu-id="f109e-233">В этом выпуске уже внесены необходимые изменения в представления, контроллеры и модель.</span><span class="sxs-lookup"><span data-stu-id="f109e-233">This release already made the necessary changes to views, controllers, and model.</span></span> <span data-ttu-id="f109e-234">Он также включает в себя перенос базы данных с использованием *Alembic* (`flask db migrate`).</span><span class="sxs-lookup"><span data-stu-id="f109e-234">It also includes a database migration generated via *alembic* (`flask db migrate`).</span></span> <span data-ttu-id="f109e-235">Все внесенные изменения можно просмотреть с помощью следующей команды Git:</span><span class="sxs-lookup"><span data-stu-id="f109e-235">You can see all changes made via the following git command:</span></span>

```bash
git diff 0.1-initialapp 0.2-migration
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="f109e-236">Проверьте изменения локально.</span><span class="sxs-lookup"><span data-stu-id="f109e-236">Test your changes locally</span></span>

<span data-ttu-id="f109e-237">Выполните приведенные ниже команды, чтобы проверить изменения в локальной среде, запустив сервер Flask.</span><span class="sxs-lookup"><span data-stu-id="f109e-237">Run the following commands to test your changes locally by running the flask server.</span></span>

<span data-ttu-id="f109e-238">MAC и Linux:</span><span class="sxs-lookup"><span data-stu-id="f109e-238">Mac / Linux:</span></span>
```bash
source venv/bin/activate
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="f109e-239">Перейдите по адресу http://127.0.0.1:5000 в браузере, чтобы просмотреть изменения.</span><span class="sxs-lookup"><span data-stu-id="f109e-239">Navigate to http://127.0.0.1:5000 in your browser to view the changes.</span></span> <span data-ttu-id="f109e-240">Создайте тестовую регистрацию.</span><span class="sxs-lookup"><span data-stu-id="f109e-240">Create a test registration.</span></span>

![Приложение Python Flask из контейнера Docker, выполняемое в локальной среде](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app-v2.png)

### <a name="publish-changes-to-azure"></a><span data-ttu-id="f109e-242">Публикация изменений в Azure</span><span class="sxs-lookup"><span data-stu-id="f109e-242">Publish changes to Azure</span></span>

<span data-ttu-id="f109e-243">Создайте образ Docker, отправьте его в реестр контейнеров и перезапустите приложение.</span><span class="sxs-lookup"><span data-stu-id="f109e-243">Build the new docker image, push it to the container registry, and restart the app.</span></span>

```bash
docker build -t flask-postgresql-sample .
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
az appservice web restart --resource-group myResourceGroup --name <app_name>
```

<span data-ttu-id="f109e-244">Перейдите в веб-приложение Azure и еще раз проверьте новые функции.</span><span class="sxs-lookup"><span data-stu-id="f109e-244">Navigate to your Azure web app and try out the new functionality again.</span></span> <span data-ttu-id="f109e-245">Создайте еще одну регистрацию событий.</span><span class="sxs-lookup"><span data-stu-id="f109e-245">Create another event registration.</span></span>

```bash 
http://<app_name>.azurewebsites.net 
```

![Приложение Docker Python Flask в службе приложений Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="f109e-247">Управление веб-приложением Azure</span><span class="sxs-lookup"><span data-stu-id="f109e-247">Manage your Azure web app</span></span>

<span data-ttu-id="f109e-248">Перейдите на [портал Azure](https://portal.azure.com), чтобы увидеть созданное веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="f109e-248">Go to the [Azure portal](https://portal.azure.com) to see the web app you created.</span></span>

<span data-ttu-id="f109e-249">В меню слева выберите **Службы приложений**, а затем щелкните имя своего веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="f109e-249">From the left menu, click **App Services**, then click the name of your Azure web app.</span></span>

![Переход к веб-приложению Azure на портале](./media/app-service-web-tutorial-docker-python-postgresql-app/app-resource.png)

<span data-ttu-id="f109e-251">По умолчанию на портале отображается страница **Обзор** веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="f109e-251">By default, the portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="f109e-252">Здесь вы можете наблюдать за работой приложения.</span><span class="sxs-lookup"><span data-stu-id="f109e-252">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="f109e-253">Вы также можете выполнять базовые задачи управления: обзор, завершение, запуск, перезагрузку и удаление.</span><span class="sxs-lookup"><span data-stu-id="f109e-253">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="f109e-254">На вкладках в левой части страницы отображаются различные страницы конфигурации, которые можно открыть.</span><span class="sxs-lookup"><span data-stu-id="f109e-254">The tabs on the left side of the page show the different configuration pages you can open.</span></span>

![Страница службы приложений на портале Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/app-mgmt.png)

## <a name="next-steps"></a><span data-ttu-id="f109e-256">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f109e-256">Next steps</span></span>

<span data-ttu-id="f109e-257">Перейдите к следующему руководству, чтобы научиться сопоставлять пользовательские DNS-имена с веб-приложением.</span><span class="sxs-lookup"><span data-stu-id="f109e-257">Advance to the next tutorial to learn how to map a custom DNS name to your web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="f109e-258">Сопоставление существующего настраиваемого DNS-имени с веб-приложениями Azure</span><span class="sxs-lookup"><span data-stu-id="f109e-258">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
