---
title: "aaaBuild Docker Python и PostgreSQL веб-приложения в Azure | Документы Microsoft"
description: "Узнайте, как tooget приложения Docker Python работают в Azure с tooa подключения PostgreSQL базы данных."
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
ms.openlocfilehash: e594ef9ec8c04ef2bf725e5f998691f3fb8cf815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-docker-python-and-postgresql-web-app-in-azure"></a><span data-ttu-id="1d7ab-103">Создание в Azure веб-приложения Docker Python с подключением к базе данных PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="1d7ab-103">Build a Docker Python and PostgreSQL web app in Azure</span></span>

<span data-ttu-id="1d7ab-104">Веб-приложения Azure — это служба веб-размещения с самостоятельной установкой исправлений и высоким уровнем масштабируемости.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="1d7ab-105">В этом учебнике показано, как toocreate основные Python Docker веб-приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-105">This tutorial shows how toocreate a basic Docker Python web app in Azure.</span></span> <span data-ttu-id="1d7ab-106">Эта база данных PostgreSQL tooa приложения будет подключиться.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-106">You'll connect this app tooa PostgreSQL database.</span></span> <span data-ttu-id="1d7ab-107">После выполнения всех действий у вас будет приложение Python Flask, работающее в контейнере Docker в [веб-приложениях службы приложений Azure](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1d7ab-107">When you're done, you'll have a Python Flask application running within a Docker container on [Azure App Service Web Apps](app-service-web-overview.md).</span></span>

![Приложение Docker Python Flask в службе приложений Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

<span data-ttu-id="1d7ab-109">Вы можете использовать описанные ниже шаги hello на macOS.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-109">You can follow hello steps below on macOS.</span></span> <span data-ttu-id="1d7ab-110">Инструкции для Linux и Windows являются одинаковыми hello в большинстве случаев, но не hello различия описаны в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-110">Linux and Windows instructions are hello same in most cases, but hello differences are not detailed in this tutorial.</span></span>
 
## <a name="prerequisites"></a><span data-ttu-id="1d7ab-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1d7ab-111">Prerequisites</span></span>

<span data-ttu-id="1d7ab-112">toocomplete этого учебника:</span><span class="sxs-lookup"><span data-stu-id="1d7ab-112">toocomplete this tutorial:</span></span>

1. <span data-ttu-id="1d7ab-113">[установите Git](https://git-scm.com/);</span><span class="sxs-lookup"><span data-stu-id="1d7ab-113">[Install Git](https://git-scm.com/)</span></span>
1. <span data-ttu-id="1d7ab-114">[установите Python](https://www.python.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="1d7ab-114">[Install Python](https://www.python.org/downloads/)</span></span>
1. <span data-ttu-id="1d7ab-115">[установите и запустите PostgreSQL](https://www.postgresql.org/download/);</span><span class="sxs-lookup"><span data-stu-id="1d7ab-115">[Install and run PostgreSQL](https://www.postgresql.org/download/)</span></span>
1. <span data-ttu-id="1d7ab-116">[установите Docker Community Edition](https://www.docker.com/community-edition).</span><span class="sxs-lookup"><span data-stu-id="1d7ab-116">[Install Docker Community Edition](https://www.docker.com/community-edition)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="1d7ab-117">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-117">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="1d7ab-118">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-118">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="1d7ab-119">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1d7ab-119">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-postgresql-installation-and-create-a-database"></a><span data-ttu-id="1d7ab-120">Проверка локальной установки PostgreSQL и создание базы данных</span><span class="sxs-lookup"><span data-stu-id="1d7ab-120">Test local PostgreSQL installation and create a database</span></span>

<span data-ttu-id="1d7ab-121">Откройте окно терминала hello и выполните `psql postgres` tooconnect tooyour локального сервера PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-121">Open hello terminal window and run `psql postgres` tooconnect tooyour local PostgreSQL server.</span></span>

```bash
psql postgres
```

<span data-ttu-id="1d7ab-122">Если подключение успешно установлено, это означает, что база данных PostgreSQL запущена.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-122">If your connection is successful, your PostgreSQL database is running.</span></span> <span data-ttu-id="1d7ab-123">В противном случае убедитесь, что локальной базы данных PostgresQL запущена с hello процедуры, описанной в [загружает - Core распространения PostgreSQL](https://www.postgresql.org/download/).</span><span class="sxs-lookup"><span data-stu-id="1d7ab-123">If not, make sure that your local PostgresQL database is started by following hello steps at [Downloads - PostgreSQL Core Distribution](https://www.postgresql.org/download/).</span></span>

<span data-ttu-id="1d7ab-124">Создайте базу данных *eventregistration* и настройте отдельного пользователя базы данных пользователя *manager* с паролем *supersecretpass*.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-124">Create a database called *eventregistration* and set up a separate database user named *manager* with password *supersecretpass*.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```
<span data-ttu-id="1d7ab-125">Тип *\q* tooexit hello PostgreSQL клиента.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-125">Type *\q* tooexit hello PostgreSQL client.</span></span> 

<a name="step2"></a>

## <a name="create-local-python-flask-application"></a><span data-ttu-id="1d7ab-126">Создание локального приложения Python Flask</span><span class="sxs-lookup"><span data-stu-id="1d7ab-126">Create local Python Flask application</span></span>

<span data-ttu-id="1d7ab-127">На этом шаге настраивается hello локального проекта термосе Python.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-127">In this step, you set up hello local Python Flask project.</span></span>

### <a name="clone-hello-sample-application"></a><span data-ttu-id="1d7ab-128">Пример приложения hello клонирования</span><span class="sxs-lookup"><span data-stu-id="1d7ab-128">Clone hello sample application</span></span>

<span data-ttu-id="1d7ab-129">Hello откройте окно терминала, и `CD` tooa рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-129">Open hello terminal window, and `CD` tooa working directory.</span></span>  

<span data-ttu-id="1d7ab-130">Выполнения hello следующими командами tooclone hello образец репозитория и go toohello *initialapp 0,1* выпуска.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-130">Run hello following commands tooclone hello sample repository and go toohello *0.1-initialapp* release.</span></span>

```bash
git clone https://github.com/Azure-Samples/docker-flask-postgres.git
cd docker-flask-postgres
git checkout tags/0.1-initialapp
```

<span data-ttu-id="1d7ab-131">Этот пример репозитория содержит приложение [Flask](http://flask.pocoo.org/).</span><span class="sxs-lookup"><span data-stu-id="1d7ab-131">This sample repository contains a [Flask](http://flask.pocoo.org/) application.</span></span> 

### <a name="run-hello-application"></a><span data-ttu-id="1d7ab-132">Запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="1d7ab-132">Run hello application</span></span>

> [!NOTE] 
> <span data-ttu-id="1d7ab-133">На более позднем этапе упрощают процесс путем построения toouse контейнера Docker с hello рабочей базы данных.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-133">In a later step you simplify this process by building a Docker container toouse with hello production database.</span></span>

<span data-ttu-id="1d7ab-134">Установка hello необходимые пакеты и запуск приложения hello.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-134">Install hello required packages and start hello application.</span></span>

```bash
pip install virtualenv
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="1d7ab-135">После полной загрузки приложение hello, вы увидите нечто похожее toohello следующие сообщения:</span><span class="sxs-lookup"><span data-stu-id="1d7ab-135">When hello app is fully loaded, you see something similar toohello following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

<span data-ttu-id="1d7ab-136">Перейдите toohttp://127.0.0.1:5000 в браузере.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-136">Navigate toohttp://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="1d7ab-137">Щелкните **Зарегистрировать**</span><span class="sxs-lookup"><span data-stu-id="1d7ab-137">Click **Register!**</span></span> <span data-ttu-id="1d7ab-138">и создайте тестового пользователя.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-138">and create a test user.</span></span>

![Приложение Python Flask, выполняемое в локальной среде](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

<span data-ttu-id="1d7ab-140">термосе пример приложения Hello хранятся данные пользователя в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-140">hello Flask sample application stores user data in hello database.</span></span> <span data-ttu-id="1d7ab-141">Если сбой регистрации пользователя, приложение производит запись данных toohello локальных данных PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-141">If you are successful at registering a user, your app is writing data toohello local PostgreSQL database.</span></span>

<span data-ttu-id="1d7ab-142">сервер термосе toostop hello в любое время, введите сочетание клавиш Ctrl + C в hello терминалов.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-142">toostop hello Flask server at anytime, type Ctrl+C in hello terminal.</span></span> 

## <a name="create-a-production-postgresql-database"></a><span data-ttu-id="1d7ab-143">Создание рабочей базы данных PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="1d7ab-143">Create a production PostgreSQL database</span></span>

<span data-ttu-id="1d7ab-144">На этом шаге вы создадите базу данных PostgreSQL в Azure.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-144">In this step, you create a PostgreSQL database in Azure.</span></span> <span data-ttu-id="1d7ab-145">Когда приложение будет развернутой tooAzure, он будет использовать эту базу данных в облаке.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-145">When your app is deployed tooAzure, it will use this cloud database.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="1d7ab-146">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="1d7ab-146">Log in tooAzure</span></span>

<span data-ttu-id="1d7ab-147">В этом случае будет toouse hello Azure CLI 2.0 toocreate hello ресурсы необходимости toohost Python приложения в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-147">You are now going toouse hello Azure CLI 2.0 toocreate hello resources needed toohost your Python application in Azure App Service.</span></span>  <span data-ttu-id="1d7ab-148">Войдите в подписку Azure совместно с hello tooyour [входа az](/cli/azure/#login) команды и выполните hello на экране инструкциям.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-148">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> 

```azurecli
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="1d7ab-149">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="1d7ab-149">Create a resource group</span></span>

<span data-ttu-id="1d7ab-150">Создание [группы ресурсов](../azure-resource-manager/resource-group-overview.md) с hello [Создание группы az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="1d7ab-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with hello [az group create](/cli/azure/group#create).</span></span> 

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="1d7ab-151">Hello следующий пример создает группу ресурсов в hello Запад США:</span><span class="sxs-lookup"><span data-stu-id="1d7ab-151">hello following example creates a resource group in hello West US region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West US"
```

<span data-ttu-id="1d7ab-152">Используйте hello [список расположений az appservice](/cli/azure/appservice#list-locations) Azure CLI команды toolist доступных расположений.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-152">Use hello [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command toolist available locations.</span></span>

### <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="1d7ab-153">Создание сервера базы данных Azure для PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="1d7ab-153">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="1d7ab-154">Создать сервер PostgreSQL с hello [az postgres server создать](/cli/azure/documentdb#create) команды.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-154">Create a PostgreSQL server with hello [az postgres server create](/cli/azure/documentdb#create) command.</span></span>

<span data-ttu-id="1d7ab-155">Hello следующую команду, подставьте уникальным именем сервера для hello  *\<postgresql_name >* заполнитель и имя пользователя для hello  *\<admin_username >* заполнителя .</span><span class="sxs-lookup"><span data-stu-id="1d7ab-155">In hello following command, substitute a unique server name for hello *\<postgresql_name>* placeholder and a user name for hello *\<admin_username>* placeholder.</span></span> <span data-ttu-id="1d7ab-156">Имя сервера Hello используется как часть конечной точки PostgreSQL (`https://<postgresql_name>.postgres.database.azure.com`), поэтому hello имя должно toobe уникальным для всех серверов в Azure.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-156">hello server name is used as part of your PostgreSQL endpoint (`https://<postgresql_name>.postgres.database.azure.com`), so hello name needs toobe unique across all servers in Azure.</span></span> <span data-ttu-id="1d7ab-157">имя пользователя Hello предназначен для учетной записи администратора базы данных начальной hello.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-157">hello user name is for hello initial database admin user account.</span></span> <span data-ttu-id="1d7ab-158">Все запрашиваемые toopick пароль для этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-158">You are prompted toopick a password for this user.</span></span>

```azurecli-interactive
az postgres server create --resource-group myResourceGroup --name <postgresql_name> --admin-user <admin_username>
```

<span data-ttu-id="1d7ab-159">При создании hello базы данных Azure для сервера PostgreSQL hello Azure CLI показано toohello аналогичные сведения, следующий пример:</span><span class="sxs-lookup"><span data-stu-id="1d7ab-159">When hello Azure Database for PostgreSQL server is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="create-a-firewall-rule-for-hello-azure-database-for-postgresql-server"></a><span data-ttu-id="1d7ab-160">Создание правила брандмауэра для hello базы данных Azure для сервера PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="1d7ab-160">Create a firewall rule for hello Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="1d7ab-161">Запустите hello следующих Azure CLI команда tooallow toohello базы данных со всех IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-161">Run hello following Azure CLI command tooallow access toohello database from all IP addresses.</span></span>

```azurecli-interactive
az postgres server firewall-rule create --resource-group myResourceGroup --server-name <postgresql_name> --start-ip-address=0.0.0.0 --end-ip-address=255.255.255.255 --name AllowAllIPs
```

<span data-ttu-id="1d7ab-162">Hello Azure CLI аналогичные toohello вывода следующий пример подтверждает hello создания правила брандмауэра:</span><span class="sxs-lookup"><span data-stu-id="1d7ab-162">hello Azure CLI confirms hello firewall rule creation with output similar toohello following example:</span></span>

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

## <a name="connect-your-python-flask-application-toohello-database"></a><span data-ttu-id="1d7ab-163">Подключение базы данных приложения toohello термосе Python</span><span class="sxs-lookup"><span data-stu-id="1d7ab-163">Connect your Python Flask application toohello database</span></span>

<span data-ttu-id="1d7ab-164">На этом шаге подключения вашей термосе Python образец приложения toohello базы данных Azure для созданный сервер PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-164">In this step, you connect your Python Flask sample application toohello Azure Database for PostgreSQL server you created.</span></span>

### <a name="create-an-empty-database-and-set-up-a-new-database-application-user"></a><span data-ttu-id="1d7ab-165">Создание пустой базы данных и настройка нового пользователя приложения базы данных</span><span class="sxs-lookup"><span data-stu-id="1d7ab-165">Create an empty database and set up a new database application user</span></span>

<span data-ttu-id="1d7ab-166">Создайте пользователя базы данных с tooa одной базы данных access только.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-166">Create a database user with access tooa single database only.</span></span> <span data-ttu-id="1d7ab-167">Вы будете использовать эти учетные данные tooavoid, предоставляя полный доступ toohello hello приложения сервера.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-167">You'll use these credentials tooavoid giving hello application full access toohello server.</span></span>

<span data-ttu-id="1d7ab-168">Подключение базы данных toohello (появится запрос пароля администратора).</span><span class="sxs-lookup"><span data-stu-id="1d7ab-168">Connect toohello database (you're prompted for your admin password).</span></span>

```bash
psql -h <postgresql_name>.postgres.database.azure.com -U <my_admin_username>@<postgresql_name> postgres
```

<span data-ttu-id="1d7ab-169">Создание базы данных hello и пользователя с hello PostgreSQL CLI.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-169">Create hello database and user from hello PostgreSQL CLI.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```

<span data-ttu-id="1d7ab-170">Тип *\q* tooexit hello PostgreSQL клиента.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-170">Type *\q* tooexit hello PostgreSQL client.</span></span>

### <a name="test-hello-application-locally-against-hello-azure-postgresql-database"></a><span data-ttu-id="1d7ab-171">Тестирование приложения hello локально для базы данных Azure PostgreSQL hello</span><span class="sxs-lookup"><span data-stu-id="1d7ab-171">Test hello application locally against hello Azure PostgreSQL database</span></span> 

<span data-ttu-id="1d7ab-172">Вернемся теперь toohello *приложения* папки hello клонированы репозитории Github, приложение hello термосе Python можно запустить, обновив hello переменные среды базы данных.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-172">Going back now toohello *app* folder of hello cloned Github repository, you can run hello Python Flask application by updating hello database environment variables.</span></span>

```bash
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="1d7ab-173">После полной загрузки приложение hello, вы увидите нечто похожее toohello следующие сообщения:</span><span class="sxs-lookup"><span data-stu-id="1d7ab-173">When hello app is fully loaded, you see something similar toohello following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

<span data-ttu-id="1d7ab-174">Перейдите toohttp://127.0.0.1:5000 в браузере.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-174">Navigate toohttp://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="1d7ab-175">Щелкните **Зарегистрировать**</span><span class="sxs-lookup"><span data-stu-id="1d7ab-175">Click **Register!**</span></span> <span data-ttu-id="1d7ab-176">и создайте тестовую регистрацию.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-176">and create a test registration.</span></span> <span data-ttu-id="1d7ab-177">Теперь вы пишете toohello базу данных в Azure.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-177">You are now writing data toohello database in Azure.</span></span>

![Приложение Python Flask, выполняемое в локальной среде](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

### <a name="running-hello-application-from-a-docker-container"></a><span data-ttu-id="1d7ab-179">Запуск приложения hello из контейнера Docker</span><span class="sxs-lookup"><span data-stu-id="1d7ab-179">Running hello application from a Docker Container</span></span>

<span data-ttu-id="1d7ab-180">Создать образ контейнера Docker hello.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-180">Build hello Docker container image.</span></span>

```bash
cd ..
docker build -t flask-postgresql-sample .
```

<span data-ttu-id="1d7ab-181">Docker отображает подтверждение hello контейнера успешно создана.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-181">Docker displays a confirmation that it successfully created hello container.</span></span>

```bash
Successfully built 7548f983a36b
```

<span data-ttu-id="1d7ab-182">Добавление переменной файла базы данных среды переменные tooan среды *db.env*.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-182">Add database environment variables tooan environment variable file *db.env*.</span></span> <span data-ttu-id="1d7ab-183">приложение Hello подключится к рабочей базе данных PostgreSQL toohello в Azure.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-183">hello app will connect toohello PostgreSQL production database in Azure.</span></span>

```text
DBHOST="<postgresql_name>.postgres.database.azure.com"
DBUSER="manager@<postgresql_name>"
DBNAME="eventregistration"
DBPASS="supersecretpass"
```

<span data-ttu-id="1d7ab-184">Запустите приложение hello из контейнера Docker hello.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-184">Run hello app from within hello Docker container.</span></span> <span data-ttu-id="1d7ab-185">Hello следующая команда указывает файл переменных среды hello и сопоставляет hello по умолчанию термосе 5000 toolocal порта 5000.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-185">hello following command specifies hello environment variable file and maps hello default Flask port 5000 toolocal port 5000.</span></span>

```bash
docker run -it --env-file db.env -p 5000:5000 flask-postgresql-sample
```

<span data-ttu-id="1d7ab-186">Hello выходные данные выглядят аналогично toowhat, который приводился выше.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-186">hello output is similar toowhat you saw earlier.</span></span> <span data-ttu-id="1d7ab-187">Однако hello миграции первоначальная база данных больше не требуется выполнять toobe и таким образом пропускается.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-187">However, hello initial database migration no longer needs toobe performed and therefore is skipped.</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
 * Serving Flask app "app"
 * Running on http://0.0.0.0:5000/ (Press CTRL+C tooquit)
```

<span data-ttu-id="1d7ab-188">Hello базы данных уже содержит регистрации hello, созданный ранее.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-188">hello database already contains hello registration you created previously.</span></span>

![Приложение Python Flask из контейнера Docker, выполняемое в локальной среде](./media/app-service-web-tutorial-docker-python-postgresql-app/local-docker.png)

## <a name="upload-hello-docker-container-tooa-container-registry"></a><span data-ttu-id="1d7ab-190">Отправка в реестре контейнеров tooa контейнера Docker hello</span><span class="sxs-lookup"><span data-stu-id="1d7ab-190">Upload hello Docker container tooa container registry</span></span>

<span data-ttu-id="1d7ab-191">На этом шаге необходимо отправить реестре контейнеров tooa контейнера Docker hello.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-191">In this step, you upload hello Docker container tooa container registry.</span></span> <span data-ttu-id="1d7ab-192">Вы будете использовать реестр контейнеров Azure, однако можно также использовать другие популярные реестры контейнеров, например Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-192">You'll use Azure Container Registry, but you could also use other popular ones such as Docker Hub.</span></span>

### <a name="create-an-azure-container-registry"></a><span data-ttu-id="1d7ab-193">Создание реестра контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="1d7ab-193">Create an Azure Container Registry</span></span>

<span data-ttu-id="1d7ab-194">Замените в hello, следующая команда toocreate реестре контейнеров  *\<registry_name >* с именем реестра уникальный контейнер Azure по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-194">In hello following command toocreate a container registry replace *\<registry_name>* with a unique Azure container registry name of your choice.</span></span>

```azurecli-interactive
az acr create --name <registry_name> --resource-group myResourceGroup --location "West US" --sku Basic
```

<span data-ttu-id="1d7ab-195">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="1d7ab-195">Output</span></span>
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

### <a name="retrieve-hello-registry-credentials-for-pushing-and-pulling-docker-images"></a><span data-ttu-id="1d7ab-196">Получить учетные данные реестра hello для принудительной отправки и извлекать образы Docker</span><span class="sxs-lookup"><span data-stu-id="1d7ab-196">Retrieve hello registry credentials for pushing and pulling Docker images</span></span>

<span data-ttu-id="1d7ab-197">tooshow учетные данные реестра, сначала включите режим администратора.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-197">tooshow registry credentials, enable admin mode first.</span></span>

```azurecli-interactive
az acr update --name <registry_name> --admin-enabled true
az acr credential show -n <registry_name>
```

<span data-ttu-id="1d7ab-198">Вы увидите два пароля.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-198">You see two passwords.</span></span> <span data-ttu-id="1d7ab-199">Запишите имя пользователя hello и hello первый пароль.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-199">Make note of hello user name and hello first password.</span></span>

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

### <a name="upload-your-docker-container-tooazure-container-registry"></a><span data-ttu-id="1d7ab-200">Отправьте ваш tooAzure контейнера Docker реестра контейнера</span><span class="sxs-lookup"><span data-stu-id="1d7ab-200">Upload your Docker container tooAzure Container Registry</span></span>

```bash
docker login <registry_name>.azurecr.io -u <registry_name> -p "<registry_password>"
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
```

## <a name="deploy-hello-docker-python-flask-application-tooazure"></a><span data-ttu-id="1d7ab-201">Развертывание tooAzure приложения hello термосе Python Docker</span><span class="sxs-lookup"><span data-stu-id="1d7ab-201">Deploy hello Docker Python Flask application tooAzure</span></span>

<span data-ttu-id="1d7ab-202">На этом шаге развертывания вашего Docker на основе контейнера термосе Python приложения tooAzure службы приложений.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-202">In this step, you deploy your Docker container-based Python Flask application tooAzure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="1d7ab-203">Создание плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="1d7ab-203">Create an App Service plan</span></span>

<span data-ttu-id="1d7ab-204">Создать план служб приложений с hello [создать план служб приложений az](/cli/azure/appservice/plan#create) команды.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-204">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="1d7ab-205">Hello следующий пример создает план службы приложений под управлением Linux, с именем *myAppServicePlan* hello S1 ценовой категории с помощью:</span><span class="sxs-lookup"><span data-stu-id="1d7ab-205">hello following example creates a Linux-based App Service plan named *myAppServicePlan* using hello S1 pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku S1 --is-linux
```

<span data-ttu-id="1d7ab-206">При создании плана служб приложений hello hello Azure CLI показано toohello аналогичные сведения, следующий пример:</span><span class="sxs-lookup"><span data-stu-id="1d7ab-206">When hello App Service plan is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="create-a-web-app"></a><span data-ttu-id="1d7ab-207">Создание веб-приложения</span><span class="sxs-lookup"><span data-stu-id="1d7ab-207">Create a web app</span></span>

<span data-ttu-id="1d7ab-208">Создание веб-приложения в hello *myAppServicePlan* план служб приложений с hello [создать веб-приложение az](/cli/azure/webapp#create) команды.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-208">Create a web app in hello *myAppServicePlan* App Service plan with hello [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="1d7ab-209">Предоставляет приложение Hello веб вы размещения пространство toodeploy кода и предоставляет URL-адрес для вас tooview hello развернутого приложения.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-209">hello web app gives you a hosting space toodeploy your code and provides a URL for you tooview hello deployed application.</span></span> <span data-ttu-id="1d7ab-210">Используйте toocreate hello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-210">Use  toocreate hello web app.</span></span> 

<span data-ttu-id="1d7ab-211">Hello следующую команду, замените hello  *\<имя_приложения >* заполнитель с именем уникальный приложения.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-211">In hello following command, replace hello *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="1d7ab-212">Это имя является частью URL-адреса для веб-приложения hello, по умолчанию hello, поэтому hello имя должно toobe уникальным для всех приложений в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-212">This name is part of hello default URL for hello web app, so hello name needs toobe unique across all apps in Azure App Service.</span></span> 

```azurecli
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="1d7ab-213">При создании веб-приложения hello hello Azure CLI показано toohello аналогичные сведения, следующий пример:</span><span class="sxs-lookup"><span data-stu-id="1d7ab-213">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span> 

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

### <a name="configure-hello-database-environment-variables"></a><span data-ttu-id="1d7ab-214">Настройка переменных среды hello базы данных</span><span class="sxs-lookup"><span data-stu-id="1d7ab-214">Configure hello database environment variables</span></span>

<span data-ttu-id="1d7ab-215">Ранее в учебнике hello определенные базы данных PostgreSQL tooyour tooconnect переменных среды.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-215">Earlier in hello tutorial, you defined environment variables tooconnect tooyour PostgreSQL database.</span></span>

<span data-ttu-id="1d7ab-216">В службе приложений устанавливаются переменные среды, как _параметры приложения_ с помощью hello [az webapp конфигурации appsettings набора](/cli/azure/webapp/config#set) команды.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-216">In App Service, you set environment variables as _app settings_ by using hello [az webapp config appsettings set](/cli/azure/webapp/config#set) command.</span></span> 

<span data-ttu-id="1d7ab-217">Hello пример указывает сведения о подключении базы данных hello как параметры приложения.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-217">hello following example specifies hello database connection details as app settings.</span></span> <span data-ttu-id="1d7ab-218">Она также использует hello *ПОРТ* переменной toomap PORT 5000 из контейнера Docker трафика tooreceive HTTP на ПОРТ 80.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-218">It also uses hello *PORT* variable toomap PORT 5000 from your Docker Container tooreceive HTTP traffic on PORT 80.</span></span>

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBPASS="supersecretpass" DBNAME="eventregistration" PORT=5000
```

### <a name="configure-docker-container-deployment"></a><span data-ttu-id="1d7ab-219">Настройка развертывания контейнера Docker</span><span class="sxs-lookup"><span data-stu-id="1d7ab-219">Configure Docker container deployment</span></span> 

<span data-ttu-id="1d7ab-220">Служба приложений может автоматически скачать и запустить контейнер Docker.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-220">AppService can automatically download and run a Docker container.</span></span>

```azurecli
az webapp config container set --resource-group myResourceGroup --name <app_name> --docker-registry-server-user "<registry_name>" --docker-registry-server-password "<registry_password>" --docker-custom-image-name "<registry_name>.azurecr.io/flask-postgresql-sample" --docker-registry-server-url "https://<registry_name>.azurecr.io"
```

<span data-ttu-id="1d7ab-221">При обновлении контейнера Docker hello или изменить параметры hello, перезапустите приложение hello.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-221">Whenever you update hello Docker container or change hello settings, restart hello app.</span></span> <span data-ttu-id="1d7ab-222">Перезапуск гарантирует, что все параметры будут применены и последнюю контейнера hello извлекается из реестра hello.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-222">Restarting ensures that all settings are applied and hello latest container is pulled from hello registry.</span></span>

```azurecli-interactive
az webapp restart --resource-group myResourceGroup --name <app_name>
```

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="1d7ab-223">Обзор toohello веб-приложение Azure</span><span class="sxs-lookup"><span data-stu-id="1d7ab-223">Browse toohello Azure web app</span></span> 

<span data-ttu-id="1d7ab-224">Обзор toohello развертывания веб-приложения с помощью веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-224">Browse toohello deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
```
> [!NOTE]
> <span data-ttu-id="1d7ab-225">Hello веб-приложения требует больше времени, tooload, так как hello контейнер содержит toobe загружается и запускается после изменения конфигурации контейнера hello.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-225">hello web app takes longer tooload because hello container has toobe downloaded and started after hello container configuration is changed.</span></span>

<span data-ttu-id="1d7ab-226">Вы увидите ранее зарегистрированного Гости, сохраненные в предыдущем шаге hello toohello Azure рабочей базы данных.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-226">You see previously registered guests that were saved toohello Azure production database in hello previous step.</span></span>

![Приложение Python Flask из контейнера Docker, выполняемое в локальной среде](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-app-deployed.png)

<span data-ttu-id="1d7ab-228">**Поздравляем!**</span><span class="sxs-lookup"><span data-stu-id="1d7ab-228">**Congratulations!**</span></span> <span data-ttu-id="1d7ab-229">Вы запустили приложение Python Flask из контейнера Docker в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-229">You're running a Docker container-based Python Flask app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="1d7ab-230">Обновление модели данных и повторное развертывание</span><span class="sxs-lookup"><span data-stu-id="1d7ab-230">Update data model and redeploy</span></span>

<span data-ttu-id="1d7ab-231">На этом шаге необходимо добавить номер hello регистрации событий tooeach участников, обновив hello гостевой модели.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-231">In this step, you add hello number of attendees tooeach event registration by updating hello Guest model.</span></span>

<span data-ttu-id="1d7ab-232">Извлечение hello *миграции 0,2* выпуска с hello следующую команду git:</span><span class="sxs-lookup"><span data-stu-id="1d7ab-232">Check out hello *0.2-migration* release with hello following git command:</span></span>

```bash
git checkout tags/0.2-migration
```

<span data-ttu-id="1d7ab-233">Этот выпуск уже внесены hello tooviews необходимые изменения, контроллеры и модели.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-233">This release already made hello necessary changes tooviews, controllers, and model.</span></span> <span data-ttu-id="1d7ab-234">Он также включает в себя перенос базы данных с использованием *Alembic* (`flask db migrate`).</span><span class="sxs-lookup"><span data-stu-id="1d7ab-234">It also includes a database migration generated via *alembic* (`flask db migrate`).</span></span> <span data-ttu-id="1d7ab-235">Можно просмотреть все изменения, сделанные посредством hello следующую команду git:</span><span class="sxs-lookup"><span data-stu-id="1d7ab-235">You can see all changes made via hello following git command:</span></span>

```bash
git diff 0.1-initialapp 0.2-migration
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="1d7ab-236">Проверьте изменения локально.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-236">Test your changes locally</span></span>

<span data-ttu-id="1d7ab-237">Запустите следующие команды tootest hello изменения локально, работающего сервера термосе hello.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-237">Run hello following commands tootest your changes locally by running hello flask server.</span></span>

<span data-ttu-id="1d7ab-238">MAC и Linux:</span><span class="sxs-lookup"><span data-stu-id="1d7ab-238">Mac / Linux:</span></span>
```bash
source venv/bin/activate
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="1d7ab-239">Перейдите toohttp://127.0.0.1:5000 изменения hello tooview браузера.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-239">Navigate toohttp://127.0.0.1:5000 in your browser tooview hello changes.</span></span> <span data-ttu-id="1d7ab-240">Создайте тестовую регистрацию.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-240">Create a test registration.</span></span>

![Приложение Python Flask из контейнера Docker, выполняемое в локальной среде](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app-v2.png)

### <a name="publish-changes-tooazure"></a><span data-ttu-id="1d7ab-242">Публикация изменений tooAzure</span><span class="sxs-lookup"><span data-stu-id="1d7ab-242">Publish changes tooAzure</span></span>

<span data-ttu-id="1d7ab-243">Создать новый образ docker hello, принудительно отправить его toohello контейнер реестра и перезапустите приложение hello.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-243">Build hello new docker image, push it toohello container registry, and restart hello app.</span></span>

```bash
docker build -t flask-postgresql-sample .
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
az appservice web restart --resource-group myResourceGroup --name <app_name>
```

<span data-ttu-id="1d7ab-244">Перейдите tooyour веб-приложение Azure и испытать новые функции hello.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-244">Navigate tooyour Azure web app and try out hello new functionality again.</span></span> <span data-ttu-id="1d7ab-245">Создайте еще одну регистрацию событий.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-245">Create another event registration.</span></span>

```bash 
http://<app_name>.azurewebsites.net 
```

![Приложение Docker Python Flask в службе приложений Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="1d7ab-247">Управление веб-приложением Azure</span><span class="sxs-lookup"><span data-stu-id="1d7ab-247">Manage your Azure web app</span></span>

<span data-ttu-id="1d7ab-248">Go toohello [портал Azure](https://portal.azure.com) toosee hello веб-приложения был создан.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-248">Go toohello [Azure portal](https://portal.azure.com) toosee hello web app you created.</span></span>

<span data-ttu-id="1d7ab-249">Hello в левом меню, щелкните **службы приложений**, затем щелкните имя hello Azure веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-249">From hello left menu, click **App Services**, then click hello name of your Azure web app.</span></span>

![Веб-приложения портала навигации tooAzure](./media/app-service-web-tutorial-docker-python-postgresql-app/app-resource.png)

<span data-ttu-id="1d7ab-251">По умолчанию hello портал отображает веб-приложения **Обзор** страницы.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-251">By default, hello portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="1d7ab-252">Здесь вы можете наблюдать за работой приложения.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-252">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="1d7ab-253">Вы также можете выполнять базовые задачи управления: обзор, завершение, запуск, перезагрузку и удаление.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-253">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="1d7ab-254">Hello вкладках hello левой части страницы приветствия отображаются страницы hello другой конфигурации, которые можно открыть.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-254">hello tabs on hello left side of hello page show hello different configuration pages you can open.</span></span>

![Страница службы приложений на портале Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/app-mgmt.png)

## <a name="next-steps"></a><span data-ttu-id="1d7ab-256">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1d7ab-256">Next steps</span></span>

<span data-ttu-id="1d7ab-257">Переместить следующий учебник toolearn toohello как toomap пользовательские DNS имя tooyour веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="1d7ab-257">Advance toohello next tutorial toolearn how toomap a custom DNS name tooyour web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="1d7ab-258">Сопоставьте существующий пользовательский DNS имя tooAzure веб-приложений</span><span class="sxs-lookup"><span data-stu-id="1d7ab-258">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
